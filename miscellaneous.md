# Miscellaneous

## Segment & Binary Index Tree & Disjointed&#x20;

## Sets**Segment Tree ( simple )**

```java
import java.util.*;
import java.io.*;
import java.lang.*;

class GFG {

    static int getSum(int arr[], int qs, int qe) {
        int sum = 0;

        for (int i = qs; i <= qe; i++)
            sum = sum + arr[i];

        return sum;
    }

    static void update(int arr[], int i, int newVal) {
        arr[i] = newVal;
    }

    public static void main(String args[]) {

        int arr[] = { 10, 20, 30, 40, 50 }, n = 5;

        System.out.print(getSum(arr, 0, 2) + " ");
        System.out.print(getSum(arr, 1, 3) + " ");

        update(arr, 1, 60);

        System.out.print(getSum(arr, 0, 2) + " ");
        System.out.print(getSum(arr, 1, 3) + " ");

    }

}
```

## Segment Tree Prefix Sum&#x20;

```java
import java.util.*;
import java.io.*;
import java.lang.*;

class GFG {

    static int getSum(int pre_sum[], int qs, int qe) {
        if (qs == 0)
            return pre_sum[qe];

        else
            return pre_sum[qe] - pre_sum[qs - 1];
    }

    static void update(int pre_sum[], int arr[], int i, int newVal, int n) {
        int diff = newVal - arr[i];

        for (int j = i; j < n; j++)
            pre_sum[j] += diff;
    }

    static void initialize(int pre_sum[], int arr[], int n) {
        pre_sum[0] = arr[0];

        for (int i = 1; i < n; i++) {
            pre_sum[i] = pre_sum[i - 1] + arr[i];
        }
    }

    public static void main(String args[]) {

        int arr[] = { 10, 20, 30, 40, 50 }, n = 5;

        int pre_sum[] = new int[n];

        initialize(pre_sum, arr, n);

        System.out.print(getSum(pre_sum, 0, 2) + " ");
        System.out.print(getSum(pre_sum, 1, 3) + " ");

        update(pre_sum, arr, 1, 60, n);

        System.out.print(getSum(pre_sum, 0, 2) + " ");
        System.out.print(getSum(pre_sum, 1, 3) + " ");

    }

}
```

## **Constructing Segment Tree**

```java
import java.util.*;
import java.io.*;
import java.lang.*;

class GFG {

    static int CST(int ss, int se, int si, int arr[], int tree[]) {
        if (ss == se) {
            tree[si] = arr[ss];
            return arr[ss];
        }

        int mid = (ss + se) / 2;

        tree[si] = CST(ss, mid, 2 * si + 1, arr, tree) + CST(mid + 1, se, 2 * si + 2, arr, tree);

        return tree[si];
    }

    public static void main(String args[]) {

        int arr[] = { 10, 20, 30, 40 }, n = 4;

        int tree[] = new int[4 * n];

        System.out.println(CST(0, n - 1, 0, arr, tree));

    }

}
```

## **Range Query on Segment Tree**

```java
import java.util.*;
import java.io.*;
import java.lang.*;

class GFG {

    static int CST(int ss, int se, int si, int arr[], int tree[]) {
        if (ss == se) {
            tree[si] = arr[ss];
            return arr[ss];
        }

        int mid = (ss + se) / 2;

        tree[si] = CST(ss, mid, 2 * si + 1, arr, tree) + CST(mid + 1, se, 2 * si + 2, arr, tree);

        return tree[si];
    }

    static int getSumRec(int qs, int qe, int ss, int se, int si, int tree[]) {
        if (se < qs || ss > qe)
            return 0;
        if (qs <= ss && qe >= se)
            return tree[si];

        int mid = (ss + se) / 2;

        return getSumRec(qs, qe, ss, mid, 2 * si + 1, tree) + getSumRec(qs, qe, mid + 1, se, 2 * si + 2, tree);
    }

    public static void main(String args[]) {

        int arr[] = { 10, 20, 30, 40 }, n = 4;

        int tree[] = new int[4 * n];

        CST(0, n - 1, 0, arr, tree);

        System.out.println(getSumRec(0, 2, 0, 3, 0, tree));

    }

}
```

## **Update Query on Segment Tree**

```java
import java.util.*;
import java.io.*;
import java.lang.*;

class GFG {

    static int CST(int ss, int se, int si, int arr[], int tree[]) {
        if (ss == se) {
            tree[si] = arr[ss];
            return arr[ss];
        }

        int mid = (ss + se) / 2;

        tree[si] = CST(ss, mid, 2 * si + 1, arr, tree) + CST(mid + 1, se, 2 * si + 2, arr, tree);

        return tree[si];
    }

    static void updateRec(int ss, int se, int i, int si, int diff, int tree[]) {
        if (i < ss || i > se)
            return;

        tree[si] = tree[si] + diff;

        if (se > ss) {
            int mid = (ss + se) / 2;

            updateRec(ss, mid, i, 2 * si + 1, diff, tree);
            updateRec(mid + 1, se, i, 2 * si + 2, diff, tree);

        }
    }

    public static void main(String args[]) {

        int arr[] = { 10, 20, 30, 40 }, n = 4;

        int tree[] = new int[4 * n];

        CST(0, n - 1, 0, arr, tree);

        updateRec(0, 3, 1, 0, 5, tree);

    }

}
```

