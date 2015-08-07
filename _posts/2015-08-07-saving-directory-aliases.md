---
layout: post
title:  "A Quick Way to Make CD Aliases"
date:   2015-07-08 18:29:37
categories: npm
---
##The Problem

When I first started using command line tools heavily, I found that it was cumbersome to move through the directories. I would in “ls” to see the files and folders in the current directory, then “cd” into the next directory. I would then repeat the process, until I got to the directory I was looking for.

##The Short Term Fix

I was later introduced to aliases, which allow you to set up short bash commands that execute more complicated lines of code. With this, I could set up a shortcut to a directory by adding a fairly simple line to my bash profile. As an example:

{% highlight bash %}
alias doc="cd  /Users/Me/Documents"
{% endhighlight %}


Every time I typed in doc, or any other alias I set up, it would take me to the correct directory. 

##The Solution

At a hackathon, I was given the opportunity to make this process even easier. I decided to write a bash script that would add an alias to the bash profile automatically. This means I could just type in a simple command in any directory to save an appropriate alias.

I decided to call this script: **mkal** (short for make alias).

After chatting with some fellow programmers, it turned out that quite a few other people wanted access to the command, so we decided to publish an npm module, and make an open source git repo for the script. 

##You can install it now!

You can now download mkal for yourself by typing in:

{% highlight bash %}
npm install -g mkal
{% endhighlight %}


##How to use it 

When you're in a directory and want to save an alias to it, just type: 

{% highlight bash %}
mkal [shortcut name]
{% endhighlight %}

Then, when you want to return to that folder, simply type in [shortcut name].

##The Code

If you’re interested, here’s the bash script itself:

{% highlight bash %}
#!/bin/bash

X=$(pwd)   #saves present working directory to X
WD=${X// /\\ }  #replaces spaces with '\ '
  sed -i '' -e '$a\' ~/.bash_profile   #creates a new line at the end of bash_profile if necessary
  echo 'alias' "$1"'="cd ' $WD'"' >>~/.bash_profile   #creates an alias for pwd at end of bash_profile
  . ~/.bash_profile   #reloads bash_profile
{% endhighlight %}
