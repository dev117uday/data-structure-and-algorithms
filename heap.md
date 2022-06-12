---
description: Garbage
---

# Heap

**children elements are smaller/bigger than parent**

## Types of Heaps

* Min Heap : Highest priority items assigned the lowest value
* Max Heap : Highest priority items assigned the highest value

## Applications of Heap

* Used to implement HeapSort
* Used to implement PriorityQueue

## Formulae's

* left of element : (2\*i+1)
* right of element : (2\*i+2)
* parent of element : (i-1)/2

## Binary Heap Implementation (Array)

```java
import java.util.*;
import java.io.*;
import java.lang.*;

class Main {

    public static class MinHeap {
        int arr[];
        int size;
        int capacity;

        MinHeap(int c) {
            size = 0;
            capacity = c;
            arr = new int[c];
        }

        int left(int i) {
            return (2 * i + 1);
        }

        int right(int i) {
            return (2 * i + 2);
        }

        int parent(int i) {
            return (i - 1) / 2;
        }
    }

    public static void main(String args[]) {
        MinHeap h = new MinHeap(11);

    }

}
```

## Binary Heap Insert (Array) : MinHeap

```java
import java.util.*;
import java.io.*;
import java.lang.*;

class Test {

    public static class MinHeap {
        int arr[];
        int size;
        int capacity;

        MinHeap(int c) {
            size = 0;
            capacity = c;
            arr = new int[c];
        }

        int left(int i) {
            return (2 * i + 1);
        }

        int right(int i) {
            return (2 * i + 2);
        }

        int parent(int i) {
            return (i - 1) / 2;
        }


        public void insert(int x) {
            if (size == capacity) return;
            size++;
            arr[size - 1] = x;

            for (int i = size - 1; i != 0 && arr[parent(i)] > arr[i]; ) {
                int temp = arr[i];
                arr[i] = arr[parent(i)];
                arr[parent(i)] = temp;
                i = parent(i);
            }
        }

    }

    public static void main(String args[]) {
        MinHeap h = new MinHeap(11);
        h.insert(3);
        h.insert(2);
        h.insert(15);
        h.insert(20);
    }

}
```

## Binary Heap (Heapify and Extract) : MinHeap

**Extract operation is super important**

```java
import java.util.*;
import java.io.*;
import java.lang.*;

class Test {

    public static class MinHeap {
        int arr[];
        int size;
        int capacity;

        MinHeap(int c) {
            size = 0;
            capacity = c;
            arr = new int[c];
        }

        int left(int i) {
            return (2 * i + 1);
        }

        int right(int i) {
            return (2 * i + 2);
        }

        int parent(int i) {
            return (i - 1) / 2;
        }


        public void insert(int x) {
            if (size == capacity) return;
            size++;
            arr[size - 1] = x;

            for (int i = size - 1; i != 0 && arr[parent(i)] > arr[i]; ) {
                int temp = arr[i];
                arr[i] = arr[parent(i)];
                arr[parent(i)] = temp;
                i = parent(i);
            }
        }

        public void minHeapify(int i) {
            int lt = left(i);
            int rt = right(i);
            int smallest = i;
            if (lt < size && arr[lt] < arr[i])
                smallest = lt;
            if (rt < size && arr[rt] < arr[smallest])
                smallest = rt;
            if (smallest != i) {
                int temp = arr[i];
                arr[i] = arr[smallest];
                arr[smallest] = temp;
                minHeapify(smallest);
            }
        }

        public int extractMin() {
            if (size <= 0)
                return Integer.MAX_VALUE;
            if (size == 1) {
                size--;
                return arr[0];
            }
            int temp = arr[0];
            arr[0] = arr[size - 1];
            arr[size - 1] = temp;
            size--;
            minHeapify(0);

            return arr[size];
        }

    }

    public static void main(String args[]) {
        MinHeap h = new MinHeap(11);
        h.insert(3);
        h.insert(2);
        h.insert(15);
        h.insert(20);
        System.out.print(h.extractMin());
    }

}
```

## Binary Heap (Decrease Key | Delete)

