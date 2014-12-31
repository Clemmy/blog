---
title: "A Simple Closure Example"
tags: [javascript, technology]
---

Ah, the night before New Years, the _perfect_ time for programming. Recently, I have been brushing up on my Javascript coding in preparation of my co-op term, and revisited closures. Closures is a very powerful feature of Javascript, albeit one that is quite tricky to understand at first. Below is an excerpt from [Jibbering](http://jibbering.com/faq/notes/closures/) that aims to define closures in a couple of paragraphs.

>Closures are one of the most powerful features of ECMAScript (javascript) but they cannot be property exploited without understanding them. They are, however, relatively easy to create, even accidentally, and their creation has potentially harmful consequences, particularly in some relatively common web browser environments. To avoid accidentally encountering the drawbacks and to take advantage of the benefits they offer it is necessary to understand their mechanism. This depends heavily on the role of scope chains in identifier resolution and so on the resolution of property names on objects.
>
>The simple explanation of a Closure is that ECMAScript allows inner functions; function definitions and function expressions that are inside the function bodes of other functions. And that those inner functions are allowed access to all of the local variables, parameters and declared inner functions within their outer function(s). A closure is formed when one of those inner functions is made accessible outside of the function in which it was contained, so that it may be executed after the outer function has returned. At which point it still has access to the local variables, parameters and inner function declarations of its outer function. Those local variables, parameter and function declarations (initially) have the values that they had when the outer function returned and may be interacted with by the inner function.
>
>Unfortunately, properly understanding closures requires an understanding of the mechanism behind them, and quite a bit of technical detail. While some of the ECMA 262 specified algorithms have been brushed over in the early part of the following explanation, much cannot be omitted or easily simplified. Individuals familiar with object property name resolution may skip that section but only people already familiar with closures can afford to skip the following sections, and they can stop reading now and get back to exploiting them.



<!--end-->
