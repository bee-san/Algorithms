# Introduction

## Discovering a Recursive Problem

A recursive function should have the following properties so that it does not result in an infinite loop:

1. A simple `base case` \(or cases\) — a terminating scenario that does not use recursion to produce an answer.
2. A set of rules, also known as `recurrence relation` that reduces all other cases towards the base case.

Note that there could be multiple places where the function may call itself.

A good hint is that **recursion is built off of subproblems**.

When you hear a problem with the following statements, it's often \(though not always\) a good candidate for recursion: "Design a problem to compute the nth....", "Write code to list the first n....", "implement a method to compute all....", and so on.

People typically have about 50% accuracy in their "this sounds like a recursive problem...." instinct. Use that instinct, since that 50% is valuable. But don't be afraid to look at the problem in a different way, even if you initially thought it seemed recursive. There's a 50% chance you are wrong

Other things that can indicate a recursion problem are:

* Does the problem obviously break down into subproblems?
* Could the problem be solved with an arbitrary number of nested `for` loops? For when you think "this problem would be easy if I can control how many nested for loops are generated"
* Can you reframe the problem as a search problem? If so, DFS can be used.
* Is it easier to solve recursively than iteratively?

## Understanding any recursive code, step by step

Look at the following code:

```text
void f(int n) {
   if (n == 0) return;
   f(n-1);
   print(n);
}
```

What is the output of this code?

If we read the code in order, we might think it'll print `5, 4, 3, 2, 1`. But this is wrong, the recursive call happens before we can continue to the end.

Our code executes as:

```text
f(5)
   f(4)
       f(3)
           f(2)
               f(1)
                   f(0)
                   print(1)
               print(2)
           print(3)
       print(4)
   print(5)
```

**The output is not always going to occur in the order it appears in our code**

### How do we accurately compute the output?

Walk through the code step by step. You are now the compiler.

The most important thing to do is to walk through the code exactly as the compiler would. As soon as you start assuming how the code will behave and not reading through it line-by-line, you’re screwed.

#### Draw the tree

All recursive functions act like a tree.

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8c42d9b9-4ab8-4bb0-a279-5dfb9fb4c38f/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8c42d9b9-4ab8-4bb0-a279-5dfb9fb4c38f/Untitled.png)

#### Do not lose track of variables

As functions get more complicated it becomes harder and harder to actually store everything in your head, especially since you have to do your recursion out of order. The tree will help you with this.

#### Practice

I know this may not sound like the most fun task, but understanding recursive code is critically important. If you can understand the recursive code that other people write and why it works it will make it exponentially easier for you to write your own recursive code.

## Returning from Recursive Functions

Some recursive functions simply return an object after it's done. But not always! Let's talk about the different ways it can return.

### Global Variable

The first option \(and the only one here that I’d say you should probably never use\) is to store your result into a global variable. We all know that global variables aren’t a great solution when there is another option, so try to avoid this if possible.

For demonstration purposes, let’s look at a function that counts the number of even values in an array. Here’s how we could write this code using a global variable:

```text
int globalResult;
 
void countEvenGlobal(int[] arr) {
   globalResult = 0;
   countEvenGlobal(arr, 0);
}
 
void countEvenGlobal(int[] arr, int i) {
   if (i >= arr.length) return;
   if (arr[i] % 2 == 0) globalResult++;
   countEvenGlobal(arr, i+1);
}
```

The key here is that we will simply create a global variable and update the value as we recurse through our code. Whenever we find an even value in our array, we just increment the global variable, similar to how we might solve this problem iteratively.

### Passed Variable

We pass a variable to our recursive function that will update as it goes.

```text
class ResultWrapper {
   int result;
}
 
int countEvenPassed(int[] arr) {
   ResultWrapper result = new ResultWrapper();
   result.result = 0;
   countEvenPassed(arr, 0, result);
   return result.result;
}
 
void countEvenPassed(int[] arr, int i, ResultWrapper result) {
   if (i >= arr.length) return;
   if (arr[i] % 2 == 0) result.result++;
   countEvenPassed(arr, i+1, result);
}
```

