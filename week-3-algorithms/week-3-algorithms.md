# [Lecture 3](https://cs50.harvard.edu/x/weeks/3)

- There are many ways to solve a problem correct - algorithms
- However the design of solution can impact cost of solving a problem in terms of limited resources - time, storage, money, etc.
- An efficient algorithm is the one bringing down the cost of limited resource that cannot be compromised

### Searching
- As problem, we are given a set of values and are required to find a particular one
- Computers can access limited set of items at a time due to design constraints of memory
- Thus the location of required value is supposed to be found with operations and compute

*1. Linear Search - Checking each item available one by one and comparing with required value till it is found or end of set is reached*

*2. Binary Search - If the given set is sorted, divide it in half and compare for required value in middle. If according to sort order the required value is behind or in front ignore where it wouldn't be and repeat steps till value is found or end is reached.*

*Pseudo-coding such operations often help designing the program*

### Running Time
- Amount of time a algorithm takes to complete the task
- Often used to compare algorithms for consumed time in terms of required steps $n$ to execute
- To represent time in order of steps $n$, asymptotic notations are used such as - $O$ : Big O notation, and - $O(n)$: Big O of n, representing an upper bound
- When representing time in order of steps $n$, the focus is on dominant term influencing growth per step $n$ ignoring those that don't 
- Some algorithms may have different growth per step but eventually, they converge in terms of growth rate per step

### Structs
- User-defined custom data structure that associates each of it's instance with defined attributes encapsulated in its structure definition
- Instance declared as a variable with datatype
- `instance.attribute` helps accessing it's particular attribute

### Sorting
Done based on required order of values

*3. Selection Sort: Pass through whole set and order the set with least value on left till whole set is ordered least to largest*

*4. Bubble Sort: Pass through whole set comparing two items and swap the least of those to left and other to right till whole set is sorted*

### Recursion
- A recursive function is defined in terms of itself
- In mathematics it is dependent on itself
- In computer science it calls itself till a terminating condition is met called a base case
- Recursive cases divide the given problem so that solving till a base case is costing less and less computationally
- Each time a function calls itself it consumes more memory till a base case is reached

*5. Merge Sort: Reach base case of comparing two values and sort them, then merge the sorted entities and again sort per merge, eventually sorting the whole set*
