---
description: IQ
---

# Math & Logic

### Basic Maths

#### Sum of AP

$$
sum = n/2*(2a+(n-1)d
$$

#### Sum of GP

$$
sum.of.GP = a(1-r^n)/1-r
$$

**Mean :** sum of all numbers divided by number of numbers

**Median** :

* For odd number of numbers : middle number&#x20;
* For even number of numbers : = (mean\_of\_2\_middle a numbers)/2

**LCM**

$$
LCM (a,b) = |a.b|/gcd(a,b)
$$



### Number of Digits

### Number of Digits in a number ( iteratively )

{% tabs %}
{% tab title="Java" %}
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
{% endtab %}
{% endtabs %}

### Number of Digits in a number ( recursively )

{% tabs %}
{% tab title="Java" %}
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
{% endtab %}
{% endtabs %}

### Number of Digits in a number ( mathematically )

{% tabs %}
{% tab title="Java" %}
```java
class Solution {
	public static void main(String[] args) {
		int number = 12345;
		System.out.println("Number : " +
				(int) (Math.log10(number) + 1));
	}
}
```
{% endtab %}
{% endtabs %}

### GCD or HCF

{% tabs %}
{% tab title="Java" %}
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
{% endtab %}
{% endtabs %}

### First N Prime

{% tabs %}
{% tab title="Java" %}
```java
import java.util.ArrayList;

class Solution {
	public static ArrayList<Integer> firstPrime(int num) {
		ArrayList<Integer> lst = new ArrayList<>();

		for (int i = 0; i <= num; i++) {
			if (i == 1) {
				continue;
			}
			int flag = 0;
			for (int j = 2; j <= i / 2; j++) {
				if (i % j == 0) {
					flag = 1;
					break;
				}
			}
			if (flag == 0) {
				lst.add(i);
			}
		}

		return lst;
	}

	public static void main(String[] args) {
		ArrayList<Integer> lst = firstPrime(100);
		lst.forEach(value -> System.out.print("|" + value + "|"));
	}
}
```
{% endtab %}
{% endtabs %}

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



### First Bad Version

```
Suppose you have n versions [1, 2, ..., n] and you want to 
find out the first bad one, which causes all the following ones to be bad.

You are given an API bool isBadVersion(version) which returns 
whether version is bad. 

Implement a function to find the first bad version. 
You should minimize the number of calls to the API.

 
Example 1:

Input: n = 5, bad = 4
Output: 4
Explanation:
call isBadVersion(3) -> false
call isBadVersion(5) -> true
call isBadVersion(4) -> true
Then 4 is the first bad version.
```

```java
/* The isBadVersion API is defined in the parent class VersionControl.
      boolean isBadVersion(int version); */

public class Solution extends VersionControl {
	public int firstBadVersion(int n) {
		int left = 1;
		int right = n;
		while (left < right) {
			int mid = left + (right - left) / 2;
			if (isBadVersion(mid)) {
				right = mid;
			} else {
				left = mid + 1;
			}
		}
		return left;
	}
}
```
