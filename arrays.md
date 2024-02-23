# Arrays

### Left most index of an element

* Count of occurrences of x in sorted element
* Count of 1s in binary sorted array

1. Perform binary search to the left most element
2. Perform the required operation from that side

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

### Contains Duplicate

[https://leetcode.com/problems/contains-duplicate/](https://leetcode.com/problems/contains-duplicate/)

```
Given an integer array nums, return true if any value appears 
at least twice in the array, and return false if every element is distinct. 

Example 1:

Input: nums = [1,2,3,1]
Output: true
Example 2:

Input: nums = [1,2,3,4]
Output: false
Example 3:

Input: nums = [1,1,1,3,3,4,3,2,4,2]
Output: true
```

```cpp
class Solution {
public:
    bool containsDuplicate(vector<int>& nums) {
        unordered_set<int> st;
        bool flag = false;
        for(int i: nums) {
            if(st.find(i)==st.end()) {
                st.insert(i);
            } else {
                return true;
            }
        }
        return false;
    }
};
```

### Maximum Subarray

[https://leetcode.com/problems/maximum-subarray/](https://leetcode.com/problems/maximum-subarray/)

```
Given an integer array nums, 
find the contiguous subarray (containing at least one number) 
which has the largest sum and return its sum.

A subarray is a contiguous part of an array.

Example 1:

Input: nums = [-2,1,-3,4,-1,2,1,-5,4]
Output: 6
Explanation: [4,-1,2,1] has the largest sum = 6.
Example 2:

Input: nums = [1]
Output: 1
```

```java
class Solution {
	public int maxSubArray(int[] nums) {

		int maxsum = Integer.MIN_VALUE;
		int maxcalc = 0;

		for (int ele : nums) {
			maxcalc = maxcalc + ele;

			if (maxsum < maxcalc) {
				maxsum = maxcalc;
			}

			if (maxcalc < 0) {
				maxcalc = 0;
			}
		}

		return maxsum;
	}
}
```

### Two Sum

[https://leetcode.com/problems/two-sum/](https://leetcode.com/problems/two-sum/)

```
Given an array of integers nums and an integer target, 
return indices of the two numbers such that they add up to target.

You may assume that each input would have exactly one solution, 
and you may not use the same element twice.

You can return the answer in any order.

Example 1:

Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].
```

```java
class Solution
{
public:
    vector<int> twoSum(vector<int> &nums, int target)
    {

        vector<int> ans;
        if (nums.size() == 2)
        {
            ans.push_back(0); ans.push_back(1);
            return ans;
        }

        map<int, int> hmap;

        for (int i = 0; i < nums.size(); i++)
        {
            int temp = target - nums[i];
            if (hmap.find(temp) != hmap.end())
            {
                ans.push_back(i);
                ans.push_back(hmap[temp]);
                return ans;
            }
            hmap[nums[i]] = i;
        }

        return ans;
    }
};
```

### Merge Sorted Array

[https://leetcode.com/problems/merge-sorted-array/](https://leetcode.com/problems/merge-sorted-array/)

```
You are given two integer arrays nums1 and nums2, 
sorted in non-decreasing order, and two integers m and n, 
representing the number of elements in nums1 and nums2 respectively.

Merge nums1 and nums2 into a single array sorted in non-decreasing order.

Input: nums1 = [1,2,3,0,0,0], m = 3, nums2 = [2,5,6], n = 3
Output: [1,2,2,3,5,6]
Explanation: The arrays we are merging are [1,2,3] and [2,5,6].
The result of the merge is [1,2,2,3,5,6] 
    with the underlined elements coming from nums1.
```

```java
class Solution {
public:
    void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
		int mainid = nums1.size() - 1;
		int fend = m - 1;
		int send = n - 1;
		while (fend >= 0 && send >= 0) {
			if (nums1[fend] > nums2[send]) {
				nums1[mainid--] = nums1[fend--];
			} else {
				nums1[mainid--] = nums2[send--];
			}
		}

		while (fend >= 0) {
			nums1[mainid--] = nums1[fend--];
		}

		while (send >= 0) {
			nums1[mainid--] = nums2[send--];
		}
    }
};
```

### Intersection of Two Arrays II

[https://leetcode.com/problems/intersection-of-two-arrays-ii/](https://leetcode.com/problems/intersection-of-two-arrays-ii/)

```java
Given two integer arrays nums1 and nums2, 
return an array of their intersection. 

Each element in the result must appear as many times 
as it shows in both arrays and you may return the 
result in any order.

Example 1:

Input: nums1 = [1,2,2,1], nums2 = [2,2]
Output: [2,2]
Example 2:

Input: nums1 = [4,9,5], nums2 = [9,4,9,8,4]
Output: [4,9]
Explanation: [9,4] is also accepted.
```

```java
class Solution {
public:
    vector<int> intersect(vector<int>& nums1, vector<int>& nums2) {
        int n=nums1.size();
        int m=nums2.size();
        vector<int> res;
        unordered_map<int,int> map1;
        unordered_map<int,int> map2;
        for(int i=0;i<n;i++){
            map1[nums1[i]]++;
        }
        for(int j=0;j<m;j++){
            map2[nums2[j]]++;
        }
        for(auto& num : nums1){
            if(map2[num]-->0){
                res.push_back(num);
            } 
        } return res;
    }
};
```

### Best Time to Buy and Sell Stock

[https://leetcode.com/problems/best-time-to-buy-and-sell-stock/](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)

```
You are given an array prices where prices[i] 
is the price of a given stock on the ith day.

You want to maximize your profit by choosing a single day to 
buy one stock and choosing a different day in the future to sell that stock.

Input: prices = [7,1,5,3,6,4]
Output: 5
Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), 
profit = 6-1 = 5.

Note that buying on day 2 and selling on day 1 is not 
    allowed because you must buy before you sell.
```

```java
class Solution {
	public int maxProfit(int[] prices) {
		int maxProfit = 0;
		int minBuy = prices[0], maxSell = prices[0];

		for (int n : prices) {
			if (n < minBuy) {
				minBuy = n;
				maxSell = n;
			} else if (n > maxSell) {
				maxSell = n;
			}
			maxProfit = Math.max(maxProfit, maxSell - minBuy);
		}
		return maxProfit;

	}
}
```

### Binary Search

[https://leetcode.com/problems/binary-search/](https://leetcode.com/problems/binary-search/)

Given an array of integers `nums` which is sorted in ascending order, and an integer `target`, write a function to search `target` in `nums`. If `target` exists, then return its index. Otherwise, return `-1`.

```java
Input: nums = [-1,0,3,5,9,12], target = 9
Output: 4
Explanation: 9 exists in nums and its index is 4
```

```java
class Solution {
	public int search(int[] nums, int target) {

		int left = 0;
		int right = nums.length - 1;

		while (left <= right) {
			int mid = left + (right - left) / 2;

			if (nums[mid] == target) {
				return mid;
			}

			if (nums[mid] > target) {
				right = mid - 1;
			} else {
				left = mid + 1;
			}
		}

		return -1;

	}
}
```

### Search Insert Position

[https://leetcode.com/problems/search-insert-position/](https://leetcode.com/problems/search-insert-position/)

Given a sorted array of distinct integers and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

You must write an algorithm with `O(log n)` runtime complexity.

```java
class Solution {
	public int searchInsert(int[] nums, int target) {

		int left = 0;
		int right = nums.length - 1;

		while (left <= right) {

			int mid = left + (right - left) / 2;

			if (nums[mid] > target) {
				right = mid - 1;
			} else if (nums[mid] < target) {
				left = mid + 1;
			} else {
				return mid;
			}
		}

		return left;

	}
}
```

### Squares of a Sorted Array

[https://leetcode.com/problems/squares-of-a-sorted-array/](https://leetcode.com/problems/squares-of-a-sorted-array/)

```
Given an integer array nums sorted in non-decreasing order, 
return an array of the squares of each number sorted in non-decreasing order.

Example 1:

Input: nums = [-4,-1,0,3,10]
Output: [0,1,9,16,100]
Explanation: After squaring, the array becomes [16,1,0,9,100].
After sorting, it becomes [0,1,9,16,100].
```

```java
class Solution {
	public int[] sortedSquares(int[] nums) {
		int start = 0;
		int end = nums.length - 1;
		int pointer = nums.length - 1;
		int[] result = new int[nums.length];

		while (start <= end) {
			if (Math.abs(nums[start]) > Math.abs(nums[end])) {
				result[pointer] = nums[start] * nums[start];
				start++;
			} else {
				result[pointer] = nums[end] * nums[end];
				end--;
			}
			pointer--;
		}

		return result;
	}
}
```

### Rotate Array

[https://leetcode.com/problems/rotate-array/](https://leetcode.com/problems/rotate-array/)

```java
Given an array, rotate the array to the right by k steps, 
where k is non-negative.

Example 1:

Input: nums = [1,2,3,4,5,6,7], k = 3
Output: [5,6,7,1,2,3,4]
Explanation:
rotate 1 steps to the right: [7,1,2,3,4,5,6]
rotate 2 steps to the right: [6,7,1,2,3,4,5]
rotate 3 steps to the right: [5,6,7,1,2,3,4]
```

```java
class Solution {
	public void swap(int low, int high, int[] arr) {
		while (low < high) {
			int temp = arr[low];
			arr[low] = arr[high];
			arr[high] = temp;
			low++;
			high--;
		}
	}

	public void rotate(int[] nums, int k) {
		if (k == 0) {
			return;
		}
		if (k > nums.length) {
			k = k % nums.length;
		}
		swap(0, nums.length - k - 1, nums);
		swap(nums.length - k, nums.length - 1, nums);
		swap(0, nums.length - 1, nums);
	}
}
```

### Move Zeroes

[https://leetcode.com/problems/move-zeroes/](https://leetcode.com/problems/move-zeroes/)

```
Given an integer array nums, move all 0's to the end of it 
while maintaining the relative order of the non-zero elements.

Note that you must do this in-place without making a copy of the array.
```

```java
class Solution {
	public void moveZeroes(int[] nums) {

		int i = 0;
		for (int j = 0; j <= nums.length - 1; j++) {
			if (nums[j] == 0) {
				continue;
			} else {
				nums[i] = nums[j];
				i++;
			}
		}

		for (int x = i; x <= nums.length - 1; x++) {
			nums[x] = 0;
		}
	}
}
```

### Two Sum II - Input Array Is Sorted

[https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/)

```java
Given a 1-indexed array of integers numbers that is 
already sorted in non-decreasing order, 
find two numbers such that they add up to a specific target number. 

Let these two numbers be numbers[index1] and numbers[index2] 
where 1 <= index1 < index2 <= numbers.length.

Return the indices of the two numbers, index1 and index2, 
added by one as an integer array [index1, index2] of length 2.

Example 1:

Input: numbers = [2,7,11,15], target = 9
Output: [1,2]
Explanation: The sum of 2 and 7 is 9. 
Therefore, index1 = 1, index2 = 2. We return [1, 2].
```

```java
class Solution {
	public int[] twoSum(int[] numbers, int target) {
		int leftPtr = 0;
		int rightPtr = numbers.length - 1;
		int currentSum = 0;
		while (leftPtr <= rightPtr) {
			int leftEle = numbers[leftPtr];
			int rightEle = numbers[rightPtr];
			currentSum = leftEle + rightEle;
			if (currentSum == target) {
				return new int[] { leftPtr + 1, rightPtr + 1 };
			} else if (currentSum < target) {
				leftPtr++;
			} else {
				rightPtr--;
			}
		}
		return new int[] {};
	}
}
```

### Largest Subarray with Sum Zero

```java
import java.util.*;

class Solution {
    public static void main(String[] args) {
        int arr[] = new int[] { 5, 3, 9, -4, -6, 7, -1 };
        int n = arr.length;
        System.out.println(ZeroSumSubarray(arr, n));
    }

    static int ZeroSumSubarray(int arr[], int n) {
        Set<Integer> us = new HashSet<Integer>();
        int prefix_sum = 0;
        us.add(0);
        for (int i = 0; i < n; i++) {
            prefix_sum += arr[i];
            if (us.contains(prefix_sum) == true)
                return 1;
            us.add(prefix_sum);
        }
        return 0;
    }
}
```

### Largest Subarray with Sum X

```java
import java.util.HashSet;

class Solution {
    public static void main(String[] args) {
        int arr[] = new int[]{8, 3, -7, -4, 1};
        int n = arr.length;
        int sum = -8;
        System.out.println(largestSubarrayWithSumX(arr, n, sum));
    }

    static int largestSubarrayWithSumX(int arr[], int n, int sum) {
        int prefix_sum = 0;
        HashSet<Integer> us = new HashSet<>();
        us.add(0);
        for (int i = 0; i < n; i++) {
            prefix_sum += arr[i];
            if (us.contains(prefix_sum - sum))
                return 1;
            us.add(prefix_sum);
        }
        return 0;
    }
}
```

### Longest Subarray with equal 0s and 1s

```java
import java.util.*;

class Solution {
    public static void main(String[] args) {
        int arr[] = new int[] { 1, 1, 1, 0, 1, 0, 1, 1, 1 };
        int len = arr.length;
        System.out.println(largestZeroSubarray(arr, len));
    }

    static int largestZeroSubarray(int arr[], int n) {
        Map<Integer, Integer> hm = new HashMap<Integer, Integer>();
        int sum = 0, maxLen = 0;
        for (int i = 0; i < n; i++)
            arr[i] = (arr[i] == 0) ? -1 : 1;
        for (int i = 0; i < n; i++) {
            sum += arr[i];
            if (sum == 0)
                maxLen = i + 1;
            if (hm.containsKey(sum + n) == true) {
                if (maxLen < i - hm.get(sum + n))
                    maxLen = i - hm.get(sum + n);
            } else
                hm.put(sum + n, i);
        }
        return maxLen;
    }
}
```

### Find pair with having sum X in unsorted array

```java
import java.util.*;

class Solution {
    public static void main(String[] args) {
        int arr[] = new int[] { 3, 8, 4, 7, 6, 1 };
        int len = arr.length;
        int x = 14;
        System.out.println(pairWithSumX(arr, len, x));
    }

    static int pairWithSumX(int arr[], int n, int X) {
        HashSet<Integer> us = new HashSet<>();
        for (int i = 0; i < n; i++) {
            if (us.contains(X - arr[i]))
                return 1;
            us.add(arr[i]);
        }
        return 0;
    }
}
```

### Reverse an array

```java
class Solution {

    static void reverse(int arr[], int n) {
        for (int i = 0; i < n / 2; i++) {
            int temp = arr[i];
            arr[i] = arr[n - i - 1];
            arr[n - i - 1] = temp;
        }

        int start = 0;
        int end = arr.length - 1;

        while (start < end) {
            int temp = arr[start];
            arr[start] = arr[end];
            arr[end] = temp;
            start++;
            end--;
        }
    }

    public static void main(String[] args) {
        int arr[] = new int[] { 2, 8, 7, 10, 5 };
        int n = arr.length;

        reverse(arr, n);
        for (int i = 0; i < n; i++)
            System.out.print(arr[i] + " ");
    }
}
```

### Rotate an array by number by D

link : [https://leetcode.com/problems/rotate-array/](https://leetcode.com/problems/rotate-array/)

```java
class Solution {
	public void rotate(int[] nums, int k) {
		int n = nums.length;
		k %= nums.length;
		reverse(nums, 0, n - 1);
		reverse(nums, 0, k - 1);
		reverse(nums, k, n - 1);
	}

	static void reverse(int arr[], int start, int end) {
		int temp = 0;
		while (start < end) {
			temp = arr[start];
			arr[start] = arr[end];
			arr[end] = temp;
			start++;
			end--;
		}
	}
}
```

### Replace Elements with Greatest Element on Right Side

link : [https://leetcode.com/problems/replace-elements-with-greatest-element-on-right-side/](https://leetcode.com/problems/replace-elements-with-greatest-element-on-right-side/)

```java
import java.util.Arrays;

class Solution {
	public int[] replaceElements(int[] arr) {
		int max = -1;
        for (int i = arr.length - 1; i >= 0; i--) {
			var temp = arr[i];
			arr[i] = max;
			max = Math.max(max, temp);
		}
		return arr;
	}

    public static void main(String[] args) {
        Solution sol = new Solution();
        var arr = sol.replaceElements(new int[]{17,18,5,4,6,1});
        System.out.println(Arrays.toString(arr));
        // [18, 6, 6, 6, 1, -1]
    }
}
```

### Prefix Sum array

* input : 10, 4, 16, 20
* output : 10 14 30 50

```java
class Solution {
	// Fills prefix sum array
	static void fillPrefixSum(int[] arr, int n, int[] prefixSum) {
		prefixSum[0] = arr[0];

		// Adding present element
		// with previous element
		for (int i = 1; i < n; ++i)
			prefixSum[i] = prefixSum[i - 1] + arr[i];
	}

	// Driver code
	public static void main(String[] args) {
		int[] arr = { 10, 4, 16, 20 };
		int n = arr.length;
		int[] prefixSum = new int[n];

		fillPrefixSum(arr, n, prefixSum);

		for (int i = 0; i < n; i++)
			System.out.print(prefixSum[i] + " ");

	}
}
```

### Find Pivot Index or Equilibrium Point

[https://leetcode.com/problems/find-pivot-index/](https://leetcode.com/problems/find-pivot-index/)

```java
class Solution {
	public int pivotIndex(int[] nums) {

		int sum = 0;

		for (int ele : nums) {
			sum += ele;
		}

		int leftsum = 0;
		for (int i = 0; i < nums.length; i++) {
			if (leftsum == sum - leftsum - nums[i]) {
				return i;
			}
			leftsum += nums[i];
		}

		return -1;
	}
}
```

### Maximum occurred integer in N ranges\*

Here `L[i]` and `R[i]` present ranges : 1- 15, 4-8, 9-12 etc...

* mark the starting of the range with 1 and ending with -1 on the next element after the range ends, do this for all ranges
* find the prefix sum array for the array and find the max element, the index will the be most occur ed integer in N ranges

```java
class Solution {

	static int MAX = 1000000;

	// Return the maximum occurred element in all ranges.
	static int maximumOccuredElement(int[] L, int[] R, int n) {
		// Initalising all element of array to 0.
		int[] arr = new int[MAX];

		// to find the last range 
		int maxi = -1;
		
		for (int i = 0; i < n; i++) {
			arr[L[i]] += 1;
			arr[R[i] + 1] -= 1;
			if (R[i] > maxi) {
				maxi = R[i];
			}
		}

		// Finding prefix sum and index
		// having maximum prefix sum.
		int msum = arr[0];
		int ind = 0;
		for (int i = 1; i < maxi + 1; i++) {
			arr[i] += arr[i - 1];
			if (msum < arr[i]) {
				msum = arr[i];
				ind = i;
			}
		}
		return ind;
	}

	// Driver program
	static public void main(String[] args) {
		int[] L = { 1, 4, 9, 13, 21 };
		int[] R = { 15, 8, 12, 20, 30 };
		int n = L.length;
		System.out.println(maximumOccuredElement(L, R, n));
	}
}
```

### Strongest Neighbour | Find Peak Element

link : [https://leetcode.com/problems/find-peak-element/](https://leetcode.com/problems/find-peak-element/)

```java
public class Solution {
    public int findPeakElement(int[] nums) {
        for (int i = 0; i < nums.length - 1; i++) {
            if (nums[i] > nums[i + 1])
                return i;
        }
        return nums.length - 1;
    }
}
```

### First Missing Positive

link : [https://leetcode.com/problems/first-missing-positive/](https://leetcode.com/problems/first-missing-positive/)

```java
class Solution {
	public int firstMissingPositive(int[] nums) {

		Set<Integer> set = new TreeSet<>();
		for (int i = 0; i < nums.length; i++) {
			if (nums[i] > 0)
				set.add(nums[i]);
		}
		for (int i = 0; i < nums.length; i++) {
			if (!set.contains(i + 1))
				return i + 1;
		}
		return nums.length + 1;
	}
}
```

### Rearrange array alternatively

```
- Input:
N = 6
arr[] = {1,2,3,4,5,6}

- Output: 
6 1 5 2 4 3
Modified array is : 6 1 5 2 4 3

Explanation: Max element = 6, min = 1, second max = 5, second min = 2, 
and so on... 
```

```java
public class Solution {

	// Prints max at first position, min at second
	// position second max at third position, second
	// min at fourth position and so on.
	public static void rearrange(int arr[], int n) {

		// initialize index of first minimum and first
		// maximum element
		int max_ele = arr[n - 1];
		int min_ele = arr[0];

		// traverse array elements
		for (int i = 0; i < n; i++) {
			
			// at even index : we have to put maximum element
			if (i % 2 == 0) {
				arr[i] = max_ele;
				max_ele -= 1;
			}

			// at odd index : we have to put minimum element
			else {
				arr[i] = min_ele;
				min_ele += 1;
			}
		}
	}

	// Driver code
	public static void main(String args[]) {
		int arr[] = { 1, 2, 3, 4, 5, 6, 7, 8, 9 };
		int n = arr.length;

		System.out.println("Original Array");
		for (int i = 0; i < n; i++)
			System.out.print(arr[i] + " ");

		rearrange(arr, n);

		System.out.print("\nModified Array\n");
		for (int i = 0; i < n; i++)
			System.out.print(arr[i] + " ");
	}
}

```

### Rearrange the array

Given an array **arr\[]** of size **N** where every element is in the range from **0 to n-1**. Rearrange the given array so that **arr\[i]** becomes **arr\[arr\[i]]**.

```java
class Solution {
	// The function to rearrange an array in-place so that arr[i]
	// becomes arr[arr[i]].
	static void rearrange(int arr[], int n) {
		// First step: Increase all values by (arr[arr[i]]%n)*n
		for (int i = 0; i < n; i++)

			// learn
			arr[i] += (arr[arr[i]] % n) * n;

		// Second Step: Divide all values by n
		// learn
		for (int i = 0; i < n; i++)
			arr[i] /= n;
	}

	// A utility function to print an array of size n
	static void printArr(int arr[], int n) {
		for (int i = 0; i < n; i++)
			System.out.print(arr[i] + " ");
		System.out.println("");
	}

	/* Driver program to test above functions */
	public static void main(String[] args) {
		int arr[] = { 3, 2, 0, 1 };
		int n = arr.length;

		System.out.println("Given Array is :");
		printArr(arr, n);

		rearrange(arr, n);

		System.out.println("Modified Array is :");
		printArr(arr, n);
	}
}
```

### Maximum Index

```java
class Solution {

	/*
	 * For a given array arr[], returns the maximum j-i such that
	 * arr[j] > arr[i]
	 */
	static int maxIndexDiff(int arr[], int n) {
		int maxDiff;
		int i, j;

		int RMax[] = new int[n];
		int LMin[] = new int[n];

	/*
	 * Construct LMin[] such that LMin[i] stores the minimum value
	 * from (arr[0], arr[1], ... arr[i])
	 */
		LMin[0] = arr[0];
		for (i = 1; i < n; ++i)
			LMin[i] = Math.min(arr[i], LMin[i - 1]);

	/*
	 * Construct RMax[] such that RMax[j] stores the maximum value
	 * from (arr[j], arr[j+1], ..arr[n-1])
	 */
		RMax[n - 1] = arr[n - 1];
		for (j = n - 2; j >= 0; --j)
			RMax[j] = Math.max(arr[j], RMax[j + 1]);

	/*
	 * Traverse both arrays from left to right to find optimum j - i
	 * This process is similar to merge() of MergeSort
	 */
		i = 0;
		j = 0;
		maxDiff = -1;
		while (j < n && i < n) {
			if (LMin[i] <= RMax[j]) {
				maxDiff = Math.max(maxDiff, j - i);
				j = j + 1;
			} else
				i = i + 1;
		}

		return maxDiff;
	}

	/* Driver program to test the above functions */
	public static void main(String[] args) {
		int arr[] = { 9, 2, 3, 4, 5, 6, 7, 8, 18, 0 };
		int n = arr.length;
		int maxDiff = maxIndexDiff(arr, n);
		System.out.println(maxDiff);
	}
}

```

### Check if array is sorted and rotated

```java
class Solution {

	// Function to check if an array is
	// Sorted and rotated clockwise
	static boolean checkIfSortRotated(int arr[], int n) {
		// Initializing two variables x,y as zero.
		int x = 0, y = 0;

		// Traversing array 0 to last element.
		// n-1 is taken as we used i+1.
		for (int i = 0; i < n - 1; i++) {
			if (arr[i] < arr[i + 1])
				x++;
			else
				y++;
		}

		// If till now both x,y are greater
		// then 1 means array is not sorted.
		// If both any of x,y is zero means
		// array is not rotated.
		if (x == 1 || y == 1) {
			// Checking for last element with first.
			if (arr[n - 1] < arr[0])
				x++;
			else
				y++;

			// Checking for final result.
			if (x == 1 || y == 1)
				return true;
		}
		// If still not true then definitely false.
		return false;
	}

	// Driver code
	public static void main(String[] args) {
		int arr[] = { 5, 1, 2, 3, 4 };

		int n = arr.length;

		// Function Call
		boolean x = checkIfSortRotated(arr, n);
		if (x == true)
			System.out.println("YES");
		else
			System.out.println("NO");
	}
}
```

### Trapping Rainwater

* Step 1 : Find the max of ( tallest bar to the left `left[]` , itself )
  * This will give the tallest bar on left till which it can hold water
* Step 2 : Find the max of ( tallest bar to the `right` , itself )
  * This will give the tallest bar on right till which it can hold water
* Step 3 : Find the sum : `water += min ( left[i] , right[i] ) - arr[i]`
  * This will give you the water captured in between the bars

link : [https://leetcode.com/problems/trapping-rain-water/](https://leetcode.com/problems/trapping-rain-water/)

```java
class Solution {
	public int trap(int[] height) {
		int[] leftPeak = new int[height.length];
		int[] rightPeak = new int[height.length];

		// from left to right, we track all the peaks we see
		int l = 0;
		for (int i = 0; i < height.length; i++) {
			l = Math.max(l, height[i]);
			leftPeak[i] = l;
		}

		// from right to left, we track all the peaks we see
		int r = 0;
		for (int i = height.length - 1; i >= 0; i--) {
			r = Math.max(r, height[i]);
			rightPeak[i] = r;
		}

		// for each cell we compute the amount of water knowing left and right peak
		int water = 0;
		for (int i = 0; i < height.length; i++) {
			int h = Math.min(leftPeak[i], rightPeak[i]);
			water += h - height[i];
		}
		return water;
	}
}
```

### Best Time to Buy and Sell Stock

link : [https://leetcode.com/problems/best-time-to-buy-and-sell-stock/](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)

```java
class Solution {
	public int maxProfit(int[] prices) {
		int maxProfit = 0;
		int minBuy = prices[0], maxSell = prices[0];

		for (int n : prices) {
			if (n < minBuy) {
				minBuy = n;
				maxSell = n;
			} else if (n > maxSell) {
				maxSell = n;
			}
			maxProfit = Math.max(maxProfit, maxSell - minBuy);
		}
		return maxProfit;
	}
}
```

### Best Time to Buy and Sell Stock II

link : [https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/)

```java
class Solution {
	public int maxProfit(int[] prices) {
		int maxprofits = 0;

		for (int i = 0; i < prices.length - 1; i++) {
			if (prices[i] < prices[i + 1]) {
				maxprofits += prices[i + 1] - prices[i];
			}
		}
		return maxprofits;
	}
}
```

### Best Time to Buy and Sell Stock III

link : [https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iii/](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iii/)

```java
class Solution {
    public int maxProfit(int[] prices) {
        int n = prices.length;
        int arr[] = new int[n];
        arr[0] = 0;
        int min = prices[0];
        for (int i = 1; i < n; i++) {
            arr[i] = Math.max(arr[i - 1], prices[i] - min);
            min = Math.min(min, prices[i]);
        }
        int brr[] = new int[n];
        brr[n - 1] = 0;
        int max = prices[n - 1];
        for (int i = n - 2; i >= 0; i--) {
            brr[i] = Math.max(brr[i + 1], max - prices[i]);
            max = Math.max(max, prices[i]);
        }
        int ans = 0;
        for (int i = 0; i < n; i++) {
            ans = Math.max(ans, arr[i] + brr[i]);
        }
        return ans;
    }
}
```

### Sub array Sum Equals K

link : [https://leetcode.com/problems/subarray-sum-equals-k/](https://leetcode.com/problems/subarray-sum-equals-k/)

```java
public class Solution {
    public int subarraySum(int[] nums, int k) {
        int count = 0, sum = 0;
        HashMap < Integer, Integer > map = new HashMap < > ();
        map.put(0, 1);
        for (int i = 0; i < nums.length; i++) {
            sum += nums[i];
            if (map.containsKey(sum - k))
                count += map.get(sum - k);
            map.put(sum, map.getOrDefault(sum, 0) + 1);
        }
        return count;
    }
}
```

### Minimum Size Sub array Sum

link : [https://leetcode.com/problems/minimum-size-subarray-sum/](https://leetcode.com/problems/minimum-size-subarray-sum/)

```java
class Solution {
    public int minSubArrayLen(int target, int[] nums) {
        int leftPos = 0, ret = Integer.MAX_VALUE, curSum = 0;
        boolean flag = false;
        for (int i = 0; i < nums.length; i++) {
            curSum += nums[i];
            if (curSum >= target) {
                flag = true;
                while (curSum >= target) {
                    curSum -= nums[leftPos++];
                }
                ret = Math.min(ret, i - leftPos + 2);
            }
        }

        return flag ? ret : 0;
    }
}
```

### Sum of Sub array Minimums

link : [https://leetcode.com/problems/sum-of-subarray-minimums/](https://leetcode.com/problems/sum-of-subarray-minimums/)

```java
public class Solution {
    public int subarraySum(int[] nums, int k) {
        int count = 0, sum = 0;
        HashMap < Integer, Integer > map = new HashMap < > ();
        map.put(0, 1);
        for (int i = 0; i < nums.length; i++) {
            sum += nums[i];
            if (map.containsKey(sum - k))
                count += map.get(sum - k);
            map.put(sum, map.getOrDefault(sum, 0) + 1);
        }
        return count;
    }
}
```

### Maximum Sub array | Kadane Algorithm

link : [https://leetcode.com/problems/maximum-subarray/](https://leetcode.com/problems/maximum-subarray/)

```java
class Solution {
	public int maxSubArray(int[] nums) {

		int maxsum = Integer.MIN_VALUE;
		int maxcalc = 0;

		for (int ele : nums) {
			maxcalc = maxcalc + ele;

			if (maxsum < maxcalc) {
				maxsum = maxcalc;
			}

			if (maxcalc < 0) {
				maxcalc = 0;
			}
		}
		return maxsum;
	}
}
```

#### Kadane Algorithm

```java
class Solution {

	static void maxSubArraySum(int a[], int size) {
		int max_so_far = Integer.MIN_VALUE,
				max_ending_here = 0, start = 0,
				end = 0, s = 0;

		for (int i = 0; i < size; i++) {
			max_ending_here += a[i];

			if (max_so_far < max_ending_here) {
				max_so_far = max_ending_here;
				start = s;
				end = i;
			}

			if (max_ending_here < 0) {
				max_ending_here = 0;
				s = i + 1;
			}
		}
		System.out.println("Maximum contiguous sum is "
				+ max_so_far);
		System.out.println("Starting index " + start);
		System.out.println("Ending index " + end);
	}

	// Driver code
	public static void main(String[] args) {
		int a[] = { -2, -3, 4, -1, -2, 1, 5, -3 };
		int n = a.length;
		maxSubArraySum(a, n);
	}
}
```

### Sliding Window Maximum

```java
import java.util.ArrayList;
import java.util.Arrays;

public class Solution {

	public static int[] maxSlidingWindow(int[] nums, int k) {

		int sum = 0;
		int max = Integer.MIN_VALUE;

		for (int i = 0; i < k; i++) {
			sum += nums[i];
		}

		int index = 0;

		for (int i = k; i < nums.length; i++) {
			sum = sum - nums[i - k] + nums[i];
			if (sum > max) {
				max = sum;
				index = i;
			}
		}

		ArrayList<Integer> arr = new ArrayList<>();
		for (int i = index - k +1, j = 0; j < k; j++, i++) {
			arr.add(nums[i]);
		}

		return arr.stream().mapToInt(i -> i).toArray();
	}

	public static void main(String[] args) throws Exception {
		int[] nums = new int[] { 1, 3, -1, -3, 5, 3, 6, 7 };
		int k = 3;
		System.out.println(Arrays.toString(maxSlidingWindow(nums, k)));
	}
}

```

### Maximum Gap

link : [https://leetcode.com/problems/maximum-gap/](https://leetcode.com/problems/maximum-gap/)

```cpp
class Solution
{
public:
	int maxSubArray(vector<int> &nums)
	{
		int maxsum = -99990;
		int maxcalc = 0;
		for (int ele : nums)
		{
			maxcalc = maxcalc + ele;
			if (maxsum < maxcalc)
				maxsum = maxcalc;

			if (maxcalc < 0)
				maxcalc = 0;
		}
		return maxsum;
	}
};
```
