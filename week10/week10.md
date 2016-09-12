# <i class="fa fa-database"></i> INFOSYS 222
### Week 10: DBMS fundamentals
<i class="fa fa-copyright"></i> [Johnny Chan](mailto:jh.chan@auckland.ac.nz) | <i class="fa fa-twitter"></i> [@infosys222](http://twitter.com/infosys222)



## <i class="fa fa-history"></i> Previously on 222 ...

- Constraint

- CASE and CAST

- UNION, UNION ALL, INTERSECT, and EXCEPT

- VIEW and TRIGGER



## <i class="fa fa-list-alt"></i> Agenda
- Database efficiency

- Transaction management

- Concurrency control



## Database efficiency
- Database efficiency is the property that the database uses the least amount of computational and storage resource without sacrificing performance

- One of the reasons for DBMS to be so successful is that, to a large extend, they are efficient automatically – as database programmer we specify what to do but never how to do, the DBMS takes care of the rest

- But there are still things we could do to help the DBMS to further improve its efficiency
	- Defining suitable indexes
	- Tuning the database schema


## Hard drive
- Tables of large database are usually stored on hard drive – they can store large amount of data but they are very slow comparing to the memory of a computer:
	- The time to access a specific piece of data is on the order of 10 million times slower
	- The rate at which data can be read/write is on the order of 10-100 times slower
	- SSD performs better than hard drive but they are still a lot slower than RAM

- For database that does not fit in the computer’s main memory, the time used for accessing disk is usually the main performance bottleneck

- RAID system


## Full table scan
```
SELECT * FROM R WHERE <condition>;
```

- When a DBMS encounters a query like this, the obvious thing to do is read through all rows of R and return rows that satisfy the condition
	- This is known as a full table scan

- If we have to return 80% of the rows in R, it makes sense to do a full table scan; but if the query is very selective and returns just a small percentage of the rows, we might hope to do better

- 😶 Is there a way of skipping over rows that will not be selected?


## Point query
```
SELECT * FROM R WHERE score = 5;
```

- This is called a point query, all rows with a score 5 are returned; point query is often very selective or the selectivity is high

- Suppose the rows of R were sorted by score, then the DBMS could
	1. Search for the first row with score = 5
	2. Return that row and all the following rows with score = 5


## Range query
```
SELECT * FROM R WHERE score > 2 AND score < 10;
```

- This is a range query, since we return all rows with score from 3 to 9

- Suppose that the rows of R were sorted by score, then the DBMS could:
	1. Search for the first row with score > 2
	2. Return that row and all the following rows with score < 10


## Index
- To be able to quickly find the first row with a specific score, the DBMS may build an index on the score column from the previous example

```
CREATE INDEX scoreInd on R (score);

DROP INDEX scoreInd;
```

- A [database index](https://en.wikipedia.org/wiki/Database_index) is similar to an index of a book:
	- For every piece of data you might be interested in, the index says where to find it
	- The index itself is organised such that one can quickly do the lookup

- Looking for data in a table with the help of an index is called an index scan


## Primary index
- If the rows of a table are stored sorted according to some column, an index of that column is called a primary index

	- Primary index makes point and range queries on the associated column very efficient
	- Some DBMS automatically builds a primary index on the primary key for each table (including SQLite)
	- A primary index is also known as a clustering index


## Secondary index
- It is possible to have more than one index in a table

- The non-primary index is called secondary index
	- They make most point queries on the column more efficient
	- They make some range queries on the column more efficient
	- They are also known as non-clustering indexes


## Index on multiple columns
- An index can be defined on one or more columns:

```
CREATE INDEX myIndex ON Book (bookTitle, bookType);
```

- Due to the way indexes are implemented, an index on multiple columns automatically gives index for any prefix column:

	- myIndex also gives an index for (bookTitle)
	- myIndex has a similar effect as storing the rows in Book sorted first according to bookTitle, then according to bookType


## Index utilisation
- Point and range queries on the column of the primary index are almost always best performed using an index scan

- Secondary index should be used with high selectivity query
	- As a rule of thumb, a secondary index scan is faster than a full table scan for query returning less than 20% of rows in a table

- Even if an index scan is possible, a good DBMS sometimes chooses to do a full table scan
	- The decision is usually based on statistics on the data in the table, which allows the selectivity of the query to be estimated


## Quiz 01
- If creating primary and secondary indexes could potentially improve the efficiency of all queries (including both point and range), why not create indexes among all possible sets of columns in every table?

- What would be the situation when dropping and re-creating indexes improves database efficiency?


## Space and storage
- In addition to taking time to update, an index has a space cost
	- Primary index usually has modest space requirement
	- Secondary index uses space similar to that required for the columns indexed
	- One should therefore be careful with creating secondary indexes on large amount of data

- Besides from point and range queries, indexes could also speed up join operations, or they are used for checking referential integrity constraints

- Indexing is a science of its own

- <i class="fa fa-book"></i> Further: [Partial index in SQLite](https://www.sqlite.org/partialindex.html)


## Normalisation and efficiency
- Normalisation is used to eliminate data redundancy in a database design by breaking down complex data structure into a set of relation. Less redundancy could help to make full table scan faster

- But that also implies potentially more join operation must be performed when answering queries. Performance may not be adequate

- Sometimes a database designer may choose to denormalise a database schema: join several tables into one, for the sake of efficiency



## Transaction and concurrency
- In most large database systems, many users and application programs will be (and must be) accessing the database at the same time

- Consecutive updates to a database that “belong together” can be grouped into transactions by the database programmer

- Having concurrent users updating the database raises a number of problems that, if not properly dealt with by the DBMS, could leave the database in an inconsistent state, even if all users "did the right thing"



## Transaction
- A logical atomic unit of work that must be either entirely completed or aborted

- It consists of one or more database requests

- It starts and ends with the database in a consistent state (where inconsistent state may violate integrity and business rule)


## Consistent state
- It is a state when all data integrity constraints are satisfied

- Transaction should always begin in a consistent state

```
x = 40        Initial State [Consistent State]
x = x - 10    Transaction [Modification]
x = 30        Final State [Consistent State]
```


## Example: ATM
- When a user of ATM transfers money from a saving account to a checking account, the transaction have to include three separate operations:
	- Decrement in the saving account
	- Increment in the checking account
	- Record the transaction in the transaction journal

- The operations could be represented by three SQL statements
	- If all SQL statements maintain the accounts in proper balance, then the effect of the transaction (i.e. the change made to the data) should persist

	- If a problem (e.g. insufficient fund, invalid account number, or a hardware failure) prevents one or two of the SQL statements from completing, then the database must roll back the entire transaction


## Example: ATM
```
BEGIN TRANSACTION;

UPDATE Saving
SET balance = balance – 100
WHERE accNo = 1250;

UPDATE Checking
SET balance = balance + 100
WHERE accNo = 1201;

INSERT INTO Journal (transType, fromAccNo, toAccNo, amount)
VALUES ('1B', 1250, 1201, 100);

COMMIT; -- or ROLLBACK;

```


## Quiz 02
- Describe the operations involved in the transaction of purchasing a lotto ticket online


## [ACID](https://en.wikipedia.org/wiki/ACID)
Property | Description
--- | ---
Atomicity | Ensure all operations of a transaction are completed; if not completed, transaction is aborted. A transaction is a single indivisible logical unit of work
Consistency | The transaction takes the database from one consistent state to another consistent state
Isolation | The effect of a transaction is not visible to other transaction until it is committed. It appears to users as if transactions are executing serially
Durability | Changes made by committed transactions are permanent; the database would ensure the changes from the transaction are not lost (even if there is a system failure)


## Transaction management
- All transactions are controlled and executed by the DBMS to enforce a high degree of data integrity
	- BEGIN TRANSACTION;
	- COMMIT;
	- ROLLBACK;

- Transaction log
	- Records all transactions that update database
	- Stores before-and-after data about database
	- DBMS uses it to roll back
	- Consumes processing overhead

- In SQLite, [temporary files](https://www.sqlite.org/tempfiles.html) are used to support transaction management


## Transaction log
transNo | table | rowID | column | before | after
--- | -- | --- | --- | --- | ---
101 | ** Start transaction | | | |
101 | Product | 34TYX | qtyInStock | 243 | 143
101 | AccReceivable | 60120010 | accBalance | 1200 | 4700
101 | ** End transaction | | | |



## Concurrency control
- The coordination of simultaneous execution of transactions in a multiprocessing database

- It ensures the serialisability of transactions (i.e. isolation in ACID) in a multi-user database environment

- Concurrency control tackles three main problems:
	- The lost update problem
	- The dirty read problem
	- The inconsistent summary problem


## Example
- Consider two transactions, T1 and T2, try to update the quantity in stock of product X

- T1 adds 100 units; T2 subtracts 30 units

```
Time   Trans.  Request                        Stored Value
----   ------  -----------------------------  ------------
1      T1      Read qtyInStock                          35
2      T1      qtyInStock = qtyInStock + 100
3      T1      Write qtyInStock                        135
4      T1      Commit
5      T2      Read qtyInStock                         135
6      T2      qtyInStock = qtyInStock - 30
7      T2      Write qtyInStock                        105
8      T2      Commit
```


## Lost Update
- What if T2 starts before T1 ends?

```
Time   Trans.   Request                        Stored Value
----   ------   -----------------------------  ------------
1      T1       Read qtyInStock                          35
2      T2       Read qtyInStock                          35
3      T1       qtyInStock = qtyInStock + 100
4      T2       qtyInStock = qtyInStock - 30
5      T1       Write qtyInStock                        135*
6      T2       Write qtyInStock                          5
```


## Dirty Read
- What if T2 reads updated but uncommitted data from T1, and then T1 is rolled back?

```
Time   Trans.   Request                        Stored Value
----   ------   -----------------------------  ------------
1      T1       Read qtyInStock                          35
2      T1       qtyInStock = qtyInStock + 100
3      T1       Write qtyInStock                        135
4      T2       Read qtyInStock                         135
5      T2       qtyInStock = qtyInStock - 30
6      T1       Rollback*
7      T2       Write qtyInStock                        105
8      T2       Commit
```


## Inconsistent Summary
- A transaction calculates some summary (aggregate) functions over a set of data while other transaction are updating the data

- One transaction might read some data before they are changed and other data after they are changed


## Concurrency control
- Concurrency control category
	- Optimistic
	- Pessimistic
	- Semi-optimistic

- Concurrency control method
	- Locking
	- Timestamp


## Locking
- Lock guarantees exclusive use of data items to a current transaction

- There are different levels of locking: column, row, page, table, database

- Although locking prevents serious data integrity error, it could hamper the serializability of data and causes [deadlock](http://en.wikipedia.org/wiki/Deadlock)


## Timestamp
- Timestamp is unique and global; a high-valued timestamp occurs later in time than a lower-valued timestamp

- All database operations within the same transaction must have the same timestamp

- DBMS executes conflicting operations in timestamp order

- They increase memory requirement



## <i class="fa fa-list-alt"></i> Summary
- By now you have learnt:

	- how database efficiency could be improved and refined

	- the importance of transaction management

	- how a database handles concurrency control


## <i class="fa fa-book"></i> Reading

- Further
	- [Indexing and Tuning of SQL for Web Nerds ](http://philip.greenspun.com/sql/tuning.html)

	- [Database transaction](http://en.wikipedia.org/wiki/Database_transaction)

	- [Concurrency control](http://en.wikipedia.org/wiki/Concurrency_control  )


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
08 | SQL <i class="fa fa-check fa-pull-right"></i> | SQL <i class="fa fa-check fa-pull-right"></i>
09 | SQL <i class="fa fa-check fa-pull-right"></i> | SQL <i class="fa fa-check fa-pull-right"></i>
10 | DBMS fundamentals <i class="fa fa-check fa-pull-right"></i> | Workshop <i class="fa fa-spinner fa-pulse fa-pull-right"></i>
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
