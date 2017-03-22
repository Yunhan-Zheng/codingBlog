---
layout: post
title: Bug fix of Project Page URL Structure
tags: bug front_end
---

As a newbie in front end development, I prefer learning by doing and researching instead of taking an online course.

When I set up my personal site, clicking the About item in the sidebar directed me to a 404 page. It turned out that the url of About page is https://yunhan-zheng.github.io/about.html which missed my repo **/lmdolphy** between **https://yunhan-zheng.github.io** and **/about.html**. 

<p>By searching  
	<em class="highlight">
		jekyll github about 404
	</em>
		I found the <a href="https://github.com/tararoys/simple-documentation-process/commit/2693c8a74270d5b2d4a0209bb77b0d3f71c92a0e">similar issue</a> happened to tararoys. The bug is because the <a href="http://jekyllrb.com/docs/github-pages/#project_page_url_structure">git hub page structure is incompatible with simply adopting jekyll</a>. 
</p>

Thanks to the solution posted by *tararoys*, I was able to update _config.yml and sidebar.html to assign correct links to navigation items on the sidebar.

<h2>My solution</h2>

My site resides on github with a url https://yunhan-zheng.github.io/lmdolphy/ where */lmdolphy* actually acts as the base url. Instead of using the whole url in the url setup in the _config.yml, I commented out the url and added the baseurl.  
<p>
	<img style="width:100%;display:inline-block" alt="baseurl setting" src="{{site.baseurl}}/public/image/2.jpeg">
</p>

<p>
	Accordingly, the 
	<em class="highlight">sidebar.html</em> needs the following change - add {% raw  %}{{ site.baseurl }}{% endraw %} - so that it reacts to the change in the config.
</p>
<p>
	<img style="width:100%;display:inline-block" alt="add baseurl to node" src="{{site.baseurl}}/public/image/2-2.jpeg">
</p>