# LinkedList

### Remove Nth Node From End of List

Given the `head` of a linked list, remove the `nth` node from the end of the list and return its head.

```
Input: head = [1,2,3,4,5], n = 2
Output: [1,2,3,5]
Example 2:

Input: head = [1], n = 1
Output: []
Example 3:

Input: head = [1,2], n = 1
Output: [1]
```

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution 
{
    public ListNode removeNthFromEnd(ListNode head, int n) 
    {
        if(head.next==null)
            return null;
        
        ListNode slow=head;
        ListNode fast=head;
        
        for(int i=1;i<=n;i++)
            fast=fast.next;
        
        // edge case handeled when we have to delete the 1st node 
        // i.e n=size of linked list
        
        if(fast==null)
            return head.next;
        
        while(fast!=null && fast.next!=null)
        {
            fast=fast.next;
            slow=slow.next;
        }
        
        slow.next=slow.next.next;
        return head;
    }
}
```

### LinkedList Cycle

```java
/**
 * Definition for singly-linked list.
 * class ListNode {
 * int val;
 * ListNode next;
 * ListNode(int x) {
 * val = x;
 * next = null;
 * }
 * }
 */
public class Solution {
	public boolean hasCycle(ListNode head) {
		if (head == null || head.next == null || head.next.next == null) {
			return false;
		}

		ListNode slow = head;
		ListNode fast = head.next;

		while (fast != null && fast.next != null) {
			fast = fast.next.next;
			slow = slow.next;
			if (slow == fast) {
				return true;
			}
		}
		return false;
	}
}
```

### Delete the Middle Node of a Linked List

```
You are given the head of a linked list. Delete the middle node, 
and return the head of the modified linked list.

Input: head = [1,3,4,7,1,2,6]
Output: [1,3,4,1,2,6]
Explanation: 7 is the middle element


class Solution {
	public ListNode deleteMiddle(ListNode head) {
		if (head == null || head.next == null) {
			return null;
		}
		if (head.next.next == null) {
			head.next = null;
			return head;
		}
		ListNode fast = head;
		ListNode slow = head;
		while (fast != null && fast.next != null) {
			fast = fast.next.next;
			slow = slow.next;
		}
		slow.val = slow.next.val;
		slow.next = slow.next.next;
		return head;
	}
}Delete the Middle Node of a Linked List
```

```java
You are given the head of a linked list. Delete the middle node, 
and return the head of the modified linked list.

Input: head = [1,3,4,7,1,2,6]
Output: [1,3,4,1,2,6]
Explanation: 7 is the middle element
```

```java

class Solution {
	public ListNode deleteMiddle(ListNode head) {
		if (head == null || head.next == null) {
			return null;
		}
		if (head.next.next == null) {
			head.next = null;
			return head;
		}
		ListNode fast = head;
		ListNode slow = head;
		while (fast != null && fast.next != null) {
			fast = fast.next.next;
			slow = slow.next;
		}
		slow.val = slow.next.val;
		slow.next = slow.next.next;
		return head;
	}
}
```

### Merge two sorted List

```java
class Solution {
	public ListNode mergeTwoLists(ListNode list1, ListNode list2) {

		ListNode temp = new ListNode();
		ListNode ans = temp;

		while (list1 != null && list2 != null) {
			if (list1.val < list2.val) {
				temp.next = list1;
				temp = temp.next;
				list1 = list1.next;
			} else {
				temp.next = list2;
				temp = temp.next;
				list2 = list2.next;
			}
		}

		if (list1 != null) {
			temp.next = list1;
		}
		if (list2 != null) {
			temp.next = list2;
		}

		return ans.next;
	}
}
```

### Remove Linked List Elements

Given the `head` of a linked list and an integer `val`, remove all the nodes of the linked list that has `Node.val == val`, and return _the new head_.

```
Input: head = [1,2,6,3,4,5,6], val = 6
Output: [1,2,3,4,5]
Example 2:

Input: head = [], val = 1
Output: []
Example 3:

Input: head = [7,7,7,7], val = 7
Output: []
```

### Middle of the Linked List

Given the `head` of a singly linked list, return _the middle node of the linked list_.

If there are two middle nodes, return **the second middle** node.

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 * int val;
 * ListNode next;
 * ListNode() {}
 * ListNode(int val) { this.val = val; }
 * ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
	public ListNode middleNode(ListNode head) {
		ListNode slow = head, fast = head;
		while (fast != null && fast.next != null) {
			slow = slow.next;
			fast = fast.next.next;
		}
		return slow;
	}
}
```

### Remove Nth Node From End of List

Given the `head` of a linked list, remove the `nth` node from the end of the list and return its head.

```
Input: head = [1,2,3,4,5], n = 2
Output: [1,2,3,5]
Example 2:

Input: head = [1], n = 1
Output: []
Example 3:

Input: head = [1,2], n = 1
Output: [1]
```

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution 
{
    public ListNode removeNthFromEnd(ListNode head, int n) 
    {
        if(head.next==null)
            return null;
        
        ListNode slow=head;
        ListNode fast=head;
        
        for(int i=1;i<=n;i++)
            fast=fast.next;
        
        // edge case handeled when we have to delete the 1st node 
        // i.e n=size of linked list
        
        if(fast==null)
            return head.next;
        
        while(fast!=null && fast.next!=null)
        {
            fast=fast.next;
            slow=slow.next;
        }
        
        slow.next=slow.next.next;
        return head;
    }
}
```



### Singly LinkedList Implementation

```java
public class Program {
    static class Node {
        int number;
        Node next;

        public Node(int number) {
            this.number = number;
            next = null;
        }
    }

    public static void main(  ) {

        Node head;
        Node first = new Node(10);
        Node second = new Node(20);
        Node third = new Node(30);
        Node fourth = new Node(40);

        first.next = second;
        second.next = third;
        third.next = fourth;

        System.out.println("Iterative Printing");
        printLinkedList(first);

        System.out.println("Recursive Printing");
        printLinkedLRecursive(first);

        System.out.println("Inserting head");
        head = insertHeadLL(0, first);
        printLinkedLRecursive(head);

        System.out.println("Inserting at end");
        head = insertNodeEndLL(50, head);
        printLinkedLRecursive(head);

        System.out.println("Deleting Head node");
        head = deleteHeadNodeLL(head);
        printLinkedList(head);

        System.out.println("Delete Last node");
        head = deleteLastNodeLL(head);
        printLinkedLRecursive(head);

        System.out.println("Insert data at postion");
        head = insertDataAtPos(4, 25, head);
        printLinkedLRecursive(head);

        System.out.println("Find Data iter  : " + searchInLLIter(30, head));
        System.out.println("Find Data recur : " + searchInLLRec(60, 1, head));

    }

    public static void printLinkedList(Node curr) {
        while (curr != null) {
            System.out.print(curr.number + " ");
            curr = curr.next;
        }
        System.out.println();
    }

    public static void printLinkedLRecursive(Node curr) {
        if (curr == null) {
            System.out.println();
            return;
        }
        System.out.print(curr.number + " ");
        printLinkedLRecursive(curr.next);
    }

    public static Node insertHeadLL(int number, Node currHead) {
        Node newNode = new Node(number);
        newNode.next = currHead;
        return newNode;
    }

    public static Node insertNodeEndLL(int number, Node head) {
        Node ptr = head;
        if (head == null) {
            return insertHeadLL(number, null);
        }

        // DESIGN
        while (ptr.next != null)
            ptr = ptr.next;

        ptr.next = new Node(number);
        return head;

    }

    public static Node deleteHeadNodeLL(Node head) {
        if (head == null) {
            return null;
        }
        return head.next;
    }

    public static Node deleteLastNodeLL(Node head) {
        if (head == null) {
            return null;
        }

        if (head.next == null) {
            return null;
        }

        Node ptr = head;

        // DESIGN
        while (ptr.next.next != null)
            ptr = ptr.next;

        ptr.next = null;
        return head;
    }

    public static Node insertDataAtPos(int position, int number, Node head) {
        if (position == 1) {
            return insertHeadLL(number, head);
        }

        // *** DESIGN ***
        Node ptr = head;
        for (int i = 1; i < position - 1 && ptr != null; i++) {
            ptr = ptr.next;
        }

        if (ptr == null) {
            return head;
        }

        Node temp = new Node(number);
        temp.next = ptr.next;
        ptr.next = temp;
        return head;

    }