```java
import java.util.*;
import java.io.*;
import java.lang.*;

class Test {

    public static class MinHeap {
        int arr[];
        int size;
        int capacity;

        MinHeap(int c) {
            size = 0;
            capacity = c;
            arr = new int[c];
        }

        int left(int i) {
            return (2 * i + 1);
        }

        int right(int i) {
            return (2 * i + 2);
        }

        int parent(int i) {
            return (i - 1) / 2;
        }


        public void insert(int x) {
            if (size == capacity) return;
            size++;
            arr[size - 1] = x;

            for (int i = size - 1; i != 0 && arr[parent(i)] > arr[i]; ) {
                int temp = arr[i];
                arr[i] = arr[parent(i)];
                arr[parent(i)] = temp;
                i = parent(i);
            }
        }

        public void minHeapify(int i) {
            int lt = left(i);
            int rt = right(i);
            int smallest = i;
            if (lt < size && arr[lt] < arr[i])
                smallest = lt;
            if (rt < size && arr[rt] < arr[smallest])
                smallest = rt;
            if (smallest != i) {
                int temp = arr[i];
                arr[i] = arr[smallest];
                arr[smallest] = temp;
                minHeapify(smallest);
            }
        }

        public int extractMin() {
            if (size <= 0)
                return Integer.MAX_VALUE;
            if (size == 1) {
                size--;
                return arr[0];
            }
            int temp = arr[0];
            arr[0] = arr[size - 1];
            arr[size - 1] = temp;
            size--;
            minHeapify(0);

            return arr[size];
        }

        void decreaseKey(int i, int x) {
            arr[i] = x;
            while (i != 0 && arr[parent(i)] > arr[i]) {
                int temp = arr[i];
                arr[i] = arr[parent(i)];
                arr[parent(i)] = temp;
                i = parent(i);
            }
        }

        void deleteKey(int i) {
            decreaseKey(i, Integer.MIN_VALUE);
            extractMin();
        }

    }

    public static void main(String args[]) {
        MinHeap h = new MinHeap(11);
        h.insert(3);
        h.insert(2);
        h.deleteKey(0);
        h.insert(15);
        h.insert(20);
        System.out.println(h.extractMin());
        h.decreaseKey(2, 1);
        System.out.println(h.extractMin());
    }

}
```

## Binary Heap ( Build Heap ) IMPORTANT

```java
import java.util.*;
import java.io.*;
import java.lang.*;

class Test {

    public static class MinHeap {
        int arr[];
        int size;
        int capacity;

        MinHeap(int c) {
            size = 0;
            capacity = c;
            arr = new int[c];
        }

        int left(int i) {
            return (2 * i + 1);
        }

        int right(int i) {
            return (2 * i + 2);
        }

        int parent(int i) {
            return (i - 1) / 2;
        }

        public void minHeapify(int i) {
            int lt = left(i);
            int rt = right(i);
            int smallest = i;
            if (lt < size && arr[lt] < arr[i])
                smallest = lt;
            if (rt < size && arr[rt] < arr[smallest])
                smallest = rt;
            if (smallest != i) {
                int temp = arr[i];
                arr[i] = arr[smallest];
                arr[smallest] = temp;
                minHeapify(smallest);
            }
        }
        // IMPORTANT
        public void buildHeap() {
            for (int i = (size - 2) / 2; i >= 0; i--)
                minHeapify(i);
        }

    }

    public static void main(String args[]) {
        MinHeap h = new MinHeap(11);
    }

}
```

## Heap Sort

```java
import java.lang.*;

public class Main {
    public void buildheap(int arr[], int n) {
        for (int i = n / 2 - 1; i >= 0; i--)
            heapify(arr, n, i);
    }

    public void sort(int arr[]) {
        int n = arr.length;

        buildheap(arr, n);

        for (int i = n - 1; i > 0; i--) {

            int temp = arr[0];
            arr[0] = arr[i];
            arr[i] = temp;

            heapify(arr, i, 0);
        }
    }

    void heapify(int arr[], int n, int i) {
        int largest = i;
        int l = 2 * i + 1;
        int r = 2 * i + 2;

        if (l < n && arr[l] > arr[largest])
            largest = l;

        if (r < n && arr[r] > arr[largest])
            largest = r;

        if (largest != i) {
            int swap = arr[i];
            arr[i] = arr[largest];
            arr[largest] = swap;

            heapify(arr, n, largest);
        }
    }

    static void printArray(int arr[]) {
        int n = arr.length;
        for (int i = 0; i < n; ++i)
            System.out.print(arr[i] + " ");
        System.out.println();
    }

    public static void main(String args[]) {
        int arr[] = {12, 11, 13, 5, 6, 7};
        int n = arr.length;

        Main ob = new Main();
        ob.sort(arr);

        System.out.println("Sorted array is");
        printArray(arr);
    }
}
```

