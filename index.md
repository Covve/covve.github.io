---
layout: default
---
{% for post in site.posts limit: 100 %}
  {% assign author = site[post.author] %}
  <section>
    <h2 class="heading"><a href="{{ post.url }}" class="no-link-styling">{{ post.title }}</a></h2>
    <p class="padding--bottom-one-space  border-bottom">
      {% if author %}<a href="{{ author.link }}" target="_blank" rel="nofollow">{{ author.name }}</a>{% endif %} <span class="text--grey">in</span> <a href="{{ site.url }}/categories/#{{ post.categories | first }}">{{ post.categories | first | capitalize}}</a> <span class="text--grey">on</span> {{ post.date | date: '%d %b' }}.
    </p>
    <article>
      {% if post.cover %}
        <p><a href="{{ post.url }}"><img src="{{ post.cover }}" alt="{{ post.title}}" width="800" /></a></p>
      {% endif %}
      <p>{{ post.content | split:'<!--more-->' | first | strip_html }}</p>
      <p class="text--smaller"><a href="{{ post.url }}">Read more &rarr;</a></p>
    </article>
  </section>
{% endfor %}