    public static int searchInLLIter(int number, Node head) {
        Node ptr = head;
        int count = 1;
        while (ptr != null) {
            if (ptr.number == number) {
                return count;
            }
            ptr = ptr.next;
            count++;
        }
        return -1;
    }

    public static int searchInLLRec(int number, int index, Node head) {
        if (head == null) {
            return -1;
        }
        if (head.number == number) {
            return index;
        }
        return searchInLLRec(number, index + 1, head.next);
    }
}
```

### Circular LinkedList Implementation

```java
public class Program {
    static class Node {
        int number;
        Node next;

        public Node(int number) {
            this.number = number;
            next = null;
        }
    }

    public static void main(  ) {
        Node head = new Node(10);
        head.next = new Node(20);
        head.next.next = new Node(30);
        head.next.next.next = new Node(40);
        head.next.next.next.next = head;

        System.out.println("Printing CLL");
        printCLL(head);

        System.out.println("Insert Head");
        head = insertHead(0, head);
        printCLL(head);

        System.out.println("Insert tail");
        head = insertTail(50, head);
        printCLL(head);

        System.out.println("delete head");
        head = deleteHead(head);
        printCLL(head);

        System.out.println("delete kth node");
        head = deleteKthNode(3, head);
        printCLL(head);

    }

    public static void printCLL(Node head) {
        Node ptr = head;

        if (head == null) {
            return;
        }

        // DESIGN
        do {
            System.out.print(ptr.number + " ");
            ptr = ptr.next;
        } while (ptr != head);
        System.out.println();
    }

    public static Node insertHead(int number, Node head) {
        Node temp = new Node(number);

        if (head == null) {
            temp.next = temp;
            return temp;
        }

        temp.next = head.next;
        head.next = temp;

        int t = head.number;
        head.number = temp.number;
        temp.number = t;
        return head;

    }

    public static Node insertTail(int number, Node head) {

        Node temp = new Node(number);

        if (head == null) {
            temp.next = temp;
            return temp;
        }

        temp.next = head.next;
        head.next = temp;

        int t = temp.number;
        temp.number = head.number;
        head.number = t;
        return temp;

    }

    public static Node deleteHead(Node head) {
        if (head == null || head.next == head) {
            return null;
        }

        int t = head.next.number;
        head.next = head.next.next;
        head.number = t;

        return head;

    }

    public static Node deleteKthNode(int pos, Node head) {
        if (pos == 1) {
            return deleteHead(head);
        }

        Node ptr = head;

        for (int i = 0; i < pos - 2; i++) {
            ptr = ptr.next;
        }

        ptr.next = ptr.next.next;
        return head;

    }
}
```

### Doubly LinkedList Implementation

```java
public class Program {

    static class Node {
        int number;
        Node next;
        Node prev;

        public Node(int number) {
            this.number = number;
            this.next = null;
            this.prev = null;
        }
    }

    public static void main(  ) {

        Node head;
        Node first = new Node(10);
        Node second = new Node(20);
        Node third = new Node(30);
        Node fourth = new Node(40);

        first.next = second;
        first.prev = null;
        second.next = third;
        second.prev = first;
        third.prev = second;
        third.next = fourth;
        fourth.prev = third;
        fourth.next = null;

        System.out.println("Inserting at the beginning");
        head = insertAtTheBegin(0, first);
        printLL(head);

        System.out.println("Inserting at the End");
        head = insertAtTheEnd(50, head);
        printLL(head);

        System.out.println("Delete Head");
        head = deleteHeadDLL(head);
        printLL(head);

        System.out.println("Delete Last Node ");
        head = deleteLastHead(head);
        printLL(head);

        System.out.println("reversing a DLL");
        Node newHead = reverseDLL(head);
        printLL(newHead);
    }

    public static void printLL(Node node) {

        if (node == null) {
            System.out.println();
            return;
        }

        System.out.print(node.number + " ");
        printLL(node.next);

    }

    public static Node insertAtTheBegin(int number, Node head) {

        if (head == null) {
            return new Node(number);
        }

        Node temp = new Node(number);
        head.prev = temp;
        temp.next = head;
        return temp;
    }

