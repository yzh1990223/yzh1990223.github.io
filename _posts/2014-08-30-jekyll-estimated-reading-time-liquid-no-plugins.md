---
layout: post
published: true
title: "Jekyll Estimated Reading Time: Liquid, no plugins"
mathjax: false
featured: false
comments: true
chart: false
description: Implementing Medium inspired Estimated Reading Time (ERT) Calculator on Github Pages with Jekyll
categories: 
  - webdevelopment
tags: jekyll reading time
---

The first time I discovered Medium, I fell in love with its **Estimated Reading Time (ERT)** feature. It helps bring in the right audience to the right article. The idea behind of this is, maybe it’s early in the morning, you’re in the mood of reading something terse while you get prepared for work, and at dawn, you’re back at home and you just want to curl up on the couch and gorge in a long essay. The ERT helps you find the right article, for the right time.

![Medium ERT]({{ site.url }}/images/post/medium-readingtime.jpg "Medium Estimated Reading Time")

So with that in mind, I looked for a solution to integrate this feature in my site. Soon enough, I found a Jekyll plugin that does it right. Have a look at this [Jekyll Estimated Reading Times Plugin](http://51bits.com/writing/estimated-reading-times-in-jekyll/) by 51bits. But the problem was, I was and currently am hosting with **GitHub pages**, which does not allow external plugins. So I decided write my own code in **Liquid** and I will share it in this post.

To make the code easier to understand I will provide step-by-step breakdown of the code.

### Understanding the code

First of all, lets make a switch for the **Estimated Reading Time (ERT)** feature, so that you can turn it on/off anytime you like. Put these two lines in your `_config.yml` file.

{% highlight yaml %}
# Read Time is a calculator to provide post Estimated Reading Time (ERT) based on word count. Usage is recommended.
readtime:		true
wpm:			200
{% endhighlight %}

`readtime` acts as a switch to turn on/off the **ERT** feature sitewide. `wpm` is used for specifying the *average words-per-minute* your viewers can read.

Then the calculator for the blog index page:

{% highlight ruby %}
{% raw %}
  {% if site.readtime %}
  {% for post in site.posts %}
  	{% assign readtime = post.content | strip_html | number_of_words | append: '.0' | divided_by:site.wpm %}
  {% endfor %}
{% endif %}
{% endraw %}
{% endhighlight %}

Without `append: '.0'`, you will get a whole number, but it will not be rounded. So 4.8 will be 4, not 5. **Liquid** provides math operators which can round numbers, but with the update of Jekyll version 2.2.0, those operators has been deprecated in favor of more elegant *data-type* based calculations.

The calculator does not display anything on your page, it just calculates the reading times for each post in your blog and holds it in the RAM. Place the code anywhere before you call `{% raw %}{{ readtime }}{% endraw %}` in the page to actually display the calculated results.

But before displaying the data lets make the code better. Lets give the calculator a fallback option if you did not specify or forgot to specify a wpm value in the `_config.yml` file. I opt to use **180 wpm** as the default fallback option. But you can use whatever you like.

{% highlight ruby %}
{% raw %}
{% if site.readtime %}
  {% for post in site.posts %}
    {% if site.wpm %}
      {% assign readtime = post.content | strip_html | number_of_words | append: '.0' | divided_by:site.wpm %}
    {% else %}
      {% assign readtime = post.content | strip_html | number_of_words | append: '.0' | divided_by:180 %}
    {% endif %}
  {% endfor %}
{% endif %}
{% endraw %}
{% endhighlight %}

### Displaying the ERT

Now we come to the main part, displaying the **Estimated Reading Time (ERT)** for each post.

Simply putting the `{% raw %}{{ readtime }}{% endraw %} minute` tag will display a floating point value.

{% assign readtime = page.content | strip_html | number_of_words | append: '.0' | divided_by:site.wpm %}
Like this, for this post `{% raw %}{{ readtime }}{% endraw %} minute` will display `{{ readtime }} minute`

But I am sure you are more interested in integer values for aesthetic and ease of reading purposes. With the **Jekyll 2.2.0** update, Jekyll supports a wide array of important data types like `int` and `float` and does not support many of the older liquid math operators that would have made doing this much easier, which is good in a sense. Prior to Jekyll version 2.2.0, the `divided_by` operator would return a rounded integer. It means calculations in Jekyll are more precise with this update. Anyways, to display the rounded number, there is a JavaScript snippet written by [Josh Bassett](https://twitter.com/nullobject). Just put it in the site's footer.

{% highlight javascript %}
{% raw %}
<script type='text/javascript'>
  $(document).ready(function() {
    $(".time").text(function (index, value) {
      return Math.round(parseFloat(value));
    });
  });
</script>
{% endraw %}
{% endhighlight %}

Now any floating point enclosed by the `<span class="time">12.3334455</span>` will be rounded by the JavaScript snippet, in this case it will simply display 12.

Now that the JavaScript is in place, you can now display the calculated and rounded Estimated Reading time to the reader. Lets make things interesting. Lets make the ***User eXperience(UX)*** better by handling the pluralization of the word *"minute"* if its greater than 1. We will be focusing on three different scenarios. 

1. If the calculated reading time is less than 1 minute, display *"Less than 1 minute read"*, 
2. if its between 1 minute and 1 and a half minutes display *"1 minute read"*, 
3. and if its more than 1 and half minutes, display the *"calculated+rounded minutes read"*. 
 
Here is the code to achieve this:

{% highlight ruby %}
{% raw %}
{% if site.readtime %}
  {% if readtime < 1 %}Less than 1 minute read
  {% elsif readtime > 1 and readtime < 1.5 %}1 minute read
  {% elsif readtime > 1.5 %}<span class="time">{{ readtime }}</span> minutes read{% endif %}
{% endif %}
{% endraw %}
{% endhighlight %}

To display the **Estimated Reading Time (ERT)** inside the Article page, the method is pretty straightforward. Simply put this code anywhere before using the `{% raw %}{{ readtime }}{% endraw %}` tag:

{% highlight ruby %}
{% raw %}
{% if site.readtime %}
  {% if site.wpm %}
    {% assign readtime = page.content | strip_html | number_of_words | append: '.0' | divided_by:site.wpm %}
  {% else %}
    {% assign readtime = page.content | strip_html | number_of_words | append: '.0' | divided_by:180 %}
  {% endif %}
{% endif %}
{% endraw %}
{% endhighlight %}

Then put the required markup as before to display the **Estimated Reading Time (ERT)** anywhere you like. You can wrap all these in your own styling, maybe add a [Font-Awesome Clock](http://fortawesome.github.io/Font-Awesome/icon/clock-o/) icon to it.

### Advanced

The **Liquid** + **JS** code mentioned above will get the job done. But what happens if you have a really long post that has a readtime estimate more than an hour? Or maybe your `site.wpm` is set to a really low number. Suppose you've a post that might take a user 127 minutes to read. Will not it be awesome if you can display 2 hours and 7 minutes instead of 127 minutes.

Lets make our existing code a fully functioning, semantically correct by integrating hours and minutes in it.

The math is simple, if the readtime is less than 60 minutes, jekyll only runs the above mentioned code. But if its more than 60 minutes, there are a few more steps to tackle.

Here is the complete code that integrates the code mentioned above and adds to it:

{% highlight ruby %}
{% raw %}
{% if site.readtime %}
{% if readtime > 60 %}
{% assign readtime_hours = readtime | divided_by: 60 %}
{% assign readtime_minutes = readtime | modulo:60 %}
	{% if readtime_hours > 1 and readtime_hours < 2 %}1 hour
	{% else %}<span class="hour">{{ readtime_hours }}</span> hours
	{% endif %}{% if readtime_minutes < 1 %}{% elsif readtime_minutes > 1 and readtime_minutes < 1.5 %} and 1 minute {% elsif readtime_minutes > 1.5 %} and <span class="time">{{ readtime_minutes }}</span> minutes{% endif %}
{% else %}
	{% if readtime < 1 %}Less than 1 minute {% elsif readtime > 1 and readtime < 1.5 %}1 minute {% elsif readtime > 1.5 %}<span class="time">{{ readtime }}</span> minutes {% endif %}{% endif %} read
{% endif %}
{% endraw %}
{% endhighlight %}

As you can see, I had to enclose the **readtime_hours** in a `<span class="hour"></span>`. that's because the Hour has to be a floored number. Finally a small modification to the JavaScript snippet to make these all work.

{% highlight javascript %}
{% raw %}
<script type='text/javascript'>
  $(document).ready(function() {
    $(".time").text(function (index, value) {
      return Math.round(parseFloat(value));
    });
    $(".hour").text(function (index, value) {
      return Math.floor(parseFloat(value));
    });
  });
</script>
{% endraw %}
{% endhighlight %}

Why take all these trouble? **Because we can!** And our Core i7s can!

## **Requests?**

If you have some specific requests for this snippet, or if you need help custom coding, message me on Twitter [@hmfaysal](http://twitter.com/hmfaysal) or email me at [hmfaysal@alum.mit.edu](mailto:hmfaysal@alum.mit.edu)

If you'd like to give me credit somewhere on your blog or tweet a shout out to [@hmfaysal](https://twitter.com/hmfaysal), that would be pretty sweet.
