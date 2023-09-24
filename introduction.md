---
description: Theory Theory Theory
---

# Introduction

## Asymptotic Notation

* Asymptotic notations are mathematical tools to represent the time complexity of algorithms for asymptotic analysis. The following 3 asymptotic notations are mostly used to represent the time complexity of algorithms.
* Asymptotic analysis refers to **computing the running time of any operation in mathematical units of computation**

## Θ Theta Notation

* The theta notation bounds a function from above and below, so it defines exact asymptotic behavior.

<figure><img src=".gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

```
Θ(g(n)) = {      f(n): there exist positive constants c1, c2 and n0 
  		  such that :
                      0 <= c1*g(n) <= f(n) <= c2*g(n) 
                  for all n >= n0
	  }
```

A simple way to get the Theta notation of an expression is to drop low-order terms and ignore leading constants.&#x20;

## Big O Notation

**The Big O notation defines an upper bound of an algorithm, it bounds a function only from above**

If we use O notation to represent time complexity of Insertion sort, we have to use two statements for best and worst cases

1. The worst case time complexity of Insertion Sort is O($n^2$).
2. The best case time complexity of Insertion Sort is O(n). Note that O($n^2$) also covers linear time.

<figure><img src=".gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

```
O(g(n)) = {     f(n): there exist positive constants 
                c and n0 such that 
		                0 <= f(n) <= c*g(n) 
                for all n >= n0
          }
```

## **Ω Delta Notation**

Just as Big O notation provides an asymptotic upper bound on a function, _**Ω notation**_ provides an asymptotic lower bound.

<figure><img src=".gitbook/assets/image (3) (1).png" alt=""><figcaption></figcaption></figure>

```
Ω (g(n)) = {    f(n): there exist positive constants c and n0 
                such that 
                    0 <= c*g(n) <= f(n) 
                for all n >= n0
            }
```

### Deriving Big O notation

**O(1):** Time complexity of a function (or set of statements) is considered as O(1) if it doesn't contain loop, recursion and call to any other non-constant time function.

**O(n):** Time Complexity of a loop is considered as O(n) if the loop variables is incremented / decremented by a constant amount

```jsx
// Here c is a positive integer constant   
for (int i = 1; i <= n; i += c) {  
    // some O(1) expressions
}
```

**O($n^c$)**: Time complexity of nested loops is equal to the number of times the innermost statement is executed. For example the following sample loops have O($n^c$) time complexity

```jsx
for (int i = 1; i <=n; i += c) {
       for (int j = 1; j <=n; j += c) {
          // some O(1) expressions
    }
}
```

**O( Log(n) )**: Time Complexity of a loop is considered as O( Log(n) ) if the loop variables is divided / multiplied by a constant amount

```jsx
for (int i = 1; i <=n; i *= c) {
       // some O(1) expressions
 }

for (int i = n; i > 0; i /= c) {
   // some O(1) expressions
}
```

**O( Log(Log(n)) )**: Time Complexity of a loop is considered as **O( Log(Log(n)) )** if the loop variables is reduced / increased exponentially by a constant amount

```jsx
// Here c is a constant greater than 1   
 for (int i = 2; i <=n; i = pow(i, c)) { 
     // some O(1) expressions
 }
```

**O( m+n ) :** When there are consecutive loops, we calculate time complexity as sum of time complexities of individual loops.

```jsx
for (int i = 1; i <=m; i += c) {  
        // some O(1) expressions
 }

for (int i = 1; i <=n; i += c) {
    // some O(1) expressions
}
```