    public static Node insertAtTheEnd(int number, Node head) {
        if (head == null) {
            return new Node(number);
        }

        Node ptr = head;

        // DESIGN
        while (ptr.next != null)
            ptr = ptr.next;

        Node temp = new Node(number);
        ptr.next = temp;
        temp.prev = ptr;
        return head;
    }

    public static Node reverseDLL(Node head) {
        if (head == null || head.next == null) {
            return head;
        }

        Node prev = null;
        Node curr = head;

        while (curr != null) {
            prev = curr.prev;
            curr.prev = curr.next;
            curr.next = prev;
            curr = curr.prev;
        }
        return prev.prev;

    }

    public static Node deleteHeadDLL(Node head) {
        if (head == null) {
            return head;
        }

        if (head.next == null) {
            return null;
        }

        head = head.next;
        head.prev = null;
        return head;

    }

    public static Node deleteLastHead(Node head) {
        if (head == null) {
            return head;
        }
        if (head.next == null) {
            return null;
        }

        Node ptr = head;
        while (ptr.next.next != null)
            ptr = ptr.next;

        ptr.next = null;
        return head;
    }

}
```

### Insert into sorted Linkedlist

```java
public class Program {

    static class Node {
        int number;
        Node next;

        public Node(int number) {
            this.number = number;
            this.next = null;
        }
    }

    public static void main(String[] args) {
        Node first = new Node(10);
        first.next = new Node(20);
        first.next.next = new Node(30);
        first.next.next.next = new Node(40);

        Node head = first;

        System.out.println("sorted insert");
        head = sortedInsert(13, head);
        printLL(head);

    }

    public static void printLL(Node head) {
        Node ptr = head;

        do {
            System.out.print(ptr.number + " ");
            ptr = ptr.next;
        } while (ptr != null);

        System.out.println();
    }

    public static Node sortedInsert(int number, Node head) {

        Node temp = new Node(number);

        if (head == null) {
            return temp;
        }

        if (number < head.number) {
            temp.next = head;
            return temp;
        }

        Node curr = head;
        while (curr.next != null && curr.next.number < number) {
            curr = curr.next;
        }

        temp.next = curr.next;
        curr.next = temp;
        return head;

    }
}
```

### Middle of Linked List

```java
class Program {

    static class Node {
        int data;
        Node next;

        Node(int x) {
            data = x;
            next = null;
        }
    }

    public static void main ( String[] args ) {
        Node head = new Node(10);
        head.next = new Node(20);
        head.next.next = new Node(30);
        head.next.next.next = new Node(40);
        head.next.next.next.next = new Node(50);
        printlist(head);
        System.out.print("Position of element in Linked List: ");
        printMiddle(head);

    }

    static void printMiddle(Node head) {
        if (head == null) return;
        Node slow = head, fast = head;
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }
        System.out.print(slow.data);
    }

    public static void printlist(Node head) {
        Node curr = head;
        while (curr != null) {
            System.out.print(curr.data + " ");
            curr = curr.next;
        }
        System.out.println();
    }
}
```

### Reverse a Linked-list Iteratively

```java
public class Program {

    static class Node {
        int data;
        Node next;

        Node(int x) {
            data = x;
            next = null;
        }
    }

    public static void main(String[] args ) {
        Node head = new Node(10);
        head.next = new Node(20);
        head.next.next = new Node(30);
        head.next.next.next = new Node(40);
        head.next.next.next.next = new Node(50);

        System.out.print("Position of element in Linked List: ");
        head = reverseLL(head);
        printlist(head);

    }

    static Node reverseLL(Node head) {
        if(head == null || head.next == null) {
            return head;
        }

        Node prev = null;
        Node curr = head;

        while(curr != null) {
            Node next = curr.next;
            curr.next = prev;
            prev = curr;
            curr = next;
        }
        return prev;
    }

    public static void printlist(Node head) {
        Node curr = head;
        while (curr != null) {
            System.out.print(curr.data + " ");
            curr = curr.next;
        }
        System.out.println();
    }
}
```

### Reverse a linked-list recursively

```java
public class Main {
    static class Node {
        int number;
        Node next;

        public Node(int number) {
            this.number = number;
            this.next = null;
        }
    }

    public static void main(String[] args) {
        Node head = new Node(0);
        head.next = new Node(10);
        head.next.next = new Node(20);
        head.next.next.next = new Node(30);

        head = reverseLL(head, null);
        printLL(head);
    }

