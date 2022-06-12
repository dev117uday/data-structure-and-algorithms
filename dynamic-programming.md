# Dynamic Programming

## Factorial using DP

### Memoization

```java
/*package whatever //do not write package name here */

import java.io.*;
import java.util.*;
import static java.lang.System.out;

class GFG {

    static int[] memo;

    static int fib(int n) {
        if (memo[n] == -1) {
            int res;

            if (n == 0 || n == 1)
                return n;

            else {
                res = fib(n - 1) + fib(n - 2);

            }

            memo[n] = res;

        }

        return memo[n];
    }

    public static void main(String[] args) {

        int n = 5;

        memo = new int[n + 1];

        Arrays.fill(memo, -1);

        out.println(fib(n));

    }
}
```

### Tabulation

```java
/*package whatever //do not write package name here */

import java.io.*;
import java.util.*;
import static java.lang.System.out;

class GFG {

    static int fib(int n) {
        int f[] = new int[n + 1];

        f[0] = 0;
        f[1] = 1;

        for (int i = 2; i <= n; i++) {
            f[i] = f[i - 1] + f[i - 2];
        }

        return f[n];

    }

    public static void main(String[] args) {

        int n = 5;

        out.println(fib(n));

    }
}
```

## **Longest Common Subsequence (Part 1)**

### **Memoization**

```java
/*package whatever //do not write package name here */

import java.io.*;
import java.util.*;
import static java.lang.System.out;

class GFG {

    static int[][] memo;

    static int lcs(String s1, String s2, int n, int m) {
        if (memo[n][m] != -1)
            return memo[n][m];

        if (n == 0 || m == 0)
            memo[n][m] = 0;

        else {
            if (s1.charAt(n - 1) == s2.charAt(m - 1))
                memo[n][m] = 1 + lcs(s1, s2, n - 1, m - 1);
            else
                memo[n][m] = Math.max(lcs(s1, s2, n - 1, m), lcs(s1, s2, n, m - 1));
        }

        return memo[n][m];

    }

    public static void main(String[] args) {

        String s1 = "AXYZ", s2 = "BAZ";

        int n = 4, m = 3;

        memo = new int[n + 1][m + 1];

        for (int[] i : memo) {
            Arrays.fill(i, -1);
        }

        System.out.println(lcs(s1, s2, n, m));

    }
}
```

### Tabulation

```java
/*package whatever //do not write package name here */

import java.io.*;
import java.util.*;
import static java.lang.System.out;

class GFG {

    static int lcs(String s1, String s2) {
        int m = s1.length(), n = s2.length();

        int dp[][] = new int[m + 1][n + 1];

        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                if (s1.charAt(i - 1) == s2.charAt(j - 1))
                    dp[i][j] = 1 + dp[i - 1][j - 1];
                else
                    dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - 1]);
            }
        }

        return dp[m][n];

    }

    public static void main(String[] args) {

        String s1 = "AXYZ", s2 = "BAZ";

        System.out.println(lcs(s1, s2));

    }
}
```

## **Variation of LCS**

* Diff Utility
* Min. insert or delete to convert s1 to s2
* Short common sequence
* Longest Palindrome Sub sequence
* Longest Repeating Sub sequence
* Printing LCS

## **Coin Change Count Combinations**

```java
/*package whatever //do not write package name here */

import java.io.*;
import java.util.*;
import static java.lang.System.out;

class GFG {

    static int getCount(int coins[], int n, int sum) {
        int dp[][] = new int[sum + 1][n + 1];

        for (int i = 0; i <= n; i++) {
            dp[0][i] = 1;
        }

        for (int i = 1; i <= sum; i++) {
            for (int j = 1; j <= n; j++) {
                dp[i][j] = dp[i][j - 1];

                if (coins[j - 1] <= i)
                    dp[i][j] += dp[i - coins[j - 1]][j];
            }
        }

        return dp[sum][n];

    }

    public static void main(String[] args) {

        int coins[] = { 1, 2, 3 }, sum = 4, n = 3;

        System.out.println(getCount(coins, n, sum));

    }
}
```

## **Edit Distance Problem**

