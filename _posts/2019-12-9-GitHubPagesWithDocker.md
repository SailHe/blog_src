---
layout: post
title:  "Github Pages with docker"
image: ''
date:   2018-12-9 17:22:31
tags:
- docker
description: 'template for blog'
categories:
- Learning
---

<p class="music-read">
	<a href="spotify:track:0npodwOWWkfh83yfGK5ZOW">Lost in paradise</a>
</p>

<figure class="foto-legenda">
	<figcaption>
		<p>现象</p>
	</figcaption>
	<img src="{{ "/assets/img/sharding/err/Docker_err_1_begin.PNG"}}" width='50%' height='100%' alt="万恶之源">
</figure>

<figure class="foto-legenda">
	<figcaption>
		<p>查询</p>
	</figcaption>
	<img src="{{ "/assets/img/sharding/err/Docker_err_1_query.PNG"}}" width='50%' height='100%' alt="大海捞针">
</figure>

<figure class="foto-legenda">
	<figcaption>
		<p>结果</p>
	</figcaption>
	<img src="{{ "/assets/img/sharding/err/Docker_err_1_result.PNG"}}" width='50%' height='100%' alt="针">
</figure>

<figure class="foto-legenda">
	<figcaption>
		<p>搞定</p>
	</figcaption>
	<img src="{{ "/assets/img/sharding/err/Docker_err_1_end.PNG"}}" width='50%' height='100%' alt="结束即是开始">
</figure>

## Google Keywords

Bundler::HTTPError Could not fetch specs from https://gems.ruby-china.org/
替换 Docker Ruby 源

### 引用链接列表

1. <a href="https://gist.github.com/SailHe/498aa5fbccb261a3e074a76296fb41d8" target="_blank">Gist</a>
2. <a href="https://github.com/sailhe" target="_blank">HomePage</a>
3. <a href="https://help.github.com/articles/customizing-css-and-html-in-your-jekyll-theme/" target="_blank">在Jekyll主题中自定义CSS和HTML</a>

## Build an image from a Dockerfile

{% highlight javascript %}

docker build -t jekyll-local .

{% endhighlight %}
