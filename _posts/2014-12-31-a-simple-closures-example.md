---
title: "A Simple Closure Example"
tags: [javascript, technology]
layout: post
date: 2014-12-31
---

Ah, the night before New Years, the _perfect_ time for programming. Recently, I have been brushing up on my Javascript coding in preparation of my co-op term, and revisited closures. Closures is a very powerful feature of Javascript, albeit one that is quite tricky to understand at first. Below is an excerpt from [Jibbering](http://jibbering.com/faq/notes/closures/) that aims to define closures in a couple of paragraphs.

>Closures are one of the most powerful features of ECMAScript (javascript) but they cannot be properly exploited without understanding them. They are, however, relatively easy to create, even accidentally, and their creation has potentially harmful consequences, particularly in some relatively common web browser environments. To avoid accidentally encountering the drawbacks and to take advantage of the benefits they offer it is necessary to understand their mechanism. This depends heavily on the role of scope chains in identifier resolution and so on the resolution of property names on objects.
>
>The simple explanation of a Closure is that ECMAScript allows inner functions; function definitions and function expressions that are inside the function bodes of other functions. And that those inner functions are allowed access to all of the local variables, parameters and declared inner functions within their outer function(s). A closure is formed when one of those inner functions is made accessible outside of the function in which it was contained, so that it may be executed after the outer function has returned. At which point it still has access to the local variables, parameters and inner function declarations of its outer function. Those local variables, parameter and function declarations (initially) have the values that they had when the outer function returned and may be interacted with by the inner function.
>
>Unfortunately, properly understanding closures requires an understanding of the mechanism behind them, and quite a bit of technical detail. While some of the ECMA 262 specified algorithms have been brushed over in the early part of the following explanation, much cannot be omitted or easily simplified. Individuals familiar with object property name resolution may skip that section but only people already familiar with closures can afford to skip the following sections, and they can stop reading now and get back to exploiting them.

A very simple example of a closure looks like this:

{% highlight javascript linenos %}
function foo(x) {
  var tmp = 3;

  function bar(y) {
    alert(x + y + (++tmp)); // will alert 16
  }

  bar(10);
}

foo(2);
{% endhighlight %}

where ```bar``` can access both the parameter of the outer function ```x``` as well as its local variable ```tmp```. The original post on [StackOverflow](http://stackoverflow.com/a/111200/2252894) goes a lot more in-depth into the explanation.

##Where I Came Across It
A common way closures are created is from the heavy usage of callback methods in Javascript. While I was writing some code to perform GET requests on three provided URLs asynchronously, I ran into a weird bug. My first iteration of the code looked like this:

{% highlight javascript linenos %}
var http = require('http')
var bl = require('bl');

var dataList = [];
var count = 0;

for (var i=0; i<3; ++i) {
  http.get(process.argv[2+i], function (response) {
    response.pipe(bl(function (err, data) {
      if (err)
        return console.error(err);
      dataList[i] = data.toString();
      ++count;
      if (count == 3)
        printAll();
    }));
  });
}

function printAll() {
  for (var i=0; i<3; ++i) {
    console.log(dataList[i]);
  }
}
{% endhighlight %}

At first glance, this code will seem to work, but the output of the preceding program is:

~~~
undefined
undefined
undefined
~~~

The reason for this was apparent once I traced through the code. At line 7, I have a synchronous for-block that executes asynchronous code. Line 10 defines a callback function for bl:

{% highlight javascript linenos %}
function (err, data) {
  if (err)
    return console.error(err);
  dataList[i] = data.toString();
  ++count;
  if (count == 3)
    printAll();
}
{% endhighlight %}

In this callback, the variable ```i``` refers to the ```i``` in the for-loop, which is in the outer scope. The variables ```i``` used in the three definitions of the callback functions continue to refer to the ```i``` in the loop, so that at the end of the synchronous for-loop, all the ```i``` variables will have the value ```3```. This can be confirmed with the following addition to the callback definition:

~~~
console.log(i);
~~~

The new result will be:

~~~
3
3
3
undefined
undefined
undefined
~~~

In order to fix this, I wrapped the for-loop contents in a function, which creates a new closure, closing ```i``` to my new helper function. Each respective ```i``` definition is closed to its respective helper "factory" function, and it will have a value of ```i``` that corresponds with the index that the factory function was originally closed to. The final iteration of my code looked like this, which works as expected:

{% highlight javascript linenos %}
var http = require('http')
var bl = require('bl');

var dataList = [];
var count = 0;

for (var i=0; i<3; ++i) {
  httpget(i);
}

function printAll() {
  for (var i=0; i<3; ++i) {
    console.log(dataList[i]);
  }
}

function httpget(i) {
  http.get(process.argv[2+i], function (response) {
    response.pipe(bl(function (err, data) {
      if (err)
        return console.error(err);
      dataList[i] = data.toString();
      ++count;
      if (count == 3)
        printAll();
    }));
  });
}
{% endhighlight %}

So in the end, it wasn't one closure example, but two that I wrote about in this post. Regardless, I hope you guys find this post useful. Have a Happy New Year and 2015, here I come!

<!--end-->
