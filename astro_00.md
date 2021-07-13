---
layout: ../../layouts/thoughtPost.astro
title: Using Astro to create a blog
abstract: There's a new player in town. Meet Astro! The framework that allow you to use other frameworks! This site use it, this post explain how I did it so you can too!
categories: 
- Astro
- Blog
published: true
date: 20210713
---
# One framework to rule them all!

I've discovered Astro on Reddit, if you don't know what Reddit is I can only give you one tip: don't go on Reddit. I've been nearly Facebook free for years but I can't make one day without going on Reddit. As if being able to follow only things you're interested in make you check it non-stop. In the past we had jokes book in the WC, now I've Reddit with beautiful permaculture gardens, compost bins & some development sprinkled on top.

Back to Astro: if you check for it on Google you will not find it (at least not on the 21/07/13), you've to use the astro.build keywords. The aim is clear: Ship websites without (too much) client-side Javascript.

In the search of constructing this portfolio I was aiming to go with NextJS for the server-side rendering but since I had the opportunity to test Astro (in beta currently), I took it. And spoiler... It was a pleasure to do so!

## Lots of HTML & CSS
So Astro is aiming to ship less JavaScript, big news wow. I've used it and I can say that going back to writing semantic HTML & CSS (scoped to the "component") is a pleasure. It supports SCSS out-of-the-box by adding the quick `lang=scss` tag at the top.
It aims to have a simple folders structure. Here's a picture of the complete structure for this portfolio/blog. ![project structure](/assets/images/blog_posts/00_astro/01_folderStructure.png "Dendauw.tech project structure")

As you can see, removing the usual suspects `dist` which is our build repo `node_modules` that contains our npm installed packages & the rest is mainly code and used files on the website. If you wonder what is the `.gitmodules` learn more [at the end of this article](#git-submodules)

In the `src` folder we've a components folder (hello React), a `layout` one & `pages` that contains well our pages. You should see that our file extension reads `.astro` which is a special file type.

## .astro magic
Inside those files is the content of our pages. Astro is smart enough to create links for each of our page. It's even able to render markdown natively!
At the top of the file you can execute JavaScript code, for example at the top of my `index.astro` page I use the following code block.
```
---
import TopNavigation from '../components/TopNavigation.astro';
import Footer from '../components/Footer.astro';

let title = 'Julien Dendauw';
---
```
I import my navigation component & my footer. You now the DRY principle? [Don't repeat yourself](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself), it has it's own Wikipedia page. And every page on my website should've a `Navigation` & a `Footer`. I can also define my title there for example and just reference it later using JSX like syntax 
```
<head>
    ...
    <title>{title}</title>
    <link rel="icon" type="image/svg+xml" href="/favicon.svg">
    <link rel="stylesheet" href="/style/global.css">
</head>
```

### Git Submodules
I'm using [Git submodules](https://git-scm.com/book/en/v2/Git-Tools-Submodules) to separate the content from the website code. I wanted for it to be completely decoupled but since I'm using the `layout` property inside the `Front Matter YAML block` it's a bit more coupled to Astro that I would've liked. Oh well 🤷