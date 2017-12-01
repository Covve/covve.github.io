---
layout: post
title:  5 + 1 things to consider before starting with Azure Container Service
categories: Engineering
cover: /images/blog/2017-02-16-5plus1-things-to-consider-before-starting-with-acs/cover.png
author: mk
---
Managing a production environment consisting of numerous containerized microservices can pose quite a challenge. Coupling this with the requirement for rapid release cycles and just in time scaling, Azure Container Service (ACS) provides a very promising solution.

Having adopted ACS at Covve for our production Docker environment, and having learnt tons along the way, this is a run through of some of the main lessons and gotchas we’ve gathered along the way.
<!--more-->

### Setting the scene

In a microservices environment, each service will consist of many containers which are spawned and die dynamically inside physical hosts that scale out and in. In the meantime, for each service, the outside world must have a fixed endpoint always available to respond to a request. 

These are some of the challenges which ACS promises to deal with. It makes it simpler for an engineering team to create and manage containerized applications. It does so through leveraging the Docker format and offering a variety of famous tools such as [DC/OS][DC/OS], [Docker Swarm][Docker Swarm] and [Kubernetes][Kubernetes] for scheduling and orchestration.  

In Covve we adopted ACS along with DC/OS about a semester ago in order to deploy part of our solution. The first phase included the deployment of our stateless dockerized services. The second phase included the deployment of our stateful services and most specifically some of our databases (Redis, Cassandra, Elasticsearch).  Phase one is already in production and phase two is on its way. Based on this experience, here are 5 + 1 things to keep in mind before starting with Azure Container Service.


### Lesson 1: Do not be afraid of the ACS JSON template. Use it from the beginning!

The entire JSON that describes an ACS and its components can be exported from an already existing ACS deployment or be [found on GitHub][found on GitHub]. While a first look at it can be quite intimidating -since its size can be a few thousand lines- my first advice is to invest as much time as it’s needed in order to thoroughly understand it. 

- Deploying an ACS from the Azure UI greatly limits the capability to fully parametrize your environment since it does not expose most of the available configuration options. However, all of them are available through the template. For example, you may want to change the IPs of your master nodes of the deployed cluster in order to solve a possible IP clash when trying to peer your ACS VNet with an already existing one.
- Understanding the template and its outcomes will allow you to optimize the produced environment, get rid of components that you may not need, and avoid possible extra charges.
- Having the JSON file of the ACS enables proper source control and versioning of the deployment. Treat it exactly as you treat your code.

![ACS template](/images/blog/2017-02-16-5plus1-things-to-consider-before-starting-with-acs/template.png)

*Go to the ACS resource group deployment, Automation script and Download the template.*


### Lesson 2: It’s something between PaaS and IaaS – What happens with software updates?

When you deploy an ACS you actually deploy a set of resources along with some preconfigured software for scheduling, orchestration, containerization etc. Once ACS is deployed, releasing your first dockerized service can happen immediately. In this respect, ACS behaves like a typical PaaS setup (which nowadays is transformed to Containers as a Service - CaaS). 

However, updating the various software components is not provided by Azure (which is actually IaaS-like behavior). This means that updating your DC/OS and all of its components in a production cluster while ensuring no downtime is practically impossible. An update like this can only happen through deploying a brand new ACS with the new versions preinstalled. After that, you should redeploy all your services. Do not worry though, since deploying fast and uniformly your services is one of the most important promises of the containerized world!


### Lesson 3: Choose your agents wisely

In all of the available orchestration configurations that ACS offers (Docker Swarm, DC/OS, Kubernetes), your services will run in a cluster of VMs (actually virtual machines scale sets - [VMSS][VMSS]) that are called agents. Each service instance reserves some resources on the agent that it’s deployed on. If all agents are of a single size, this may lead to situations where all the CPU of a VM is fully allocated but most of its memory is free (or vice versa). 

Break your services down to CPU-intensive and memory-intensive services and deploy various VMSS with different size of VMs in each one (keep in mind that in each VMSS all VMs must be of the same size). Deploy each service in the corresponding pool. Thus, you can achieve optimum allocation of your resources. 

