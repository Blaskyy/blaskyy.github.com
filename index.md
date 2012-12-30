---
layout: page
tagline: Goodbye Yesterday and Hello Tomorrow!
---
{% include JB/setup %}
<div class="row">
  <div class="span8">
    <h2>最新文章</h2><hr class="index" />
    {% for post in site.posts limit: 1 %}
    <h3><a href="{{ post.url }}">{{ post.title }}</a></h3>
    <div class="list"><time>{{ post.date | date:"%Y年%m月%d日" }}</time></div>
    <p>{{ post.content}} <a href="{{ post.url }}">查看评论</a></p>
    {% endfor %}
    <hr class="index" />
    <h2>以往文章</h2><br />
    <ul>
      {% for post in site.posts limit: 5 offset: 1 %}
      <li class="list">
        <time>{{ post.date | date:"%Y年%m月%d日" }}</time> <a href="{{ post.url }}">{{ post.title }}</a>
      </li>
      {% endfor %}
    </ul>
    <a class="btn" href="/archive.html">更多文章</a>
  </div>

  <div class="span4">

    <ul class="nav nav-list">
      <li class="nav-header">Latest</li>
      {% for post in site.posts limit: 8 %}
      <li class="list">
        <a href="{{ post.url }}" title="{{ post.title }}">{{ post.title }}</a>
      </li>
      {% endfor %}

      <li class="nav-header">Categories</li>
      {% assign categories_list = site.categories %}
      {% include JB/categories_list %}

      <li class="nav-header">Tags</li>
      {% assign tags_list = site.tags %}
      {% if tags_list.first[0] == null %}
        {% for tag in tags_list %}
          <li class="index_tags"><a href="{{ BASE_PATH }}{{ site.JB.tags_path }}#{{ tag }}-ref">{{ tag }} <span>{{ site.tags[tag].size }}</span></a></li>
        {% endfor %}
      {% else %}
        {% for tag in tags_list %}
          <li class="index_tags"><a href="{{ BASE_PATH }}{{ site.JB.tags_path }}#{{ tag[0] }}-ref">{{ tag[0] }} <span>{{ tag[1].size }}</span></a></li>
        {% endfor %}
      {% endif %}
      {% assign tags_list = nil %}
      <li class="clear"></li>

      <li class="nav-header">Links</li>
      <li><a href="https://github.com/blaskyy">➤ My Github</a></li>
      <li><a href="http://kshift.me/">➤ Kshift.lv's Blog</a></li>
      <li><a href="http://fxck.it/">➤ Alsotang's Blog</a></li>
    </ul>

  </div>
</div>