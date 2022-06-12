---
description: overflow
---

# Stack

### Implement Queue using Stack

```java
class MyQueue {
	Stack stack;
	int top;

	public MyQueue() {
		stack = new Stack();
	}

	public void push(int x) {
		Stack temp = new Stack();
		if (stack.isEmpty()) {
			stack.push(x);
		} else {
			while (!stack.isEmpty()) {
				temp.push(stack.pop());
			}
			stack.push(x);
			while (!temp.isEmpty()) {
				stack.push(temp.pop());
			}
		}
	}

	public int pop() {
		return (int) stack.pop();
	}

	public int peek() {
		return (int) stack.peek();
	}

	public boolean empty() {
		return stack.isEmpty();
	}
}
```

### Balanced Parenthesis

```java
import java.util.Stack;

class Solution {

	static public boolean isValid(String s) {
		Stack<Character> stck = new Stack<>();

		for (char bracket : s.toCharArray()) {
			if (bracket == '(' || bracket == '[' || bracket == '{') {
				stck.push(bracket);
			} else {
				try {
					char lstBracker = stck.peek();
					if (lstBracker == '(' && bracket == ')') {
						stck.pop();
					} else if (lstBracker == '[' && bracket == ']') {
						stck.pop();
					} else if (lstBracker == '{' && bracket == '}') {
						stck.pop();
					} else {
						return false;
					}
				} catch (Exception e) {
					return false;
				}
			}
		}

		return stck.size() == 0 ? true : false;

	}

	public static void main(String[] args) {
		System.out.println(isValid("{()}[]"));
	}
}
```

### Two stacks in an array(Useless Question)

```java
        import java.io.*;
        import java.util.*;

class TwoStacks {
    int cap;
    int top1, top2;
    int arr[];

    TwoStacks(int n) {
        arr = new int[n];
        cap = n;
        top1 = -1;
        top2 = cap;
    }

    void push1(int x) {
        if (top1 < top2 - 1) {
            top1++;
            arr[top1] = x;
        } else {
            System.out.println("Stack Overflow");
            System.exit(1);
        }
    }

    void push2(int x) {
        if (top1 < top2 - 1) {
            top2--;
            arr[top2] = x;
        } else {
            System.out.println("Stack Overflow");
            System.exit(1);
        }
    }

    int pop1() {
        if (top1 >= 0) {
            int x = arr[top1];
            top1--;
            return x;
        } else {
            System.out.println("Stack Underflow");
            System.exit(1);
        }
        return 0;
    }

    int pop2() {
        if (top2 < cap) {
            int x = arr[top2];
            top2++;
            return x;
        } else {
            System.out.println("Stack Underflow");
            System.exit(1);
        }
        return 0;
    }
}

class Main {

    public static void main(String[] args) {

        TwoStacks ts = new TwoStacks(5);
        ts.push1(5);
        ts.push2(10);
        ts.push2(15);
        ts.push1(11);
        ts.push2(7);
        System.out.println("Popped element from stack1 is: " + ts.pop1());
        ts.push2(40);
        System.out.println("Popped element from stack2 is: " + ts.pop2());

    }

}
```

### K Stacks in an array(UseLess Question)

```java
class kStacks {
    int arr[];
    int top[];
    int next[];
    int cap, k;
    int freeTop;

    kStacks(int k1, int n) {
        k = k1;
        cap = n;
        arr = new int[cap];
        top = new int[k];
        next = new int[cap];

        for (int i = 0; i < k; i++)
            top[i] = -1;

        freeTop = 0;
        for (int i = 0; i < cap - 1; i++)
            next[i] = i + 1;
        next[cap - 1] = -1;
    }

    boolean isFull() {
        return (freeTop == -1);
    }

    boolean isEmpty(int sn) {
        return (top[sn] == -1);
    }

    void push(int x, int sn) {
        if (isFull()) {
            System.out.print("\nStack Overflow\n");
            return;
        }

        int i = freeTop;
        freeTop = next[i];
        next[i] = top[sn];
        top[sn] = i;
        arr[i] = x;
    }

    int pop(int sn) {
        if (isEmpty(sn)) {
            System.out.print("\nStack Underflow\n");
            return Integer.MAX_VALUE;
        }

        int i = top[sn];
        top[sn] = next[i];
        next[i] = freeTop;
        freeTop = i;
        return arr[i];
    }

}

class Main {

    public static void main(String[] args) {

        int k = 3, n = 10;
        kStacks ks = new kStacks(k, n);

        ks.push(15, 2);
        ks.push(45, 2);

        ks.push(17, 1);
        ks.push(49, 1);
        ks.push(39, 1);

        ks.push(11, 0);
        ks.push(9, 0);
        ks.push(7, 0);

        System.out.println("Popped element from stack 2 is " + ks.pop(2));
        System.out.println("Popped element from stack 1 is " + ks.pop(1));
        System.out.println("Popped element from stack 0 is " + ks.pop(0));

    }

}
```