## Priority Queue (Min Heap Edition)

```java
// Java program to demonstrate working of
// PriorityQueue in Java

import java.util.*;

class Main {
    public static void main(String args[]) {
        // Creating empty priority queue
        PriorityQueue<Integer> pq = new PriorityQueue<Integer>();

        // Adding items to the pQueue using add()
        pq.add(10);
        pq.add(20);
        pq.add(15);


        // Printing the top element of PriorityQueue
        System.out.println(pq.peek());

        // Printing the top element and removing it
        // from the PriorityQueue container
        System.out.println(pq.poll());


        // Printing the top element again
        System.out.println(pq.peek());
    }
}
```

## Priority Queue (Max Heap Edition)

```java
// Java program to demonstrate working of
// PriorityQueue in Java

import java.util.*;

class Main {
    public static void main(String args[]) {
        // Creating empty priority queue
        PriorityQueue<Integer> pq
                = new PriorityQueue<Integer>(
                Collections.reverseOrder());

        // Adding items to the pQueue using add()
        pq.add(10);
        pq.add(20);
        pq.add(15);

        // Above PriorityQueue is stored as following
        //       20
        //      /  \
        //    10    15

        // Printing the top element of PriorityQueue
        System.out.println(pq.peek());

        // Printing the top element and removing it
        // from the PriorityQueue container
        System.out.println(pq.poll());

        // Post poll() PriorityQueue looks like
        //       15
        //      /  
        //    10   

        // Printing the top element again
        System.out.println(pq.peek());
    }
}
```

## K-Sorted Array

```java
import java.util.*;
import java.io.*;
import java.lang.*;

class Main {
    private static void sortK(int[] arr, int n, int k) {

        PriorityQueue<Integer> pq = new PriorityQueue<>();

        for (int i = 0; i < k + 1; i++) {
            pq.add(arr[i]);
        }

        int index = 0;
        for (int i = k + 1; i < n; i++) {
            arr[index++] = pq.peek();
            pq.poll();
            pq.add(arr[i]);
        }

        while (pq.isEmpty() == false) {
            arr[index++] = pq.poll();
        }

    }

    private static void printArray(int[] arr, int n) {
        for (int i = 0; i < n; i++)
            System.out.print(arr[i] + " ");
    }

    public static void main(String[] args) {
        int k = 3;
        int arr[] = {2, 6, 3, 12, 56, 8};
        int n = arr.length;
        sortK(arr, n, k);
        System.out.println("Following is sorted array");
        printArray(arr, n);
    }
}
```

## Buy Maximum Items with the given sum

```java
import java.util.*;
import java.io.*;
import java.lang.*;

class Main {

    public static void main(String args[]) {
        int n = 5;
        int cost[] = new int[]{1, 12, 5, 111, 200};
        int sum = 10;

        PriorityQueue<Integer> pq = new PriorityQueue<Integer>();

        int res = 0;
        for (int i = 0; i < n; i++)
            pq.add(cost[i]);

        for (int i = 0; i < n; i++) {
            if (pq.peek() <= sum) {
                sum -= pq.poll();
                res++;
            } else {
                break;
            }
        }
        System.out.print(res);

    }

}
```

## Kth Largest Element

```java
import java.io.*;
import java.util.*;

class GFG {

    public static void firstKElements(int arr[], int n, int k) {

        PriorityQueue<Integer> minHeap = new PriorityQueue<>();
        for (int i = 0; i < k; i++) {
            minHeap.add(arr[i]);
        }
        for (int i = k; i < n; i++) {
            if (minHeap.peek() > arr[i])
                continue;
            else {
                minHeap.poll();
                minHeap.add(arr[i]);
            }
        }

        Iterator iterator = minHeap.iterator();

        while (iterator.hasNext()) {
            System.out.print(iterator.next() + " ");
        }
    }

    public static void main(String[] args) {
        int arr[] = {11, 3, 2, 1, 15, 5, 4, 45, 88, 96, 50, 45};

        int size = arr.length;

        int k = 3;

        firstKElements(arr, size, k);
    }
}
```

