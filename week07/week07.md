# <i class="fa fa-database"></i> INFOSYS 222
### Week 07: SQL
<i class="fa fa-copyright"></i> [Johnny Chan](mailto:jh.chan@auckland.ac.nz) | <i class="fa fa-twitter"></i> [@infosys222](http://twitter.com/infosys222)



## <i class="fa fa-history"></i> Previously on 222 ...

- Normalisation
	- Eliminate and control data redundancy
	- 1NF, 2NF and 3NF
	- Practice with business documents

- Physical data modelling



## <i class="fa fa-list-alt"></i> Agenda
- Revisit and continue on the basics of SQL
	- CREATE, ALTER and DROP TABLE
	- INSERT, SELECT, UPDATE and DELETE ([CRUD](https://en.wikipedia.org/wiki/Create,_read,_update_and_delete))
	- Operator
	- Sorting

- Get familiar with SQLite



## SQL
- What is [structured query language (SQL)](http://en.wikipedia.org/wiki/SQL)?
	- Industrial standard ([ANSI](https://en.wikipedia.org/wiki/American_National_Standards_Institute) and [ISO](https://en.wikipedia.org/wiki/International_Organization_for_Standardization))
	- 4GL
	- 😶 How does SQL relate to [Codd's relational model](https://en.wikipedia.org/wiki/Relational_model)?

- SQL statement
	- [DDL](https://en.wikipedia.org/wiki/Data_definition_language) vs [DML](https://en.wikipedia.org/wiki/Data_manipulation_language)
	- Case insensitive
	- White space and carriage return are ignored
	- Single quote is used for string and date [literal]
	- The semi-colon
[literal]: #/10


## SQLite
- SQLite is an open source cross-platform embedded relational database management system
	- [SQLite command](http://sqlite.org/cli.html) vs [SQL statement in SQLite](http://sqlite.org/lang.html)

- All SQL related content and assessment in this course are expected to be run with SQLite

- 😶 What is the major difference between SQLite and other RDBMS product?


# <i class="fa fa-play-circle-o"></i> Demo
### The book dataset



## CREATE TABLE
[![create_table](http://sqlite.org/images/syntax/create-table-stmt.gif)
<!-- .element: height="250px" -->](https://www.sqlite.org/lang_createtable.html)

```
CREATE TABLE Author
(authorNo INTEGER PRIMARY KEY NOT NULL,
 authorFirstName TEXT,
 authorLastName TEXT,
 authorStreet TEXT,
 authorSuburb TEXT
);
```
<!-- .element: contenteditable="true" -->

- <i class="fa fa-book"></i> Further: [ROWID](https://www.sqlite.org/lang_createtable.html#rowid)  and [AUTOINCREMENT](https://www.sqlite.org/autoinc.html) in SQLite


## Naming convention
- Must begin with a letter
- Can be 1–30 characters long
- Must contain only A–Z, a–z, 0–9, _, $, and #
- Must not duplicate the name of another database object of the same user
- Must not be a [reserved word](https://www.sqlite.org/lang_keywords.html)


## CREATE TABLE AS SELECT
- The following statement creates and populates a table based on the result of a SELECT statement: the table has no defined PRIMARY KEY, no defined constraint, and the default value of each column is NULL

- Use this command only for temporary or testing purpose

	```
CREATE TABLE AuthorTemp AS
SELECT * FROM Author
WHERE authorSuburb = 'Meadowbank';
	```


## ALTER TABLE
[![alter_table](http://sqlite.org/images/syntax/alter-table-stmt.gif)
<!-- .element: height="250px" -->](https://www.sqlite.org/lang_altertable.html)

- SQLite only supports two forms of alteration to an existing table in the database: to rename the table or to add a new column to the table

	```
ALTER TABLE Author ADD authorCity TEXT;
ALTER TABLE AuthorTemp RENAME TO MeadowbankAuthor;
	```

- 😶 Why is it not a good idea to support removable of a column too?


## DROP TABLE
[![drop_table](http://sqlite.org/images/syntax/drop-table-stmt.gif)
<!-- .element: height="80px" -->](https://www.sqlite.org/lang_droptable.html)

- All the data, structure, constraint and index associated with the table are deleted completely and permanently

	```
DROP TABLE MeadowbankAuthor;
	```

- 😶 What would happen if foreign key constraint is involved in a table drop?



## INSERT
[![insert](http://sqlite.org/images/syntax/insert-stmt.gif)
<!-- .element: height="650px" -->](https://www.sqlite.org/lang_insert.html)


## INSERT INTO VALUES
```
INSERT INTO Author (authorFirstName, authorLastName,
authorStreet, authorSuburb, authorCity) VALUES
('De Silva','Clarice', '21 Park View Street',
'Park View', 'Auckland');

INSERT INTO Author (authorFirstName, authorLastName, authorStreet, authorSuburb, authorCity) VALUES ('Stevens','Rob', '123 Hungry Lane', 'Meadowbank','Auckland');
INSERT INTO Author (authorFirstName, authorLastName, authorStreet, authorSuburb, authorCity) VALUES ('Peiris','Louis', '463 Galle Road','Moratuwa', 'Napier');
INSERT INTO Author (authorFirstName, authorLastName, authorStreet, authorSuburb, authorCity) VALUES ('Parker','Clive','21 Anderson Glen Road','Glen Innes','Auckland');
INSERT INTO Author (authorFirstName, authorLastName, authorStreet, authorSuburb, authorCity) VALUES ('Mendis','Theodora','75D Glenvar Road','Torbay', 'Auckland');
INSERT INTO Author (authorFirstName, authorLastName, authorStreet, authorSuburb, authorCity) VALUES ('Bingly','Lisa', '14E Glenfield Road','Glenfield','Auckland');
INSERT INTO Author (authorFirstName, authorLastName, authorStreet, authorSuburb, authorCity) VALUES ('St.Louis','Gabriella','1163 Remuera Road','Remuera','Auckland');
INSERT INTO Author (authorFirstName, authorLastName, authorStreet, authorSuburb, authorCity) VALUES ('Coorey','Beatrice','456 Dominion Road','Mt Eden','Auckland');
INSERT INTO Author (authorFirstName, authorLastName, authorStreet, authorSuburb, authorCity) VALUES ('Koorey','Beatrice','12 Peach Parade','Remuera','Auckland');
```

- 😶 What is the difference between including and not including named columns in the INSERT statement?

- 😶 What does such difference imply?


## INSERT INTO SELECT
```
INSERT INTO AuthorTemp
SELECT authorFirstName, authorLastName, authorStreet,
authorSuburb, authorCity
FROM Author;
```



## SELECT
[![select](http://sqlite.org/images/syntax/select-stmt.gif)
<!-- .element: height="650px" -->](https://www.sqlite.org/lang_select.html)


## Quiz 01
- Compose a simplest and valid SELECT statement in SQLite

```
SELECT ...
```
<!-- .element: contenteditable="true" -->


## SELECT all columns
```
SELECT *
FROM Book;

bookCode    bookTitle           bookType    paperback
----------  ------------------  ----------  ----------
110         Far from the Crowd  PSY         Y         
111         A Loud Game         FIC         Y         
112         The Artist          FIC         Y         
113         Passage to Freedom  HOR         N         
114         Tornado             MYS         Y         
115         Knockdown           MYS         Y         
116         Judo                HOR         Y         
117         Sneaky Stories                  Y         
999         Pilgrim's Progress              N         
```
- The columns selected are collectively known as a projection


## SELECT specific columns
```
SELECT bookCode 'Book Code', bookTitle Title
FROM Book;

Book Code   Title         
----------  ------------------
110         Far from the Crowd
111         A Loud Game       
112         The Artist        
113         Passage to Freedom
114         Tornado           
115         Knockdown         
116         Judo              
117         Sneaky Stories    
999         Pilgrim's Progress
```
- Column alias renames a column heading; useful for derived column


## SELECT DISTINCT
```
SELECT DISTINCT staffCity City
FROM Staff;

City
----------
Hamilton
Auckland
Nelson   
Dunedin  
Westland
Manukau
```
- Duplicate rows are detected and removed from the set of result rows
- In SQLIte, two NULL values are considered to be equal (but also unique)


## LIMIT and OFFSET clauses
```
SELECT * FROM Book LIMIT 3;

bookCode    bookTitle           bookType    paperback
----------  ------------------  ----------  ----------
110         Far from the Crowd  PSY         Y         
111         A Loud Game         FIC         Y         
112         The Artist          FIC         Y         

SELECT * FROM Book LIMIT 3 OFFSET 2;

bookCode    bookTitle   bookType    paperback
----------  ----------  ----------  ----------
112         The Artist  FIC         Y         
113         Passage to  HOR         N         
114         Tornado     MYS         Y         
```



## WHERE clause
```
SELECT roleID, branchNo, staffCode
FROM StaffAssignment
WHERE roleID = 1;

roleID      branchNo    staffCode
----------  ----------  ----------
1           1           1         
1           2           2         
1           3           3         
1           4           4         
```

- When a WHERE clause is specified, each row from the input data is evaluated as a boolean expression
	- Rows evaluated as true are included
	- Rows evaluated as false (or NULL) are excluded
- Commonly used in SELECT, UPDATE and DELETE statements



## UPDATE
[![update](https://www.sqlite.org/images/syntax/update-stmt.gif)
<!-- .element: height="300px" -->](https://www.sqlite.org/lang_update.html)

```
UPDATE Author
SET authorStreet = '22 Park View Street'
WHERE authorFirstName = 'De Silva';
```

- 📢 Always use a WHERE clause in an UPDATE statement!



## DELETE
[![delete](https://www.sqlite.org/images/syntax/delete-stmt.gif)
<!-- .element: height="200px" -->](https://www.sqlite.org/lang_delete.html)

```
DELETE
FROM AuthorTemp
WHERE authorFirstName = 'De Silva';
```

- 📢 Always use a WHERE clause in a DELETE statement!



## Literal
Type | Example
--- | ---
Integer | 1000
Real | 1000.0
String | '1000', 'Johnny is the king'
Date | '2016-09-12'
NULL | NULL
<br />
- A literal represents a constant value, which could be an integer, real number, string, date, [BLOB] or [NULL]
	- String literal is case sensitive
	- Date literal is format sensitive (YYYY-MM-DD)
	- BLOB literal is outside the scope of this course
- There are specific functions designed to work with literal
[BLOB]: https://en.wikipedia.org/wiki/Binary_large_object
[NULL]: https://en.wikipedia.org/wiki/Null_(SQL)



## Operator
- SQLite supports the following operator, in order of precedence:

```
1. ||
2. * / %
3. + -
4. < <= > >= BETWEEN
5. = == != <> IS IN LIKE
6. NOT
7. AND
8. OR
```



## Concatenation
```
SELECT authorFirstName || ' ' || authorLastName Name
FROM Author;

Name            
----------------
De Silva Clarice
Stevens Rob     
Peiris Louis    
Parker Clive    
Mendis Theodora
Bingly Lisa     
St.Louis Gabriel
Coorey Beatrice
Koorey Beatrice
```
- 😶 How many string literals are being concatenated per row?


## Quiz 02
- Rewrite the previous SELECT statement so that the last name goes before the first name, separated with a comma in between



## Arithmetic
```
SELECT staffCode, salary, salary/12 monthly
FROM StaffAssignment;

staffCode   salary      monthly   
----------  ----------  ----------
1           72000.0     6000.0    
2           64000.0     5333.33333
3           45000.0     3750.0    
4           54000.0     4500.0    
5           48000.0     4000.0    
6           35000.0     2916.66666
7           40000.0     3333.33333
8           40000.0     3333.33333
9           45000.0     3750.0    
...

```


## Quiz 03
- Rewrite the previous SELECT statement with an additional column named tax which shows the annual income tax of staff



## Logical
Operator | Description
--- | ---
AND | Returns TRUE if both conditions are TRUE
OR | Returns TRUE if either condition is TRUE
NOT | Returns TRUE if the condition is FALSE

```
SELECT staffCode, salary FROM StaffAssignment
WHERE salary IS NOT 72000
AND salary > 50000
OR salary = 45000;

staffCode   salary    
----------  ----------
2           64000.0   
3           45000.0   
4           54000.0   
9           45000.0   
11          45000.0   
```


## Quiz 04
- Explain how the logical operators work in the previous SELECT statement; and what may happen if the order of AND and OR is swapped



## Comparison
```
SELECT staffCode, salary
FROM StaffAssignment
WHERE salary BETWEEN 54000 AND 72000;

SELECT staffCode, salary
FROM StaffAssignment
WHERE salary >= 54000
AND salary <= 72000;

staffCode   salary    
----------  ----------
1           72000.0   
2           64000.0   
4           54000.0    
```


## IN
```
SELECT staffCode, salary
FROM StaffAssignment
WHERE salary IN (54000, 72000);

SELECT staffCode, salary
FROM StaffAssignment
WHERE salary NOT IN (35000, 40000, 45000,
48000, 50000, 64000);

staffCode   salary    
----------  ----------
1           72000.0   
4           54000.0   

```


## IS
```
SELECT *
FROM Book
WHERE bookType IS NULL;

bookCode    bookTitle       bookType    paperback
----------  --------------  ----------  ----------
117         Sneaky Stories              Y         
999         Pilgrim's Prog              N         

```

<br />
- In SQLite, IS operator is equivalent to = and ==
- Similarly, IS NOT is equivalent to <> and =!


## LIKE
```
SELECT authorFirstName
FROM Author
WHERE authorFirstName LIKE 'P%';

authorFirstName
---------------
Peiris         
Parker     
```
- The LIKE operator performs pattern matching comparison with wildcard symbols:
	- % denotes zero or many characters
	- _ denotes one character


## Quiz 05
- Rewrite the previous SELECT statement to show all authors with a first name that does not start with letter P

- Modify the SELECT statement to show all authors with a first name that is exactly 6 characters long



## Sorting
```
SELECT authorLastName, authorFirstName FROM Author
ORDER BY authorLastName DESC, authorFirstName;

authorLastName  authorFirstName
--------------  ---------------
Theodora        Mendis         
Rob             Stevens        
Louis           Peiris         
Lisa            Bingly         
Gabriella       St.Louis       
Clive           Parker         
Clarice         De Silva       
Beatrice        Coorey         
Beatrice        Koorey         
```

- In SQL, the ORDER BY clause is used to sort rows selected
	- ASC stands for ascending order, the default mode
	- DESC stands for descending order
- The ORDER BY clause comes last in a SELECT statement


## ORDER BY clause
```
SELECT staffCode, salary/12 monthly
FROM StaffAssignment
ORDER BY monthly DESC, roleID DESC;

staffCode   monthly   
----------  ----------
1           6000.0    
2           5333.33333
4           4500.0    
10          4166.66666
12          4166.66666
5           4000.0    
9           3750.0    
11          3750.0     
...
```
- It is allowed to sort by a non-projected column
- It is allowed to sort by a derived column




## <i class="fa fa-list-alt"></i> Summary
- By now you should:

	- be familiar with the basics of SQL including
		- CREATE, ALTER and DROP TABLE

		- INSERT, SELECT, UPDATE and DELETE

		- operator

		- sorting


## <i class="fa fa-book"></i> Reading
- Essential
	- [Queries from SQL for Web Nerds](http://philip.greenspun.com/sql/queries.html)

- Further
	- [SQL supported in SQLite](http://www.sqlite.org/lang.html)

	- [Expression and operator in SQLite](https://sqlite.org/lang_expr.html)

	- [Datatype in SQLite](https://www.sqlite.org/datatype3.html)


## <i class="fa fa-calendar"></i> Schedule
Week | Lecture | Lab
--- | --- | ---
01 | Introduction <i class="fa fa-check fa-pull-right"></i>| No lab <i class="fa fa-check fa-pull-right"></i>
02 | Relational model <i class="fa fa-check fa-pull-right"></i>| Introduction <i class="fa fa-check fa-pull-right"></i>
03 | ER modelling <i class="fa fa-check fa-pull-right"></i>| ER diagram <i class="fa fa-check fa-pull-right"></i>
04 | Data modelling <i class="fa fa-check fa-pull-right"></i> | Data modelling <i class="fa fa-check fa-pull-right"></i>
05 | Data modelling <i class="fa fa-check fa-pull-right"></i> | Workshop <i class="fa fa-check fa-pull-right"></i>
06 | Normalisation <i class="fa fa-check fa-pull-right"></i> | Normalisation <i class="fa fa-check fa-pull-right"></i>
07 | SQL <i class="fa fa-check fa-pull-right"></i> | SQL <i class="fa fa-spinner fa-pulse fa-pull-right"></i>
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
