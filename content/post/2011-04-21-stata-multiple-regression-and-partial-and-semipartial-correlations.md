---
layout: post
title: 'Stata: Multiple Regression and Partial and Semipartial Correlations'
date: 2011-04-21 05:26:12.000000000 -06:00
tags: [Stata, Tutorial]
comments: true
---

# Multiple Regression 
This post will:

1. Show how to extend [bivariate regression](http://www.psychstatistics.com/2011/04/19/stata-bivariate-regression/) to include multiple predictor variables.
2. Show how to manually create partial and semipartial correlations using residuals from a regression model.
3. Show how to use the `pcorr` command to obtain partial and semipartial correlations.

## Multiple Predictors 

We will again use the **auto** dataset.

	sysuse auto, clear

![autodata.jpg](/img/autodata.jpg)

Suppose we want to regress *price* on three variables -- *mpg*, *weight*, and *foreign*. To add three predictors, we simply add the variables we want after the dependent variable.

	regress price mpg weight foreign

This produces the following output.

![multreg.jpg](/img/multreg.jpg)

## Partial and Semipartial Correlations - Manual Method 

Recall that a partial correlation is the relationship between *x* and *y* once the shared variance between *x* and *x2* has been removed from *x* and once the shared variance between *y* and *x2* has been removed from *y*. A semipartial correlation is similar except that we only remove the shared variance between *x* and *x2* (i.e., *y* remains untouched). Note: Although I've only referenced *x2*, we can in principle include many control variables as our example will show.

Suppose we want to obtain the partial correlation between *price* and *mpg* controlling for *weight* and *foreign*. To do this we need the part of *price* that is independent of *weight* and *foreign*. We also need the part of *mpg* that is independent of *weight* and *foreign*. We can get this information with residuals.

### The part of *price* independent of *weight* and *foreign* 

To obtain the part of *price* independent of *weight* and *foreign* we regress *price* on *weight* and *foreign*. 

	regress price weight foreign

We then save the residuals for *price*. We'll call this *priceres*

	predict priceres, residuals

We now have a new variable in our dataset called *priceres*.

	summarize priceres, detail

![priceres.jpg](/img/priceres.jpg)

### The part of *mpg* that is independent of *weight* and *foreign* 

At this point, we need to repeat what we did about except substitute *mpg* for price. We regress *mpg* on *weight* and *foreign*.

	regress mpg weight foreign

We save the residuals for *mpg*. We'll call this *mpgres* (not very original, I know).

	predict mpgres, residuals

We now have a new variable in our dataset called *mpgres*.

	summarize mpgres, detail

![mpgres.jpg](/img/mpgres.jpg)

### Partial correlation 

We know have everything we need for the partial correlation between *price* and *mpg* controlling for *weight* and *foreign*. Specifically, we have *priceres* -- which is the part of *price* that is independent of *weight* and *foreign*. We also have *mpgres* -- which is the part of *mpg* that is independent of *weight* and *foreign*. Therefore, to obtain the partial correlation we simply need to correlate *priceres* and *mpgres*. 

	corr priceres mpgres

![partialcorrelation.jpg](/img/partialcorrelation.jpg)

### Semipartial correlation 

We also already have everything we need for the semipartial correlation. Recall that for the semipartial correlation we only remove the shared relationship between *x* and the *x2* (or set of covariates). We don't do anything with *y*. In our example *price* is our *y* variable. So to compute the semipartial correlation we correlate *price* (i.e., the "untouched" *y* variable) and *mpgres* (i.e., the part of *mpg* that is independent of *weight* and *foreign*).

	corr price mpgres

![semipartialcorrelation.jpg](/img/semipartialcorrelation.jpg)

## Partial and Semipartial Correlations - `pcorr` 

Thankfully Stata has a built in command for computing partial and semipartial correlations -- [pcorr](http://www.stata.com/help.cgi?pcorr). To obtain the partial and semipartial correlations, we type:

	pcorr price mpg weight foreign

Note that the first variable listed is considered the *y* variable. All other variables are variables are considered *x* variables. Stata reports as many partial and semipartial correlations as there are *x* variables. Additionally, Stata reports the squared partial and squared semipartial correlations. These are interpreted as the proportion of shared variance between *y* and *x* controlling for the other *x* variables. The partial and semipartial correlations listed for *mpg* are the same as what we found above.

![pcorr.jpg](/img/pcorr.jpg)
