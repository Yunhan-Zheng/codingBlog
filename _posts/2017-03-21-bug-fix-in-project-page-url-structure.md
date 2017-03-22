---
layout: post
title: Bug fix of Project Page URL Structure
tags: bug front_end
---

As a newbie in front end development, I prefer learn by doing and researching instead of taking an online course.

The first bug in my personal site is because the [git hub page structure is incompatible with simply adopting jekyll](http://jekyllrb.com/docs/github-pages/#project_page_url_structure).  


Thanks to the [similar issue](https://github.com/tararoys/simple-documentation-process/commit/2693c8a74270d5b2d4a0209bb77b0d3f71c92a0e) found and resolved by *tararoys*, I was able to update _config.yml and sidebar.html to assign correct links to navigation items on the sidebar.

<h2>My case</h2>

My site resides on github with a url https://yunhan-zheng.github.io/lmdolphy/ where '/lmdolphy' actually acts as the base url. Instead of using the whole url in the url setup in the _config.yml, I deleted url and added the baseurl.  
<p>
	<img style="width:100%;display:inline-block" alt="baseurl setting" src="{{site.baseurl}}/public/image/2.jpeg">
</p>

<p>
	Accordingly, the sidebar.html needs the following change (added {% raw  %}{{ site.baseurl }}{% endraw %}) so that it reacts to the change in the config.
</p>
<p>
	<img style="width:100%;display:inline-block" alt="add baseurl to node" src="{{site.baseurl}}/public/image/2-2.jpeg">
</p>