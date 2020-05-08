---
layout: post
title: 'Stata: Correlation and Covariance'
date: 2011-04-21 14:18:41.000000000 -06:00
tags: [Stata, Tutorial]
comments: true
---

# Correlation and Covariance 
This post will illustrate how to:

1. Create a correlation matrix of variables using the [`correlate`](http://www.stata.com/help.cgi?correlate) command.
2. Display a correlation matrix as a covariance matrix.
3. Obtain the statistical significance of a correlation using the [`pwcorr`](http://www.stata.com/help.cgi?pwcorr) command.

## Correlation Matrix 

We'll use the **auto** dataset for this tutorial.

	sysuse auto, clear 

![auto.jpg](/img/auto.jpg)

We'll create a correlation matrix of four variables -- *price*, *mpg*, *weight*, and *length*.

	correlation price mpg weight length

![corr.jpg](/img/corr.jpg)

Note: We can shorten the `correlation` command to `corr` for convenience.

## Covariance Matrix 

If we want to create of covariance matrix, we simply add the `covariance` option to the `correlation` command. 

	correlation price mpg weigh length, covariance

![covariance.jpg](/img/covariance.jpg)

## Statistical Significance of a Correlation 

The `correlation` command produces a clean correlation matrix (or covariance matrix with the `covariance` option). If we want to see the statistical significance of a correlation, we need to use the `pwcorr` command with the `sig` option.

	pwcorr price mpg weight length, sig

![pwcorr.jpg](/img/pwcorr.jpg)