```java
/*package whatever //do not write package name here */

import java.io.*;
import java.util.*;
import static java.lang.System.out;

class GFG {

    static int eD(String s1, String s2, int m, int n) {
        if (m == 0)
            return n;
        if (n == 0)
            return m;

        if (s1.charAt(m - 1) == s2.charAt(n - 1))
            return eD(s1, s2, m - 1, n - 1);
        else {
            return 1 + Math.min(eD(s1, s2, m, n - 1), Math.min(eD(s1, s2, m - 1, n), eD(s1, s2, m - 1, n - 1)));
        }

    }

    public static void main(String[] args) {

        String s1 = "CAT", s2 = "CUT";
        int n = 3, m = 3;

        System.out.println(eD(s1, s2, m, n));

    }
}
```

## **Edit Distance Problem DP**&#x20;

```java
/*package whatever //do not write package name here */

import java.io.*;
import java.util.*;
import static java.lang.System.out;

class GFG {

    static int eD(String s1, String s2, int m, int n) {
        int dp[][] = new int[m + 1][n + 1];

        for (int i = 0; i <= m; i++) {
            dp[i][0] = i;
        }

        for (int j = 0; j <= n; j++) {
            dp[0][j] = j;
        }

        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                if (s1.charAt(i - 1) == s2.charAt(j - 1)) {
                    dp[i][j] = dp[i - 1][j - 1];
                } else {
                    dp[i][j] = 1 + Math.min(dp[i - 1][j], Math.min(dp[i][j - 1], dp[i - 1][j - 1]));

                }
            }
        }

        return dp[m][n];
    }

    public static void main(String[] args) {

        String s1 = "CAT", s2 = "CUT";
        int n = 3, m = 3;

        System.out.println(eD(s1, s2, m, n));

    }
}
```

## **Longest Increasing Subsequence Problem**

```java
/*package whatever //do not write package name here */

import java.io.*;
import java.util.*;
import static java.lang.System.out;

class GFG {

    static int LIS(int arr[], int n) {
        int lis[] = new int[n];

        lis[0] = 1;

        for (int i = 1; i < n; i++) {
            lis[i] = 1;
            for (int j = 0; j < i; j++)
                if (arr[i] > arr[j])
                    lis[i] = Math.max(lis[i], lis[j] + 1);
        }

        int res = lis[0];

        for (int i = 0; i < n; i++) {
            res = Math.max(lis[i], res);
        }

        return res;

    }

    public static void main(String[] args) {
        int arr[] = { 3, 4, 2, 8, 10, 5, 1 };
        int n = 7;

        System.out.println(LIS(arr, n));

    }
}
```

## **Longest Increasing Subsequence O( nlog(n) )**

```java
/*package whatever //do not write package name here */

import java.io.*;
import java.util.*;
import static java.lang.System.out;

class GFG {

    static int ceilIdx(int tail[], int l, int r, int key) {
        while (r > l) {
            int m = l + (r - l) / 2;
            if (tail[m] >= key)
                r = m;
            else
                l = m + 1;
        }

        return r;
    }

    static int LIS(int arr[], int n) {

        int[] tail = new int[n];
        int len = 1;

        tail[0] = arr[0];

        for (int i = 1; i < n; i++) {

            if (arr[i] > tail[len - 1]) {
                tail[len] = arr[i];
                len++;
            } else {
                int c = ceilIdx(tail, 0, len - 1, arr[i]);

                tail[c] = arr[i];
            }
        }

        return len;
    }

    public static void main(String[] args) {
        int arr[] = { 3, 10, 20, 4, 6, 7 };
        int n = 6;

        System.out.println(LIS(arr, n));

    }
}
```

## Variation of LIS

* Minimum deletions to make array sorted
* Maximum Sum Increasing Sub sequence
* Max Length Bitonic Solution
* Building Bridges
* The longest chain

## **Maximum Cuts**

