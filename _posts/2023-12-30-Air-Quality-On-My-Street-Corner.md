---
layout: post
title: "Monitoring the air quality on my street corner"
categories: misc
published: true
---

# Monitoring the air quality on my street corner

Air quality is massively improving in Paris, where I live. But Paris is big, and I am only breathing right where I am. What is the situation right where I live, on my street corner?

Without giving too much away, our building is next to a moderately busy Parisian street corner, and our apartment is on the fourth floor.. There is a traffic light where cars and motorcycles stop and accelerate. People smoke outside the bar downstairs. But there is also one of the biggest parks in Paris nearby.



<script src="https://cdnjs.cloudflare.com/ajax/libs/moment.js/2.29.1/moment.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/moment-timezone/0.5.34/moment-timezone-with-data-1970-2030.min.js"></script>


<script>
  // Function to fetch data and create the plot
  function fetchDataAndPlot() {
    fetch('/data/PM_daily_data.json')
      .then(response => response.json())
      .then(data => {
//        var convertedXData = data.xData.map(unixTime => new Date(unixTime * 1000));
	var convertedXData = data.xData.map(unixTime => {
    	return moment(unixTime * 1000).tz('Europe/Paris').format();
	});
        var trace = {
          x: convertedXData,
          y: data.yData,
          type: 'scatter'
        };
        var layout = {
	    xaxis: {
	    	   type: 'date',
		   title: 'Time (Paris)'},
	    yaxis: {
	    	   title: 'PM 2.5 [ μg/m³ ]'},
	    dragmode: 'zoom',
	    title: 'Interactive plot of particulate matter concentration'
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
