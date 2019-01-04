---
title: Reverse engineer the WordPress database with RDA
author: ferdy
date: 2007-01-22T00:39:49+00:00
url: /blog/2007/01/22/reverse-engineer-the-wordpress-database-with-rda/
b2007:
  - 01
bcategories:
  - Data modelling
  - IBM
  - Tools
  - Wordpress

---
I was evaluating some enterprise data modelling tools when I realized that one of them, the new version 7.01 of [Rational Data Architect][1] (RDA), now supports [MySQL][2]. Simultaneous, I was working on a personal project trying to analyse the [WordPress][3] database, that relies on MySQL, in order to understand how does it works. So I decided to combine both projects and try to reverse engineer the MySQL WordPress database with RDA to obtain the WordPress data model.

Based on this experience, I wrote a short tutorial for beginners that explains how you can reverse engineer a MySQL database with RDA. I didn&#8217;t intend to cover all aspects of the product, that is the job of the reference manuals. And if you want to go deeper in the Rational Data Architect functionalities, at the bottom of this article you can also find some [references][4].

So, here it is the tutorial as well as my conclusion. Hope you find it useful.

<!--more-->

### Prerequisites

  1. A [WordPress][5] installation configured and running (so I assume that you have also a [MySQL][6] instance running). In this tutorial we are going to use a wordpress 2.07 database and MySQL 5.0 (despite RDA only supports up to version 4.1).
  2. Rational Data Architect V7.01. If you don&#8217;t have a license and you are just evaluating the product, you can download a [trial][7]. RDA can be installed on top of an existing [Eclipse 3.2][8] environment or will install its own Eclipse 3.2 instance.
  3. A MySQL jdbc driver. You can use the official [MySQL Connector/J][9].

### Creating a new data design project

A data design project is primarily used to store modelling objects, including logical and physical data models, <acronym title="Data Definition Language">DDL</acronym> scripts, mapping models, and more. To create a data design project:

  1. On the main menu bar, select **File > New > Project**. Or, you could right-click in any blank space in the Package Explorer (if you are using the RDA plugin on Eclipse) or in the Data Project Explorer (if you are using RDA with the Eclipse bundled on it) and select **New > Project**. The New Project wizard opens.
  2. Select **Data Design Project**, under the Data folder.
  3. Name the Project **WordPress** and select **Finish**.

### Creating a new physical data model:

A physical data model (PDM) is a database-specific model that represents relational data objects, such as tables, columns, primary and foreign keys. A PDM can be used to generate DDL statements that can then be deployed to a database server.

You can use the New Physical Data Model wizard to create a physical data model:

  1. Select **File > New > Physical Data Model** from the main menu file. The New Physical Data Model wizard opens.
  2. On the first page of the wizard, change the file name of the model to **WordPress PDM**, the selected database to **MySQL**, the selected version to **4.1**, and check the **Create from reverse engineering** check box. Then select **Next**.
<center>
  <a class="imagelink" href="/blog/images/2007/01/figure-1.jpg" title="Creating a new physical data model"><img id="image84" src="/blog/images/2007/01/figure-1.thumbnail.jpg" alt="Creating a new physical data model" /></a>
</center>


  


  3. On the second page, note the **Create a new connection** is checked. Leave that as it is and select **Next**.
  4. On the third panel, specify:
  * Database: The name of the WordPress database, in this case **wordpress**
  * JDBC driver class: **com.mysql.jdbc.Driver**
  * Class location: Browse to the location of the MySQL jdbc driver file **mysql-connector-java-5.0.4-bin.jar**
  * Connection url: **jdbc:mysql://_host_:_port/_**, where **_host_** is the name of the system where MySQL is installed, in this case **localhost**, and **_port_** is the database server port that the MySQL instance is using to listen to communications from remote clients, in this case **3306**
  * User and Password: type your **user ID** and **password**

<center>
  <a class="imagelink" href="/blog/images/2007/01/figure-2.jpg" title="Connection Parameters"><img id="image85" src="/blog/images/2007/01/figure-2.thumbnail.jpg" alt="Connection Parameters" /></a>
</center>


  


  5. Select **Test Connection** and if the connection is successful then select **Next**.
  6. On the fourth panel, select the wordpress schema to reverse engineer and then select **Next**.
  7. On the fifth, select the database elements to reverse engineer and then select **Next**.
  8. On the sixth panel, check the **Generate Overview diagram** option and then select **Next**.
  9. Select **Finish**.

The PDM is created and displayed in the Data Models folder under the WordPress data design project (this model has a .dbm extension to represent physical data model).

If you expand WordPress PDM.dbm and wordpress schema, you will see the database elements we have reverse engineer. Double-click the wordpress diagram, in the Diagrams folder under the wordpress schema, to see the new generated diagram. In the properties tab, you can change the elements that must appear in the diagram.
  