## **Binary Indexed Tree ( Prefix Sum Implementation )**

```java

import java.util.*;
import java.lang.*;
import java.io.*;

class BinaryIndexedTree {

    final static int MAX = 1000;

    static int BITree[] = new int[MAX];

    int getSum(int index) {
        int sum = 0;

        index = index + 1;

        while (index > 0) {

            sum += BITree[index];

            index -= index & (-index);
        }
        return sum;
    }

    public static void updateBIT(int n, int index, int val) {

        index = index + 1;

        while (index <= n) {

            BITree[index] += val;

            index += index & (-index);
        }
    }

    void constructBITree(int arr[], int n) {

        for (int i = 1; i <= n; i++)
            BITree[i] = 0;

        for (int i = 0; i < n; i++)
            updateBIT(n, i, arr[i]);
    }

    public static void main(String args[]) {
        int freq[] = { 10, 20, 30, 40, 50, 60, 70, 80, 90 };
        int n = freq.length;
        BinaryIndexedTree tree = new BinaryIndexedTree();

        tree.constructBITree(freq, n);

        System.out.println("Sum of elements in arr[0..5]" + " is " + tree.getSum(5));

    }
}

```

## **Binary Indexed Tree ( Update Operation )**

```java

import java.util.*;
import java.lang.*;
import java.io.*;

class BinaryIndexedTree {

    final static int MAX = 1000;

    static int BITree[] = new int[MAX];

    public static void updateBIT(int n, int index, int val) {

        index = index + 1;

        while (index <= n) {

            BITree[index] += val;

            index += index & (-index);
        }
    }

    void constructBITree(int arr[], int n) {

        for (int i = 1; i <= n; i++)
            BITree[i] = 0;

        for (int i = 0; i < n; i++)
            updateBIT(n, i, arr[i]);
    }

    public static void main(String args[]) {
        int freq[] = { 10, 20, 30, 40, 50, 60, 70, 80, 90 };
        int n = freq.length;
        BinaryIndexedTree tree = new BinaryIndexedTree();

        tree.constructBITree(freq, n);

        updateBIT(n, 2, 35);

    }
}
```



## **Segment Tree ( simple )**

```java
import java.util.*;
import java.io.*;
import java.lang.*;

class GFG {

    static int getSum(int arr[], int qs, int qe) {
        int sum = 0;

        for (int i = qs; i <= qe; i++)
            sum = sum + arr[i];

        return sum;
    }

    static void update(int arr[], int i, int newVal) {
        arr[i] = newVal;
    }

    public static void main(String args[]) {

        int arr[] = { 10, 20, 30, 40, 50 }, n = 5;

        System.out.print(getSum(arr, 0, 2) + " ");
        System.out.print(getSum(arr, 1, 3) + " ");

        update(arr, 1, 60);

        System.out.print(getSum(arr, 0, 2) + " ");
        System.out.print(getSum(arr, 1, 3) + " ");

    }

}
```

## Segment Tree Prefix Sum&#x20;

```java
import java.util.*;
import java.io.*;
import java.lang.*;

class GFG {

    static int getSum(int pre_sum[], int qs, int qe) {
        if (qs == 0)
            return pre_sum[qe];

        else
            return pre_sum[qe] - pre_sum[qs - 1];
    }

    static void update(int pre_sum[], int arr[], int i, int newVal, int n) {
        int diff = newVal - arr[i];

        for (int j = i; j < n; j++)
            pre_sum[j] += diff;
    }

    static void initialize(int pre_sum[], int arr[], int n) {
        pre_sum[0] = arr[0];

        for (int i = 1; i < n; i++) {
            pre_sum[i] = pre_sum[i - 1] + arr[i];
        }
    }

    public static void main(String args[]) {

        int arr[] = { 10, 20, 30, 40, 50 }, n = 5;

        int pre_sum[] = new int[n];

        initialize(pre_sum, arr, n);

        System.out.print(getSum(pre_sum, 0, 2) + " ");
        System.out.print(getSum(pre_sum, 1, 3) + " ");

        update(pre_sum, arr, 1, 60, n);

        System.out.print(getSum(pre_sum, 0, 2) + " ");
        System.out.print(getSum(pre_sum, 1, 3) + " ");

    }

}
```

## **Constructing Segment Tree**

