---
layout: post
title: 'Stata: Reshaping Data'
date: 2011-08-17 17:33:17.000000000 -06:00
tags: [Stata, Tutorial]
comments: true
---
## Reshaping Data

### Reshaping

You will often have to reshape your data or change the name or values of your data to analyze it more easily. First, we’ll show you how to transform your data between "long" format, where there are multiple lines of data for every person, and "wide" format, where each subject has only one row and all data is entered in columns.

Right now, my data is in the "wide" format, where each participant reported their mood in four conditions.

![Reshaping.wideformat.png](/img/Reshaping_wideformat.png)

However, for many analyses where participants have repeated measures, you will need your data in "long" format. In order to do this, you will use the `reshape` command, specifying that you’re reshaping to the long format. The syntax is `reshape long/wide stubname, i(i) j(j)` where the stubname is the stub of your variables (in this case, it is "cond"), *i* is the id variable and *j* is the new variable you’ll create (or the existing variable if reshaping the data into wide format).

	reshape long cond, i(id) j(condition)

Now my data looks like this:

![Reshaping.longformat-176x300.png](/img/Reshaping_longformat-176x300.png)

Now each participant has 4 rows with their reported mood in each condition. This may be confusing because "cond" actually reflects the value for mood in this data. So, in order to make your data more clear, you can use the `rename` command.

	rename cond mood

![rename.condition.png](/img/rename_condition.png)