<center>
  <a class="imagelink" href="/blog/images/2007/01/figure-3.jpg" title="Using the diagram, palette, and properties view to design a PDM"><img id="image86" src="/blog/images/2007/01/figure-3.thumbnail.jpg" alt="Using the diagram, palette, and properties view to design a PDM" /></a>
</center>

### Creating the foreign key relationships

As wordpress database doesn&#8217;t use foreign keys, we must create them manually in order to see relationships between tables. To create a foreign key relationship from a parent table to a child parent table in a physical data model diagram:

  1. Select a type of relationship in the palette.
  2. Select the parent table that has the primary key
  3. Drag to the child table. Depending on the type of relationship you are creating, a pop up window might open asking you to specify relationship options.</li> 

Be aware that the key from the parent table is migrated to the child table. As wordpress doesn&#8217;t use a similar name on the child table, we must delete this new field at the child table and assign manually the relation between the primary key at the parent table and the foreign key at the child table.

  1. In the Data Project Explorer view, select the **WordPress PDM** model and then the **wordpress** schema.
  2. Select the **child table** to modify.
  3. Select the **Foreign key relation** to modify.
  4. Select **Details** under the **Properties** tab.
  5. Select the appropriate **column** in the child table.
  6. Delete the generated column in the child table.

<center>
  <a class="imagelink" href="/blog/images/2007/01/figure-5.jpg" title="Foreign keys details"><img id="image87" src="/blog/images/2007/01/figure-5.thumbnail.jpg" alt="Foreign keys details" /></a>
</center>


  


So in order to establish all relations, we must create manually the following relationships:

  * wp\_linkcategories[cat\_id] -> wp\_links[link\_category]
  * wp\_categories[cat\_ID] -> wp\_post2cat[category\_id]
  * wp\_categories[cat\_ID] -> wp\_categories[category\_parent]
  * wp\_posts[ID] -> wp\_post2cat[post_id]
  * wp\_posts[ID] -> wp\_comments[comment\_post\_ID]
  * wp\_posts[ID] -> wp\_posts[post_parent]
  * wp\_posts[ID] -> wp\_postmeta[post_id]
  * wp\_comments[comment\_ID] -> wp\_comments[comment\_parent]
  * wp\_users[ID] -> wp\_links[link_owner]
  * wp\_users[ID] -> wp\_posts[post_author]
  * wp\_users[ID] -> wp\_comments[user_id]
  * wp\_users[ID] -> wp\_usermeta[user_id]



And you will get this final diagram:
  


<center>
  <a class="imagelink" href="/blog/images/2007/01/figure-6.jpg" title="Wordpress Physical Data Model"><img id="image88" src="/blog/images/2007/01/figure-6.thumbnail.jpg" alt="Wordpress Physical Data Model" /></a>
</center>



You can also define the referential integrity constrains, but this is not the object of this tutorial.

### Publishing the data model

Finally, you can publish the data model outside of the modelling tool, as an HTML page or as a PDF file. To create a PDF report:

  1. In the Data Project Explorer view, select the **WordPress PDM** model to on which to create a report.
  2. On the main menu bar, select **Data > Publish > Report**.
  3. In the Generate Report window, select the **Diagram Report for Physical Data Model**. Each row contains information on the type of file to be generated, the name of the report, and a description.
  4. Type an **output file name** in the Select the file name for the generated report field.
  5. Select **OK** to publish the model report.

### Summary

In this tutorial you learned how to create a new physical data model and reverse engineer an existing MySQL database. You created a foreign key relationship from a parent table to a child parent table, and you modified the columns involved in the relationship. Finally, you published the data model outside of the modelling tool, as a PDF file.

### My opinion

Rational Data Architect supports lots of relational data sources ([Cloudscape][10], [DB2 Universal Database (UDB)][11], [DB2 UDB iSeries][12], [DB2 UDB zSeries][13], [Derby][14], [Informix][15],  [MySql][2], [Oracle][16], [Microsoft® SQL Server][17] and [Sybase][18]), and that it&#8217;s great.

You can work in the Logical model or in the Physical model separately, and you have the ability to transform a Logical model to a Physical model or vice versa. This sounds good, as you can differentiate roles but reusing the previous work: analysts designs the application, the logical model, and developers could implement the physical model based on the target <acronym title="Database Management System">DBMS</acronym> reusing the work done by the analyst. The only problem is that both models are not synchronized, so if the analyst changes an entity in the logical model, it is not propagated to the physical model, and this could be a mess.

