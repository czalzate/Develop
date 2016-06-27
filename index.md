---
title       : Slidify
subtitle    : Calculating your Body Mass Index
author      : Cindy Alzate
job         : Ministry of Finance
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : [mathjax]
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---

## Body Mass Index

The body mass index (BMI) or Quetelet index is a value derived from the mass (weight) and height of an individual. The BMI is defined as the body mass divided by the square of the body height, and is universally expressed in units of $kg/m^2$, resulting from mass in kilograms and height in metres.

$$BMI = \frac{mass}{height^2}$$

--- .class #id 

## Calculating your BMI App

This project shows you an app created to calculates your body mass index, you just need to know your current weight(kilograms) and height(meters).

--- .class #id

## server.R

If you are a R developer you can find this server.R useful


```r
library(shiny)
```

```
## Warning: package 'shiny' was built under R version 3.2.4
```

```r
bmi<-function(mass, height){
  result<-round(mass/height^2,digits=2)
  return(result)}
shinyServer( 
  function(input, output) {
  output$mass <- renderText({input$mass})
  output$height <- renderText({input$height}) 
  output$bmiresult <- renderText({bmi(input$mass,input$height)})
} )
```
End of code.

--- .class #id

## ui.R

If you are a R developer you can find this ui.R useful


```r
library(shiny)
shinyUI(pageWithSidebar(
  headerPanel("Calculating you BMI"),
  sidebarPanel(
    numericInput(inputId="mass", label = "Insert your mass (kilograms)",0, min=0,max=200,step=1),
    numericInput(inputId="height", label = "Insert your height (meters) 
Example : 1.67 -1 meter and 67 centimeters-",0,min=0,max=10,step=0.01),
    h3("Score"),helpText("Low weight (BMI < 18,5)","Normal weight (BMI = 18,5-24,99)", "Overweight (BMI = 25-29,99)","Obesity (BMI >= 30)"
    )
  ),
  mainPanel(
    h3('Results'),
    p('Your mass is:'),textOutput('mass'),
    p('Your height is:'),textOutput('height'),
    h4('Your BMI is:'),textOutput("bmiresult"))))
```

<!--html_preserve--><div class="container-fluid">
<div class="row">
<div class="col-sm-12">
<h1>Calculating you BMI</h1>
</div>
</div>
<div class="row">
<div class="col-sm-4">
<form class="well">
<div class="form-group shiny-input-container">
<label for="mass">Insert your mass (kilograms)</label>
<input id="mass" type="number" class="form-control" value="0" min="0" max="200" step="1"/>
</div>
<div class="form-group shiny-input-container">
<label for="height">Insert your height (meters) 
Example : 1.67 -1 meter and 67 centimeters-</label>
<input id="height" type="number" class="form-control" value="0" min="0" max="10" step="0.01"/>
</div>
<h3>Score</h3>
<span class="help-block">
Low weight (BMI &lt; 18,5)
Normal weight (BMI = 18,5-24,99)
Overweight (BMI = 25-29,99)
Obesity (BMI &gt;= 30)
</span>
</form>
</div>
<div class="col-sm-8">
<h3>Results</h3>
<p>Your mass is:</p>
<div id="mass" class="shiny-text-output"></div>
<p>Your height is:</p>
<div id="height" class="shiny-text-output"></div>
<h4>Your BMI is:</h4>
<div id="bmiresult" class="shiny-text-output"></div>
</div>
</div>
</div><!--/html_preserve-->