```java
/*package whatever //do not write package name here */

import java.io.*;
import java.util.*;
import static java.lang.System.out;

class GFG {

    static int maxCuts(int n, int a, int b, int c) {

        int dp[] = new int[n + 1];

        dp[0] = 0;

        for (int i = 1; i <= n; i++) {
            dp[i] = -1;

            if (i - a >= 0)
                dp[i] = Math.max(dp[i], dp[i - a]);

            if (i - b >= 0)
                dp[i] = Math.max(dp[i], dp[i - b]);

            if (i - c >= 0)
                dp[i] = Math.max(dp[i], dp[i - c]);

            if (dp[i] != -1)
                dp[i]++;
        }

        return dp[n];

    }

    public static void main(String[] args) {
        int n = 5, a = 1, b = 2, c = 3;

        System.out.println(maxCuts(n, a, b, c));

    }
}
```

## **Minimum coins to make a value**

```java
/*package whatever //do not write package name here */

import java.io.*;
import java.util.*;
import static java.lang.System.out;

class GFG {

    static int minCoins(int arr[], int m, int value) {

        int dp[] = new int[value + 1];

        dp[0] = 0;

        for (int i = 1; i <= value; i++)
            dp[i] = Integer.MAX_VALUE;

        for (int i = 1; i <= value; i++) {

            for (int j = 0; j < m; j++)
                if (arr[j] <= i) {
                    int sub_res = dp[i - arr[j]];
                    if (sub_res != Integer.MAX_VALUE && sub_res + 1 < dp[i])
                        dp[i] = sub_res + 1;

                }

        }
        return dp[value];

    }

    public static void main(String[] args) {
        int arr[] = { 3, 4, 1 }, val = 5, n = 3;

        System.out.println(minCoins(arr, n, val));

    }
}
```

## **Minimum Jumps to reach at end**

```java
/*package whatever //do not write package name here */

import java.io.*;
import java.util.*;
import static java.lang.System.out;

class GFG {

    static int minJumps(int arr[], int n) {

        int dp[] = new int[n];
        int i, j;

        dp[0] = 0;

        for (i = 1; i < n; i++) {
            dp[i] = Integer.MAX_VALUE;
            for (j = 0; j < i; j++) {
                if (i <= j + arr[j] && dp[j] != Integer.MAX_VALUE) {
                    dp[i] = Math.min(dp[i], dp[j] + 1);
                    break;
                }
            }
        }
        return dp[n - 1];
    }

    public static void main(String[] args) {
        int arr[] = { 3, 4, 2, 1, 2, 1 }, n = 6;

        System.out.println(minJumps(arr, n));

    }
}
```

## **0-1 knapsack problem**

```java
/*package whatever //do not write package name here */

import java.io.*;
import java.util.*;
import static java.lang.System.out;

class GFG {

    static int knapSack(int W, int wt[], int val[], int n) {

        if (n == 0 || W == 0)
            return 0;

        if (wt[n - 1] > W)
            return knapSack(W, wt, val, n - 1);

        else
            return Math.max(val[n - 1] + knapSack(W - wt[n - 1], wt, val, n - 1), knapSack(W, wt, val, n - 1));
    }

    public static void main(String[] args) {
        int val[] = { 10, 40, 30, 50 };
        int wt[] = { 5, 4, 6, 3 };
        int W = 10;
        int n = 4;

        System.out.println(knapSack(W, wt, val, n));

    }
}
```

## **0-1 knapsack problem DP Solution**

```java
/*package whatever //do not write package name here */

import java.io.*;
import java.util.*;
import static java.lang.System.out;

class GFG {

    static int knapSack(int W, int wt[], int val[], int n) {

        int dp[][] = new int[n + 1][W + 1];

        for (int i = 0; i <= W; i++) {
            dp[0][i] = 0;
        }

        for (int i = 0; i <= n; i++) {
            dp[i][0] = 0;
        }

        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= W; j++) {
                if (wt[i - 1] > j)
                    dp[i][j] = dp[i - 1][j];
                else
                    dp[i][j] = Math.max(val[i - 1] + dp[i - 1][j - wt[i - 1]], dp[i - 1][j]);
            }
        }

        return dp[n][W];
    }

    public static void main(String[] args) {
        int val[] = { 10, 40, 30, 50 };
        int wt[] = { 5, 4, 6, 3 };
        int W = 10;
        int n = 4;

        System.out.println(knapSack(W, wt, val, n));

    }
}
```