### Stock Span Problem

```java
        import java.io.*;
        import java.util.*;

class GFG {

    public static void printSpan(int arr[], int n) {
        Stack<Integer> s = new Stack<>();
        s.add(0);
        System.out.print(1 + " ");
        for (int i = 1; i < n; i++) {
            while (s.isEmpty() == false && arr[s.peek()] <= arr[i]) {
                s.pop();
            }
            int span = s.isEmpty() ? i + 1 : i - s.peek();
            System.out.print(span + " ");
            s.push(i);
        }
    }

    public static void main(String[] args) {

        int[] arr = new int[]{18, 12, 13, 14, 11, 16};

        printSpan(arr, arr.length);

    }

}
```

### Previous Greater Element

```java
        import java.io.*;
        import java.util.*;

class GFG {

    public static void printPrevGreater(int arr[], int n) {

        Stack<Integer> s = new Stack<>();
        s.add(arr[0]);
        for (int i = 0; i < n; i++) {
            while (s.isEmpty() == false && s.peek() <= arr[i])
                s.pop();
            int pg = s.isEmpty() ? -1 : s.peek();
            System.out.print(pg + " ");
            s.add(arr[i]);
        }
    }

    public static void main(String[] args) {

        int[] arr = new int[]{20, 30, 10, 5, 15};

        printPrevGreater(arr, arr.length);

    }

}
```

### Next Greater Element

```java
import java.io.*;
import java.util.*;

class GFG {

    public static ArrayList<Integer> nextGreater(int arr[],int n){
        ArrayList<Integer> v=new ArrayList<>();
        Stack <Integer> s=new Stack<>();
        s.add(arr[n-1]);v.add(-1);
        for(int i=n-2;i>=0;i--){
            while(s.isEmpty()==false && s.peek()<=arr[i])
                s.pop();
            int ng=s.isEmpty()?-1:s.peek();
            v.add(ng);
            s.add(arr[i]);
        }
        Collections.reverse(v);
        return v;
    }
    public static void main (String[] args) {

        int[] arr=new int[]{5,15,10,8,6,12,9,18};

        for(int x: nextGreater(arr,arr.length)){
            System.out.print(x + " ");   
        }  

    }

}
```

### Largest Rectangular Area in a Histogram (Part 1)

```java
import java.io.*;
import java.util.*;

class GFG {

    public static int getMaxArea(int arr[], int n) {
        int res = 0;
        int[] ps = new int[n];
        int[] ns = new int[n];

        Stack<Integer> s = new Stack<>();
        s.add(0);
        for (int i = 0; i < n; i++) {
            while (s.isEmpty() == false && arr[s.peek()] >= arr[i])
                s.pop();
            int pse = s.isEmpty() ? -1 : s.peek();
            ps[i] = pse;
            s.push(i);
        }

        while (s.isEmpty() == false) {
            s.pop();
        }

        s.push(n - 1);
        for (int i = n - 1; i > 0; i--) {
            while (s.isEmpty() == false && arr[s.peek()] >= arr[i])
                s.pop();
            int nse = s.isEmpty() ? n : s.peek();
            ns[i] = nse;
            s.add(i);
        }

        for (int i = 0; i < n; i++) {
            int curr = arr[i];
            curr += (i - ps[i] - 1) * arr[i];
            curr += (ns[i] - i - 1) * arr[i];
            res = Math.max(res, curr);
        }
        return res;

    }

    public static void main(String[] args) {
        int[] arr = new int[]{6, 2, 5, 4, 1, 5, 6};
        System.out.print("Maximum Area: " + getMaxArea(arr, arr.length));
    }
}
```

### Largest Rectangular Area in a Histogram (Part 2)

```java
import java.io.*;
import java.util.*;

class GFG {

    public static int getMaxArea(int arr[], int n) {
        Stack<Integer> s = new Stack<>();
        int res = 0;
        int tp;
        int curr;
        for (int i = 0; i < n; i++) {
            while (s.isEmpty() == false && arr[s.peek()] >= arr[i]) {
                tp = s.peek();
                s.pop();
                curr = arr[tp] * (s.isEmpty() ? i : i - s.peek() - 1);
                res = Math.max(res, curr);
            }
            s.add(i);
        }
        while (s.isEmpty() == false) {
            tp = s.peek();
            s.pop();
            curr = arr[tp] * (s.isEmpty() ? n : n - s.peek() - 1);
            res = Math.max(res, curr);
        }

        return res;

    }

    public static void main(String[] args) {
        int[] arr = new int[]{6, 2, 5, 4, 1, 5, 6};
        System.out.print("Maximum Area: " + getMaxArea(arr, arr.length));
    }
}
```

