---
layout: post
title: "Monitoring the air quality on my street corner"
categories: misc
published: true
---


## My Interactive Plot

<!-- Start Data -->
<script>
var xData = [1, 2, 3, 4];
var yData = [10, 15, 13, 17];
</script>
<!-- End Y Data -->

<div id="myPlot"></div>

<script>
    var trace1 = {
      x: xData,
      y: yData,
      type: 'scatter'
    };

    var layout = {
      dragmode: 'zoom', // this enables the zoom functionality
      title: 'Interactive Plot Example'
    };

    var data = [trace1];

    Plotly.newPlot('myPlot', data, layout);
</script>

