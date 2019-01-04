---
title: Learning Erlang
author: ferdy
date: 2007-08-07T17:54:50+00:00
url: /blog/2007/08/07/learning-erlang/
b2007:
  - 08
bcategories:
  - Languages

---
After reading some exciting posts about [Erlang][1], I decided to find out for myself what this language is all about. So I ordered [Programming Erlang. Software for a Concurrent World][2], from the Pragmatic Bookshelf, and today I received my copy of the book.

> It&#8217;s about concurrency. It&#8217;s about distribution. It&#8217;s about fault tolerance. It&#8217;s about functional programming. It&#8217;s about programming a distributed concurrent system without locks and mutexes but using only pure message parsing. It&#8217;s about speeding up your programs on multi-core CPUs. It&#8217;s about writing distributed applications that allow people to interact with each other. It&#8217;s about design methods and behaviors for writing fault-tolerant and distributed systems. It&#8217;s about modeling concurrency and mapping those models onto computer programs, a process I call _concurrency-oriented programming_.

I don&#8217;t have time right now to dive into it too deep, I just started reading the first chapter, and I am already shocked.

> Erlang has _single assignment variables_. As the name suggests, **single assignment variables can be given a value only once**. If you try to change the value of a variable once it has been set, then you&#8217;ll get an error.

Wondering why?

> If you use a conventional programming language such as C or Java to program a multi-core CPU, then you will have to contend with the problem of _shared memory_. In order not to corrupt shared memory, the memory has to be locked while it is accessed. &#8230; In Erlang, there is no mutable state, there is no shared memory, and there are no locks. This makes it easy to parallelize our programs.

I am sure I will have lots of fun learning it!

 [1]: http://en.wikipedia.org/wiki/Erlang_%28programming_language%29
 [2]: http://pragmaticprogrammer.com/titles/jaerlang/index.html

## Comments

### Comment by xavier on 2007-09-11 02:08:02 +0000
I&#8217;m green with envy! You are making good progress!

When you posted this I was about to tell you that I was interested in joining you in the Erlang adventure, but after checking the huge backlog of non-day job projects I decided that this will have to wait&#8230;

My interest in Erlang was born when former IBM/Rational Doug Landauer <a href="http://radio.weblogs.com/0100945/2005/01/11.html" rel="nofollow">named his great intranet blog as Pyscerocha</a>, after Python, Scala, Erlang, OCaml, and Haskell.

In the last months, bcn&#8217;s IBM <a href="http://twiki.org/cgi-bin/view/Sandbox/ParadigmShift" rel="nofollow">Claudi Paniagua&#8217;s event driven architectures and event processing evangelizing</a> in the coffee machine and elsewhere has made me think more and more about the need to check how would Erlang fit that model.