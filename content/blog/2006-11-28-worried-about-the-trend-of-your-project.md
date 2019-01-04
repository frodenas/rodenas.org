---
title: Worried about the trend of your project?
author: ferdy
date: 2006-11-28T00:57:31+00:00
url: /blog/2006/11/28/worried-about-the-trend-of-your-project/
b2006:
  - 11
bcategories:
  - Tools

---
Trying to determinate the best way to implement [Continuous integration][1] at our shop, and specifically, which information we must generate after nightly builds, I’ve discovered [QALab][2], an opensource project that “_collects and consolidates data from several QA tools and keeps track of them overtime, allowing developers, architects and project managers alike to be presented with a trend of the QA statistics of their project_”

It collects data from the following tools:

  * [Checkstyle][3]: code style validation and design checks. QALab keeps track of number of violations per file and overall.
  * [PMD][4]: Code checks (possible bugs, dead code, sub-optimal code, etc). QALab keeps track of number of violations per file and overall.
  * [PMD CPD][5]: Duplicate code (always a bad idea) detection. QALab keeps track of number of the overall number of duplicated lines.
  * [FindBugs][6]: fantastic tool to detect potential bugs (really!). QALab keeps track of number of violations per file and overall.
  * [Cobertura][7]: Coverage tool. QALab keeps track of percentage of branch and line coverage.
  * [Simian][8]: excellent duplicate code detection (non-open source). QALab keeps track of number of the overall number of duplicated lines.

(Via [The Server Side][9])

 [1]: http://en.wikipedia.org/wiki/Continuous_Integration
 [2]: http://qalab.sourceforge.net/
 [3]: http://checkstyle.sourceforge.net/
 [4]: http://pmd.sourceforge.net/
 [5]: http://pmd.sourceforge.net/cpd.html
 [6]: http://findbugs.sourceforge.net/
 [7]: http://cobertura.sourceforge.net/
 [8]: http://www.redhillconsulting.com.au/products/simian/
 [9]: http://www.theserverside.com/news/thread.tss?thread_id=43248