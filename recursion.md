---
description: Just like inception
---

# Recursion

### Tail recursion

The tail recursion is better than non-tail recursion. As there is no task left after the recursive call, it will be easier for the compiler to optimize the code. When one function is called, its address is stored inside the stack. So if it is tail recursion, then storing addresses into stack is not needed.

We can use factorial using recursion, but the function is not tail recursive. The value of fact(n-1) is used inside the fact(n).

```java
long fact(int n){
   if(n <= 1)
      return 1;
   n * fact(n-1);
}
```

We can make it tail recursive, by adding some other parameters. This is like below −

```java
long fact(long n, long a){
   if(n == 0)
      return a;
   return fact(n-1, a*n);
}
```

When last statement is recursion, it is tail recursion, which is optimized by compiler using goto statements.

### 1 to N and N to 1

```java

class Solution {
    public static void main(String[] args) {
        System.out.println("--- start ---");

        print1ToN(9);
        System.out.println();
        printNTo1(9);

        System.out.println("\n--- end ---");
    }

    private static void printNTo1(int i) {
        if (i == 0) {
            return;
        }
        System.out.print(i + "|");
        printNTo1(i - 1);
    }

    private static void print1ToN(int i) {
        if (i == 0) {
            return;
        }
        print1ToN(i - 1);
        System.out.print(i + "|");
    }
}

```

### Tower of Hanoi

Tower of Hanoi is a mathematical puzzle where we have three rods and n disks. The objective of the puzzle is to move the entire stack to another rod, obeying the following simple rules:

1. Only one disk can be moved at a time.
2. Each move consists of taking the upper disk from one of the stacks and placing it on top of another stack i.e. a disk can only be moved if it is the uppermost disk on a stack.
3. No disk may be placed on top of a smaller disk.

Just remember : `132 | 123 | 231`

```
Take an example for 2 disks :
Let rod 1 = 'A', rod 2 = 'B', rod 3 = 'C'.

Step 1 : Shift first disk from 'A' to 'B'.
Step 2 : Shift second disk from 'A' to 'C'.
Step 3 : Shift first disk from 'B' to 'C'.

The pattern here is :
Shift 'n-1' disks from 'A' to 'B'.
Shift last disk from 'A' to 'C'.
Shift 'n-1' disks from 'B' to 'C'.

Image illustration for 3 disks 

```

<figure><img src=".gitbook/assets/image (1) (2).png" alt=""><figcaption></figcaption></figure>

```
Output : Disk 1 moved from A to B
         Disk 2 moved from A to C
         Disk 1 moved from B to C

Input : 3
Output : Disk 1 moved from A to C
         Disk 2 moved from A to B
         Disk 1 moved from C to B
         Disk 3 moved from A to C
         Disk 1 moved from B to A
         Disk 2 moved from B to C
         Disk 1 moved from A to C
```

```java

class Program {
    static void towerOfHanoi(int n, char from_rod,
            char to_rod, char aux_rod) {
        if (n == 1) {
            System.out.println(
                    "Move disk 1 from rod " +
                            from_rod + " to rod " + to_rod);
            return;
        }

        towerOfHanoi(n - 1, from_rod, aux_rod, to_rod);

        System.out.println(
                "Move disk " + n + " from rod " +
                        from_rod + " to rod " + to_rod);

        towerOfHanoi(n - 1, aux_rod, to_rod, from_rod);
    }

    public static void main(String[] args) {
        int n = 4; // Number of disks
        towerOfHanoi(n, 'A', 'C', 'B');
        // A, B and C are names of rods
    }
}

```

### Fibonacci (Recursion)

```java

class Solution {
    static public int fib(int n) {
        if (n <= 1)
            return n;
        return fib(n - 1) + fib(n - 2);
    }

    public static void main(String[] args) {
        System.out.println(fib(5));
    }
}

```

### Count Total Digits

```java

class Solution {
    public static int countDigits(int n) {
        if (n < 10) {
            return 1;
        }

        // triming one digit in recursive call
        return 1 + countDigits(n / 10);
    }

    public static void main(String[] args) {
        System.out.println(countDigits(10121));
    }
}

```

### Sum of Digits

```java
class Solution {
	public static int sumOfDigits(int n) {
		if (n == 0) {
		  return 0;
		}
	  
		// extract first digit + sum of all others
		// why extract, cuz it will be left out in first call stack
		return n % 10 + sumOfDigits(n / 10);
	  }

	public static void main(String[] args) {
		System.out.println(sumOfDigits(10121));
	}
}
```

