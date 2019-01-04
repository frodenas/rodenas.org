---
title: Eclipse Ganymede hidden treasures
author: ferdy
date: 2008-07-30T23:52:01+00:00
url: /blog/2008/07/31/eclipse-ganymede-hidden-treasures/
b2008:
  - 07
bcategories:
  - Collaboration
  - Eclipse
  - IDE
btags:
  - Collaboration
  - Eclipse
  - IDE
  - Statistics

---
The last week of June (as usual), the [Eclipse Foundation][1] delivered the new release of Eclipse, called [Ganymede][2]. This year the updated version is a coordinated release of [23 different projects][3] and represents 18 <acronym title="Million Lines Of Code">MLOC</acronym>. There are lots of [articles][4] and [posts][5] out there explaining the new features, so I&#8217;m not going to bore you with the rehashed details. I would just like to mention on two interesting features.

The first one is a really cool feature introduced in the [Eclipse Communication Framework][6] project that enables distributed teams to reap the benefits of pair programming. Based on a [Google Summer of Code][7] proposal, [Mustafa Isik][8] developed [Real-Time Shared Editing][9], dubbed Cola (**col**l**a**borate), a mechanism that allows two developers to work collaboratively in real-time to edit source code and/or documents. He has put together a short [screencast][10] showing the usage of this technology. Check it out! Digging further in this amazing feature, Mustafa [pointed me][11] to a [Google Tech Talk][12] he gave at [EclipseDay at the Googleplex][13] where he explained how this plugin resolves in real time any change conflict. The video is worth a visit. And if you want to add this feature to other editors (by default it has has been added to the JDT Java Source Code editor and Eclipse&#8217;s Default Text Editor), [Scott Lewis][14] has wrote some easy instructions &#8230; simply by adding a little bit of [markup to plugin.xml][15].

The second one is the [Usage Data Collector][16], a piece of technology that will generate statistics on how the various components of the Eclipse workbench (loaded bundles, commands and actions, perspective changes, view usage, &#8230;) are being used by developers. The Eclipse Foundation intent is to use this data to help committers and organizations better understand how developers are using Eclipse, in order to improve the overall user experience. Privacy must not be a problem, as this feature is opt-in (there is an option on the &#8220;Usage Data Collector&#8221; preferences page labeled &#8220;Enable Capture&#8221;) and it is completely anonymous. Although the data collected is not quite representative, you can see right now some [statistics][17] (I see lots of [Cut-and-Paste Programming][18]). I hope that these statistics will be public and the Eclipse Foundation will publish some reports regularly (I have not seen any notice about this). But besides the benefits that these statistics may have for the Eclipse Foundation, I believe they can also be attractive to some organizations which have developed internal plugins. And I say this from my own experience. One of the problems we had in the past was how to measure the use of the different plugins we developed, and also, which was the response time (we had several complains about the client performance). We finally had to create an infrastructure in order to collect and analyze these data. So, I see with interest the possibility of extending the official UDC API (both, listeners and monitors). Let&#8217;s see how it evolves in the future.

 [1]: http://www.eclipse.org/org/
 [2]: http://www.eclipse.org/ganymede/
 [3]: http://www.eclipse.org/ganymede/learn.php
 [4]: http://www.eclipse.org/ganymede/buzzmore.php
 [5]: http://www.technorati.com/search/Eclipse+Ganymede?language=n&authority=n
 [6]: http://www.eclipse.org/ecf/
 [7]: http://code.google.com/soc/
 [8]: http://codesurgeonblog.com/
 [9]: http://wiki.eclipse.org/DocShare_Plugin
 [10]: http://www.vimeo.com/1195398
 [11]: http://twitter.com/codesurgeon/statuses/872309665
 [12]: http://www.youtube.com/watch?v=GfeUCT-tRJQ
 [13]: http://google-opensource.blogspot.com/2008/06/eclipseday-at-googleplex.html
 [14]: http://eclipseecf.blogspot.com/
 [15]: http://wiki.eclipse.org/Extending_Real-Time_Shared_Editing_for_Use_with_Other_Editors
 [16]: http://www.eclipse.org/epp/usagedata/
 [17]: http://www.eclipse.org/org/usagedata/results.php
 [18]: http://c2.com/cgi/wiki?CopyAndPasteProgramming