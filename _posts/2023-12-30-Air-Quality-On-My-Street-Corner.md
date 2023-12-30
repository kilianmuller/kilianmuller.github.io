---
layout: post
title: "Monitoring the air quality on my street corner"
categories: misc
published: true
---

Air quality is [massively improving in Paris](/misc/2023/04/20/PM25-pollution-Paris-2007-to-2021.html), where I live. But Paris is big, and I am only breathing right where I am. What is the situation on my street corner?

Without giving too much away, our apartment is on the fourth floor, next to a moderately busy Parisian street corner. There is a traffic light where cars and motorcycles stop and accelerate. People smoke outside the bar downstairs. One of the biggest parks in Paris is only five minutes away.

I have installed an air quality sensor outside the window that looks onto our street corner. It measures the atmospheric particulate matter concentration. Here's the data:



<script src="https://cdnjs.cloudflare.com/ajax/libs/moment.js/2.29.1/moment.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/moment-timezone/0.5.34/moment-timezone-with-data-1970-2030.min.js"></script>


<script>

// Function that determines whether the user has set a preference for bright or dark mode.
// Define colours of the plot accordingly:

function getUserColorScheme() {
    if (window.matchMedia && window.matchMedia('(prefers-color-scheme: dark)').matches) {
      // Dark mode
      return {
        plot_bgcolor: "#333",
        paper_bgcolor: "#333",
        font: {color: "#fff"}
      };
    } else {
      // Bright mode (default)
      return {
        plot_bgcolor: "#fff",
        paper_bgcolor: "#fff",
        font: {color: "#333"}
      };
    }
  }

  // Function to fetch data and create the plot
  function fetchDataAndPlot() {
    fetch('/data/PM_daily_data.json')
      .then(response => response.json())
      .then(data => {
	var convertedXData = data.xData.map(unixTime => {
    	return moment(unixTime * 1000).tz('Europe/Paris').format();
	});
        var trace = {
          x: convertedXData,
          y: data.yData,
          type: 'bar'
        };
        var layout = {
	    xaxis: {
	    	   type: 'date',
		   title: 'Date'},
	    yaxis: {
	    	   title: 'PM 2.5 [ μg/m³ ]',
		   showgrid: true,
		   gridcolor: '#bdbdbd'},
	    dragmode: 'zoom',
	    title: 'Daily average of PM 2.5 concentration',
	    ...getUserColorScheme() // Apply bright or dark colour scheme
		   };
        Plotly.newPlot('myDiv', [trace], layout);
      })
      .catch(error => console.error('Error loading data:', error));
  }

  // Call the function when the window loads
  window.onload = fetchDataAndPlot;
</script>

<!-- The div where your plot will appear -->
<div id="myDiv"></div>


[The WHO recommends](https://www.who.int/publications/i/item/9789240034228) the PM 2.5 concentration not to exceed 15 μg/m³ over a 24 hour window. The threshold for the yearly average concentration is set to 5 μg/m³. [Current EU regulations](https://environment.ec.europa.eu/topics/air/air-quality/eu-air-quality-standards_en) are less stringent, setting the annual average to 20 μg/m³. At the time of writing this post [each Parisian](https://airparif.asso.fr/surveiller-la-pollution/bilan-et-cartes-annuels-de-pollution) is exposed to roughly twice to three times the limit recommended by the WHO, but staying below the one recommended by the EU.

The sensor I am using ([Plantower PMS7003](PMS7003)) is not bad: it claims to have a counting efficiency of 98% for particles larger than 0.5 μm. Still, take my data with a grain of salt. Probably the pros have more sophisticated sensors, and also calibrate their equipment. That being said, the concentrations I measure are qualitatively in line with those provided by the NGO [Airparif](https://airparif.asso.fr), which monitors the air quality in the greater Paris region.