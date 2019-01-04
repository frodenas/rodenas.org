---
title: QCon London 2008 – Summary
author: ferdy
date: 2008-04-27T23:20:56+00:00
url: /blog/2008/04/28/qcon-london-2008-summary/
b2008:
  - 04
bcategories:
  - Conferences
btags:
  - conference
  - qcon
  - Software Development

---
Last month I attended the [QCon London 2008][1] conference, one of the best conferences about software development. I&#8217;ve been very busy after the conference and I didn&#8217;t had time to write my thoughts about some of the sessions I attended until now. In the meantime, [InfoQ][2], one of the organizers, has published a worth read post with some [views and perspectives][3] of other attendees who blogged about this conference. Anyway, here they are my notes:

#### [How Eclipse changed my views on Software Development][4] &#8211; Erich Gamma

Erich started his keynote explaining the [Eclipse][5] evolution, from its inception in 2000 as a closed project, the reaction from the development team when IBM decided to release the code in 2002, the success of the transparency model, to the design of the [Jazz Project][6] in 2006 as a team collaboration platform to integrate all the best practices learned during the years of the Eclipse development.

He talked about how transparency and accountability added an incremental value to Eclipse, and how it&#8217;s related to the Open Commercial Development style, an hybrid development model that takes aspects of both the open and proprietary development models, something that IBM is applying to the Jazz Project and to [Project Zero][7]. He said that <acronym title="Open Commercial Development">OCD</acronym> is more than publishing the source code, it is an open, transparent process, from feature requests and planning through delivery. BTW, this model is very criticized outside IBM due to some misconceptions (developers works for IBM for free).

He described some best practices applied during the Eclipse development, summarized as &#8220;It is about being continuous: Continuous iterative and adaptive planning, continuous design/refactoring, continuous integration/testing, continuous delivering/demos, continuous feedback, continuous learning&#8221;. It&#8217;s what they call the &#8220;Eclipse Way&#8221;, some practices from all kinds of sources (Scrum, RUP, &#8230;) underpinned with values (for example, ship quality on time). But he also said there were some pain points, specially with some boring and painful tasks, and the lack of a integrated tool set.

Then, he explained the Jazz Project, which goal is to be a scalable, extensible team collaboration platform for seamlessly integrating tasks across the software lifecycle, and he finally did a demo about Rational Team Concert, the first product based on Jazz, and asked us to try it by ourselves at the [Jazz.net][6] site.

#### [Amazon Services: Building blocks for true Internet applications][8] &#8211; Jeff Barr

Jeff, Amazon&#8217;s senior web services evangelist, summarized in this session the different services offered by Amazon focused on [Cloud Computing][9]. He explained which are today challenges for a company that operates globally: data centers, bandwidth, operations and scaling. Then, he explained in detail the utility computing services available to users:

  * [Amazon Simple Storage Server (S3)][10]: data storage
  * [Amazon Elastic Compute Cloud (EC2)][11]: virtualized processing capacity
  * [Amazon Simple Queue Service (SQS)][12]: inter-process messages
  * [Amazon SimpleDB (SBD)][13]: distributed data storage

He also said that, unlike what many people think, most users who use their services are large companies. He gave the example that many of the Fortune 500 companies use Amazon&#8217;s infrastructure services to run their development environments.

#### [Keeping 99.95% up time on 400+ key systems at Merrill][14] &#8211; Iain Mortimer

Despite the session title, Iain, Chief Architect at Merill Lynch, talked about how Merrill monitored their systems (about 344 tier 0 & 1 globally disperse servers). Two interesting notes:

  * They implemented their own technology, as none of the vendors was able to guarantee a 99,95% SLA (_eat their own dog food_).
  * They monitor 9 billion messages a day.

#### [Born to Cycle? An Agile Approach to Working][15] &#8211; Linda Rising

Funny session, with lots of participation and a great discussion.