Note in this code, if we are using a language like Java, we have to use some sort of ResultWrapper class because we cannot directly pass a pointer to our function and we will be updating the value as we go.

The advantage of this approach is that it is generally the easiest for most people to understand. It also gives us the opportunity to do tail recursion, if that is something that our language \(and the problem\) supports.

### Build the result as we return

Our third strategy is a bit more difficult to understand because we are essentially doing the work that we need to do in reverse order. We will return partial values as we return from our recursive calls and combine them into the result that we want.

The reason that this strategy is critical is that it will make it possible for us to use the FAST Method to solve dynamic programming problems. If we use one of the previous two approaches, we are not isolating our subproblems and so it becomes impossible for us to actually cache the values that we want.

```text
int countEvenBuiltUp(int[] arr) {
   return countEvenBuiltUp(arr, 0);
}
 
int countEvenBuiltUp(int[] arr, int i) {
   if (i >= arr.length) return 0;
   int result = countEvenBuiltUp(arr, i+1);
   if (arr[i] % 2 == 0) result++;
   return result;
}
```

For the most part, you can use these return strategies interchangeably for different recursive problems.

Don’t bother practicing using global variables, since you really should never use that in your interview. However, I would recommend practicing both of the others. Try doing a practice problem both ways. See what the similarities and differences are. The extra practice will do you good!

## Backtracing

Backtracking is an essential strategy that we use in recursion. It essentially allows us to try different possible results without actually knowing ahead of time what the right result is.

Consider the Knight’s Tour problem. In this problem, we want to find a path that a knight can follow on a chessboard where it will visit each square exactly once.

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5d5116f4-5f85-4f8b-ae13-4b31b5696683/image6.gif](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5d5116f4-5f85-4f8b-ae13-4b31b5696683/image6.gif)

We don’t actually know what the right more is to make ahead of time and a knight can make up to 8 different moves from any one square, so we just have to pick a move at random.

But obviously not all combinations of moves will take us through a valid path. Some moves might trap us in a corner that we can’t get out of without visiting the same square twice.

So what do we do? We “backtrack”.

The idea behind backtracking is simply that we retrace our steps backwards and then try a different path. This allows us to try every different path until we ultimately find one that is valid.

Another example of this that you’re likely already familiar with is depth-first search in a tree. When we are looking for a node in a tree, we consider the leftmost branch first. Then what happens if we don’t find the node we’re looking for? We backtrack.

We go back up one level and try the other child of the parent node. If we still haven’t found what we are looking for, we go back up the tree even further. This continues until we find what we are looking for or have gone through the entire tree.

Some common backtracking problems include:

