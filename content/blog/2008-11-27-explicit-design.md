---
title: Explicit Design
author: ferdy
date: 2008-11-27T22:45:59+00:00
url: /blog/2008/11/27/explicit-design/
b2008:
  - 11
bcategories:
  - Case
  - MDD
  - Microsoft
btags:
  - Explicit Design
  - MDD

---
[Steve Cook][1]:

> [Cameron][2] has been blogging about new features in our product.. In [a recent post][3] he used the term Explicit Design. I&#8217;ve been reflecting on this, and I like it. In software development we really do need to capture design data that is not just the code, but should be saved and versioned just like the code. What do we call it? We could call it &#8220;models&#8221; but &#8220;model&#8221; and &#8220;model driven development&#8221; are subject to so much historical baggage and methodology and [terminology arguments][4]. &#8220;Model&#8221; just seems to imply baked-in code generation and round tripping, when there is so much more that you can do with it: planning, verifying, testing, refactoring. We need new vocabulary that represents our ability to capture versioned design data at a more abstract level than the code without simultaneously implying the history of CASE. 

I have to agree: changing the name doesn&#8217;t solve the root of the problem, but perhaps we start thinking in a different way.

 [1]: http://blogs.msdn.com/stevecook/archive/2008/11/27/explicit-design.aspx
 [2]: http://blogs.msdn.com/camerons/
 [3]: http://blogs.msdn.com/camerons/archive/2008/11/10/testing-draft-to-blog.aspx
 [4]: http://blogs.msdn.com/keith_short/archive/2008/11/18/comments-on-communication-between-doug-purdy-and-lars-corneliussen.aspx

## Comments

### Comment by Bill Higgins on 2008-12-03 06:22:19 +0000
Grady Booch has an interesting take around this topic area:

&#8220;Every interesting software-intensive system has an architecture. While some of these architectures are intentional, most appear to be accidental.&#8221;

Links:
  
<a href="http://www.informit.com/articles/article.aspx?p=471929" rel="nofollow">http://www.informit.com/articles/article.aspx?p=471929</a>
  
<a href="http://www2.computer.org/portal/web/computingnow/onarchitecture" rel="nofollow">http://www2.computer.org/portal/web/computingnow/onarchitecture</a>

&#8211; Bill

### Comment by Ferdy on 2008-12-08 00:22:57 +0000
Bill, thanks for the link! A very interesting reading, a natural thing as it comes from Grady.

Some conclusions after reading the article:

1) We need to enumerate architectural patterns or styles, even if they come from accidental architectures. Something that I believe Grady is working on (<a href="http://www.handbookofsoftwarearchitecture.com/index.jsp?page=Main" rel="nofollow">Handbook of Software Architecture</a>), and, with a wide aim, <a href="http://www.hillside.net/" rel="nofollow">The Hillside Group</a>.

2) Most architectures come from previous works (theft): bifurcations, scrap and rework. Although most of them are accidental architectures, they are inevitable and some of them could become useful in future systems, but only if we&#8217;re able to describe them as a pattern.