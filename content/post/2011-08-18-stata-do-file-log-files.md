---
layout: post
title: 'Stata: Do-files and Log-files'
date: 2011-08-18 14:21:24.000000000 -06:00
tags: [Stata, Tutorial]
comments: true
---
As you begin to work with datasets, there are two record and save your commands and actions in Stata.

## Creating do-files

Do-files allow you to record all of your commands. There are a number of benefits to using do-files. By using do-files to run your commands, you have a copy of what you did, which allows you and other researchers to replicate your analyses exactly. It also allows you to run analyses without changing your original data file until you are ready to save out a clean data set. Many researchers will keep a do-file recording data management (addressing missing data, reverse-scoring if necessary, etc) and may have separate do-files for analyses for the final clean data set or subsets of the data. To create a do-file, you can either go to "File"-&gt;"New Do File" or you can use this icon on the toolbar in the Stata window.

![Picture-131.png](/img/Picture-131.png)

 You're new do file should open in a separate window that looks like this:

![blank.dofile.png](/img/blank.dofile.png)

One optional step that can be helpful in creating do-files is placing a comment at the top of the file denoting which data you’re using and any other notes you want. To separate notes and comments from commands in do-files, begin the line with an asterisk. If it is a longer note, you can set it apart by typing /* before your comment and */ after the comment. For example, if I were using a data set called "relate", I might begin my data file like this:

![Picture-14.png](/img/Picture-14.png)

The first command you will need is the `use` command to specify the file you want Stata to use. If the file is not in the working directory that you are currently in, just specify which directory you want to pull the file from. Here are three examples of the `use` command, one from a data set in the current working directly, one from the internet and one from a jump drive in a different working directory. Notice that on the end of each command, I add the option `clear`. This is to clear any data that Stata is currently working with.

	use relate.dta, clear
	use http://www.stata-press.com/data/agis3/relate, clear
	use "E:\relate.dta", clear

After I specify the data file, I enter the rest of the commands I want to run. Within this file, Stata will assume that each line is a new command unless you tell it otherwise. If you have a long command that you need on separate lines, add /// at the end of each line. That tells Stata that the next line is part of the same command. When I am ready to run the analyses, I select the commands I would like to run (you don’t have to select any text if you want to run them all) and click on the last icon on the toolbar in the do-file window:

![do.file_.toolbar.run_.png](/img/do.file_.toolbar.run_.png)

To save your do-file, you can either use the icon on the toolbar or use the "File"-&gt;"Save As" menu while the do-file editor is active.

## Creating log files

In addition to recording all of your commands in a do-file, you can also have Stata create a copy of everything that is sent to the Results window, with the exception of graphs. This is called a log file and can be helpful for you to save all of your output. This will also retain your commands, although it will not save them in the same way a do-file does (they will be embedded in the output). To create a log file, go to "File" -&gt; "Log" -&gt; "Begin." This will bring up a dialogue box where you will save your log file. The default in Stata is to save the file with the extension .smcl. This will allow you to open the log file in Stata, but other programs will not read this type of file. The other extension available is .log. This file format will allow you to open your log file in other programs and may be easier to manage than the .smcl files. To save it as a .log file, just select the Stata Log option under the "File Format" menu in the dialogue box.

![log.dialogue.choose.png](/img/log.dialogue.choose.png)

Once you begin a log file, you can suspend it at any time and resume later. You can do this by going to the "File" -&gt; "Log" -&gt; "Suspend" (or "Resume"). You can also close your log using this menu.

You can also start, suspend, resume and close logs using the log command. I will use this command to begin a log file, specify the name and location of the file as well as the extension. If I were going to create a log file called "creatinglogfiles" in a file on my desktop called "501" (filepath: /Desktop/501), I would type:

	log using "/Desktop/501/creatinglogfiles", text

I included `text` because I want the file to be a .log file, not an .smcl file. If I wanted to overwrite a file that already existed, I would add `replace` after `text`.

After the log file is open, typing `log off` will suspend the log file, `log on` will resume the log file and `log close` will close your log file.
