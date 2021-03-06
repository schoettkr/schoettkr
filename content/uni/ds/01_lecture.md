+++
title = "Datastructures - Lecture 01"
author = ["eo shiru"]
date = 2019-04-04
lastmod = 2019-04-07T20:19:22+02:00
tags = ["uni", "datastructures"]
draft = false
+++

In the first lectures of the datastructures we'll repeat a few things that were already covered in the Algorithm & Programming Lecture so you may want to refer those blog posts as well. After all both courses belong to the same module.


## Computational Effort & Complexity {#computational-effort-and-complexity}

To compare datastructures and algorithms in regards to efficiency we need a way to measure the "cost" / computational effort. This is done by counting the required computing "steps" (Rechenschritte). A computation step is generally an elementary operation like an arithmetic operation or accessing an memory adress. More complex operations may in cases also be seen as one computational step. Because it is known how long a step takes we also speak about _computation time_. The computation time does not only depends on the concrete algorithm or the used datastructure but also on the distribution of data. That's why we distinguish between the best, worst and average case. However the average computational time can only be stated if there's also a probality distribution which is known.<br />
Let's compare the computing steps for two functions that compute the sum up to a certain number:

```C++
int sum1(int n) {
  int s = 0;
  for (int i = 1; i <= n; i++)
    s = s + i;
  return s;
}

int sum2(int n) {
  int s;
  s = n * (n+1) / 2;
  return s;
}
```

The function `sum1` has 4n+3 (`n+2` assignments, `n` increments, `n+1` comparisons, `n` additions) steps while `sum2` executes 4 operations (1 assignment, 3 basic mathematical operations) which are independant of `n`.<br />
Since we do not want to determine the computational time for a concrete set of data we aim to find a function which determines the computational time in regards to the amount of elements _n_ in a data set. Furthermore the concrete function is kind of irrelevant as well. What we are really interested in, is the behaviour of this function, especially when the input data set and therefore _n_ grows (asymptotic complexity). Doing so we can neglect/ignore constants and implementation details which are irrelevant to the function growth.


### O-Notation {#o-notation}

O-Notation is used to express the efficiency of an algorithm separately from the computer architecture, programming language and compiler etc. The efficiency is usually judged in regards to time as well as space. There also posts from the algorithm lecture that cover O-Notation on here, so you might want to check those out. Here are common typical complexities:
![](/knowledge-database/images/common-complexities.png)


## Datastructure - Array {#datastructure-array}

An array is a linear arrangement of elements of the same data type, which gets stored in a continuous block of memory. Accessing an element at a certain index is an operation which requires constant time O(1).


### Operations on Arrays {#operations-on-arrays}

-   accessing each element has a complexity of O(n)
-   searching/counting elements has a complexity of O(n)

**Inserting an element into an array** requires that all elements from the position of insertion _p_ have to be pushed back by one position before the new element can be set to position _p_. One problem in this case however is what happens with the last element in the array? If the element is already at full capacity we loose the last element. One way to avoid this would be to create an overflow buffer (Ueberlaufpuffer) by creating a larger array in advance and tracking the real size of the array (count of elements) in a separate variable. Disadvantages of this are however that first of all storage is wasted and second of all there still would be no guarantee that the array fills up to its capacity at some point on time. In the bad case the insertion of a element into an array would require n Operations &rarr; complexity of O(n)  because all n elements would have to be moved.<br />
**Deleting an element from an array** requires that all elements from the position of deletion _p_ are moved/shifted forward by one position. Here's the problem that that there's an empty field at the end of array left over. Analogously to the insertion we could track the actual count of elements via a separate variable. This results however in wasting storage aswell and also includes the linear time complexity of O(n) in the worst case where every element has to be shifted.

So arrays are not really suited for storing data where elements often have to be added/deleted. It is also not good optimal when it is unsorted and elements have to be searched for often times.


#### Example of array usage: Sieve of Eratosthenes {#example-of-array-usage-sieve-of-eratosthenes}

The Sieve of Eratosthenes is an algorithm to determine prime numbers. An array can be used to implement this algorithm:

1.  Write down (store) all natural numbers from 2 up to an arbitrary maximum number `m`. First all numbers are unmarked.
2.  Repeat the following:
    -   take the smallest unmarked number _P_ which has not been taken already (P is always a prime number btw)
    -   is \\(P^2 > m\\) than the algorithms stops and all unnmarked numbers are the prime numbers from 2 to m
    -   mark all multiples of P, starting at \\(P^2\\)

```C++
void sieve_of_eratosthenes(int m) {
  int arr[m] = {0};

  for (int i = 2; i < m; i++) {
    for (int j = i*i; j < m; j += i) {
      arr[j-1] = 1;
    }
  }

  for (int i = 1; i < m; i++) {
    if (!arr[i-1])
      cout << i << "  ";
  }
}
sieve_of_eratosthenes(50);
```

```text
1  2  3  5  7  11  13  17  19  23  29  31  37  41  43  47
```


#### Example of array usage: Binary Search {#example-of-array-usage-binary-search}

When the elements of an array are sorted we can speed up the search process significantly:

1.  Look at the whole array
2.  Compare the middle element with the search value
    -   is the search value smaller than the middle element, continue looking at the part of the array that is to the left of the middle element
    -   is the search value larger than the middle element, continue looking at the part of the array that is to the right of the middle element
3.  Go to step 2 until the values match or the size of the part of the array to look at is 0

Because the array is halved in each iteration the time complexity is only O(log n).
