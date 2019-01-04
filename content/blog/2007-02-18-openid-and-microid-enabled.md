---
title: OpenID and MicroID enabled
author: ferdy
date: 2007-02-17T23:24:58+00:00
url: /blog/2007/02/18/openid-and-microid-enabled/
b2007:
  - 02
bcategories:
  - Off topic
  - Wordpress

---
I have enabled [OpenID][1] at this site through the [WordPress OpenID plugin][2], so now you will be able to leave comments using your OpenID identity.

If you haven&#8217;t heard about it, OpenID is a &#8220;decentralized digital identity system, in which any user&#8217;s online identity is given by <acronym title="Uniform Resource Identifier">URI</acronym> (such as for a blog or a home page) and can be verified by any server running the protocol&#8221;. Uh, mmm, uhhh, what? Basically, that you can use the <acronym title="Uniform Resource Locator">URL</acronym> of your blog or other website as an identity to sign in or leave comments on others sites without the need to type your name, email and website and preventing the spoof of your ID. A lot of this is explained by Simon Willison in his [post about OpenID][3] or in his [screencast][4].

I also have enabled [MicroID][5], &#8220;a lightweight identity layer for the web that enables anyone to claim verifiable ownership over content hosted anywhere on the web&#8221;. I have installed the [MicroID plugin for WordPress][6], that attach a microID on each of the comments (based on the supplied email address and URL of the commentator), so now you will be able to claim your comments by using a service like [claimID][7].

 [1]: http://openid.net/
 [2]: http://verselogic.net/projects/wordpress/wordpress-openid-plugin/
 [3]: http://simonwillison.net/2006/Dec/19/openid/
 [4]: http://simonwillison.net/2006/openid-screencast/
 [5]: http://microid.org/
 [6]: http://www.richardkmiller.com/blog/archives/2006/03/microid-plugin-for-wordpress
 [7]: http://claimid.com/