## **Optimal Strategy for a Game**

```java
/*package whatever //do not write package name here */

import java.io.*;
import java.util.*;
import static java.lang.System.out;

class GFG {

    static int sol(int[] arr, int n) {
        int dp[][] = new int[n][n];

        for (int i = 0; i < n - 1; i++) {
            dp[i][i + 1] = Math.max(arr[i], arr[i + 1]);
        }

        for (int gap = 3; gap < n; gap = gap + 2) {
            for (int i = 0; i + gap < n; i++) {
                int j = gap + i;

                dp[i][j] = Math.max((arr[i] + Math.min(dp[i + 1][j], dp[i + 1][j - 1])),
                        (arr[i] + Math.min(dp[i + 1][j - 1], dp[i][j - 2])));
            }
        }

        return dp[0][n - 1];
    }

    public static void main(String[] args) {

        int n = 4;

        int arr[] = { 20, 5, 4, 6 };

        System.out.println(sol(arr, n));

    }
}
```

## **Egg Dropping Puzzle - Part 1**

```java
public class GFG {

    /*
     * Function to get minimum number of trials needed in worst case with n eggs and
     * k floors
     */
    static int eggDrop(int n, int k) {
        // If there are no floors, then
        // no trials needed. OR if there
        // is one floor, one trial needed.
        if (k == 1 || k == 0)
            return k;

        // We need k trials for one egg
        // and k floors
        if (n == 1)
            return k;

        int min = Integer.MAX_VALUE;
        int x, res;

        // Consider all droppings from
        // 1st floor to kth floor and
        // return the minimum of these
        // values plus 1.
        for (x = 1; x <= k; x++) {
            res = Math.max(eggDrop(n - 1, x - 1), eggDrop(n, k - x));
            if (res < min)
                min = res;
        }

        return min + 1;
    }

    // Driver code
    public static void main(String args[]) {
        int n = 2, k = 10;
        System.out.print("Minimum number of " + "trials in worst case with " + n + " eggs and " + k + " floors is "
                + eggDrop(n, k));
    }

}

```

## **Egg Dropping Puzzle - Part 2**

```java
/*package whatever //do not write package name here */

import java.io.*;
import java.util.*;
import static java.lang.System.out;

class GFG {

    static int res(int e, int f) {

        int dp[][] = new int[f + 1][e + 1];

        for (int i = 1; i <= e; i++) {
            dp[1][i] = 1;
            dp[0][i] = 0;
        }

        for (int j = 1; j <= f; j++) {
            dp[j][1] = j;
        }

        for (int i = 2; i <= f; i++) {
            for (int j = 2; j <= e; j++) {
                dp[i][j] = Integer.MAX_VALUE;
                for (int x = 1; x <= i; x++) {
                    dp[i][j] = Math.min(dp[i][j], 1 + Math.max(dp[x - 1][j - 1], dp[i - x][j]));
                }
            }
        }

        return dp[f][e];
    }

    public static void main(String[] args) {

        int n = 2;

        int f = 10;

        System.out.println(res(n, f));

    }
}
```

## **Count BSTs with n keys**

A recursive structure is discussed, then a dynamic programming solution is discussed, finally relation with Catalan Numbers.

```java
/*package whatever //do not write package name here */

import java.io.*;
import java.util.*;
import static java.lang.System.out;

class GFG {

    static int countBSTs(int n) {
        int dp[] = new int[n + 1];

        dp[0] = 1;

        for (int i = 1; i <= n; i++) {
            dp[i] = 0;

            for (int j = 0; j < i; j++) {
                dp[i] += dp[j] * dp[i - j - 1];
            }
        }

        return dp[n];
    }

    public static void main(String[] args) {

        int n = 4;

        System.out.println(countBSTs(n));

    }
}
```

## **Maximum sum with no two consecutive**

### DP-Code in O(1) space

