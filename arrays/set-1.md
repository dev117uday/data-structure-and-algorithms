# Set 1

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

{% tabs %}
{% tab title="Java" %}
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
{% endtab %}
{% endtabs %}

### Rotate an array by number by D

link : [https://leetcode.com/problems/rotate-array/](https://leetcode.com/problems/rotate-array/)

{% tabs %}
{% tab title="Java" %}
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
{% endtab %}
{% endtabs %}

### Replace Elements with Greatest Element on Right Side

link : [https://leetcode.com/problems/replace-elements-with-greatest-element-on-right-side/](https://leetcode.com/problems/replace-elements-with-greatest-element-on-right-side/)

{% tabs %}
{% tab title="Java" %}
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
{% endtab %}
{% endtabs %}

### Prefix Sum array

* input   : 10, 4, 16, 20
* output : 10 14 30 50

{% tabs %}
{% tab title="Java" %}
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
{% endtab %}
{% endtabs %}

### Find Pivot Index or Equilibrium Point

[https://leetcode.com/problems/find-pivot-index/](https://leetcode.com/problems/find-pivot-index/)

{% tabs %}
{% tab title="Java" %}
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
{% endtab %}
{% endtabs %}

### Maximum occurred integer in N ranges\*

Here `L[i]` and `R[i]` present ranges : 1- 15, 4-8, 9-12 etc...

* mark the starting of the range with 1 and ending with -1 on the next element after the range ends, do this for all ranges
* find the prefix sum array for the array and find the max element, the index will the be most occur ed integer in N ranges

{% tabs %}
{% tab title="Java" %}
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


{% endtab %}
{% endtabs %}

### Strongest Neighbour | Find Peak Element

link :  [https://leetcode.com/problems/find-peak-element/](https://leetcode.com/problems/find-peak-element/)

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

link  : [https://leetcode.com/problems/first-missing-positive/](https://leetcode.com/problems/first-missing-positive/)

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
* Step 3 : Find the sum  : `water += min (  left[i] , right[i] ) - arr[i]`
  * This will give you the water captured in between the bars

link : [https://leetcode.com/problems/trapping-rain-water/](https://leetcode.com/problems/trapping-rain-water/)

{% tabs %}
{% tab title="Java" %}
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
{% endtab %}
{% endtabs %}

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

```java
class Solution {
    public int maximumGap(int[] nums) {
        
        if(nums.length < 2)
            return 0;
        
        if(nums.length == 2)
            return Math.abs(nums[0] - nums[1]);
        
        Arrays.sort(nums);
        
        int maxDiff = Integer.MIN_VALUE;
        
        for(int i = 0; i < nums.length - 1; i++)
            maxDiff = Math.max((nums[i+1] - nums[i]), maxDiff);
        
        return maxDiff;
    }
}

```

