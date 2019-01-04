---
title: From the Eclipse Platform to the IBM Rational Jazz Platform
author: ferdy
date: 2009-04-19T23:05:18+00:00
url: /blog/2009/04/20/from-the-eclipse-platform-to-the-ibm-rational-jazz-platform/
b2009:
  - 04
bcategories:
  - Collaboration
  - Eclipse
  - History
  - IBM
  - IDE
  - Tools
btags:
  - Collaboration
  - Eclipse
  - Integration
  - Jazz Project
  - Rational
  - Tools

---
Several months ago, I promised to write about the [IBM Rational Jazz platform][1] and [IBM Rational Team Concert][2]. As you may have noticed, I have not yet write about them, but in my defense I can say that I have not had much time to devote to this nor other posts in this blog. As I mentioned in some others posts, lately I have been leading a major renovation of our entire suite of custom development tools, and these last 3 months I have been fairly busy managing all this change. Taking advantage of Easter holidays, I finally found the right time to get to write about the Jazz platform.

But before proceeding, a disclaimer. What I am going to write about Jazz is just a personal opinion, may or may not be wise, may or may not have something to do with reality, but I want to make clear that this is an entirely personal opinion, and do not mean any endorsement from my current employer.

#### The Eclipse vision

To describe the Jazz platform, I think we should go back to the past, because in my opinion, Jazz is trying to evolve the vision/mission/wildest dream that [Lee Nackman][3] had in 1998: to create a single technology platform on which to build the various IBM&#8217;s application development tools. The objectives Lee had at that time were:

  1. to solve one of the most customer complaints: instead of having tools with their own &#8220;personality&#8221;, customers demanded a common look and feel;
  2. to be able to integrate different tools, especially from IBM, but also from external <acronym title="Independent Software Vendor">ISV</acronym> in order to complement IBM&#8217;s product line;
  3. all reducing the development costs, as at that time each IBM tooling group used its own specific platform.

With the help from the autonomous [OTI][4] subsidiary (acquired by IBM in 1996), and overcoming an enormous amount of skepticism within IBM, Lee and his team delivered a technology platform that became what today is known as the [Eclipse platform][5]. Looking at the success of this platform, especially in terms of IBM adoption across the different brands and tools, it seems that the main objectives were reached. Not to mention also that open sourcing the platform and several projects (as the [JDT][6]), they killed lots of competitors, [shrinking the Java tools market][7], and created a great ecosystem around it.

#### The Eclipse vision revisited

But the knowledge and tool set that IBM acquired when they bought [Rational Software][8] in 2002, mixed with a retrospective analysis they did based on the experience they gained in the Eclipse development, helped them to figure out which were the new challenges for the software delivery process. I&#8217;ll try to summarize, <acronym title="in My Humble Opinion">IMHO</acronym>, some of the improvements they realize:

  * When IBM built Eclipse, their focus was on the developer productivity. But the software development process usually involves some more skills, specialists, roles, levels, &#8230; and they need to work together, they need to share information, and when all members of the team work in a [geographically dispersed][9] manner, the conflicts inevitably appears. So there is a need to involve all the team in all the phases of the software lifecycle regardless of their location and role, and instead of improving the productivity of the developer, we need tools to improve the productivity of the entire team, and directly or indirectly, the productivity of the whole organization.
  * When talking about covering the overall development cycle, we usually find that we need several tools, and sometimes these tools are outside of the scope of Eclipse. And we also find that there are lots of barriers to share resources between these heterogeneous tools, as they use private vocabularies, formats and stores. So the integration between these external tools are usually built on bridges, and lots of times, highly cobbled (so they require updates with every interface change). There is a need to raise the level of integration. We need to be able to integrate and share cross-repository information using open interfaces and a loosely coupled approach.
  * When thinking about non coding activities, we realize that not each role or tool needs a heavy desktop client. There are some situations where a web <acronym title="User Interface">UI</acronym> (or another type of client) is more suitable. Despite some incubators ([e4 Bespin][10] or [Eclifox][11]), Eclipse nowadays only supports its desktop client. It&#8217;s true that using [Equinox][12] and its underlying [OSGi][13] services, you can deploy Eclipse plugins into the server-side, but there isn&#8217;t any &#8220;standard&#8221; way to share user interfaces or a framework for the web UI. Which will be the problem? the same Lee discovered in 1998: tools with their own &#8220;personality&#8221;, tools without a common behavior.
  * Process, process and process. How much we love them and how much we hate them also? Why is so hard to try to follow a process? Why the only Eclipse tools available ([RMC][14] or [EPF][15]) only try to author and then publish a static document? Why tools doesn&#8217;t live the process?
  * Creating a new Eclipse environment with all of the required plugins, configuring the project, setting-up the build process and all the other little pieces that come into play to give code life could be a mess for a new team member. This kind of manual tasks are tedious and error-prone, and they are perceived by developers as a waste time. So it is not strange that tools like [Maven][16] had a great adoption.

