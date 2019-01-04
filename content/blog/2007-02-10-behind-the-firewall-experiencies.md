---
title: Behind the firewall experiencies
author: ferdy
date: 2007-02-10T01:59:16+00:00
url: /blog/2007/02/10/behind-the-firewall-experiencies/
b2007:
  - 02
bcategories:
  - Case
  - MDA
  - SOA
  - Tools

---
Well, I just finished the work I have been involved during the last month. The task consisted mainly to assemble a [RFP][1] document to renew all of our modeling and automatic code generation toolset. Next Monday, we will introduce to some selected providers which are the project objectives and which are the requirements.

Advancing some details, I will tell you that in a first stage we will start designing and developing an infrastructure where all the development tools will rely on. We will also ask to design and develop a tool to model the business logic flow and to automatically generate the code that will execute on a [IMS][2]/[PL/I][3]/[DB2][4] mainframe environment under a property framework (we call this framework “_Application Services Integration_”).

The architecture of this framework could be compared to a [service oriented architecture][5] (<acronym title="Service Oriented Architecture">SOA</acronym>), thought in this case services are coupled, mainly because performance (we have constant peaks of 1.500 tx/s and one requirement is that the response time must be lower than 1 second).

This RFP is our second attempt to renew our development toolset. First attempt, developed under something similar to the [MDA][6] paradigm (or should I say [DSL][7] as we didn’t use [UML][8]?) and based on [Eclipse PDE][9] framework plus a [metamodel][10] that relies on a central repository database, was a complete failure. I will explain the reasons (a forensic analysis) in another post, although it’s about performance and scalability in a geographically disperse environment.

Why I’m telling you this? Well, because I want to share with you similar experiences. Unfortunately, this kind of experiences are usually hidden “_behind the firewall_”, and, in my opinion, it’s positive to share these details with others as we can learn about success and failures (as my manager usually says to me, “_you always must assume that the rest of the people are cleverer than you_”).

 [1]: http://en.wikipedia.org/wiki/RFP
 [2]: http://en.wikipedia.org/wiki/Information_Management_System
 [3]: http://en.wikipedia.org/wiki/PL/I
 [4]: http://en.wikipedia.org/wiki/IBM_DB2
 [5]: http://en.wikipedia.org/wiki/Service-oriented_architecture
 [6]: http://en.wikipedia.org/wiki/Model-driven_architecture
 [7]: http://en.wikipedia.org/wiki/Domain_Specific_Language
 [8]: http://en.wikipedia.org/wiki/Unified_Modeling_Language
 [9]: http://www.eclipse.org/pde/
 [10]: http://en.wikipedia.org/wiki/Meta-modeling