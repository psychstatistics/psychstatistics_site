---
layout: post
title: 'Stata: Planned Comparisons with the test command'
tags: [Stata, Tutorial]
comments: true
---
# Planned Comparisons

This post will show you how to:

1. Run a one-way ANOVA using an independent variable with four levels.
2. Use planned comparisons to contrast levels of the independent variable.

We will use the built-in dataset **systolic**.

	webuse systolic

## Examining the data

We will treat the *systolic* variable as the outcome and *drug* as the independent variable. Let's look at descriptive statistics for *systolic* and frequencies for *drug*.

	summarize systolic, detail

![Results-systolic.dta-1.jpg](/img/Results-systolic_dta-1.jpg)


	table drug

![Results-systolic.dta_.jpg](/img/Results-systolic_dta.jpg)

Let's also look at a boxplot of systolic by drug.

	graph box systolic, by(drug)

![NewImage.png](/img/NewImage.png)

Thus, it appears there are some differences between drug levels and systolic blood pressure.

## Oneway ANOVA

Let's run a oneway ANOVA. The null hypothesis is that there is no difference in the mean systolic blood pressure among the levels of drug.

	anova systolic drug

We reject the null hypothesis.

![Results-systolic.dta-2.jpg](/img/Results-systolic_dta-2.jpg)

## Using the `test` command to perform planned comparisons

In Stata, once we have completed the ANOVA, we can use the `test` command to perform planned comparisons. Note two important things about the `test` command:

1. You can only use it **after** you have run the ANOVA. If you try to run it before you run the ANOVA, it won't work.
2. The `test` command is available to use for the most recently run model. If you run a second (or third, fourth, etc.) ANOVA model or another model that supports the `test` command (e.g., a regression) after you run the ANOVA you care about, you won't be able to run the analysis you care about. That is, the information that `test` needs will not be available if you run another model.

Let's say we want to know whether the average of drugs 1 and 2 differ from the averages of 3 and 4. To do this, we'd type the following command (after we ran the ANOVA).

	test (1.drug + 2.drug)/2 = (3.drug + 4.drug)/2

![Results-systolic.dta-3.jpg](/img/Results-systolic_dta-3.jpg)

We reject the null hypothesis that they are not different. Note that to reference levels of the variable *drug* we type `1.drug` or `2.drug`, etc. We put the level number, then a period, then the variabl ename.
See if you can figure out why the following statement is equivalent

	test (1.drug + 2.drug)/2 - (3.drug + 4.drug)/2 = 0
	
Suppose we want to know if level 1 of drug is different from level 2.

	test 1.drug = 2.drug

![Results-systolic.dta-5.jpg](/img/Results-systolic_dta-5.jpg)

We cannot reject reject the null.

The `test` command is really quite flexible. Fiddle around with it to better learn the syntax.
