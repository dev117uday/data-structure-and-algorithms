---
description: you will never find them !!
---

# Searching

### Left most index of an element

**Important** : To find the left most occurrence of element in array

```java
class Solution {
	static int leftIndex(int arr[], int n, int x) {
		int l = 0, h = n - 1;
		int mid = 0;
		while (l <= h) {
			mid = l + (h - l) / 2;
			if (arr[mid] == x && (mid == 0 || arr[mid - 1] != x))
				return mid;
			else if (arr[mid] >= x)
				h = mid - 1;
			else
				l = mid + 1;
		}
		return -1;
	}

	public static void main(String[] args) {
		int arr[] = new int[] { 2, 3, 3, 3, 3, 3 };
		int n = arr.length;
		int ele = 3;
		System.out.println(leftIndex(arr, n, ele));
	}
}
```

### Count of occurrences of x in sorted element

```java
class Solution {
	static int leftIndex(int arr[], int n, int x) {
		int l = 0, h = n - 1;
		int mid = 0;
		while (l <= h) {
			mid = l + (h - l) / 2;
			if (arr[mid] == x && (mid == 0 || arr[mid - 1] != x))
				return mid;
			else if (arr[mid] >= x)
				h = mid - 1;
			else
				l = mid + 1;
		}
		return -1;
	}

	static int rightIndex(int arr[], int n, int x) {
		int l = 0, h = n - 1;
		int mid = 0;
		while (l <= h) {
			mid = l + (h - l) / 2;
			if (arr[mid] == x && (mid == n - 1 || arr[mid + 1] != x))
				return mid;
			else if (arr[mid] > x)
				h = mid - 1;
			else
				l = mid + 1;
		}
		return -1;
	}

	public static void main(String[] args) {
		int arr[] = new int[] { 2, 3, 4, 5, 5, 5, 6, 6 };
		int n = arr.length;
		int ele = 5;
		int leftOccur = leftIndex(arr, n, ele);
		int rightOccur = rightIndex(arr, n, ele);
		System.out.println(rightOccur - leftOccur + 1);
	}
}
```

### Count of 1s in binary sorted array

```java
class Solution {
	static int count1s(int arr[], int n) {
		int l = 0, h = n - 1;
		int mid = 0;
		while (l <= h) {
			mid = l + (h - l) / 2;
			if (arr[mid] == 1 && (mid == 0 || arr[mid - 1] != 1))
				return n - mid;
			else if (arr[mid] == 0)
				l = mid + 1;
			else
				h = mid - 1;
		}
		return 0;
	}

	public static void main(String[] args) {
		int arr[] = { 0, 0, 0, 0, 1, 1, 1, 1, 1 };
		int n = arr.length;
		System.out.println(count1s(arr, n));
	}
}
```

### Peak element

```java
class Solution {
    // A binary search based function that returns index of a peak element
    
    static int findPeakUtil(int arr[], int low, int high, int n) {
        // Find index of middle element
        int mid = low + (high - low) / 2; /* (low + high)/2 */
        
        // Compare middle element with its neighbours (if neighbours exist)
        if ((mid == 0 || arr[mid - 1] <= arr[mid]) && (mid == n - 1 ||
                arr[mid + 1] <= arr[mid]))
            return mid;
        
            // If middle element is not peak and its left neighbor is
        // greater than it,then left half must have a peak element
        else if (mid > 0 && arr[mid - 1] > arr[mid])
            return findPeakUtil(arr, low, (mid - 1), n);
        
        // If middle element is not peak and its right neighbor
        // is greater than it, then right half must have a peak
        // element
        else
            return findPeakUtil(arr, (mid + 1), high, n);
    }

    // A wrapper over recursive function findPeakUtil()
    static int findPeak(int arr[], int n) {
        return findPeakUtil(arr, 0, n - 1, n);
    }

    // Driver method
    public static void main(String[] args) {
        int arr[] = { 1, 3, 20, 4, 1, 0 };
        int n = arr.length;
        System.out.println("Index of a peak point is " +
                findPeak(arr, n));
    }
}
```

### Find an element in infinite sized sorted array

```java
class Solution {
    
    // Simple binary search algorithm
    static int binarySearch(int arr[], int l, int r, int x) {
        if (r >= l) {
            int mid = l + (r - l) / 2;
            if (arr[mid] == x)
                return mid;
            if (arr[mid] > x)
                return binarySearch(arr, l, mid - 1, x);
            return binarySearch(arr, mid + 1, r, x);
        }
        return -1;
    }

    // Method takes an infinite size array and a key to be
    // searched and returns its position if found else -1.
    // We don't know size of arr[] and we can assume size to be
    // infinite in this function.
    // NOTE THAT THIS FUNCTION ASSUMES arr[] TO BE OF INFINITE SIZE
    // THEREFORE, THERE IS NO INDEX OUT OF BOUND CHECKING
    static int findPos(int arr[], int key) {
        int l = 0, h = 1;
        int val = arr[0];
        // Find h to do binary search
        while (val < key) {
            l = h; // store previous high
            // check that 2*h doesn't exceeds array
            // length to prevent ArrayOutOfBoundException
            if (2 * h < arr.length - 1)
                h = 2 * h;
            else
                h = arr.length - 1;
            val = arr[h]; // update new val
        }
        // at this point we have updated low
        // and high indices, thus use binary
        // search between them
        return binarySearch(arr, l, h, key);
    }

    // Driver method to test the above function
    public static void main(String[] args) {
        int arr[] = new int[] { 3, 5, 7, 9, 10, 90,
                100, 130, 140, 160, 170 };
        int ans = findPos(arr, 10);
        if (ans == -1)
            System.out.println("Element not found");
        else
            System.out.println("Element found at index " + ans);
    }
}
```

