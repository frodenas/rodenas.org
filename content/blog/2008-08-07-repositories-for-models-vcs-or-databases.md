---
title: 'Repositories for Models: VCS or Databases?'
author: ferdy
date: 2008-08-06T23:29:36+00:00
url: /blog/2008/08/07/repositories-for-models-vcs-or-databases/
b2008:
  - 08
bcategories:
  - Case
  - MDD
  - SCM
btags:
  - Case Tools
  - DSL
  - DSM
  - MDD
  - VCS

---
A recent [post][1] from Markus Voelter replying [some][2] [articles][3] from Martin Fowler has resulted in an excellent discussion about repositories for <acronym title="Model Driven Software Development">MDSD</acronym> and textual vs graphical <acronym title="Domain Specific Languages">DSLs</acronym>. I was thinking about joining the discussion in the original post, but as my answer is a bit long to be added as a comment, I&#8217;ll reply him here.

In his post, Markus raised a question that recurrently appears in my thoughts: where is it better to store models? as files in a [VCS][4] (like CVS/SVN) or as structured data in databases?

Unlike Markus, my first answer is usually: without any doubt, in databases. I suppose that this answer has much to do with my professional background, since in the past I [have worked][5] extensively with <acronym title="Computer Aided Software Engineering)">CASE</acronym> tools. Yes, I believe I&#8217;m one of these people that M. Fowler describes in his [post][3] about MDSD:

> The MDSD vision evolved from the development of graphical design notations and CASE tools. Proponents of these techniques saw graphical design notations as a way to raise the abstraction level above programming languages &#8211; thus improving development productivity. While these techniques and tools never caught on too far, the basic core ideas still live on and there is an ongoing community of people still developing them.

But also, it is because I&#8217;m used to working with very large repositories, where there are lots of relationships between models. If you work with lots of components but few relationships, you usually do not have problems working with local files (such as Eclipse does). VCSs are able to deal quite well large amount of files. But what happens when you have, for example, your entire transactional system modeled (> 30,000 components), with a very high index of reusability between models (lots of links), and each model can belong to a different owner (only the owner can modify it)? As Markus points out at the comments:

> Also, text files tend to be a bit hard to scale. Often the minimum you need is some kind of &#8220;cross-indexer&#8221; via a database so you can efficiently cross-ref, search, etc. In a &#8220;real repository&#8221; that&#8217;s easier.
> 
> Consider the Xtext case. What do you do once you have hundreds of Xtext resources? Each linking into each other. How do you efficiently load, unload, search, find-refs, etc? You need some kind of (in memory or persistent) index.

Exactly. When you work with huge amount of data and links, you need to provide some kind of impact analysis or cross-reference functionalities, you must be able to do complex queries, you must version not only the components but also the relationships, and you must be able to link to other models without the need to download them locally. Yes, I know that there are some solutions out there that provide some of those facilities also for files, as text search engine libraries ([Apache Lucene][6]) and query languages (for example, [XQuery][7] for <acronym title="Extensible Markup Language">XML</acronym> or [SPARQL][8] for <acronym title="Resource Description Framework">RDF</acronym>). But IMHO all of these solutions, although they work very well with few components, are not as powerful as what you can get \*for free\* using relational databases.

But I must also say that my opinion has changed somewhat over the years, due to my experience working with repositories. The approach of working with databases also has some problems. One of them is that in order to work with the tool you always must be connected to the database, and, although this situation sounds silly, this may limit the productivity of some developers. With VCS, you only need to be connected while you perform the checkout of the component, but after that, you can work locally with it. Another pain point is that in relational databases, you must to create a fixed schema (no matter if you use a metamodel, you always must create it), and that could be a mess when you need to modify the data structure, since <acronym title="Relational Database Management System">RDBMS</acronym> doesn&#8217;t provide schema versioning facilities. Fortunately, some new approaches has appeared in the market in the last years, as [schema-free][9] databases, that will help in this task. Another side effect is that if you want to preserve the integrity of the models and the relationships, you have to deal with locking mechanisms, so the scenario become worse, and usually, the system tends to be over-engineered. And finally, there are also some functionalities not provided by databases, as versioning, accountability (who, when and what) and in some cases traceability (why), so you must develop it by yourself (yay! we love to reinvent the wheel!). Almost all VCSs provide these facilities.

Let&#8217;s go back again to the original post. Markus talks about some conditions where repositories could fit well in this scenario:

