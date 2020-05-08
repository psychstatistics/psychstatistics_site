---
layout: post
title: 'Stata: Labeling & Recoding Data'
date: 2011-08-29 15:32:37.000000000 -06:00
tags: [Stata, Tutorial]
comments: true
---
# Labeling Variables
In order to assign labels to values of your variable, you can use either the variables manager or command syntax. For example, if you wanted to assign labels to each condition, where 1 represents No treatment, 2 represents Treatment A, 3 represents Treatment B & 4 represents Treatment C, you could double-click on the variable manager & click on "condition" and then "Manage."

![pic1.png](/img/pic1.png)

When the Manage Value Label box appears, click "Create Labels" and it will open a new dialogue box where you can give a label name to the variable and then assign labels for particular values. After you assign all of your values, be sure to click "Apply" back in your Variables Manager window.

![pic2.png](/img/pic2.png)

To create labels using commands, you would use the `label` command. The syntax is:
	
	label define labelname value "name"
	label define cond 1 "No tx" 2 "Tx A" 3 "Tx B" 4 "Tx C"

To apply your labels, use the `label` command again. The syntax is `label value variable labelname`
	
	label value condition cond

# Recoding Data

You will often need to recode values in your data for a number of reasons. For example, you may need to reverse-score items negatively-worded items on a measure. To do this via point and click, Go to Data -> Create or Change Data -> Other Variable Transformation Commands -> Recode Categorical Variable. In the Main tab, you will enter the variable(s) you want recoded and in the "Required" window, you will enter how you want them recoded. This is an example of how you might reverse score a 5-pt Likert item.

![pic3.png](/img/pic3.png)

If you’re done, click "Ok". If you want to retain your original variable and create a new variable for the reverse-scored item, go to the "Options" tab and enter the name of the new variable(s).

![pic4.png](/img/pic4.png)

It is also quick and easy to recode variables using the `recode` command:\

	recode item2 (1=5) (2=4) (3=3) (4=2) (5=1)

If you wanted to create a new variable with the recoded values, just use the `clonevar` command *first*, which will create a new variable with identical values to the first one. Then run the `recode` command on your new variable. The syntax is `clonevar newvariable = variabletoclone`

	clonevar item2_reverse = item2	

If you wanted to rename your new variable later, you would simply use the `rename` command. The syntax is `rename oldname newname`.
