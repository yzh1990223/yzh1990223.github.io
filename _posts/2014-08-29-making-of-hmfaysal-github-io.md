---
layout: post
title: Making of hmfaysal.github.io
description: "The journey of designing & coding this site"
modified: "2014-08-29 23:18:46 +0600"
category: webdevelopment
tags: 
  - design
  - github
  - jekyll
imagefeature: null
location: "Mirpur 11, Bangladesh"
locationgps: null
mathjax: false
chart: false
comments: true
featured: true
published: true
---

This is the first chapter of how I designed this site. I will explain my choice of the site engine, share some concepts that ultimately shaped this site and elaborate on the features of this site. This project has taken a week to develop and optimize.

## Day 1 - The Concept

**"Speed"**, I wanted blazing fast loading times for this site. I wanted a super-fast blog where my thoughts and ideas can scream freely. For long I had been confined to the [WordPress](http://wordpress.org/)/PHP ecosystem. PHP is growing old and feeble, and it stumbles in this new era of computing. From the planning stages to the initial sketches to the development phases to the final production, speed has been the main point of focus from the get go.

> "Speed has been the main point of focus from the get go"

To achieve that level of performance, I had some features in mind:

1. Fast and light
2. Beautiful Typography
3. Block/Grid layout
4. Minimal embellishments — <del>content first</del>
5. Responsive layout. Looking good on mobile, tablet, and desktop
6. High Performance Coding

### The First Sketch

Like any other project, the design process started with a sketch. I had an idea what my website should look like and I sketched the idea pretty quickly.

![First Sketch]({{ site.url }}/images/post/sketch-web.jpg "First Sketch")
<figcaption>The preliminary wire-frame model</figcaption>

### The Inspiration

This website was heavily inspired by [Medium.com](https://medium.com/). From the minimal typography to the graceful responsiveness, Medium heavily influenced my design philosophy.

The idea of implementing a Status Update system in a big header form came from [Facebook](http://www.facebook.com)'s status update system and [WordPress's sticky posts](http://codex.wordpress.org/Sticky_Posts). I had a few concepts of how to implement this feature. My preliminary ideas to implement this feature were:

#### 1. Usage Post Types

I coined the idea to implement a post "type: status" in the post matter YAML and give this post type a different styling via CSS in the post index.

#### 2. Usage of Post Types to stick the "status" posts on top of the feed

I also conceived an idea to isolate the "status" type posts and stick those on top of the regular post index

But what I really wanted was to drive the uttermost attention to my most current status post. To achieve this I put it in big header font in the site's header. I also use subtle CSS tricks to make the other texts in the page become invisible (which become available on scrolling) on site's first load to drive the attention to the Status Message.

## Day 2 - The Prerequisites

#### Jekyll: Blog Aware Static Site Generator

For the blog, I decided to go static. There are quite a handful of great static blog generators out there, but I shortlisted [Pelican](http://blog.getpelican.com/) and [Jekyll](http://jekyllrb.com/) as my choices. Pelican is a great Python based static site generator. But I finally decided to use Jekyll, its an absolutely fantastic ruby gem.

![Jekyll]({{ site.url }}/images/post/jekyllrb.dark.png "Jekyll")

Jekyll is amazingly vanilla. It does not do anything you do not ask it to do. Now this may be a matter of nuisance for most users, but for this project where speed matters the most, Jekyll was the perfect choice.

#### Foundation: Mobile-First Vanilla CSS

For the base CSS, I decided to go with [Zurb Foundation 5](http://foundation.zurb.com/). (There is a [great article](http://blog.teamtreehouse.com/use-bootstrap-or-foundation) by Treehouse about the differences between Bootstrap and Foundation) Foundation's mobile-first approach is awesome when building minimalist websites. To keep the footprint minimal, I [customized](http://foundation.zurb.com/develop/download.html#customizeFoundation) the Foundation CSS file to have the minimal markup.

![Zurb Foundation 5]({{ site.url }}/images/post/zurb-foundation.png "Foundation 5")


## Day 3 - Back to the drawing board

Now that I have all the prerequisites, I decided to brush up my preliminary mock-up and give it some real world value. I always find an intermediary sketch to be extremely helpful as this weeds out any design flaw that the preliminary sketch might have had and was overlooked. The following sketches show a more realistic realization of desktop version of this project.

<figure class="half">
<img src="{{ site.url }}/images/post/Index-Diagram.png" title="Sketch: Blog Index" />
<img src="{{ site.url }}/images/post/Post-Diagram.png" title="Sketch: Post View" />
<figcaption>Intermediate Sketches</figcaption>
</figure>

These sketches gave me a solid overview of the elements sizing and positioning. Now that I have some valid blueprints, its time to move on to the real work


## Day 4 - The Typography

Zurb Foundation provided an excellent framework to achieve the pretty standard block layout. The second most important feature on my list was readability. I wanted my viewers to have an immersive reading experience which is beautiful to look at and free from clutter. I settled on **"Montserrat"** by [Google Fonts](https://www.google.com/fonts) to deliver the optimum reading experience.

![Dropcap]({{ site.url }}/images/post/dropcap.jpg "Dropcap")

There is a switchable "Dropcap" CSS feature that adds elegance to the posts by turning the first letter of the first paragraph into a dropcap. Plus the block-quotes float elegantly in between paragraphs.

## Day 5 - Going Mobile

Foundation's mobile-first approach + responsive grid layout meant I did not have to do much to get a mobile-friendly, gracefully responsive view on a hand-held device. The only thing I had to implement was a mobile-menu. I sketched out a couple of wire-frame models to give myself a clear understanding of what I was going to implement.

![Sketch: Mobile Layout]({{ site.url }}/images/post/sketch-mobile.jpg "Sketch: Mobile Layout")
![Sketch: Mobile Menu]({{ site.url }}/images/post/mobile-menu.jpg "Sketch: Mobile Menu")
<figcaption>Mobile menu</figcaption>

Foundation Visibility feature and CSS3 transforms were used for the mobile menu animation to get the best performance.

## Day 6 - Added Functions

#### Fullscreen Cover Photos

I was inspired by a [Codrops article](http://tympanus.net/codrops/2014/05/22/inspiration-for-article-intro-effects/) to include this feature. The idea was to show some creative transition containing a full-screen image when continuing to the article body. The effect slices the main image into two where the first half moves up and the second one slides down, giving space for the title to enlarge.

![Fullscreen Cover Photos]({{ site.url }}/images/post/fullscreen-cover.jpg "Fullscreen Cover Photos")

Animating large images can become a bit sluggish, also because a couple of transitions happening at the same time. The effect gets triggered when scrolling begins or when the button is clicked.

##### Background-Check.js

I included [backgroundcheck.js](http://www.kennethcachia.com/background-check/) by [Kenneth Cachia](http://www.kennethcachia.com/) to automatically switch the post title to a darker or a lighter version depending on the brightness of the image behind it.

#### Twitter Select Share

This site has been heavily inspired by [Medium.com](https://medium.com/). I particularly liked the concept of "Text Select to Share on Twitter" functionality. I wrote a JavaScript snippet that brings up an option to share some text to Twitter when selected.

![Twiiter Share: Selected Text]({{ site.url }}/images/post/select-share.png "Twitter Selected Text Share")

#### NProgress.JS

I could not make the website content-first, well I could have done it, but it would mean I had to sacrifice a few aesthetic elements. So I included [NProgress.JS](http://ricostacruz.com/nprogress/), a nanoscopic progress bar on top of the page that shows realistic trickle animations to convince users that something is happening!

![NProgress.JS on top of the website]({{ site.url }}/images/post/browser-mockup.jpg "NProgress.JS Trickle Animation")

## Day 7 - "Pushing" The code and Going live

After 7 days of careful planning and coding, debugging and optimizing performance, I pushed the code to [Github Pages](https://pages.github.com/) on 29th August, 2014 and this site went live utilizing Github's built in Jekyll engine.

![Device Demonstration]({{ site.url }}/images/post/showcase.jpg "Final Product")

If you like this post, feel free to share it with your friends, or give me a shout-out at @[hmfaysal](https://twitter.com/hmfaysal)