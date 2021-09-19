# Computational Complexity
In computer science, the computational complexity or simply complexity of an algorithm is the amount of resources required to run it. Particular focus is given to time and memory requirements. The complexity of a problem is the complexity of the best algorithms that allow solving the problem.

### Time
The resource that is most commonly considered is **time**. When "complexity" is used without qualification, this generally means time complexity.

The usual units of time (seconds, minutes etc.) are not used in complexity theory because they are too dependent on the choice of a specific computer and on the evolution of technology. For instance, a computer today can execute an algorithm significantly faster than a computer from the 1960s; however, this is not an intrinsic feature of the algorithm but rather a consequence of technological advances in computer hardware. Complexity theory seeks to quantify the intrinsic time requirements of algorithms, that is, the basic time constraints an algorithm would place on any computer. This is achieved by counting the number of elementary operations that are executed during the computation. These operations are assumed to take constant time (that is, not affected by the size of the input) on a given machine, and are often called steps.

| Name | Running time | Example algorithm |
| -- | -- | -- |
| Constant time | O(1) | Finding the median value in a sorted array of numbers |
| Logarithmic time | O(log n) | binary search and height of balanced binary trees |
| Polylogarithmic time | O((log2 n)^k) | - |
| Liniar time | O(n) | Finding the smallest or largest item in an unsorted array, linear search |
| Quadratic time | O(n^2) | Bubble sort, Insertion sort |
| Polynomial time | O(n^k) | - |
| Exponential time | O(2^n) | Solving the traveling salesman problem using dynamic programming |
| Factorial time | O(n!) | Solving the traveling salesman problem via brute-force search |

[Read more about time complexity](https://en.wikipedia.org/wiki/Time_complexity)

### Space
Another important resource is the size of computer memory that is needed for running algorithms. The space complexity estimates the quantity of memory required by the algorithm to store the input data, the final results and the intermediate results. As the time complexity, the space complexity is also estimated using "O" and "Omega" notation.

### Complexity as a function of input size
Only time complexity is considered in this section, but everything applies (with slight modifications) to the complexity with respect to other resources 

It is impossible to count the number of steps of an algorithm on all possible inputs. As the complexity generally increases with the size of the input, the complexity is typically expressed as a **function of the size n (in bits) of the input**, and therefore, **the complexity is a function of n**. However, the complexity of an algorithm may vary dramatically for different inputs of the same size. Therefore, several complexity functions are commonly used.

The worst-case complexity is the maximum of the complexity over all inputs of size n, and the average-case complexity is the average of the complexity over all inputs of size n (this makes sense, as the number of possible inputs of a given size is finite). Generally, when "complexity" is used without being further specified, this is the worst-case time complexity that is considered.

### Efficiency of a function
Measuring effciency:
* **Empirical analysis** - determines exact running times for a sample of specific inputs, but cannot predict algorithm performance on all inputs.
* **Asymptotic analysis** - mathematical analysis that captures efficiency aspects for all possible inputs but cannot provide execution times.
Function run time is studied in direct relation to data input size. We focus on asymptotic analysis, and illustrate it using empirical data.

* **Best case (BC)**, for the data set leading to minimum running time 
* **Worst case (WC)**, for the data set leading to maximum running time
* **Average case (AC)**, average running time of the algorithm 

# "Big-O" notation
**O(n) notation provides the asymptotic upper bound.** \
We say that T(n) belongs to O(f(n)) if limit(n->infinite) of T(n)/f(n) is 0 or a constant, but not infinite.

If T(n) = 13 * n^3 + 42 * n^2 + 2 * n * log2(n) + 3 * sqrt(n), and f(n) = n^3, then limit(n->infinite) of T(n)/f(n) = 13. So, we say that T(n) belongs to O(n^3). 

The O notation is good for putting an upper bound on a function. We notice that if T(n) belongs to O(n^3), it also belongs to O(n^4), O(n^5), since the limit will then go to 0.

# "Omega" notation
**The Ω notation is used for establishing a lower bound on an algorithm's complexity.** \
We say that T(n) belongs to Ω(f(n)) if limit(n->infinite) of T(n)/f(n) is a constant or infinite, but not 0.

If T(n) = 13 * n^3 + 42 * n^2 + 2 * n * log2(n) + 3 * sqrt(n), and f(n) = n^3, then limit(n->infinite) of T(n)/f(n) = 13. So, we say that T(n) belongs to Ω(n^3). 

# "Theta" notation
**The Θ notation is used for establishing an exact bound on an algorithm's complexity.** \
We say that T(n) belongs to Θ(f(n)) if limit(n->infinite) of T(n)/f(n) is a constant (but not infinite or 0).

If T(n) = 13 * n^3 + 42 * n^2 + 2 * n * log2(n) + 3 * sqrt(n), and f(n) = n^3, then limit(n->infinite) of T(n)/f(n) = 13. So, we say that T(n) belongs to Θ(n^3). This can also be deduced from "T(n) belongs to O(n^3)" and "T(n) belongs to Ω(n^3)".

The run time of an algorithm is Θ(f(n)) if and only if its worst case run time is O(f(n)) and best case run time is Ω(f(n)).

# In plain words
Big O (O()) describes the upper bound of the complexity. \
Omega (Ω()) describes the lower bound of the complexity. \
Theta (Θ()) describes the exact bound of the complexity. \
Little O (o()) describes the upper bound excluding the exact bound.

[Read more about notations](https://www.freecodecamp.org/news/big-o-notation-why-it-matters-and-why-it-doesnt-1674cfa8a23c/)

