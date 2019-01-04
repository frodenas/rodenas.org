---
title: Transparency in Software Development
author: ferdy
date: 2008-05-06T22:25:05+00:00
url: /blog/2008/05/07/transparency-in-software-development/
b2008:
  - 05
bcategories:
  - IBM
  - Methodologies
  - Software Development
btags:
  - Jazz Project
  - open commercial development
  - Rational Team Concert
  - Software Development
  - transparency

---
Some days ago, I [wrote][1] about a QCon 2008 session where [Erich Gamma][2] spoke about transparency and how it is related to the IBM’s Open Commercial Development model (OCD). As I have been involved since last year as a beta customer in one of the projects where OCD is been applied, the [Rational Jazz Project][3], I want to discuss with all of you some thoughts and opinions about this software development style.

First of all, and just to be clear, I&#8217;m not going to talk about which is the license model behind OCD. The words “Open” and “Commercial”, when seen together, produces some unexpected chills and thrills, and they have generated some controversial discussions out there, mainly in the open source community (maybe, as Stephen O&#8217;Grady [points out][4], it will be more accurate to characterize this as transparent development). In the case of the Jazz Platform, there is also some confusion, because we don&#8217;t know if IBM is going to [release it as an open source software][5] and then develop commercial products based on this platform (like Eclipse), or if they, both platform and products, will remain as commercial products. I vote for the first option, but the word “commercial” in OCD suggest me the second one.

Instead, what I&#8217;m going to talk about is how transparency in a great feature in the software development process. So go ahead.

During my career, I have dealt with lots of products, from both open and non-open source software providers. One pattern that I always find in traditional proprietary software is that you never interact with the development team; there is a barrier between you, the customer, and the vendor&#8217;s developers. If you need to report a bug or to ask for an enhancement, you can only interact with a service desk. Usually, they have a support web site, where you can see your own tickets, but you can’t see any other bugs or enhancements reported by others companies. You never know when they are going to deliver a solution for your problem (except if it is a blocker), which will be the way they are going to implement your enhancement, if there are more people interested in some enhancement, … You can only check if the bug is fixed or the enhancement implemented when the vendor delivers a new version of the product, and, sometimes, results are not what you wanted. Furthermore, sometimes, you will have to deal with lots of useless questions, mainly due to misunderstandings between you, the service desk and the development team. This is what Erich Gamma calls “Swiss bank approach to software development”.

This firewall between customers and developers is really very frustrating, not only for the customers, but [also for the developers][6]. Some companies try to supply this lack of communication organizing user’s conferences (where you can meet some developers), meetings with whatever worldwide VPs, or through a customer advocate. In some cases, frustrated users set up unofficial forums to share their problems or to try to join forces so that the vendor accepts an enhancement. They try to establish some kind of user&#8217;s community, but without the vendor involvement. In my experience, and without intention to offend anyone, you will get lots of nice words, but you rarely archive a real solution.

With open-source products, there is a really different way of relationship between customers and providers. There is an open participation and customers can influence easily in the development process in several ways. And I’m not talking about having access to the source code, which is important, but also having access to the bug tracking system, the development mailing-lists, user’s forums, and, in some cases, the development plans, all of them maintained by the development team (fewer misunderstandings). This well-known transparent and collaborative model usually produces enhanced feedback, which leads to deliver better products (in terms of user’s expectations). It’s about archiving customer value, instead of vendor value.

This is the same interaction I have found while working with the Jazz Project. I have had access not only to the source code but also to the latest integration builds (so I can check how my enhancements are implemented), a wiki with technical information about the platform (if you care about the extensibility), a community forum, the development plans and a dashboard to monitor the health of the overall project. I have had also full access to the issue tracking system, where I can submit my own bugs and enhancements, but I can also see which other enhancements are requested by other customers (and to enroll them if I found someone interesting), in which version are they planned … Summarizing, full transparency in the development process. One of the consequences is that I’ve felt, and this is personal and subjective opinion, more involved in the development process, more biased towards submitting enhancements and more confident about future problems that could appear. This feeling is nothing new if you have previously worked with open source projects, but it is something strange coming from an proprietary product.

