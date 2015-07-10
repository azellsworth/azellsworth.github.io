---
layout: post
title:  "Solving a Decision Tree Using a Stack"
date:   2015-07-08 18:29:37
categories: decision trees
---

In this blog post, I'll cover solving decision tree problems using a stack. This method was brought to my attention by Matthieu Faugere and Tim Quach, fellow students at [Hack Reactor](http://www.hackreactor.com). The code and pseudocode were written by Kiri Strack-Grose and myself. 

## What is a Stack?
A stack is a method of organizing data, where you add and remove from the top of the list. For example, when you place T-shirts into a drawer, you add shirts to the top of the pile and take out the top shirt first. When browsing the web, every time you click a link, you are adding a webpage to the history stack. Each time you press the back button, the browser is taking the webpage off the top of the history stack and showing it to you.

It turns out that stacks can be used to solve some pretty complex problems in a straightforward manner.

##What is a Decision Tree?
Say that you want to determine all the possible outcomes of a rocks, paper, scissors game. Let’s say there are 5 rounds in the game. The first round you have three options. The next round, you will have another set of three options for each variation of the first round. As you can see, the number of combinations is going to add up very quickly.

![Rock, Paper, Scissors Decision Tree](http://nicmitchell.com/wp-content/uploads/2014/11/rock-paper-scissors.jpg)

This is an example of a decision tree. Every level in a decision tree will expand based on the number of options you have (in this case: rock, paper, or scissors). 

This problem can be solved recursively, but by using a stack, we can save time, and create very clear code.

## A General Approach

The general approach for solving for all solutions with a stack is as follows:

* Create a stack containing the starting state of the game
* Start a while loop that runs as long as the stack is not empty
* Pull an element off the top of the stack, make n copies of it (3 in this case for R-P-S)
* Push one decision to each of the element copies (rock, paper, or scissors)
* Push each element copy back into the stack
* Keep repeating until an element’s length is 5 (or number of rounds) 
* This is a solution! Push it to a separate solutions array

##Rocks Paper Scissors Pseudocode 

{% highlight javascript %}
var rpsSolutions = function(rounds){
  // create an external solutions array
  // create a stack, which will contain all states leading up to the solutions
  // push an empty array to the stack - this represents the root of the tree
  // we need a current round variable, which will start at 0
  // we need an array containing possible throws
  // we need a while loop that will run until the stack is empty
    // (inside the while loop)
    // we need to pop a state off of the stack
    // if the length of the state is equal to max rounds
      // this is a solution, push the state to the external solutions array
    // else
    // we need to run a loop for all the possible throws
      // make a deep copy of the state
      // push the current possible throw to the stateCopy
      // push the stateCopy to the stack
    // increment the current round
  // return external solutions array
};
{% endhighlight %}

##Javascript Code

{% highlight javascript %}
var rpsSolutions = function(rounds){
  var solutions = []; // external solutions array
  var stack = []; // starting empty stack
  stack.push([]); // starting state of an RPS game is an empty array
  var currentRound = 0;
  var possibilities = ['rock', 'paper', 'scissors']; 
  while (stack.length) { // while loop will run until the stack is empty
    var state = stack.pop(); // pull a state out of the stack
    if (state.length === rounds) { // if state length is total rounds
      solutions.push(state); // this is a solution, push it to the array
    }
    else {
    // we need to run a loop for all the possible throws
      for (var i = 0; i < possibilities.length; i++) {
        var stateCopy = state.slice(); // make a deep copy of the state
        stateCopy.push(possibilities[i]); // push the throw to the copy
        stack.push(stateCopy); // push the stateCopy to the stack
      }
    }
    currentRound++; // move to the next round
  }
  return solutions; // return filled solutions array
}
{% endhighlight %}

You can try this out by copying the code into repl.it(hyperlink) or any other javascript tester. It could be helpful to step through with a debugger to see how it’s working.

##Takeaway

This stack approach can be very useful for other decision tree problems, such as [n-queens](https://developers.google.com/optimization/puzzles/queens). If you are being asked to solve for all possible solutions, chances are you’re looking at a decision tree problem, and may be able to employ this method. Hope you found this helpful!

