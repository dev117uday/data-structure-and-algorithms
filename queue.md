---
description: FIFO
---

# Queue

## Implementation of Queue using Array

#### Special trick (in order to maintain queue in array, make it circular by using %capacity)

```java
import java.lang.*;

class Queue {
    int front, rear, size;
    int capacity;
    int[] array;

    public Queue(int capacity) {
        this.capacity = capacity;
        front = this.size = 0;
        rear = capacity - 1;
        array = new int[this.capacity];
    }

    boolean isFull(Queue queue) {
        return (queue.size == queue.capacity);
    }

    boolean isEmpty(Queue queue) {
        return (queue.size == 0);
    }

    void enqueue(int item) {
        if (isFull(this))
            return;
        this.rear = (this.rear + 1)
                % this.capacity;
        this.array[this.rear] = item;
        this.size = this.size + 1;
        System.out.println(item
                + " enqueued to queue");
    }

    int dequeue() {
        if (isEmpty(this))
            return Integer.MIN_VALUE;

        int item = this.array[this.front];
        this.front = (this.front + 1)
                % this.capacity;
        this.size = this.size - 1;
        return item;
    }

    int front() {
        if (isEmpty(this))
            return Integer.MIN_VALUE;

        return this.array[this.front];
    }

    int rear() {
        if (isEmpty(this))
            return Integer.MIN_VALUE;

        return this.array[this.rear];
    }
}


public class Main {
    public static void main(String[] args) {
        Queue queue = new Queue(1000);

        queue.enqueue(10);
        queue.enqueue(20);
        queue.enqueue(30);
        queue.enqueue(40);

        System.out.println(queue.dequeue()
                + " dequeued from queue\n");

        System.out.println("Front item is "
                + queue.front());

        System.out.println("Rear item is "
                + queue.rear());
    }
}
```

## Implementing stack using queue

```java
import java.util.*;

class Main {

    static class Stack {

        static Queue<Integer> q1 = new LinkedList<Integer>();
        static Queue<Integer> q2 = new LinkedList<Integer>();


        static int curr_size;

        Stack() {
            curr_size = 0;
        }

        static void push(int x) {
            curr_size++;


            q2.add(x);


            while (!q1.isEmpty()) {
                q2.add(q1.peek());
                q1.remove();
            }


            Queue<Integer> q = q1;
            q1 = q2;
            q2 = q;
        }

        static void pop() {


            if (q1.isEmpty())
                return;
            q1.remove();
            curr_size--;
        }

        static int top() {
            if (q1.isEmpty())
                return -1;
            return q1.peek();
        }

        static int size() {
            return curr_size;
        }
    }


    public static void main(String[] args) {
        Stack s = new Stack();
        s.push(10);
        s.push(5);
        s.push(15);
        s.push(20);

        System.out.println("current size: " + s.size());
        System.out.println(s.top());
        s.pop();
        System.out.println(s.top());
        s.pop();
        System.out.println(s.top());

        System.out.println("current size: " + s.size());
    }
}
```

## Reversing a Queue

### Recursively

```java
import java.util.LinkedList;
import java.util.*;


public class Main {


    static void Print(Queue<Integer> q) {
        for (Integer x : q)
            System.out.print(x + " ");
    }


    static void reverse(Queue<Integer> q) {
        if (q.isEmpty())
            return;

        int x = q.peek();
        q.remove();

        reverse(q);
        q.add(x);

    }


    public static void main(String args[]) {
        Queue<Integer> queue = new LinkedList<Integer>();
        queue.add(12);
        queue.add(5);
        queue.add(15);
        queue.add(20);

        reverse(queue);
        Print(queue);
    }
}
```

## Reversing a Queue

### Iteratively

```java
import java.util.LinkedList;
import java.util.Queue;
import java.util.Stack;


public class Main {

    static Queue<Integer> queue;


    static void Print() {
        for (Integer x : queue)
            System.out.print(x + " ");
    }


    static void reversequeue() {
        Stack<Integer> stack = new Stack<>();
        while (!queue.isEmpty()) {
            stack.add(queue.peek());
            queue.remove();
        }
        while (!stack.isEmpty()) {
            queue.add(stack.peek());
            stack.pop();
        }
    }


    public static void main(String args[]) {
        queue = new LinkedList<Integer>();
        queue.add(12);
        queue.add(5);
        queue.add(15);
        queue.add(20);

        reversequeue();
        Print();
    }
}
```

## Generate numbers with given digits

```java
import java.util.LinkedList;
import java.util.*;


public class Main {


    static void printFirstN(int n) {
        Queue<String> q = new LinkedList<>();

        q.add("5");
        q.add("6");

        for (int i = 0; i < n; i++) {
            String curr = q.poll();

            System.out.print(curr + " ");

            q.add(curr + "5");
            q.add(curr + "6");
        }

    }


    public static void main(String args[]) {
        int n = 5;

        printFirstN(n);
    }
}
```