    public static Node reverseLL(Node curr, Node prev) {
        if (curr == null) {
            return prev;
        }

        Node next = curr.next;
        curr.next = prev;

        return reverseLL(next, curr);
    }

    public static void printLL(Node head) {
        Node ptr = head;
        while (ptr != null) {
            System.out.print(ptr.number + " ");
            ptr = ptr.next;
        }
    }

}
```

### Delete duplicate Item

```java
public class Main {
    static class Node 
    {
        int number;
        Node next;

        public Node(int number)
        {
            this.number = number;
            this.next = null;
        }
    }

    public static void main(String[] args)
    {

        Node head = new Node(0);
        head.next = new Node(10);
        head.next.next = new Node(10);
        head.next.next.next = new Node(30);
        head.next.next.next.next = new Node(30);

        System.out.println("Printing : ");
        printLL(head);

        System.out.println("Deleting : ");
        deleteDLL(head);
        printLL(head);

    }

    static void printLL(Node head) {
        Node ptr = head;
        while(ptr != null) {
            System.out.print(ptr.number+" ");
            ptr = ptr.next;
        }
        System.out.println();
    }

    static void deleteDLL(Node head) {
        Node ptr = head;
        while(ptr != null && ptr.next != null) {
            if (ptr.number == ptr.next.number) {
                ptr.next = ptr.next.next;
            } else {
                ptr = ptr.next;
            }            
        }
    }

}
```

### Floyd Detection Algorithm

```java
public class Main {
    static class Node {
        int data;
        Node next;

        Node(int x) {
            data = x;
            next = null;
        }
    }

    public static void main(String args[]) {
        Node head = new Node(15);
        head.next = new Node(10);
        head.next.next = new Node(12);
        head.next.next.next = new Node(20);
        head.next.next.next.next = head.next;
        if (isLoop(head))
            System.out.print("Loop found");
        else
            System.out.print("No Loop");
    }

    static boolean isLoop(Node head) {
        Node slow_p = head, fast_p = head;

        while (fast_p != null && fast_p.next != null) {
            slow_p = slow_p.next;
            fast_p = fast_p.next.next;
            if (slow_p == fast_p) {
                return true;
            }
        }
        return false;
    }

    public static void printlist(Node head) {
        Node curr = head;
        while (curr != null) {
            System.out.print(curr.data + " ");
            curr = curr.next;
        }
        System.out.println();
    }
}
```

### Detect and remove the loop in Linked List

```java
public class Main {
    static class Node {
        int data;
        Node next;

        Node(int x) {
            data = x;
            next = null;
        }
    }

    public static void main(String args[]) {
        Node head = new Node(15);
        head.next = new Node(10);
        head.next.next = new Node(12);
        head.next.next.next = new Node(20);
        head.next.next.next.next = head.next;
        if (isLoop(head))
            System.out.print("Loop found");
        else
            System.out.print("No Loop");
    }

    static boolean isLoop(Node head) {
        Node slow_p = head, fast_p = head;

        while (fast_p != null && fast_p.next != null) {
            slow_p = slow_p.next;
            fast_p = fast_p.next.next;
            if (slow_p == fast_p) {
                return true;
            }
        }
        return false;
    }

    public static void printlist(Node head) {
        Node curr = head;
        while (curr != null) {
            System.out.print(curr.data + " ");
            curr = curr.next;
        }
        System.out.println();
    }
}
```

### Delete node with only pointer given to it

```java
class Main {

    static class Node {
        int data;
        Node next;

        Node(int x) {
            data = x;
            next = null;
        }
    }

    public static void main(String args[]) {
        Node head = new Node(10);
        head.next = new Node(20);
        Node ptr = new Node(30);
        head.next.next = ptr;
        head.next.next.next = new Node(40);
        head.next.next.next.next = new Node(25);
        printlist(head);
        deleteNode(ptr);
        printlist(head);
    }

    static void deleteNode(Node ptr) {
        Node temp = ptr.next;
        ptr.data = temp.data;
        ptr.next = temp.next;
    }

    public static void printlist(Node head) {
        Node curr = head;
        while (curr != null) {
            System.out.print(curr.data + " ");
            curr = curr.next;
        }
        System.out.println();
    }
}
```

### Segregate even & odd nodes in Linked List

```java
public class Main {

