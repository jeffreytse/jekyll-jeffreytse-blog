---
layout: post
title: The handbook of algorithm
author: Jeffrey Tse
categories: computer
tags:
  - computer
  - software
  - note
---

Here is a handbook to help us better understanding algorithm.

Program = Data Structure (DS) + Algorithm

## Algorithm Analysis

It's very common for programmers to compare their programs or algorithms
with one another. When two programs solve the same problem but look
different, is one program better than the other?

### Analysis Dimensions

- Time
- Space

### Analysis Method

We use the "Big-O Notation" to expression complexsity of a algorithm.

Here is some common algorithm complexities:

- O(1)
- O(log n)
- O(n)
- O(n log n)
- O(n^2)
- O(2^n)
- O(n!)

Big-O Complexity Chart

![Big-O Complexity Chart](https://user-images.githubusercontent.com/9413601/145718294-f51966dc-bc29-43be-b490-4716b28095c4.png)


## Data Structure

- Linear
  - List or Array
  - Queue
  - Deque
  - Stack
- Non-linear
  - Tree
  - Graph


## Algorithm Design

### Algorithm Strategy

Algorithm strategy can also be called Algorithm Paradigm, it's a general
method or template for designing and solving a class of problems. Each
algorithm strategy has its own design ideas and problem-solving steps.

- Brute Force Enumeration
  - Classic Applications
    - Selection Sort
    - Bubble Sort
    - Linear Search
- Greedy Algorithm
  - Features
    - It may not find the optimal solution
  - Classic Applications
    - Making change using the fewest coins
- Divide and Conquer
  - Classic Problems
    - Quick Sort
    - Merge Sort
    - Binary Search
- Backtracking
  - Classic Problems
    - Depth First Search (DFS)
    - Breadth First Search (BFS)
- Dynamic Programming (DP)
  - Features
    - Optimal Substructure
    - Overlapping Sub-Problem
  - Approaches
    - Top-down Approach
    - Down-Top Approach
  - Classic Problems
    - Fibonacci Sequence
    - Making change using the fewest coins

### Algorithm Implementation

Recursion is one implement of the algorithm strategies


## References

- [Algorithm Analysis](https://runestone.academy/runestone/books/published/pythonds3/AlgorithmAnalysis/toctree.html)
- [Know Thy Complexities!](https://www.bigocheatsheet.com/)
