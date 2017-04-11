---
layout: post
title: Algorithmic efficiency - watch out!
tags: code_efficiency lynda
---
Following my previous post on code efficiency, today I'm gonna write down some traps where efficiency may be compromised because of poor algorithm.
<ol>
<li>Loops within loops</li>
Iterate the same data in both the inner loop and outer loop.
<br>
Example A:
{% highlight ruby %}
abcMethod(){
	for (a : aCollection){
	   // do sth
	   for (b : aCollection){
	      // do sth
	   }
	}
}
{% endhighlight %}

Example B:
<pre>
abcMethod(){
	for (a : aCollection){
	   //do sth
	   <strong>xyzMethod()</strong>;
	}
}

<strong>xyzMethod()</strong>{
	for (b : aCollection){
	      //do sth
	}
}
</pre>

<li>Instantiation inside loops</li>

Example C:
<pre>
abcMethod(){
	for (a : aCollection){
	   //...
	   AbcClass a = new AbcClass();
	}
}
</pre>

<li>Collection</li>
<p>
Depending on what funtion to use to a collection and how often the collection changes, it's extremely <em>important</em> to choose a right collection type. For instance, it's O(1) to direct access an element in an array, but it can be worse than O(n log n) to sort an array. Since big O is a critical topic in algorithm efficiency, I'll write a separate post to talk about its details.
</p>
<li>Concatenation of strings</li>
<p>
Strings are immutable. Therefore, it's always suggested that you use StringBuffer or StringBuilder if you want to use concatenetion in a loop.
</p>

<li>Search in large strings</li>
<p>
Be cautious to use wild card 
<strong>* %</strong>
or regular expression when you are about to find some text pattern in a large string. 
</p>
</ol>