So in my opinion, and as I told previously, the Jazz platform is the evolution of the original Eclipse vision, keeping in mind the above and some more other concerns, with an special focus on teams and collaboration. But its aim is not to replace Eclipse, they are distinct platforms with different goals, although Jazz seems to be the perfect complement to Eclipse. This new vision is well summarized at the [About Jazz][17] page:

> Our goal is to provide a frictionless work environment that helps teams collaborate, innovate, and create great software. To that end, **we are focusing on driving fundamental improvements in team collaboration, automation, and reporting across the software lifecycle**. 

#### The Jazz Platform

When trying to describe what compose the Jazz platform, albeit IBM have split the original Jazz project in several projects at the [jazz.net][1] site, I still have some problems trying to draw the line between the platform and the applications, to see which components are part of the Jazz platform and which are part of the different products based on it. So I will try to use the below picture, that I have borrowed from the IBM Rational guys, in order to clarify my ideas:

<center>
  <img src="/blog/images/2009/04/jazz-platform.jpg" alt="The Jazz platform" title="The Jazz platform" width="600" height="351" class="aligncenter size-full wp-image-691" />
</center>

To enable a seamless and higher level of integration between tools, IBM has defined a reference architecture, <acronym title="Application Programming Interface">API</acronym> specifications, and a set of common services and tool building blocks, that together are called the [Jazz Integration Architecture][18] (JIA). At the center of this integration architecture we found the Jazz Team Server (that may consist of one or more physical servers that act together as a single logical server), which provides foundational services ([RESTful web services][19]) to enable groups of tools to work together. Let&#8217;s summarize each of these foundational services:

  * **Presentation**: in a multi-tool integration scenario we usually found lots of linked resources that may not be familiar to a particular client tool or this tool may not be able to provide a user interface for theses resources. The services provided by the presentation foundational services enables a client tool to find and invoke a suitable user interface for any resource URL in order to present the relevant data. There are also two main components (I believe, but I am not sure, they belong to the presentation services) that allow tools developers to implement specific user interfaces: the web dashboards component, that provides the infrastructure and UI for creating and presenting dashboards in a web browser, and the web UI component, that provides a framework for rich web user interfaces (based on the [Dojo toolkit][20]).
  * **Process enactment**: these are the services that allows to define and implement a wide range of processes. It is focused on agile processes, but it can also be used in highly-structured processes, as it provides the essential components of a development work flow, such as operations, roles, permissions, preconditions or follow-up actions. By default, it is packaged with several process, as [Scrum][21], [OpenUp][22] or the [Eclipse Way][23] (PDF), and it has an editor to be able to modify the process configuration. Each time you create a project you must assign a process, but you can have several projects and each project can follow a different process. It governs all activities, artifacts, artifact relationships, and operations that are pursued within the context of the process area, and it works in a seamless and unobtrusive way, as it manifests itself through artifacts types, operations manipulating the artifacts, and artifact change events.
  * **Administration, users, projects, teams**: For dealing with users, projects, security, and licenses, each server hosts a set of core administration services. For example, these services can provide a common user identity in order to support authentication (establishes user identity) and authorization (a particular operation can be performed) based on the team membership or role in a project.
  * **Collaboration**: Collaboration between the team members of a project can be performed in real-time, but also asynchronously (especially important for teams working across time zones). It also occurs at different contexts: around tools, process, tasks or data elements. The collaboration services in the Jazz platform supports and enables some of these core functions, for example, instant messaging, sending email and SMS, maintaining subscriptions, etc. It is something like a mix of the Eclipse [ECF][24] and [Corona][25] projects (and I wonder why they did not use these projects).
  * **Storage, data warehouse and search**: You may have noticed that I have deliberately grouped 3 core foundation services in only one. The reason is because the Jazz repository model is composed by three logical DB in one, working together in order to provide the above 3 services. I am going to use another &#8220;stolen&#8221; picture to describe it:
  
      
    <center>
      <img src="/blog/images/2009/04/jazz-repository.jpg" alt="Jazz Platform Repository" title="Jazz Platform Repository" width="500" height="199" class="aligncenter size-full wp-image-833" />
    </center></p> 
    
      * Instead of having a fixed schema (that make integration hard) or a very generic schema (that makes writing tools tough), the Jazz repository allows tools to store their data their way. So content resources are created in a particular representation by the client, and can only be retrieved in that representation. The server doesn&#8217;t know enough about the content to transform it into an alternate representation. The storage services provides a completely RESTful framework for <acronym title="Create, Read, Update and Delete">CRUD</acronym> operations on resources stored in the Jazz private DB.
      * For every resource stored in the private DB, there are a set of “indexed properties” that are stored automatically in another DB using [RDF][26]. The indexing process is able to extract [RDF triples][27] from some resource representations and able to extract text streams from some resource representations as well. This process extracts asynchronously each tool&#8217;s data into searchable indexes, consolidates them, and provides centralized query services for searching across the consolidated index. In this way, the search foundation services are able to provide common queries, both structured queries (based on [SPARQL][28]) and full text search (based on [Apache Lucene][29]).
      * And finally, we find the data warehouse DB, a periodically snapshot of all the information, used for public reporting. The data warehouse services relies on the Eclipse [BIRT][30] project for its reporting system.

