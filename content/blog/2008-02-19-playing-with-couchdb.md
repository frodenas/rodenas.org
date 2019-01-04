---
title: Playing with CouchDb
author: ferdy
date: 2008-02-18T23:24:28+00:00
url: /blog/2008/02/19/playing-with-couchdb/
b2008:
  - 02
bcategories:
  - Software Development
btags:
  - couchdb
  - erlang
  - json
  - rest
  - schema-free
  - simpledb

---
Over the course of my career working as a software engineer, I have had the opportunity to play with different data structures (arrays, vectors, trees, &#8230;) and different persistence data systems, from hierarchical databases ([IMS DB][1]) to indexed and relative files ([VSAM][2]) to [RDBMS][3]. Even so, I consider myself as an apprentice, and I still have the insane curiosity to learn new persistence data models. That&#8217;s the reason why, recently, I have been playing with [CouchDb][4].

For those of you who do not know CouchDb, it is a distributed, fast, reliable, fault-tolerant and schema-free [document-oriented database][5] accessible via a [RESTful][6] [JSON][7] API. It has been getting a lot of attention lately, specially after [Amazon][8] launched its cloud database system,  [SimpleDB][9], which has some similarities with CouchDb, and after [IBM][10] [hired][11] its creator, [Damien Katz][12], that caused the donation and [acceptance][13] of CouchDb as an incubation project by the [Apache Software Foundation][14]. Despite this hype, it is still an alpha level software, it&#8217;s stable enough for testing but not ready for a production environment.

The first interesting feature about CouchDb is that, unlike typical relational systems, it will not enforce you to use an schema. Instead of designing tables, CouchDb stores in a flat file, called _database_, documents, which are lists of key-value pairs, called _fields_, with no predefined structure. If you want to think in a relational way, databases are tables, documents are rows, and fields are columns, but in the same database (table), you could have different documents (rows) and each row could have any number of different fields (columns) without the need to structure their data types (field = dynamic key + value). So you don&#8217;t need to structure your data in advance, you can do it later if you want using views, which will organize your data adding structure back to semi-structured data. It&#8217;s a &#8220;[Data First vs. Structure First][15]&#8221; strategy.

Here it is an example of a document (using the built in web front end):
  


<center>
  <img src='/blog/images/2008/02/couchdb.png' alt='CouchDb built in web front' />
</center>

&nbsp;

This lack of schema, however, is not a suite-for-all solution, but it could be advantageous in some situations. I&#8217;ll give you a simple example. Imagine you need to create a repository of information related to all the software components of your information system (something like a [CMDB][16]), that is programs (or classes), databases, configuration files, web pages, &#8230; Components has common attributes and specific attributes depending on the type of product. For example, common attributes are type of product, name, description, &#8230; and specific attributes for a program are language, technology used (DB2, MQSeries, &#8230;) &#8230; You will have several approaches to store these information: 

  1. Design a relational table for each type of product with all the attributes (common and specific);
  2. Use only one table with all the common attributes plus some generic attributes (for example, attrib1 varchar(255), &#8230;), and an external [data dictionary][17] that identifies and describes the format of each generic atribute;
  3. No predefined structure, each row stores different attributes depending on the type of product.

From a pure relational perspective, it seems natural to use the first option. But what happens if you&#8217;re a tools vendor and you let the users add they own products? You still have the choice to use the first option, but the problem is a bit more complicated, as you&#8217;ll have to deal with some unknown tables (and, perhaps, not normalized). OK, no _problema_ here, we&#8217;ll just use the second alternative. It&#8217;s a perfect choice (in fact, I&#8217;ve used this approach occasionally), but doesn&#8217;t seem very natural to the relational discipline. And here is when it comes the third approach, each row will have different columns (as a key+value pair) representing the product attributes. In summary, all three options are correct (and yes, I&#8217;m polite because I don&#8217;t want a flame war now), but in this case, it&#8217;s more advantageous to use the schema-free approach.

Another interesting feature is that CouchDb uses the [Erlang OTP][18] platform (internally, you&#8217;ll never see it), which is a perfect choice for highly concurrent access and fault-tolerant systems. But being highly concurrent means that you must try to avoid locks, something hard to design if you want to enforce all [ACID][19] properties. To deal with this situation, CouchDb uses a [MVCC][20] and a [lockless optimistic][21] writer mechanism (in comparison to Mnesia, Erlang&#8217;s DBMS, which uses a pessimistic locking). Using these approaches, readers could access documents without being locked by a writer, seeing only the version of the document that existed when he began reading (despite a writer updated the document at the meantime), because data is always versioned by the writers. But this strategy involves big database files, because they are growing all the time (remember, writers never overwrites data, they only append it, even if you&#8217;re deleting data). And even though CouchDb has an automatically compaction process that clones all the data without any service interruption, it would be nice to see some performance metrics to check which will be the performance parsing large files in Erlang.

The last interesting feature is its simple REST API to manage the data, using JSON for data transport. It is very easy to create, read, update or delete documents and views, that have a unique <acronym title="Uniform Resource Identifier">URI</acronym>, using HTTP resources. Yes, and that means no painful database drivers, just regular HTTP connections, so you can use your favourite HTTP library. Let&#8217;s see some examples using [cURL][22]:

Getting a list of all databases on my local CouchDb server:

<pre>curl -i http://localhost:5984/_all_dbs
</pre>

And the response:

<pre>HTTP/1.1 200 OK
Server: inets/develop
Date: Sat, 16 Feb 2008 23:57:32 GMT
Cache-Control: no-cache
Pragma: no-cache
Expires: Sat, 16 Feb 2008 23:57:32 GMT
Transfer-Encoding: chunked
Content-Type: text/plain;charset=utf-8

["ferdydb","test_suite_db","test_suite_db_a","test_suite_db_b"]
</pre>

Retrieving a document:

<pre>curl -i http://localhost:5984/ferdydb/post-272/
</pre>

And the response. Remember that documents are simple JSON objects:

<pre>HTTP/1.1 200 OK
Server: inets/develop
Date: Sat, 16 Feb 2008 23:58:25 GMT
Cache-Control: no-cache
Pragma: no-cache
Expires: Sat, 16 Feb 2008 23:58:25 GMT
Transfer-Encoding: chunked
Content-Type: text/plain;charset=utf-8
Etag: 1882588955

{
 "_id":"post-272",
 "_rev":"1882588955",
 "Type":"post",
 "Status":"publish",
 "Title":"Playing with CouchDb",
 "Author":"Ferdy",
 "PostDate":"2008-02-17T00:30:52+01:00",
 "Tags":["couchdb","erlang","json","rest","schema-free","simpledb"],
 "Contents":"&lt;p&gt;Over the course of my career working as a softw..."
}
</pre>

Did you see the [Etag header][23]? Let&#8217;s see if it works:

<pre>curl -i http://localhost:5984/ferdydb/post-272/  \
     -H "If-None-Match: "1882588955""
</pre>

It works! Here is the response:

<pre>HTTP/1.1 304 Not Modified
Server: inets/develop
Content-Type: text/html
Date: Sun, 17 Feb 2008 00:26:26 GMT
Cache-Control: no-cache
Pragma: no-cache
Expires: Sun, 17 Feb 2008 00:26:26 GMT
Etag: 1882588955
</pre>

Enough experiments for today, right?

After reading this brief summary, and if you come from a relational model discipline, your first reaction may be &#8220;[WTF][24]&#8220;. But I would encourage you to go deeper with this new persistence data model approach checking the [technical overview][25] page at the [CouchDb Documentation Wiki][26] or reading these [slides][27] by [Jan Lehnardt][28] (don&#8217;t forget the [comments][29] also). You&#8217;ll find a lot more features that I didn&#8217;t explain in this post. And of course, share with me your opinion!

 [1]: http://en.wikipedia.org/wiki/Information_Management_System
 [2]: http://en.wikipedia.org/wiki/VSAM
 [3]: http://en.wikipedia.org/wiki/Relational_database_management_system
 [4]: http://couchdb.org/
 [5]: http://en.wikipedia.org/wiki/Document-oriented_database
 [6]: http://en.wikipedia.org/wiki/RESTful
 [7]: http://en.wikipedia.org/wiki/JSON
 [8]: http://www.amazon.com/
 [9]: http://www.amazon.com/b?ie=UTF8&node=342335011
 [10]: http://www.ibm.com
 [11]: http://damienkatz.net/2008/01/new_gig.html
 [12]: http://damienkatz.net/
 [13]: http://damienkatz.net/2008/02/couchdb_accepte.html
 [14]: http://www.apache.org/
 [15]: http://www.betaversion.org/~stefano/linotype/news/93/
 [16]: http://en.wikipedia.org/wiki/CMDB
 [17]: http://en.wikipedia.org/wiki/Data_dictionary
 [18]: http://www.erlang.org/
 [19]: http://en.wikipedia.org/wiki/ACID
 [20]: http://en.wikipedia.org/wiki/Multiversion_concurrency_control
 [21]: http://en.wikipedia.org/wiki/Optimistic_locking
 [22]: http://curl.haxx.se/
 [23]: http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.19
 [24]: http://www.urbandictionary.com/define.php?term=wtf
 [25]: http://www.couchdbwiki.com/index.php?title=Technical_Overview
 [26]: http://www.couchdbwiki.com/
 [27]: http://jan.prima.de/~jan/plok/archives/105-Slides-From-the-Latest-CouchDB-Talk-at-PHP-UG-FFM.html
 [28]: http://jan.prima.de/plok/
 [29]: http://jan.prima.de/~jan/plok/archives/72-Some-Context.html

## Comments

### Comment by Reuben Moore on 2010-03-29 23:04:42 +0000
Nice article! Very informative and helpful as I learn CouchDB. Thanks.

-Reuben :)+<