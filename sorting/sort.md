## Why sort?
Whenever you interact with a web or mobile application, you can sort a large set of data by some property.
1. It helps make a set of data more readable
1. It makes it easier to implement **search algorithms** in order to find or retrieve an item from the entire dataset.
e.g. [Amazon](https://docs.aws.amazon.com/AWSECommerceService/latest/DG/SortingbyPopularityPriceorCondition.html) lets users to sort items by Price,Popularity, Condition

## Sorting Algorithms
An **algorithm** is just fancy term for a set of instructions of what a program should do, and how it should do it. In other words: it’s nothing more than a manual for your code. That’s it. (Really!) Some of the most-referenced algorithms in the world of software are generally a subset of sorting algorithms, or algorithms that provide a set of instructions for how a program or system should go about organizing a set of data.
### Types of sorting algorithms
There are many types. We will focus on **selection sort** and **quick sort** as per the Study Design.
### You should be able to
* explain how they work
* compare advantages and disadvantages using time complexity (Big O)
* interpret pseudocode
* implement the algorithms in JS
### Key words
* *Pass* : each time array is cycled through. You need to pay attention to the number of passes before the sorting is completed
* *Comparison* : each time two array elements are compared
* *Swap* : each time two array elements are swapped. You can think about how to implement swapping two array elements.
### Selection Sort
A selection sort algorithm sorts through a list of items by iterating through a list of elements, finding the smallest one, and putting it aside into a sorted list. It continues to sort by finding the smallest unsorted element, and adding it to the sorted list.

* Watch the video below to see how it works in action.[Very cool Selection sort video](https://youtu.be/AgFR0kO05RM)
Remember, however, that even though we, as humans can look at the list and immediately know that 1 is the smallest number: computers can’t do that! They have to iterate through in the entire dataset in order to figure out which number is the smallest or the largest.

* Read the pseudocode: ![selection sort](https://i.stack.imgur.com/lFGCb.jpg)
So, our pseudo-coded algorithm started off by just assuming that the first item was the smallest number in the list. Then, we iterated through and found the actual smallest number.
* Implement it in JS. You will need to use nested for loops. i is the pointer used to iterate over each element in the array. i is the pointer to loop through the unordered list. You also need a pointer to keep track of the index of the smallest element. Create a test array to test your code.
* Time complexity: Imagine that we passed in [33,2,52,106,73,300,19,12,1,60] — ten numbers. We’d make 9 comparisons on the first pass! And then we’d make 8 on the second, and 7 on the the third pass. If there are n numbers, the total number of comparisons made will be n + (n-1) + (n-2) +(n-3) + ... + 3 + 2 + 1 = n(n-1)/2. Therefore the time complexity is O(n^2).
* PROS: 
    * Simple to understand and implement 
    * Good to use when sorting small numbers of elements
    * In place sorting – no additional temp storage
* CON: 
    * Inefficient for large data sets
    * Large number of processing steps (n2 steps for n elements)


### Quick Sort
**“Make it work, make it right, make it fast”** by Kent Beck. At some point, once we’ve made it work and made it right, you should ask yourself: can I make it fast? Can I make it better?

The basic idea is to find a **“pivot”** item in the array to compare all other items against, then shift items such that all of the items before the pivot are less than the pivot value and all the items after the pivot are greater than the pivot value. After that, recursively perform the same operation on the items before and after the pivot. There are many different algorithms to achieve a quicksort and this post explores just one of them.
![](https://images.deepai.org/glossary-terms/a5228ea07c794b468efd1b7f758b9ead/Quicksort.png)

### ways to choose the pivot
* Always pick first element as pivot
* Always pick last element as pivot
* Pick a random element as pivot
* Pick median as pivot
### Steps
1. Find a “pivot” item in the array. This item is the basis for comparison for a single round.
1. Start a pointer (the left pointer) at the first item in the array.
1. Start a pointer (the right pointer) at the last item in the array.
1. While the value at the left pointer in the array is less than the pivot value, move the left pointer to the right (add 1). Continue until the value at the left pointer is greater than or equal to the pivot value.
1. While the value at the right pointer in the array is greater than the pivot value, move the right pointer to the left (subtract 1). Continue until the value at the right pointer is less than or equal to the pivot value.
1. If the left pointer is less than or equal to the right pointer, then swap the values at these locations in the array.
1. Move the left pointer to the right by one and the right pointer to the left by one.
1. If the left pointer and right pointer don’t meet, go to step 1.
![quicksort](https://humanwhocodes.com/images/wp-content/uploads/2012/11/quicksort_partition1.png)

### Implement in JS. Three functions are needed. Partition, Swap and quickSort which call itself recursively. You need to use while loop this case.

* PROS: 
    * Highly efficient for large sized data sets (faster than selection sort)
    * Fast
    * Able to deal with huge lists
    * In place – so no additional storage
* CON: 
    * More complex algorithm and code
    * If list is nearly sorted – than bubble sort is more efficient
