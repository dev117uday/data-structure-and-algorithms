# Binary Search Tree

### Populating Next Right Pointers in Each Node

```java
class Solution {
    public Node connect(Node root) {
        Queue<Node> q=new LinkedList<>();
        if(root==null){
            return null;
        }
        q.add(root);
        while(!q.isEmpty()){
          int size=q.size();
          for(int i=1;i<=size;i++){
              Node curr=q.remove();
              if(i==size){
                 curr.next=null; 
              }else{
                 curr.next=q.peek(); 
              }
             
              if(curr.left!=null){
                  q.add(curr.left);
                  q.add(curr.right);
              }
          }   
        }
        
        return root;
    }
}
```

### Binary Tree Level Order Traversal

```java
class Solution {
    ArrayList<List<Integer>> list = new ArrayList<>();
    public List<List<Integer>> levelOrder(TreeNode root) {
        if(root==null) return list;
        Queue<TreeNode> q = new LinkedList<>();
        q.add(root);
        while(!q.isEmpty()){
            int size = q.size(); 
            ArrayList<Integer> levelElement = new ArrayList<>(); 
            for(int i =0;i<size;i++){
                TreeNode node = q.remove();
                levelElement.add(node.val);
                if(node.left!=null) q.add(node.left);
                if(node.right!=null) q.add(node.right);
            }
            list.add(levelElement);
        }
        return list;
    }
}
```

### Search in BST

```java
import java.util.*;
import java.io.*;
import java.lang.*;

class Node {
    int key;
    Node left;
    Node right;

    Node(int k) {
        key = k;
        left = right = null;
    }
}


class Main {

    public static void main(String args[]) {
        Node root = new Node(15);
        root.left = new Node(5);
        root.left.left = new Node(3);
        root.right = new Node(20);
        root.right.left = new Node(18);
        root.right.left.left = new Node(16);
        root.right.right = new Node(80);
        int x = 16;

        if (search(root, x))
            System.out.print("Found");
        else
            System.out.print("Not Found");
    }

    public static boolean search(Node root, int x) {
        if (root == null)
            return false;
        if (root.key == x)
            return true;
        else if (root.key > x) {
            return search(root.left, x);
        } else {
            return search(root.right, x);
        }
    }
}
```

### Search in BST ( recursively )

```java
import java.util.*;
import java.io.*;
import java.lang.*;

class Node {
    int key;
    Node left;
    Node right;

    Node(int k) {
        key = k;
        left = right = null;
    }
}


class Main {

    public static void main(String args[]) {
        Node root = new Node(15);
        root.left = new Node(5);
        root.left.left = new Node(3);
        root.right = new Node(20);
        root.right.left = new Node(18);
        root.right.left.left = new Node(16);
        root.right.right = new Node(80);
        int x = 16;

        if (search(root, x))
            System.out.print("Found");
        else
            System.out.print("Not Found");
    }

    public static boolean search(Node root, int x) {
        while (root != null) {
            if (root.key == x)
                return true;
            else if (root.key < x)
                root = root.right;
            else
                root = root.left;
        }
        return false;
    }
}
```

## Insert BST ( Recursively )

```java
import java.util.*;
import java.io.*;
import java.lang.*;

class Node {
    int key;
    Node left;
    Node right;

    Node(int k) {
        key = k;
        left = right = null;
    }
}


class Main {

    public static void main(String args[]) {
        Node root = new Node(10);
        root.left = new Node(5);
        root.right = new Node(15);
        root.right.left = new Node(12);
        root.right.right = new Node(18);
        int x = 20;

        root = insert(root, x);
        inorder(root);
    }

    public static Node insert(Node root, int x) {
        if (root == null)
            return new Node(x);
        else if (root.key < x)
            root.right = insert(root.right, x);
        else if (root.key > x)
            root.left = insert(root.left, x);
        return root;
    }

    public static void inorder(Node root) {
        if (root != null) {
            inorder(root.left);
            System.out.print(root.key + " ");
            inorder(root.right);
        }
    }
}
```

## Insert in BST ( Iteratively )

