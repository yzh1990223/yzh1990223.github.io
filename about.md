---
layout: page
permalink: /about/
title: About me
tags: 
  - Hossain
  - Mohd
  - Faysal
  - hmfaysal
imagefeature: fourseasons.jpg
chart: true
charttype: pie
published: true
---

<figure>
  <img src="{{ site.url }}/images/page/hmfaysal-crest-square.jpg" alt="Hossain Mohammad Faysal">
  <figcaption>Hossain Mohammad Faysal</figcaption>
</figure>

{% assign total_words = 0 %}
{% assign readtime = 0 %}
{% assign featuredcount = 0 %}
{% assign statuscount = 0 %}

{% for post in site.posts %}
    {% assign post_words = post.content | strip_html | number_of_words %}
    {% if site.wpm %}{% assign indi_readtime = post_words | append: '.0' | divided_by:site.wpm %}{% else %}{% assign indi_readtime = post_words | append: '.0' | divided_by:180 %}{% endif %}
    {% assign total_words = total_words | plus: post_words %}
    {% assign readtime = readtime | plus: indi_readtime %}
    {% if post.featured %}
    {% assign featuredcount = featuredcount | plus: 1 %}
    {% endif %}
{% endfor %}
{% for status in site.data.statuses %}{% assign statuscount = statuscount | plus:1 %}{% endfor %}

