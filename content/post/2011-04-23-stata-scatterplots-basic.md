---
layout: post
title: 'Stata: Scatterplots and Histograms'
tags: [Stata, Tutorial]
comments: true
---

# Scatterplots and Histograms
In this post I'll show you how to:

1. Create a basic scatterplot for examining the relationship between two variables.
2. Add a lowess smoother to a scatterplot to help visualize the relationship between two variables.
3. Create a histogram to look at your data.

## Basic Scatterplots

In this post we'll use the **auto** dataset.

	sysuse auto, clear

![autoscatter.jpg](/img/autoscatter.jpg)

## Creating a Scatterplot 

Creating scatterplots is easy in Stata. We'll use the `graph twoway scatter` command (we can just type `scatter` but I like to use the `graph twoway` syntax to make things more consistent across graph types. We'll visualize the relationship between *price* and *length*. When using `graph twoway scatter` we first list the variable that we want on the y-axis and then the variable we want on the x-axis. We'll also add a title to the graph.

	graph twoway scatter price length, title("Scatterplot of price and length")

![scatter1.jpg](/img/scatter1.jpg)

## Adding a Lowess Smoother

Adding the lowess smoother is easy as well. To do this we are going to append two `graph twoway` plots. Specifically, we are going to append `scatter` and `lowess`. We append two plots by using double-pipes -- `||`. The pipe is found on the key directly above return or enter on most keyboards (you need to hold shift).

So to get the scatterplot of *price* and *length* with a lowess smoother, we type:

	graph twoway scatter price length || lowess price length, title("Scatterplot of price and length")

![lowess1.jpg](/img/lowess1.jpg)

## Histograms

You can also use a histogram to look at your data. To create a histogram using drop-down menus, you will go to Graphics -> Histogram. In this dialogue box you need to specify which variable you are looking at in the “Variable” box. You can make any other changes or specifications you need within this window. For example, if I wanted to create a histogram of price, with the y-axis reflecting frequency, I would enter "price" in the "Variable" box and click on the "Frequency" option under the Y axis.

![Picture-61.jpg](/img/Picture-61.jpg)

To create a histogram using commands, just type “histogram (your variable).” For example, to look at miles per gallon, you would type:

	histogram mpg

![Picture-7.png](/img/Picture-7.png)

Often the default settings of the histogram may not be the best representation of your data. There are a number of useful options with the `histogram` command, including `width` with allows you to specify bin width, `frequency` which changes the y-axis to reflect frequency instead of density and `normal` which overlays a normal curve onto your graphic. You can also modify the title and axes of the graph using syntax options.

	histogram mpg, width(2) frequency normal title(mpg histogram)

![Picture-11.png](/img/Picture-11.png)