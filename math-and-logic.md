---
description: back to school
---

# Math & Logic

### Basic Maths

#### Sum of AP

$$
sum = n/2*(2a+(n-1)d
$$

#### Sum of GP

$$
sum \space of \space GP = a(1-r^n)/1-r
$$



**Mean :** sum of all numbers divided by number of numbers

**Median** :

* For odd number of numbers : middle number&#x20;
* For even number of numbers : ( mean of middle numbers ) / 2

**LCM**

$$
LCM (a,b) = |a.b| \space / \space gcd(a,b)
$$

### Number of Digits

* Number of Digits in a number ( iteratively )

```java

class Solution {

    public static void main(String[] args) {
        int number = 123456;
        int len = 0;

        while (number > 0) {
            number = number / 10;
            len++;
        }

        System.out.println("Length : " + len);
    }
}

```

* Number of Digits in a number ( recursively )

```java

class Solution {
    public static int numOfDigits(int num) {
        if (num == 0) {
            return 0;
        }

        return numOfDigits(num / 10) + 1;
    }

    public static void main(String[] args) {
        int number = 123456;
        System.out.println("Length : " + numOfDigits(number));
    }
}

```

* Number of Digits in a number ( mathematically )

```java

class Solution {
	public static void main(String[] args) {
		int number = 12345;
		System.out.println("Number : " +
				(int) (Math.log10(number) + 1));
	}
}

```

### GCD or HCF

```java

class Solution {

    static int GCD(int a, int b) {
		if (a == 0) {
			return b;
		}
		return GCD(b % a, a);
	}

	public static void main(String[] args) {
		System.out.println("GCD : " + GCD(28, 8));
	}
}

```

### First N Prime

```java
class Solution {

    // function to check if a given number is prime
    static boolean isPrime(int n) {
        // since 0 and 1 is not prime return false.
        if (n == 1 || n == 0)
            return false;

        // Run a loop from 2 to n-1
        for (int i = 2; i < n; i++) {
            // if the number is divisible by i, then n is not a prime number.
            if (n % i == 0)
                return false;
        }
        // otherwise, n is prime number.
        return true;
    }

    // Driver code
    public static void main(String[] args) {
        int N = 100;
        // check for every number from 1 to N
        for (int i = 1; i <= N; i++) {
            // check if current number is prime
            if (isPrime(i)) {
                System.out.print(i + " ");
            }
        }
    }
}
```

### Factorial of a number

```java
class Solution {

    static int fact(int n) {
        if(n == 0) {
            return 1;
        }
        
        return n*fact(n-1);
    }

    public static void main(String[] args) {
        System.out.println(fact(4));
    }
}
```
