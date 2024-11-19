---
{"dg-publish":true,"permalink":"/cover-by-me/"}
---

![Cover.png](/img/user/Archives/Cover.png)



![Explanation for the design of the cover.png](/img/user/Archives/Explanation%20for%20the%20design%20of%20the%20cover.png)

Cover made in D3.js, a Javascript library made for data visualisation. I used it for the personalization it offers to create details in graphics, and for its virtually limitless resolution due to its use of SVG. It is also thematically coherent to the AI book narrator.
Creating the cover took several creative sessions distributed among two days.

### Watch the 4+ hour-long making process :

- Sped up version : [Here](https://drive.google.com/file/d/1udYeWSBOxtybJ449EOYSuR3ARUEUi2Pj/view?usp=sharing)
	- [Music](https://www.youtube.com/watch?v=D-O-Z_-Kybk)
	- [Clip](https://www.youtube.com/watch?v=cZIUW55IL_M) (Minute 23)

- Uncut[^1] and unmodified version : [Here](https://drive.google.com/file/d/1TUerGJkgwv-vlCI7VyqlAVRMNBPfkBE8/view?usp=sharing)

### Full code used to draw the cover :

```html
<html>
    <head>
        <script src="https://d3js.org/d3.v7.min.js"></script>
        <link href="https://fonts.googleapis.com/css?family=Aldrich|Arima+Madurai|Arvo|Henny+Penny|Tinos|M PLUS 1 Code|Indie+Flower|Libre+Baskerville|Pirata+One|Poiret+One|Sancreek|Satisfy|Share+Tech+Mono|Smokum|Snowburst+One|Special+Elite|Electrolize|Jua" rel="stylesheet">
    </head>
    <body>
        <div id="cover"></div>
        <script>
            var svg = d3.select("#cover").append("svg").attr("width", 750).attr("height", 1150)

            // Glow
var defs = svg.append("defs");

var filter = defs.append("filter")
    .attr("id","glow");
filter.append("feGaussianBlur")
    .attr("stdDeviation","105")
    .attr("result","coloredBlur");
var feMerge = filter.append("feMerge");
feMerge.append("feMergeNode")
    .attr("in","coloredBlur");
feMerge.append("feMergeNode")
    .attr("in","SourceGraphic");

    var defs = svg.append("defs2");

var filter = defs.append("filter")
    .attr("id","blur");
filter.append("feGaussianBlur")
    .attr("stdDeviation","35")
    .attr("result","coloredBlur");

    var defs = svg.append("defs");

var filter = defs.append("filter")
    .attr("id","blur3");
filter.append("feGaussianBlur")
    .attr("stdDeviation","3.5")
    .attr("result","coloredBlur");


    //These glow filters were made following a tutorial from Nadieh Bremer's website: .style("filter", "url(#glow)");

    // Goey filter from https://www.visualcinnamon.com/2016/06/fun-data-visualizations-svg-gooey-effect/

    var filter = svg.append("defs")
    .append("filter")
    .attr("id","gooeyCodeFilter");

filter.append("feGaussianBlur")
    .attr("in","SourceGraphic")
    .attr("stdDeviation","10")
    .attr("color-interpolation-filters","sRGB")
    .attr("result","blur");
filter.append("feColorMatrix")
    .attr("class","blurValues")
    .attr("in","blur")
    .attr("mode","matrix")
    .attr("values","1 0 0 0 0  0 1 0 0 0  0 0 1 0 0  0 0 0 19 -9")
    .attr("result","gooey");

    // Background

    svg.append("path")
  .attr("d", "M 0 0, 800 0, 800 1150 0 1150 Z")
.attr("fill", "#242424");

            // Inside pages

           var lastpage = svg.append("polygon")
            .attr("points", "0 0, 730 0, 730 1100, 0 1100, 0 0")
            .attr("fill", "#FDFD96");

            svg.append("g")
            .append("polygon")
            .attr("points", "0 0, 700 0, 700 1100, 0 1100, 0 0")
            .attr("fill", "#b0f2c2");

            svg.append("polygon")
            .attr("points", "20 20, 720 20, 720 1120, 20 1120, 20 20")
            .attr("fill", "#C3B1E1");

            d3.selectAll("g").attr('transform', "translate(40, 30) rotate(0.5, 0, 0)")
        
            d3.selectAll(lastpage).attr('transform', "translate(50, 40) rotate(-0.5, 0, 0)")
            
            // cover outline

            svg.append("polyline")
            .attr("points", "0 0, 700 0, 700 1100, 0 1100, 0 0")
            .attr("stroke", "black")
            .attr("fill", "none")
            .attr("stroke-width", "5");

            // Picture outline

            svg.append("polyline")
            .attr("points", "70 200, 530 200, 530 550, 70 550, 70 200 ")
            .attr("stroke", "black")
            .attr("fill", "none")
            .attr("stroke-width", "5");

            // Picture

            svg.append("polygon")
            .attr("points", "530 200, 70 200, 70 550, 530 550")
            .attr("fill", "#FA90F4")
            .style("filter", "url(#blur)");

            svg.append("polygon")
            .attr("points", "530 200, 70 200, 70 550, 300 550")
            .attr("fill", "#F9B179")
            .style("filter", "url(#glow)");

            svg.append("polygon")
            .attr("points", "530 200, 70 200, 70 550")
            .attr("fill", "gold")
            .style("filter", "url(#glow)");

            svg.append("polygon")
            .attr("points", "530 200, 70 200, 70 350")
            .attr("fill", "red")
            .style("filter", "url(#blur)");

            // Houses

            svg.append("path")
  .attr("d", "M 70,530 Q80,355 300, 440 T490,530")
.attr("fill", "#EFBA6B")
.attr("stroke", "cyan")
.attr("stroke-width", "5")

svg.append('ellipse')
  .attr('cx', 220)
  .attr('cy', 415)
  .attr('width', 30)
  .attr('height', 20)
  .attr('fill', '#EDE8D0')
  .attr("rx", 40)
  .attr("ry", 60)
  .style("filter", "url(#gooeyCodeFilter)");

  svg.append('circle')
  .attr('cx', 170)
  .attr('cy', 435)
  .attr('r', 40)
  .attr("fill", "#F5F5DC")
  .style("filter", "url(#gooeyCodeFilte)");

  svg.append('circle')
  .attr('cx', 330)
  .attr('cy', 465)
  .attr('r', 40)
  .attr("fill", "#F5CFB5")
  .style("filter", "url(#gooeyCodeFilte)");

                        // Picture incover

                        svg.append("polyline")
            .attr("points", "70 200, 530 200, 530 550, 70 550, 70 200 ")
            .attr("stroke", "black")
            .attr("fill", "none")
            .attr("stroke-width", "30");

                        svg.append("polyline")
            .attr("points", "450 200, 530 200, 530 550, 450 550")
            .attr("stroke", "black")
            .attr("fill", "black")
            .attr("stroke-width", "5");

            // Cover colour

            svg.append("polyline")
            .attr("points", "0 0, 0 1100, 70 1100, 70 0")
            .attr("stroke", "#FF8482")
            .attr("fill", "#FF8482")
            .attr("stroke-width", "1");

            svg.append("polyline")
            .attr("points", "0 1100, 0 540, 600 540, 600 1100")
            .attr("stroke", "#FF8482")
            .attr("fill", "#FF8482")
            .attr("stroke-width", "1");

            svg.append("polyline")
            .attr("points", "700 0, 520 0, 520 1100, 700 1100")
            .attr("stroke", "#FF8482")
            .attr("fill", "#FF8482")
            .attr("stroke-width", "1");


                                //Incover outline

                                svg.append("polyline")
            .attr("points", "0 0, 700 0, 700 1100, 600 1100, 600 100, 0 100, 0 0")
            .attr("stroke", "black")
            .attr("fill", "black")
            .attr("stroke-width", "5");

                        // corner Sun

                        svg.append("circle")
            .attr("cx", 650)
            .attr("cy", 80)
            .attr("r", 100)
            .attr("fill", "yellow");

            svg.append("polygon")
            .attr("points", "701 20, 740 0, 740 200, 701 120, 701 0")
            .attr("fill", "#FDFD96");

            svg.append("polygon")
            .attr("points", "703 20, 703 200, 720 200, 720 20, 0 20")
            .attr("fill", "#C3B1E1");

            // Cover colour external

            svg.append("polyline")
            .attr("points", "0 100, 597 100, 597 200, 0 200")
            .attr("fill", "#FF8482");


            // Title and author outline

            svg.append("polyline")
            .attr("points", "100 600, 500 600, 500 1050, 100 1050, 100 600 ")
            .attr("stroke", "black")
            .attr("fill", "none")
            .attr("stroke-width", "5");

            // Fragmented Sun

            svg.append("path")
  .attr("transform", "translate(300,825)")
  .attr("d", d3.arc()
    .innerRadius( 0 )
    .outerRadius( 135 )
    .startAngle( -1.87 )     // It's in radian, so Pi = 3.14 = bottom.
    .endAngle( -0.97 )       // 2*Pi = 6.28 = top
    )
  .attr('fill', 'gold')
  .attr("fill-opacity", "0.5")
  .attr("stroke", "#FF8482")
  .attr("stroke-width", "5")
  .style("filter", "url(#blur3)");

  svg.append("path")
  .attr("transform", "translate(300,825)")
  .attr("d", d3.arc()
    .innerRadius( 0 )
    .outerRadius( 200 )
    .startAngle( -0.97 )     // It's in radian, so Pi = 3.14 = bottom.
    .endAngle( -0.07 )       // 2*Pi = 6.28 = top
    )
  .attr('fill', 'gold')
  .attr("fill-opacity", "0.5")
  .attr("stroke", "#FF8482")
  .attr("stroke-width", "5")
  .style("filter", "url(#blur3)");

  svg.append("path")
  .attr("transform", "translate(300,825)")
  .attr("d", d3.arc()
    .innerRadius( 0 )
    .outerRadius( 115 )
    .startAngle( -0.07 )     // It's in radian, so Pi = 3.14 = bottom.
    .endAngle( 0.82 )       // 2*Pi = 6.28 = top
    )
  .attr('fill', 'gold')
  .attr("fill-opacity", "0.5")
  .attr("stroke", "#FF8482")
  .attr("stroke-width", "5")
  .style("filter", "url(#blur3)");

  svg.append("path")
  .attr("transform", "translate(300,825)")
  .attr("d", d3.arc()
    .innerRadius( 0 )
    .outerRadius( 165 )
    .startAngle( 0.82 )     // It's in radian, so Pi = 3.14 = bottom.
    .endAngle( 1.71 )       // 2*Pi = 6.28 = top
    )
  .attr('fill', 'gold')
  .attr("fill-opacity", "0.5")
  .attr("stroke", "#FF8482")
  .attr("stroke-width", "5")
  .style("filter", "url(#blur3)");
      
  svg.append("path")
  .attr("transform", "translate(300,825)")
  .attr("d", d3.arc()
    .innerRadius( 0 )
    .outerRadius( 125 )
    .startAngle( 1.71 )     // It's in radian, so Pi = 3.14 = bottom.
    .endAngle( 2.61 )       // 2*Pi = 6.28 = top
    )
  .attr('fill', 'gold')
  .attr("fill-opacity", "0.5")
  .attr("stroke", "#FF8482")
  .attr("stroke-width", "5")
  .style("filter", "url(#blur3)");

  svg.append("path")
  .attr("transform", "translate(300,825)")
  .attr("d", d3.arc()
    .innerRadius( 0 )
    .outerRadius( 155 )
    .startAngle( 2.61 )     // It's in radian, so Pi = 3.14 = bottom.
    .endAngle( 3.51 )       // 2*Pi = 6.28 = top
    )
  .attr('fill', 'gold')
  .attr("fill-opacity", "0.5")
  .attr("stroke", "#FF8482")
  .attr("stroke-width", "5")
  .style("filter", "url(#blur3)");

  svg.append("path")
  .attr("transform", "translate(300,825)")
  .attr("d", d3.arc()
    .innerRadius( 0 )
    .outerRadius( 195 )
    .startAngle( 3.51 )     // It's in radian, so Pi = 3.14 = bottom.
    .endAngle( 4.41 )       // 2*Pi = 6.28 = top
    )
  .attr('fill', 'gold')
  .attr("fill-opacity", "0.5")
  .attr("stroke", "#FF8482")
  .attr("stroke-width", "5")
  .style("filter", "url(#blur3)");

  // Title

  svg.append('text')
  .attr('x', 125)
  .attr('y', 680)
  .attr("fill", "black")
  .style("font-size", 40)
  .text("KLARA")
  .attr("font-family", "Electrolize")

  svg.append('text')
  .attr('x', 260)
  .attr('y', 680)
  .attr("fill", "black")
  .style("font-size", 20)
  .text("and")
  .attr("font-family", "Electrolize")

  svg.append('text')
  .attr('x', 300)
  .attr('y', 680)
  .attr("fill", "black")
  .style("font-size", 40)
  .text("THE SUN")
  .attr("font-family", "Electrolize")

  svg.append('text')
  .attr('x', 235)
  .attr('y', 735)
  .attr("fill", "black")
  .style("font-size", 30)
  .text("A NOVEL")
  .attr("font-family", "Electrolize")

  // Author

  svg.append('text')
  .attr('x', 120)
  .attr('y', 800)
  .attr("fill", "black")
  .style("font-size", 40)
  .text("by Nobel prize winner")
  .attr("font-family", "Tinos")

  svg.append('text')
  .attr('x', 195)
  .attr('y', 870)
  .attr("fill", "black")
  .style("font-size", 50)
  .text("石黒一雄")
  .attr("font-family", "M PLUS 1 Code")

  svg.append('text')
  .attr('x', 200)
  .attr('y', 910)
  .attr("fill", "black")
  .style("font-size", 31)
  .text("Ishiguro Kazuo")
  .attr("font-family", "Tinos")

  // Sheep "d", "M 70,530 Q80,355 300, 440 T490,530"

  svg.append("path")
  .attr("d", "M 25,1000 Q 29 985, 50 985 T 75,1000 M 75 1000 Q 65 1050, 50 1050 T 25 1000")
.attr("fill", "none")
.attr("stroke", "black")
.attr("stroke-width", "2")
.attr("transform", "translate(0, 35)");

svg.append("path")
  .attr("d", "M 25 1000 L 10 1005 L 30 1020")
.attr("fill", "none")
.attr("stroke", "black")
.attr("stroke-width", "2")
.attr("transform", "translate(0, 35)");

svg.append("path")
  .attr("d", "M 75 1000 L 90 1005 L 70 1020")
.attr("fill", "none")
.attr("stroke", "black")
.attr("stroke-width", "2")
.attr("transform", "translate(0, 35)");

// Bull

svg.append("path")
  .attr("d", "M 525,1000 Q 522 985, 550 985 T 575,1000 M 575 1000 Q 570 1050, 550 1050 T 525 1000")
.attr("fill", "none")
.attr("stroke", "black")
.attr("stroke-width", "2")
.attr("transform", "translate(0, 35)");

svg.append("path")
  .attr("d", "M 525 990 C 500 990, 510 1010, 540 1025 Q 520 1000, 525 990")
.attr("fill", "none")
.attr("stroke", "black")
.attr("stroke-width", "2")
.attr("transform", "translate(0, 35)");

svg.append("path")
  .attr("d", "M 575 990 C 600 990, 590 1010, 560 1025 Q 580 1000, 575 990")
.attr("fill", "none")
.attr("stroke", "black")
.attr("stroke-width", "2")
.attr("transform", "translate(0, 35)");



      </script>
    </body>
</html>
}
```

[^1]: The work sessions are separated, but the work is there.