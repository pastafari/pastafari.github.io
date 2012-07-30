---
layout: post
title: "SICP notes - Week 1"
date: 2012-07-30 22:07
comments: true
categories: [sicp, scheme, lambda calculus]
---

This was a slow week for SICP. I managed to read 20 pages (thru section 1.1.6) and [solve exercises 1.1 thru 1.5.](https://github.com/pastafari/sicp-redux/commit/0ded16f54e46dc8b451dd39c72edc08af776477c)  
*As an aside, I also read the foreword by Alan Perlis which was a pleasure to read and the preface to both the first and second editions (both worth reading IMO).*

I find the book incredibly dense with insights and learnings and am happy to read at a leisurely pace absorbing as much as I can. 
 
The 1st chapter titled **Building Abstractions with Procedures** begins with a quote:

{% blockquote John Locke, An Essay concerning Human Understanding(1690) %}
The acts of the mind wherein it exerts its power over simple ideas are chiefly these three: 
1. Combining several simple ideas into one compound one, and thus all complex ideas are made. 
2. The second is bringing two ideas, whether simple or complex, together, and setting them by one another so as to take a view of them at once, without uniting them into one, by which it gets all its ideas of relations. 
3. The third is separating them from all other ideas that accompany them in their real existence: this is called abstraction, and thus all general ideas are made.    
{% endblockquote %}

It seems that `abstraction` is going to be a strong theme through the book. We dive into things with an introduction to 'computational processes' and by introducing the Lisp programming language.   

One section of note asks the question:   
**_If Lisp is not a mainstream programming language, why are we using it as the framework for our discussion of programming?_**
  

The answer:  
**Lisp descriptions of processes, called `procedures`, can themselves be represented and manipulated as Lisp data.**
**The importance of this is that there are powerful program-design techniques that rely on the ability to blur the traditional distinction between `"passive" data` and `"active" processes`** 
  

The next section begins with the general idea of `language` itself:

{% blockquote %}
... Every powerful language has three mechanisms for accomplishing this:

**primitive expressions -> which represent the simplest entities the language is concerned with.**
**means of combination -> by which compound elements are made from simpler ones, and**
**means of abstraction -> by which compound elements can be named and manipulated as units.**

{% endblockquote %}

Last week, I read a bit about [the lambda calculus *PDF](ftp://ftp.cs.ru.nl/pub/CompMath.Found/lambda.pdf) and realized that the above is in fact a translation into English of the formal definition for `lambda terms`! Very interesting to note that the document linked above states clearly that the two branches of programming languages - The Fortran derivatives and The Lisp derivatives are essentially manifestations of the `Turing Machine (Alan Turing)` and `the Lambda Calculus (Alonzo Church)` respectively. Math is awesome stuff indeed :) 

The rest of the sections introduce the Scheme dialect of Lisp, which seems to be easy to pick up once you get used to the prefix notation and parentheses! 

The concept of `tree accumulation`, `substitution model` and the examples of `applicative order` and `normal order` substitution are introduced with examples. 

The application of these concepts is made clear in example 1.5 whose solution I have pasted below: 

<script src="https://gist.github.com/3208989.js?file=sicp-1.5.scm"></script>

I am not sure about the format for these notes. They will probably evolve as I continue reading. But for now, they are akin to a chronological walk through the book itself. 