Anyway, the Jazz platform is still in its early stages, and it is constantly evolving to meet additional challenges. What I have summarized previously is what it is know as the Jazz Platform 0.6, but a new version is expected to be delivered on June with a new name, the [Jazz Foundation][31]. So if you are interested in more deep details about the above or new services that are going to be delivered, I recommend that you go through the development team [wiki][32] (registration required).

#### The killer-application

There is also an interesting parallelism between how Eclipse and Jazz has been developed. In order to convince other IBM&#8217;s development tools product managers to adopt the Eclipse platform, Lee and his team decided to build a Java IDE. There were two reasons behind that decision: 1) to provide a real example (a killer-application) of a tool developed on the platform, proving in that way its benefits; 2) to help the Eclipse development team to better understand the needs of future consumers of the platform and to discover areas that required further development. This strategy was a success and the Eclipse platform and the Java IDE were quickly adopted inside IBM.

The Jazz project seems to use the same kind of strategy. They are developing a real tool using the Jazz platform. This killer-application is called [Rational Team Concert][2] and as far as I know it is also rapidly adopted inside IBM. I hope to write about this product in the near future.

#### Adoption

Looking at the [jazz.net][1] site the increasing number of IBM tools that are adopting the Jazz platform, I have no doubt that it will be another success in terms of IBM adoption. But &#8230;

  * Will it be a success outside IBM as was the Eclipse platform? IBM has not contributed the Jazz platform to the open source world (in terms of a [free software license][33]), and nor it is licensing it in any way (as far as I know). The only way to get this platform is licensing some of the Jazz based products. I am sure they are going to attract some more new customers looking for a complete lifecycle solution, but I believe it will not be a great success as Eclipse was. Anyway, I think the current goal for the Jazz platform is different from the Eclipse platform goal.
  * Are ISVs going to adopt this platform for their own products? There are the usual [business partners][34] that are complementing/extending the IBM&#8217;s Jazz based products with some new features, but it does not seem that they are going to adopt the Jazz platform for their own products. And it does not seem that IBM is trying to convince them to adopt the platform, as they did with Eclipse, or licensing it on an <acronym title="Original Equipment Manufacturer">OEMs</acronym> basis.
  * Will this platform attract external developers? IBM is not encouraging them to contribute in terms of code (the rights of what you contribute are transfered to IBM). They are only encouraging people to influence the direction of products through direct, early, and continuous conversations at the [jazz.net][1] website. So it will be very strange to see any non-customer developer.

