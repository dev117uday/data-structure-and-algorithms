# LeetCode

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

```java
import java.util.HashSet;
import java.util.Set;

class Solution {
	public boolean containsDuplicate(int[] nums) {

		Set<Integer> set = new HashSet<>();
		for (int ele : nums) {
			if (set.contains(ele)) {
				return true;
			}

			set.add(ele);
		}

		return false;
	}
}
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
import java.util.HashMap;
import java.util.Map;

class Solution {
    public int[] twoSum(int[] nums, int target) {
     
         if (nums.length == 2) {
            return new int[] {0,1};
        }
        
        Map<Integer,Integer> hmap = new HashMap<>();
        hmap.put(nums[0],0);
        
        for(int i=1; i<nums.length; i++) {
            if(hmap.containsKey(target - nums[i])) {
                return new int[]{ hmap.get(target - nums[i]), i };
            }
            hmap.put(nums[i],i);
        }
    
        return new int[]{0,0};
        
        
    }
}
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
	public void merge(int[] nums1, int m, int[] nums2, int n) {

		int mainid = nums1.length - 1;
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
}
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
import java.util.ArrayList;
import java.util.HashMap;

class Solution {
	public int[] intersect(int[] nums1, int[] nums2) {
		ArrayList<Integer> arr = new ArrayList<Integer>();
		HashMap<Integer, Integer> map = new HashMap<>();
		for (int i = 0; i < nums1.length; i++) {
			if (map.containsKey(nums1[i])) {
				int value = map.get(nums1[i]);
				map.replace(nums1[i], value + 1);
			} else {
				map.put(nums1[i], 1);
			}
		}

		for (int i = 0; i < nums2.length; i++) {
			if (map.containsKey(nums2[i]) 
				&& map.get(nums2[i]).intValue() > 0) {
				arr.add(nums2[i]);
				map.replace(nums2[i], 
					map.get(nums2[i]).intValue() - 1);
			}
		}

		return arr.stream().mapToInt(i -> i).toArray();
	}
}
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
