---
layout: post
title: Installation of Yeoman and the Aspnet Generator
tags: install npm yeoman aspnet
date: 2017-06-17 19:02:00 -0400
comments: true
---
Since Visual Studio Code is light tool, I decided to install Yeoman, a series of generators to create files and projects including web applications, so that I can use command lines to build projects. In fact,Yeoman has a generator called **Aspnet** which creates projects as Visual Studio will do.

Prerequisites: VS Code

1. Open VS Code

2. Type `node --version` in the terminal. If you don't have it open, navigate to View to bring it up in VS Code.
<p>
	<img style="width:100%;display:inline-block" alt="integrated terminal" src="{{site.baseurl}}/public/image/integratedTerminal.jpeg">
</p>

3. If you don't have node installed. Download it from <a href="https://nodejs.org/" target="_blank">Node.JS</a>.

4. Type `npm install yo -g` in terminal so that Yeoman is installed globally.

5. Install the generator for ASP.NET by entering `npm install generator-aspnet -g` in terminal.

If you see the same options once you type `yo aspnet`, you have successfully installed Yeoman and the ASP.NET generator!

<p>
	<img style="width:100%;display:inline-block" alt="options of the aspnet generator" src="{{site.baseurl}}/public/image/yeoman.jpeg">
</p>
