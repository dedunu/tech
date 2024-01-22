---
layout: post
title: Sri Lanka Cartogram with d3.js
---

We have been using d3js to visualize things on maps. And after struggling with topojson application my boss found a way to convert Sri Lanka Shapefile (.shp) to topojson format. Then we wanted to use cartograms for our visualizations.  
  
I found that there was a d3js cartogram implementation. - [https://github.com/shawnbot/d3-cartogram/](https://github.com/shawnbot/d3-cartogram/)  

With the help of this blog post - [http://www.limn.co.za/2013/10/making-a-cartogram/](http://www.limn.co.za/2013/10/making-a-cartogram/), I finished cartogram Visualization. 

And Nisansa's co-ordinations for the center of Sri Lanka was very helpful to calibrate Sri Lanka map.  

You can find my sri-lanka-cartogram repository on GitHub - [https://github.com/dedunu/sri-lanka-cartogram](https://github.com/dedunu/sri-lanka-cartogram). 

You find the live demo from here - [https://www.dedunu.info/sri-lanka-cartogram/](https://www.dedunu.info/sri-lanka-cartogram/)

[![](https://1.bp.blogspot.com/-iM4dwOWUPlM/UzRX3S_LWwI/AAAAAAAAA8Q/V557_WoM0MI/s1600/sri-lanka-population-cartogram.png)](http://1.bp.blogspot.com/-iM4dwOWUPlM/UzRX3S_LWwI/AAAAAAAAA8Q/V557_WoM0MI/s1600/sri-lanka-population-cartogram.png)

Thanks, [https://github.com/mbostock](https://github.com/mbostock) for d3js library! He is a wizard in visualizations.  Thanks a lot, [https://github.com/shawnbot](https://github.com/shawnbot) for cartogram.js! Hope this will be useful to you.

### Tags

- sri lanka cartogram
- cartogram
- sri lanka d3js
- d3js