So in terms of external adoption/extension, it seems that IBM is focusing only in the interface as a way to integrate non-IBM tools, encouraging developers, customers and ISVs to participate in the development of the [Open Services for Lifecycle Collaboration][35] initiative, something like an open standards consortium.

#### Conclusion

Starting looking at the original Eclipse vision and how IBM revisited it after the Rational Software acquisition and the Eclipse success, I have attempted in this post to describe what it is the Jazz platform. I am sure some of you have realized that some of the improvements that I have described previously can be easily or are already implemented through Eclipse plugins, but I think these are the minor ones. There are three main conceptual differences between Eclipse and Jazz:

  * a server centric approach instead of a local workbench in order to leverage the team concept;
  * a persistent storage using a federated cross-linked repository to store resources;
  * a seamless integration between tools using standard loosely coupled open interfaces and web protocols.

And in my opinion, these conceptual differences can only be implemented through the creation of a new platform. Instead of solving some particular problems in an isolated way, Jazz is trying to attack the essence of the software development process. Does it means that we must convert to a new religion, drop the Eclipse platform and adopt the Jazz platform? No, Jazz is not going to replace Eclipse. There will be a strong relationship between the Jazz and Eclipse environments, yet the
  
two are distinct and can run independently. Jazz is going to complement Eclipse in some particular scenarios:

> Eclipse for Individuals, Jazz for Teams 

We have also seen that IBM&#8217;s decision is not to open source this new platform, but to create a community around the [jazz.net][1] and [OSLC][36] websites. However, it will need to attract a broad and active participation from a wide external community in order to be a great success outside IBM, as it was Eclipse, something that I believe it is not a current IBM goal.

What will happen in the future? Sincerely, I don&#8217;t know, time will decide. From my particular point of view, this new vision match up what we have been doing for a long time and that has lead us to extend the Eclipse platform in order to create a [custom collaborative tool set][37]. So, as we are already an IBM Rational customer and we have licensed some of the Jazz products, I will be very happy if we can integrate, in an easy way, our custom tools with the IBM Rational tool set.

#### If you reached this point, please, participate in the conversation 🙂

