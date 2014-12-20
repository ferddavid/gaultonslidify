---
title       : Galton Child Height Predictor
subtitle    : Predicting Child Height Based on Parent Height
author      : Ferdinand David
job         : 
framework   : io2012   # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : [mathjax]            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---

## A Child Height Predictor?

- Many parents want to know the gender of their child before birth.
- A natural extension...predict your child's height!
- Envision how tall your child will be.

--- .class #id 

## The Model Basis
- in 1885, Francis Galton studied the relationship of the heights of parents and their children.
- 928 children heights were studied
- Data was built using the midparent height as the input

$$\frac{father height + (1.08 * mother height)} {2}$$

---
## Ease of Use
- Using the two sliders in the model makes for an easy calculation of the midparent height

- The ease of use will enable adoption

![width](Capture.png)

---

##  ui.R code
- The product uses the follwing code below


```r
library(UsingR)
data(galton)
lmgalton <- lm(galton$child~., data = galton)
heightpredict <- function(height,height2) 
  predict(lmgalton, data.frame(parent=(height+(1.08*height2))/2), interval = "predict")
shinyServer(
  function(input, output) {
    output$inputValue <- renderPrint({input$height})
    output$inputValue2 <- renderPrint({input$height2})
    output$prediction <- renderPrint({heightpredict(input$height,input$height2)})
  }
)  
```