However, there is a huge difference between open source and OCD models. While in open source software you can contribute to the code base by fixing a bug or improving some features, in OCD it is not clear which will be the contributor’s role. It will depend on the license model selected, which, in turn, it will establish if there will be a vibrant community and ecosystem outside IBM or if there will be a vibrant IBM’s customer community. Anyway, if the final decision is to keep the software as a commercial product, the transparency applied in this model it will represent a great improvement in the proprietary software development process, for both customers and vendors.

But after using this software development style for some time, I believe that this model it is not useful only to software vendors, but it also could be applied to any IT department, especially in big enterprises, in order to improve their software development process. I also believe this is one of the objectives pursued by [Rational Team Concert][7], the first product based on the Jazz Platform (I will talk about this product in future posts). But this is something that I need to try by myself in the company where I work. As most of my readers already knows, I am in charge of the application developments tools in one major Spanish savings bank. Looking through the development process we use, I am sure that if I ask the users of the tools we develop (our internal customers) how much transparent are we, they are going to complain me. Although we meet periodically, it is hard to achieve transparency only with meetings, we need to adopt different and innovative approaches, the ones I have told you in this post.

And finally, although this is what I honestly think about transparency and OCD, I want to hear other opinions. Do you think this is a good software development model for proprietary software? Do you think this model could be applied inside enterprise firewalls?

 [1]: http://www.rodenas.org/blog/2008/04/28/qcon-london-2008-summary/
 [2]: http://en.wikipedia.org/wiki/Erich_Gamma
 [3]: http://jazz.net/
 [4]: http://redmonk.com/sogrady/2007/06/17/rsdc_2007/
 [5]: http://www.infoworld.com/article/07/08/24/IBM-open-source-Jazz-collaboration-software_1.html
 [6]: http://pmuellr.blogspot.com/2007/07/history-of-transparency.html
 [7]: http://www-306.ibm.com/software/rational/jazz/

## Comments

### Comment by xavier on 2008-05-07 02:35:45 +0000
>Do you think this model could be applied inside enterprise firewalls?
  
To be honest, transparency is both The Right Thing To Do and something that will bring you lots of problems.

There are lots and lots of organizations and people that do not share your view of &#8220;internal customers&#8221; (no matter if the have fancy mission statement that state the opposite); they make work days a pain, progress a drag, and change and improvements impossible. They run their businesses as small monopolies, and holding back info is critical to maintain the status quo. It&#8217;s not something driven by power greed or laziness, just by some tribal us-vs-them feeling.

So transparency is about choosing the right side, about making the workplace something more enjoyable, about giving the transparent team the gratifying challenge of having happy customers instead of the boring challenge of keeping alive a power silo. Most people love helping others and being useful, and transparency empowers teams to get that feeling. 

Of course, not everything is nice and comfy. If you open up your development process, you get some of the problems that OSS projects get: you need to deal with a flood of tickets, or occasional rude assholes that previously did not have access to the development team may get annoying or&#8230;

I&#8217;ve always been a big fan of transparency, but having <a href="http://xdexavier.blogspot.com/2008/05/back-in-ussr.html" rel="nofollow">just read Ricardo Semler&#8217;s book</a> I guess I&#8217;m (still) more vocal 🙂

Soooo (apologies for such a long comment!), a transparent developemnt process behind the firewall is possible, is good for the team, is good for the corporation and it is The Right Thing. Go for it! Good luck!

### Comment by Kelly Drahzal on 2008-05-07 20:29:54 +0000
The Rational eSupport and Knowledge Management teams are now engaging in transparent
  
and agile project management using Jazz and RTC &#8230; transparency is the ONLY way
  
to go, IMHO, and our internal stakeholders are appreciating our efforts, I think.