### Square root of an integer

```java
// A Java program to find floor(sqrt(x) 
class Solution {
    public static int floorSqrt(int x) {
        // Base Cases
        if (x == 0 || x == 1)
            return x;
        // Do Binary Search for floor(sqrt(x))
        int start = 1, end = x, ans = 0;
        while (start <= end) {
            int mid = (start + end) / 2;
            // If x is a perfect square
            if (mid * mid == x)
                return mid;
            // Since we need floor, we update answer when mid*mid is
            // smaller than x, and move closer to sqrt(x)
            if (mid * mid < x) {
                start = mid + 1;
                ans = mid;
            } else // If mid*mid is greater than x
                end = mid - 1;
        }
        return ans;
    }

    // Driver Method
    public static void main(String[] args) {
        int x = 11;
        System.out.println(floorSqrt(x));
    }
}
```

### Find pair in unsorted array which gives sum X

```java
import java.util.HashSet;

class Solution {
    static void printpairs(int arr[], int sum) {
        HashSet<Integer> s = new HashSet<Integer>();
        for (int i = 0; i < arr.length; ++i) {
            int temp = sum - arr[i];
            // checking for condition
            if (s.contains(temp)) {
                System.out.println("Pair with given sum " + sum + " is (" + arr[i] + ", " + temp + ")");
            }
            s.add(arr[i]);
        }
    }

    // Main to test the above function
    public static void main(String[] args) {
        int A[] = { 1, 4, 45, 6, 10, 8 };
        int n = 16;
        printpairs(A, n);
    }
}
```

### Find pair in sorted array which gives sum X

```java
class Solution {
    static int isPresent(int arr[], int n, int sum) {
        int l = 0, h = n - 1;
        while (l <= h) {
            if (arr[l] + arr[h] == sum)
                return 1;
            else if (arr[l] + arr[h] > sum)
                h--;
            else
                l++;
        }
        return 0;
    }

    public static void main(String[] args) {
        int arr[] = new int[] { 2, 3, 7, 8, 11 };
        int n = arr.length;
        int sum = 14;
        System.out.println(isPresent(arr, n, sum));
    }
}
```

### Find triplet in an array which gives sum X

```java
class Solution {
    // returns true if there is triplet with sum equal
    // to 'sum' present in A[]. Also, prints the triplet
    boolean find3Numbers(int A[], int arr_size, int sum) {
        int l, r;
        /* Sort the elements */
        quickSort(A, 0, arr_size - 1);
        /*
         * Now fix the first element one by one and find the
         * other two elements
         */
        for (int i = 0; i < arr_size - 2; i++) {
            // To find the other two elements, start two index variables
            // from two corners of the array and move them toward each
            // other
            l = i + 1; // index of the first element in the remaining elements
            r = arr_size - 1; // index of the last element
            while (l < r) {
                if (A[i] + A[l] + A[r] == sum) {
                    System.out.print("Triplet is " + A[i] + ", " + A[l] + ", " + A[r]);
                    return true;
                } else if (A[i] + A[l] + A[r] < sum)
                    l++;
                else // A[i] + A[l] + A[r] > sum
                    r--;
            }
        }
        // If we reach here, then no triplet was found
        return false;
    }

    int partition(int A[], int si, int ei) {
        int x = A[ei];
        int i = (si - 1);
        int j;
        for (j = si; j <= ei - 1; j++) {
            if (A[j] <= x) {
                i++;
                int temp = A[i];
                A[i] = A[j];
                A[j] = temp;
            }
        }
        int temp = A[i + 1];
        A[i + 1] = A[ei];
        A[ei] = temp;
        return (i + 1);
    }

    /*
     * Implementation of Quick Sort
     * A[] --> Array to be sorted
     * si --> Starting index
     * ei --> Ending index
     */
    void quickSort(int A[], int si, int ei) {
        int pi;
        /* Partitioning index */
        if (si < ei) {
            pi = partition(A, si, ei);
            quickSort(A, si, pi - 1);
            quickSort(A, pi + 1, ei);
        }
    }

    // Driver program to test above functions
    public static void main(String[] args) {
        FindTriplet triplet = new FindTriplet();
        int A[] = { 1, 4, 45, 6, 10, 8 };
        int sum = 22;
        int arr_size = A.length;
        triplet.find3Numbers(A, arr_size, sum);
    }
}
```
