---
title: WP-chgFontSize WordPress plugin
author: ferdy
date: 2007-03-08T00:28:36+00:00
url: /blog/2007/03/08/wp-chgfontsize/
b2007:
  - 03
bcategories:
  - Wordpress

---
Although users can change the font size of a web page [through standard browser settings][1], few people knows or remembers how to do it.

WP-chgFontSize is a [WordPress][2] plugin that allows users to change dynamically the font size by adding a text or image selection on your blog. It also stores the user selection on their user&#8217;s browser cookies.

It can be used as a widget or directly as a PHP call in the theme.

See an example of how it works at the upper right side (header) of this blog.

### Installation

  1. Download [WP-chgFontSize][3].
  2. Decompress and upload the contents of the archive into /wp-content/plugins/.
  3. Activate the plugin on your WP Admin &raquo; Plugins page by clicking ‘Activate’ at the end of the ‘WP-chgFontSize’ row.
  4. Configure the plugin on your WP Admin &raquo; Options &raquo; Font Size page.

### Usage

To use it, there are two possibilities:

  * If your theme supports widgets, and you have installed the [widget plugin][4] or you are using WordPress 2.2 or higher, add the &#8216;WP-chgFontSize&#8217; widget on your WP Admin > Presentation > Widgets page.
  * Add this code to the theme&#8217;s file where you want the font size selection appear, for example, on the [sidebar.php file][5]:
  
```php
<?php chgfontsize_display_options(); ?>
```

### License

This plugin is released under the [GPL][6].

This plugin is provided with absolutely no support or warranty.

### Version History

  * March 8 2007 &#8211; v1.0 
      * Initial release to the public.
  * August 1 2007 &#8211; v1.1 
      * Bug: use get\_bloginfo(’wpurl’) instead of get\_bloginfo(’url’).
      * New feature: option to restore default font size.
      * New feature: be able to specify min, max and interval values for the font size.
      * New feature: be able to use pixels, ems and percentages units for the font size.
  * September 6 2007 &#8211; v1.2 
      * Bug: first click on + size, it jump to GIANT font size.
  * October 21 2007 &#8211; v1.3 
      * New feature: widgetized version.
  * October 26 2007 &#8211; v1.4 
      * Bug: change js function names to avoid name duplications.
  * February 5 2008 &#8211; v1.5 
      * Bug: allow class type div elements.
  * April 23 2008 &#8211; v1.6 
      * Bug: fix IE issues with class type elements.
  * June 10 2009 &#8211; v1.7 
      * Bug: Determine the correct wp-content directory.
  * May 4 2010 &#8211; v1.8 
      * New feature: add &#8216;Steps&#8217; mode (Thanks to Leo Brown!).

### To Do

**Updated 11 Sep 2008**

  * <del datetime="2007-08-02T22:50:43+00:00">Bug: use get_bloginfo(’wpurl’) instead of get_bloginfo(’url’)</del>
  * <del datetime="2007-08-02T22:50:43+00:00">New feature: option to restore default display</del>
  * <del datetime="2007-08-02T22:50:43+00:00">New feature: be able to use ems or percentages instead of pixels for the font-sizes</del>
  * <del datetime="2007-10-21T22:50:43+00:00">New feature: widgetized version</del>
  * <del datetime="2008-04-23T00:50:43+00:00">Bug: fix IE issues with class type elements</del>
  * New feature: add non-constant intervals
  * New feature: add a `<noscript>` section for non-ActionScript-enabled browsers

 [1]: http://www.w3.org/WAI/changedesign
 [2]: http://wordpress.org/
 [3]: http://wordpress.org/extend/plugins/plugin/wp-chgfontsize/ "WP-chgFontSize"
 [4]: http://wordpress.org/extend/plugins/widgets
 [5]: http://codex.wordpress.org/Customizing_Your_Sidebar
 [6]: http://www.gnu.org/licenses/gpl.html

## Comments

### Comment by macewan on 2007-03-20 19:26:26 +0000
Thank you.

### Comment by Kristin on 2007-03-22 11:39:38 +0000
I tested this plugin on one of my sites which has wp installed in a subdirectory, and it didn&#8217;t work at first. But then I changed line 142 ( function add\_chgfontsize\_js() ) to be get\_bloginfo(&#8216;wpurl&#8217;) instead of get\_bloginfo(&#8216;url&#8217;) and then it worked like it should.
  
&#8211; so you might consider changing that to add support for people who has their wp blog/ site set up just like me.

And thank you for making this plugin, it was just what I needed.

### Comment by Eddie on 2007-04-02 02:45:06 +0000
Good plugin, except that it only works with my posts, it does not work with my pages. Any ideas on how to fix that?

The theme I am using, should it matter, is &#8211; Andreas01-12.

Thanks in advance, hope you can shed some light on yhis problem

### Comment by Dave on 2007-04-03 00:57:06 +0000
I have my WP blog set up in a subdirectory like Kristin, and tried installing the plugin both before I saw her tip, and after making her suggested adjustment, and neither time it has worked. 

This is a plugin I \*really\* want for my readers. Any help would be appreciated!

### Comment by Ferdy on 2007-04-04 00:28:49 +0000
Eddie (19), the problem is within Andreas theme, it uses different DIV containers. Try using &#8220;post&#8221; DIV instead of &#8220;content&#8221;, although it will only change post&#8217;s font size.

### Comment by Ferdy on 2007-04-04 00:32:11 +0000
Dave (20), check the contents of the /wp-content/plugins/wp-chgfontsize/ directory. You must see 6 files. And remember that the subdirectory name (/plugins/wp-chgfontsize) is case sensitive.

### Comment by Ralev on 2007-04-07 18:27:17 +0000
I&#8217;ve just installed the plugin and it works fine, thank you Rodenas 🙂
  
have a nice Easter!

### Comment by Able-Mart.com on 2007-04-22 10:00:26 +0000
Unlike your blog, it only changes the size of the posts on mine. The sidebar remains the same size?

### Comment by Ferdy on 2007-04-22 12:18:58 +0000
Able-Mart, try using &#8220;wrap&#8221; instead of &#8220;content&#8221; as the DIV Base element.

### Comment by UrbanMonk on 2007-05-29 12:07:44 +0000
Hi, for some reason its not showing up on my list of plugins, even though I&#8217;m pretty sure I uploaded it correctly. Any ideas? Thanks!

### Comment by UrbanMonk on 2007-05-29 12:09:39 +0000
Oops! Sorry I&#8217;m a retard! It works now!

### Comment by Mosey on 2007-06-13 14:50:00 +0000
I love the idea of this plugin! 😀 I&#8217;ve been using another javascript to achieve the same effect but a plugin is of course a much better option! Is there any potential release date for the widgetised version of the plugin please? Thanks!

### Comment by Ferdy on 2007-06-14 00:52:21 +0000
Mosey, my hope is to start working on the widgetised version in July.

### Comment by Dave on 2007-07-11 01:17:38 +0000
This is an update to comment #20 which I left in early April. After upgrading to WP versions 2.2.1, I tried this plugin again, and it installed perfectly.

### Comment by Daniel (Aypeus) on 2007-07-20 21:05:54 +0000
Hi. A question and a sugestion. Making this a widget would make this plug-in one of the best ones. I wonder can the &#8220;code&#8221; be pasted in a text widegt and still function?

If anyone knows anything feel free to contact me, msn or email; <aypeus@aypeus.org>

Thx for creating this, your time reading this 🙂

Regards, Aypeus (Daniel)

### Comment by Ferdy on 2007-07-22 22:52:17 +0000
Daniel, I don&#8217;t know if pasting the code in a text widget will work. I suggest you to wait 2-3 weeks more, as actually I&#8217;m working in the widgetized version.

### Comment by bev on 2007-08-19 04:05:57 +0000
It seems to be with just my installation, but I keep getting unsightly link borders around the images when I put it on my blog. Other blogs I&#8217;ve looked at who have this plugin installed DON&#8217;T have this problem, so I am not sure why this is happening. Does anyone by any chance has any suggestions? (I have removed the code from my sidebar in the meantime due to this issue. Not really sure if I can add a border=0 anywhere to fix it&#8230;

### Comment by Ferdy on 2007-08-21 23:41:02 +0000
bev, just modify your css file and add something like this:

#chgfontsizeoptions a, #chgfontsizeoptions a:visited, #chgfontsizeoptions img {
  
border: none;
  
}

### Comment by bev on 2007-08-22 03:40:35 +0000
Thank you, Ferdy! I&#8217;ll go and add that to my CSS stylesheet now. Thanks for helping out 🙂

### Comment by Steve on 2007-08-27 21:46:24 +0000
Hi Ferdy- Terrific plugin&#8230; installed fine and works effectively, but one question: The first time someone clicks the + size to enlarge, the font jumps to GIANT size, 24 point or something. Works normally after the first time. I&#8217;ve limited it to 14 pixels, but it still does the same. Any ideas? Thank you for your time, and a great plugin.

### Comment by Ferdy on 2007-08-28 01:25:36 +0000
Steve, I&#8217;m not able to reproduce the problem. Which OS + browser + version are you using?

In the meantime, I&#8217;ll do some tests with several configurations trying to reproduce it.

