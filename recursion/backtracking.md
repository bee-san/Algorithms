# Backtracking

## What is Backtracking?

Backtracking is where we incrementally build candidates to solutions, and abandon candidates \(backtrack\) as soon we as determine that candidate is not valid.

Backtracking has 3 key features:

1. Make a change
2. Recurse
3. Undo the change

And Backtracking is often used to solve 3 types of problems:

1. Decision Problem – We search for a feasible solution.
2. Optimisation Problem – We search for the best solution.
3. Enumeration Problem – We find all feasible solutions.

## What Problems can be solved by Backtracking?

Any problem that recursively build candidates to a solution and abandons a candidate \(backtracks\) when it is found to not be valid.

* Choice - we have a decision
* Constraints - we have some constraints
* Goal - we have a goal.

Imagine recursive problems. Normally we can speed things up with dynamic programming, but sometimes we don't even want to consider a solution -- we just want to throw it out.

That's what backtracking is.



{% embed url="https://www.youtube.com/watch?v=Zq4upTEaQyM" %}

  
The way I think of backtracking is as follows:

1. Make a change
2. Recurse
3. Undo the change

If at any point we reach the goal state, return true/print/whatever.

* So for the sudoku problem: For all possible squares on the board see if we can add any value between 1-9. If we can, add the value and recurse for the rest of the board. Then undo the changes by making the board blank again. Goal state is when we have successfully filled in last square
* For n queens: Iterate through the first row. If we can place a queen at a given column place it and recurse for the remaining rows. Then undo the change by removing the queen and moving to the next column. Goal is when we have placed queen on nth row
* Print all possible permutations: Initialize an empty String for results. In the input string iterate through each character. For each character, remove it from input and add it to result and recurse. Then remove the character from result and insert it back in same position in input string. Goal is when result size = n.
* Given n print all sets of valid parentheses that amount to n: Start with blank input string and 2 numbers i, j initialized to n that denote number of opening/closing parentheses remaining - you can add opening parentheses to the string if i&gt;0. You can add closing parentheses if j&gt;i. If you can add opening parentheses, add it to stringbuilder, recurse and then remove it from end of stringbuilder. If you can add closing parentheses add it to stringbuilder, recurse and then remove it from end of stringbuilder. Goal is when both i, j =0.
* Print all subsets of a set: For each character in set, remove it from input set add it to result set and if it has not been printed already, print \(goal is any set that has not been printed already\). Then recurse for remaining elements. Then remove element from result set and add it back to input set.

Pretty much all the backtracking problems I have done follows this pattern.