```java
import java.util.*;
import java.io.*;
import java.lang.*;

class Node {
    int key;
    Node left;
    Node right;

    Node(int k) {
        key = k;
        left = right = null;
    }
}


class Main {

    public static void main(String args[]) {
        Node root = new Node(10);
        root.left = new Node(5);
        root.right = new Node(15);
        root.right.left = new Node(12);
        root.right.right = new Node(18);
        int x = 20;

        root = insert(root, x);
        inorder(root);
    }

    public static Node insert(Node root, int x) {
        Node temp = new Node(x);
        Node parent = null, curr = root;
        while (curr != null) {
            parent = curr;
            if (curr.key > x)
                curr = curr.left;
            else if (curr.key < x)
                curr = curr.right;
            else
                return root;
        }
        if (parent == null)
            return temp;
        if (parent.key > x)
            parent.left = temp;
        else
            parent.right = temp;
        return root;
    }

    public static void inorder(Node root) {
        if (root != null) {
            inorder(root.left);
            System.out.print(root.key + " ");
            inorder(root.right);
        }
    }
}
```

## Delete in BST

```java
import java.util.*;
import java.io.*;
import java.lang.*;

class Node {
    int key;
    Node left;
    Node right;

    Node(int k) {
        key = k;
        left = right = null;
    }
}


class Main {

    public static void main(String args[]) {
        Node root = new Node(10);
        root.left = new Node(5);
        root.right = new Node(15);
        root.right.left = new Node(12);
        root.right.right = new Node(18);
        int x = 15;

        root = delNode(root, x);
        inorder(root);
    }

    public static Node getSuccessor(Node curr) {
        curr = curr.right;
        while (curr != null && curr.left != null)
            curr = curr.left;
        return curr;
    }

    public static Node delNode(Node root, int x) {
        if (root == null)
            return root;
        if (root.key > x)
            root.left = delNode(root.left, x);
        else if (root.key < x)
            root.right = delNode(root.right, x);
        else {
            if (root.left == null) {
                return root.right;
            } else if (root.right == null) {
                return root.left;
            } else {
                Node succ = getSuccessor(root);
                root.key = succ.key;
                root.right = delNode(root.right, succ.key);
            }
        }
        return root;
    }

    public static void inorder(Node root) {
        if (root != null) {
            inorder(root.left);
            System.out.print(root.key + " ");
            inorder(root.right);
        }
    }
}
```

## Floor in BST

```java
import java.util.*;
import java.io.*;
import java.lang.*;

class Node {
    int key;
    Node left;
    Node right;

    Node(int k) {
        key = k;
        left = right = null;
    }
}


class Main {

    public static void main(String args[]) {
        Node root = new Node(15);
        root.left = new Node(5);
        root.left.left = new Node(3);
        root.right = new Node(20);
        root.right.left = new Node(18);
        root.right.left.left = new Node(16);
        root.right.right = new Node(80);
        int x = 17;

        System.out.print("Floor: " + (floor(root, 17).key));
    }

    public static Node floor(Node root, int x) {
        Node res = null;
        while (root != null) {
            if (root.key == x)
                return root;
            else if (root.key > x)
                root = root.left;
            else {
                res = root;
                root = root.right;
            }
        }
        return res;
    }
}
```

## Ceil in BST

```java
import java.util.*;
import java.io.*;
import java.lang.*;

class Node {
    int key;
    Node left;
    Node right;

    Node(int k) {
        key = k;
        left = right = null;
    }
}

class Main {

    public static void main(String args[]) {
        Node root = new Node(15);
        root.left = new Node(5);
        root.left.left = new Node(3);
        root.right = new Node(20);
        root.right.left = new Node(18);
        root.right.left.left = new Node(16);
        root.right.right = new Node(80);
        int x = 17;

        System.out.print("Ceil: " + (ceil(root, 17).key));
    }

    public static Node ceil(Node root, int x) {
        Node res = null;
        while (root != null) {
            if (root.key == x)
                return root;
            else if (root.key < x)
                root = root.right;
            else {
                res = root;
                root = root.left;
            }
        }
        return res;
    }
}
```

## Revisit AVL Tree

## Revisit Red Black Tree

## TreeSet In java

### Add | Contains | Iterator

```java
import java.util.*;

class TreeSetExample {

    public static void main(String[] args) {

        // Creating an empty TreeSet
        TreeSet<String> s = new TreeSet<String>();

        // Elements are added using add() method
        s.add("gfg");
        s.add("courses");
        s.add("ide");

        // Displaying the TreeSet
        // in sorted order
        System.out.println(s);

        // Checking whether "ide" is present
        // or not
        System.out.println(s.contains("ide"));

        // Iterator to traverse the TreeSet
        Iterator<String> i = s.iterator();
        while (i.hasNext())
            System.out.println(i.next());
    }
}
```

### Add+Remove