    static class Node {
        int data;
        Node next;

        Node(int x) {
            data = x;
            next = null;
        }
    }

    public static void main(String args[]) {
        Node head = new Node(17);
        head.next = new Node(15);
        head.next.next = new Node(8);
        head.next.next.next = new Node(12);
        head.next.next.next.next = new Node(10);
        head.next.next.next.next.next = new Node(5);
        head.next.next.next.next.next.next = new Node(4);
        printlist(head);
        head = segregate(head);
        printlist(head);

    }

    static Node segregate(Node head) {
        Node eS = null, eE = null, oS = null, oE = null;
        for (Node curr = head; curr != null; curr = curr.next) {
            int x = curr.data;
            if (x % 2 == 0) {
                if (eS == null) {
                    eS = curr;
                    eE = eS;
                } else {
                    eE.next = curr;
                    eE = eE.next;
                }
            } else {
                if (oS == null) {
                    oS = curr;
                    oE = oS;
                } else {
                    oE.next = curr;
                    oE = oE.next;
                }
            }
        }
        if (oS == null || eS == null)
            return head;
        eE.next = oS;
        oE.next = null;
        return eS;
    }

    public static void printlist(Node head) {
        Node curr = head;
        while (curr != null) {
            System.out.print(curr.data + " ");
            curr = curr.next;
        }
        System.out.println();
    }
}
```

### Intersection of two linked-list

```java
class Main {

    static Node headA, headB;

    static class Node {

        int data;
        Node next;

        Node(int d) {
            data = d;
            next = null;
        }
    }

    int getNode() {
        int c1 = getCount(headA);
        int c2 = getCount(headB);
        int d;

        if (c1 > c2) {
            d = c1 - c2;
            return _getIntesectionNode(d, headA, headB);
        } else {
            d = c2 - c1;
            return _getIntesectionNode(d, headB, headA);
        }
    }

    int _getIntesectionNode(int d, Node node1, Node node2) {
        int i;
        Node current1 = node1;
        Node current2 = node2;
        for (i = 0; i < d; i++) {
            if (current1 == null) {
                return -1;
            }
            current1 = current1.next;
        }
        while (current1 != null && current2 != null) {
            if (current1.data == current2.data) {
                return current1.data;
            }
            current1 = current1.next;
            current2 = current2.next;
        }

        return -1;
    }

    int getCount(Node node) {
        Node current = node;
        int count = 0;

        while (current != null) {
            count++;
            current = current.next;
        }

        return count;
    }

    public static void main(String[] args) {
        Main list = new Main();

        list.headA = new Node(3);
        list.headA.next = new Node(6);
        list.headA.next.next = new Node(9);
        list.headA.next.next.next = new Node(15);
        list.headA.next.next.next.next = new Node(30);

        list.headB = new Node(10);
        list.headB.next = new Node(15);
        list.headB.next.next = new Node(30);

        System.out.println(list.getNode());
    }
}
```

### Pairwise swap in linked-list

```java
class Main {
    static class Node {
        int data;
        Node next;

        Node(int x) {
            data = x;
            next = null;
        }
    }

    public static void main(String args[]) {
        Node head = new Node(1);
        head.next = new Node(2);
        head.next.next = new Node(3);
        head.next.next.next = new Node(4);
        head.next.next.next.next = new Node(5);
        printlist(head);
        head = pairwiseSwap(head);
        printlist(head);

    }

    static Node pairwiseSwap(Node head) {
        if (head == null || head.next == null)
            return head;
        Node curr = head.next.next;
        Node prev = head;
        head = head.next;
        head.next = prev;
        while (curr != null && curr.next != null) {
            prev.next = curr.next;
            prev = curr;
            Node next = curr.next.next;
            curr.next.next = curr;
            curr = next;
        }
        prev.next = curr;
        return head;
    }

    public static void printlist(Node head) {
        Node curr = head;
        while (curr != null) {
            System.out.print(curr.data + " ");
            curr = curr.next;
        }
        System.out.println();
    }
}
```

### Clone a linked list using a random pointer

```java
import java.util.HashMap;

class Main {

    static class Node {
        int data;
        Node next, random;

