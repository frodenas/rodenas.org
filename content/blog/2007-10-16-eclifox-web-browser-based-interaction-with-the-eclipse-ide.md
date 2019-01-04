---
title: Eclifox – Web Browser-Based Interaction with the Eclipse IDE
author: ferdy
date: 2007-10-15T23:05:41+00:00
url: /blog/2007/10/16/eclifox-web-browser-based-interaction-with-the-eclipse-ide/
b2007:
  - 10
bcategories:
  - Eclipse
  - IDE
btags:
  - eclifox
  - Eclipse
  - firefox
  - IDE
  - web

---
[alphaWorks][1], the IBM emerging technologies portal, has released a new [Eclipse][2] plug-in that sounds very interesting: [Web Browser-Based Interaction with the Eclipse IDE][3] (codename Eclifox or Eclipse Web Enabler). It is an Eclipse plug-in that enables [Gecko][4]-based browsers, like [Firefox][5], access to the Eclipse <acronym title="Integrated Development Environment">IDE</acronym>.

> Browser-based access to an Eclipse IDE or an Eclipse-based application allows users to access Eclipse without any installation or configuration. Users can evaluate an application without downloading it. Alternatively, Eclipse can be accessed by multiple browser-based users. This application provides an opportunity for combining Eclipse content in mashups. 

Developed by 6 interims from the [SJCE][6] and guided by [Gautham B Pai][7] from the IBM India Software Lab, this plug-in converts Eclipse User Interface content, except for the ones created with <acronym title="Graphical Editing Framework">GEF</acronym> or visual editors, to <acronym title="XML User interface Language)">XUL</acronym> format, that it is served by a [Jetty web server][8] and then rendered in the Gecko browser.

Here it is an screenshot of the PHP plug-in viewed inside a Firefox browser:

<center>
  <a href='/blog/images/2007/10/eclifox.jpg' title='Eclifox - Web Browser-Based Interaction with the Eclipse IDE'><img src='/blog/images/2007/10/eclifox.jpg' alt='Eclifox - Web Browser-Based Interaction with the Eclipse IDE' width="450" height="349" /></a>
</center>


  


And view this impressive [flash demo][9] that shows the usage of Python and Ruby plug-ins from Eclifox.

This is the second attempt I see to bring us a web browser IDE. The first one, who follows a different programming model based on [Ajax][10] and [REST][11], is the Web UI Foundation Component of the [Jazz Platform][12], which allows users to directly access a Jazz server from a web browser.

We shall be keeping an eye on them.

 [1]: http://www.alphaworks.ibm.com/
 [2]: http://www.eclipse.org/
 [3]: http://www.alphaworks.ibm.com/tech/eclifox?open&S_TACT=105AGX01&S_CMP=LP
 [4]: http://wiki.mozilla.org/Gecko:Home_Page
 [5]: http://www.mozilla.com/en-US/firefox/
 [6]: http://www.sjce.ac.in/
 [7]: http://gauthampai.livejournal.com/
 [8]: http://jetty.mortbay.com/
 [9]: http://www.alphaworks.ibm.com/demo/flash/display/eclifox0
 [10]: http://en.wikipedia.org/wiki/AJAX
 [11]: http://en.wikipedia.org/wiki/REST
 [12]: http://jazz.net/