* [0-1 Knapsack](https://www.byte-by-byte.com/01knapsack/)
* [Sudoku Solving](https://leetcode.com/problems/sudoku-solver/)
* [N Queens](https://leetcode.com/problems/n-queens/)
* [And many more…](https://leetcode.com/tag/backtracking/)

A note on backtracking: A lot of people hear “backtracking” and they stress out about it, but my guess is that if you’ve done any recursion in the past, you’re already familiar with the basic concept. Don’t stress too much about this one specifically. Just make sure you understand how to implement the 6 recursive patterns and you’ll learn how to do backtracking as a side-effect.

## Tail Recursion

Okay this is the most unnecessarily worried about concept in all of recursion. Tail recursion almost never comes up in an interview and isn’t even supported by [most major programming languages](https://en.wikipedia.org/wiki/Tail_call).

Tail recursion is an optimization technique that you can use to improve the space complexity of a small subset of recursive problems. To understand how this works, we do need to talk about space usage for a second.

When you make recursive calls, the computer needs to save the state of the current function \(all the variables, the current position that you’re executing at, etc\) so that you can return back after the end of the recursive call.

Therefore, for every recursive call you make, you are using some space on the call stack. The more recursive calls you make, the more space you’re using.

Tail recursion allows us to avoid having to use extra space. Imagine that you write a function where the very last line of the function is the recursive call that immediately returns. Then do you really need to save the previous function state on the call stack?

No. You can just return the value from the deepest level of your recursion directly to the top.

That is what tail recursion does for us. If we have a single recursive call that is the very last thing before we return, then we can optimize out the extra stack space.

To look at our simple example from earlier, which of these is tail recursive?

```text
void f1(int n) {
   if (n == 0) return;
   f1(n-1);
   print(n);
}
```

Or

```text
void f2(int n) {
   if (n == 0) return;
   print(n);
   f2(n-1);
}
```

Based on our definition, you can see that in f2\(\), the very last thing we do is our recursive call. f1\(\) prints after we make the recursive call so we can’t optimize it because we are going to need to return back to the previous function so that we can call print\(n\).

So in limited circumstances, tail recursion can be useful. It is particularly useful while doing functional programming, since you are often doing basic things like iteration recursively that can be easily optimized.

However, most of the time, tail recursion won’t be helpful to us. Chances are the language that you’re using won’t support it and on top of that, many of the examples that we will see in our interviews will require us to make multiple recursive calls within our function. If you have multiple calls, they can’t both be the last thing before we return and so tail recursion is out of the question.

## Calculating Time & Space Complexity

Time and space complexity for recursive problems tends to pose quite a challenge. Because recursive problems are so hard to parse in the first place, it is often non-obvious how we would compute the complexity.

### Time Complexity

Remember when we represented our recursion as a tree structure? Well that tree structure can show us very clearly the number of recursive calls we’re making.

And simply put, the time complexity is going to be `O(number of recursive calls * work per recursive call)`.

With this formula, we are now able to simplify dramatically into two components that we can more easily calculate.

First, let’s talk about the number of recursive calls.

How do we estimate the total number of recursive calls without drawing out the whole tree? Well if we wanted to compute the number of nodes in a tree, we can look at the height of the tree and the branching factor.

The height of the tree is how deep our recursion goes.

if you keep recursively calling f\(n-1\) and your base case is when n == 0, then our depth is going to be O\(n\), since we keep decrementing until n reaches 0. If we have multiple different recursive calls, we just consider whatever the maximum depth is \(remember that Big Oh is an upper bound\).

The branching factor is the maximum number of child nodes any parent has in a tree. If we have a binary tree, the branching factor will be 2.

To find the branching factor of our recursive tree, we simply need to look at the maximum number of recursive calls. In our Fibonacci function, we call fibonacci\(n-1\) and fibonacci\(n-2\) every time, which gives us a branching factor of 2.

```text
int f(n) {
   if (n == 0) return 0;
 
   int sum = 0;
   for (int i = 0; i < n; i++) {
       sum += f(n-i);
   }
 
   return sum;
}
```

What would be the branching factor here?

It seems hard as the branching factor depends on `n`. But remember, we only need the worst case.

In this case, the worst case is `n`.

Now we have the branching factor and height of our recursive tree, we can use these to calculate the time complexity of our recursive function using this heuristic:

$$number\\_of\\_nodes = O\(branching\\_factor^{depth\\_of\\_recursion}\)$$

Knowing the number of nodes, we get that our total time complexity is:

$$number\\_of\\_nodes = O\(branching\\_factor^{depth\\_of\\_recursion}\*work\\_per\\_recursive\\_call\)$$

Work per recursive call is simply the amount of work that we’re doing in our function other than when we call it recursively. If we have any sort of for loop, such as in the example above, our work per recursive call will be proportional to that loop, or O\(n\) in this case.

That gives us a time complexity of $O\(n^n\*n\)$ for the function above.

### Space Complexity

Recursive space complexity is a bit easier for us to compute, but is also not exactly trivial.

The space does not depend on the branching factor, only on the height and then amount of space used per recursive call.

When we think about this for a minute, it makes sense. The branching factor leads to multiple different paths through our recursive tree. We have to consider each of these separately for the time complexity because time is additive. There is no way to reuse time.

Space, however, can be reused. Each time we recurse down, we will be using more and more space. However, once we return from our recursive function, we clear up space that can be reused for the next path.

This gives us a formula for our space complexity of simply:

$$O\(depth\\_of\\_recursion \* space\\_per\\_recursive\\_call\)$$

It is, however, important to remember that recursion does actually use up space, since that is something that many people often tend to forget.

## How to Approach

Recursive solutions, by definition, are built off of solutions to subproblems. Many times, this will mean simply to compute F\(n\) by adding something, removing something, or otherwise changing the solution for F\(n-1\).

In other cases, you might solve the problem for the first half of the data set, then the second half, and then merge those results.

Three of the most common approaches to dividing a problem into subproblems are:

### Bottom Up Approach

The bottom-up approach is often the must intuitive. We start with knowing how to solve the problem for a simple case, like a list with only one element. Then we figure out how to solve the problem for two elements, then for three elements and so on.

The key here is to think about how you can _build_ the solution for one case off of the previous case \(or multiple previous cases\).

### Top Down Approach

The top down approach can be more complex since it's less concrete. But sometimes, it's the best way to think about the problem.

In these problems, we think about how we can divide the problem for case N into subproblems.

Be careful of overlap between cases.

### Half and Half

Divide the dataset in half.

Binary search works with a half and half approach. When we look for an element in an sorted array, we first figure out which half of the array contains the value. Then we recurse and search for it in that half.

Merge sort is also a half and half approach.

## Recursion Relation

There are two important things that one needs to figure out before implementing a recursive function:

* `recurrence relation`: the relationship between the result of a problem and the result of its subproblems.
* `base case`: the case where one can compute the answer directly without any further recursion calls. Sometimes, the base cases are also called _bottom cases_, since they are often the cases where the problem has been reduced to the minimal scale, the bottom, if we consider that dividing the problem into subproblems is in a top-down manner.

Once we figure out the above two elements, to implement a recursive function we simply call the function itself according to the recurrence relation until we reach the base case.

To explain the above points, let's look at a classic problem, Pascal's Triangle:

Pascal's triangle are a series of numbers arranged in the shape of triangle. In Pascal's triangle, the leftmost and the rightmost numbers of each row are always 1. For the rest, each number is the sum of the two numbers directly above it in the previous row.

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b51cce56-3073-4a0c-99ab-547991fae4f5/PascalTriangleAnimated2.gif](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b51cce56-3073-4a0c-99ab-547991fae4f5/PascalTriangleAnimated2.gif)

Given the above definition, one is asked to generate the Pascal's Triangle up to a certain number of rows.

### Recurrence Relation of Pascal's Triangle

Let's start with the recurrence relation within the Pascal's Triangle.

First of all, we define a function f\(i,j\) which returns the number in the Pascal's Triangle in the `i-th` row and `j-th` column.

We then can represent the recurrence relation with the following formula:

$$f\(i, j\) = f\(i - 1, j - 1\) + f\(i - 1, j\)$$

## The 6 Core Recursive Patterns

[https://www.youtube.com/watch?v=BibDrTCGXRM](https://www.youtube.com/watch?v=BibDrTCGXRM)

If you understand each of these patterns and how to code them, then you can apply these concepts to almost any recursive problems that might come up in your interview. These 6 patterns are Iteration, Subproblems, Selection, Ordering, Divide & Conquer, and Depth First Search. For the remainder of this section, we will go into each in more detail.

### Iteration

As you hopefully know, any problem that can be solved recursively can also be solved iteratively and vice versa. This is a fundamental concept behind functional languages, where you use recursion to do everything; there are no loops.

For example, consider the problem of printing a linked list in reverse order. There are plenty of approaches we can take for this problem, but recursion is uniquely concise:

```text
void printReverse(Node n) {
   if (n == null) return;
   printReverse(n.next);
   print(n.val);
}
```

For iteration, we simply make our recursive call on the remainder of our inputs, either by passing in the next node \(as we did above\) or by incrementing some index. While this doesn’t come up too often, this is one of the simplest applications of recursion.

### Subproblems

* Breaking down a problem into subproblems

With all that being said, there are some problems that just lend themselves to being broken down into subproblems.

One example of this is the Fibonacci problem that we’ve talked about earlier in this post. In that case, even the mathematical definition of a Fibonacci sequence is recursive.

Another problem that frequently comes up is the Towers of Hanoi problem. In this case, we can simply break down our problem by considering the subproblem of moving the top n-1 disks. If we can move the top n-1 disks, we just move all of them to the middle pin, move our bottom disk to the destination pin, and then move the above disks again over to the destination pin. This works because all of the disks above our bottom pin are not affected by any pins below them.

In problems like this, you have to look for those subproblems with which to break up the problem. However, there aren’t too many problems in this category, since most can be more explicitly solved with one of the following patterns.

### Selection

This is my favorite pattern to test people on because it is one of the most common patterns to come up in recursion \(and dynamic programming\). In this pattern, we are simply finding all of the combinations of our input that match a certain criteria.

Consider for example the 0-1 Knapsack Problem. In this problem, we have a series of items that have weights and values. We want to figure out what the maximum value is that we can achieve while remaining under some fixed weight.

Many people recognize this as a dynamic programming problem, since it’s a classic example, but let’s look at it from a recursive standpoint.

What would be a brute force solution to this problem? Well we can easily validate for a given combination of items whether it is under the maximum weight, and we can also easily compute the weight for any combination. That means if we could just generate all the different combinations, we could figure out the optimal answer.

Figuring out all the combinations is the core of a selection problem. I like the term “selection” because the way our code works is to simply include/exclude, or “select”, each item in our list.

The brute force code to generate all combinations might look something like this \(this is simplified, but you get the idea\):

```text
List<List<Integer>> combinations(int[] n) {
   List<List<Integer>> results = new LinkedList();
   combinations(n, 0, results, new LinkedList<Integer>());
   return results;
}
 
void combinations(int[] n, int i, List<List<Integer>> results, List<Integer> path) {
   if (i == n.length) {
       results.add(path);
       return;
   }
 
   List<Integer> pathWithCurrent = new LinkedList(path);
   pathWithCurrent.add(n[i]);
 
   // Find all the combinations that exclude the current item
   combinations(n, i+1, results, path);
 
   // Find all the combinations that include the current item
   combinations(n, i+1, results, pathWithCurrent);
}
```

Once we understand this basic pattern, we can start to make optimizations. In many cases, we may actually be able to filter out some combinations prematurely. For example, in the Knapsack problem, we can limit our recursion to only consider combinations of items that stay below the prescribed weight.

If you spend the majority of your time on any one pattern, it should be this one. It comes up so frequently in so many different forms. Some good problems to get your started are 0-1 Knapsack, Word Break, and N Queens.

### Ordering

This pattern is the permutation to Selection’s combination. Essentially here we’re looking at any case in which we want to consider different orderings of our values. The most straightforward problem here is just to figure out all of the permutations of a given set of elements, although just like with selection, we may add in additional restrictions.

Some examples of problems that fall under this category are Bogosort \(sorting a list of items by generating all permutations and determining which is sorted\), finding all numbers that can be made from a set of digits that match a certain property, determine all palindromic strings that can be made from a set of characters, and more.

In its most simple form, this is one way that we can brute force generate all permutations of a list. You can also see an alternative approach here:

```text
List<List<Integer>> permutations(Set<Integer> n) {
   List<List<Integer>> results = new LinkedList();
   permutations(n, results, new LinkedList<Integer>());
   return results;
}
 
void permutations(Set<Integer> n, List<List<Integer>> results, List<Integer> path) {
   if (n.isEmpty()) {
       results.add(path);
       return;
   }
 
   for (int i : n) {
       // For now ignore concurrent modification issue
       n.remove(i);
       List<Integer> pathWithCurrent = new LinkedList(path);
       pathWithCurrent.add(i);
       permutations(n, results, pathWithCurrent);
       n.add(i);
   }
}
```

As you can hopefully see, there is a lot of similarity between this solution and the combinations solution above. By understanding these two patterns and their variants, you can cover a huge number of the different possible recursive problems you might be asked in your interview.

### Divide and Conquer

If you know about some of the common applications of recursion, you probably saw this one coming. Divide and conquer is the backbone to how we use techniques such as mergesort, binary search, depth first search, and more. In this technique, we attempt to break the problem space in half, solve each half separately, and then come back together.

Most frequently, this pattern is used as part of common algorithms that you should already know, such as the one I mentioned above, but there are a handful of problems for which this can be valuable.

For example, consider trying to determine all of the unique binary trees that we can generate from a set of numbers. If you pick a root node, you simply need to generate all of the possible variations of a left and right subtree.

Consider trying to find the maximum and minimum value of a list using the minimum number of comparisons. One way that we can do this is by splitting the list repeatedly, much the same as how we would do mergesort.

This technique generally applies to tree and sorting/searching problems where we will be splitting the problem space and then recombining the results.

There is also a slightly different case in which D&C is very useful: Trying to find all of the ways to group a set. Imagine, for example, that you have a mathematical function. You want to determine all of the different ways that you can group the arguments. This can be done by recursively trying splitting your formula at every different point. Here is an example of what this code might look like. It uses a string, but demonstrates the same concept:

```text
List<String> parentheses(String s) {
   if (s.length() == 1) {
       List<String> result = new LinkedList<String>();
       result.add(s);
       return result;
   }
 
   List<String> results = new LinkedList<String>();
 
   for (int i = 1; i < s.length(); i++) {
       List<String> left = parentheses(s.substring(0, i));
       List<String> right = parentheses(s.substring(i, s.length()));
           
       for (String s1 : left) {
           for (String s2 : right) {\\
               results.add("(" + s1 + s2 + ")");
           }
       }
   }
       
   return results;
}
```

In this example, we take the string and we try finding every different midpoint. For example “abcd” becomes “\(a\)\(bcd\)”, “\(ab\)\(cd\)”, and “\(abc\)\(d\)”. Then we recursively apply this to each of the halves of the string.

### Depth First Search

Depth first search is our final pattern that our recursive functions can fall under. It’s also one that we’ll likely find ourselves using a lot. That’s because DFS \(and BFS\) are used extensively whenever we are doing anything with trees or graphs.

In terms of the details of trees and graphs, I’m not going to go in depth here. There is way too much to cover so I’m going to leave them to their own study guides.

The main important thing with DFS is to understand how not only to search for a node in a tree or graph but also how to actually find the path itself. If you can’t do that, you’re severely limiting what you can actually do.

Here is what the code might look like to find the path to a specific node in a tree:

```text
List<Node> pathToNode(Node root, int val) {
   if (root == null) return null;
   if (root.value == val) {
       List<Node> toReturn = new LinkedList<Node>();
       toReturn.add(root);
       return toReturn;
   }
       
   List<Node> left = pathToNode(root.left, val);
   if (left != null) {
       left.add(0, root);
       return left;
   }
      
   List<Node> right = pathToNode(root.right, val);
   if (right != null) {
       right.add(0, root);
       return right;
   }
 
   return null;
}
```

And there’s not that much more to it than that. In most cases, you will use depth first search as part of a larger problem, rather than actually having to modify it in any significant way. Therefore the most important thing is understanding the core of how DFS works.

With these 6 recursive patterns, you will be able to solve almost any recursive problem that you could see in your interview. The key is to look for those patterns in the problems that you are solving. If you see the pattern, use it. If not, try something else. Different patterns will work better for different people, so do what feels right to you.

## Example

[344. Reverse String](https://www.notion.so/344-Reverse-String-513a1698572a4906b4772d04157a736b)

Print a string in reverse order.

You can easily solve this problem iteratively, i.e. looping through the string starting from its last character. But how about solving it recursively?

First, we can define the desired function as `printReverse(str[0...n-1])`, where `str[0]` represents the first character in the string. Then we can accomplish the given task in two steps:

1. `printReverse(str[1...n-1])`: print the substring `str[1...n-1]` in reverse order.
2. `print(str[0])`: print the first character in the string.

Notice that we call the function itself in the first step, which by definition makes the function recursive.

Here is the code snippet:

```text
private static void printReverse(char [] str) {
  helper(0, str);
}

private static void helper(int index, char [] str) {
  if (str == null || index >= str.length) {
    return;
  }
  helper(index + 1, str);
  System.out.print(str[index]);
}
```

