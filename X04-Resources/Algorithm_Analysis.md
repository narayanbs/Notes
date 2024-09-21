##### Asymptotic Analysis
------------------

Suppose we want to compare the performance of two algorithms, the natural way 
would be to time them against an input and run them on the same computer. But 
it could be the case that the same algorithms could run at a different speed 
with another set of input, on a different computer etc. 
Is there a way to analyze the performance of algorithms without the overhead of 
hardware, input patterns etc?? 
It would be pointless to test against all the inputs and on different computers.

In asymptotic analysis we evaluate the performance of an algorithm in terms 
of input size i.e instead of measuring the actual running time, we analyze how 
the time (or space) taken by an algorithm increases with the input size.

for ex:  Suppose we have a sorted array and we need to search for an element. 
Lets consider linear and binary search algorithms,  In linear search, we 
compare each element until we reach the end. 
Worst case -> we would have compared all the n elements
In binary search, we divide the arrays and search in the half that is relevant, 
the comparison is less, 
worst case -> it takes logarithmic comparisons against the input

Let's assume that linear search is running on a fast computer and binary search 
on a slow computer, and let us represent  these input characteristics i.e 
computer hardware as constants. so assuming the constants representing overhead 
(hardware and i/p characteristics), is 0.2 for linear search  and 2.0 for 
binary search, we can represent the worst case comparisons as 0.2(n) for linear 
and 2log(n)

Let's analyze the running times against the input size: 

```

n       0.2n      2log(n)	
-----------------------------------
10     2sec		    1h
100    20sec		1.8h
10^6   ~55hr		5.5h
10^9   ~6.3 years	8.3h
```

It may be the case that for smaller arrays, linear could be faster, but binary 
search will always be faster as the input size grows.
Asymptotic Analysis is not perfect, but that’s the best way available for 
analyzing algorithms. 

Note: 
The overhead constants doesn't matter after a certain value of input size. So 
in asymptotic analysis we ignore overhead constants.
so if two algorithms run at 1000logn and 0.2logn, they are considered 
asymptotically same. 

##### Best case, average case and worst case
-----------------------------------------
for linear search, best case would be if the first element is what we need, so 
just 1 comparison
average case would be we look at time of finding each element, and not finding 
it too and average it.
worst case would be not finding the element so we would have had n 
comparisons.. 
The worst case analysis would always be the one that makes sense. 

##### Notation
----------
Analyzing running time against input sizes implies analyzing a function, where 
i/p is the size and o/p is the time. The result of  the analysis is represented 
by notations that indicate the asymptotic complexity of the algorithm. These 
include

`Big Omega`:  this is used to represent the lower bound of an algorithm. 
Meaning when we say the asymptotic complexity is Big-Omega(log(n)),
it means that the algorithm will take at least log(n) to produce the output.

`Big Oh` : this is used to represent the upper bound of an algorithm. When the 
complexity is `Big-Oh(log(n))`, then it means the algorithm
will take at most log(n) to produce the output.

`Big theta` : this is used to represent the exact asymptotic behavior. When the 
complexity is `Big-theta(log(n))`, it indicates that the
algorithm will perform within a lower and upper bound of log(n). 

##### Mathematically
--------------
`Big-Omega(g(n))` - For a given function g(n), we denote by Ω(g(n)) the set of 
functions.  
```bash
Ω(g(n)) = {f(n): there exist positive constants c and
                  n0 such that 0 <= c*g(n) <= f(n) for
                  all n >= n0}.
```

```bash
Big-Oh(g(n)) - For a given g(n), we denote O(g(n)) as the set of functions:

O(g(n)) = { f(n): there exist positive constants c and 
                  n0 such that 0 <= f(n) <= c*g(n) for 
                  all n >= n0}
```

```bash
Big-theta(g(n)) - For a given function g(n), we denote Θ(g(n)) is following 
set of functions.  

Θ(g(n)) = {f(n): there exist positive constants c1, c2 and n0 such 
                 that 0 <= c1*g(n) <= f(n) <= c2*g(n) for all n >= n0}
```


Note: 
Suppose we get the following expression when we are doing asymptotic analysis, 
3n^3 + 6n^2 + 6000
Dropping lower order terms is always fine because there will always be a 
number(n) after which n^3 overshadows n^2
irrespective of the constants involved. The effects of these lower order terms 
will be negligible on the complexity.

so analyzing 3n^3 + 6n^2 + 6000 means analyzing n^3


##### Analyzing Time Complexities 
-----------------------------

O(1): meaning constant time. Program Statements take a constant time. It is 
considered O(1).
Time complexity of a function (or set of statements) is considered as O(1) if 
it doesn’t contain loop, recursion, and 
call to any other non-constant time function. 

A loop or recursion that runs a constant number of times is also considered as 
O(1). For example, the following loop is O(1). 
```bash
   // Here c is a constant   
   for (int i = 1; i <= c; i++) {  
        // some O(1) expressions
   }
   
Note: c is a constant, not the size of the input n. No matter the size of the 
input, these take constant time. 
```

O(n): Time Complexity of a loop is considered as O(n) if the loop variables are 
incremented/decremented by a constant amount. 
For example following functions have O(n) time complexity. 
```bash
   // Here c is a positive integer constant   
   for (int i = 1; i <= n; i += c) {  
        // some O(1) expressions
   }

   for (int i = n; i > 0; i -= c) {
        // some O(1) expressions
   }
   
The amount of time taken depends on the size of the input linearly. 
```

O(n^c): Time complexity of nested loops is equal to the number of times the 
innermost loop is executed. For example, the following sample loops have O(n^2) 
time complexity . 
 
```bash
     for (int i = 1; i <=n; i += c) {
       for (int j = 1; j <=n; j += c) {
          // some O(1) expressions
       }
   }

   for (int i = n; i >= 0; i -= c) {
       for (int j = n; j >=0; j -= c) {
          // some O(1) expressions
   }
```

Time exponentially increases as more inner loops are added. 
   
O(Logn) Time Complexity of a loop is considered as O(Logn) if the loop 
variables are divided/multiplied by a constant amount. 

```bash

   for (int i = 1; i <=n; i *= c) {
       // some O(1) expressions
   }
   for (int i = n; i > 0; i /= c) {
       // some O(1) expressions
   }
```

For example, Binary Search(refer iterative implementation) has O(Logn) time 
complexity. 
Let us see mathematically how it is O(Log n). The series that we get in the 
first loop is
`1, c, c^2, c^3, … c^k. `
meaning for n input, we do c^k, so k will be (log)c(n)..  

Even though size increases, the time complexity only increases logarithmically.

O(LogLogn) Time Complexity of a loop is considered as O(LogLogn) if the loop 
variables are reduced/increased exponentially by a constant amount. 
 
```bash
   // Here c is a constant greater than 1   
   for (int i = 2; i <=n; i = pow(i, c)) { 
       // some O(1) expressions
   }
   //Here fun is sqrt or cuberoot or any other constant root
   for (int i = n; i > 1; i = fun(i)) { 
       // some O(1) expressions
   }
```
How to combine the time complexities of consecutive loops? 
When there are consecutive loops, we calculate time complexity as a sum of time 
complexities of individual loops. 
 
```bash
   for (int i = 1; i <=m; i += c) {  
        // some O(1) expressions
   }
   for (int i = 1; i <=n; i += c) {
        // some O(1) expressions
   }
```

Time complexity of above code is O(m) + O(n) which is O(m+n),  If m == n, the 
time complexity becomes O(2n) which is O(n).   
   
 