Keep in mind that the ACS deployment UI in the Azure portal does not allow such an opportunity. Lesson 1 FTW! 

![agents](/images/blog/2017-02-16-5plus1-things-to-consider-before-starting-with-acs/agents.png)

*DC/OS agents with mostly CPU intensive services. Memory is mostly unallocated.*


### Lesson 4: Think twice if you are about to deploy a stateful app

At the time of writing, the implementation of the VMSS does not allow the attachment of external hard disks on the VMs. That is to say, if you want to deploy a database on a virtual machine you’ll have to depend on the VM’s disks for persisting your data. This is not a good practice when it comes to Azure VMs since the [non-OS disks are temporary][non-OS disks are temporary].

It is worth saying that we have communicated with the Azure support team on this issue and we have been informed that attaching external hard disks to VMs in a VMSS is a feature that is about to be released in preview soon.

Another reason to be careful when deploying a stateful app is that as of Marathon 1.3.10, persistent storage functionality [is still in beta version][is still in beta version]. Generally speaking, the containerized world is perfect for stateless apps while stateful apps are not its first class citizens yet.


### Lesson 5: Growing support by the community, but still there is a lot to be done

[Microsoft’s documentation][Microsoft’s documentation] is rich in most of its products and ACS is not an exception. However, nowadays the real power comes from the community. It’s true that ACS’s support by the community is not optimum with just a few tens of questions on Stackoverflow and generally limited resources available. This may be normal for a new product but it’s still something to consider.


### Lesson 5+1: DC/OS specific

This lesson comes from our experience on DC/OS and its components. Investing in such a technology was a normal-risk and high-profit decision to take. Some months after this decision and while our services are live in this environment here are only two of the most important outcomes that I would like to share.

Firstly, DC/OS stands for Data Center Operating System. Are you sure that you need such a capability, i.e a Data Center? Are you in this level of scaling? Are you about to reach it, or is this a possible requirement in a distant future? Investing in a technology that is built for a Data Center scale may not be the best match for simpler scenarios with limited size clusters. The additional system complexity may be an overkill or the costs may get out of budget. 

For example, you deploy an ACS with DC/OS with three master nodes of D2V2 size. They cost about 300$ per month. The master nodes hold the DC/OS and manage the agents’ cluster. No services can be deployed in the masters. If you deploy three D2V2 agents where your services will live then you’ll have a “supportive” infrastructure (masters) of a similar cost to the actual “productive” infrastructure. Your infrastructure needs to keep this ratio reasonable.

![Are you running a DC](/images/blog/2017-02-16-5plus1-things-to-consider-before-starting-with-acs/datacentre.png)

Secondly, many of the Mesos frameworks (Redis, Elasticsearch etc) are in alpha or beta phases at the time of writting. Even if the promise to have an Elasticsearch cluster “as-a-service” seems really appealing and a great reason to adopt DC/OS, in my opinion it would not be wise to use it at this point in time in a production environment.

### Conclusion

To sum up, Azure Container Service is a great PaaS solution which abstracts the installation and configuration of the orchestration and scheduling tools that are necessary for a large scale production cluster. Through leveraging the Docker format the compatibility and consensus with the community is great and keeps up with the hottest trends in devops. Of course, there are quite a few issues to resolve but it’s just normal for a product/collection-of-products that is still young and under development. 

[found on GitHub]: https://github.com/Azure/azure-quickstart-templates
[VMSS]: https://docs.microsoft.com/en-us/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-overview
[Microsoft’s documentation]: https://docs.microsoft.com/en-us/azure/container-service/
[is still in beta version]: https://mesosphere.github.io/marathon/docs/persistent-volumes.html
[non-OS disks are temporary]: https://docs.microsoft.com/azure/virtual-machines/linux/about-disks-and-vhds
[DC/OS]: https://dcos.io
[Docker Swarm]: https://www.docker.com/get-docker
[Kubernetes]: https://kubernetes.io