Basically, Linda explained that humans are not designed to be linear, instead we act by pulses: we move between energy consumption and the renewal of the energy consumed. Therefore, we must be able to manage our energy, not our time (see the article &#8220;[Manage your energy, not your time][16]&#8220;, Tony Schwartz, HBR, October 2007). If we can find a balance by establishing a regular rhythm of work and rest, then we will have a higher productivity in a more sustained way. She gave the example of setting four 90-minutes sprints (like the REM sleep cycles) a day, where, in each sprint, we have to concentrate on the work to be done without allowing interruptions, and then rest for 20 to 30 minutes. Anyway, everyone must find his own cycle.

She also explained that if you switch your attention from a primary task to a secondary one, then the time it takes increases 25%. The audience answered explaining that this was a nice statement, but hard to be done. What must we do with email, phone calls or IM interruptions? This question resulted to a funny discussion about a study stating that CNN or BBC tickers reduces <acronym title="Intelligence Quotient">IQ</acronym> by 10%, and someone replied saying that smoking marijuana only reduces IQ by 5%. Session conclusion: is better to smoke marijuana than to watch CNN!

#### [REST: A Pragmatic Introduction to the Web&#8217;s Architecture][17] &#8211; Stefan Tilkov

[Stefan][18] did a great introduction to REST. First, he explained that there are 3 different definitions for <acronym title="Service-Oriented Architecture">SOA</acronym>:

  * An approach to business/IT alignment: driven by business instead of technology, relying on strong governance and implemented using any technology.
  * A technical architecture: service oriented with clearly defined interfaces, and could be technology-independent.
  * Web Services: business data as XML messages implemented using WS-* stack.

Then, he explained 3 different definitions for <acronym title="REpresentational State Transfer">REST</acronym>:

  * An architectural style (the right one): what appears in the Roy Fielding&#8217;s doctoral dissertation.
  * The web used correctly (aka <acronym title="Web-Oriented Architecture">WOA</acronym> or <acronym title="Resource-Oriented Architecture">ROA</acronym>): to use HTTP, URI and other Web standards “correctly”.
  * XML without SOAP: send plain XML via HTTP violating the Web as much as WS-* stack.

After this introduction, he explained the basic principles of REST with some nice examples. He finally stated that there isn&#8217;t any REST vs SOA war, it is REST **for** SOA. There are two visions for SOA, to use REST or to use WS-*. The difference is on the technical layer and on their roots:

> WS-* roots = The Enterprise: &#8220;A gigantic, uncontrollable anarchy of heterogeneous systems with varying quality
  
> that evolve independently and constantly get connected in new and unexpected ways.&#8221;
> 
> REST roots = The Internet : &#8220;A worldwide, publicly accessible series of interconnected computer networks that transmit data by packet switching using the standard Internet Protocol (IP).&#8221;

If you are interested in this presentation, Stefan has put the [slides][19] in his blog.

#### [The Cathedral, the Bazaar and the Commissar: The Evolution of Innovation in Enterprise Java][20] &#8211; Rod Johnson

In this session, Rod started citing some sources of innovation: creativity, experimentation, competition and economic motivations. Then, he detailed the J2EE evolution linking with the innovation factors before commented, with particular emphasis on how the standards established by the <acronym title="Java Community Process">JCP</acronym> resulted on the decline of J2EE.

He compared the JCP with two development models: the Cathedral model, software built by relatively few people, with centralized design; and the Bazaar model, many developers, especially linked to Open Source, who lay out their wares. He stated that neither model is a complete solution: the bazaar model encourages competition but may not produce innovation, and the cathedral model is more likely to produce innovation but doesn&#8217;t produce competition. He finally said that JCP acts like a politburo commissar (they know what’s best for the developers), creating excessive standards and ignoring existing technologies. Something that it&#8217;s actually evolving but that should change much more and much faster if they want to survive.

#### [eBay&#8217;s Architectural Principles][21] &#8211; Randy Shoup

Randy, eBay Distinguished Architect, talked about 4 architectural strategies they use at eBay:

  * Partition Everything: 
      * Split every problem into manageable chunks. eBay uses 2 partitioning patterns: segment databases into functional areas and split databases horizontally.
      * No database transactions (lot of buzz from last year session by Dan Pritchett). Developers must careful order DB operations. And remember: consistency is not always required or possible.
      * No session state, so user session can move through multiple application pools. Transient state is maintained by URL, cookies or scratch databases.
  * Async Everywhere: use asynchronous processing as much as possible, applying message dispatch or periodic batch patterns.
  * Automate Everything: it is better to use automated systems to manual systems. Example: automated tool executes staged roll out, with built-in checkpoints and immediate rollback if necessary.
  * Remember Everything Fails: assume every operation will fail and every resource will be unavailable, so build all systems to be tolerant of failure. eBay enforces that every change must have a rollback plan, because they roll out their entire site every 2 weeks (16,000 application servers in 220 pools).

#### [Functions + Messages + Concurrency = Erlang][22] &#8211; Joe Armstrong 

Great fun with Joe&#8217;s session, the inventor of the [Erlang programming language][23]. He satirized about the reasons that a 25 years old language like Erlang is scheduled in the &#8220;Programming Languages of tomorrow&#8221; track. He told us that Erlang was created by accident, due to the strong requirements from the telecomm industries (severe penalties if the system is unavailable for more than 4 minutes per year).

He explained that functional language is not the most important characteristic of Erlang. What really matters is concurrency and distribution oriented. He gave the example that Moore&#8217;s law is reaching its limit, and how after a 52% power increase in each new CPU architecture prior to 2002, now we are seeing increases of only 20%. He explained that computer architectures are evolving towards: multicore (without success, because applications are still running on a single CPU), cell computers (hard to program) and network on chip (NOC). He also discussed the significant decrease of new CPU&#8217;s power consumption: 850 KW for 1 Tflop in 1997 to 24W for 1 Tflop in 2007.

After that, he explained the Erlang&#8217;s excellences to run on multicore systems, essentially using the [Actor Model][24] paradigm, and the ability to be a fault tolerance language. Finally, he said that every year we will see how sequential programs will be increasingly slower, and for that reason, it is important to be prepared for concurrent-oriented languages.

 [1]: http://jaoo.dk/london-2008/conference/
 [2]: http://infoq.com/
 [3]: http://www.infoq.com/articles/qconlondon-2008-summary
 [4]: http://qcon.infoq.com/london-2008/presentation/How+Eclipse+changed+my+views+on+Software+Development
 [5]: http://www.eclipse.org
 [6]: http://jazz.net/
 [7]: http://www.projectzero.org/
 [8]: http://qcon.infoq.com/london-2008/presentation/Amazon+Services%3A+Building+blocks+for+true+Internet+applications
 [9]: http://en.wikipedia.org/wiki/Cloud_computing
 [10]: http://aws.amazon.com/s3
 [11]: http://aws.amazon.com/ec2
 [12]: http://www.amazon.com/Simple-Queue-Service-home-page/b?ie=UTF8&node=13584001
 [13]: http://www.amazon.com/SimpleDB-AWS-Service-Pricing/b?ie=UTF8&node=342335011
 [14]: http://qcon.infoq.com/london-2008/presentation/Keeping+99.95%25+up+time+on+400%2B+key+systems+at+Merrill
 [15]: http://qcon.infoq.com/london-2008/presentation/Born+to+Cycle%3F+An+Agile+Approach+to+Working
 [16]: http://www.hbsp.harvard.edu/hbsp/hbr/articles/article.jsp?articleID=R0710B&ml_action=get-article&print=true
 [17]: http://qcon.infoq.com/london-2008/presentation/REST%3A+A+Pragmatic+Introduction+to+the+Web%27s+Architecture
 [18]: http://www.innoq.com/blog/st/
 [19]: http://www.innoq.com/blog/st/2008/03/qcon_london_2008_myself_on_res.html
 [20]: http://qcon.infoq.com/london-2008/presentation/The+Cathedral%2C+the+Bazaar+and+the+Commissar%3A+The+Evolution+of+Innovation+in+Enterprise+Java
 [21]: http://qcon.infoq.com/london-2008/presentation/eBay%27s+Architectural+Principles
 [22]: http://qcon.infoq.com/london-2008/presentation/Functions+%2B+Messages+%2B+Concurrency+%3D+Erlang
 [23]: http://en.wikipedia.org/wiki/Erlang_(programming_language)
 [24]: http://en.wikipedia.org/wiki/Actor_model

## Comments

### Comment by martin on 2008-04-29 10:02:33 +0000
Good summary, Ferran (I was waiting for it). That must have been a great conference!

It seems however that some of the talks are slightly redundant from previous years (e.g. ebay&#8217;s one or gamma&#8217;s one). Although very good talks probably rest, erlang, banking experiences, etc. were &#8220;fresher&#8221; subjects.

### Comment by Ferdy on 2008-05-08 00:34:54 +0000
Martin, it was a great conference! eBay&#8217;s talk was a slight different from last year, although same contents. There were some talks more interesting than others (depending on you interests), but always lots of quality on them.