> My point is that a repository is not per se a bad thing, provided the following criteria: (1) you store all your relevant stuff in it (2) it provides versioning facilities (3) supports diff/merge on a meaningful abstraction level.

Ummm, I agree with almost everything, but I&#8217;ve some concerns:

  1. Not sure, if he talks about storing all of the data that belongs to a model in the repository, then I agree. But if he talks about storing the model and the code together, then I disagree. There are some scenarios where this is not convenient. For example, when you want to be platform independent (and I&#8217;m not talking about all the <acronym title="Model-Driven Architecture">MDA</acronym> stuff). The various parser/generator/interpret could run and store the code/binary on several platforms, and not always the same platform where you store the model.
  2. I agree, versioning is an essential facility.
  3. Diff/Merge works well with textual DSL&#8217;s, with a concrete syntax. But, although this is a great feature, is it mandatory? I have worked a long time without this feature and I assure you that you can survive without it. And what happens with graphical DSLs?

Before concluding, I would also like to comment one of the latest projects where [we applied][10] MDSD. At this project, we decided to use a [Oracle XML DB][11] to store our models in XML (something like to what [Eurocontrol-CFMU][12] [have done][13] for their <acronym title="Unified Modeling Language">UML</acronym> models), but we added also some [metadata][14]. By storing the XML directly in the database, we avoid the need to decompose the XML into a relational schema, and allow developers to download the XML and work locally without the need to be connected to the database. We could use also all the <acronym title="Structured Query Language">SQL</acronym> query facilities, and for those situations where the performance could be a problem, then we use the metadata to store some relevant data and relationships. Oh, and this RDBMS provides us also with versioning facilities. At this moment, we don&#8217;t have enough data in the repository to tell you if this approach will be a success or not. Let&#8217;s see!

To sum up (or not!). I believe you should never reject the database approach (nor the VCS option). I can not give you a &#8220;Golden Rule&#8221;, but my advice is that if you are not going to have lots of relationships between models, then use the VCS approach. If not, then analyze first what a VCS approach could offer you, and if it doesn&#8217;t fit well with your requirements, then use the database approach. But please, be careful and don&#8217;t tend to design the metamodel too much complicated, or you could have lots of performance problems.

As the post is quite long, I will leave for another post my thoughts about textual vs graphical DSLs. In the meantime, what is your opinion? I would love to hear stories from other folks on what people are doing in their companies.

 [1]: http://voelterblog.blogspot.com/2008/07/replying-to-martin-fowlers-recent-co.html
 [2]: http://martinfowler.com/bliki/MDSDandDSL.html
 [3]: http://martinfowler.com/bliki/ModelDrivenSoftwareDevelopment.html
 [4]: http://en.wikipedia.org/wiki/Version_control_system
 [5]: http://www.rodenas.org/blog/2006/11/07/object-oriented-case-tools-lost-opportunities-and-future-directions/
 [6]: http://lucene.apache.org/java/docs/
 [7]: http://www.w3.org/TR/xquery/
 [8]: http://www.w3.org/TR/rdf-sparql-query/
 [9]: http://www.rodenas.org/blog/2008/02/19/playing-with-couchdb/
 [10]: http://www.rodenas.org/blog/2007/02/10/behind-the-firewall-experiencies/
 [11]: http://www.oracle.com/technology/tech/xml/xmldb/index.html
 [12]: http://www.cfmu.eurocontrol.int/
 [13]: http://www.oracle.com/technology/oramag/oracle/06-jan/o16xml.html
 [14]: http://en.wikipedia.org/wiki/Metadata

## Comments

### Comment by Steven Kelly on 2008-08-07 16:02:52 +0000
Great to see people writing on this topic based on extensive experience of actual real world projects and tools! I&#8217;ve added my own 2c worth on the topic of RepositoryBasedCode in my blog &#8211; like you, I have over 15 years experience, so like you, it&#8217;s too long for a comment :-)!
  
<a href="http://www.metacase.com/blogs/stevek/blogView?showComments=true&#038;entry=3395579842" rel="nofollow">http://www.metacase.com/blogs/stevek/blogView?showComments=true&entry=3395579842</a>

### Comment by Ferdy on 2008-08-08 01:20:33 +0000
Steven, glad to see you here. 

I&#8217;ve read your post and I agree with you. I believe that working with a repository usually is easier than a VCS when multiple users are involved, but it also depends on the number of relationships between models. On the other hand, I believe that locking mechanisms can become very dangerous, so I definitely agree with your last sentence: &#8220;the best kind of conflict resolution is to avoid conflict in the first place!&#8221; 🙂