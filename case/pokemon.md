# <i class="fa fa-database"></i> INFOSYS 222
### Case: Pokémon Go
<i class="fa fa-copyright"></i> [Johnny Chan](mailto:jh.chan@auckland.ac.nz) | <i class="fa fa-twitter"></i> [@infosys222](http://twitter.com/infosys222) | <i class="fa fa-calendar"></i> 2016-08-01



## Background
- [Pokémon Go](http://www.pokemongo.com/) is the first location-based augmented reality mobile game developed by Nintendo in partnership with Google under the company Niantic. Soon after its launch in July 2016 the game becomes a worldwide phenomena with an unprecedented popularity. Within 2 weeks Nintendo has gained around US$20b in market capitalisation

- The game is successful for many reasons; one key factor is its capability to manage massive amount of location-based and game data among millions of active users at any given moment. Designing such a data model to represent the complex game world is a huge challenge



## Specification
The following specification captures only part of the game. The case is aimed for learning and practicing data modelling; it has no affiliation with Pokémon Go or Niantic



## Trainer
- The purpose of the game is to explore the game world with a map, which mimics the real world, through encounters and battles with Pokémon to advance the experience point (XP) and level of the player

- When the game starts for the first time, player is greeted with an login screen that requires a Google account. Pokémon Go leaves authentication to Google and only stores the email of player

- Player is known as trainer. A trainer must choose an unique ID. The game stores the gender, start date, XP and level of each trainer. There are 40 levels in total and each requires a certain accumulation of XP except level 1

- A trainer does not belong to any team at the beginning; but when they reach level 5 they will join one of the three teams in the game: Valor, Mystic or Instinct. No change of team is allowed afterwards



## Item
- Trainer has one bag to carry items which could be used or discarded in the game. The bag begins with an allowance of 350 items

- Item has an unique number, name, description and unlock level. Some, such as Pokéball and Razz berry, can only be used during Pokémon encounters; while others, such as Potion and Lure module, can only be used when trainer is exploring

- Most items are consumed after a single use. The Egg Incubator is consumed after 3 uses. The Camera and the Egg Incubator ∞, which are given to a trainer when the game starts, have unlimited use



## Egg
- An egg is an item that is not carried in the bag. Trainer could collect up to 9 eggs. Each egg represents an unborn Pokémon and it has a travel distance to specify how far a trainer has to travel before it hatches

- To hatch an egg, trainer needs to place it in an empty Egg Incubator (or Egg Incubator ∞), and then travel the required distance (2km, 5km or 10km)

- When an egg hatches, it is consumed and in return a Pokémon is born and captured. The Egg Incubator will become empty or consumed



## Pokémon
- Pokémon has an unique ID, name, health point (HP), max HP, weight, height, and combat power (CP). At any point in the game, the stage of a Pokémon indicates if it is unborn, in the wild, captured or released

- Each Pokémon belongs to one species. There are 151 species in the game. Each species has an unique Pokédex, name, average weight, average height, attack, defense, stamina, and the number of candy needed to evolve

- Species could be classified by one or two types. For instance, Pikachu (#25) is an Electric type, whereas Pidgey (#16) belongs to both Normal and Flying types. There are 18 types in total



## Evolution
- Some species of Pokémon could evolve into another species

  - Pidgey (#16) could evolve into Pidgeotto (#17) with 12 candies; and Pidgeotto could evolve into Pidgeot (#18) with 50 candies

  - Eevee (#133) could evolve into either Vaporeon (#134), Jolteon (#135) or Flareon (#136) with 25 candies

- Not all species participates in evolution

- When a Pokémon evolves from one species to another, its HP, max HP and CP would normally increase, while other properties like name, weight and height could be changed

- Trainer gains XP when evolving Pokémon



## Location
- The game collects the geolocation of trainer every second through the [GPS](https://en.wikipedia.org/wiki/Global_Positioning_System) receiver of the mobile in the form of latitude and longitude

- Pokémon in the wild is constantly assigned by the game to various location in random; and it would appear in a trainer's map when they are nearby to each other. The trainer could choose to encounter a Pokémon or ignore it

- There are two types of fixed location in the game where trainer could visit when nearby: PokéStop and Gym. Each has a name that corresponds to a landmark in the real world (e.g. a park), and all visits are stored



## Encounter
- There are three possible outcomes to an encounter: Pokémon is captured by trainer; Pokémon escapes; or trainer runs. Only the first outcome would create an association between a Pokémon and a trainer

- Trainer uses at least one item (i.e. Pokéball) to capture a Pokémon through throw and catch. It is not uncommon to have used multiple items among multiple throws and catches before a Pokémon is captured (or escaped)

- When a Pokémon is captured, XP and candies are rewarded where candies could be used for evolving or powering up the Pokémon. There is no limit to how many candies a trainer could have

- Trainer could choose to release any of the captured Pokémon; the maximum number of Pokémon is 250 for each trainer



## PokéStop and Gym
- Trainer receives 3-6 random items from a PokéStop in one visit, and some XP as well. A visited PokéStop would become unavailable for 5 minutes to that trainer; after that the PokéStop could be revisited to receive items

- Trainer cannot visit any PokéStop if the bag is full

- A Gym is either empty or occupied by one of the three teams. Trainer could join an empty Gym by assigning one Pokémon to it, and then the Gym becomes occupied by the team of that trainer

- Each occupied Gym has a prestige point. The higher the prestige, the more trainers of the same team could join (each assigns one Pokémon). The highest number of trainers in one occupied Gym is 10. If the prestige of an occupied Gym decreases to 0, it will be reset to empty



## Battle
- When visiting a friendly Gym, trainer could choose one Pokémon to battle with all the Pokémon in that Gym. Each win rewards XP to the trainer and increases prestige of the Gym

- When visiting a rival Gym, trainer could choose a team of up to 6 Pokémon to battle with all the Pokémon in that Gym. Each win rewards XP to the trainer and decreases prestige of the Gym

- During a battle, Pokémon could lose HP from the attack of the opponent. When a Pokémon loses all HP, the status of the Pokémon becomes fainted and it is withdrawn from the battle

- A fainted Pokémon could not join any battle nor Gym until it is revived by using the item Revive; the item Potion could be used to increase the HP of injured Pokémon



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