```java
/*package whatever //do not write package name here */

import java.io.*;
import java.util.*;
import static java.lang.System.out;

class GFG {

    static int maxSum(int arr[], int n) {
        if (n == 0)
            return arr[0];

        int prev_prev = arr[0];
        int prev = Math.max(arr[0], arr[1]);
        int res = prev;

        for (int i = 3; i <= n; i++) {
            res = Math.max(prev, prev_prev + arr[i - 1]);

            prev_prev = prev;

            prev = res;
        }

        return res;
    }

    public static void main(String[] args) {

        int n = 5, arr[] = { 10, 20, 30, 40, 50 };

        System.out.println(maxSum(arr, n));

    }
}
```

### DP-Code in O(n) space

```java
/*package whatever //do not write package name here */

import java.io.*;
import java.util.*;
import static java.lang.System.out;

class GFG {

    static int maxSum(int arr[], int n) {
        if (n == 0)
            return arr[0];

        int dp[] = new int[n + 1];

        dp[1] = arr[0];
        dp[2] = Math.max(arr[0], arr[1]);

        for (int i = 3; i <= n; i++) {
            dp[i] = Math.max(dp[i - 1], dp[i - 2] + arr[i - 1]);
        }

        return dp[n];
    }

    public static void main(String[] args) {

        int n = 5, arr[] = { 10, 20, 30, 40, 50 };

        System.out.println(maxSum(arr, n));

    }
}
```

## **Subset Sum Problem (Recursive Solution)**

```java
/*package whatever //do not write package name here */

import java.io.*;
import java.util.*;
import static java.lang.System.out;

class GFG {

    static int countSubsets(int arr[], int n, int sum) {
        if (n == 0)
            return sum == 0 ? 1 : 0;

        return countSubsets(arr, n - 1, sum) + countSubsets(arr, n - 1, sum - arr[n - 1]);
    }

    public static void main(String[] args) {

        int n = 3, arr[] = { 10, 20, 15 }, sum = 25;

        System.out.println(countSubsets(arr, n, sum));

    }
}
```

## **Subset Sum Problem (DP Solution)**

```java
/*package whatever //do not write package name here */

import java.io.*;
import java.util.*;
import static java.lang.System.out;

class GFG {

    static int countSubsets(int arr[], int n, int sum) {
        int dp[][] = new int[n + 1][sum + 1];

        for (int i = 0; i <= n; i++)
            dp[i][0] = 1;
        for (int j = 1; j <= sum; j++)
            dp[0][j] = 0;

        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= sum; j++) {
                if (j < arr[i - 1])
                    dp[i][j] = dp[i - 1][j];
                else
                    dp[i][j] = dp[i - 1][j] + dp[i][j - arr[i - 1]];
            }
        }

        return dp[n][sum];
    }

    public static void main(String[] args) {

        int n = 3, arr[] = { 2, 5, 3 }, sum = 5;

        System.out.println(countSubsets(arr, n, sum));

    }
}
```

## **Matrix Chain Multiplication**

```java
/* A naive recursive implementation that simply follows 
the above optimal substructure property */
class MatrixChainMultiplication {
    // Matrix Ai has dimension p[i-1] x p[i] for i = 1..n
    static int MatrixChainOrder(int p[], int i, int j) {
        if (i + 1 == j)
            return 0;

        int min = Integer.MAX_VALUE;

        // place parenthesis at different places between first
        // and last matrix, recursively calculate count of
        // multiplications for each parenthesis placement and
        // return the minimum count
        for (int k = i + 1; k < j; k++) {
            int count = MatrixChainOrder(p, i, k) + MatrixChainOrder(p, k, j) + p[i] * p[k] * p[j];

            if (count < min)
                min = count;
        }

        // Return minimum count
        return min;
    }

    // Driver program to test above function
    public static void main(String args[]) {
        int arr[] = new int[] { 40, 20, 30, 10, 30 };
        int n = arr.length;
        System.out.println("Minimum number of multiplications is " + MatrixChainOrder(arr, 0, n - 1));

    }
}
```

## **Matrix Chain Multiplication (DP Solution)**