It&#8217;s very easy to reverse engineer a database, as I have show you in this tutorial. The biggest concern about obtaining a data model through reverse engineering is discovering relationships. This is a hard work, as many apps database designs doesn&#8217;t use foreign keys (as WordPress) and they don&#8217;t tend to normalize column names. RDA has a discover function that can help you find the matching elements automatically so that you don&#8217;t have to specify them manually. I need to check deeper this functionality, but I don&#8217;t have a hope that it will succeed completely, as there are lots of relations that rely on the code, not in the database.

It will be very useful that when you create a new relation between two entities/tables, you could also specify the child column. In the tutorial example, I had to delete the new field created automatically at the child table and to assign manually the relation between the primary key at the parent table and the foreign key at the child table. In my opinion, this steps can be avoided if you let specify which is the target child column.

RDA can be installed on top of an existing Eclipse 3.2 environment or will install its own Eclipse 3.2 instance. I didn&#8217;t find any list of plug-in dependencies in the installation guide, so I tried to install RDA on top of my existing Eclipse 3.2 (Birt, CDT, DTP, PHP, TPTP and WTP). The plug-in worked fine, except some few functionalities as the report generation and the XML Schema Validator. This is a problem that I have had with lots of Eclipse plug-ins. If you don&#8217;t want to deal with plug-in dependencies problems, my recommendation is to install RDA with its own Eclipse instance.

I have also found some bugs:

  * You can not specify a precision for the BIGINT numerical type, despite you can specify it in MySQL.
  * RDA doesn&#8217;t support the MySQL **ENUM** type. Enum is not a SQL standard (you must create a separate table that maps different values or use a check restriction), but if the RDA brochure says it supports MySQL then it must support the ENUM type.
  * With the previous problem in the physical model, RDA doesn&#8217;t generate DDL, despite there isn&#8217;t any error in the Problems tabs and no message appeared in the Generate DDL wizard. This problem drives me crazy, until I found the problem. It will be very useful to have a validation utility.

Despite these bugs, Rational Data Architect made a very good impression on me.

### <a id="references">References</a>

  * &#8220;[Use Rational Data Architect to define and enforce data object naming standards][19]&#8221; (developerWorks, Jan. 2007) examines the features of IBM Rational Data Architect that enable users to define and implement object naming standards, and then demonstrates with a real-world example.
  * RDA skills series at [developerWorks][20]:
  * &#8220;[Rational Data Architect skills series, Part 3: Discover schema relationships with Rational Data Architect][21]&#8221; (developerWorks, Dec. 2006) describes how to create schema mappings semi-automatically.
  * &#8220;[Rational Data Architect skills series, Part 2: Generate SQL/XML queries with Rational Data Architect][22]&#8221; (developerWorks, Sep. 2006) describes how to transform data from relational data sources into XML format.
  * &#8220;[Rational Data Architect skills series, Part 1: Access and integrate enterprise metadata with Rational Data Architect][23]&#8221; (developerWorks, Jul. 2006) describes how to create a unified view across heterogeneous data sources.

 [1]: http://www-306.ibm.com/software/data/integration/rda/
 [2]: http://www.mysql.com
 [3]: http://wordpress.org
 [4]: #references
 [5]: http://wordpress.org/download/
 [6]: http://dev.mysql.com/downloads/mysql/5.0.html
 [7]: http://www.ibm.com/developerworks/downloads/r/rda/?S_TACT=105AGX28&S_CMP=TRIALS
 [8]: http://www.eclipse.org/downloads/
 [9]: http://www.mysql.com/products/connector/j/
 [10]: http://www-306.ibm.com/software/data/cloudscape/
 [11]: http://www-306.ibm.com/software/data/db2/
 [12]: http://www-03.ibm.com/servers/eserver/iseries/db2/
 [13]: http://www-306.ibm.com/software/data/db2/zos/
 [14]: http://db.apache.org/derby/
 [15]: http://www-306.ibm.com/software/data/informix/
 [16]: http://www.oracle.com/database/index.html
 [17]: http://www.microsoft.com/sql/default.mspx
 [18]: http://www.sybase.com/
 [19]: http://www-128.ibm.com/developerworks/db2/library/techarticle/dm-0701liu/
 [20]: http://www-128.ibm.com/developerworks
 [21]: http://www-128.ibm.com/developerworks/edu/ar-dw-ar-rdamap.html
 [22]: http://www-128.ibm.com/developerworks/edu/dm-dw-dm-0609bittner-i.html
 [23]: http://www-128.ibm.com/developerworks/edu/ar-dw-ar-wbirda.html

## Comments

### Comment by Edward de Leau on 2008-02-07 04:53:57 +0000
Great stuff, i was planning to do this but before i started i googled on it and found this. I&#8217;m going to try this also this weekend (i think), thanks for the great tutorial.

### Comment by Edward de Leau on 2008-02-07 04:57:23 +0000
The fun thing will be that both RDA and WordPress have new versions!