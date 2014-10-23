---
layout: post
published: true
title: Featured Posts in Jekyll
mathjax: false
featured: false
comments: true
chart: false
description: Grabbing Attention to your most beloved articles
categories: 
  - webdevelopment
tags: jekyll featured
---

If you are an avid blogger, there must be some writings that you value dearly and you might want your blog visitors to notice those posts in the blog index. The simplest way to achieve this attention to a few great posts is to feature those posts with visible markers and indexing those in a special page.

I do it simply by putting a statement in the post matter YAML.

{% highlight yaml %}
featured: true
{% endhighlight %}

Then I use the post.featured YAML statement to append visible markers to the featured posts in the blog index. You can do this a variety of ways depending on your theme CSS.
For me, I simply put a if command in the site.posts loop to find out the featured posts.

{% highlight ruby %}
{% raw %}
{% for post in paginator.posts %}
	{{ post.title }} {% if post.featured %}Put Some Marker{% endif %}
  	{{ post.excerpt }}
{% endfor %}
{% endraw %}
{% endhighlight %}

The most important part of the process is to index the featured posts in a different page. This allows the posts which have been featured to never fall into oblivion and ensures that these posts will always be in the spotlight. I index my blog's featured posts in a page called featured and provide a hard-link for it in the blog's header menu.
Populating the featured page index is horribly easy. Just include these codes in the featured page.

{% highlight ruby %}
{% raw %}
{% for post in site.posts %}
	{% if post.featured %}
		{{ post.title }} Put some Marker
    	{{ post.excerpt }}
  {% endif %}
{% endfor %}
{% endraw %}
{% endhighlight %}

I like to have a fallback option in case you have not featured any posts yet. In that case, the featured page will sit empty with no content. To fix that problem, I like to announce that "No posts has been featured yet".

{% highlight ruby %}
{% raw %}
{% assign featuredcount = '0' %}
{% for post in site.posts %}
  {% if post.featured %}
  {% assign featuredcount = featuredcount | plus:'1' %}
		{{ post.title }} Put some Marker
        {{ post.excerpt }}
  {% endif %}
{% endfor %}

{% if featuredcount == '0' %}
	<h1>No posts has been featured yet</h1>
{% endif %}
{% endraw %}
{% endhighlight %}

## **Requests?**

If you have some specific requests for this feature, or if you need help custom coding, message me on Twitter [@hmfaysal](http://twitter.com/hmfaysal) or email me at [hmfaysal@alum.mit.edu](mailto:hmfaysal@alum.mit.edu)

If you'd like to give me credit somewhere on your blog or tweet a shout out to [@hmfaysal](https://twitter.com/hmfaysal), that would be pretty sweet.