Before concluding this long post, I would like to ask you:

  * To the IBM/Rational guys: As I assume that I could make mistakes (history, goals, &#8230;) , if you want to add or point out something wrong, please write me, better as a comment in this post although I will also accept private emails, and I will correct it.
  * To the non IBM/Rational guys: 
      * How much of you have heard about Jazz? How much of you have experimented with it? Which is your (technological) opinion?
      * Must IBM open source the Jazz platform? Do you think it will be interesting and wide adopted? Why?

#### Additional information

<small>PS: One of the latest tasks Lee Nackman did before his retirement at IBM, was to help spur the development of the Jazz platform.</small>

<small>PS: Most of the people actually involved in the development of the Jazz project were part of the Eclipse platform development team, so it is not strange to see that they are applying the same strategy, but also adopting the best practices they learned during the Eclipse development process.</small>

<small>PS: There is an excellent case study on IBM’s strategy and process for creating Eclipse at the <a href="http://harvardbusinessonline.hbsp.harvard.edu/b02/en/common/item_detail.jhtml?id=906007">Harvard Business School</a>. It&#8217;s a worth read.</small>

<small>PS: Another interesting read is a paper on <a href="http://www.booch.com/architecture/blog/artifacts/CDE.pdf">Collaborative Development Environments</a> (PDF) by <a href="http://en.wikipedia.org/wiki/Grady_Booch">Grady Booch</a> and <a href="http://www.alanbrown.net/">Alan W. Brown</a>, which seems to be the &#8220;spark&#8221; that started the new vision.</small>

 [1]: https://jazz.net/
 [2]: http://www-01.ibm.com/software/awdtools/rtc/
 [3]: http://www.nackman.com/lee-s-resume
 [4]: http://en.wikipedia.org/wiki/Object_Technology_International
 [5]: http://www.eclipse.org/platform/
 [6]: http://www.eclipse.org/jdt/
 [7]: http://www.infoworld.com/d/developer-world/shrinking-java-tools-market-855
 [8]: http://en.wikipedia.org/wiki/Rational_Software
 [9]: http://en.wikipedia.org/wiki/Virtual_team
 [10]: http://wiki.eclipse.org/E4/Bespin
 [11]: http://www.alphaworks.ibm.com/tech/eclifox
 [12]: http://www.eclipse.org/equinox/
 [13]: http://en.wikipedia.org/wiki/OSGi
 [14]: http://www-01.ibm.com/software/awdtools/rmc/
 [15]: http://www.eclipse.org/epf/
 [16]: http://maven.apache.org/index.html
 [17]: https://jazz.net/learn/about-jazz-objectives.jsp
 [18]: https://jazz.net/development/DevelopmentItem.jsp?href=content/project/plans/jia-overview/index.html
 [19]: http://en.wikipedia.org/wiki/Representational_State_Transfer
 [20]: http://www.dojotoolkit.org/
 [21]: http://en.wikipedia.org/wiki/Scrum_(development)
 [22]: http://en.wikipedia.org/wiki/OpenUP
 [23]: http://www.eclipsecon.org/2005/presentations/econ2005-eclipse-way.pdf
 [24]: http://www.eclipse.org/ecf/
 [25]: http://www.eclipse.org/corona/
 [26]: http://en.wikipedia.org/wiki/Resource_Description_Framework
 [27]: http://www.robertprice.co.uk/robblog/archive/2004/10/What_Is_An_RDF_Triple_.shtml
 [28]: http://en.wikipedia.org/wiki/SPARQL
 [29]: http://lucene.apache.org/
 [30]: http://www.eclipse.org/birt/phoenix/
 [31]: https://jazz.net/development/DevelopmentItem.jsp?href=content/project/plans/jf-plan-1.0.html
 [32]: https://jazz.net/wiki/bin/view
 [33]: http://en.wikipedia.org/wiki/Free_software_license
 [34]: https://jazz.net/community/ensemble/index.jsp
 [35]: https://jazz.net/open-services/
 [36]: http://open-services.net/
 [37]: http://wiki.eclipse.org/EclipseBankingDayLondon/SessionAbstracts#Repository_Based_Application_Development_Environment_for_Banking_Systems

## Comments

### Comment by Scott Rich on 2009-04-20 17:28:24 +0000
I&#8217;d say you&#8217;ve got it, Ferdy. I know you&#8217;ve had more access to the Jazz team than the average person, but I hope some credit goes to the open-ness of the project, and that you&#8217;re not alone in understanding the Jazz vision.

### Comment by Ferdy on 2009-04-21 02:03:15 +0000
Scott, thanks for dropping by.

It&#8217;s true that I&#8217;ve had some access to your team, but all the information I gathered for this post is available through the jazz.net <a href="https://jazz.net/wiki/bin/view" rel="nofollow">wiki</a>, or at <a href="http://billhiggins.us/weblog/" rel="nofollow">Bill&#8217;s blog</a>, or at <a href="http://www.ibm.com/developerworks/blogs/page/johnston" rel="nofollow">Simon&#8217;s blog</a>, or on <a href="http://twitter.com/JazzDotNet" rel="nofollow">twitter</a>, or on <a href="http://www.infoq.com/presentations/Eclipse-Lessons-Erich-Gamma" rel="nofollow">InfoQ</a>, &#8230; 

So, yes, ALL credit goes to the open-ness of the project. I&#8217;ve expressed my opinion <a href="http://www.rodenas.org/blog/2008/05/07/transparency-in-software-development/" rel="nofollow">several</a> <a href="http://twitter.com/ferdy/status/1251548904" rel="nofollow">times</a>. I want more Rational projects using the transparent development process.

### Comment by Theju Mudda on 2009-04-30 11:49:27 +0000
Thanks for the article! It gives a nice overview on Jazz platform and how it is different from Eclipse.

### Comment by Frank Gerhardt on 2009-05-05 17:48:26 +0000
> How much of you have heard about Jazz? How much of you have experimented with it? Which is your (technological) opinion?

I think it&#8217;s great. The design can be taken as a blueprint for mulit-user RCP applications. I would prefer RAP for the web UI but RAP was not available at that time they started it. 

> Must IBM open source the Jazz platform? Do you think it will be interesting and wide adopted? Why?

Yes, or adoption will be minimal outside of IBM. Tool vendors and ISV will not buy into it otherwise. To apapt their tools/software they will rather put a Jazz isolation layer around their code. Given that the Jazz team must be quite busy with developing the product, there might just not be enough time available for evangelizing the community. For Eclipse, community building was a project in itself, consuming quite a bit of frequent flyer miles. I hope will will see similar efforts for Jazz. What will not help is IBM sales people doing road shows. That does not &#8220;sell&#8221; the platform to developers and architects. I guess Erich Gamma needs to do that again.

But I can&#8217;t answer \*why\* IBM should open-source the platform. They must have a goal &#8211; I don&#8217;t see one. A killer app needs to kill something. Eclipse killed all the other Java IDEs and only let VisualStudio co-exist. What thing should Jazz or RTC kill? It&#8217;s not an established market, unlike the Java IDEs. It&#8217;s a new market and you win by being the first and best since there are not others to kill. Sorry about using the k-word so often.

My background is RCP development. I would REALLY welcome the Jazz platform for developing multi-user business applications. I have done a lot of custom inhouse special user management, persistence, remoting, web services etc. I just don&#8217;t see why IBM would give me that present for free. 😉 Please! 

Today you can&#8217;t use the Jazz platform at all for custom development. That&#8217;s the worst of all. Or you make your users buy RTC for 50k+client licences and bundle your application inside of that&#8230; Obviously not a option. Even a commercial licence would make sense, if the platform gives me a productivity boost. On the other hand, many productivity booster like Spring can&#8217;t be sold &#8211; they must be open-source for a community to adopt them.

### Comment by Adrian Cho on 2009-05-07 06:00:20 +0000
Great article Ferdy. A couple of details you may want to know on the licensing front. You&#8217;re right that the Jazz Foundation and RTC are not made available under an open source license. We&#8217;re using many of the open source practices learned from Eclipse to develop the software in an open and transparent manner but it&#8217;s very much a commercial offering when it comes to the licensing. That said:

We make all the source code for RTC available with each build. You can modify this for your own internal use but you cannot redistribute it.

We offer free RTC licenses for academic researchers, educators and open source projects (<a href="https://jazz.net/community/academic/" rel="nofollow">https://jazz.net/community/academic/</a>).

### Comment by Bob Gulledge on 2010-06-02 22:04:44 +0000
Has anyone tried to integrate their own tools as a domain service provider ala OSLC? Has anyone attempted to federate between two domain service providers in the same domain space (eg. Clearcase and Quality Center)?

I think the concept is interesting with a lot of potential, but the complexities of implementing something like this in a large enterprise with heterogeneous vendor tools.

### Comment by Ferdy on 2010-06-03 00:33:47 +0000
Bob, beyond Rational Jazz based products, on the CM space <a href="http://www.eclipse.org/mylyn/" rel="nofollow">Mylyn</a> is <a href="http://www.eclipse.org/org/press-release/20100308_mylyn.php" rel="nofollow">supporting</a> OSLC.

I agree with you that it could be a complex approach (format, semantics, agree on a standard, &#8230;), it has its strengths and weaknesses, but integration has never been an easy task, specially, as you mention, with heterogeneous vendor tools.

### Comment by Bob Gulledge on 2010-06-03 14:47:26 +0000
I understand there are to be new announcements at the IBM Rational Conference next week that will add more vendors to the list of partners. I am anxious to see that list.

I am also anxious to see if there is any indication IBM will make the Jazz Foundation Services truly open. As the author indicated, I see that as a major obstacle to cross-vendor adoption.