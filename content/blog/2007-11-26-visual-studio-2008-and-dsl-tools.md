---
title: Visual Studio 2008 and DSL Tools
author: ferdy
date: 2007-11-25T23:17:02+00:00
url: /blog/2007/11/26/visual-studio-2008-and-dsl-tools/
b2007:
  - 11
bcategories:
  - IDE
  - MDA
  - MDD
  - Microsoft
btags:
  - DSL
  - DSM
  - MDA
  - MDD
  - Microsoft
  - Visual Studio

---
Surely, by the time you read this you will have already read it. Last week, Microsoft released [Visual Studio 2008][1] (codename Orcas).

But what has not been announced are the changes in [DSL Tools][2] for VS2008, mainly because there are not any new major features except some changes in the runtime, support for [LINQ][3] and lots of bug fixing. Anyway, if you are interested, [Stuart Kent][4], Senior Program Manager with the Visual Studio Ecosystem team, summarizes them in a [blog post][5], and most interesting, he also describes the [roadmap][6] for the next version of Visual Studio (codename Rosario).

I&#8217;m personally interested in DSL Tools mainly for two reasons. First, because last summer I finished my degree thesis about [Model Driven Development][7], where I&#8217;ve been analyzing at length [Domain-Specific Modeling][8] and [Model-Driven Architecture][9] methodologies. Among other tools, I analyzed the DSL Tools that were part of the VS2005, and I found them one of the best and most advanced tools for designing domain specific graphical notations (as opposed to textual notations, which, depending on the domain problem, are better suited) and for generating code from models. The main problem I saw in this tool was the lack of support for <acronym title="Unified Modeling Language">UML</acronym> and <acronym title="XML Metadata Interchange">XMI</acronym>. I&#8217;m not a big fan of UML, but I must recognize that, in some cases, a common modeling language helps a lot, specially to reduce the learning curve that it is inherent to all DSLs. I know that this statement sounds opposed to the main concept of <acronym title="Domain-Specific Language">DSL</acronym>, so I will address you to the article &#8220;[Unified or Domain-Specific Modeling languages?][10]&#8221; (thanks [Metacase][11] for recovering this article), by [S. Ambler][12], who explains this contradiction very well. Also, the lack of support to XMI limits the interoperability between tools, something I believe Microsoft is not worried at all. Despite of these problems (<acronym title="In my humble opinion">IMHO</acronym>), I believe Microsoft has done a really bad job of publicizing this tool, which is one of the pillars of Microsoft&#8217;s [Software Factories][13] initiative.

By the way, if you are interested in <acronym title="Model Driven Development">MDD</acronym>, I would recommend you [openArchitectureWare][14], now part of the [Eclipse GMT Project][15], which is using an hybrid model, since it uses both approaches (<acronym title="Model-Driven Architecture">MDA</acronym> and <acronym title="Domain-Specific Modeling">DSM</acronym>), and it allows both graphical and textual notations. And it is FREE!!!. Just check the [overview diagram][16], so you get an idea of which technologies supports.

The second reason why I&#8217;m interested in DSL Tools is because we have successfully applied some external and internal DSLs at work (see this [post][17] by M. Fowler to know the differences between external and internal DSL). For a long time, we have been using textual internal DSL&#8217;s ([PL/I Macros][18]) in order to improve the quality of the code and to abstract the developer of some complex parts of the system, and we are very satisfied with the results. And more recently, we have been using graphical external DSL&#8217;s to represent the models for the online transactions which runs on our main backend (a [z/OS][19] mainframe) and to generate code addressed specifically to an in-house runtime framework. Last year, when we submitted an <acronym title="Request for Proposal">RFP</acronym> to renew our domain-specific tool set, we received several proposals from different vendors, and one of them came up with DSL Tools. We finally decided not to use this tool and, instead, use [Eclipse][20] and a modified version of the [jBPM plugin][21]. Anyway, as I told you before, I consider DSL Tools one of the most advanced tools for DSM, so, periodically, I try to learn which is the evolution of this tool. And just for your curiosity, here it is the DSL design for our main mainframe architecture using the DSL Tools Designer (yes, it&#8217;s a service orchestrator!):

<center>
  <a href='/blog/images/2007/11/dsl-tools.jpg' title='DSL Tools'><img src='/blog/images/2007/11/dsl-tools.thumbnail.jpg' alt='DSL Tools' /></a><br />
</center>


  


And now to conclude, I am really interested in knowing if someone has a real experience using DSL&#8217;s. If this is your case, are you using VS DSL Tools? If not, which tools are you using?

BTW, if you are interested in the thesis document, just drop me a line using the [contact form][22] and I will send you it. Be aware that the document is written in [Catalan][23] language.

 [1]: http://msdn2.microsoft.com/en-us/vstudio/products/default.aspx
 [2]: http://msdn2.microsoft.com/en-us/vstudio/Aa718368.aspx
 [3]: http://msdn2.microsoft.com/en-us/netframework/aa904594.aspx
 [4]: http://blogs.msdn.com/stuart_kent/default.aspx
 [5]: http://blogs.msdn.com/stuart_kent/archive/2007/11/22/what-s-new-for-dsl-tools-in-vs2008-vs2008-sdk.aspx
 [6]: http://blogs.msdn.com/stuart_kent/archive/2007/11/22/dsl-tools-beyond-vs2008.aspx
 [7]: http://en.wikipedia.org/wiki/Model-driven_development
 [8]: http://en.wikipedia.org/wiki/Domain-Specific_Modeling
 [9]: http://en.wikipedia.org/wiki/Model-driven_architecture
 [10]: http://www.metacase.com/news/AgileModelingMarch2006.html
 [11]: http://www.metacase.com/
 [12]: http://www.ambysoft.com/
 [13]: http://en.wikipedia.org/wiki/Software_factory
 [14]: http://www.openarchitectureware.org/
 [15]: http://www.eclipse.org/gmt/
 [16]: http://www.eclipse.org/gmt/oaw/diagram.php
 [17]: http://martinfowler.com/bliki/DomainSpecificLanguage.html
 [18]: http://en.wikipedia.org/wiki/Macro_(computer_science)#Procedural_macros
 [19]: http://en.wikipedia.org/wiki/Z/OS
 [20]: http://www.eclipse.org/
 [21]: http://sourceforge.net/projects/jbpm/
 [22]: http://www.rodenas.org/blog/contact/
 [23]: http://en.wikipedia.org/wiki/Catalan_language

## Comments

### Comment by Pascal on 2007-11-29 14:32:34 +0000
Hi Ferdy,

Interesting article. We&#8217;ve been investigating different MDD solutions the last couple of years. I was quite charmed by the what Acceleo accomplishes, but it does not serve us as much as we like, primarily because it integrates into Eclipse and our own software development facility works with .NET (VS2005). With the advent of VS2008 we, like you, were hoping for more extended MDD support, but unfortunately this does not seem to have Microsoft&#8217;s real attention. Do you have particular good experience with MDD in the .NET arena apart from the VS DSL tools?

Pascal.

### Comment by Ferdy on 2007-12-03 00:48:09 +0000
Pascal, we don&#8217;t have any experience in .NET. We are primarily a J2EE installation, that is one of the reason why we didn&#8217;t choose VS DSL Tools. Unlike you, we prefer an Eclipse environment. 😉

### Comment by AlySangadji on 2010-06-11 02:43:40 +0000
Nice, How about mono Framework?