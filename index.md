---
layout: default
title: Everything on Information Security
tagline: Personal Blog
---
{% include JB/setup %}

<div class="posts">
  <div class="span14">  
  {% for post in site.posts %}
  
  <div style="float: left">
    <h2>
      {{ post.title }}
    </h2>
  </div>
  <div style="float:right">
    <h3>
      {{ post.date | date_to_string }}
    </h3>
  </div>
  <div style="clear: both"></div>

  <div style="display: inline">
      
      {{ post.content | truncatehtml: 500 }}
        
        <a href="{{ post.url }}" style="float: left;">Read more</a>
      <p style="float: right">
        <a href='{{post.url}}#disqus_thread'>Comments</a>
      </p>
  </div> <hr/><br/>
  {% endfor %}
  </div>
</div>


## Latest Posts

<ul class="posts">
  {% for post in site.posts limit: 5 %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>



