[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-718a45dd9cf7e7f842a935f5ebbe5719a5e09af4491e668f4dbf3b35d5cca122.svg)](https://classroom.github.com/online_ide?assignment_repo_id=12129032&assignment_repo_type=AssignmentRepo)
# Quicksort Pivots

in the lectures I only briefly mentioned strategies for determining a good pivot
for quicksort. The implementation on the slides simply picks the leftmost
element in the part of the array that we consider as a pivot. I also mentioned a
few other ways of picking a good pivot, e.g. randomly.

Median-of-three is also a good way of picking a pivot -- inspect the first,
middle, and last elements of the part of the array under consideration and
choose the median value. Using the probabilities for picking a pivot in a
particular part of the array (in the same way as we did on slide 34), argue
whether this method is more or less (or equally) likely to pick a good pivot
compared to simply choosing the first element. Assume that all permutations are
equally likely, i.e. the input array is ordered randomly.

Your answer must derive probabilities for choosing a good pivot and
quantitatively reason with them.

Add your answer to this markdown file. [This
page](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/writing-mathematical-expressions)
might help with the notation for mathematical expressions.

## Answer

The quicksort and randomized-quicksort procedures differ only in how they select pivot elements. However, they are the same in all other aspects.
Let's rename the elements in the array A as $Z_1, Z_2, ...., Z_n$ , with $Z_i$ being the ith smallest element. We define the set $Z_{ij} = Z_i, Z_{i+1}, ...., Z_j$ as the included each element between $Z_i$ and $Z_j$. $Z_{ij}$ has j-i+1 elements, if we choose the first, middle, and last element, the probability is $\frac{3}{j-i+1}$.

We can easily characterize the total number of comparisons performed by the algorithm by comparing each element with the pivot at most once.
X = $\displaystyle\sum_{i=1}^{n-1}\sum_{j=i+1}^{n} X_{ij}$

To obtain the solution, we need to take the expectation of both sides of the equation above.

E[X] = $E[\displaystyle\sum_{i=1}^{n-1}\sum_{j=i+1}^{n} X_{ij}]$

E[X] = $\displaystyle\sum_{i=1}^{n-1}\sum_{j=i+1}^{n}$ Pr { $Z_i$ is compared to $Z_j$ }

E[X] = $\displaystyle\sum_{i=1}^{n-1}\sum_{j=i+1}^{n}$ $\frac{3}{j-i+1}$

A change of variables: p=j-i

E[X] = $\displaystyle\sum_{i=1}^{n-1}\sum_{p=1}^{n-i}$ $\frac{3}{p+1}$ < $\displaystyle\sum_{i=1}^{n-1}\sum_{p=1}^{n}$ $\frac{3}{p}$

E[X] = $\displaystyle\sum_{i=1}^{n-1}$ $O(\lg{}n)$

E[X] = $O(n\lg{}n)$

Therefore, if we use randomized-quicksort, quicksort's expected running time is $O(n\lg{}n)$ when all element values differ.

#### The possibility of median-three-choose method to choose a good pivot

1/2 possible rate to choose a good pivot since 1/n*(3n/4-n/4) = 1/2

Assume any whole list as 1, and split the list into 4 parts. 1/4 to choose a pivot is from left(L), 1/4 and another 1/4 from center parts as good pivot(M), and the rest 1/4 is from right part(R).

Exploring all possible combines:

LLL $\frac{1}{4} * \frac{1}{4} * \frac{1}{4} = \frac{1}{64}$

LMR $\frac{1}{4} * \frac{2}{4} * \frac{1}{4} = \frac{2}{64}$

LMM $\frac{1}{4} * \frac{2}{4} * \frac{2}{4} = \frac{4}{64}$

LRR $\frac{1}{4} * \frac{1}{4} * \frac{1}{4} = \frac{1}{64}$

...

By adding all those possible combines to get 44/64 = 11/16 = 68.75%

Therefore, the total possibility of choosing a good pivot from the median-three-choose method is 68.75%.


// get help from TA and textbook: Introduce to algorithm p180-184