        Node(int x) {
            data = x;
            next = random = null;
        }
    }

    public static void print(Node start) {
        Node ptr = start;
        while (ptr != null) {
            System.out.println("Data = " + ptr.data + ", Random  = " + ptr.random.data);
            ptr = ptr.next;
        }
    }

    public static Node clone(Node head) {
        HashMap<Node, Node> hm = new HashMap<Node, Node>();
        for (Node curr = head; curr != null; curr = curr.next)
            hm.put(curr, new Node(curr.data));

        for (Node curr = head; curr != null; curr = curr.next) {
            Node cloneCurr = hm.get(curr);
            cloneCurr.next = hm.get(curr.next);
            cloneCurr.random = hm.get(curr.random);
        }
        Node head2 = hm.get(head);

        return head2;
    }

    public static void main(String[] args) {
        Node head = new Node(10);
        head.next = new Node(5);
        head.next.next = new Node(20);
        head.next.next.next = new Node(15);
        head.next.next.next.next = new Node(20);

        head.random = head.next.next;
        head.next.random = head.next.next.next;
        head.next.next.random = head;
        head.next.next.next.random = head.next.next;
        head.next.next.next.next.random = head.next.next.next;

        System.out.print("Original list : \n");
        print(head);

        System.out.print("\nCloned list : \n");
        Node cloned_list = clone(head);
        print(cloned_list);
    }
}
```

### Clone linked-list using random pointer without hashing

```java
public class Main {
    static class Node {
        int data;
        Node next, random;

        Node(int x) {
            data = x;
            next = random = null;
        }
    }

    public static void print(Node start) {
        Node ptr = start;
        while (ptr != null) {
            System.out.println("Data = " + ptr.data + ", Random  = " + ptr.random.data);
            ptr = ptr.next;
        }
    }

    public static Node clone(Node head) {
        Node next, temp;
        for (Node curr = head; curr != null;) {
            next = curr.next;
            curr.next = new Node(curr.data);
            curr.next.next = next;
            curr = next;
        }
        for (Node curr = head; curr != null; curr = curr.next.next) {
            curr.next.random = (curr.random != null) ? (curr.random.next) : null;
        }

        Node original = head, copy = head.next;

        temp = copy;

        while (original != null && copy != null) {
            original.next = original.next != null ? original.next.next : original.next;

            copy.next = copy.next != null ? copy.next.next : copy.next;
            original = original.next;
            copy = copy.next;
        }

        return temp;
    }

    public static void main(String[] args) {
        Node head = new Node(10);
        head.next = new Node(5);
        head.next.next = new Node(20);
        head.next.next.next = new Node(15);
        head.next.next.next.next = new Node(20);

        head.random = head.next.next;
        head.next.random = head.next.next.next;
        head.next.next.random = head;
        head.next.next.next.random = head.next.next;
        head.next.next.next.next.random = head.next.next.next;

        System.out.print("Original list : \n");
        print(head);

        System.out.print("\nCloned list : \n");
        Node cloned_list = clone(head);
        print(cloned_list);
    }
}
```

### LRU ( least recently used ) Cache Design

```java
import java.util.*;
import java.io.*;
import java.lang.*;
import java.util.*; 

class Node { 
    int key; 
    int value; 
    Node pre; 
    Node next; 

    public Node(int key, int value) 
    { 
        this.key = key; 
        this.value = value; 
    } 
} 

class LRUCache { 
    private HashMap<Integer, Node> map; 
    private int capacity, count; 
    private Node head, tail; 

    public LRUCache(int capacity) 
    { 
        this.capacity = capacity; 
        map = new HashMap<>(); 
        head = new Node(0, 0); 
        tail = new Node(0, 0); 
        head.next = tail; 
        tail.pre = head; 
        head.pre = null; 
        tail.next = null; 
        count = 0; 
    } 

    public void deleteNode(Node node) 
    { 
        node.pre.next = node.next; 
        node.next.pre = node.pre; 
    } 

    public void addToHead(Node node) 
    { 
        node.next = head.next; 
        node.next.pre = node; 
        node.pre = head; 
        head.next = node; 
    } 