### Is string palindrome

```java
class App {
    public static void main(String[] args) {
        System.out.println(palindrome("aabaa"));
        System.out.println(palindrome("abc"));
    }

    private static boolean palindrome(String str) {
        if(str.length() == 0) return true;
        return checkPalindrome(str, 0, str.length() - 1);
    }

    private static boolean checkPalindrome(String str, int s, int e) {

        // reach the same character
        if(s == e) return true;

        // base case
        if (str.charAt(s) != str.charAt(e)) return true;
        
        // advance to start+1 and end-1
        if (s < e + 1) {
            return checkPalindrome(str, s + 1, e - 1);
        }

        return true;
    }
}kjava
```

### Josephus problem

```java
class Solution {

	static int josephus(int n, int k) {
		if (n == 1)
			return 1;
		else
			// learn this ....
			return (josephus(n - 1, k) + k - 1) % n + 1;
	}

	public static void main(String[] args) {
		int n = 14;
		int k = 2;
		System.out.println("The chosen place is "
				+ josephus(n, k));
	}
}
```

### Power Using Recursion

```java
class Solution {

	// Function to calculate N raised to the power P
	static int power(int N, int P) {
		if (P == 0)
			return 1;
		else
			return N * power(N, P - 1);
	}

	public static void main(String[] args) {
		int N = 2;
		int P = 3;
		// n**p
		System.out.println(power(N, P));
	}
}
```

### Digital Root

Sum of all digits ,, till a single digit is achieved

ex : `99999` -> `45` -> `9`&#x20;

```java
class Solution {

    public static int digitalRoot(int n) {
        if (n < 10)
            return n;
            
        return digitalRoot(n % 10 + digitalRoot(n / 10));
    }

	public static void main(String[] args) {
		System.out.println(digitalRoot(99999));
	}
}
```

### S**um of digit of a number**&#x20;

using recursion

```java

class Solution {
    static int sum_of_digit(int n) {
        if (n == 0)
            return 0;
        return (n % 10 + sum_of_digit(n / 10));
    }

    public static void main(String[] args) {
        int num = 12345;
        int result = sum_of_digit(num);
        System.out.println("Sum of digits is " + result);
    }
}
j
```

### Rod cutting

Important : Inputs should be sort

```java

class Solution {
	static int rodCutting(int n, int a, int b, int c) {
		if (n == 0)
			return 0;
		if (n < 0)
			return -1;

		int res = Math.max(
				Math.max(
				rodCutting(n - a, a, b, c),
				rodCutting(n - b, a, b, c)),
				rodCutting(n - c, a, b, c));

		if (res == -1)
			return -1;
		return 1 + res;
	}

	public static void main(String[] args) {
		int n = 25;
		int a = 11, b = 12, c = 13;
		System.out.println(rodCutting(n, a, b, c));

	}
}

```

### All subsets of string

```java

class Soltution {

    // str : Stores input string
    // curr : Stores current subset
    // index : Index in current subset, curr
    static void powerSet(String str, int index, String curr) {
        int n = str.length();

        // base case
        if (index == n) {
            System.out.println(curr);
            return;
        }

        // Two cases for every character
        // (i) We consider the character
        // as part of current subset
        // (ii) We do not consider current
        // character as part of current subset
        powerSet(str, index + 1, curr + str.charAt(index));
        powerSet(str, index + 1, curr);
    }

    public static void main(String[] args) {
        String str = "abc", curr = "";
        int index = 0;
        powerSet(str, index, curr);
    }
}

```

### All permutation of String&#x20;

```java
import java.util.ArrayList;

class Solution {
	static public void findPermutation(String s, ArrayList<String> lst,
			String ans) {
		if (s.length() == 0) {
			lst.add(ans);
			return;
		}

		for (int i = 0; i < s.length(); i++) {
			String str = s.substring(0, i) + s.substring(i + 1);
			findPermutation(str, lst, ans + s.charAt(i));
		}
	}

	static public ArrayList<String> permutation(String S) {
		ArrayList<String> lst = new ArrayList<>();
		String ans = "";

		findPermutation(S, lst, ans);
		return lst;
	}

	public static void main(String[] args) {
		var result = permutation("uday");
		System.out.println(result.toString());
	}
}
```