## K Closet Element

```java
import java.io.*;
import java.util.*;

class GFG {

    public static void firstKElements(int arr[], int n, int k) {

        PriorityQueue<Integer> minHeap = new PriorityQueue<>();
        for (int i = 0; i < k; i++) {
            minHeap.add(arr[i]);
        }
        for (int i = k; i < n; i++) {
            if (minHeap.peek() > arr[i])
                continue;
            else {
                minHeap.poll();
                minHeap.add(arr[i]);
            }
        }

        Iterator iterator = minHeap.iterator();

        while (iterator.hasNext()) {
            System.out.print(iterator.next() + " ");
        }
    }

    public static void main(String[] args) {
        int arr[] = {11, 3, 2, 1, 15, 5, 4, 45, 88, 96, 50, 45};

        int size = arr.length;

        int k = 3;

        firstKElements(arr, size, k);
    }
}
```

## Merge K Sorted Arrays

```java
import java.io.*;
import java.util.*;

class Triplet implements Comparable<Triplet> {
    int val, aPos, vPos;

    Triplet(int v, int ap, int vp) {
        val = v;
        aPos = ap;
        vPos = vp;
    }

    public int compareTo(Triplet t) {
        if (val <= t.val) return -1;
        else return 1;
    }
}

class GFG {


    public static List<Integer> mergeArr(ArrayList<ArrayList<Integer>> arr) {
        List<Integer> res = new ArrayList<Integer>();
        PriorityQueue<Triplet> pq = new PriorityQueue<Triplet>();

        for (int i = 0; i < arr.size(); i++)
            pq.add(new Triplet(arr.get(i).get(0), i, 0));

        while (pq.isEmpty() == false) {
            Triplet curr = pq.poll();
            res.add(curr.val);
            int ap = curr.aPos;
            int vp = curr.vPos;
            if (vp + 1 < arr.get(ap).size()) {
                pq.add(new Triplet(arr.get(ap).get(vp + 1), ap, vp + 1));
            }
        }

        return res;
    }

    public static void main(String[] args) {
        ArrayList<ArrayList<Integer>> arr = new ArrayList<ArrayList<Integer>>();

        ArrayList<Integer> a1 = new ArrayList<Integer>();
        a1.add(10);
        a1.add(20);
        a1.add(30);
        arr.add(a1);

        ArrayList<Integer> a2 = new ArrayList<Integer>();
        a2.add(5);
        a2.add(15);
        arr.add(a2);

        ArrayList<Integer> a3 = new ArrayList<Integer>();
        a3.add(1);
        a3.add(9);
        a3.add(11);
        a3.add(18);
        arr.add(a3);

        List<Integer> res = mergeArr(arr);

        System.out.println("Merged array is ");
        for (int x : res)
            System.out.print(x + " ");
    }
}
```

## Median of Stream

```java
import java.io.*;
import java.util.*;

class Node {
    double data;
    Node left, right;
    int lCount;
    Node(double x)
    {
        data = x;
        left = right = null;
        lCount = 0;
    }
}

class GFG{

public static void printMedians(int arr[],int n){
    PriorityQueue<Integer> g=new PriorityQueue<Integer>();
    PriorityQueue<Integer> s=new PriorityQueue<Integer>(Collections.reverseOrder());
    s.add(arr[0]);
    System.out.print(arr[0]+" ");
    for(int i=1;i<n;i++){
        int x=arr[i];
        if(s.size()>g.size())
        {
            if(s.peek()>x){
                g.add(s.poll());
                s.add(x);
            }else g.add(x);
            System.out.print(((double)(s.peek()+g.peek())/2)+" ");
        }else{
            if(x<=s.peek()){
                s.add(x);
            }else{
                g.add(x);
                s.add(g.poll());
            }
            System.out.print(s.peek()+" ");
        }
    }
}

    public static void main(String args[])
    {
        int keys[] = { 12, 15, 10, 5, 8, 7, 16};

        printMedians(keys,7);
    }
}
```
