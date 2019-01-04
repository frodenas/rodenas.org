---
title: Unix System Services roll-out history
author: ferdy
date: 2007-03-20T00:09:57+00:00
url: /blog/2007/03/20/unix-system-services-roll-out-history/
b2007:
  - 03
bcategories:
  - IBM
  - Mainframe

---
[Mark Cathcart][1] has posted a [nice article][2] about the [Unix System Services][3] roll-out process. He provides a historical overview of the decisions involved in the revitalization of the mainframe back in the early 90’s.

Personally, I remember when we introduced <acronym title="Unix System Services">USS</acronym> at my company about 8 years ago. It was a hard but also a funny work. Lots of mainframe guys dealing with a subsystem under [OS/390][4] that has a strange behaviour and terminology.

> What the hell is a &#8220;_sticky bit_&#8220;?
  
> Oh, I see, it&#8217;s an executable that resides on <acronym title="Link Pack Area">LPA</acronym> or <acronym title="Linked List">LNKLST</acronym>.
  
> Why this guys doesn&#8217;t speak more clear! 

> Can I manage the user access rights via [TSS][5]?
  
> Yes but not. Do you know what are the file mode permissions bits?
  
> Ehhhhhh? 

I also remember when I personally had to deal with [Rexx][6] and USS. We needed to implement a change control system to manage the production environment changes. Executing OpenEdition (USS former name) services through the &#8220;_Address Syscall_&#8221; Rexx instruction under a [TSO][7]/[ISPF][8] environment on a OS/390 mainframe was very very funny (and painful!).

I remember specially when one of our sysprogs executed the &#8220;_rm_&#8221; instruction on the development root filesystem using the change control user, which was, logically, a superuser. Just imagine his face when he realized what he has done! After this destructive action, we created an &#8220;_rm_&#8221; alias to prevent these kind of incidents.

Snif, I miss these great moments.

 [1]: http://cathcam.wordpress.com/
 [2]: http://cathcam.wordpress.com/2007/03/03/looking-back-unix-system-services-linux-et-al/
 [3]: http://www-03.ibm.com/servers/eserver/zseries/zos/unix/
 [4]: http://en.wikipedia.org/wiki/OS/390
 [5]: http://www3.ca.com/solutions/ProductFamily.aspx?ID=141
 [6]: http://en.wikipedia.org/wiki/REXX
 [7]: http://en.wikipedia.org/wiki/Time_Sharing_Option
 [8]: http://en.wikipedia.org/wiki/ISPF