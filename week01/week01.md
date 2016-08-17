# <i class="fa fa-database"></i> INFOSYS 222
### Week 01: Introduction
<i class="fa fa-copyright"></i> [Johnny Chan](mailto:jh.chan@auckland.ac.nz) | <i class="fa fa-twitter"></i> [@infosys222](http://twitter.com/infosys222)



## <i class="fa fa-list-alt"></i> Agenda
- Practical information about the course

- Why study database?

- What you would learn from the course

- Overview of the course

- Course schedule



## <i class="fa fa-group"></i> People
Role | Name
--- | ---
Lecturer | Johnny Chan [<i class="fa fa-envelope-o pull-right"></i>](mailto:jh.chan@auckland.ac.nz)
Coordinator | Udayangi Muthupoltotage [<i class="fa fa-envelope-o pull-right"></i>](mailto:u.muthupoltotage@auckland.ac.nz)
Tutor | Denzil Brokken, Grace Li, Jose Ortiz, Mai Honda, Kun Qian, Shivanka Kathiravel, Veronika Ott, Zubair Mohamed
Student | 200+ of you from A to Z


## <i class="fa fa-road"></i> Activity
- Lecture (Week 01 - Week 12)
	- Mon 11:00 @ 401-401
	- Tue 12:00 @ 260-115
	- Wed 11:00 @ 260-073

- Lab (Week 02 - Week 11)
	- A 1.5-hr lab session on Wed, Thu or Fri
	- Attend only your enrolled session

- Working on your own
	- At least 6 hours per week
	- Knowledge → Understanding → Skill


## <i class="fa fa-calendar-check-o"></i> Assessment
- Internal (50%)
	- Assignment 01: started on 01/08; due on 22/08 Mon 10:00 (15%)

	- Assignment 02: started on 19/09; due on 10/10 Mon 10:00 (15%)

	- Test: held on 23/09 Fri 18:30-20:00 (20%)

- Exam (50%)

📢 Students __must__ [pass](https://uoa.custhelp.com/app/answers/detail/a_id/2748/~/marking-schemes-or-grade-scales-at-the-university-of-auckland) both internal and exam separately


## <i class="fa fa-wrench"></i> Resource
- LMS: All course related material could be found in [Canvas](https://canvas.auckland.ac.nz/courses/2932) including announcements, lecture slides, lab slides, assessment specifications, and marks

- Discussion Forum: [Piazza](https://piazza.com/class/iphe9yxcc9m79g)

- Reading: There is no textbook nor course book. Most readings for this course could be accessed online where [links](https://auckland.rl.talis.com/lists/67385800-22DC-21D5-CBF3-00CC4AFE9E1E.html) are provided

- Software: [Draw.io](https://www.draw.io) or [ERWin](https://software.isom.auckland.ac.nz/Software/Details/ee120a1f-1975-4404-a882-ee28f8b69ef9), [SQLite](http://sqlite.org/download.html) and [Atom](https://atom.io/) (or any text editor)


## <i class="fa fa-phone"></i> Communication
- Discussion Forum: This is the primary platform for Q&A related to any course material and administrative matter. Please check if your question has been asked and answered before posting one

- Email: Use it for _private message_ only. Direct all administrative matter and lab material to the coordinator; lecture material and assessment question to the lecturer

- Office Hour: By appointment only (Mon 12:00-13:00 @ 260-349)

- Class Rep: [Ryan Edwards](mailto:redw764@aucklanduni.ac.nz)



## Why study database?
- Database is an interesting topic that relates to a wide range of domains beyond information systems, including computer science, mathematics, accounting, marketing and so on

- Most if not all software applications need to have a database

- It helps [data scientist](https://en.wikipedia.org/wiki/Data_science) to deal with large and distributed datasets

- Under the trend of increasing complexity, the demand for database to host our ever growing data would only go up



## What you would learn
- By the end of this course, students would have gained a solid background in database design and implementation. Specifically:

	- use [data modelling](https://en.wikipedia.org/wiki/Data_modeling) to define and analyse data requirements
	- design a database in [entity-relationship (ER) model](https://en.wikipedia.org/wiki/Entity%E2%80%93relationship_model) and translate that to the [relational model](https://en.wikipedia.org/wiki/Relational_model)
	- Utilise theoretical technique like [normalisation](https://en.wikipedia.org/wiki/Database_normalization) to improve database design and implementation
	- program basic to complex queries in [SQL](https://en.wikipedia.org/wiki/SQL)
	- understand the [fundamentals](https://en.wikipedia.org/wiki/Database) of a relational database management system (DBMS)
	- recognise database technologies beyond relational DBMS



## Overview of the course
- What is a database?

- What is a DBMS?

- What is a relational database?

- How to design a relational database?

- How to implement and use a relational database?


## What is a database?
- According to the [Oxford Dictionary](http://www.oxforddictionaries.com/definition/english/database):

	> A structured set of data held in a computer, especially one that is accessible in various ways

- 😶 How is a database different from a file system?

- It is a collection of information that exists over a long period of time; the term database refers to a collection of data that is managed by a database management system (DBMS)


## What is a DBMS?
> It is a system for providing __efficient__, __convenient__, and __safe__ storage of and __multi-user__ access to (possibly __massive__) amounts of __persistent__ data

- 😶 Think of five examples when each of the bolded words applies

- The [evolution](https://en.wikipedia.org/wiki/Database#History) of DBMS: hierarchical → network → relational → object-oriented → object-relational


## What is a relational database?
- All major general purpose DBMSs are based on the so-called [relational data model](https://en.wikipedia.org/wiki/Relational_model). It means that all data are stored in a number of named tables (with named columns), such as the following table __Account__:

accNo | balance | type
--- | --- | ---
11111 | 1234.50 | saving
22222 | 7654.32 | check
99999 | -8888.00 | loan

- For historical, mathematical reasons such table is referred to as a relation. This course focuses solely on [relational database](https://en.wikipedia.org/wiki/Relational_database) and relational DBMS


## How to design a relational database?
- It is often far from obvious to decide how to store data from an application as relations. A considerable part of the course will deal with a methodology for good relational database design

- 😶 Suggest how to represent the following types of data as one or more relations: 1) a contact list, 2) a shopping cart

- 😶 Can you avoid (or reduce) duplication of data?


## Database design methodology
- We will cover the dominant design methodology for relational database, which consists of three steps:

	1. Identify all relevant entities and relationships, and use an ER model to describe them
	2. Convert the ER model to a number of relations
	3. Eliminate (or reduce) redundancy by splitting up relations. This process is known as normalisation

- Data modelling can also be differentiated among three stages:
	- conceptual → logical → physical


## How to implement and use a relational database?
- The success of relational database is largely due to the existence of powerful programming language for writing database queries

- The most important of such language is [structured query language (SQL)](https://en.wikipedia.org/wiki/SQL):
	- convenience: queries can be written with little effort
	- efficiency: even for large datasets, a good DBMS can answer queries written in SQL very quickly



## SQL

accNo | balance | type
--- | --- | ---
11111 | 1234.50 | saving
22222 | 7654.32 | check
99999 | -8888.00 | loan

- Consider the relation __Account__, the command to get the balance from accNo 22222:

	```
SELECT balance
FROM Account
WHERE accNo = 22222;
	```
<!-- .element: contenteditable="true" -->


## SQL: example

```
SELECT accNo, balance
FROM Account
WHERE type = ‘loan’
AND balance < -10000;
```
<!-- .element: contenteditable="true" -->

```
SELECT *
FROM Account
WHERE accNo > balance;
```
<!-- .element: contenteditable="true" -->

📢 * is the shorthand for all columns/attributes


## SQL: more example

accNo | name | address
--- | --- | ---
11111 | Dexter Morgan | 666 Miami Road
22222 | Steven Roger | 222 Patriot Street
22222 | Peggy Carter | 999 Marvel Avenue
99999 | John Reese | 314 Machine Place

- Suppose we have a related relation __Holder__, the command to get the names of holders with check accounts:

	```
SELECT name
FROM Account, Holder
WHERE Account.accNo = Holder.accNo
AND Account.type = 'check';
	```
<!-- .element: contenteditable="true" -->


## SQL: SELECT-FROM-WHERE
```
SELECT column1, column2, ...
FROM relation1
WHERE <conditions>;
```

```
SELECT column1, column2, ...
FROM relation1, relation2, ...
WHERE <join conditions>
AND <conditions>;
```


## SQL: Quiz
- Consider the relation [__Account__](#/6) again

	Write a SQL command that lists all accounts (with accNo and type) that have a positive balance

	```
SELECT ...
FROM ...
WHERE ...

	```
<!-- .element: contenteditable="true" -->


## SQL: Syntax and semantics
- As demonstrated, SQL command resembles asking question in English. Quite often, the effect of a command can be intuitively understood

- During the course you will learn how to compose much more complex command in SQL. To do that you need a precise understanding of SQL’s:

	- Syntax: The way SQL command could be written
	- Semantics: The meaning of a SQL command  


## SQL: More aspects
- SQL is based on a mathematical formalism called [relational algebra](https://en.wikipedia.org/wiki/Relational_algebra)

- In addition to queries, SQL can be used to express many types of database operations:
	- Define new relations
	- Perform changes to data (e.g. insert, update and delete)
	- Set up constraints and triggers
	- Manage users, permissions, etc
	- Control transactions in a multi-user environment



## Other topics in the course
- Besides from data modelling and SQL, this course also covers:

	- Database efficiency

	- Transaction management

	- Concurrency management

	- Data warehouse (OLAP)

	- Beyond relational DBMS



## <i class="fa fa-list-alt"></i> Summary
- By now you should:

	- know what this course is about

	- know how you could do well in this course

	- know a little about some key concepts: database, DBMS, relation, SQL; and know how they fit into the course

	- understand SELECT-FROM-WHERE of SQL


## <i class="fa fa-book"></i> Reading
- Essential
	- [The Worlds of Database Systems (p1-13)](http://infolab.stanford.edu/~ullman/fcdb/ch1.pdf)

	- [Introduction from SQL for Web Nerds](http://philip.greenspun.com/sql/introduction.html)

- Further
	- [Database from Wikipedia](https://en.wikipedia.org/wiki/Database)


## <i class="fa fa-calendar"></i> Schedule
Week | Lecture | Lab
--- | --- | ---
01 | Introduction <i class="fa fa-check fa-pull-right"></i>| No lab <i class="fa fa-check fa-pull-right"></i>
02 | Relational model | Introduction
03 | ER modelling | ER diagram
04 | Data modelling | Data modelling
05 | Data modelling | Workshop
06 | Normalisation | Normalisation
07 | SQL | SQL
08 | SQL | SQL
09 | SQL | SQL
10 | DBMS fundamentals | Workshop
11 | Data warehouse | Data warehouse
12 | Review | No lab



# THE END
<canvas width=300 height=300 class="anything">
<!--
{
  "initialize": "function(container) {
	var width = container.width,
	    height = container.height;
	var projection = d3.geo.orthographic()
	    .translate([width / 2, height / 2])
	    .scale(width / 2 - 20)
	    .clipAngle(90)
	    .precision(0.6);

	var c = container.getContext('2d');

	var path = d3.geo.path()
	    .projection(projection)
	    .context(c);

	var title = container.parentElement.querySelector('.country');
	queue()
	    .defer(d3.json, '../asset/world-110m.json')
	    .defer(d3.tsv, '../asset/world-country-names.tsv')
	    .await(ready);

	function ready(error, world, names) {
	  if (error) throw error;

	  var globe = {type: 'Sphere'},
	      land = topojson.feature(world, world.objects.land),
	      countries = topojson.feature(world, world.objects.countries).features,
	      borders = topojson.mesh(world, world.objects.countries, function(a, b) { return a !== b; }),
	      i = -1,
	      n = countries.length;

	  countries = countries.filter(function(d) {
	    return names.some(function(n) {
	      if (d.id == n.id) return d.name = n.name;
	    });
	  }).sort(function(a, b) {
	    return a.name.localeCompare(b.name);
	  });

	  (function transition() {
	    d3.transition()
	        .duration(1250)
	        .each('start', function() {
			while ( !countries[i = (i + 1) % n] ) {};			
			title.innerHTML = (countries[i].name);
	        })
	        .tween('rotate', function() {
	          var p = d3.geo.centroid(countries[i]),
	              r = d3.interpolate(projection.rotate(), [-p[0], -p[1]]);
	          return function(t) {
	            projection.rotate(r(t));
	            c.clearRect(0, 0, width, height);
	            c.fillStyle = '#fff', c.lineWidth = 2, c.beginPath(), path(globe), c.fill();
	            c.fillStyle = '#42affa', c.beginPath(), path(land), c.fill();
	            c.fillStyle = '#f00', c.beginPath(), path(countries[i]), c.fill();
	            c.strokeStyle = '#ccc', c.lineWidth = .5, c.beginPath(), path(borders), c.stroke();
	            c.strokeStyle = '#ccc', c.lineWidth = 2, c.beginPath(), path(globe), c.stroke();
	          };
	        })
	      .transition()
	        .each('end', transition);
	  })();
	}

	d3.select(self.frameElement).style('height', height + 'px');

    }"
}
-->
</canvas>

#### Database rules in <span class="country">Everywhere</span>!
[<i class="fa fa-print"></i>](?print-pdf#)
