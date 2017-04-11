---
layout: post
title: Memory efficiency - late instantation
tags: code_efficiency lynda
---

One of my favorite lynda lecturers, [Simon Allardice](https://www.lynda.com/Simon-Allardice/21-1.html), offers foundational courses regardless of what language you use. I'm taking his course [Foundation of Programming: Code Efficiency](https://www.lynda.com/Developer-Programming-Foundations-tutorials/Foundations-Programming-Code-Efficiency/122461-2.html) 


One strategy to improve memory efficiency, specifically, is called late instantiation - when an object is requested, check if **it's null**, then instantiate the object.

Here is an example. Instead of using below
<p>
{% highlight ruby %}
// class creation
class Student{   
	String name;
	Image photo;
	// something

	// constructor
	public Student (String st){     
	  name = n;
	  // an image object is created when a student object is created
	  photo = new Image("~/path/student/images"+name);  
	}

	public Image getPhoto(){
	  return photo;
	}
}
{% endhighlight %}
</p>

some attributes of an object can be moved out of the constructor which in this case is the *photo* property. They will be created if a user asks for it.
<pre>
//...

public Student (String st){     //constructor
	name = n;
	<strike>photo = new Image("~/path/student/images"+name);</strike>
}

public Image getPhoto(){
	<strong>if (photo == null)</strong>{
		photo = new Image("~/path/student/images"+name);
	}
	return photo;
}
</pre> 