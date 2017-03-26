---
layout: post
title: memory efficiency - late instantation
tags: code_efficiency lynda
---

One of my favorite lynda lecturers, [Simon Allardice](https://www.lynda.com/Simon-Allardice/21-1.html) offers foundational course regardless of what language you use. I'm taking his course [Foundation of Programming: Code Efficiency](https://www.lynda.com/Developer-Programming-Foundations-tutorials/Foundations-Programming-Code-Efficiency/122461-2.html) 


Late instantiation: when an object is requested, check if **it's null**, then instantiate the object.

Instead of using below
<p><pre>
//class creation
class Student{   
	String name;
	Image photo;
	//etc

	//constructor
	public Student (String st){     
		name = n;
		//an image object is created when a student object
		is created
		photo = new Image("~/path/student/images"+name);  
	}

	public Image getPhoto(){
		return photo;
	}
}
</pre></p>

some attributes of an object can be moved out of the constructor. They will be created if a user asks for it.
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