### Comment by Steve on 2007-08-28 02:52:09 +0000
Hi Ferdy- It happens with both IE6 and Firefox for me, which is strange. I&#8217;ll try it on some other computers and browsers. If you haven&#8217;t reproduced it, that&#8217;s good news. I&#8217;m using the Cutline theme and WP 2.1. Thanks for the reply and great plugin!

### Comment by ppip on 2007-09-04 06:22:42 +0000
Hi, I came with the same problem: with first click on A+ image, it jump to GIANT font size. but after the first click, it works fine. (I test it on FF2 and IE7，IE6 on Windows XP)

MY SITE: <a href="http://www.happysky.org" rel="nofollow">http://www.happysky.org</a>
  
(It&#8217;s in Chinese but you can see the plugin on the top)

### Comment by ppip on 2007-09-04 07:21:09 +0000
OK, this is the solution:

Change the line 256 in wp-chgfontsize.php form

`echo "   chgfontsize_font_size = getCookie('wp-chgfontsize');\n";`

into

`echo "   chgfontsize_font_size = Number(getCookie('wp-chgfontsize'));\n";`

### Comment by Ferdy on 2007-09-06 02:52:44 +0000
Steve, the new version 1.2 solves your problem.

ppip, thanks for the solution. I just updated the pluggin to version 1.2 with the corrected code.

### Comment by bluedogranch on 2007-09-21 18:36:50 +0000
I&#8217;d like to get to be able to use the font size changer at the end of each wordpress post, (in addition to in my sidebar), and while I have php code execution enabled and working for each post, the images for the font size don&#8217;t display. Would this seem to be an issue with images inside posts rather than an issue with the font size php code? Thanks for any ideas?

### Comment by canarkadaş on 2007-09-23 19:06:08 +0000
Thanks..
  
[…]  <a href="http://worldarchivetr.com/wp/100-wordpress-eklentisi/" rel="nofollow">Açıklamalı 232 WordPress eklentisi (Agu. 15, 2007 !!) (WordPress plugin list),</a>[…]

### Comment by koz on 2007-10-02 11:52:05 +0000
Hi !

I&#8217;d love to use your plugin, as some people complain aout the font size of my blog but I don&#8217;t even manage to have the function appear&#8230;

I tried to put it in a text thing in a widget and it did not work. I later saw you mention that you are working on a widgetized version.

I tried to put it directly in posts but, again, it does not show up.

Where do I screw up ? Do I mention a wrong &#8220;div&#8221; ?

### Comment by koz on 2007-10-02 11:56:34 +0000
Seems I did not filled in all information (intervall, in particular). Now, it&#8217;s not showing in the sidebar, ok in the post, but not working yet. Probably my fault. I&#8217;ll work on it.

### Comment by Erin on 2007-10-23 07:34:04 +0000
Whenever I click the image to change the font size, nothing happens.

### Comment by Ferdy on 2007-10-23 18:41:04 +0000
Erin, which is the URL of your site? Have you configured the plug-in at the Admin -> Options page? Be sure to specify the DIV container.

### Comment by Erin on 2007-10-25 22:42:29 +0000
Yes I&#8217;ve done all that. It&#8217;s still not working. I included my url, just click my name.

### Comment by Ferdy on 2007-10-26 00:27:09 +0000
Erin, there was a conflict between two javascript function names. I&#8217;ve modified the chgfontsize plugin to avoid name duplications with other plugins. Download the new <a href="http://wordpress.org/extend/plugins/wp-chgfontsize/" rel="nofollow">version 1.4</a> and don&#8217;t hesitate to contact me if you still have problems.

### Comment by Erin on 2007-10-26 06:48:57 +0000
It still isn&#8217;t working for me. I don&#8217;t know if it&#8217;s something I&#8217;m doing or what.

### Comment by June on 2007-10-27 11:14:50 +0000
I installed the plugin but obviously am missing font size background. My style sheet has  **defined as 62.5% so I put that as the default size &#8211; then picked 40 as min and 150 as max with 6 intervals. The pages showed up in tiny type and clicking on the display showing in the sidebar did nothing. I had to disable the plugin so the pages would be readable again. Please point me somewhere so I can learn how to set this up. Thanks.**

### Comment by Ferdy on 2007-10-28 23:36:01 +0000
Erin, sorry to say this, but I believe the plugin is not compatible with the theme you&#8217;re using. I have found lots of &#8220;content&#8221; DIVs on your main page, so the javascript function doesn&#8217;t know which one must change.

### Comment by Ferdy on 2007-10-28 23:41:39 +0000
June, I have tested on my local machine the same configuration you pointed on your comment and it has worked for me. So I don&#8217;t know where is the problem. If you try it again, just drop me a line via the comment page and I&#8217;ll watch your site to figure out what is happening.

### Comment by Jérôme on 2007-11-02 13:38:22 +0000
hi, good plugin for the accessibility.

but the plugin doesn&#8217;t work in my website. how to configure it?

I have wordpress 2.3 and many themes widget ready

thanks for your help. i need your plugin for my readers

### Comment by Ferdy on 2007-11-02 14:04:13 +0000
Jéròme, at the wp-chgfontsize options page, change the DIV element value to &#8220;wrapper&#8221; or &#8220;content&#8221;. Hope this helps.

### Comment by Jérôme on 2007-11-02 14:36:02 +0000
Very thanks for you help. The problem is resolved.

Thanks for your speed answer. My frend who write with me on the blog have a low vision. your plugin give the blog easy readable for him.

thanks again.

### Comment by Jérôme on 2007-11-06 01:18:39 +0000
Hi Ferdy,

i have a new problem on my new blog: your plugin doesn&#8217;t appear, i have tried to slide the wpchgtfontsize widget in my widget leftbar but your widget is invisible! i have tried to delete and reinstall him but the problem is the same.

### Comment by Ferdy on 2007-11-07 00:49:42 +0000
Jérôme, 

Check the contents of the /wp-content/plugins/wp-chgfontsize/ directory. You must see 6 files. And remember that the subdirectory name (/plugins/wp-chgfontsize) is case sensitive.

### Comment by Dario on 2007-12-09 20:24:54 +0000
I keep getting the following error:

chgFontSize_getCookie is not defined

I&#8217;ve changed a couple of thing but I haven&#8217;t been able to fix it.

### Comment by Dario on 2007-12-09 20:25:12 +0000
Oh.. I&#8217;m using the latest version. 1.4

### Comment by Ferdy on 2007-12-09 22:36:46 +0000
Dario, which is the url for your site? I&#8217;ll check what&#8217;s happening.

### Comment by Dario on 2007-12-10 14:25:46 +0000
<a href="http://www.natoura.com" rel="nofollow">http://www.natoura.com</a>

### Comment by Ferdy on 2007-12-10 22:41:05 +0000
Dario, 

The problem resides in your wordpress header file, because the main javascript file is not loaded.

Check you header.php file to see if there is an statement that contains <?php wp_head(); ?>. If you don&#8217;t find this statement, add it at the end of the file. 

Another option could be adding manually the next statement:
  
<http://www.natoura.com/natouraW/wp-content/plugins/wp-chgfontsize/wp-chgfontsize.js>

Hope this helps!

### Comment by Dario on 2007-12-11 01:33:27 +0000
Thanks a lot, I was able to figure it out, thanks to your help.

### Comment by http-jkwasn01.myid.net- on 2007-12-17 19:41:50 +0000
Hi Ferdy,

When you increase or decrease the text size it only seems to affect the &#8216;Posted in&#8217; and not the actual post. 

<a href="http://blog.yantotc.com/" rel="nofollow">http://blog.yantotc.com/</a>

Any ideas? 

Thanks
  
Josh

### Comment by Ferdy on 2007-12-17 20:07:22 +0000
Josh, at the Font size options page, change the DIV Base Element from &#8220;content&#8221; to &#8220;container&#8221; or &#8220;wrapper&#8221;.

### Comment by http-jkwasn01.myid.net- on 2007-12-17 20:59:43 +0000
Both container and wrapper still work like content (just resizes the &#8216;Posted in&#8217;&#8230; I viewed the source, and the text is within the wrapper, container and content tags&#8230;

Anymore ideas? 

Thanks

Josh

### Comment by Ferdy on 2007-12-18 02:15:46 +0000
Josh, the problem is that the .entry and .post h2 classes, among others, specifies the font size in pixels, so they override the font size of the content, container and wrapper classes.

The only solution I see is not specifying the font size in pixels in these &#8220;low level&#8221; CSS classes. I suggest you to use percentages instead. If not, I&#8217;m sorry, but this pluggin will not work for you.

### Comment by http-jkwasn01.myid.net- on 2007-12-20 16:32:29 +0000
I removed the font size tags from those classes and it works!

Thanks for your help Ferdy!

### Comment by Caroline on 2007-12-22 00:23:22 +0000
Hi, I hate to be a bother&#8230;I seem to have the same question as a lot of others, but I&#8217;ve not been able to make their solutions work. Clicking on the icons (I&#8217;m not using the text) just doesn&#8217;t do anything. I&#8217;ve tested with Firefox and IE7. I believe &#8220;content&#8221; is the correct DIV tag to use, and it doesn&#8217;t appear multiple times on the site. I&#8217;ve removed any references in my CSS to font sizes according to pixels or em. In the config panel, I&#8217;ve tested it in ems, pixels, and percentage with no effect, small intervals, huge intervals, etc. I know that the plugin, consisting of 4 gif files, 1 javascript, and 1 php file, are in the right directory (all lowercase: &#8230;/wp-content/plugins/wp-chgfontize). I&#8217;m really at a loss, and hope that it&#8217;s something small I&#8217;m missing, as opposed to something wrong with my theme.

### Comment by Eme Navarro on 2008-01-06 20:01:01 +0000
Hello: great pugin and very thanks for do it. I tried to install on a wordpress theme in a Intranet. This plugin it&#8217;s very important for my readers. I have been many troubles trying the installation
  
(only works on the side bar), but finally I find the DIV tag : &#8220;main&#8221; in more themes works very well

Very thanks Ferdy

(I beg your pardon for my english)

### Comment by Katie Cummings on 2008-01-10 20:29:03 +0000
Where in my single post php file do I add the code for this plugin if I want it to appear in the upper right hand corner of each post? I&#8217;ve tried it in several places, but it ends up right next to the author name&#8230; I wouldn&#8217;t mind if it was on the same line, just aligned right. Please help.
  
Katie

### Comment by Ferdy on 2008-01-12 23:43:48 +0000
Caroline, at the wp-chgfontsize options page, change the DIV element value to “center”, the min font size to 80, the max font size to 120, and the default font size to 100. Hope this helps.

### Comment by Ferdy on 2008-01-12 23:44:40 +0000
Katie, I need to check the single php file. Please, send me this file.

### Comment by Morgan on 2008-01-31 21:36:00 +0000
I&#8217;m using the same theme as used on this weblog, or so it appears. Latest version of WP running, but however I do have some other plugins up. I deactivated them all, but still wp-chgfontsize is not working. I&#8217;m using the widgetized version. Subfolder has correct name, 6 files. What is the div you are using because I cannot seem to figure out which one i need (currently I have entered page, but I already tried sidebar and content). The plugin just does not show up (the widget). What am I doing wrong? Thx!

### Comment by Ferdy on 2008-02-01 00:43:15 +0000
Morgan, your div is correct, but seems that you didn&#8217;t specify the min, max, interval and the default font size at the pluggin options panels. Check the values and try again.

### Comment by Sally on 2008-02-02 01:06:26 +0000
All I see in my widget box is &#8220;?a-??A+?

### Comment by Ferdy on 2008-02-02 11:20:16 +0000
Sally, change the DIV element from &#8220;left&#8221; to &#8220;page&#8221; or &#8220;center-widget&#8221;.
  
Also, there is a bug in this version of the plugin and it only works with DIVs that are ID elements. So, in order to work properly with your theme, change your DIV element (instead of using div class=&#8221;page&#8221;, you must use div **id**=&#8221;page&#8221;). Or wait until I release a new version of the plugin (hope it will be next week).

### Comment by Promecius on 2008-02-13 05:29:54 +0000
This doesn&#8217;t work on my IE7, but it does work in Firefox and Opera. Have you any idea what can cause this and if there is a solution?

### Comment by cartmanxxl on 2008-02-17 10:19:38 +0000
first I&#8217;m impressed with the effort you put in this awesome plugin&#8230; thanks
  
I hope you can help me sort out my problem; the plugin used to work like a charm on many themes which I used but on this one <a href="http://www.fulham.pl" rel="nofollow">http://www.fulham.pl</a> it distorts the layout (sidebar); I wonder why is this happening and how can I correct this; div is content (tried wrap, wrapper and nothing happens); ty in advance

### Comment by Jonathon on 2008-02-20 21:49:39 +0000
Non-Constant Intervals:
  
Instead of setting min, max and interval, can I list my desired font sizes: 11, 12, 13, 15, 19, 23?

### Comment by kimsch on 2008-03-14 17:23:24 +0000
I can&#8217;t seem to get this to work in ie7 either, it works fine in Firefox 2. The drop down box works, the default button works, but no changes to the font size in the posts work in IE.

### Comment by songdogtech on 2008-04-01 21:14:52 +0000
Hello, This plugin works great for WordPress 2.5. I&#8217;m wondering if you want to release the the bare bones code (with comments to be able to select the default font size and other options) for use on a site that is not based on WordPress? I&#8217;d like to use it on other sites, and have found that other font resizers just don&#8217;t work that well )and don&#8217;t have a default size control, either.) &#8211; Thanks, Mark

### Comment by Rajesh on 2008-04-16 06:52:59 +0000
Thanks a ton. I was looking for this for quite sometime!

### Comment by PNOOZ on 2008-04-16 23:44:12 +0000
I too am experiencing functionality issues with IE.
  
Tested with (Windows XP OS):
  
Opera 8.5x and 9.2x &#8211; both work great.
  
Firefox 1.5 and 2.x &#8211; both work great.
  
Safari 3.x &#8211; works great.
  
IE 5.5, 6.x and 7.x &#8211; none work at all.
  
I&#8217;ve tried all variations of available options (div element, units, display, etc.) with no success.

I love the idea behind this plugin and appreciate the efforts of the author and would love to be able to offer to my visitors, but am afraid that it will cause too much confusion amongst the users of the most popular browsers (IE).

Thanks, I would greatly appreciate any feedback as to a workaround or fix.

### Comment by Ferdy on 2008-04-17 00:25:40 +0000
PNOOZ, I&#8217;ve tested the plugin with IE (all versions) and works well in some sites (for example, in this blog) and doesn&#8217;t do anything in others. Actually, I don&#8217;t have a fix for this issue, I need to investigate what&#8217;s wrong.

### Comment by Ferdy on 2008-04-17 00:40:29 +0000
songdogtech, the code is released under the <a href="http://www.gnu.org/licenses/gpl.html" rel="nofollow">GPL</a>. So you can modify it if you want. But if you just need to use it without any modification, you can <a href="http://wordpress.org/extend/plugins/wp-chgfontsize/" rel="nofollow">download</a> the code, and upload the wp-chgfontsize directory to your site. Then add the following code to your pages:

`<br />
<script type="text/javascript" src="http://<i>your site URL</i>/wp-chgfontsize/wp-chgfontsize.js"><br />
<!--<br />
chgfontsize_element = 'page';<br />
chgfontsize_min_font_size = 80;<br />
chgfontsize_max_font_size = 120;<br />
chgfontsize_interval_font_size = 5;<br />
chgfontsize_units_font_size = '%';<br />
chgfontsize_default_font_size = 100;<br />
chgfontsize_units = chgFontSize_getCookie('wp-chgfontsize-units');<br />
if (chgfontsize_units != chgfontsize_units_font_size) {<br />
 chgfontsize_font_size = chgfontsize_default_font_size;<br />
} else {<br />
 chgfontsize_font_size = Number(chgFontSize_getCookie('wp-chgfontsize'));<br />
 if (chgfontsize_font_size == null) { chgfontsize_font_size = chgfontsize_default_font_size; }<br />
}<br />
chgfontsize_imgdecact = new Image();<br />
chgfontsize_imgdecact.src = 'http://<i>your site URL</i>/wp-chgfontsize/decrease_activated.gif';<br />
chgfontsize_imgdecdea = new Image();<br />
chgfontsize_imgdecdea.src = 'http://<i>your site URL</i>/wp-chgfontsize/decrease_deactivated.gif';<br />
chgfontsize_imgincact = new Image();<br />
chgfontsize_imgincact.src = 'http://<i>your site URL</i>/wp-chgfontsize/increase_activated.gif';<br />
chgfontsize_imgincdea = new Image();<br />
chgfontsize_imgincdea.src = 'http://<i>your site URL</i>/wp-chgfontsize/increase_deactivated.gif';<br />
chgFontSize_display(<i>display_text (on / off)</i>, <i>display_image (on / off)</i>, <i>display_restore on / off)</i>);<br />
chgFontSize();<br />
//--><br />
`

### Comment by Ferdy on 2008-04-17 00:47:48 +0000
Jonathon, added Non-Constant Intervals as a to-do feature.

### Comment by PNOOZ on 2008-04-17 14:08:32 +0000
Sorry, I meant to add that I have discovered that if I leave the &#8220;DIV Base Element&#8221; field empty or blank that is has the opposite effect that I described in my previous post &#8211; the plugin will work with IE but not the others. Just thought that I would pass along in hopes that it will help someone figure out what&#8217;s going on.

Thanks again, Ferdy.

### Comment by PNOOZ on 2008-04-17 14:46:07 +0000
Sorry again, but I just made another discovery. I viewed your source and then mine and tried the following which worked:

I added the &#8220;id&#8221; element to my div tage and it now works in all browsers. Have successfully tested in IE 7, FF 2, Opera 9 and Safari 3.

I did have to tweak a few style sheet elements due to alignment issues, but I&#8217;m sure that this will vary by theme.

Hope this helps.

### Comment by PNOOZ on 2008-04-17 14:53:26 +0000
The tag was stripped from my last post it was:
  
`</p>
<p>`

If it gets stripped again, it&#8217;s the following less the angle brackets:
  
div class=&#8221;entry&#8221; id=&#8221;content&#8221;

### Comment by PNOOZ on 2008-04-17 19:05:09 +0000
Have now had more time to evaluate in all of the browsers available to me and found that my last post was a little premature. After testing in IE 5.5 and 6 I found major alignment problems. I edited once again to the following:
  
div class=&#8221;entry&#8221; id=&#8221;entry&#8221; and set the matching &#8220;Font Size&#8221; plugin &#8220;DIV Base Element&#8221; option to &#8220;entry&#8221;. I have since successfully tested in all browsers.

The &#8220;entry&#8221; class element in my stylesheet is the one that governs just the post and only the post. I only wanted to give the option to my visitors to resize the text of those posts. So, setup as I have, all functions well as desired.

The &#8216;div class=&#8221;entry&#8221; id=&#8221;entry&#8221;&#8216; tag referenced is found on my &#8220;main index template&#8221; under &#8220;presentation > theme editor&#8221; in my WP admin panel.

Apologies again for so many posts, just trying to be helpful. If it were possible to edit posts, I would have done so.

Thanks again for your excellent work!

### Comment by Ferdy on 2008-04-23 01:04:31 +0000
PNOOZ, I&#8217;ve discovered what causes the bad behaviour in IE. Upgrade to version 1.6 and it&#8217;ll work well (I hope!).

### Comment by Prasannah on 2008-04-23 06:48:37 +0000
How do I specify multiple DIV classes?

### Comment by Ferdy on 2008-04-23 22:51:47 +0000
Prasannah, you can&#8217;t specify multiple DIV classes.

### Comment by songdogtech on 2008-04-24 05:33:45 +0000
Re: comment 5306

Thanks for the bare font size changer code &#8211; I will use it on a static non-WP site where I don&#8217;t need all the extra functions of jquery or prototype. &#8211; Mark

### Comment by Prasannah on 2008-04-24 16:08:03 +0000
> Prasannah, you can’t specify multiple DIV classes.

:-(. I would really like to have this feature (maybe in your next version) as it makes sense to also change the font-size of the sidebar content and comments!

### Comment by BabyGotMac.com on 2008-04-26 05:41:19 +0000
Thank you for this great plugin. It&#8217;s tough to make a site everyone can enjoy, and this helps tremendously.

### Comment by PNOOZ on 2008-05-07 02:37:59 +0000
Is there a simple way to have the font size automatically reset to default on page refresh or click through to a new page? I find that with all of my various browsers when I set the font size larger or smaller, it doesn&#8217;t &#8220;stick&#8221; and the plugin will reflect one value when it is actually default. I hope that this makes sense, if not please click over to my site and give it a try and I believe that (hopefully) you&#8217;ll see what I mean.

Thanks

### Comment by Matt on 2008-05-08 16:25:10 +0000
I&#8217;m having trouble getting the plugin to work properly. I&#8217;ve set all the settings, but it only changes the size of the titles, byline, and links, not the main text of the posts. There is only one main\_content\_shortened div (which is the div base element). 

Thanks,
  
Matt

### Comment by Ferdy on 2008-05-09 00:24:12 +0000
Matt,

Add these lines to your CSS files and it&#8217;ll work:

.MsoNormal {
      
font-size: 1em;
  
}

### Comment by Matt on 2008-05-09 17:41:10 +0000
Excellent. It works now.

### Comment by jn on 2008-05-23 16:43:10 +0000
Hi. I can&#8217;t get this to work on WPMU 1.5.1 &#8211; Any suggestions? Also any plans for multiple divs in the near future? Thanks!

### Comment by Ferdy on 2008-05-27 00:07:28 +0000
jn, 

&#8211; Which error are you seeing in your WPMU installation?
  
&#8211; There aren&#8217;t any short-term plans to support multiple divs

### Comment by Scott on 2008-05-29 18:33:55 +0000
This is just the plugin I&#8217;ve been looking for. I assume I have done something wrong and that is why the widget plugin is not working on my site. I could use advice about how to get it to work. Thanks for your help and for not assuming I&#8217;ll know where to place the correct code if that&#8217;s what&#8217;s needed &#8212; I am new to using css.

### Comment by Scott on 2008-05-29 22:44:27 +0000
It works now. I just needed to set it to posts instead of content, and it works for posts and pages. Sorry to bother you. Thanks for the plugin.

### Comment by Lawrence on 2008-06-11 09:30:08 +0000
Hi, thanks for sharing this plugin. I have decompressed and uploaded it into /wp-content/plugins/ but I can&#8217;t see the plugin in the WP-Admin > Plugins page. Any idea what is the cause of this problem or anywhere that I need to check on?

### Comment by Darryl on 2008-06-11 10:59:36 +0000
I have a strange problem&#8230; I&#8217;ve been looking at the code for ages and can&#8217;t seem to see where it&#8217;s coming from. underneath where I have implemented the plugin, there are 3 extra links: A, A, and A&#8230; each with the titles decrease font size, default font size, and increase font size, respectively. They each appear on a new line directly below the images. Any ideas? thanks.

### Comment by Ferdy on 2008-06-13 00:12:04 +0000
Lawrence, check the contents of the /wp-content/plugins/wp-chgfontsize/ directory. There must be 6 files. And remember that the subdirectory name (/plugins/wp-chgfontsize) is case sensitive.

### Comment by Ferdy on 2008-06-13 00:13:09 +0000
Darryl, after checking your site, seems to me that the plugin is working as expected now. Let me know if the problem persists.

### Comment by Vic on 2008-06-24 20:39:03 +0000
Hi there,
  
Know anyone which plugin to use if I want only the first part (first paragraph) of the article to be displayed? If someone want to read more there will be a &#8220;read more&#8221; link&#8230;
  
On my blog right now is displayed all of article content and I don&#8217;t want this&#8230;
  
I&#8217;m talking about the latest 10 articles displayed on the first page of my blog.
  
I&#8217;m using WordPress.
  
Can anyone help?

### Comment by Caspar Hübinger on 2008-07-06 23:15:10 +0000
Thank you for this handy plugin!

I&#8217;ve spent some time today customizing the output a little bit. Not that the plugin would need any improvement, but a certain project I&#8217;m working on does require some visual changes here and there. So I added an image for the &#8220;default font-size&#8221; option and coded its usage into the files. I also customized the link title-attributes, planning localization for the whole plugin in the near future.

If you&#8217;re interested in taking a look at the code now, please send me an email and I&#8217;ll be happy to email a ZIP back.

There&#8217;s no way to see the customization in action, unfortunately, for the project site is under construction pw-protected.

Keep it on!
  
Caspar

### Comment by Caspar Hübinger on 2008-07-07 10:34:07 +0000
Update:
  
Issue in IE 6 on Win XP SP2

Plugin settings:
  
Restored to the original, non-customized 1.6. version
  
Images = activated, Restore to default = activated, DIV Base element = page 

Description:
  
After one click on the &#8220;A+&#8221;-image both of the images (&#8220;A+&#8221; and &#8220;a-&#8220;) disappear.
  
The wrapping links stay functional, though, will say: I can click on the empty links and the script itself keeps working fine. I can also see the &#8220;Default&#8221; text-link. Just the images are gone and won&#8217;t re-appear unless the whole page is refreshed.

Attempts:
  
None so far. I have no idea what&#8217;s happening except it might have to do with the image paths being corrupted in IE?

Thank you for ANY ideas!

### Comment by Ferdy on 2008-07-08 01:10:55 +0000
Caspar, it&#8217;s very difficult to analyze what&#8217;s happening without being able to see the plugin in action. 

Have you tried other browsers, like FF, Safari or even IE 7? Did you see the same strange behavior using those browsers?

One suggestion, check the html code generated, and look for the chgfontsizeimginc or chgfontsizeimgdec id&#8217;s. These are the vars where the images are stored. If you can save the html page, send it to me and I&#8217;ll try to analyze what&#8217;s happening.

### Comment by Caspar Hübinger on 2008-07-08 18:31:04 +0000
Ferdy, thanks for your reply. I&#8217;ve switched to the drop-down option meanwhile and will keep working with it until this project is done.
  
Nevertheless, I&#8217;ll keep your hint in mind and will look at the image option again afterwards. Whatever I&#8217;ll find, I&#8217;ll let you know.

Thanks again!

### Comment by songdogtech on 2008-07-23 02:17:15 +0000
Ferdy,

Thanks for the code listing way back in April; I&#8217;m trying to get the font size changer to work in a non-Wordpress site. I have the js link data you posted in my pages and wp-chgfontsize directory in place. Now I get this error in my test index page

Call to undefined function: get\_option() in wp-chgfontsize.php on the line that begins $chgfontsize\_div\_element = get\_option(&#8216;chgfontsize\_div\_element&#8217;);

Seems like wp-chgfontsize.php isn&#8217;t able to read the options that used to be in the database and now are in the page header?

Thanks for any help, Mark

### Comment by Adam on 2008-07-23 23:29:28 +0000
Hi,

I install WP-chgFontSize 1.6 in plugins.
  
I filled some Font Size options
  
DIV Base Element, as entry, since other words doesn&#8217;t regognize.
  
But the changes in my site just only in paragraphs&#8217; lines intervals.
  
I have no changes in font size.
  
What can I do?

### Comment by Ferdy on 2008-07-24 00:53:16 +0000
songdogtech, it seems that you&#8217;re invoking the wp-chgfontsize.php file. You can&#8217;t do that, because it only runs under a wordpress installation (unless you&#8217;ve modified it). In order to use the font size functions, you don&#8217;t need the php file. Just link the js file on your pages and use the javascript code I wrote in my earlier comment.

### Comment by Ferdy on 2008-07-24 00:56:13 +0000
Adam, it could be that the DIV element specified is incorrect or the CSS file overrides some font size options. If you provide me your blog URL (as a comment on this post or using the contact form), I could check your site and tell you what&#8217;s wrong.

### Comment by songdogtech on 2008-07-24 06:05:24 +0000
Ferdy, Hmmm&#8230;.. Reason I tried linking the php file is that I thought I needed to call in the body of the page in order to display the increase/decrease images.

I&#8217;ve tried the js in the head and the body of the page but no luck. My links to the js file and images are correct.

I don&#8217;t know much javascript 🙂 !!

&#8211; any ideas? Thanks, Mark

### Comment by Adam on 2008-07-24 08:58:59 +0000
Mr Ferdy
  
I use as DIV element entry word, since other words can&#8217;t recognize.
  
Thanks

### Comment by Philix on 2008-07-24 12:03:34 +0000
This is a great plug in 🙂

### Comment by Adam on 2008-07-25 08:55:49 +0000
I install WP-chgFontSize 1.6 in plugins.
  
I filled some Font Size options
  
DIV Base Element, as entry, since other words doesn’t regognize.
  
But the changes in my site just only in paragraphs’ lines intervals.
  
I have no changes in font size.
  
What can I do?

Sorry, the problem is on

### Comment by Adam on 2008-07-29 08:44:40 +0000
Anybody, can answer my question?

### Comment by Ferdy on 2008-07-29 23:57:26 +0000
Adam, you&#8217;ve a before each paragraph. This sentence overrides the wp-chgfontsize style.

### Comment by Adam on 2008-07-30 10:14:40 +0000
Hi Ferdy,
  
Thank you for the reply.

In my “style.css” file there is neither “span style” nor “span style=”font-size: small”

These are “font-size” in my style.css

```
h1 {font-size: 1.5em;}

h2, h3, h4 {font-size: 1.2em;}

.date1 {font-size: 3em; display: block; color: #fb3;}

.date2 {font-size: 2em; display: block;}

.date3 {font-size: 2em; display: block; font-weight: bold; color: #fb3;}

.rockit {text-align: right; border-top: 1px dashed #b80; font-size: 0.8em; clear: both; padding: 5px 10px 0 10px;}

.pageInfo {font-size: 0.8em; color: #aaa; text-align: right; border-top: 1px dashed #ccc; border-bottom: 1px dashed #ec5; padding: 1em; clear: both;}

.boxedin {padding: 0 0.5em; margin: 0 120px 20px 0.5em; font-size: 0.9em;}
  
#newheader h1 a {font-size: 2em; color: #f90;}

#newheader h2 {color: #f90; padding-right: 20px; margin-top: 10px; font-size: 0.9em; font-weight: normal;}

#column1 h2 {font-size: 1.5em;}

#column2 {float: left; position: relative; width: 185px; margin-left: -185px; font-size: 0.8em;}
  
#column3 {float: right; position: relative; width: 178px; margin-right: -178px; font-size: 0.8em;}
  
#footer {background: url(&#8216;images/shadow_footer.png&#8217;) top left repeat-x; font-size: 0.8em; clear: both; padding: 20px 10px; margin: 0 210px 0 230px;}

#back {clear: both; font-size: 0.8em; text-align: right; padding: 0 10px; clear: both; margin-top: 20px;}

#nav, #nav ul {text-align: left; font-size: 1.1em; list-style: none; font-weight: normal; z-index: 8;}

#nav li ul {margin: 0; padding: 0; font-size: 1em; border: 1px solid #ddd; background: url(&#8216;images/page_nav.png&#8217;) repeat #eb5; position: absolute; left: -999em; height: auto; width: 14em;}

#breadcrumbs {position: absolute; font-size: 0.8em; top: 6px; left: 5px; text-align: left; text-transform: lowercase;}
  
#searchCSS {font-size: 0.9em; position: absolute; top: 6px; right: 5px;}

#searchsubmit {font-size: 10px; background: #fff url(&#8216;icons/icon_search.gif&#8217;) 1px 1px no-repeat; cursor: pointer; padding: 0 0 0 15px; border: 1px solid #ca3;}

.comment_no {padding: 10px 0; float: right; font-size: 3em; color: #ec5;}

.commentmetadata {border-top: 1px dashed #ec5; clear: both; text-align: right; font-size: 0.8em; font-weight: normal; color: #ca5; margin-top: 20px !important;}

.icons dt {margin: 0; padding: 0.5em; font-size: 1.1em; font-weight: bold; color: #fff; background: url(&#8216;images/portlet_header.png&#8217;) !important;}

.newfont { font-family: Arial, sans-serif; font-size: 1.1em; color: #000000; }
```

### Comment by songdogtech on 2008-07-30 19:35:17 +0000
Ferdy, Hah! &#8211; I finally figured how to get the font sizer to work in a non-Wordpress page. Between the js code you listed and looking at the source for a WordPress page where it does work, I figured out the settings. Thanks &#8211; Mark

### Comment by Ferdy on 2008-07-31 02:05:15 +0000
songdogtech, nice to hear that.

### Comment by Ferdy on 2008-07-31 02:10:24 +0000
Adam, the span style is located in your index.php and single.php files, not in your style.css file.

### Comment by damian on 2008-08-15 17:38:48 +0000
Does anyone else have the issue where wp-chgfontsize is not reading the stored cookie?

Everything works fine, however when I go to another page/post the font size always resets (even though the correct value is in the cookie).

Any thoughts?

Thanks! Great plugin.

### Comment by crystallinity on 2008-08-17 15:15:55 +0000
i have a couple questions regarding the output of the plugin:

1) i plan to use the &#8220;image&#8221; format of the plugin (Display Font Size Values as: Image) in the sidebar, but the problem is, i also want to place text next to the images as a label. for example, the format i desire would be:

\[a-\] \[A+\] Resize Text

for the plugin, i just have this in my sidebar: &#8221; Resize Text &#8221;

the problem is that the plugin seems to automatically create a new line after the images, so in my sidebar, i get:

\[a-\] \[A+\]
  
Resize Text

is there a way to place text on the same line, but after the images the plugin generates?

2) the plugin also puts two spaces between the [a-] and [A+] images when it outputs them into the sidebar (it also puts one space before and one after).

is there a way to remove the two spaces (or reduce to just one) so that the images are directly side by side?

thanks for any help you can offer, and great work on the plugin 🙂

### Comment by crystallinity on 2008-08-17 15:18:56 +0000
whoops, the code part didn&#8217;t display&#8230; basically i just have the piece of code you suggest above for placing the plugin in the sidebar, with &#8220;Resize Text&#8221; next to it, which produces the &#8220;Resize Text&#8221; on the line below.

### Comment by Loona on 2008-09-02 19:40:15 +0000
Hello Ferdy!

Thanks for your work on the plugin!
  
One improvement suggestion, though: Can you add a -Section to the output of the plugin so that it doesn&#8217;t display anything on a non-ActionScript-enabled browser?

Kind regards,

Loona.

### Comment by Loona on 2008-09-02 19:43:34 +0000
D&#8217;oh! &#8211; WordPress swallowed part of my posting&#8230; I wrote:

Can you add a <noscript>-Section&#8230;

### Comment by Kugelblitz on 2008-09-05 11:14:03 +0000
does the plugin work with WordPress 2.6 ?

### Comment by Ferdy on 2008-09-11 00:46:23 +0000
Loona, added as a new feature.

### Comment by Ferdy on 2008-09-11 00:47:43 +0000
Kugelblitz, yes, it works with WP 2.6. I&#8217;ll update the plugin description soon.

### Comment by Rob on 2008-09-14 02:45:23 +0000
Excellent plugin Ferdy, my site is running on the latest version (2.6.2), the code shows (view source) but the function seemed invisible on the page. I tried the widget variant and the same thing happen except for the description I keyed in. Your assistance is much appreciated.

### Comment by Ferdy on 2008-09-14 23:57:52 +0000
Rob, there must be a javascript error. If you provide me your blog URL (as a comment on this post or using the contact form), I could check your site and tell you what’s wrong.

### Comment by Fabricio Vasselai on 2008-09-16 07:33:48 +0000
This plugin is a great piece of job!

I would just ask if:

1) is it possible to make the plugin resize not just the font, but also the size between lines so we do not get things messed up with bigger fonts? Maybe it is possiblem with some CSS options, and in that case, let me know how to do that!

2) choosing the proper DIV to be resized is great, and I was here wondering if would it be possible, in the future, to have differents plugin calls in each post, so readers could only resize the specific post they choose.

Well, anyway, I thank you a lot for that plugin!!

### Comment by Fabricio Vasselai on 2008-09-16 07:44:19 +0000
Oooops, I forgot to ask:

3) choosing &#8220;post&#8221; as my DIV, I can have the plugin resizing just posts, but it excludes the title and the biggest problem, includes the bottom div I have to links like Comments, Print, etc.

