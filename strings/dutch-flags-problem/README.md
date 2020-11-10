# Dutch Flags Problem

{% embed url="https://en.wikipedia.org/wiki/Dutch\_national\_flag\_problem" %}

The **Dutch national flag problem** [\[1\]](https://en.wikipedia.org/wiki/Dutch_national_flag_problem#cite_note-monash-1) is a [computer science](https://en.wikipedia.org/wiki/Computer_science) programming problem proposed by [Edsger Dijkstra](https://en.wikipedia.org/wiki/Edsger_Dijkstra).[\[2\]](https://en.wikipedia.org/wiki/Dutch_national_flag_problem#cite_note-:0-2) The [flag of the Netherlands](https://en.wikipedia.org/wiki/Flag_of_the_Netherlands) consists of three colors: red, white and blue. Given balls of these three colors arranged randomly in a line \(it does not matter how many balls there are\), the task is to arrange them such that all balls of the same color are together and their collective color groups are in the correct order.

The solution to this problem is of interest for designing [sorting algorithms](https://en.wikipedia.org/wiki/Sorting_algorithm); in particular, variants of the [quicksort](https://en.wikipedia.org/wiki/Quicksort) algorithm that must be [robust to repeated elements](https://en.wikipedia.org/wiki/Quicksort#Repeated_elements) may use a three-way partitioning function that groups items less than a given key \(red\), equal to the key \(white\) and greater than the key \(blue\). Several solutions exist that have varying performance characteristics, tailored to sorting arrays with either small or large numbers of repeated elements