```java
import java.util.*;

class TreeSetExample {

    public static void main(String[] args) {

        // Creating an empty TreeSet
        TreeSet<Integer> s = new TreeSet<Integer>();

        // Elements are added using add() method
        s.add(10);
        s.add(5);
        s.add(2);
        s.add(15);

        // Removing 5 from TreeSet
        s.remove(5);

        // foreach way of traversal
        for (Integer x : s)
            System.out.print(x + " ");
    }
}
```

### Lower | Higher | Floor | Ceiling

```java
import java.util.*;

class TreeSetExample {

    public static void main(String[] args) {

        // Creating an empty TreeSet
        TreeSet<Integer> s = new TreeSet<Integer>();

        // Elements are added using add() method
        s.add(10);
        s.add(5);
        s.add(2);
        s.add(15);

        // Prints the largest value lower than 5
        // Here it is 2
        System.out.println(s.lower(5));

        // Prints the smallest higher value than 5
        // Between 10 and 15 smallest is 10
        System.out.println(s.higher(5));

        // Value <= 5
        System.out.println(s.floor(5));

        // Value >= 5
        System.out.println(s.ceiling(5));
    }
}
```

## TreeMap in Java

### Example

```java
import java.util.*;

class GFG {
    public static void main(String args[]) {
        // Initialization of a TreeMap 
        // using Generics 
        TreeMap<Integer, String> t
                = new TreeMap<Integer, String>();

        // Inserting the Elements 
        t.put(10, "geeks");
        t.put(15, "ide");
        t.put(5, "courses");

        // Prints the TreeMap
        System.out.println(t);

        // Check for the key in the map
        System.out.println(t.containsKey(10));

        // Iterating over TreeMap
        for (Map.Entry<Integer, String> e : t.entrySet())
            System.out.println(e.getKey() + " " + e.getValue());
    }
}
```

### HigherKey | LowerKey | FloorKey | CeilingKey

```java
import java.util.*;

class GFG {
    public static void main(String args[]) {
        // Initialization of a TreeMap 
        // using Generics 
        TreeMap<Integer, String> t
                = new TreeMap<Integer, String>();

        // Inserting the Elements 
        t.put(10, "geeks");
        t.put(15, "ide");
        t.put(5, "courses");

        // returns the smallest key greater 
        // than the passed key i.e., 15
        System.out.println(t.higherKey(10));

        // returns the greatest smaller key 
        // than the passed key i.e., 5
        System.out.println(t.lowerKey(10));

        // greatest key <= passed key i.e., 10
        System.out.println(t.floorKey(10));

        // greatest key >= passed key i.e., 10
        System.out.println(t.ceilingKey(10));
    }
}
```

### GetValue

```java
import java.util.*;

class GFG {
    public static void main(String args[]) {
        // Initialization of a TreeMap 
        // using Generics 
        TreeMap<Integer, String> t
                = new TreeMap<Integer, String>();

        // Inserting the Elements 
        t.put(10, "geeks");
        t.put(15, "ide");
        t.put(5, "courses");

        // returns the key-value pair corresponding
        // to higher key and prints the associated value
        System.out.println(t.higherEntry(10).getValue());

        // returns the key-value pair corresponding
        // to lower key prints the associated value
        System.out.println(t.lowerEntry(10).getValue());

        // returns a key-value mapping associated 
        // with the greatest key <= to the given key
        System.out.println(t.floorEntry(10).getValue());

        // returns a key-value mapping associated 
        // with the least key >= to the given key
        System.out.println(t.ceilingEntry(10).getValue());
    }
}
```

## Ceiling on left side in an array

```java
import java.util.*;
import java.io.*;
import java.lang.*;

class GFG {

    public static void main(String args[]) {
        int arr[] = {2, 8, 30, 15, 25, 12};
        int n = arr.length;

        printCeiling(arr, n);
    }

    public static void printCeiling(int arr[], int n) {
        System.out.print("-1" + " ");
        TreeSet<Integer> s = new TreeSet<>();
        s.add(arr[0]);
        for (int i = 1; i < n; i++) {
            if (s.ceiling(arr[i]) != null)
                System.out.print(s.ceiling(arr[i]) + " ");
            else
                System.out.print("-1" + " ");
            s.add(arr[i]);
        }
    }
}
```

## Find Kth Smallest in BST

