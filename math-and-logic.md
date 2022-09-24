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
sum.of.GP = a(1-r^n)/1-r
$$

**Mean :** sum of all numbers divided by number of numbers

**Median** :

* For odd number of numbers : middle number&#x20;
* For even number of numbers : = ( mean of middle numbers ) / 2

**LCM**

$$
LCM (a,b) = |a.b|/gcd(a,b)
$$

### Number of Digits

* Number of Digits in a number ( iteratively )

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

* Number of Digits in a number ( recursively )

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

* Number of Digits in a number ( mathematically )

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

### Factorial of a number

```java
class App {

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
