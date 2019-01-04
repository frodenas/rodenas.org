---
title: My own OpenID identity provider
author: ferdy
date: 2007-02-23T23:03:58+00:00
url: /blog/2007/02/24/my-own-openid-identity-provider/
b2007:
  - 02
bcategories:
  - Off topic

---
After [enabling OpenID authentication at this site][1], I was wondering if I could become my own [OpenID][2] identity provider. [Googling][3] for references, I have found a detailed guide at Sam Ruby post [OpenID for non-SuperUsers][4].

I followed Sam&#8217;s instructions, but I found a problem when I tried to delegate my identity. Sam&#8217;s post talks about [decrufting][5] the openid.delegate, setting _$idp_url_ to the value you want it to be, in this case, my blog address. The problem is that I must use [phpMyID][6] version 0.5 instead of version 0.3 (I&#8217;m running PHP in <acronym title="Common Gateway Interface ">CGI</acronym> mode), and this hack doesn&#8217;t work with version 0.5.

After reviewing the phpMyID code, it seems that the _MyID.php_ script checks that the end user identity matches the <acronym title="Identity Provider">IdP</acronym> URL, and this is the main reason which caused the problem. So why don&#8217;t define a &#8220;delegate&#8221; var and use it as the identity match? In this way, you can authenticate a controlled end user identity URL that it&#8217;s different to the IdP URL. I modified the code and [tested][7] the new setup. Now it works!

So, if you have the same problem, download this [patch version of phpMyID][8], change the _$profile[&#8216;delegate&#8217;]_ at _MyID.config.php_ file, and run it again.

PD: I have emailed Christopher J. Niemira, but unfortunately I didn&#8217;t have any response from him.

 [1]: http://www.rodenas.org/blog/2007/02/18/openid-and-microid-enabled/
 [2]: http://openid.net/
 [3]: http://en.wikipedia.org/wiki/Google_(verb)
 [4]: http://www.intertwingly.net/blog/2007/01/03/OpenID-for-non-SuperUsers
 [5]: http://en.wikipedia.org/wiki/Cruft
 [6]: http://siege.org/projects/phpMyID/
 [7]: http://www.openidenabled.com/resources/openid-test/checkup
 [8]: /blog/images/2007/02/myid.zip "phpMyID patch version"