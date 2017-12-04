---
layout: post
title:  Uploading Block Blobs larger than 256 MB in Azure
categories: Engineering
cover: /images/blog/2017-02-20-Uploading-Block-Blobs-larger-than-256-Mb-in-Azure/blob.png
author: mk
redirect_from: "/Uploading-Block-Blobs-larger-than-256-Mb-in-Azure/"
---
The Azure Blob service stores text and binary data as blobs in the cloud. Data can be uploaded using the [Blob service REST API][Blob service REST API]. In Covve we use this service in order to upload various binary files such as database backups etc. We use the block blobs type since they are optimum for streaming and we do not need append (append blocks) or arbitrary read/write operations (page blobs). Check [this Microsoft post][this Microsoft post] for a thorough description of these three kinds of blobs.
<!--more-->

Block blobs are composed of blocks, each of which is identified by a block Id. Uploading a block is one operation and merging a set of blocks in order to form a blob is another. Each block can be up to 100 MB (4 MB for requests using REST versions before 2016-05-31), and a block blob can include up to 50,000 blocks. 

Uploading a block blob that is no more than 256 MB (64 MB for requests using REST versions before 2016-05-31) can be a single write operation using [Put Blob][Put Blob]. However, uploading a larger blob requires some more effort. Break it down in blocks of max 4 or 100MB depending on the REST API version that you use. Post each block separately to the [Put Block][Put Block] endpoint  and then post the list of the block ids to the [Put Block List][Put Block List] endpoint. Only then, the independent blocks will be merged to one blob. More details can be found in this [great post][great post]. Here, we’ll present a sample C# code which implements this procedure.

~~~
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using System.Net.Http;
using System.Text;
using System.Threading.Tasks;
using System.Xml.Linq;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;

namespace azure.common
{
    public class AzureBlobUploader : IBlobUploader
    {
        public async Task UploadAsync() {
            const int storageSharedAccessWriteExpiryInMinutes = 5;
            const string storageAccountConnectionString = "storageConnection-String";
            const string storageAccountContainer = "containerWhereToUpload";
            const string blobFilename = "filenameOfBlob";
            var utcNow = DateTime.UtcNow;

            var sasConstraints = new SharedAccessBlobPolicy {
                SharedAccessStartTime = utcNow.AddMinutes(-10),//you may not have exactly the same time as the azure server that receives the request 
                SharedAccessExpiryTime = utcNow.AddMinutes(storageSharedAccessWriteExpiryInMinutes),
                Permissions = SharedAccessBlobPermissions.Write
            };
            var storageAccount = CloudStorageAccount.Parse(storageAccountConnectionString);
            var blobClient = storageAccount.CreateCloudBlobClient();

            var blobContainer = blobClient.GetContainerReference(storageAccountContainer);
            blobContainer.CreateIfNotExists();

            var pathInsideContainer = $"{blobFilename.Substring(0, 2)}/{blobFilename}";
            var blob = blobContainer.GetBlockBlobReference(pathInsideContainer);

            var sasBlobToken = blob.GetSharedAccessSignature(sasConstraints);
            var sasUri = blob.Uri + sasBlobToken;
	    
	    var file = File.ReadAllBytes(@"C:\PathToFile\FileToUpload");
	    const int pageSizeInBytes = 104857600; //100MB for requests using REST versions after 2016-05-31
	    //const int pageSizeInBytes = 4096; //4MB for requests using REST versions before 2016-05-31
            var prevLastByte = 0;
            var bytesRemain = file.Length;
            var blockIds = new List<string>();
            do {                
                var bytesToCopy = Math.Min(bytesRemain, pageSizeInBytes);
                var bytesToSend = new byte[bytesToCopy];
                Array.Copy(file, prevLastByte, bytesToSend, 0, bytesToCopy);
                prevLastByte += bytesToCopy;
                bytesRemain -= bytesToCopy;

                //create blockId
                var blockId = Guid.NewGuid().ToString();
                var base64BlockId = Convert.ToBase64String(Encoding.UTF8.GetBytes(blockId));
                blockIds.Add(base64BlockId);

                //final uri
                var uri = $"{sasUri}&comp=block&blockid={base64BlockId}";

                //post block
                using (var client = new HttpClient()) {
                    var request = new HttpRequestMessage(HttpMethod.Put, uri);
	            	request.Headers.Add("x-ms-version", "2016-05-31"); //for requests using REST versions after 2016-05-31
	           	//request.Headers.Add("x-ms-version", "2015-04-05"); //for requests using REST versions before 2016-05-31
                    request.Content = new ByteArrayContent(bytesToSend);
                    await client.SendAsync(request);
                }
            } while (bytesRemain > 0);

            //post blocklist
            var blocklistUri = $"{sasUri}&comp=blocklist";
            var xmlBlockIds = new XElement("BlockList", blockIds.Select(id => new XElement("Latest", id)));
            using (var client = new HttpClient()) {
                var request = new HttpRequestMessage(HttpMethod.Put, blocklistUri);
			request.Headers.Add("x-ms-version", "2016-05-31"); //for requests using REST versions after 2016-05-31
			//request.Headers.Add("x-ms-version", "2015-04-05"); //for requests using REST versions before 2016-05-31
                request.Content = new StringContent(xmlBlockIds.ToString(), Encoding.UTF8, "application/xml");
                await client.SendAsync(request);
            }
        }
    }
}
~~~

This is all you need to upload a large block blob in Azure. You can boost this code in production with extra configuration or parallel asynchronous http calls for better performance but you get the idea. Hope that our experience has come in hand and saved you some time.

[Blob service REST API]: https://docs.microsoft.com/rest/api/storageservices/blob-service-rest-api
[this Microsoft post]: https://docs.microsoft.com/rest/api/storageservices/understanding-block-blobs--append-blobs--and-page-blobs
[Put Blob]: https://docs.microsoft.com/rest/api/storageservices/put-blob
[Put Block]: https://docs.microsoft.com/rest/api/storageservices/put-block
[Put Block List]: https://docs.microsoft.com/rest/api/storageservices/put-block-list
[great post]: https://docs.microsoft.com/rest/api/storageservices/understanding-block-blobs--append-blobs--and-page-blobs
