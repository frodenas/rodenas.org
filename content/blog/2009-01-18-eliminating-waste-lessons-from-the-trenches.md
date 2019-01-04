---
title: 'Eliminating Waste: Lessons From The Trenches'
author: ferdy
date: 2009-01-18T00:12:15+00:00
url: /blog/2009/01/18/eliminating-waste-lessons-from-the-trenches/
b2009:
  - 01
bcategories:
  - Agile
  - Methodologies
  - Software Development
btags:
  - Agile
  - features
  - lean
  - Methodologies
  - process
  - waste

---
As I explained in a [previous post][1], the last year I have been involved in a renewal process of all of our application development tools. One of the first things we did when we started the program was to apply the most fundamental lean principle: **eliminate waste**. To lean thinking, waste is anything that does not create value for a customer. For those of you who are not familiarized with the lean principles, I recommend the &#8220;[Lean Software Development: An Agile Toolkit][2]&#8221; book. In this book, Mary and Tom Poppendieck translated the seven wastes of manufacturing identified in the [Toyota Production System][3] into the [seven wastes of software development][4]: _Partially Done Work_, _Extra Processes_, _Extra Features_, _Task Switching_, _Waiting_, _Motion_ and _Defects_. In this entry I would like to explain some of the problems we have encountered while trying to eliminate waste and some lessons learned.

The first waste we tried to eliminate was the **extra processes**. In other word, we tried to eliminate paperwork that does not means adding value for our users or for our organization. In our case, this task was not related to the development of our tools, it was about eliminating extra processes that were embedded in the tools we developed which forced our users (developers) to execute some unnecessary processes. This action produced some surprises, since near the end of the development, in one of the latest functional demos, there was a crisis moment. Some developers reminded us an essential process they were following in the old tool: they defined the batch programs in a product repository. This process was removed deliberately, because it does not provide any value, so it was a surprise for us that our users asked for this. When we asked them why this process is necessary, they answered that they did not know, but it was something they used to do because someone told them that they must do this task. &#8220;Is this useful?&#8221; we replied. &#8220;No, but we must continue doing that because &#8230; we must do that&#8221;. Wow, it remembers me the [monkey experiment][5]. Obviously, and despite the laments of our users, we did not add again that process. So lesson learned: **in order to eliminate waste you need to break the _status quo_, you need to break the corporate culture**.

The second waste we tried to eliminate was the **extra features**, because this was one of the biggest mistakes we did in the past in other tools. Some years ago we started developing a new tool and, using the usability argument, we added a lot of features that lately nobody used. Some of the hitches you may suffer adding those features are that your code-base grows uselessly, increases maintenance costs and makes future developments more complex. This must not be a big problem if users really need these features, but why must we maintain them if they are not being used? Users, moreover, feel that the tool is more complex, so your usability argument disappears, and they reproached us that we are not focusing on what it is really important for them. Now, I am proud to say that our tools have less features, but, at least, the ones we implemented are really used. So two more lessons learned: 1) **more features does not mean better tools**; 2) **usability does not mean more features**.

I am going to stop here. I am sure most of you who have tried to eliminate waste have found these or similar problems. But I do not want to conclude this entry without explaining one of my latest lessons learned. It is not strictly related to lean thinking, it applies to software development in general, albeit it could only apply to some organizations. Sometimes, I believe it is better not to explain that you are using an &#8220;x&#8221; methodology, or to intensify your position saying that you learned those practices from whatever methodology. Sound strange, isn&#8217;t it? But I have discovered that lots of developers hate the words &#8220;methodology&#8221; and &#8220;process&#8221;, and they have adverse reactions when they hear them. I find easier to explain practices without any reference to the original methodology. Lots of times, using the common sense is better to prove the goodness of a practice. And if it does not sound good, perhaps it does not match your organization. OK, maybe I am generalizing. In every change process you will find resistance, so perhaps if it does not sound good it is because fear. So, my last lesson learned: **use common sense, do not arbitrarily adopt new practices**.

 [1]: http://www.rodenas.org/blog/2008/12/09/thoughts-on-software-development-methodologies/
 [2]: http://www.amazon.com/gp/product/0321150783
 [3]: http://en.wikipedia.org/wiki/Toyota_Production_System
 [4]: http://community.ative.dk/blogs/ative/archive/2007/01/18/Lean-Principle-Number-1-_2D00_-Eliminate-Waste.aspx
 [5]: http://www.stsc.hill.af.mil/crosstalk/2000/02/backtalk.html