4) is it possible, in the form where we choose the DIV, to exclude some besides including?

### Comment by cyanobacteria on 2008-09-24 02:58:23 +0000
Great plugin, but also having problems with WordPress 2.6.2 the same as Rob described &#8211; any suggestions?

### Comment by Ferdy on 2008-09-24 12:36:22 +0000
Cyanobacteria, did you add the code manually or you installed it as a widget?

### Comment by cyanobacteria on 2008-09-25 14:52:42 +0000
Hey Ferdy &#8211; tried both methods. It works fine if you hack the javascript and embed that directly, just not as a php script. Is this my stupidity or a 2.6.2 conflict?

### Comment by Ben Seven on 2008-10-07 02:07:23 +0000
Hi there Ferdy,
  
Great job on this plugin &#8211; however I can&#8217;t seem to track down why the paragraph text on this site won&#8217;t resize using the plugin?
  
If you could take a look, it&#8217;s <a href="http://www.7folio.com/redwoods" rel="nofollow">http://www.7folio.com/redwoods</a> &#8211; would be most grateful.

Thanks!

### Comment by Ferdy on 2008-10-08 01:14:45 +0000
Ben, because you’ve a <span style=&#8221;font-size: 12pt;&#8221;> before each paragraph. This sentence overrides the wp-chgfontsize style.

