# <i class="fa fa-database"></i> INFOSYS 222
### Week 05: Data modelling
[Johnny Chan](mailto:jh.chan@auckland.ac.nz) | [@infosys222](http://twitter.com/infosys222)



## <i class="fa fa-history"></i> Previously on 222 ...
- Revisit some concepts

- Design principles for data modelling

- Enhanced ER model
	- superset and subset
	- specialisation and generalisation
	- completeness, disjointness and discriminator
	- the concept of anybody

- Case study: Safari booking system



## <i class="fa fa-list-alt"></i> Agenda
- Case studies



# <i class="fa fa-briefcase"></i> Case study
### Food delivery system <!-- .slide: data-background="pizza.jpg" data-background-transition="zoom" -->


## Objective
- Read the specification carefully, then:

	- draw a logical ERD to represent the given case study, with the design principles in mind

	- state any assumption made


## Spec: Background
- [Dante’s Pizzeria](https://www.zomato.com/auckland/dantes-pizzeria-ponsonby/menu) in Ponsonby Central has decided to build a food delivery system to serve customer around the area. They need a database to keep track of their product, customer and order. After an interview with the owner, you have been given a list of requirement


## Spec: Product
- Each product of the company has a unique number, a name, a description and a price

- A product is made up of a number of ingredients. Each ingredient has a unique number, a name and a unit of measurement

- Occasionally, a product could be on special and the price would be discounted for a limited period of time. The system stores the history of product special, which includes a start date, an end date and the percentage of discount


## Spec: Customer
- A customer needs to register with an email address before they could use the delivery system. The system stores the first name, last name, gender, date of birth, contact number and password

- Each customer has a billing address and a delivery address, which could be the same or different. An address has a street, a suburb, a city, a postal code and an address type. An address type specifies if it is a residential or commercial address


## Spec: Order
- An order has a unique number, a timestamp, a delivery name, a delivery mobile and a status code. A status code describes the current status of the order. Each order is associated with a billing address and a delivery address. It is handled by an employee who delivers the product and collects the payment from the customer

- When a customer places an order, they could specify the quantity of each product they would like to order from the system. The company allows customer to choose the vegetarian version of some of the products without extra charge. For instance, fresh mozzarella could be swapped with vegetarian rennet for the Margherita pizza


## Spec: Feedback
- The company believes collecting feedback from customer is important, and they require the system to store review. A review is often made by a customer, but some from other media source may not have an author

- A review can be made directly to a particular product, or it could be associated with the company in general. Each review has a unique number, a date, a description, and a star number which ranges from one to five. The company could choose to show or not to show a review from the system


## <i class="fa fa-comments-o"></i> Discussion
- In your logical ER model, specify which part must accompany with assumption in order to clearly articulate the rationale behind the design decision

- Suggest any alternative way of modelling any part of the case

- What design pattern have you discovered that could potentially be reused in other case?


## Additional spec
- [Chop Chop Noodle House](http://www.ponsonbychopchop.co.nz/) in Ponsonby Central is interested in the system you are developing for Dante’s Pizzeria, and they are happy to pay an ongoing service fee to Dante’s Pizzeria if they could use the food delivery system to serve their customer. The owner of Dante’s Pizzeria thinks that is a brilliant idea - now a customer could order a variety of food product from more than one restaurants at a time

- After studying the website of Chop Chop Noodle House, list the new requirement and rule that must be followed for the food delivery system to accommodate two restaurants. Modify the logical ERD to reflect the changes required. Document and explain all the changes that have been made



# <i class="fa fa-briefcase"></i> Case study
### Animal management system <!-- .slide: data-background="zoo.jpg" data-background-transition="zoom" -->


## Objective
- Read the specification carefully, then:

	- draw a logical ERD to represent the given case study, with the design principles in mind

	- apply common design pattern and modelling technique if appropriate

	- state any assumption made


## Spec: Background
- Waitomo Zoo, is a prospering zoo in the northern King Country region of Te Ika-a-Māui. It is home to an extensive array of animal species. Animal forms a core part of the enterprise dedicated to animal conservation and the education of people

- Currently the zoo uses a simple Excel spreadsheet for their internal record keeping, and that is no longer adequate. It has been proposed that the data would be transferred to a database system. However, before that could happen some issues need to be resolved. It is apparent that the zoo currently does not capture all the information it needs. The following outlines the requirements of the animal management system


## Spec: Animal
- Waitomo Zoo wants to capture the following data for each animal: the name, species, subspecies, gender, age, and whether or not they are nocturnal

- Each animal is fed once at a particular time in a day. Often an animal’s activity increases right before and during feeding; and when that happens visitor is more interested to view the animal. Thus it is required to store the current feeding time and maintain a record of previous feeding times


## Spec: Engagement
- Another way of engaging visitor with the animal is through a scheduled animal encounter. Some animals can be held, such as arachnid and small reptile; others are involved in shows e.g. seal and monkey. Some animals, such as elephant, are taken for walks around the zoo grounds

- Not all animals engage in animal encounter. If a specific animal is involved, the detail of encounter type should be recorded. The time in a day of an animal encounter is subject to change, and the zoo would like to keep a record of both the current time and previous times of animal counters among all animals


## Spec: Diet
- Different species have different dietary requirements; they are fed specially formulated foods which consist of many ingredients

- What each species is fed needs to be recorded accurately as the food is assembled offsite and delivered daily – the purpose of the record is to flag, for instance, a delivery arrives with a carton marked for zebras containing a meat based formulated food. The manufacturer of the formulated food is also recorded


## Spec: Habitat
- Waitomo Zoo prides itself on having species from all over the world, they arrange their exhibits so that species naturally located in the same habitat are in adjacent enclosures, or if possible share enclosures e.g. zebra and giraffe can share, whereas lion and gazelle cannot. The habitat of each species needs to be stored with minimum and maximum temperatures, average humidity, soil condition and light availability


## Spec: Enclosure
- Each enclosure is built according to certain dimensions. It is required to keep track of which enclosure each specific animal occupies over time. If for any reason a specific animal needs to be removed from an enclosure, e.g. aggressive behaviour towards cohabitants, this needs to be recorded

- It is critical to ensure an animal is not placed with any of their natural predator or prey

- An enclosure has security measures installed to prevent the occupant from escaping, and this is extremely important for lethal carnivores, animals prone to charging, and those with wings. Each security measure is classified by a security level. Animals should be placed in enclosure that match the required security level of their species (e.g. tiger = 5, penguin = 1)


## Spec: Conservation
- Finally, Waitomo Zoo is heavily involved in animal conservation, they participate in many global initiatives and themselves have created some conservation programmes. Many animals at the zoo participate in conservation programmes and the database stores the history of their participation



## <i class="fa fa-list-alt"></i> Summary
- By now you should:

	- have practiced logical ER modelling through a number of case studies and understood the process well

	- know how and when to apply common design pattern and modelling technique

	- understand and appreciate the importance of assumption

	- be confident in data modelling


## <i class="fa fa-book"></i> Reading

- Further

	- [Previous exams](http://librarysearch.auckland.ac.nz/primo_library/libweb/action/display.do?tabs=detailsTab&ct=display&fn=search&doc=uoa_digitool_exams361449&indx=1&recIds=uoa_digitool_exams361449&recIdxs=0&elementId=0&renderMode=poppedOut&displayMode=full&frbrVersion=&frbg=&&dscnt=0&scp.scps=scope%3A%28CM_EP%29%2Cscope%3A%28uoa_elamdb%29%2Cscope%3A%28Combined_record%29&tb=t&mode=Basic&vid=UOA2_A&srt=rank&tab=course_resources&dum=true&vlfreeText0=INFOSYS%20222&dstmp=1468046366879)


## <i class="fa fa-calendar"></i> Schedule
Week | Lecture | Lab
--- | --- | ---
01 | Introduction <i class="fa fa-check fa-pull-right"></i>| No lab <i class="fa fa-check fa-pull-right"></i>
02 | Relational model <i class="fa fa-check fa-pull-right"></i>| Introduction <i class="fa fa-check fa-pull-right"></i>
03 | ER modelling <i class="fa fa-check fa-pull-right"></i>| ER diagram <i class="fa fa-check fa-pull-right"></i>
04 | Data modelling <i class="fa fa-check fa-pull-right"></i> | Data modelling <i class="fa fa-check fa-pull-right"></i>
05 | Data modelling <i class="fa fa-check fa-pull-right"></i>| Workshop <i class="fa fa-spinner fa-pulse fa-pull-right"></i>
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
