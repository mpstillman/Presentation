---
title       : Developing Data Products
subtitle    : Slidify Project - Automobile mpg Prediction
author      : Mike Stillman
logo        : Star.png
job         : 
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---

## Introduction

<p>Are you interested in validating the miles per gallon of your automobile?</p>
<p>Are you interested in ensuring that salesperson is telliing the truth about the automobile you want to buy?</p>
<p>Check out this App which will determine the miles per gallon (mpg) of the automobile based on historic mpg automobile data.</p>
<p><a> https://mpstills.shinyapps.io/Project</a></p>

--- .class #id 

## Data

1. For the Automobile mpg Prediction App, the mtcars R dataset was used to create the model.

```r
library(datasets)
head(mtcars)
```

```
##                    mpg cyl disp  hp drat    wt  qsec vs am gear carb
## Mazda RX4         21.0   6  160 110 3.90 2.620 16.46  0  1    4    4
## Mazda RX4 Wag     21.0   6  160 110 3.90 2.875 17.02  0  1    4    4
## Datsun 710        22.8   4  108  93 3.85 2.320 18.61  1  1    4    1
## Hornet 4 Drive    21.4   6  258 110 3.08 3.215 19.44  1  0    3    1
## Hornet Sportabout 18.7   8  360 175 3.15 3.440 17.02  0  0    3    2
## Valiant           18.1   6  225 105 2.76 3.460 20.22  1  0    3    1
```

```r
nrow(mtcars)
```

```
## [1] 32
```

--- .class #id 

## Model

1. The Automobile mpg Prediction app uses a multiple covariate regression model.
2. Initially, the model will be trained and validated with a training and test data set.
3. The model is created using the R caret package.

```r
library(caret)
inTrain<-createDataPartition(y=mtcars$mpg,p=0.75,list=FALSE)
training<-mtcars[inTrain,]
modFit<- train(mpg ~ cyl + hp + wt , method = "lm", data=training)
```
4. The model is then used within the server.R shiny app file to produce interactivity with this app.

```r
mpgprec <- function(cyl, hp, wt) 
{ data <- data.frame(cyl, hp, wt)
  predict(modFit,newdata=data)}
```

--- .class #id 

## Conclusion

<p> Using the Shiny and Slidify R packages, the Automobile mpg Prediction app is a simple use case, but shows the capabilities of these R packages.</p>
<p> Use this URL to access the app.  <a>https://mpstills.shinyapps.io/Project</a></p>

--- .class #id 