### Comment by Ben Seven on 2008-10-08 19:13:03 +0000
Thanks for the reply &#8211; but which file is causing this? it&#8217;s not in the CSS!

### Comment by Prinz on 2008-10-12 23:21:23 +0000
Hi,

First of all, thank you for this great plugin!

I have the same problem as damian.

Everything works fine, however when I go to another page/post the font size always resets (even though the correct value is in the cookie).

Any ideas?

### Comment by Scott Bernadot on 2008-11-07 00:32:24 +0000
Line Height resolved:

To change the line height, add this code to your targeted Div ID or class:

line-height: 150%;

You can tweak the percentage of course, but this works well for me.

### Comment by Time Synchronisation on 2008-12-10 11:57:31 +0000
This is a great plugin.

### Comment by Sharon on 2008-12-12 19:56:26 +0000
I&#8217;m having trouble getting it to show on my wordpress site. It shows in my settings and widgets when I&#8217;m logged into my dashboard, but on the actual site, there are no buttons for resizing the text. I&#8217;m using wordpress 2.7. Could that be part of the problem?

### Comment by Trace on 2008-12-13 20:08:33 +0000
I cannot seem to get it to work wtih WP 2.7. I installed it as a widget. I have checked for the overwrites but don&#8217;t think that is the problem. Any idea?

