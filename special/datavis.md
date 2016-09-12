# <i class="fa fa-database"></i> INFOSYS 222
### Special: Data Visualisation
<i class="fa fa-copyright"></i> [Johnny Chan](mailto:jh.chan@auckland.ac.nz) | <i class="fa fa-twitter"></i> [@infosys222](http://twitter.com/infosys222)



## ```<1>```


<!-- .slide: data-background="https://upload.wikimedia.org/wikipedia/commons/c/cd/The_Human_Connectome.png" data-background-transition="zoom"-->

<br />
<small>[Connectome](https://en.wikipedia.org/wiki/Connectome)</small>


## Our brain is amazing

- We are very good at recognising shapes and patterns 😃
<!-- .element: class="fragment" -->

- It receives __8.96 megabits__ of data from the eye every second 😱
<!-- .element: class="fragment" -->


## When we read

- The average person comprehends 120 words per minute 😑
<!-- .element: class="fragment" -->

- That is equivalent to __81.6 bits__ of data per second 😴
<!-- .element: class="fragment" -->


<!-- .slide: data-background="https://icyseas.files.wordpress.com/2016/02/greely1888_2tides-table.png" data-background-transition="zoom"-->


<!-- .slide: data-background="http://cdn2.hubspot.net/hub/295090/file-313525636-png/Infographic_of_infographic_2.png" data-background-transition="zoom"-->


## We are not wired to read fast but wired to visualise really fast!
- A [picture](https://pic.twitter.com/ay8V8CPvXt) is better than a thousand words 📸


## ```</1>```



## ```<2>```


## Storytelling


## A tale of two stories
- Discovery vs Forecast
- Static vs Dynamic / Interactive


![Aging Population](http://www.pewresearch.org/files/2014/04/847889448.gif) <!-- .element: height="600px" -->

<small>Source: [Pew Research Center](http://www.pewresearch.org/next-america/#Two-Dramas-in-Slow-Motion)</small>


<iframe data-src="https://podio.com/site/creative-routines" width="1200" height="700" scrolling="true"></iframe>

<small>Source: [Podio](https://podio.com/site/creative-routines)</small>


<iframe data-src="http://www.bloomberg.com/graphics/2015-whats-warming-the-world/" width="1200" height="700" scrolling="true"></iframe>

<small>Source: [Bloomberg](http://www.bloomberg.com/graphics/2015-whats-warming-the-world/)</small>


<iframe data-src="http://setosa.io/bus/" width="1200" height="700" scrolling="true"></iframe>

<small>Source: [Setosa](http://setosa.io/bus/)</small>


<iframe data-src="http://googletrends.github.io/iframe-scaffolder/#/view?urls=Thanksgiving%202015%7Chttps:%252F%252Fgoogledataorg.cartodb.com%252Fu%252Fgoogledata%252Fviz%252Fbf595f4c-7381-11e5-9ec5-42010a14800c%252Fembed_map&active=0&sharing=1&autoplay=0&loop=1&layout=narrative&theme=red&title=A%20day%20in%20the%20life:%20US%20Thanksgiving%20on%20Google%20Flights&description=The%20day%20before%20Thanksgiving%202015%20shown%20in%20US%20domestic%20and%20international%20air%20travel%20booked%20with%20Google%20Flights" width="1200" height="700" scrolling="true"></iframe>

<small>Source: [Google Trends](http://googletrends.github.io/iframe-scaffolder/#/view?urls=Thanksgiving%202015%7Chttps:%252F%252Fgoogledataorg.cartodb.com%252Fu%252Fgoogledata%252Fviz%252Fbf595f4c-7381-11e5-9ec5-42010a14800c%252Fembed_map&active=0&sharing=1&autoplay=0&loop=1&layout=narrative&theme=red&title=A%20day%20in%20the%20life:%20US%20Thanksgiving%20on%20Google%20Flights&description=The%20day%20before%20Thanksgiving%202015%20shown%20in%20US%20domestic%20and%20international%20air%20travel%20booked%20with%20Google%20Flights)</small>


<iframe data-src="http://projects.fivethirtyeight.com/2016-election-forecast/" width="1200" height="700" scrolling="true"></iframe>

<small>Source: [FiveThirtyEight](http://projects.fivethirtyeight.com/2016-election-forecast/)</small>


<iframe data-src="http://gdeltproject.org/globaldashboard/" width="1200" height="700" scrolling="true"></iframe>

<small>Source: [GDELT](http://gdeltproject.org/globaldashboard/)</small>


## ```</2>```



## ```<3>```


<iframe data-src="https://d3js.org/" width="1200" height="700" scrolling="true"></iframe>

<small>Source: [D3](https://d3js.org/)</small>


## Example
<iframe src="https://dl.dropboxusercontent.com/u/7603925/strategies/itsp-progress/dashboard-itsp-pa-class.html" width="1200" height="680"></iframe>


## ```</3>```



<iframe data-src="http://www.thought-wired.com/" width="1200" height="700" scrolling="true"></iframe>

<small>Source: [Thought-Wired](http://www.thought-wired.com/)</small>



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

#### Data visualisation rules in <span class="country">everywhere</span>!
[<i class="fa fa-print"></i>](?print-pdf#)