```java
import java.util.*;
import java.io.*;
import java.lang.*;

class Node {
    int data;
    Node left, right;
    int lCount;

    Node(int x) {
        data = x;
        left = right = null;
        lCount = 0;
    }
}

class Gfg {
    public static Node insert(Node root, int x) {
        if (root == null)
            return new Node(x);

        if (x < root.data) {
            root.left = insert(root.left, x);
            root.lCount++;
        } else if (x > root.data)
            root.right = insert(root.right, x);
        return root;
    }

    public static Node kthSmallest(Node root, int k) {
        if (root == null)
            return null;

        int count = root.lCount + 1;
        if (count == k)
            return root;

        if (count > k)
            return kthSmallest(root.left, k);

        return kthSmallest(root.right, k - count);
    }

    public static void main(String args[]) {
        Node root = null;
        int keys[] = {20, 8, 22, 4, 12, 10, 14};

        for (int x : keys)
            root = insert(root, x);

        int k = 4;
        Node res = kthSmallest(root, k);
        if (res == null)
            System.out.println("There are less "
                    + "than k nodes in the BST");
        else
            System.out.println("K-th Smallest"
                    + " Element is " + res.data);
    }
}
```

## Check for BST

```java
import java.util.*;
import java.io.*;
import java.lang.*;

class Node {
    int key;
    Node left, right;

    Node(int x) {
        key = x;
        left = right = null;
    }
}

class Gfg {
    static int prev = Integer.MIN_VALUE;

    public static boolean isBST(Node root) {
        if (root == null)
            return true;

        if (isBST(root.left) == false) return false;

        if (root.key <= prev) return false;
        prev = root.key;

        return isBST(root.right);
    }

    public static void main(String args[]) {
        Node root = new Node(4);
        root.left = new Node(2);
        root.right = new Node(5);
        root.left.left = new Node(1);
        root.left.right = new Node(3);

        if (isBST(root))
            System.out.println("IS BST");
        else
            System.out.println("Not a BST");
    }
}
```

## Fix BST with Two Nodes Swapped

```java
import java.util.*;
import java.io.*;
import java.lang.*;

class Node {
    int key;
    Node left, right;

    Node(int x) {
        key = x;
        left = right = null;
    }
}

class Gfg {
    public static void inorder(Node root) {
        if (root != null) {
            inorder(root.left);
            System.out.print(root.key + " ");
            inorder(root.right);
        }
    }

    static Node prev = null, first = null, second = null;

    public static void fixBST(Node root) {
        if (root == null)
            return;
        fixBST(root.left);
        if (prev != null && root.key < prev.key) {
            if (first == null)
                first = prev;
            second = root;
        }
        prev = root;

        fixBST(root.right);
    }

    public static void main(String args[]) {
        Node root = new Node(18);
        root.left = new Node(60);
        root.right = new Node(70);
        root.left.left = new Node(4);
        root.right.left = new Node(8);
        root.right.right = new Node(80);

        inorder(root);
        System.out.println();
        ;
        fixBST(root);
        int temp = first.key;
        first.key = second.key;
        second.key = temp;
        inorder(root);
    }
}
```

## Pair Sum with given BST

```java
import java.util.*;
import java.io.*;
import java.lang.*;

class Node {
    int key;
    Node left, right;

    Node(int x) {
        key = x;
        left = right = null;
    }
}

class Gfg {

    public static boolean isPairSum(Node root, int sum, HashSet<Integer> s) {
        if (root == null) return false;

        if (isPairSum(root.left, sum, s) == true)
            return true;

        if (s.contains(sum - root.key))
            return true;
        else
            s.add(root.key);
        return isPairSum(root.right, sum, s);
    }

    public static void main(String args[]) {
        Node root = new Node(10);
        root.left = new Node(8);
        root.right = new Node(20);
        root.left.left = new Node(4);
        root.left.right = new Node(9);
        root.right.left = new Node(11);
        root.right.right = new Node(30);
        root.right.right.left = new Node(25);

        int sum = 33;

        HashSet<Integer> s = new HashSet<>();
        System.out.print(isPairSum(root, sum, s));
    }
}
```

## Vertical Sum in a Binary Tree

```java
import java.util.*;
import java.io.*;
import java.lang.*;

class Node {
    int key;
    Node left, right;

    Node(int x) {
        key = x;
        left = right = null;
    }
}

class Gfg {

    public static void vSumR(Node root, int hd, TreeMap<Integer, Integer> mp) {
        if (root == null) return;
        vSumR(root.left, hd - 1, mp);
        int pSum = (mp.get(hd) == null) ? 0 : mp.get(hd);
        mp.put(hd, pSum + root.key);
        vSumR(root.right, hd + 1, mp);
    }

    public static void vSum(Node root) {
        TreeMap<Integer, Integer> mp = new TreeMap<Integer, Integer>();
        vSumR(root, 0, mp);
        for (Map.Entry sum : mp.entrySet())
            System.out.print(sum.getValue() + " ");
    }

    public static void main(String args[]) {
        Node root = new Node(10);
        root.left = new Node(20);
        root.right = new Node(50);
        root.left.left = new Node(30);
        root.left.right = new Node(40);

        vSum(root);
    }
}
```