    public int get(int key) 
    { 
        if (map.get(key) != null) { 
            Node node = map.get(key); 
            int result = node.value; 
            deleteNode(node); 
            addToHead(node); 
            System.out.println("Got the value : " + 
                result + " for the key: " + key); 
            return result; 
        } 
        System.out.println("Did not get any value" + 
                            " for the key: " + key); 
        return -1; 
    } 

    public void set(int key, int value) 
    { 
        System.out.println("Going to set the (key, "+ 
            "value) : (" + key + ", " + value + ")"); 
        if (map.get(key) != null) { 
            Node node = map.get(key); 
            node.value = value; 
            deleteNode(node); 
            addToHead(node); 
        } 
        else { 
            Node node = new Node(key, value); 
            map.put(key, node); 
            if (count < capacity) { 
                count++; 
                addToHead(node); 
            } 
            else { 
                map.remove(tail.pre.key); 
                deleteNode(tail.pre); 
                addToHead(node); 
            } 
        } 
    } 
} 

public class TestLRUCache { 
    public static void main(String[] args) 
    { 

        LRUCache cache = new LRUCache(2); 

        // it will store a key (1) with value 
        // 10 in the cache. 
        cache.set(1, 10); 

        // it will store a key (2) with value 20 in the cache. 
        cache.set(2, 20); 
        System.out.println("Value for the key: 1 is " + cache.get(1)); // returns 10 

        // removing key 2 and store a key (3) with value 30 in the cache. 
        cache.set(3, 30); 

        System.out.println("Value for the key: 2 is " + 
                cache.get(2)); // returns -1 (not found) 

        // removing key 1 and store a key (4) with value 40 in the cache. 
        cache.set(4, 40); 
        System.out.println("Value for the key: 1 is " + 
            cache.get(1)); // returns -1 (not found) 
        System.out.println("Value for the key: 3 is " + 
                        cache.get(3)); // returns 30 
        System.out.println("Value for the key: 4 is " + 
                        cache.get(4)); // return 40 
    } 
}
```

### Merge two sorted linked lists

```java
import java.util.*;
import java.io.*;
import java.lang.*;

class Node {
    int data;
    Node next;

    Node(int x) {
        data = x;
        next = null;
    }
}

class Test {

    public static void main(String args[]) {
        Node a = new Node(10);
        a.next = new Node(20);
        a.next.next = new Node(30);
        Node b = new Node(5);
        b.next = new Node(35);
        printlist(sortedMerge(a, b));

    }

    static Node sortedMerge(Node a, Node b) {
        if (a == null)
            return b;
        if (b == null)
            return a;
        Node head = null, tail = null;
        if (a.data <= b.data) {
            head = tail = a;
            a = a.next;
        } else {
            head = tail = b;
            b = b.next;
        }
        while (a != null && b != null) {
            if (a.data <= b.data) {
                tail.next = a;
                tail = a;
                a = a.next;
            } else {
                tail.next = b;
                tail = b;
                b = b.next;
            }
        }
        if (a == null) {
            tail.next = b;
        } else {
            tail.next = a;
        }
        return head;
    }

    public static void printlist(Node head) {
        Node curr = head;
        while (curr != null) {
            System.out.print(curr.data + " ");
            curr = curr.next;
        }
        System.out.println();
    }
}
```

### Palindrome linked-list

```java
import java.util.*;
import java.io.*;
import java.lang.*;

class Node {
    char data;
    Node next;

    Node(char x) {
        data = x;
        next = null;
    }
}

class Test {

    public static void main(String args[]) {
        Node head = new Node('g');
        head.next = new Node('f');
        head.next.next = new Node('g');
        if (isPalindrome(head))
            System.out.print("Yes");
        else
            System.out.print("No");

    }

    static Node reverseList(Node head) {
        if (head == null || head.next == null)
            return head;
        Node rest_head = reverseList(head.next);
        Node rest_tail = head.next;
        rest_tail.next = head;
        head.next = null;
        return rest_head;
    }

    static boolean isPalindrome(Node head) {
        if (head == null)
            return true;
        Node slow = head, fast = head;
        while (fast.next != null && fast.next.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }
        Node rev = reverseList(slow.next);
        Node curr = head;
        while (rev != null) {
            if (rev.data != curr.data)
                return false;
            rev = rev.next;
            curr = curr.next;
        }
        return true;
    }
}
```