### Comment by Ferdy on 2008-05-08 01:08:25 +0000
Xavier, you&#8217;re right. Workplace politics are always present in every organization, but you must learn to deal with them. One quote that I have always liked is from David G. Jensen, where he says &#8220;<a href="http://sciencecareers.sciencemag.org/career_development/previous_issues/articles/2006_12_15/tooling_up_be_politically_astute_but_don_t_play_politics/(parent)/13199" rel="nofollow">you must be politically astute, but don&#8217;t play politics</a>&#8220;. 

If we get scared of all potential problems that could arise, then we will never do anything. In this case, I see more advantages than hitches. So, let&#8217;s be positive and try it, and if I fail, then just another lesson learned 🙂

### Comment by Ferdy on 2008-05-08 01:14:02 +0000
Kelly, I&#8217;m sure your stakeholders are really appreciating your efforts. So go for it!

### Comment by martin on 2008-05-09 10:13:22 +0000
I reckon that internal transparency is a must for a healthy company. However, I&#8217;m afraid as you guys correctly spotted above this won&#8217;t be possible in every company. You really need very good key people in all terms, technical, business and man-managing to introduce this kind of mentality within the company itself. 

With regard to external facing companies, I believe it certainly depends on many factors like the type of business you are running, the confidence on your team, etc. Not every company will be wishing to show publicly their detailed roadmap for the next two years, as they could quite easily miss the targets with marketing consequences, their competitors could basically grab their roadmap and copy it or improve it or just use it as a weapon for targeting their own customers, &#8230; It is really a complex subject. Companies like IBM can do it as they have market ubiquity and plenty of resources to research, innovate and counteract their competitors, but not all the companies have such resources.

### Comment by Ferdy on 2008-05-11 02:39:27 +0000
Martin, thanks for dropping by. As you stated, external facing is a complex subject and there are lots of factors involving such decision. 

I think that marketing, in particular, is sometimes an inhibitor to some software development best practices and could be dangerous if you don’t manage it correctly. Just an example, the Jazz Project sometimes seemed to me a vaporware project. Two years announcing a project (hey, I want this kind of planning for my projects) and nowadays there is no product available (ok, it will be a product next month). Some days, I felt that they were teasing me.

But I believe long-term roadmaps are not the most important thing in transparency. There are lots of open-source products where you don&#8217;t have visibility on which are the future developments plans, and this does not prevent them from being mass adopted and being a successful model of collaboration between customers and providers. I believe it is more important to feel that your requirements will be taken into account and that you can influence the direction of the project. One book I always recommend about this topic is &#8220;<a href="http://www.amazon.com/Outside-Software-Development-Successful-Stakeholder-based/dp/0131575511/ref=" rel="nofollow">Outside-in Software Development</a>&#8221; (BTW, from IBM).

### Comment by Mike MacDonaggh on 2008-05-14 11:31:53 +0000
Interesting article. 

I think that in many organisations achieving effective development transparency relies on a certain maturity and understanding of software development extending from the development team all the way to executives, which makes achieving transparency complex. On the other hand I can’t think of a better way of achieving that maturity and understanding than adopting a transparent philosophy. It’s just important to understand that it’s not something that can be achieved overnight in many organisations. Especially the big ones!

### Comment by Ferdy on 2008-05-27 00:26:31 +0000
Mike, like Xavi and Martin, you hit the nail on the head. You need to manage the politics associated typically to upper management, and with large groups, you also need a organizational change process. Not every developer will adopt and follow such practices spontaneously, there is always some resistance to change.

### Comment by Surge on 2011-01-25 19:00:25 +0000
“you must be politically astute, but don’t play politics“. 

This is a great quote thanks to Ferdy for posting it. I have found office politics to be difficult to deal with. And it has become more so with the economy going the way it is.
  
I found this in another blog and found it extremely beneficial to me; &#8220;Software transparency is immediate visibility into the quality and security of all code in development, without disrupting the development process&#8221;. I must say that transparency is a great idea but the implementation of it could be rather a kaotic one and dealing with that kaos would make it even more befuddling. How do you not do this though. The client is hard enough to understand and get answers out of, in some cases. Without doing some kind of transparency you might have a useless instance. Creating trancparnecy is a canundrum. Thanks for the post.