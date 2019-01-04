---
title: QCon 2007 summary – Part 2
author: ferdy
date: 2007-03-26T22:02:56+00:00
url: /blog/2007/03/26/qcon-2007-summary-part-2/
b2007:
  - 03
bcategories:
  - Conferences

---
A bit late, I know, but here it is the second part of the summary (1st and 2nd day):

&#8220;[Modifiability: Or is there Design in Agility?][1]&#8220;: [Martin Fowler][2] lead some [ThoughtWorks][3] architects through a discussion of design in an agile context. He started talking about a misconception: &#8220;Agility means to start coding directly, without designing&#8221;. So he remarked that it&#8217;s very important to start designing at the beginning of the project, although it can be modified during the rest of the project. He also stated that simple doesn&#8217;t mean stupid, simple means that it&#8217;s simple to use and it has sense.

&#8220;[Operational Manageability][4]&#8220;: [Dan Pritchett][5] (eBay Technical Fellow) talked about designing for operations and how operational scalability is a software problem. He point out some recommendations about managing configuration in a large enterprise, deploying without taking down the site and avoiding <acronym title="Single Point Of Failure">SPOF</acronym>. He also presented a fact: &#8220;Power and cooling are now the primary constraint to growth&#8221;, a fallacy: &#8220;Hardware will provide the performance improvements needed to keep pace with transaction growth&#8221;, and a reality: Inefficient software has driven datacenters to the brink of municipal power delivery capabilities&#8221;. He recommends trying to measure power efficiency using (and improving) metrics as for example page views per second / Watts. Dan has also a [great post][6] about scaling where he mentions all of the vectors you must consider.

&#8220;[Test Driven Development: How do we know we&#8217;re done?][7]&#8220;: Steve Freeman presented this introductory session about <acronym title="Test Driven Development">TDD</acronym>. He started with some basic cyclical examples: implementing a test just enough to pass and then Refactor! He said TDD is a design technique and we must test the features not the methods. He also said that unit test code could be half of the source code.

&#8220;[Agile Project Management: Lessons learned at Google][8]&#8220;: [Jeff Sutherland][9] started comparing [The Toyota way][10] and the [Agile Principles][11], and then the Google way. After that, he described how the [Adwords][12] project leader introduced Scrum into Google (an environment that does not have an affinity to processes in general). He talked about some problems that they have found (resistance, late deliveries, &#8230;) and how Google reinvented some Lean practices (work in progress). He concluded saying that &#8220;[Google] teams embraced the process enough to continue it even without any reinforcement&#8221;. At this [Google Tech Talk][13], you will find Jeff explaining the same presentation that he showed at Qcon.

And finally, [infoQ][14] has posted a [great article][15] where they present the main takeway points and lessons learned by attendees who blogged about [QCon][16].

 [1]: http://qcon.infoq.com/qcon/speakers/show_speaker.jsp?oid=138
 [2]: http://martinfowler.com/bliki/
 [3]: http://www.thoughtworks.com/
 [4]: http://qcon.infoq.com/qcon/speakers/show_speaker.jsp?oid=175
 [5]: http://www.addsimplicity.com/
 [6]: http://www.addsimplicity.com/adding_simplicity_an_engi/2006/11/you_scaled_your.html
 [7]: http://qcon.infoq.com/qcon/speakers/show_speaker.jsp?oid=171
 [8]: http://qcon.infoq.com/qcon/speakers/show_speaker.jsp?oid=114
 [9]: http://jeffsutherland.com/
 [10]: http://en.wikipedia.org/wiki/The_Toyota_Way
 [11]: http://www.agilemanifesto.org/principles.html
 [12]: http://adwords.google.com/
 [13]: http://video.google.com/videoplay?docid=8795214308797356840
 [14]: http://www.infoq.com/
 [15]: http://www.infoq.com/articles/qcon-2007-bloggers-summary
 [16]: http://qcon.infoq.com/