### Comment by Dennis on 2008-12-14 20:40:34 +0000
Many thanks for this plug in! I like it. The installation was very easy. Good work!

### Comment by George on 2009-01-05 09:31:56 +0000
Support fo this plugin has stopped? It is not working in WP2.7
  
Too bad&#8230; Will there be any updates?

### Comment by Ferdy on 2009-01-10 02:25:40 +0000
George, it works in WP 2.7. I’ve updated the plugin description.

### Comment by San Diego Tim on 2009-01-13 00:43:22 +0000
I had no problems with version 1.5 of this plugin when I upgraded to WP 2.7. I did upgrade the plugin to 1.6 and had no problems with it in Firefox or Safari. However, it did not show up in IE7. So, I returned to version 1.5 and am very happy with this great plugin. Thank you Ferdy.

### Comment by Espen on 2009-01-21 13:37:31 +0000
Thanks for great work!

I am having problems showing the plugin in my sidebar?

Please help.

Espen

### Comment by Steven on 2009-01-27 11:49:53 +0000
This plugin does NOT work in WP 2.7. The widget is empty and putting the code in the theme also does NOT display anything&#8230; 🙁

### Comment by WebWizz on 2009-01-31 19:30:51 +0000
I´m also having a problem getting this to show up in WP 2.7. I installed it in the plugins directory but it doesn´t show up in the plugins list. I do have the settings option in the WP Dashboard but the widget just displays the heading and nothing else.

