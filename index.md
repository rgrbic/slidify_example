---
title       : text analyst
subtitle    : about shiny application for text analysis
author      : R.G.
job         : 
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : [bootstrap, shiny, interactive]   # {mathjax, quiz, bootstrap}
mode        : selfcontained     # {standalone, draft}
knit        : slidify::knit2slides
---

## What is text analyst

* text analyst is a shiny application
* find it on link https://rgrbic.shinyapps.io/appWords
* user enters text to be analyzed, app shows word frequency 

--- .class #id 

## Application structure

* user interface is <code>sidebarLayout</code> which consists of <code>sidebarPanel</code> and <code>mainPanel</code>
* <code>sidebarPanel</code> contains short application description with the radio buttons where user selects desired plot
* <code>mainPanel</code> is divided into two rows:
    + first row is input text area where user enters text to be analyzed
    + second row is output, i.e. plot of word frequency
* two plots are available:
    + word cloud plot that uses R <code>wordcloud</code> library
    + barplot of 10 most common words in the text, made with R <code>ggplot2</code> library

--- .class #id 

## Under the hood

* the code that processes the text from input text area is in <code>server.R</code>
* it first transforms text to lowercase and then removes all special charachters
* after that text is splitted into separate words and number of occurences of each word is calculated


```r
getWords <- function(text_object){
    
    text <- tolower(text_object)
    textF <- gsub("[[:punct:]]", " ", text)
    textF <- gsub("\r\n|\r|\n", " ", textF)
    textSplitted <- strsplit(textF," +")
    textWords <- unlist(textSplitted)    
    words <- plyr::count(textWords)    
    wordsSorted <- words[order(-words$freq),]
    
    wordsSorted
}
```

--- .class #id


## Word Cloud

* for plotting word cloud R library <code>wordcloud</code> is used:

<img src="assets/fig/wcloud-1.png" title="plot of chunk wcloud" alt="plot of chunk wcloud" style="display: block; margin: auto;" />

--- .class #id

## Barplot of word occurrences

* for plotting barplot R library <code>ggplot2</code> is used

<img src="assets/fig/barp-1.png" title="plot of chunk barp" alt="plot of chunk barp" style="display: block; margin: auto;" />

