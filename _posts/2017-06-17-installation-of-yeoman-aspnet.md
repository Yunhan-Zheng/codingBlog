---
layout: post
title: Installation of Yeoman and the Aspnet Generator
tags: install npm yeoman aspnet
date: 2017-06-17 19:02:00 -0400
comments: true
---
Since Visual Studio Code is light, I decided to install Yeoman, a series of generators to create files and projects including web applications, so that I can use command lines to build projects. In fact,Yeoman has a generator called **Aspnet** which creates projects as Visual Studio will do.

Prerequisites: VS Code

<ol>
	<li>Open VS Code</li>
	<li>Type <strong>node --version</strong> in the terminal. If you don't have it open, navigate to View to bring it up in VS Code.</li>
<p>
	<img style="width:50%;display:block;margin:0 auto" alt="integrated terminal" src="{{site.baseurl}}/public/image/integratedTerminal.jpeg">
</p>
<li>If you don't have node installed. Download it from <a href="https://nodejs.org/" target="_blank">Node.JS</a> and install it.</li>

<li>Type <strong>npm install yo -g</strong> in terminal so that Yeoman is installed globally.</li>
<li>Install the generator for ASP.NET by entering <strong>npm install generator-aspnet -g</strong> in terminal.</li>
</ol>

If you see the same options once you type `yo aspnet`, you have successfully installed Yeoman and the ASP.NET generator!

<p>
	<img style="width:100%;display:inline-block" alt="options of the aspnet generator" src="{{site.baseurl}}/public/image/yeoman.JPG">
</p>