```java
/* A naive recursive implementation that simply follows 
the above optimal substructure property */
class MatrixChainMultiplication {
    // Matrix Ai has dimension p[i-1] x p[i] for i = 1..n
    static int MatrixChainOrder(int p[]) {
        int n = p.length;
        int dp[][] = new int[n][n];
        for (int i = 0; i < n - 1; i++)
            dp[i][i + 1] = 0;

        for (int gap = 2; gap < n; gap++) {
            for (int i = 0; i + gap < n; i++) {
                int j = i + gap;
                dp[i][j] = Integer.MAX_VALUE;
                for (int k = i + 1; k < j; k++) {
                    dp[i][j] = Math.min(dp[i][j], dp[i][k] + dp[k][j] + p[i] * p[k] * p[j]);
                }
            }
        }

        return dp[0][n - 1];
    }

    // Driver program to test above function
    public static void main(String args[]) {
        int arr[] = new int[] { 40, 20, 30, 10, 30 };
        int n = arr.length;
        System.out.println("Minimum number of multiplications is " + MatrixChainOrder(arr));

    }
}
```

## **Palindrome Partitioning**

```java
/*package whatever //do not write package name here */

import java.io.*;
import java.util.*;
import static java.lang.System.out;

class GFG {

    static boolean isPalindrome(String input, int start, int end) {
        // Using two pointer technique to check pallindrome
        while (start < end) {
            if (input.charAt(start) != input.charAt(end))
                return false;
            start++;
            end--;
        }
        return true;
    }

    static int palPart(String str) {
        int n = str.length();

        int dp[][] = new int[n][n];

        for (int i = 0; i < n; i++) {
            dp[i][i] = 0;
        }

        for (int gap = 1; gap < n; gap++) {
            for (int i = 0; i + gap < n; i++) {
                int j = i + gap;

                if (isPalindrome(str, i, j)) {
                    dp[i][j] = 0;
                } else {
                    dp[i][j] = Integer.MAX_VALUE;

                    for (int k = i; k < j; k++) {
                        dp[i][j] = Math.min(dp[i][j], 1 + dp[i][k] + dp[k + 1][j]);
                    }
                }
            }
        }

        return dp[0][n - 1];
    }

    public static void main(String[] args) {

        String s = "geek";

        System.out.println(palPart(s));

    }
}
```

## **Allocate Minimum Pages (Naive Method)**

```java
import java.util.*;
import java.io.*;
import java.lang.*;

class GFG {

    public static void main(String args[]) {
        int arr[] = { 10, 20, 10, 30 };
        int n = arr.length;
        int k = 2;

        System.out.print(minPages(arr, n, k));
    }

    public static int sum(int arr[], int b, int e) {
        int s = 0;
        for (int i = b; i <= e; i++)
            s += arr[i];
        return s;
    }

    public static int minPages(int arr[], int n, int k) {
        if (k == 1)
            return sum(arr, 0, n - 1);
        if (n == 1)
            return arr[0];
        int res = Integer.MAX_VALUE;
        for (int i = 1; i < n; i++) {
            res = Math.min(res, Math.max(minPages(arr, i, k - 1), sum(arr, i, n - 1)));
        }
        return res;
    }
}

```

## **Allocate Minimum Pages (DP Solution)**

```java
import java.util.*;
import java.io.*;
import java.lang.*;

class GFG { 
    
    public static void main(String args[]) 
    { 
        int arr[]={10,20,10,30};
        int n=arr.length;
        int k=2;
        
    	System.out.print(minPages(arr,n,k)); 
    } 
    
    public static int sum(int arr[],int b, int e){
        int s=0;
        for(int i=b;i<=e;i++)
            s+=arr[i];
        return s;
    }
    
    public static int minPages(int arr[],int n, int k){
        int[][] dp=new int[k+1][n+1];
        for(int i=1;i<=n;i++)
            dp[1][i]=sum(arr,0,i-1);
        for(int i=1;i<=k;i++)
            dp[i][1]=arr[0];
            
        for(int i=2;i<=k;i++){
            for(int j=2;j<=n;j++){
                int res=Integer.MAX_VALUE;
                for(int p=1;p<j;p++){
                    res=Math.min(res,Math.max(dp[i-1][p],sum(arr,p,j-1)));
                }
                dp[i][j]=res;
            }
        }
        return dp[k][n];
    }
} 
```

