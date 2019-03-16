# Data Structures and Algorithms
## Introduction
Data structures and algorithms help you handle problems in a smart and efficient way.

It goes without a saying that they go hand in hand. For solving a problem with a given algorithm efficiently you need to put your data in a appropiate data structure that benefits the algorithm. Using a specific data structure will dictate which algorithms you can use.

This topic is very rich and can go very deep. Understanding the core data structures and algorithms helps you to understand what tools are out there, the more specific your challenge becomes that you try to solve, the more specific a certain data structure and algorithm gets.

The efficiency of your algorithm strongly depends also on the size of your data set that you need to processl. A certain algorithm might perform better on a small set of data, but much worse on a big data set, therefore it is commong that `sort()` functions first probe the size of your data set and based on that might choose another algorithm that is known ot perform better for given data set size.

It's also worth to take in consideration on how your typical data set will be structured or ordered. Statiscally a data set can be faily ordered already, or it can be a given that your data set is almost always sorted in a certain way. This can have an impact on the algorithm you choose.

To be able to decide what is an appropiate algorithm, you must understand the performance (time complexity) expressed in the big O notation. The performance can greatly vary based on the size of the data set and how the typical sample data set that you provide will look like (partialy ordered, always descending, etc...).

As you learn new algorithms, you will find the performance for each of the differen characteristics.

## The Big O notation
[The Big O notation explained](big-o.md)

## Data Structures

Data Structures often differ in their efficiency for each sorting algorithm and their basic operations (like read, insert, remove, update and search).

![big-0-2](assets/big-o-2.png)

* [Array](data-structures/array.md)
* [Stack](data-structures/stack.md)
* [Queue](data-structures/queue.md)
* [Singly-Linked List](data-structures/singly-linked-list.md)
* [Doubly-Linked List](data-structures/doubly-linked-list.md)
* [Hash Table](data-structures/hash-table.md)
* [Binary Tree](data-structures/binary-tree.md)

## Algorithms

![big-0-3](assets/big-o-3.png)

* [Binary Search](algorithms/binary-search.md)
* [Linear Search](algorithms/linear-search.md)
* [Bubble Sort](algorithms/bibble-sort.md)
* [Selection Sort](algorithms/selection-sort.md)
* [Insertion Sort](algorithms/insertion-sort.md)
* [Quicksort](algorithms/quick-sort.md)
* [Quickselect](algorithms/quick-select.md)
* [Graph Algorithms](algorithms/graph.md)

## Other topics

* [NP Completeness](np-completeness.md)