Any help?

WebWizz

### Comment by Jeff R. on 2009-02-06 22:29:18 +0000
I am also having this issue. I install the plugin, I have a msg saying it&#8217;s installed, but it does not show up in my list of installed plugins, and it will not display on the public website. I am able to access the menu options.

### Comment by Jeff R. on 2009-02-06 22:34:21 +0000
Ok&#8230;I got mine to show up in my list. I was using the automatic install option in WordPress 2.7&#8230;and noticed that the actual files were nested. 

If you upload the folder to where the two php files are in the root, the plugin displays in the list.

### Comment by Jeff R. on 2009-02-06 22:58:55 +0000
I&#8217;m still having issues is getting it to show up on the public side&#8230;and wondering if it is something I might be doing / not be doing in the settings&#8230;

### Comment by Heather on 2009-02-07 15:47:28 +0000
Hi, thanks for the great plugin. Just wondering if there is a way to add ALT tags to the text icons (say, &#8220;Make Text Larger&#8221; and Make Text Smaller.&#8221; I know it sounds picky, but the four text graphics are failing my project site in the FAE Accessibility Evaluator because they don&#8217;t have ALT tags.

### Comment by .wired on 2009-02-10 14:46:43 +0000
Hey! It&#8217;s a great plugin, but there are still some bugs. The following is what I would love to be cheanged:
  
1. The plugin doesn&#8217;t work if you chose in the options page to show the default font size button, too!
  
2. It would be great if the added styles on the divs could have a &#8220;!important&#8221;, because I often use the -tag to define the font size!

greatings
  
.wired

### Comment by krabbe on 2009-02-17 14:36:39 +0000
thank you very much for this great plugin. I use it on a band-site which has three different languages and I wonder if it&#8217;s possible to get your plugin gettexted. Than it would be easy to create different .mo-files.
  
This is the only thing I miss and unfortunately I&#8217;m not this good in javascript&#8230;

### Comment by BigWing on 2009-02-23 23:09:38 +0000
Like many other people above, I installed this plugin in my WP2.7 site but it dgign&#8217;t show up on the page. A quick look at the code being generated and the files installed showed that the auto-installation is faulty. It creates an extra, unrequired directory layer under &#8220;plugins&#8221;. Fix that by moving files to where the code on the page wants them to be and the plugin then works.

### Comment by Robert Felty on 2009-03-15 18:44:27 +0000
Great plugin, except that the chgFontSize() function is called before the page is finished loading. At a minimum, it has to be called in the footer of the page. The other option is to do it after page load. Here is a patch to do it after page load:
  
`<br />
*** wp-chgfontsize/wp-chgfontsize.js    2009-03-01 21:52:16.000000000 -0500<br />
--- wp-chgfontsize2/wp-chgfontsize.js   2009-03-15 13:23:06.000000000 -0400<br />
***************<br />
*** 160,165 ****<br />
--- 160,179 ----<br />
        }<br />
  }</p>
<p>+ function chgFontSizeAddLoadEvent(func) {<br />
+   var oldonload = window.onload;<br />
+   if (typeof window.onload != 'function') {<br />
+     window.onload = func;<br />
+   } else {<br />
+     window.onload = function() {<br />
+       if (oldonload) {<br />
+         oldonload();<br />
+       }<br />
+       func();<br />
+     }<br />
+   }<br />
+ }<br />
+<br />
  var chgfontsize_element = null;<br />
  var chgfontsize_min_font_size = null;<br />
  var chgfontsize_max_font_size = null;<br />
***************<br />
*** 167,169 ****<br />
--- 181,186 ----<br />
  var chgfontsize_units_font_size = null;<br />
  var chgfontsize_default_font_size = null;<br />
  var chgfontsize_font_size = null;<br />
+ chgFontSizeAddLoadEvent(function() {<br />
+   chgFontSize();<br />
+ });<br />
diff -crB wp-chgfontsize/wp-chgfontsize.php wp-chgfontsize2/wp-chgfontsize.php<br />
*** wp-chgfontsize/wp-chgfontsize.php   2009-03-01 21:52:16.000000000 -0500<br />
--- wp-chgfontsize2/wp-chgfontsize.php  2009-03-15 13:25:23.000000000 -0400<br />
***************<br />
*** 87,93 ****<br />
                echo "chgfontsize_imgincdea.src = '" . get_bloginfo('wpurl') . "/wp-content/plugins/wp-chgfontsize/increase_deactivated.gif';\n";<br />
        }<br />
        echo "chgFontSize_display('" . $chgfontsize_display_text . "', '" . $chgfontsize_display_image . "', '" . $chgfontsize_display_restore . "');\n";<br />
-       echo "chgFontSize();\n";<br />
        echo "//-->\n";<br />
        echo "\n";<br />
  }<br />
--- 87,92 ----<br />
***************<br />
*** 334,337 ****</p>
<p>  add_action('plugins_loaded', 'widget_wpchgfontsize_init');</p>
<p>! ?><br />
\ No newline at end of file<br />
--- 333,336 ----</p>
<p>  add_action('plugins_loaded', 'widget_wpchgfontsize_init');</p>
<p>! ?><br />
`

### Comment by LeeTramp on 2009-04-14 05:28:58 +0000
Thanks. I love the support here. I was having problems with the line height issue, and found the fix mentioned above. Yeah!

### Comment by Mystic Madness on 2009-04-16 08:58:50 +0000
this is working great. thansk a ton

### Comment by lavner on 2009-05-27 22:32:16 +0000
thanks&#8230;

### Comment by Carlos on 2009-06-01 06:19:53 +0000
I am interested in using your plugin. How can we change the &#8220;default text&#8221; so it adds a gif rather than the word default.

THanks,

cr

### Comment by John on 2009-06-12 20:48:55 +0000
Not sure if you know this but your Font Size controls do not show up in your black header navigation. Both in IE7+ and FF.

### Comment by Ferdy on 2009-06-12 22:58:43 +0000
John, Thanks. Fixed.

### Comment by Drew on 2009-06-14 13:47:37 +0000
Ferdy,
  
I am trying to get your plugin to work (hear good things). I uploaded to plugins folder, activated it but don&#8217;t seem to be able to find &#8216;options&#8217; to set it up. I am using WordPress 2.7.

Any help would be appreciated.

### Comment by Crystal on 2009-06-17 22:35:26 +0000
I installed and activated the plugin, updated the font settings, and added the widget. It appears on my blog but when I click on the increase or decrease images nothing happens. Any ideas? I am using WP v2.7 and IE7 browser. I also noticed that when I hover over the images the code in the lower left corner of my browser says &#8216;javascript:void(0);&#8217;. That doesn&#8217;t seem right.

Thanks for the help.

### Comment by ElderGuru.com on 2009-06-18 04:26:02 +0000
Hi, thanks for putting this together, but it doesn&#8217;t seem to be working on my site: <a href="http://www.elderguru.com" rel="nofollow">http://www.elderguru.com</a>. I have WP 2.7.1 and the widget in the top right sidebar. It&#8217;s visible, but the text won&#8217;t change. Any ideas?

My site is geared toward older people, so this would be really helpful. Thanks again.

### Comment by Ferdy on 2009-06-19 01:06:50 +0000
Elderguru, change the DIV element from “15” to “page” or “content-box” at the Font Size options page.

### Comment by Ferdy on 2009-06-19 01:08:25 +0000
Crystal, this behavior is usually related to the DIV element configuration. I need to see you site in order to check what&#8217;s wrong.

### Comment by Ferdy on 2009-06-19 01:09:34 +0000
Drew, you can find the options page at the administration page -> Options -> Font Size.

### Comment by Max on 2009-06-19 07:43:12 +0000
Hello, thank you for this great plugin. It started to work after I changed DIV Base Element to appropriate one. I have a question. I want to change the words &#8220;Text Size&#8221; to different language(Text Size: a- A+ Default). Where can I edit? I tried to change some part of wp-chgfontsize/wp-chgfontsize.php however I could not find it.
  
Thank you for your help.

### Comment by Crystal on 2009-06-23 15:31:08 +0000
Ferdy, thanks for responding. The site I reference is <a href="http://toolsforshuls.com/" rel="nofollow">http://toolsforshuls.com/</a>. I added the widget to the top of the left column, which I recently removed because of it not working.

### Comment by Crystal on 2009-06-23 20:25:44 +0000
After changing the DIV Base Element, it worked! Woohoo!

### Comment by Tal Galili on 2009-06-25 12:02:01 +0000
This doesn&#8217;t seem to work in WP 2.8, any solution ?

<a href="http://wordpress.org/support/topic/283797?replies=1#post-1115960" rel="nofollow">http://wordpress.org/support/topic/283797?replies=1#post-1115960</a>

Thanks,
  
Tal

### Comment by Avil Beckford on 2009-06-26 21:17:54 +0000
I recently changed my wordpress theme and my blog now loows more beautiful except that the fonts on the widgets are messed up. I uploaded the plugin and it says it uploaded okay but it doesn&#8217;t work. I am using wordpress 2.8, any help would be appreciated. Thanks and have a great day!

### Comment by Dario on 2009-07-11 22:10:40 +0000
I installed this plugin, but it doesn&#8217;t seem to be working &#8212; the buttons don&#8217;t show up. Am I doing something wrong? I filled in the three parameters and used post-wrapper as the DIV. Thanks!

### Comment by modo on 2009-08-04 01:24:24 +0000
The font size does not show on my site. why is this so?

### Comment by Ferdy on 2009-08-04 02:04:22 +0000
modo, did you added the widget? or did you added the php code to your theme? I&#8217;m unable to see the call to the font size function at your blog.

### Comment by modo on 2009-08-04 08:47:20 +0000
Hi,
  
I added it to the widget. You can check it again.

### Comment by Ferdy on 2009-08-04 12:56:51 +0000
modo, you must specify the Font Size Interval at the options page.

### Comment by modo on 2009-08-04 22:33:44 +0000
Thanks. I fixed it.

### Comment by modo on 2009-08-04 22:56:52 +0000
One more thing, when i select the kind of font size i want, the page font size does not change. It just remains static.

### Comment by Ferdy on 2009-08-04 23:19:20 +0000
modo, the problem is that the theme you&#8217;re using at your blog specifies the font size in some &#8220;low level&#8221; CSS classes. For example. the .entry ID specifies &#8220;font-size:12px;&#8221;, and this class is below content, so it overrides the font size used by the plugin. So, I&#8217;m sorry, but this plugin is not compatible with that theme.

### Comment by Fabricio Vasselai on 2009-08-18 12:30:15 +0000
Dears,

I am still having a problem: with bigger sized fonts, each tet line starts to over-pass the other. But I see that it does not happen here in this site, for instance.

How could I avoid such a problem??

### Comment by morteza on 2009-08-20 10:57:15 +0000
hi,
  
I can&#8217;t use plugin.it don&#8217;t change anything!
  
i tested:
  
body;
  
content;
  
wrap;
  
post;
  
and etc.
  
but nothing happened!
  
please help me!
  
regards,
  
Persian Palas

### Comment by peter on 2009-08-25 17:31:04 +0000
Thanks for this plugin. It works fine except for lists as the font size remains unchanged. How can I correct this problem?

### Comment by Arjan on 2009-08-25 20:56:43 +0000
Doesn&#8217;t seem to work on 2.8.4, at least, not on my clients blog&#8230;
  
Tried changing DIV based element to page, content, content_box to no avail.
  
Theme is Athualpa, could that the problem?

### Comment by Heather on 2009-09-05 23:12:27 +0000
I&#8217;ve upgraded a client install to 2.8.4 and the plugin is no longer working. All I see is the text that says &#8220;Change Font Size&#8221;, but it&#8217;s not linked. Should I just deactivate it?

### Comment by Ferdy on 2009-09-14 01:12:54 +0000
Arjan, Heather, this site is running WP 2.8.4 and the plugin works well. I need to see the site in order to check what’s wrong.

### Comment by Heather on 2009-09-14 12:22:22 +0000
Hi Ferdy &#8211; it&#8217;s the upper right hand corner of <a href="http://www.bipolarscotland.org.uk" rel="nofollow">http://www.bipolarscotland.org.uk</a>

### Comment by Ferdy on 2009-09-14 22:57:19 +0000
Heather, delete and reinstall the plugin again. It seems there&#8217;s something wrong with the subdirectory that contains the plugin files (I got a 403 error each time I tried to access them).

### Comment by Heather on 2009-09-16 18:12:12 +0000
That did the trick! Many thanks.

### Comment by Ronny on 2009-12-10 14:44:46 +0000
Hi, great plugin, thanks a lot. I&#8217;m using it on a site, and was wondering if its possible to display it not in a separate div, but along side other icons (without a )?

thanks

### Comment by Sebastian on 2009-12-21 12:59:23 +0000
Hi and thank&#8217;s for a great plugin.

I needed to apply Robert Felty&#8217;s (thank&#8217;s a lot for that, Robert) patch however to gain all functionality (especially for keeping the font size after adjusting), since executing the javascripts before the content containers are laoded obviously will not work.

### Comment by Mustafa on 2010-02-10 12:53:15 +0000
I can&#8217;t seem to get this plugin working. I am using the latest version of wordpress (2.9) and it just does not seem to work. I have no idea what to do.

### Comment by Tony Dunsworth on 2010-02-17 00:35:17 +0000
We&#8217;re using this plug in on a site which is running 2.7 and 2.9.2 &#8211; We had an issue this morning where after a pdf file was uploaded, we had a database collapse. We took the database out and created a new one, importing a clean back up (after we had discovered tampering on the old db&#8230;) now when we run this plug-in, we get the following error. (The error has been isolated to this plug-in)

WordPress database error You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near &#8216;order ASC&#8217; at line 1 for query SELECT t.\*, tt.\* FROM wp\_terms AS t INNER JOIN wp\_term\_taxonomy AS tt ON t.term\_id = tt.term\_id WHERE tt.taxonomy IN (&#8216;category&#8217;) AND ( t.term\_id 1 AND t.term\_id 7 AND t.term\_id 10 AND t.term\_id 13 AND t.term\_id 4 AND t.term\_id 3 AND t.term\_id 12 AND t.term\_id 8 AND t.term\_id 9 AND t.term\_id 11 AND t.term\_id 13 ) ORDER BY order ASC made by require, require\_once, include, get\_sidebar, locate\_template, load\_template, require\_once, wp\_list\_categories, get\_categories, get_terms

Any thoughts of suggestions you have as to why the plug in is causing db issues would be appreciated.

Thank you,

### Comment by Ferdy on 2010-02-17 02:28:37 +0000
Tony, 

It&#8217;s really strange, as this plugin doesn&#8217;t access to the wp tables. It only stores some options vars, using the standard wp functions.

Try this one: explore the wp_options table (using phpMyAdmin or something similar) and delete any row that contains the words &#8220;chgfontsize&#8221; or &#8220;wpchgfontsize&#8221;. Let me knows if this helps.

### Comment by Tony Dunsworth on 2010-02-17 16:19:37 +0000
Ferdy, 

Thanks for getting back to me on this. I scoured the wp_options table two ways and didn&#8217;t find any entries. I don&#8217;t get it. We&#8217;ve disabled the plug-in for now and are looking at the server to see what&#8217;s going on in there as well. 

If I can find anything more helpful, I will be glad to let you know what I find. 

Thanks again for the assistance,

Tony

### Comment by free plugins on 2010-02-23 00:06:23 +0000
Can you provide more information on other wordpress plugins, or do you have some resources you can share with us where we can find such useful stuff? Thanks.

### Comment by Mark on 2010-03-06 23:05:13 +0000
I can&#8217;t get this to work on WP 2.9.2.

### Comment by Some Guy on 2010-04-01 12:43:04 +0000
Hello Ferdy,

I am very impressed with your plug-in and wanted to have it available for the site I am helping with for a local dance club. As some of our members are old, we would love to utilize this plugin, however we cannot seem to get it to work? Any pointers?

Thank you for your time, plugin, and quick response.

Some Guy

### Comment by Adnan Sabah on 2010-05-02 03:20:25 +0000
Hello,

I can&#8217;t get this plugin to work with my WP2.9.2 php5.
  
Can you help me &#8230; please?

### Comment by Alex on 2010-06-28 14:43:59 +0000
Hello!

At the bottom of your post there is a widget that allows to share the post using twitter, facebook, and other. Don\`t you know where can I find this plugin for wordpress?

### Comment by Ferdy on 2010-06-28 22:18:25 +0000
Alex, the widget is <a href="http://wordpress.org/extend/plugins/sexybookmarks/" rel="nofollow">SexyBookmarks</a>.

### Comment by Carol on 2010-07-03 15:03:44 +0000
Thanks a lot for yet another super article. I am always trying to find good WordPress tricks to suggest to my clients. Thanks for creating this article. It&#8217;s just what I was trying to find. Truly wonderful post.

### Comment by Cristian O. Balan on 2010-07-19 18:33:27 +0000
Hi man, great plugin! Thanks to keep it update.

One note (ah no, two notes :D):
  
Function: register\_sidebar\_widget()
  
Used in wp-content/plugins/wp-chgfontsize/wp-chgfontsize.php on line 356.
  
&#8211;
  
Use wp\_register\_sidebar_widget() instead.
  
Deprecated in version 2.8.

Function: register\_widget\_control()
  
Used in wp-content/plugins/wp-chgfontsize/wp-chgfontsize.php on line 357.
  
&#8211;
  
Use wp\_register\_widget_control() instead.
  
Deprecated in version 2.8.

I hope you&#8217;re able to adjust these things for the next (soon :P) update.
  
Thanks again.

### Comment by Michael Pissas on 2010-07-20 06:31:28 +0000
hi, very nice plugin you made 🙂

i get this error on mozilla , although the plugin seems to work:

Error: jQuery(&#8220;.fontResizer&#8221;).fontresizermanager is not a function
  
Source File: <a href="http://www.goldenmag.gr/wp-content/plugins/font-resizer/js/main.js?ver=3.0" rel="nofollow">http://www.goldenmag.gr/wp-content/plugins/font-resizer/js/main.js?ver=3.0</a>
  
Line: 2

and this error on IE:

Webpage error details

User Agent: Mozilla/4.0 (compatible; MSIE 8.0; Windows NT 6.1; WOW64; Trident/4.0; SLCC2; .NET CLR 2.0.50727; .NET CLR 3.5.30729; .NET CLR 3.0.30729; Media Center PC 6.0; InfoPath.2; OfficeLiveConnector.1.4; OfficeLivePatch.1.3; .NET4.0C)
  
Timestamp: Tue, 20 Jul 2010 04:29:16 UTC

Message: Object doesn&#8217;t support this property or method
  
Line: 2
  
Char: 2
  
Code: 0
  
URI: <a href="http://www.goldenmag.gr/wp-content/plugins/font-resizer/js/main.js?ver=3.0" rel="nofollow">http://www.goldenmag.gr/wp-content/plugins/font-resizer/js/main.js?ver=3.0</a>

Any ideas?

thanks in advance!

### Comment by Ferdy on 2010-07-21 00:57:54 +0000
Cristian, thanks for your notes. I&#8217;ll update the plugin soon.

### Comment by Ferdy on 2010-07-21 01:00:24 +0000
Michael, the error is not located in wp-chgfontsize, the problem is in the font-resizer plugin.

### Comment by steve lusby on 2010-07-26 09:33:09 +0000
Have there been any peer reviewed studies on the optimal fonts, sizes or colors for displaying web pages?

### Comment by Rache McCollin on 2010-08-10 16:09:07 +0000
I tried a load of other plugins claiming they did this job and kept deactivating them as they were clunky or just didn&#8217;t have the right information included to help you run them. Yours does the job, is really simple to use and is great &#8211; thank you!

The only problem is that when you search the WP plugins page for &#8216;text resize&#8217; or &#8216;font resize&#8217;, yours doesn&#8217;t appear. I only found it through google. It may be because the name of the plug-in is all one word and the WP search engine isn&#8217;t good enough to work out what it&#8217;s saying?

### Comment by Ralf Große Wortmann on 2010-09-19 12:45:22 +0000
Hello, i did a short test and choised the chgFontSize. But now i see the IE8 don´t change text in hyperlinks und Firefox don´t change anything &#8211; only the eventkalendar Plugin. 

My Setting: WP 3.0.1, Artisteer Theme, div. Plugins, DIV Base Element leave blank to change the whole blog-text. If i set DIV Base Element to content the IE don\`t work and the Firefox does the same like before.

Can you help me where i have to change something?

my Test link is <a href="http://test-blog.edv-internet-services.de/" rel="nofollow">http://test-blog.edv-internet-services.de/</a>

With best regards

Ralf Große Wortmann

### Comment by Ferdy on 2010-09-19 22:49:03 +0000
Ralf, try using &#8220;contentLayout&#8221; as DIV Base element. Anyway, the problem is in the css file, as it seems it isn&#8217;t compatible with this plugin. There&#8217;re font sentences for hyperlinks that overrides chgfontsize sizes.

### Comment by Moving San Diego on 2010-10-15 01:35:02 +0000
I have done my first attempt but nothing change. Let me update you or ask you a question if there is still a problem arise. By the way, thank for this.

### Comment by Nathalie on 2010-10-22 11:27:23 +0000
Hi

I&#8217;ve installed the plugin and it works great on Google Chrome and Firefox but is not showing on Internet Explorer&#8230;. has anyone come across this and could help?
  
I&#8217;ve tried many other plugins but couldn&#8217;t get them to work at all.

Thank you!!!!
  
Nahtalie

### Comment by Ric on 2010-11-05 16:09:49 +0000
Hi, great plugin..BUT, is it possible to define two base div tags? 

See half my site uses one template using e.g. &#8220;content&#8221; as it&#8217;s base div, but the other half uses a different template that uses e.g. &#8220;content2&#8221; as a base div. 

So unfortunately the plugin only works for half my site!

### Comment by Ric on 2010-11-05 16:26:30 +0000
Sorry, actually I finally just solved it! Just forced and overwrite so I could use the same div element. The functionality would still be nice though for future updates!

### Comment by Patrick on 2010-11-16 23:07:39 +0000
I love the plugin. I have one feature suggestion. When you display the text size options like so: &#8220;A(small) A)medium) A(large)&#8221; could there be a &#8220;.current&#8221; or similar class added to the anchor tag for styling purposes? That would be awesome.

Thanks.

### Comment by Luke on 2010-11-17 15:06:10 +0000
I&#8217;ve just got your plugin which I&#8217;ve seen on other websites. For some reason I can only get it to show one small A to change the text to size 12. However I want it to show 3 A&#8217;s. 

A &#8211; to change to 12
  
A &#8211; to change to 14
  
A &#8211; to change to 16

Any idea how I can do this?

### Comment by gufran on 2010-11-19 09:23:13 +0000
Hi,

i have installed your plug-in on my local WP site.

but it will not work as expected.Please help me to rectify this.

Thanks.

### Comment by Susan on 2011-01-23 07:08:41 +0000
I just found it and really like how easy it makes it for changing font size. It&#8217;s cool that you guys offer this for free also. Thanks!

### Comment by Sulekha on 2011-02-13 02:14:38 +0000
Hi&#8230;
  
Nice Plugin. But it doesnt work for me fine. I am using wordpress version 3.0.4 and default theme &#8220;Twenty Ten 1.1 by the WordPress team&#8221;. When I use Div base element as &#8220;content&#8221;, it changes the size of post content only, when I use DIV base element as &#8220;wrapper&#8221;, it changes size of heading of right sidebar only. Can you please help me which elementshoul I use in Div base element so that it will increase and decrease the font-size of whole page.

Thanks,
  
Sulekha

### Comment by Antoine on 2011-02-20 19:08:47 +0000
Hello thanks for this great plugin, it is the best one that is available for WordPress. One feature would make it utterly perfect, and that is a class id for the selected textsize in the &#8220;Steps&#8221; view. So that a user can see directly which fontsize is selected. Do you have any tip for me how this can be accomplished? Thanks in advance!

### Comment by Andy on 2011-03-02 17:42:15 +0000
Hi there,

I&#8217;m building a site for The Nerve Centre, a place in Huddersfield UK, which supports people with neurological conditions. As such your plugin is very useful. :o)

My problem is that it doesn&#8217;t appear on the homepage. Is there a way of getting it to appear on every page? Some of our users are visually impaired so it would be great to have this option as soon as they arrive.

Thanks a lot, Andy