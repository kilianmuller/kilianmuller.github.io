---
layout: post
title: "Monitoring the air quality on my street corner"
categories: misc
published: true
---


## My interactive plot

<script src="https://cdnjs.cloudflare.com/ajax/libs/moment.js/2.29.1/moment.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/moment-timezone/0.5.34/moment-timezone-with-data-1970-2030.min.js"></script>


<script>
  // Function to fetch data and create the plot
  function fetchDataAndPlot() {
    fetch('/data/PM_data.json')  // Update with the correct path to your JSON file
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
	    dragmode: 'zoom',
	    title: 'Interactive Plot Example'
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
