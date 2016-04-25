---
title       : Unit Converter Presentation
subtitle    : Project - Data Product
author      :  Yushu Chen      
job         :  Data 
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---

## What it does?

### Converts units that are commonly used 

+ **length**: inch to cm
+ **mass**: lb to kg
+ **volume**: galllon to litre

--- 

## Converts in 2 Simple Steps

* Choose the type of units conversion 
* type in the amount you wish to convert to

The result will automatically shown in the right panel

---

## User Inderface Definition


```r
library(shiny)

# Define UI for application that draws a histogram
shinyUI(pageWithSidebar(
      #Application Title
      headerPanel('Unit Converter'),
      
      sidebarPanel(
            radioButtons("unit", label = h3("Type of Conversion"),
                         choices = list("inch to cm" = 1, "lb to kg" = 2, "gal to L" = 3), 
                         selected = 1),
      numericInput('num',label = h3('From value'), 1)
                  ),
      mainPanel(
            h3('Conversion Result'),
            verbatimTextOutput('output')
      )
)     
)
```

---

## Server Definition


```r
library(shiny)

# unit converter function
unitCvt<-function (unit, num){
      if(unit==1){result <- num*2.54}
      else if (unit ==2){result <-num*0.453592}
      else{result<-num * 3.78541}
      print (result)
}

shinyServer(function(input, output) {
      output$output<-renderPrint({unitCvt(input$unit, input$num)})
})
```






