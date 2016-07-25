# <i class="fa fa-database"></i> INFOSYS 222
### Database Systems
<i class="fa fa-copyright"></i> [Johnny Chan](mailto:jh.chan@auckland.ac.nz) | <i class="fa fa-twitter"></i> [@infosys222](http://twitter.com/infosys222)



## Course Prescription
Managers and other knowledge workers find that many of their duties revolve around accessing, organising, and presenting organisational and external information. The ability to develop and use computer databases is becoming a critical skill that is required in many disciplines. These skills are developed through an introduction to data modelling, relational theory, database design, and the management of databases



## Programme and Course Advice
- Prerequisite: INFOSYS 110 or 120, or COMPSCI 105 or 107

- Restriction: INFOMGMT 292



## Goals of the Course
This course aims to develop the fundamental skills of designing and developing a relational database. All assessments require student to demonstrate their mastery of the practical aspects of the course including data modelling and structured query language (SQL)



## Learning Outcomes
By the end of this course it is expected that the student will be able to:
1.	understand the fundamental concepts of relational database;
2.	design a relational database;
3.	implement a relational database;
4.	define and manage data from a relational database;
5.	understand transaction management in a relational database; and
6.	understand the fundamental concepts of a data warehouse



## Content Outline

Week | Content
--- | ---
01 | Introduction
02 | Relational model
03 | ER modelling
04 | Data modelling
05 | Data modelling
06 | Normalisation
07 | SQL
08 | SQL
09 | SQL
10 | DBMS fundamentals
11 | Data warehouse
12 | Review



## Learning and Teaching
Student must attend three 1-hour lectures and one 1.5-hour lab per week. In addition, student should be prepared to spend about another six hours per week on activities related to this course. These activities include reading, practicing, and preparing for assessments



## Teaching Staff
- _Lecturer_  
	Johnny Chan | jh.chan@auckland.ac.nz

- _Coordinator_  
	Udayangi Muthupoltotage | u.muthupoltotage@auckland.ac.nz



## Learning Resources
- Greenspun. (1998) SQL for Web Nerds. [philip.greenspun.com/sql](http://philip.greenspun.com/sql)
- Allen and Owens. (2010) _The Definitive Guide to SQLite._ New York: Apress. Available from the [library](https://auckland.rl.talis.com/items/71028B3F-9B42-EE38-BD07-18FC5028B84F.html?referrer=%2Flists%2F67385800-22DC-21D5-CBF3-00CC4AFE9E1E.html%23item-71028B3F-9B42-EE38-BD07-18FC5028B84F)

	Additional material will be posted in Canvas



## Assessment
The detail of each assessment will be provided as the course proceeds

Assessment | Weighting | Learning Outcome
--- | --- | ---
Assignment 01 | 15% | 1-2
Assignment 02 | 15% | 3-4
Test | 20% | 1-4
Exam | 50% | 1-6

This course requires student to pass both the internal and the exam



## Inclusive Learning
Student should discuss privately any impairment-related requirements face-to-face and/or in writing with the coordinator



## Student Feedback
Student will be asked to complete course and teaching evaluations at certain point of the course



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
	    .defer(d3.json, 'asset/world-110m.json')
	    .defer(d3.tsv, 'asset/world-country-names.tsv')
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

#### Database rules in <span class="country">Country</span>!

[<i class="fa fa-print"></i>](?print-pdf#)
