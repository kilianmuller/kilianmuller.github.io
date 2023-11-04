---
layout: post
title: "Monitoring the air quality on my street corner"
categories: misc
published: true
---


<div id="myPlot"></div>

<script>
    var trace1 = {
      x: [1, 2, 3, 4],
      y: [10, 15, 13, 17], 
      type: 'scatter'
    };

    var layout = {
      dragmode: 'zoom', // this enables the zoom functionality
      title: 'Particulate pollution'
    };

    var data = [trace1];

    Plotly.newPlot('myPlot', data, layout);
</script>

