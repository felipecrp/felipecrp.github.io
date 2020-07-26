---
layout: page
title: Posts
permalink: /posts/
---

{% for post in site.posts %}
<h1>
    <a href="{{ post.url }}">{{post.title}}</a>
</h1>
<div class="date">
    on {{post.date | date_to_long_string}}
</div>
<p>
    {{post.excerpt}}
</p>

<p><a href="{{ post.url }}">Continue reading ...</a></p>

{% endfor %}
