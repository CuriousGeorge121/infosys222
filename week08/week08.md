# <i class="fa fa-database"></i> INFOSYS 222
### Week 08: SQL
<i class="fa fa-copyright"></i> [Johnny Chan](mailto:jh.chan@auckland.ac.nz) | <i class="fa fa-twitter"></i> [@infosys222](http://twitter.com/infosys222)



## <i class="fa fa-history"></i> Previously on 222 ...

- Basics of SQL
	- CREATE, ALTER and DROP TABLE
	- INSERT, SELECT, UPDATE and DELETE
	- operator
	- sorting

- SQLite



## <i class="fa fa-list-alt"></i> Agenda
- Function
	- Single-row function
	- Multi-row function (aggregate function)

- Join

- Subquery



## Single-row function
- Manipulate data item
- Accept argument and return one value
- Act on each row returned
- Return one result per row
- Can be nested


## String function
| Function | Description |
| :------------- | :------------- |
| LOWER(X) | It returns a copy of string X with all ASCII characters converted to lower case |
| UPPER(X) | It returns a copy of string X with all ASCII characters converted to upper case |
| SUBSTR(X,Y) or SUBSTR(X,Y,Z) | It returns a substring of string X that begins with the Y-th character and which is Z characters long |
| LENGTH(X) | It returns the number of characters in string X |
| INSTR(X,Y) | It finds the first occurrence of string Y within string X and returns the number of prior characters plus 1, or 0 if Y is nowhere found within X |
| REPLACE(X,Y,Z) | It returns a string formed by substituting string Z for every occurrence of string Y in string X |
| RTRIM(X) or RTRIM(X,Y) | It returns a string formed by removing any and all characters that appear in Y (or white spaces if Y is not provided) from the right side of X |
| LTRIM(X) or LTRIM(X,Y) | It returns a string formed by removing any and all characters that appear in Y (or white spaces if Y is not provided) from the left side of X |
| TRIM(X) or TRIM(X,Y) | It returns a string formed by removing any and all characters that appear in Y (or white spaces if Y is not provided) from both ends of X |
<!-- .element: class="smalltr" -->


## Quiz 01
- What would be returned from the following statements?

```
SELECT LOWER('University of Auckland');
SELECT UPPER('University of Auckland');
SELECT SUBSTR('University of Auckland', 4, 7);
SELECT INSTR('University of Auckland', ' ');
SELECT LENGTH('University of Auckland');
SELECT REPLACE('University of Auckland','Auckland','Otago');
SELECT RTRIM('University of Auckland', 'U');
SELECT LTRIM('University of Auckland', 'U');
SELECT TRIM('University of Auckland', 'U');
```


## Quiz 02
- String literal is case sensitive in SQL. If your task is to look up the address of a particular staff member (e.g. James McDonald) without knowing for sure how names are stored (i.e. whether they are in upper, lower or mixed cases), what would be the optimised way to compose your SELECT statement?

<br />
```
SELECT staffStreet, staffSuburb, staffCity
FROM Staff
WHERE staffFirstName = 'James'
AND staffLastName = 'McDonald';
```
<!-- .element: contenteditable="true" -->


## Numeric function
| Function | Description |
| :------------- | :------------- |
| ABS(X) | It returns the absolute value of number X |
| MAX(X,Y,...) | It returns the maximum value among the list of numeric arguments |
| MIN(X,Y,...) | It returns the minimum value among the list of numeric arguments |
| ROUND(X) or ROUND(X,Y) | It returns a floating-point value X rounded to Y digits to the right of the decimal point. If the Y argument is omitted, it is assumed to be 0 |
| RANDOM() | It returns a pseudo-random integer between -9223372036854775808 and +9223372036854775807 |


## Date function
| Function | Description |
| :------------- | :------------- |
| DATE(X,Y,...) | It returns the date in this format: YYYY-MM-DD |
| TIME(X,Y,...) | It returns the date in this format: HH:MM:SS |
| DATETIME(X,Y,...) | It returns the date and time in this format: YYYY-MM-DD HH:MM:SS |
| JULIANDAY(X,Y,...) | It returns the [Julian day](http://en.wikipedia.org/wiki/Julian_day) - the number of days since noon in Greenwich on November 24, 4714 B.C. |
| STRFTIME(F,X,Y,...) | It returns the date formatted according to the format string F specified as the first argument. The DATE(), TIME() and DATETIME() functions are equivalent to STRFTIME() with certain formats |

<br />
- <i class="fa fa-book"></i> Further: [Date function in SQLite](https://www.sqlite.org/lang_datefunc.html)


## Example
- How many weeks have all the staff been employed?

```
SELECT staffCode, ROUND((JULIANDAY('now', 'localtime') -
JULIANDAY(startDate, 'localtime'))/7) weeks
FROM StaffAssignment;

staffCode   weeks     
----------  ----------
1           480.0     
2           475.0     
3           480.0     
4           475.0     
5           474.0     
6           479.0     
7           457.0     
8           474.0       
...
```


## Quiz 03
- Modify the SELECT statement in the previous example, so that it calculates the total weeks of employment correctly for staff that have left the company as well


## More single-row function
| Function | Description |
| :------------- | :------------- |
| IFNULL(X,Y) | It returns a copy of its first non-NULL argument; it could be used to replace a NULL value from a column with an alternative value |
| TYPEOF(X) | It returns a string that indicates the datatype of the expression X: null, integer, real, text, or blob |
| UNICODE(X) | It returns the numeric unicode code point corresponding to the first character of the string X |



## Multi-row function
- Work on multiple rows to give one result per group
- Also known as group or aggregate function


## Multi-row function
| Function | Description     |
| :------------- | :------------- |
| COUNT(*) or COUNT(X) | The COUNT(X) function returns a count of the number of times that X is not NULL in a group. The COUNT(*) function (with no arguments) returns the total number of rows in the group |
| MAX(X) | It returns the maximum value of all values in the group |
| MIN(X) | It returns the minimum value of all values in the group |
| AVG(X) | It returns the average value of all values in the group |
|SUM(X) or TOTAL(X) | It returns sum of all non-NULL values in the group |
|GROUP_CONCAT(X,Y) | It returns a string which is the concatenation of all non-NULL values of X. If parameter Y is present then it is used as the separator between instances of X |


## GROUP BY clause
- Often the intention of using multi-row function is to apply them to selected group, where the group is defined by the data
	- e.g. Write a SELECT statement to list all the cities from the Staff table and the number of staff living in each city

- The GROUP BY clause allows a multi-row function to be used on each group specified

- All columns in the SELECT statement that are not associated with the multi-row function MUST be placed in the GROUP BY clause


## Example
```
SELECT staffCity city, COUNT(staffCity) '# of staff'
FROM Staff
GROUP BY staffCity;

city        # of staff
----------  ----------
Auckland    7         
Dunedin     1         
Hamilton    1         
Manukau     1         
Nelson      1         
Westland    1         
```


## Another example
```
SELECT roleID, AVG(salary)
FROM StaffAssignment
GROUP BY roleID;

roleID      AVG(salary)
----------  -----------
1           58750.0    
2           40750.0    
3           47500.0    
```


## HAVING clause
- The HAVING clause is used to filter the result from a SELECT statement with a multi-row function and a GROUP BY clause

```
SELECT branchNo, AVG(salary)
FROM StaffAssignment
GROUP BY branchNo
HAVING AVG(salary) > 54000;

branchNo    AVG(salary)
----------  -----------
1           55000.0    
```

- 😶 How is HAVING different from WHERE in SQL?


## Quiz 04
- Write a SELECT statement to show the number of books transacted per branch



## Join
- If the core rationale behind the relational data model and normalisation is to break down a complex data structure into a set of smaller relations, then there must be a mechanism to join them back together to support queries

- What is a [join]?
	- It is a mean to combine columns from more than one table
	- Most of the time a join condition is specified
	- It is required to prefix the column name with the table name or table alias when the same column name exists in more than one table
[join]: https://en.wikipedia.org/wiki/Join_(SQL)


## Example
```
SELECT bookCode, w.authorNo, a.authorNo, authorFirstName
FROM Writing w, Author a
WHERE w.authorNo = a.authorNo
AND a.authorNo IN (1,2);

bookCode    authorNo    authorNo    authorFirstName
----------  ----------  ----------  ---------------
110         1           1           De Silva       
111         1           1           De Silva       
112         2           2           Stevens        
```
- Instead of using the full table name, it is easier to use a table alias to differentiate among the same named columns from two or more tables


## Join type
- Inner join
	- It requires each row in the two joined tables to have matching rows
	- Could use either implicit join notation or explicit join notation
	- Equi-join vs non equi-join

- Outer join
	- The joined table retains each row even if no other matching row exists
	- Left outer join always contains all rows of the left table even if the join condition does not find any matching row in the right table
	- No implicit join notation is allowed
	- Right outer join and full outer join are not supported in SQLite

- Cross join / Cartesian join
	- It joins each row of one table to each row of the other table

- Self join
	- It joins a table to itself


## Inner join: equi-join
```
SELECT bookTitle, authorLastName, pubName, pubDate
FROM Author a, Writing w, Book b, Publisher p
WHERE a.authorNo = w.authorNo
AND b.bookCode = w.bookCode
AND w.pubCode = p.pubCode;

bookTitle           authorLastName  pubName        pubDate   
------------------  --------------  -------------  ----------
Far from the Crowd  Clarice         Barclay Books  2006-08-31
A Loud Game         Clarice         Bridgeman Pub  2004-07-13
The Artist          Rob             Chuck Sawyer   2000-01-02
Passage to Freedom  Louis           Chuck Sawyer   2003-03-01
Tornado             Clive           McMillan Publ  2007-06-15
Knockdown           Clive           Metcalf Publi  1972-01-23
Judo                Lisa            Hatfield and   1985-02-24
```
- 😶 Rewrite the SELECT statement with explicit join notation


## Inner join: non equi-join
```
SELECT bookCode, price, bookGrade
FROM BookPrice p, BookGrade g
WHERE price BETWEEN minValue AND maxValue;

bookCode    price       bookGrade
----------  ----------  ----------
110         32.5        Low       
111         132.5       High      
110         82.5        Medium    
112         300.0       Very High
113         47.1        Low       
114         98.1        Medium    
115         23.45       Very Low  
114         56.24       Medium    
116         84.5        Medium    
```
- 😶 Rewrite the SELECT statement by replacing bookCode with bookTitle


## Outer join: left outer join
```
SELECT authorLastName, bookCode
FROM Author a LEFT OUTER JOIN Writing w
ON a.authorNo = w.authorNo;

authorLastName  bookCode  
--------------  ----------
Clarice         110       
Clarice         111       
Rob             112       
Louis           113       
Clive           114       
Clive           115       
Theodora                  
Lisa            116       
Gabriella                 
Beatrice                  
Beatrice                  
```
- When there is no matching bookCode for an author, a NULL is given


## Cross join
```
SELECT bookCode, a.authorNo
FROM Writing w, Author a;

bookCode    authorNo  
----------  ----------
110         1         
111         1         
112         1         
113         1         
114         1         
115         1         
116         1         
110         2         
111         2         
112         2         
113         2         
114         2         
115         2         
116         2         
110         3         
111         3         
112         3         
113         3         
114         3         
115         3         
116         3         
110         4         
111         4         
112         4         
113         4         
114         4         
115         4         
116         4         
110         5         
111         5         
112         5         
113         5         
114         5         
115         5         
116         5         
110         6         
111         6         
112         6         
113         6         
114         6         
115         6         
116         6         
110         7         
111         7         
112         7         
113         7         
114         7         
115         7         
116         7         
110         8         
111         8         
112         8         
113         8         
114         8         
115         8         
116         8         
110         9         
111         9         
112         9         
113         9         
114         9         
115         9         
116         9        
```
- 📢 Avoid this in most circumstances!


## Self join
```
SELECT c.pubName publisher, p.pubName parent
FROM Publisher c, Publisher p
WHERE c.parentPubCode = p.pubCode;

publisher           parent              
------------------  --------------------
Chuck Sawyer Books  Bridgeman Publishers
Lake House Books    Bridgeman Publishers
Barclay Books       Bridgeman Publishers
Metcalf Publishers  Chuck Sawyer Books  
Hatfield and Sons   Chuck Sawyer Books  
McMillan Publishin  Chuck Sawyer Books  
```
- 😶 Rewrite the SELECT statement so that all publishers are listed on the publisher column



## Subquery
- Who has a higher salary than Jones?
	- Main query: staff with a higher salary than Jones
	- Subquery: Jone’s salary

- Similar to nested function, using subquery in SQL is a technique to combine multiple queries into one. The subquery executes before the main query, and the result of the subquery is used to solve the main query

- Enclose subquery in parentheses

- Use single-row operator with single-row subquery; and multi-row operator with multi-row subquery

- For a SELECT statement, subquery can be used within the SELECT, FROM, WHERE and/or HAVING clauses


## Subquery with WHERE
```
SELECT staffLastName, salary
FROM Staff s, StaffAssignment sa
WHERE s.staffCode = sa.staffCode
AND salary > (SELECT salary
			  FROM Staff s, StaffAssignment sa
			  WHERE s.staffCode = sa.staffCode
			  AND LOWER(staffLastName) = 'jones');

staffLastName  salary    
-------------  ----------
Gupta          72000.0   
Marks          64000.0   
Spencer        45000.0   
McDonald       54000.0   
Todd           48000.0   
Henderson      40000.0   
Tawa           40000.0   
Hewage         45000.0   
Pikes          50000.0   
Cruise         45000.0   
Schindler      50000.0   

```


## Single-row subquery
- Who gets the highest paid?

```
SELECT staffLastName
FROM Staff
WHERE staffCode =
 (SELECT staffCode
  FROM StaffAssignment
  WHERE salary =
   (SELECT MAX(salary)
	  FROM StaffAssignment));

staffLastName
-------------
Gupta        
```


## Multi-row subquery
```
SELECT staffLastName FROM Staff
WHERE staffCode IN
 (SELECT staffCode FROM StaffAssignment
	WHERE salary >
	 (SELECT MIN(salary) FROM StaffAssignment
	  WHERE roleID = 1));

staffLastName
-------------
Gupta        
Marks        
McDonald     
Todd         
Pikes        
Schindler    
```
- 😶 What is the question of this query?


## Subquery with HAVING
```
SELECT branchNo, MIN(salary)
FROM StaffAssignment
GROUP BY branchNo
HAVING MIN(salary) >
 (SELECT MIN(salary) FROM StaffAssignment);

branchNo    MIN(salary)
----------  -----------
1           45000.0    
3           40000.0    
4           40000.0    
```


## Quiz 05
- Write a single SQL statement to list all the staff members who have either the same role or same salary as Sean Henderson (staffCode = 7). The query should have 4 columns: staffCode, branchNo, roleID and salary, and it should exclude Sean Henderson from the result


## Quiz 06
- Write a single SQL statement to list all the staff members who have been assigned/hired with the three earliest start dates


## Subquery with FROM
- Subquery could also be used as a table in the FROM clause, which could participate in join just like any table

```
SELECT MIN(avgSalary)
FROM
 (SELECT branchNo, AVG(salary) avgSalary
  FROM StaffAssignment
	GROUP BY branchNo) t;

MIN(avgSalary)  
----------------
43333.3333333333

```


## Quiz 07
- Write a single SQL statement to list all the books in stock. There should be two columns: book title and the total in stock (Hint: The total in stock can be calculated by the total received minus the total sold)


## Subquery with UPDATE and DELETE
```
UPDATE StaffAssignment
SET salary = (SELECT salary FROM StaffAssignment
	          WHERE staffCode = 7)
WHERE salary = (SELECT MIN(salary) FROM StaffAssignment);
```

```
DELETE FROM BookPrice
WHERE bookCode = (SELECT bookCode FROM Book
	              WHERE bookTitle = 'Secrets');

```



## <i class="fa fa-list-alt"></i> Summary
- By now you have learnt:

	- how to use both single-row and multi-row functions

	- how to use join

	- how to use subquery


## <i class="fa fa-book"></i> Reading
- Essential
	- [Chapter 3: SQL for SQLite](https://auckland.rl.talis.com/items/71028B3F-9B42-EE38-BD07-18FC5028B84F.html?referrer=%2Flists%2F67385800-22DC-21D5-CBF3-00CC4AFE9E1E.html%23item-71028B3F-9B42-EE38-BD07-18FC5028B84F)

- Further
	- [Core function in SQLite](https://www.sqlite.org/lang_corefunc.html)

	- [Date and time function in SQLite](http://www.sqlite.org/lang_datefunc.html)

	- [Aggregate function in SQLite](http://www.sqlite.org/lang_aggfunc.html)


## <i class="fa fa-calendar"></i> Schedule
Week | Lecture | Lab
--- | --- | ---
01 | Introduction <i class="fa fa-check fa-pull-right"></i>| No lab <i class="fa fa-check fa-pull-right"></i>
02 | Relational model <i class="fa fa-check fa-pull-right"></i>| Introduction <i class="fa fa-check fa-pull-right"></i>
03 | ER modelling <i class="fa fa-check fa-pull-right"></i>| ER diagram <i class="fa fa-check fa-pull-right"></i>
04 | Data modelling <i class="fa fa-check fa-pull-right"></i> | Data modelling <i class="fa fa-check fa-pull-right"></i>
05 | Data modelling <i class="fa fa-check fa-pull-right"></i> | Workshop <i class="fa fa-check fa-pull-right"></i>
06 | Normalisation <i class="fa fa-check fa-pull-right"></i> | Normalisation <i class="fa fa-check fa-pull-right"></i>
07 | SQL <i class="fa fa-check fa-pull-right"></i> | SQL <i class="fa fa-check fa-pull-right"></i>
08 | SQL <i class="fa fa-check fa-pull-right"></i> | SQL <i class="fa fa-spinner fa-pulse fa-pull-right"></i>
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
