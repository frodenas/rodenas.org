---
title: IBM Application Development Cycle (AD/Cycle)
author: ferdy
date: 2006-12-11T23:34:42+00:00
url: /blog/2006/12/12/ibm-application-development-cycle-adcycle/
b2006:
  - 12
bcategories:
  - Case
  - IBM

---
I&#8217;ve found an [IBM Systems Journal][1] article about the [AD/Cycle strategy and architecture][2] that makes me cry. AD/Cycle was one of the first projects that I had been involved as a software engineer (1991).

Years ago, repository technology promised to change the way corporate IT units build mission-critical software. Development teams could store meta data in a single warehouse and access that meta data using a variety of tools from multiple vendors. IBM&#8217;s AD/Cycle <acronym title="Computer Aided Software Engineering">CASE</acronym> initiative, based on [Systems Application Architecture][3], was an attempt to centralize the management of mainframe application development, supporting the integration of tools through a consistent user interface ([CUA][4]), workstation services, an AD information model, tool services, Repository Services, and Library Services that provide control for defining and sharing application development data. The centerpiece was the Repository Manager MVS (RM/MVS) running on a mainframe ([MVS][5]) and [DB2][6], that was built somewhat on the lines of the <acronym title="Information Resource Dictionary System">IRDS</acronym> though not quite compliant with the specifications. In addition, IBM also developed <acronym title="Source Code Library Manager">SCLM</acronym> to manage the various files of application development code. The architectural vision was to provide seamless operation between the IBM Repository and the SCLM.

Unfortunately, repository-based development failed to deliver the goods to IT development shops. Since then, IBM has switched to the client/server model, and its repository technology has evolved through [Configuration Management Version Control][7], from 1991, to newer products in the [Rational product line][8].

In our shop, we finally dropped AD/Cycle and developed an in-house meta data repository that it&#8217;s still running in production, providing a useful integration through our mainframe toolset.

 [1]: http://www.research.ibm.com/journal/sj/
 [2]: http://domino.watson.ibm.com/tchjr/journalindex.nsf/0/d44faeb516f5013985256bfa00685c34?OpenDocument
 [3]: http://en.wikipedia.org/wiki/Systems_Application_Architecture
 [4]: http://en.wikipedia.org/wiki/Common_User_Access
 [5]: http://en.wikipedia.org/wiki/MVS
 [6]: http://en.wikipedia.org/wiki/IBM_DB2
 [7]: http://en.wikipedia.org/wiki/IBM_Configuration_Management_Version_Control_%28CMVC%29
 [8]: http://www-306.ibm.com/software/rational/offerings/scm.html