```java
import java.util.*;
import java.io.*;
import java.lang.*;

class GFG {

    static int CST(int ss, int se, int si, int arr[], int tree[]) {
        if (ss == se) {
            tree[si] = arr[ss];
            return arr[ss];
        }

        int mid = (ss + se) / 2;

        tree[si] = CST(ss, mid, 2 * si + 1, arr, tree) + CST(mid + 1, se, 2 * si + 2, arr, tree);

        return tree[si];
    }

    public static void main(String args[]) {

        int arr[] = { 10, 20, 30, 40 }, n = 4;

        int tree[] = new int[4 * n];

        System.out.println(CST(0, n - 1, 0, arr, tree));

    }

}
```

## **Range Query on Segment Tree**

```java
import java.util.*;
import java.io.*;
import java.lang.*;

class GFG {

    static int CST(int ss, int se, int si, int arr[], int tree[]) {
        if (ss == se) {
            tree[si] = arr[ss];
            return arr[ss];
        }

        int mid = (ss + se) / 2;

        tree[si] = CST(ss, mid, 2 * si + 1, arr, tree) + CST(mid + 1, se, 2 * si + 2, arr, tree);

        return tree[si];
    }

    static int getSumRec(int qs, int qe, int ss, int se, int si, int tree[]) {
        if (se < qs || ss > qe)
            return 0;
        if (qs <= ss && qe >= se)
            return tree[si];

        int mid = (ss + se) / 2;

        return getSumRec(qs, qe, ss, mid, 2 * si + 1, tree) + getSumRec(qs, qe, mid + 1, se, 2 * si + 2, tree);
    }

    public static void main(String args[]) {

        int arr[] = { 10, 20, 30, 40 }, n = 4;

        int tree[] = new int[4 * n];

        CST(0, n - 1, 0, arr, tree);

        System.out.println(getSumRec(0, 2, 0, 3, 0, tree));

    }

}
```

## **Update Query on Segment Tree**

```java
import java.util.*;
import java.io.*;
import java.lang.*;

class GFG {

    static int CST(int ss, int se, int si, int arr[], int tree[]) {
        if (ss == se) {
            tree[si] = arr[ss];
            return arr[ss];
        }

        int mid = (ss + se) / 2;

        tree[si] = CST(ss, mid, 2 * si + 1, arr, tree) + CST(mid + 1, se, 2 * si + 2, arr, tree);

        return tree[si];
    }

    static void updateRec(int ss, int se, int i, int si, int diff, int tree[]) {
        if (i < ss || i > se)
            return;

        tree[si] = tree[si] + diff;

        if (se > ss) {
            int mid = (ss + se) / 2;

            updateRec(ss, mid, i, 2 * si + 1, diff, tree);
            updateRec(mid + 1, se, i, 2 * si + 2, diff, tree);

        }
    }

    public static void main(String args[]) {

        int arr[] = { 10, 20, 30, 40 }, n = 4;

        int tree[] = new int[4 * n];

        CST(0, n - 1, 0, arr, tree);

        updateRec(0, 3, 1, 0, 5, tree);

    }

}
```

## **Binary Indexed Tree ( Prefix Sum Implementation )**

```java

import java.util.*;
import java.lang.*;
import java.io.*;

class BinaryIndexedTree {

    final static int MAX = 1000;

    static int BITree[] = new int[MAX];

    int getSum(int index) {
        int sum = 0;

        index = index + 1;

        while (index > 0) {

            sum += BITree[index];

            index -= index & (-index);
        }
        return sum;
    }

    public static void updateBIT(int n, int index, int val) {

        index = index + 1;

        while (index <= n) {

            BITree[index] += val;

            index += index & (-index);
        }
    }

    void constructBITree(int arr[], int n) {

        for (int i = 1; i <= n; i++)
            BITree[i] = 0;

        for (int i = 0; i < n; i++)
            updateBIT(n, i, arr[i]);
    }

    public static void main(String args[]) {
        int freq[] = { 10, 20, 30, 40, 50, 60, 70, 80, 90 };
        int n = freq.length;
        BinaryIndexedTree tree = new BinaryIndexedTree();

        tree.constructBITree(freq, n);

        System.out.println("Sum of elements in arr[0..5]" + " is " + tree.getSum(5));

    }
}

```

## **Binary Indexed Tree ( Update Operation )**

```java

import java.util.*;
import java.lang.*;
import java.io.*;

class BinaryIndexedTree {

    final static int MAX = 1000;

    static int BITree[] = new int[MAX];

    public static void updateBIT(int n, int index, int val) {

        index = index + 1;

        while (index <= n) {

            BITree[index] += val;

            index += index & (-index);
        }
    }

    void constructBITree(int arr[], int n) {

        for (int i = 1; i <= n; i++)
            BITree[i] = 0;

        for (int i = 0; i < n; i++)
            updateBIT(n, i, arr[i]);
    }

    public static void main(String args[]) {
        int freq[] = { 10, 20, 30, 40, 50, 60, 70, 80, 90 };
        int n = freq.length;
        BinaryIndexedTree tree = new BinaryIndexedTree();

        tree.constructBITree(freq, n);

        updateBIT(n, 2, 35);

    }
}
```