### Largest Rectangle with all 1's (in a matrix)

```java
import java.io.*;
import java.util.*;

class GFG {

    public static int largestHist(int R, int C, int arr[]) {
        Stack<Integer> result = new Stack<Integer>();

        int top_val;
        int max_area = 0;
        int area = 0;

        int i = 0;
        while (i < C) {
            if (result.empty() || arr[result.peek()] <= arr[i])
                result.push(i++);

            else {

                top_val = arr[result.peek()];
                result.pop();
                area = top_val * i;

                if (!result.empty())
                    area = top_val * (i - result.peek() - 1);
                max_area = Math.max(area, max_area);
            }
        }

        while (!result.empty()) {
            top_val = arr[result.peek()];
            result.pop();
            area = top_val * i;
            if (!result.empty())
                area = top_val * (i - result.peek() - 1);

            max_area = Math.max(area, max_area);
        }
        return max_area;
    }

    static int maxRectangle(int R, int C, int mat[][]) {
        int res = largestHist(R, C, mat[0]);

        for (int i = 1; i < R; i++) {

            for (int j = 0; j < C; j++)

                if (mat[i][j] == 1)
                    mat[i][j] += mat[i - 1][j];

            res = Math.max(res, largestHist(R, C, mat[i]));
        }

        return res;
    }

    public static void main(String[] args) {
        int R = 4;
        int C = 4;

        int A[][] = {
                {0, 1, 1, 0},
                {1, 1, 1, 1},
                {1, 1, 1, 1},
                {1, 1, 0, 0},
        };
        System.out.print("Area of maximum rectangle is " + maxRectangle(R, C, A));
    }
}
```

### Stack with getMin() in O(1)

```java
import java.io.*;
import java.util.*;

class MyStack {

    Stack<Integer> ms;
    Stack<Integer> as;

    MyStack(){
        ms=new Stack<>();
        as=new Stack<>();
    }

void push(int x) {

      if(ms.isEmpty() ) {
          ms.add(x);as.add(x);return;
      }

      ms.add(x);

      if(as.peek()>=ms.peek())
        as.add(x);
   }

void pop() {

    if(as.peek()==ms.peek())
        as.pop();
    ms.pop();

   }

int top() {
     return ms.peek();
   }

int getMin() {
      return as.peek();
   }
}

class GFG {

    public static void main(String[] args) 
    { 
        MyStack s=new MyStack();;
        s.push(4);
        s.push(5);
        s.push(8);
        s.push(1);
        s.pop();

        System.out.print(" Minimum Element from Stack: " + s.getMin() );

    } 
}
```

### Design a Stack with getMin() in O(1) Space

#### Assuming all Elements Positive

```java
import java.io.*;
import java.util.*;

class MyStack {

    Stack<Integer> s;
    int min;

    MyStack() {
        s = new Stack<>();
    }

    void push(int x) {

        if (s.isEmpty()) {
            min = x;
            s.add(x);
        } else if (x <= min) {
            s.add(x - min);
            min = x;
        } else {
            s.add(x);
        }
    }

    int pop() {

        int t = s.peek();
        s.pop();
        if (t <= 0) {
            int res = min;
            min = min - t;
            return res;
        } else {
            return t;
        }
    }

    int peek() {
        int t = s.peek();
        return ((t <= 0) ? min : t);
    }

    int getMin() {
        return min;
    }
}

class GFG {

    public static void main(String[] args) {
        MyStack s = new MyStack();
        ;
        s.push(4);
        s.push(5);
        s.push(8);
        s.push(1);
        s.pop();

        System.out.print(" Minimum Element from Stack: " + s.getMin());
    }
}
```

#### Handles Negatives

```java
import java.io.*;
import java.util.*;

class MyStack {

    Stack<Integer> s;
    int min;

    MyStack(){
        s=new Stack<>();
    }

    void push(int x) {

        if(s.isEmpty() ) {
            min=x;
            s.add(x);
        }
        else if(x<=min){
            s.add(2*x-min);
            min=x;
        }else{
            s.add(x);
        }
    }

    int pop() {

        int t=s.peek();s.pop();
        if(t<=min){
            int res=min;
            min=2*min-t;
            return res;
        }else{
            return t;
        }
    }

    int peek() {
        int t=s.peek();
        return ((t<=min)? min : t);
    }

    int getMin() {
        return min;
    }
}

class GFG {

    public static void main(String[] args)
    {
        MyStack s=new MyStack();;
        s.push(4);
        s.push(5);
        s.push(8);
        s.push(1);
        s.pop();

        System.out.print(" Minimum Element from Stack: " + s.getMin() );
    }
}
```
