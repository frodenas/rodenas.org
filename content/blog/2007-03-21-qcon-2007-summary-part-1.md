---
title: QCon 2007 summary – Part 1
author: ferdy
date: 2007-03-20T23:56:24+00:00
url: /blog/2007/03/21/qcon-2007-summary-part-1/
b2007:
  - 03
bcategories:
  - Conferences

---
Finally I found some time to write about the [QCon 2007 conference][1] held last week in London. I think it was a great conference. As usual, there were some poor sessions (I had high expectations about some speakers and contents), but there were also some interesting ones.

So, here it is the first part of the summary (3rd day):

&#8220;[The eBay Architecture – Striking a balance between site stability, feature velocity, performance and cost][2]&#8220;: [Dan Pritchett][3] (eBay Technical Fellow) talked about some interesting eBay&#8217;s architecture features, as how they deal with vertical DB segmentation (by functional areas) and horizontal DB splits (date, location, &#8230;), and, how they don&#8217;t use stored procedures, triggers and, amazing, nor transactions (Martin Fowler is talking about this in his post [Transactionless][4]). This means that all business logic is executed by the application (sorts, joins, referential integrity, &#8230;). They use intensively prepared statements an bind variables (cached by datasources). They also scales using a rewritten connection pool and an internally developed <acronym title="Object Relational Mapping">ORM</acronym> solution called DAL (Data Access Layer). All <acronym title="Create, Read, Update and Delete">CRUD</acronym> operations are executed through this infrastructure. If you are interested in reading the full presentation, Dan has [posted it][5] (PDF) at his site.

&#8220;[Developing Expertise: Herding Racehorses, Racing Sheep][6]&#8220;: [Dave Thomas][7] ([The Pragmatic Programmers][8]), started his speech asserting that process improvement requieres PEOPLE improvement (he recommends to read Capers Jones assessments and benchmarks). Using the Dreyfus Model of Skills Acquisition, he described, on a funny way, the characteristics of people on different stages (Novice, Advanced beginner, Competent, Proficient, Expert). He stated that the vast majority of developers are on Stage 2, and we need to raise the bar. He advocates to use Dreyfus to fix companies and to fix our careers, and also, learn and apply financial management to our daily work (have a plan, diversify, look for value, be active, &#8230;).

I have also uploaded some photos to [Flickr][9], although you will find more photos, including my photos, at the [QCon 2007 Group Photo Pool][10].

 [1]: http://qcon.infoq.com/qcon/conference/
 [2]: http://qcon.infoq.com/qcon/speakers/show_speaker.jsp?oid=175
 [3]: http://www.addsimplicity.com/
 [4]: http://martinfowler.com/bliki/Transactionless.html
 [5]: http://www.addsimplicity.com.nyud.net:8080/downloads/eBaySDForum2006-11-29.pdf
 [6]: http://qcon.infoq.com/qcon/speakers/show_speaker.jsp?oid=122
 [7]: http://pragdave.pragprog.com/pragdave/
 [8]: http://www.pragmaticprogrammer.com/
 [9]: http://www.flickr.com/photos/ferranrodenas/sets/72157600004554245/
 [10]: http://www.flickr.com/groups/305032@N24/

## Comments

### Comment by diana plesa on 2007-03-22 10:47:23 +0000
Thanks for blogging about QCon! I just wanted to let you know that we quoted and linked from this entry on the over all QCon 2007 blogger&#8217;s key takeaway points and lessons learned article: <a href="http://www.infoq.com/articles/qcon-2007-bloggers-summary" rel="nofollow">http://www.infoq.com/articles/qcon-2007-bloggers-summary</a>

Feel free to link to it and of course blogging about this articles existence would help even more people learn from your and other bloggers takeaways.

Thanks again!

Diana
  
InfoQ/QCon