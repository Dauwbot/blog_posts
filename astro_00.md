---
layout: ../../layouts/thoughtPost.astro
title: Using Astro to create a blog
abstract: There's a new player in town. Meet Astro! The framework that allow you to use other frameworks! This site use it, this post explain how I did it so you can too!
categories: 
- Astro
- Blog
published: false
date: 20210709
---
# One framework to rule them all!

I've discovered Astro on Reddit, if you don't know what Reddit is I can only give you one tip: don't go on Reddit. I've been nearly Facebook free for years but I can't make one day without going on Reddit. As if being able to follow only things you're interested in make you check it non-stop. In the past we had jokes book in the WC, now I've Reddit with beautiful permaculture gardens, compost bins & some development sprinkled on top.

Back to Astro: if you check for it on Google you will not find it (at least not on the 21/07/13), you've to use the astro.build keywords. The aim is clear: Ship websites without (too much) client-side Javascript.

In the search of constructing this portfolio I was aiming to go with Next.JS for the server-side rendering but since I had the opportunity to test Astro (in beta currently), I took it. And spoiler... It was a pleasure to do so!

## Lots of HTML & CSS
So Astro is aiming to ship less JavaScript, big news wow. I've used it and I can say that going back to writing semantic HTML & CSS (scoped to the "component") is a pleasure. It supports SCSS out-of-the-box by adding the quick `lang=scss` tag at the top.
It aims to have a simple folders structure. Here's a picture of the complete structure for this portfolio/blog. ![project structure](/assets/images/blog_posts/00_astro/01_folderStructure.png "Dendauw.tech project structure")