My name is **Hossain Mohd. Faysal**, and this is my personal blog. It currently has {{ site.posts | size }} posts in {{ site.categories | size }} categories which combinedly have {{ total_words }} words, and will take an average reader ({{ site.wpm }} WPM) approximately {% if readtime > 60 %}{% assign readtime_hours = readtime | divided_by: 60 %}{% assign readtime_minutes = readtime | modulo:60 %}{% if readtime_hours > 1 and readtime_hours < 2 %}1 hour{% else %}<span class="hour">{{ readtime_hours }}</span> hours{% endif %}{% if readtime_minutes < 1 %}{% elsif readtime_minutes > 1 and readtime_minutes < 1.5 %} and 1 minute {% elsif readtime_minutes > 1.5 %} and <span class="time">{{ readtime_minutes }}</span> minutes{% endif %}{% else %}{% if readtime < 1 %}less than 1 minute {% elsif readtime > 1 and readtime < 1.5 %}1 minute {% elsif readtime > 1.5 %}<span class="time">{{ readtime }}</span> minutes {% endif %}{% endif %} to read. {% if featuredcount != 0 %}There are <a href="{{ site.url }}/featured">{{ featuredcount }} featured posts</a>, you should definitely check those out.{% endif %} The most recent post is {% for post in site.posts limit:1 %}{% if post.description %}<a href="{{ site.url }}{{ post.url }}" title="{{ post.description }}">"{{ post.title }}"</a>{% else %}<a href="{{ site.url }}{{ post.url }}" title="{{ post.description }}" title="Read more about {{ post.title }}">"{{ post.title }}"</a>{% endif %}{% endfor %} which was published on {% for post in site.posts limit:1 %}{% assign modifiedtime = post.modified | date: "%Y%m%d" %}{% assign posttime = post.date | date: "%Y%m%d" %}<time datetime="{{ post.date | date_to_xmlschema }}" class="post-time">{{ post.date | date: "%d %b %Y" }}</time>{% if post.modified %}{% if modifiedtime != posttime %} and last modified on <time datetime="{{ post.modified | date: "%Y-%m-%d" }}" itemprop="dateModified">{{ post.modified | date: "%d %b %Y" }}</time>{% endif %}{% endif %}{% endfor %}. The last commit was on {{ site.time | date: "%A, %d %b %Y" }} at {{ site.time | date: "%I:%M %p" }} [UTC](http://en.wikipedia.org/wiki/Coordinated_Universal_Time "Temps Universel Coordonné"). Check out the update log [here]({{ site.url }}/update-log).

Currently there are [{{ statuscount }} status messages.]({{ site.url }}/status-updates)

<div class="chart" id="chartdiv" style="width: 100%; height: 500px; margin-bottom: 20px;" ></div>

I am an PhD candidate in *ESE* at the [SEAS](http://www.seas.upenn.edu/) at **UPENN**. I am licensed as a Professional Engineer (P.E) to practice in the states of Texas, Massachusetts and California. I double majored in EECS and Mathematics during my undergraduate life at [MIT](http://www.mit.edu/), and currently focusing on Electrical Engineering for my post-graduate studies.

*[ESE]: Electrical and Systems Engineering
*[SEAS]: School of Engineering and Applied Science
*[MIT]: Massachusetts Institute of Technology
*[EECS]: Electrical and Computer Engineering
*[UPENN]: University of Pennsylvania

Currently I am working on solid state electronics and trying to figure out novel methods to develop computer architectures with carbon nanotubes. My research interest lie from Computational Mathematics to Quantum Physics to Numerical Analysis.

<figure>
	<img src="{{ site.url }}/images/page/Hossain-Mohd-Faysal.jpg" alt="Hossain Mohammad Faysal">
	<figcaption>At Bates Linear Accelerator Center</figcaption>
</figure>

I was born and brought up in Doha. Yes, its a desert peninsula, yes we have camels and falcons and all the other Middle Eastern traits/stereotypes you can think of.

<figure class="third">
	<a href="{{ site.url }}/images/page/about/1.jpg" title="Paul:Breakfast & light Snacks"><img src="{{ site.url }}/images/page/about/thumb/1.jpg"></a>
	<a href="{{ site.url }}/images/page/about/2.jpg" title="Souq Waqif"><img src="{{ site.url }}/images/page/about/thumb/2.jpg"></a>
	<a href="{{ site.url }}/images/page/about/3.jpg" title="Kempinski Doha"><img src="{{ site.url }}/images/page/about/thumb/3.jpg"></a>
</figure>
<figure class="half">
	<a href="{{ site.url }}/images/page/about/4.jpg" title="Pearl Qatar"><img src="{{ site.url }}/images/page/about/thumb/4.jpg"></a>
	<a href="{{ site.url }}/images/page/about/5.jpg" title="Admirals Club"><img src="{{ site.url }}/images/page/about/thumb/5.jpg"></a>
</figure>
<figure class="third">
	<a href="{{ site.url }}/images/page/about/6.jpg" title="Amphitheater at Katara Cultural Village"><img src="{{ site.url }}/images/page/about/thumb/6.jpg"></a>
	<a href="{{ site.url }}/images/page/about/7.jpg" title="Doha Skyline"><img src="{{ site.url }}/images/page/about/thumb/7.jpg"></a>
	<a href="{{ site.url }}/images/page/about/8.jpg" title="Camels at UmmSaieed Beach Resort"><img src="{{ site.url }}/images/page/about/thumb/8.jpg"></a>
	<figcaption>Doha at its full glory.</figcaption>
</figure>

I have one elder sister-- a graduate in Computer Applications-- currently living in Tokyo, Japan. My father is an Electrical Engineer and he works for the Qatar Electricity and Water Corporation(KAHRAMAA) in Doha, Qatar. My mother holds a Masters degree in Contemporary Bengali Literature, and well she is a house-maker. 

<figure>
	<img src="{{ site.url }}/images/page/world-map.jpg" alt="Places of Importance">
	<figcaption>Places of Importance</figcaption>
</figure>


At some point in the not-terribly-distant future, I hope to found a self-sustaining collective of clever people, for fun, profit(?), and the promotion of human life in the universe. This might wind up in Qatar, Bangladesh, Scandinavia, the Massachusetts Bay Area, the SF Bay Area, Japan, Germany, or the dustbin of overly idealistic plans. (Yes, I have a special bin for overly idealistic plans. In my district they can't be recycled with residential mixed paper.) The most challenging aspect of this concept is to curtail unproductive competition with other people who will inevitably have the same idea. (Some sort of cooperative federation...) I'm presently looking for people who might be interested in being a part of such an organization.

Anyways, for now I'm just working toward changing the face of Electrical Engineering forever. Not that I necessarily expect to succeed, but it's something to strive for, and it's a fun problem to work on.


Entrepreneur  
Designer  
***Engineer***  
Inventor  

I
make
stuff.


*Beautiful, practical, meaningful stuff.*


I make what I love.

*I love what I do.*


But over the years, I noticed that somehow, along the way, software designed to help us be creative, actually made us less creative. That's because we believe our best ideas emerge when we use pencils and paper.
So I set out to build tools that work the way I do.


Tools for the creative space — the 53 centimeters that magically link head, heart, and hand. Tools as simple as pencil and paper. Tools so essential, I  really can't imagine work without them.


For
the makers,  
the creators,  
the discoverers,  
the original thinkers,  
***This is the space to create.***

<!-- amCharts javascript code -->
<script type="text/javascript">
	AmCharts.makeChart("chartdiv",
		{
			"type": "pie",
			"pathToImages": "http://cdn.amcharts.com/lib/3/images/",
			"balloonText": "Category: [[title]]<br><span style='font-size:14px'><b>[[value]] Posts</b> ([[percents]]%)</span>",
			"innerRadius": "40%",
			"minRadius": 100,
			"pullOutRadius": "15%",
			"startRadius": "30%",
			"colors": [
				"#FC913A",
				"#F9D423",
				"#FF4E50",
				"#FCD202",
				"#F8FF01",
				"#B0DE09",
				"#04D215",
				"#0D8ECF",
				"#0D52D1",
				"#2A0CD0",
				"#8A0CCF",
				"#CD0D74",
				"#754DEB",
				"#DDDDDD",
				"#999999",
				"#333333",
				"#000000",
				"#57032A",
				"#CA9726",
				"#990000",
				"#4B0C25"
			],
			"hoverAlpha": 0.74,
			"pullOutEffect": "elastic",
			"pullOutOnlyOne": true,
			"startEffect": "easeOutSine",
			"titleField": "category",
			"valueField": "number-of-posts",
			"allLabels": [],
			"balloon": {},
			"legend": {
				"align": "center",
				"markerType": "diamond",
				"switchable": false,
				"textClickEnabled": true,
				"useMarkerColorForLabels": true,
				"useMarkerColorForValues": true,
				"valueText": "[[value]] Posts"
			},
			"titles": [
				{
					"id": "Title-1",
					"text": "Number of Posts Breakdown"
				}
			],
      "dataProvider": [
{% assign tags_list = site.categories %}  
  {% if tags_list.first[0] == null %}
    {% for tag in tags_list %} 
        {
          "category": "{{ tag | capitalize }}",
          "number-of-posts": {{ site.tags[tag].size }}
        },
    {% endfor %}
  {% else %}
    {% for tag in tags_list %} 
        {
          "category": "{{ tag[0] | capitalize }}",
          "number-of-posts": {{ tag[1].size }}
        },
    {% endfor %}
  {% endif %}
{% assign tags_list = nil %}
      ]
    }
  );
</script>