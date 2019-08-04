
<html>
<script src='https://d3js.org/d3.v5.min.js'></script>
<body onload='init()'>
<script src='https://d3js.org/d3.v5.min.js'></script>
<style> rect {fill: darkblue; stroke: white; }</style>
<body>
<svg id="svg1" width=300 height=300>
</svg>
<script>
async function init() {

const data2 = await d3.csv("https://raw.githubusercontent.com/sharmaarchit/DataVisualization/master/NamesHigherThan1000-Sample.csv");
data2.sort(function(a,b) { return +a.Count - +b.Count })  

//console.log(Object.keys(data2))
//console.log(data2[2].Gender)

var ticks = [0,1,2,3,4,5,6,7,8,9];
var max = d3.max(data2, function(d) { return +d.Count;} );
var bars = Object.keys(data2);

bars.length = bars.length - 1 //removing the last element "columns"


var margin = 50;
var marginplus = margin+1;
var panwidth = 650;
var width = 650;
var height = 450;
var svgwidth = width + 2*margin;
var svgheight = height + 2*margin;
var tempheight = height - margin;

var firstbar = margin+width;

var xscale2 = d3.scaleLinear().domain([0,max]).range([0, width])

var yscale2 = d3.scaleBand().domain(bars).range([height,0])
var halfBandwidth = yscale2.bandwidth()*0.5
console.log(halfBandwidth)


var yscaletext2 = d3.scaleBand().domain(bars).range([height,0])

d3.select("#svg1").append("g")
	.attr("transform","translate("+margin+","+margin+")")
	.call(d3.axisLeft(yscale2))
  //.tickValues(ticks)
  .selectAll("text").remove();//removes the tick text

d3.select("#svg1").append("g")
	.attr("transform","translate("+margin+","+(height+margin)+")")
	.call(d3.axisBottom(xscale2));


var svg_2 = d3.select('#svg1')
	.attr("width",svgwidth)
	.attr("height",svgheight)
	.attr("style","outline:1px solid black")
	.append('g')
	.attr("transform", "translate("+marginplus+","+margin+")")
	//.attr("style","outline:1px solid red");
  
var rect2 = svg_2.selectAll("rect")
	.data(data2)
	.enter()
	.append("rect")
	.attr("x",function(d,i) {return 0})
	.attr("y",function(d,i) { return yscale2(i); })
	.attr("height",yscale2.bandwidth())
	.attr("width",function(d,i) {return (xscale2(+d.Count))})
    .style("fill",function(d) {if (d.Gender == "F") {return "pink"}
                               else {return "lightblue"}})
                                
var text_2 = svg_2.selectAll("text")
	.data(data2)
	.enter()
    .append("text")
    .text(function(d) {                 
                    return d.Name;
           })
	.attr("x",function(d,i) {return 25})
	.attr("y",function(d,i) {return (yscaletext2(i)+halfBandwidth*1.2); })
	.attr("font-family", "sans-serif")
    .attr("font-size", "12px")
    .attr("fill", "black");


}
</script>
</body>
</html>









<!--
//Sorting done
//text positioning correct
-->



