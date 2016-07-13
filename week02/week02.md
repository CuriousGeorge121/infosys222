# <i class="fa fa-database"></i> INFOSYS 222
### Week 02: Relational model
[Johnny Chan](mailto:jh.chan@auckland.ac.nz) | [@infosys222](http://twitter.com/infosys222)



## <i class="fa fa-history"></i> Previously on 222 ...
- Database and DBMS

- The intuitive concept of a relation as a two-dimensional table

- Basic SQL command
	- SELECT-FROM-WHERE



## <i class="fa fa-list-alt"></i> Agenda
- What is the relational data model?

- What is SQL?



## The relational data model
- A model is an _abstraction_ of the reality or part of the reality

- A data model is a precise and conceptual way of describing and specifying the data stored in a database
	- structure of the data
	- operation on the data
	- constraint on the data

- The relational data model is a data model where all data takes the form of relation


## Tuple
- A relation consists of tuples:

	> A tuple is an __ordered list__ of __values__

- Tuples are usually written in parentheses with commas separating the values or components, e.g.

	(Interstellar, 2014, 169, colour)

	which contains the four values: Interstellar, 2014, 169, and colour

- 📢 The order of values in a tuple is important, i.e., the tuple (Interstellar, 169, 2014, colour) is different from the tuple above


## Relation
> A relation is a __set__ of tuples

- A relation is always defined on certain __domains__:
	- the sets from which the values in the tuples come from

- Example: The tuple (Interstellar, 2014, 169, colour) could be part of a relation defined on the domains of:
	- text
	- integer
	- integer
	- { 'colour', 'black and white' }

- 📢 Order does not matter in a set


## Attribute
- In order to refer to the different components in a tuple, we assign them names (called attributes)

- Example: For the tuple (Interstellar, 2014, 169, colour) we could choose the attributes title, year, length, and filmType

	The attribute _length_ would refer to the third component of the tuple with a value of 169


## Data type
- The value of an attribute belongs to a domain; it is also known as a __data type__ of an attribute

- In SQL, each attribute must be defined with a data type, and the data type specificity and availability would depend on the particular DBMS. However, the following are commonly available among different implementations:

	- TEXT for text strings
	- INTEGER for integers
	- REAL for real numbers
	- DATE for Gregorian dates


## The relation Movie
title | year | length | filmType
--- | --- | --- | ---
Interstellar | 2014 | 169 | colour
Nebraska | 2013 | 115 | black and white
Inception | 2010 | 148 | colour

<br />

title | filmType | length | year
--- | --- | --- | ---
Nebraska | black and white | 115 | 2013
Inception | colour | 148 | 2010
Interstellar | colour | 169 | 2014

🤔 Are these two relations the same?


## Same data different model

```
<movies>
	<movie title="Interstellar" filmType="colour">
		<Year>2014</Year>
		<Length>169</Length>
	</movie>
	<movie title="Nebraska" filmType="black and white">
		<Year>2013</Year>
		<Length>115</Length>
	</movie>
	<movie title="Inception" filmType="colour">
		<Year>2010</Year>
		<Length>148</Length>
	</movie>
</movies>
```
<!-- .element: contenteditable="true" -->


## Schema
- In the relational data model, a relation is often described using a schema which consists of:
	- the name of the relation
	- the set of its attributes (with or without data types)

- Example: The relation Movie can be described by the schema:

	- Movie (title, year, length, filmType)
	- Movie (title TEXT, year INTEGER, length INTEGER, filmType TEXT)

- The schemas of all relations in a database form a __database schema__


## Relation instance
- A relation is not static; it changes over time:
	- inserting new tuples
	- updating existing tuples
	- deleting tuples

- A set of tuples of a relation at a particular moment is known as an instance of that relation. As a convention DBMS maintains only one version of any relation - the current instance

- It is less common for the schema of a relation to change, and it could be very expensive when that happens  
	- 🤔 Why is that?


## Key
- There are many constraints on relations that the relational data model allows. The most fundamental one is the key constraint

- A set of attributes forms a __key__ for a relation if we do not allow two tuples in a relation instance to have the same values in all the attributes of the key  
	- 🤔 Why is this important?

- Artificial key is often used in the real world situation to provide absolute uniqueness to each tuple of a relation

- 🤔 Underline/highlight the attribute(s) that could form the key:

	Movie (<span class="fragment highlight-red">title</span>, <span class="fragment highlight-red">year</span>, length, filmType)



## Quiz 01
accNo | balance | type
--- | --- | ---
11111 | 1234.50 | saving
22222 | 7654.32 | check
99999 | -8888.00 | loan

- Given the relation __Account__, indicate clearly:

	- the tuples of the relation
	- the attributes of the relation
	- a suitable domain for each attribute
	- the relation schema for the relation with key



## Quiz 02
- Define a set of relations in schemas to model the data of a movie in [IMDb](http://www.imdb.com/)

- Make as many assumptions about the data as needed

[![Interstellar](interstellar.jpg) <!-- .element: style="width:40%; height:40%" -->](http://www.imdb.com/title/tt0816692/)



## SQL
- __Structured query language (SQL)__ is a declarative language used to describe and manipulate relational database. It was adopted as a standard by [ANSI](https://en.wikipedia.org/wiki/American_National_Standards_Institute) and [ISO](https://en.wikipedia.org/wiki/International_Organization_for_Standardization). However, most DBMS vendors implement their products similar but not identical to the standards

	- [Data definition language (DDL)](https://en.wikipedia.org/wiki/Data_definition_language)
	- [Data manipulation language (DML)](https://en.wikipedia.org/wiki/Data_manipulation_language)

- 🤔 How is SQL different from a programming language like Java?

- <i class="fa fa-book"></i> Further: [SQL from Wikipedia](http://en.wikipedia.org/wiki/SQL)


## Relation in SQL

- SQL defines a relation and stores it in a DBMS as a __table__ (with attribute becomes __column__ and tuple becomes __row__)

- The simplest way of declaring a schema of a relation in SQL begins with the keywords __CREATE TABLE__, followed by the relation name, and a list of attribute names with data types:

	```
CREATE TABLE Movie (
	title TEXT,
	year INTEGER,
	length INTEGER,
	filmType TEXT
);
	```

- 📢 All sample SQL codes are based on [SQLite](http://sqlite.org/lang.html) syntax


## Modifying relation schema
- To remove the entire relation R with all its tuples from the database:
	```
DROP TABLE R;
	```

- To rename the relation R to S:
	```
ALTER TABLE R RENAME TO S;
	```

- To add an attribute to the relation R:
	```
ALTER TABLE R ADD COLUMN newColumn1 TEXT;
ALTER TABLE R ADD COLUMN newColumn2 TEXT DEFAULT 'Yes';
	```

- 🤔 What is the default value of an attribute when it is not explicitly specified?

- 🤔 How to delete an existing attribute from the relation R?


## Declaring key constraint
- In SQL, key(s) is/are declared when a relation is defined from the schema:
	```
CREATE TABLE Movie (
	title TEXT,
	year INTEGER,
	length INTEGER,
	filmType TEXT,
	PRIMARY KEY (title, year)
);
	```


## Declaring other constraint
- Besides from the PRIMARY KEY, there are other constraints available for declaration:

	- NOT NULL
	- UNIQUE
	- FOREIGN KEY
	- CHECK
	- DEFAULT

- <i class="fa fa-book"></i> Further: [Constraints in SQLite](http://zetcode.com/db/sqlite/constraints/)


## INSERT, UPDATE and DELETE
- To insert a new tuple into the relation Movie:
	```
INSERT INTO Movie VALUES
('Interstellar', 2013, 168, 'colour');
	```

- To update the value of an attribute in an existing tuple:
	```
UPDATE Movie
SET year = 2014, length = 169
WHERE title = 'Interstellar';
	```

- To delete a tuple:
	```
DELETE FROM Movie
WHERE title = 'Interstellar';
	```
	
- 🤔 Are these DDL or DML?



## Quiz 03
- Given the following relations:
	- Product (maker, model, type)
	- PC (model, speed, ram, hd, price)
	- Laptop (model, speed, ram, hd, screen, price)
	- Printer (model, colour, type, price)

- Write the SQL command to declare:
	1. the schemas for the relations Product, PC, Laptop and Printer
	2. an alteration to the schema of the relation Laptop to add the attribute od (optical-disk type). Let the default value be 'none' if the laptop does not have an optical disk drive



## Quiz 04

1. Pick a relational DBMS of your choice ([SQLite](http://sqlite.org/) is recommended)
2. Create a new database called infosys222 in the DBMS
3. Create a relation called Food with the following attributes: name, quantity, expiredDate, refrigerated. Choose appropriate data types for the attributes
4. Now, look up your food cabinet and the fridge, and pick 5 different food items
5. Create 5 tuples in the relation Food to represent the picked items
6. Use the SELECT command learnt from Week 01 to check if all items are stored properly
7. (Optional) Take a screenshot of the result of (6) and upload it to the [discussion forum](https://piazza.com/class/iphe9yxcc9m79g)



## <i class="fa fa-list-alt"></i> Summary
- By now you should:

	- know the vocabulary of the relational data model: relation, tuple, attribute, domain, schema, key, constraint etc

	- know how to represent a relation using a schema

	- have some basic ideas of how to choose a primary key for a relation

	- understand that every decision builds on at least one assumption

	- have gained more knowledge in SQL


## <i class="fa fa-book"></i> Reading
- Essential
	- [The Relational Model of Data (p17-37)
](http://infolab.stanford.edu/~ullman/fcdb/ch2.pdf)

- Further
	- [Codd (1970): A Relational Model of Data for Large Shared Data Banks](https://auckland.rl.talis.com/items/42B382E0-AAE6-04E7-D174-1F0113752E94.html?referrer=%2Flists%2F67385800-22DC-21D5-CBF3-00CC4AFE9E1E.html%23item-42B382E0-AAE6-04E7-D174-1F0113752E94)


## <i class="fa fa-calendar"></i> Schedule
Week | Lecture | Lab
--- | --- | ---
01 | Introduction <i class="fa fa-check fa-pull-right"></i>| No lab <i class="fa fa-check fa-pull-right"></i>
02 | Relational model <i class="fa fa-check fa-pull-right"></i>| Introduction <i class="fa fa-spinner fa-pulse fa-pull-right"></i>
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
