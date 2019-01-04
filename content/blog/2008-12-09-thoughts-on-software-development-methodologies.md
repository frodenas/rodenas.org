---
title: Thoughts on software development methodologies
author: ferdy
date: 2008-12-08T23:35:10+00:00
url: /blog/2008/12/09/thoughts-on-software-development-methodologies/
b2008:
  - 12
bcategories:
  - Agile
  - Methodologies
  - Software Development
btags:
  - Agile
  - Iterative
  - Methodologies
  - Waterfall

---
Recently, I have been involved in a major IT program, framed on a high demanding business strategic plan, which aims to renovate all of our core banking system. One of the program&#8217;s first steps was changing our IT organizational and governance structure, the enterprise architecture, the application development tools and the software development methodology.

Although my responsibility in this program only relies on the application development tools, as one of the <acronym title="Project Management Office">PMO</acronym> leaders, I was able to follow closely the rest of the items. One of the topics that I was specially interested on was the software development methodology, because among other things, before the program, it was one of my responsibilities, and, after the program, it will be, again, my responsibility. The truth is that I had high hopes for change (perhaps influenced by the &#8220;Yes, we can!&#8221; slogan), but the fact that they came to conclusion that we need another waterfall methodology, perhaps a bit stricter than the one we use today, disappointed and frustrated me.

But please, that nobody misunderstood me. I deeply respect the work and decisions of my colleagues. I have had the opportunity to explain my thoughts. I gave them some books on the topic. I tried to influence the people who had the task to define the new methodology in order to introduce more innovative methods/process/practices of software development, but, maybe, being too innovative in a very classic environment doesn&#8217;t helped me. I think that changing the software development process in a big organization requires lots of effort, education, very slow and gradual steps, &#8230;, and I do not want to miss this opportunity, I believe that now is the moment to do that, taking advantage of the whole changing program. Well, at least, now some people knows that there are more life after the waterfall model, there&#8217;s a gray scale between white and black. 🙂

As I&#8217;m a bit nonconformist, I tried to find out which were the reasons behind that decision. So I decided to ask some developers and project managers to get an exact idea of what they think/know about software development methodologies. Although most of the answers were what I expected to find, I also found some <del>interesting</del> frustrating observations. I want to share with you some of them:

  * Most developers and project managers are unaware of the existence of another methodologies, and they do not have any interest in learning them. Methodologies and process are something bored and do not provide any value to what they are doing actually. Although they recognize there are lot of inefficiencies in the way they work, they don&#8217;t want to change it. When I ask some of them if they follow our actual methodology, their answer is NO. &#8220;Well, at least, are you following any predefined process?&#8221; again, the answer is NO.
  * Most project managers feel that a plan-driven methodology provides them more control over the whole project, that their projects are more predictable. But when I ask them if their projects are on time, most of them recognizes that NO. They also doesn&#8217;t have/use information from previous projects in order to estimate or improve the next ones, every project is different.
  * They see iterative / agility methodologies as a chaos, the wild west, where there isn&#8217;t any discipline. W00t? discipline and agile are not conflicting. XP, for example, requires high levels of discipline.
  * Some people told me that waterfall methodologies encourages a comprehensive documentation. &#8220;Well, could you show me your last project&#8217;s documentation? no, we didn&#8217;t have time to write it. OK, doesn&#8217;t mind. Could you show me any documentation of any project you&#8217;re involved? no, we&#8217;re still working on it, you know, we&#8217;ve tigh schedules&#8221;.
  * Some answers reflected the &#8220;[We&#8217;re Special][1]&#8221; syndrome: &#8220;Agile is suitable when you want to develop software for an Iphone, but not for financial applications&#8221; (paraphrased).
  * Some project managers get annoyed when they must talk with their clients or stakeholders, they hate them (I believe this is a mutual feeling). Yeah, those evil people that everyday changes the requirements and doesn&#8217;t have any idea how hard is the software development process.

I also tried to analyze some projects, and, surprisingly, I discovered that most of them are short term projects (2-3 months). I expected longer projects, as corresponds to a waterfall process. So I ask myself if we are really using a waterfall methodology, or we&#8217;re using a masked iterative process?

How about you? Did you find these kind of answers in your company? Any ideas on how to address this situation?

 [1]: http://www.ibm.com/developerworks/blogs/page/ambler?entry=adoption_antipattern_we_re_special

## Comments

### Comment by martin on 2008-12-09 10:18:02 +0000
Very nice summary of your experinece Ferran.

In my opinion a very good selling point of Agile methodologies is accountability. This accountability becomes specially appealing if your development team likes to work and the things they do but they feel frustrated by other departments. Agile methodologies are incredibly transparent and if there is inefficiencies in the processes they will highlight them in few weeks. The problem is that many people see a threat on this transparency as it would be fairly clear that they are not doing their job properly. 

I imagine it must be very difficult to introduce this kind of methodologies in an organization like yours. In my experience, a good way to sneakly introduce Agile into corporations would be trying to convince people of give it a try on prototypes, proof of concepts or non-core projects. Small projects of few months. The probably will be successful and slowly the team member will start to appreciate the advantages of development transparency. At least after several succesful projects you would have a sollid argument inside your own company to try to promote the methodology further up. 

Cheers.

### Comment by xavier on 2008-12-10 23:36:54 +0000
Nice post, sad reading. I think that it is brilliant how you compare all their NOs to their SHOULDs, and how they fail to take the next steps based on the actuals. 

<a href="http://flickr.com/photos/xverges/3099036368/" rel="nofollow">Flick&#8217;ed</a> and blogged a possible way to introduce changes, that may or not may apply to your situation.

Good luck!

### Comment by Ferdy on 2008-12-11 01:01:02 +0000
Martin, Xavier, Thanks for your advice!

### Comment by Thibauld on 2008-12-22 13:23:59 +0000
Interesting little survey&#8230; I&#8217;m not so used to working with big companies but I can assure you that there are problems in SMB too. Actually, the problem is more a lack of methodology. In a previous work experience, I worked for a startup whose CTO has been completely unable to come up with a product! He wanted to use an agile methodology but without exactly knowing what it was.. it ended up being a total mess with the specs constantly evolving and becoming more complex. As he was also a very poor team manager, he totally failed in building the required product and the startup collapsed&#8230; great experience but how frustrating!! This is why I now focus a lot on <a href="http://thibauld.com/2008/12/web-application-implementation-step-3-framework-vs-methodology/" rel="nofollow">development methodology</a>&#8230;
  
Thanks for this post&#8230;

### Comment by Andrés on 2009-01-30 11:24:44 +0000
Hi all,
  
I agree with Ferran (and the reason is not the fact that he is my boss 😀 ). In concrete I found very interesting his last analysis: Short term projects masking iterative processes. My personal experience about that issue is that classical (waterfall) projects are getting smaller and smaller. As a consequence of this,comprehensive documentation, good planing and other supposed features of classic methodologies are disappearing. They act as they have the control but they don&#8217;t. Ok, some feeling of &#8220;chaos&#8221; is arising, but there are lot of things to put the blame on and methodology is not present in their minds.

Regards

Andrés

### Comment by ALM Software on 2009-04-30 20:59:17 +0000
Hey Everyone, 

Excellent post!!! It gives a lot of insight as to needing some form of methodology
  
when it comes to development projects. I agree with Thibauld in that I have worked for
  
a company that crumbled because of the dis-organization of projects.

I appreciate the post.

### Comment by Software Developer on 2010-02-23 21:43:49 +0000
Nice article&#8230;..I really impressed while reading your post&#8230;..Thank you so much , it will useful to every one&#8230;.