---
layout: post
title: 'Stata: Oneway ANOVA'
date: 2011-07-01 03:24:36.000000000 -06:00
tags: [Stata, Tutorial]
comments: true
---
# Oneway ANOVA

This post will show how to use the `anova` and `loneway` commands in Stata to compute a oneway ANOVA.
We will use the **auto** dataset for this illustration. We will use *price* as the outcome variable and *foreign* as the factor.

Let's initially look at descriptive statistics for *price* stratified by *foreign*.

![Results-auto_dta_.jpg](/img/Results-auto_dta.jpg)

So it looks like there is a difference between in price between foreign and domestic cars, with foreign cars costing more money. We can test whether this difference is statistically significant with a oneway ANOVA (you could also just a use a t-test since there are just two levels of *foreign*).

## `anova` Command

The `anova` command is simple and follows the standard Stata syntax -- Command DV IV

	anova price foreign

Viola -- you've got an ANOVA source table.

![anova_oneway_auto.png](/img/anova_oneway_auto.png)

Looks like the difference in price is not statistically significant. The advantage of using `anova` is that you can fit lots of different ANOVA models using this command (e.g., factorial ANOVA, repeated measures ANOVA, nested ANOVA). However, if you just want to fit a oneway ANOVA, then you can use the `loneway` command.

## `loneway` Command

The `loneway` command is just for oneway ANOVA models. It provides output in addition to the source table, such as the intraclass correlation and the reliability of the group means. So depending upon the analysis you want to do and the information you need, `loneway` can be really useful.

	loneway price foreign

![Results-auto_dta-2.jpg](/img/Results-auto_dta-2.jpg)