## Vertical Traversal of Binary Tree

```java
import java.util.*;
import java.io.*;
import java.lang.*;

class Node {
    int key;
    Node left, right;

    Node(int x) {
        key = x;
        left = right = null;
    }
}

class Pair {
    Node node;
    int hd;

    Pair(Node n, int h) {
        node = n;
        hd = h;
    }
}

class Gfg {

    public static void vTraversal(Node root) {
        Queue<Pair> q = new LinkedList<>();
        Map<Integer, ArrayList<Integer>> mp = new TreeMap<>();
        q.add(new Pair(root, 0));
        while (q.isEmpty() == false) {
            Pair p = q.poll();
            Node curr = p.node;
            int hd = p.hd;
            if (mp.containsKey(hd))
                mp.get(hd).add(curr.key);
            else {
                ArrayList<Integer> al = new ArrayList<>();
                al.add(curr.key);
                mp.put(hd, al);
            }
            if (curr.left != null)
                q.add(new Pair(curr.left, hd - 1));
            if (curr.right != null)
                q.add(new Pair(curr.right, hd + 1));
        }
        for (Map.Entry<Integer, ArrayList<Integer>> p : mp.entrySet()) {
            ArrayList<Integer> al = p.getValue();
            for (int x : al)
                System.out.print(x + " ");
            System.out.println();
        }
    }

    public static void main(String args[]) {
        Node root = new Node(10);
        root.left = new Node(20);
        root.right = new Node(30);
        root.left.left = new Node(40);
        root.left.right = new Node(50);

        vTraversal(root);
    }
}
```

## Top View of Binary Tree

```java
import java.util.*;
import java.io.*;
import java.lang.*;

class Node {
    int key;
    Node left, right;

    Node(int x) {
        key = x;
        left = right = null;
    }
}

class Pair {
    Node node;
    int hd;

    Pair(Node n, int h) {
        node = n;
        hd = h;
    }
}

class Gfg {

    public static void topView(Node root) {
        Queue<Pair> q = new LinkedList<>();
        Map<Integer, Integer> mp = new TreeMap<>();
        q.add(new Pair(root, 0));
        while (q.isEmpty() == false) {
            Pair p = q.poll();
            Node curr = p.node;
            int hd = p.hd;
            if (mp.containsKey(hd) == false)
                mp.put(hd, curr.key);
            if (curr.left != null)
                q.add(new Pair(curr.left, hd - 1));
            if (curr.right != null)
                q.add(new Pair(curr.right, hd + 1));
        }
        for (Map.Entry<Integer, Integer> x : mp.entrySet()) {
            System.out.print(x.getValue() + " ");
        }
    }

    public static void main(String args[]) {
        Node root = new Node(10);
        root.left = new Node(20);
        root.right = new Node(30);
        root.left.left = new Node(40);
        root.left.right = new Node(50);

        topView(root);
    }
}
```

## Bottom View of Binary Tree

```java
import java.util.*;
import java.io.*;
import java.lang.*;

class Node {
    int key;
    Node left, right;

    Node(int x) {
        key = x;
        left = right = null;
    }
}

class Pair {
    Node node;
    int hd;

    Pair(Node n, int h) {
        node = n;
        hd = h;
    }
}

class Gfg {

    public static void topView(Node root) {
        Queue<Pair> q = new LinkedList<>();
        Map<Integer, Integer> mp = new TreeMap<>();
        q.add(new Pair(root, 0));
        while (q.isEmpty() == false) {
            Pair p = q.poll();
            Node curr = p.node;
            int hd = p.hd;
            mp.put(hd, curr.key);
            if (curr.left != null)
                q.add(new Pair(curr.left, hd - 1));
            if (curr.right != null)
                q.add(new Pair(curr.right, hd + 1));
        }
        for (Map.Entry<Integer, Integer> x : mp.entrySet()) {
            System.out.print(x.getValue() + " ");
        }
    }

    public static void main(String args[]) {
        Node root = new Node(10);
        root.left = new Node(20);
        root.right = new Node(30);
        root.left.left = new Node(40);
        root.left.right = new Node(50);

        topView(root);
    }
}
```
