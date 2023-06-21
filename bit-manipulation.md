---
description: on/off
---

# Bit Manipulation

### Check if the kth bit is set or not

```java
// To check if  
// k-th bit of a given number  
// is set or not using right  
// shift operator. 

class Program {
    static void isKthBitSet(int n, int k) {
        if (((n >> (k - 1)) & 1) == 1)
            System.out.println("SET");
        else
            System.out.println("NOT SET");
    }

    // Driver code
    public static void main(String[] args) {
        int n = 5, k = 1;
        isKthBitSet(n, k);
    }
}
```

### Check If The Number is Odd or Even

**Important**

```java
//  "&" operator
// [ 1 & 1 = 1 ]  [1 & 0 = 0]
// as we know one's digit of number is 1 
// if it is odd 
// or 0 if it is even
// therefore 

class Program {
    public static void Main(String[] args) {
        int a = 4;
        evenodd(a);
    }

    static void evenodd(int n) {
        if ((n & 1) == 1) {
            System.out.println("odd");
        } else {
            System.out.println("even");
        }
    }

}

```

### To swap two numbers

**Important**

```java
class Program {
    public static void main(String[] args) {
        int a = 3, b = 5;
        swap(a, b);
    }

    static void swap(int a, int b) {
        System.out.println(a + " " + b);
        a = a ^ b; // xor of a and b will be stored in a
        b = a ^ b; // value of a will be store in b
        a = a ^ b; // value of b will be store in a
        System.out.println(a + " " + b);
    }
}
```

### Check if a number is a power of 2

**Important**

```java
// Program to efficiently  
// check for power for 2 

class Program 
{ 
    /* Method to check if x is power of 2*/
    static boolean isPowerOfTwo (int x) 
    { 
      /* First x in the below expression is  
        for the case when x is 0 */
        return x!=0 && ((x&(x-1)) == 0); 
    } 

    // Driver method 
    public static void main ( String[] args )  
    { 
         System.out.println(isPowerOfTwo(31) 
             ? "Yes" : "No"); 
         System.out.println(isPowerOfTwo(64) 
             ? "Yes" : "No"); 
    } 
}
```

### Find The Number Occurring only once rest Occurring k times

```java

class Program {
    public static void main(String[] args) {
        int a[] = { 2, 3, 4, 5, 3, 2, 4 };
        int b = single(a, 2);
        System.out.println(b);
    }

    static int single(int a[], int k) {
        int count[] = new int[32];

        for (int i = 0; i < 32; i++) {
            for (int j = 0; j < a.length; j++) {
                if ((a[j] & (1 << i)) != 0) {
                    count[i] += 1;
                }
            }
        }
        int res = 0;
        for (int i = 0; i < 32; i++) {
            res += (count[i] % k) * (1 << i);
        }
        return res;

    }
}
```

### Count set bits

**Important**

```java
// Program to Count set  
// bits in an integer  

class countSetBits 
{ 
    /* Function to get no of set  
    bits in binary representation  
    of passed binary no. */
    static int countSetBits(int n) 
    { 
        int count = 0; 
        while (n > 0) 
        { 
            n &= (n - 1) ; 
            count++; 
        } 
        return count; 
    } 

    // driver program 
    public static void main ( String[] args ) 
    { 
        int i = 9; 
        System.out.println(countSetBits(i)); 
    } 
}
```

### To Count Set Bits in First N natural numbers

```java
class Program {

	static int twopower(int n) {
		int x = 0;
		while ((1 << x) <= n) {
			x++;
		}
		return x - 1;
	}

	static int totalbit(int n) {
		if (n == 0) {
			return 0;
		}

		int x = twopower(n);
		int a = x * (1 << (x - 1));
		int b = n - (1 << x) + 1;
		int c = n - (1 << x);
		int res = a + b + totalbit(c);

		return res;
	}

	// Driver program
	public static void main(String[] args) {
		int a = 6;
		System.out.println(totalbit(a));
	}

}
```

### Find the Number Occurring Odd Number of Times

```java
//Java program to find the element
// occurring odd number of times 

class Program {
	static int getOddOccurrence(int ar[], int ar_size) {
		int i;
		int res = 0;
		for (i = 0; i < ar_size; i++) {
			res = res ^ ar[i];
		}
		return res;
	}

	public static void main(String[] args) {

		int ar[] = new int[] { 2, 3, 5, 4, 5, 2, 4, 3, 5, 2, 4, 4, 2 };
		int n = ar.length;
		System.out.println(
				getOddOccurrence(ar, n));
	}
}
```

### Longest substring with count of 1s more than 0s

```java
// Java program to find largest substring 
// having count of 1s more than count 
// count of 0s. 

class Program 
{ 

    // Function to find longest substring 
    // having count of 1s more than count 
    // of 0s. 
    static int findLongestSub(String bin) 
    { 
        int n = bin.length(), i; 

        // To store sum. 
        int sum = 0; 

        // To store first occurrence of each 
        // sum value. 
        HashMap<Integer, Integer> prevSum = new HashMap<>(); 

        // To store maximum length. 
        int maxlen = 0; 

        // To store current substring length. 
        int currlen; 
        for (i = 0; i < n; i++) 
        { 

            // Add 1 if current character is 1 
            // else subtract 1. 
            if (bin.charAt(i) == '1') 
                sum++; 
            else
                sum--; 

            // If sum is positive, then maximum 
            // length substring is bin[0..i] 
            if (sum > 0) 
            { 
                maxlen = i + 1; 
            } 

            // If sum is negative, then maximum 
            // length substring is bin[j+1..i], where 
            // sum of substring bin[0..j] is sum-1. 
            else if (sum <= 0) 

            { 
                if (prevSum.containsKey(sum - 1)) 
                { 
                    currlen = i - 
                        (prevSum.get(sum - 1) 
                            == null ? 1 : 
                        prevSum.get(sum - 1)); 
                    maxlen = Math.max(maxlen, currlen); 
                } 
            } 

            // Make entry for this sum value in hash 
            // table if this value is not present. 
            if (!prevSum.containsKey(sum)) 
                prevSum.put(sum, i); 
        } 
        return maxlen; 
    } 

    // Driver code 
    public static void main ( String[] args ) 
    { 
        String bin = "1010"; 
        System.out.println(findLongestSub(bin)); 
    } 
}
```

### Generate power set

```java
// Java program for power set 

class Program { 

    static void printPowerSet(char []set, 
                            int set_size) 
    { 

        /*set_size of power set of a set 
        with set_size n is (2**n -1)*/
        long pow_set_size = 
            (long)Math.pow(2, set_size); 
        int counter, j; 

        /*Run from counter 000..0 to 111..1*/
        for(counter = 0; counter < 
                pow_set_size; counter++) 
        { 
            for(j = 0; j < set_size; j++) 
            { 
                /* Check if jth bit in the 
                counter is set If set then 
                print jth element from set */
                if((counter & (1 << j)) > 0) 
                    System.out.print(set[j]); 
            } 

            System.out.println(); 
        } 
    } 

    // Driver program to test printPowerSet 
    public static void main ( String[] args ) 
    { 
        char []set = {'a', 'b', 'c'}; 
        printPowerSet(set, 3); 
    } 
}
```
