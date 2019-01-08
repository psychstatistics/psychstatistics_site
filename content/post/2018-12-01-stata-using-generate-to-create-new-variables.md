---
title: 'Stata: Using generate to create new variables'
author: Scott
date: '2018-12-01'
slug: stata-using-generate-to-create-new-variables
categories: []
tags:
  - Stata
  - tutorial
image:
  caption: ''
  focal_point: ''
---

# Generating New Variables

The primary method for creating new variables in Stata is the `generate` command. Load the `auto` dataset.

	clear
	sysuse auto
	describe

![Results-auto.dta_1.jpg](/img/Results-auto_dta_1.jpg)

## New Variable from Existing Variables

Let's create a new variable that is the sum of `weight` and `length` (ignore for the moment that summing weights and lengths doesn't make a ton of sense). Simple with `generate`. The syntax of `generate` is:

	generate nameOfNewVariable=whateverTheNewVariableIsEqualTo
	
So to create a new variable called `weightlength` that is the sum of `weight` and `length` we type:

	generate weightlength = weight+length

Now we have new variable called `weightlength`.

![Results-auto.dta-21.jpg](/img/Results-auto_dta-21.jpg)

Suppose now that we want to create a new variable that is the square of weight.

	generate weight2 = weight^2

## New Variable that is a Constant

Suppose we want to create a new variable that is a constant value (this isn't necessarily a good idea and you can use macros to store constants but using a variable can be pretty convenient too). Let's make a new variable `x` that is equal to 100.

	generate x = 100

Let's create a new variable that is equal to the mean of weight -- we'll call it `meanweight`.

	summarize weight

![Results-auto.dta-3.jpg](/img/Results-auto_dta-3.jpg)

	generate meanweight = 3019.459

You can also use the results of the `summarize` command to create a mean.

![Viewer-1-help-summarize-1.jpg](/img/Viewer-1-help-summarize-1.jpg)

	summarize weight
	generate meanweight = r(mean)

You can use the `_N` operator to create a new variable that is equal to the number of observations in a dataset.

	generate obs = _N

If you combine this with `by` you can create a new variable that will be equal to the number of observations within the levels of the `by` variable. For example, we can type:

	by foreign: generate obs = _N

This will create a variable that is a constant within the levels of `foreign`. That is, we are going to get the number of foreign cars and the number of domestic cars. If a line in the data is associated with foreign cars the new `obs` variable will have a value of 22 and domestic cars will have a value of 52. Give it a try and see how it works.

## New Variable that is a Random Draw from a Distribution

We can create a new variable that is a random draw from a distribution. Let's create a new variable whose values will be random draws from a normal distribution with a mean of 0 and a standard deviation of 1. The random normal generator command is `rnormal()` (it defaults to a mean of 0 and standard deviation of 1 and it will draw as many values as there are observations in the dataset).

	generate random = rnormal()

## Create a New Variable that Indexes the Observations

You can use the `_n` operator to create a variable that indexes the observation number.

	generate index = _n

This will create a new variable that runs from 1 to 74. You can combine this with `by` to create an index within another variable.

	by foreign: index = _n

This will create a new variable that runs from 1 to 52 for domestic cars and 1 to 22 for foreign cars.

## Conclusion

I've just touched on the ways you can create new variables. You can also use the `egen` command to create new variables. Try new ways to create variables and be sure to read the help files.
