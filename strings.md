---
description: fancy character array
---

# Strings

### Longest Substring Without Repeating Characters

```
Given a string s, find the length of the longest substring without repeating characters
 
Example 1:

Input: s = "abcabcbb"
Output: 3
Explanation: The answer is "abc", with the length of 3.
Example 2:

Input: s = "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.
Example 3:

Input: s = "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3.
Notice that the answer must be a substring, "pwke" is a subsequence and not a substring.
```

```java
public class Solution {

	static public int lengthOfLongestSubstring(String s) {
		int result = 0;
		Set<Character> charSet = new HashSet();
		int windowStart = 0;
		for (int windowEnd = 0; windowEnd < s.length(); windowEnd++) {
	// if the character at right pointer is duplicate, keep removing
	// character at left pointer until the duplicate character is removed.
			while (charSet.contains(s.charAt(windowEnd))) {
				charSet.remove(s.charAt(windowStart));
				windowStart++;
			}
	// add the character at the right pointer to the set
			charSet.add(s.charAt(windowEnd));
	// check if the current substring length is maximum
			result = Math.max(result, windowEnd - windowStart + 1);
		}
		return result;
	}

	public static void main(String[] args) {
		System.out.println(lengthOfLongestSubstring("abcadef"));
	}
}
```

### Reverse String

```
Write a function that reverses a string. 
The input string is given as an array of characters s.

You must do this by modifying the input array in-place with O(1) extra memory.
```

```java
class Solution {
	public void reverseString(char[] s) {
		int low = 0, high = s.length - 1;
		while (low < high) {
			char temp = s[low];
			s[low] = s[high];
			s[high] = temp;
			low++;
			high--;
		}
	}
}
```

### Reverse Words in a String III

```
Given a string s, reverse the order of characters in each word 
within a sentence while still preserving whitespace and initial word order.

Example 1:

Input: s = "Let's take LeetCode contest"
Output: "s'teL ekat edoCteeL tsetnoc"
```

```java
class Solution {
	public String reverseWords(String s) {
		String ans = "";
		String temp = "";
		for (int i = 0; i < s.length(); i++) {
			if (s.charAt(i) == ' ') {
				ans += temp;
				ans += " ";
				temp = "";
			} else {
				temp = s.charAt(i) + temp;
			}
		}

		ans += temp;
		return ans;
	}
}
```

### Valid Anagram&#x20;

```
Given two strings s and t, return true if t is an anagram of s, 
and false otherwise.

An Anagram is a word or phrase formed by rearranging the 
letters of a different word or phrase, typically using all 
the original letters exactly once.

Example 1:

Input: s = "anagram", t = "nagaram"
Output: true
Example 2:

Input: s = "rat", t = "car"
Output: false
```

```java
class Solution {
	public boolean isAnagram(String s, String t) {
		if (s.length() > t.length()) {
			return isAnagram(t, s);
		}

		Map<Character, Integer> hm = new HashMap();

		for (char c : s.toCharArray()) {
			hm.put(c, hm.getOrDefault(c, 0) + 1);
		}

		for (char c : t.toCharArray()) {
			if (!hm.containsKey(c) || hm.get(c) <= 0)
				return false;
			hm.put(c, hm.get(c) - 1);
		}

		return true;
	}
}
```

### Ransom Note

```
Given two strings ransomNote and magazine, 
return true if ransomNote can be constructed from magazine and false otherwise.

Each letter in magazine can only be used once in ransomNote.

Example 1:

Input: ransomNote = "a", magazine = "b"
Output: false
Example 2:

Input: ransomNote = "aa", magazine = "ab"
Output: false
```

```java
class Solution {
    public boolean canConstruct(String ransomNote, String magazine) {
        		if (ransomNote.length() > magazine.length())
			return false;

		int[] alpha = new int[26];

		for (char ele : magazine.toCharArray()) {
			alpha[ele - 97]++;
		}

		for (char ele : ransomNote.toCharArray()) {
			if (alpha[ele - 97]-- <= 0)
				return false;
		}

		return true;
    }
}
```

### First Unique Character in a String&#x20;

```
Given a string s, find the first non-repeating character in it 
and return its index. If it does not exist, return -1.

Example 1:

Input: s = "leetcode"
Output: 0
Example 2:

Input: s = "loveleetcode"
Output: 2
```

```java
public class Solution {

	static public int firstUniqChar(String s) {

		HashMap<Character, Integer> hmap = new HashMap<>();

		for (char ele : s.toCharArray()) {
			hmap.put(ele, hmap.getOrDefault(ele, 0) + 1);
		}

		for(int i=0; i<s.length(); i++) {
			if(hmap.get( s.charAt(i) ) == 1) {
				return i;
			}
		}

		return -1;

	}

	public static void main(String[] args) {
		System.out.println(firstUniqChar("loveleetcode"));
	}
}
```

### Longest Substring Without Repeating Characters

```
Given a string s, find the length of the longest substring without repeating characters
 
Example 1:

Input: s = "abcabcbb"
Output: 3
Explanation: The answer is "abc", with the length of 3.
Example 2:

Input: s = "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.
Example 3:

Input: s = "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3.
Notice that the answer must be a substring, "pwke" is a subsequence and not a substring.
```

```java
public class Solution {

	static public int lengthOfLongestSubstring(String s) {
		int result = 0;
		Set<Character> charSet = new HashSet();
		int windowStart = 0;
		for (int windowEnd = 0; windowEnd < s.length(); windowEnd++) {
	// if the character at right pointer is duplicate, keep removing
	// character at left pointer until the duplicate character is removed.
			while (charSet.contains(s.charAt(windowEnd))) {
				charSet.remove(s.charAt(windowStart));
				windowStart++;
			}
	// add the character at the right pointer to the set
			charSet.add(s.charAt(windowEnd));
	// check if the current substring length is maximum
			result = Math.max(result, windowEnd - windowStart + 1);
		}
		return result;
	}

	public static void main(String[] args) {
		System.out.println(lengthOfLongestSubstring("abcadef"));
	}
}
```

### Print frequencies of characters of string of lower case alphabets

```java

class Solution {
    public static void main(String[] args) {
        String str = "geeksforgeeks";
        int[] count = new int[26];
        for (int i = 0; i < str.length(); i++) {
            count[str.charAt(i) - 'a']++;
        }
        for (int i = 0; i < 26; i++) {
            if (count[i] > 0) {
                System.out.println((char) (i + 'a') + " " + count[i]);
            }
        }
    }
}
```

### Check Palindrome

```java
class Solution {
    public static boolean isPalindrome(String str) {
        int start = str.length();
        int end = str.length() - 1;
        while (start < end) {
            if (str.charAt(start) != str.charAt(end)) {
                return false;
            }
            start++;
            end--;
        }
        return true;
    }

    public static void main(String[] args) {
        String str = "geeksrorgeeks";
        System.out.println(isPalindrome(str));
    }
}
```

### Check string is subsequence of one another

```java
class Solution {
    static boolean isSubSeq(String str1, String str2) {
        if (str1.length() < str2.length()) {
            return false;
        }
        int s2p = 0;
        for (int i = 0; i < str1.length(); i++) {
            if (str1.charAt(i) == str2.charAt(s2p)) {
                s2p++;
            }
        }
        return s2p == str2.length();
    }

    public static void main(String[] args) {
        String str = "geeksforgeeks";
        String str1 = "grges";
        System.out.println(isSubSeq(str, str1));
    }
}
```

### Check if two strings are anagram

```java
class Solution {
    static final int CHAR = 256;

    static boolean areAnagram(String s1, String s2) {
        if (s1.length() != s2.length())
            return false;
        int[] count = new int[CHAR];
        for (int i = 0; i < s1.length(); i++) {
            count[s1.charAt(i)]++;
            count[s2.charAt(i)]--;
        }
        for (int i = 0; i < CHAR; i++) {
            if (count[i] != 0) return false;
        }
        return true;
    }

    public static void main(String[] args) {
        String str1 = "abaac";
        String str2 = "aacba";
        if (areAnagram(str1, str2))
            System.out.println("The two strings are"
                    + " anagram of each other");
        else
            System.out.println("The two strings are not"
                    + " anagram of each other");
    }
}
```

### Leftmost Repeating character

```java
class Solution {
    static final int CHAR = 256;

    static int leftMost(String str) {
        int[] count = new int[CHAR];
        for (int i = 0; i < str.length(); i++) {
            count[str.charAt(i)]++;
        }
        for (int i = 0; i < str.length(); i++) {
            if (count[str.charAt(i)] > 1) return i;
        }
        return -1;
    }

    public static void main(String[] args) {
        String str = "geeksforgeeks";
        System.out.println("Index of leftmost repeating character:");
        System.out.println(leftMost(str));
    }
}
```

### Leftmost non repeating character

```java
class Solution {
    static final int CHAR = 256;

    static int nonRep(String str) {
        int[] count = new int[CHAR];
        for (int i = 0; i < str.length(); i++) {
            count[str.charAt(i)]++;
        }
        for (int i = 0; i < str.length(); i++) {
            if (count[str.charAt(i)] == 1) return i;
        }
        return -1;
    }

    public static void main(String[] args) {
        String str = "geeksforgeeks";
        System.out.println("Index of leftmost non-repeating element:");
        System.out.println(nonRep(str));
    }
}
```

### Reverse words in string

```java
class Solution {
    static void reverse(char str[], int low, int high) {
        while (low <= high) {
            //swap
            char temp = str[low];
            str[low] = str[high];
            str[high] = temp;
            //
            low++;
            high--;
        }
    }

    static void reverseWords(char str[], int n) {
        int start = 0;
        for (int end = 0; end < n; end++) {
            if (str[end] == ' ') {
                reverse(str, start, end - 1);
                start = end + 1;
            }
        }
        reverse(str, start, n - 1);
        reverse(str, 0, n - 1);
    }

    public static void main(String[] args) {
        String s = "Welcome to Program";
        int n = s.length();
        char[] str = s.toCharArray();
        System.out.println("After reversing words in the string:");
        reverseWords(str, n);
        System.out.println(str);
    }
}
```

### Pattern Searching in String for ALL CASES

```java
class Solution {
    static void patSearchinng(String txt, String pat) {
        int m = pat.length();
        int n = txt.length();
        for (int i = 0; i <= (n - m); i++) {
            int j;
            for (j = 0; j < m; j++)
                if (pat.charAt(j) != txt.charAt(i + j))
                    break;
            if (j == m)
                System.out.print(i + " ");
        }
    }

    public static void main(String[] args) {
        String txt = "ABCABCD";
        String pat = "ABCD";
        System.out.print("All index numbers where pattern found: ");
        patSearchinng(txt, pat);
    }
}
```

### Pattern Searching String in DISTINCT

```java
class Solution {
    static void patSearchinng(String txt, String pat) {
        int m = pat.length();
        int n = txt.length();
        for (int i = 0; i <= (n - m); ) {
            int j;
            for (j = 0; j < m; j++)
                if (pat.charAt(j) != txt.charAt(i + j))
                    break;
            if (j == m)
                System.out.print(i + " ");
            if (j == 0) {
                i++;
            } else {
                i = (i + j);
            }
        }
    }

    public static void main(String[] args) {
        String txt = "ABCABCD";
        String pat = "ABCD";
        System.out.print("All index numbers where pattern found: ");
        patSearchinng(txt, pat);
    }
}
```

### Rapin Karp Alogrithm

```java

class Solution {
    static final int d = 256;
    static final int q = 101;

    static void RBSearch(String pat, String txt, int M, int N) {

        //Compute (d^(M-1))%q
        int h = 1;
        for (int i = 1; i <= M - 1; i++)
            h = (h * d) % q;

        //Compute p and to
        int p = 0, t = 0;
        for (int i = 0; i < M; i++) {
            p = (p * d + pat.charAt(i)) % q;
            t = (t * d + txt.charAt(i)) % q;
        }

        for (int i = 0; i <= (N - M); i++) {
            //Check for hit
            if (p == t) {
                boolean flag = true;
                for (int j = 0; j < M; j++)
                    if (txt.charAt(i + j) != pat.charAt(j)) {
                        flag = false;
                        break;
                    }
                if (flag == true) System.out.print(i + " ");
            }
            //Compute ti+1 using ti
            if (i < N - M) {
                t = ((d * (t - txt.charAt(i) * h)) + txt.charAt(i + M)) % q;
                if (t < 0) t = t + q;
            }
        }

    }

    public static void main ( String[] args ) {
        String txt = "GEEKS FOR GEEKS";
        String pat = "GEEK";
        System.out.print("All index numbers where pattern found: ");
        RBSearch(pat, txt, 4, 15);
    }
}
```

### KMP Algorithm (Part 1 : Constructing LPS Array)

```java
class Solution {
    static void fillLPS(String str, int lps[]) {
        int n = str.length(), len = 0;
        lps[0] = 0;
        int i = 1;
        while (i < n) {
            if (str.charAt(i) == str.charAt(len)) {
                len++;
                lps[i] = len;
                i++;
            } else {
                if (len == 0) {
                    lps[i] = 0;
                    i++;
                } else {
                    len = lps[len - 1];
                }
            }
        }
    }

    public static void main(String[] args) {
        String txt = "abacabad";
        int[] lps = new int[txt.length()];
        fillLPS(txt, lps);
        for (int i = 0; i < txt.length(); i++) {
            System.out.print(lps[i] + " ");
        }
    }
}
```

### KMP Agorithm (Part 2 : Complete Algorithm)

```java

class Solution {
    static void fillLPS(String str, int lps[]) {
        int n = str.length(), len = 0;
        lps[0] = 0;
        int i = 1;
        while (i < n) {
            if (str.charAt(i) == str.charAt(len)) {
                len++;
                lps[i] = len;
                i++;
            } else {
                if (len == 0) {
                    lps[i] = 0;
                    i++;
                } else {
                    len = lps[len - 1];
                }
            }
        }
    }

    static void KMP(String pat, String txt) {
        int N = txt.length();
        int M = pat.length();
        int[] lps = new int[M];
        fillLPS(pat, lps);
        int i = 0, j = 0;
        while (i < N) {
            if (pat.charAt(j) == txt.charAt(i)) {
                i++;
                j++;
            }
            if (j == M) {
                System.out.println("Found pattern at index " + (i - j));
                j = lps[j - 1];
            } else if (i < N && pat.charAt(j) != txt.charAt(i)) {
                if (j == 0)
                    i++;
                else
                    j = lps[j - 1];
            }
        }
    }

    public static void main(String[] args) {
        String txt = "ababcababaad", pat = "ababa";
        KMP(pat, txt);
    }
}
```

### Check whether strings is rotated

```java
class Solution {
    static boolean areRotations(String s1, String s2) {
        if (s1.length() != s2.length()) return false;
        return ((s1 + s1).indexOf(s2) >= 0);
    }

    public static void main(String[] args) {
        String s1 = "ABCD";
        String s2 = "CDAB";
        if (areRotations(s1, s2)) {
            System.out.println("Strings are rotations of each other");
        } else {
            System.out.println("Strings are not rotations of each other");
        }
    }
}
```

### Check if Strings are Rotations

```java
class Solution {
    static boolean areRotations(String s1, String s2) {
        if (s1.length() != s2.length()) return false;
        return ((s1 + s1).indexOf(s2) >= 0);
    }

    public static void main(String[] args) {
        String s1 = "ABCD";
        String s2 = "CDAB";
        if (areRotations(s1, s2)) {
            System.out.println("Strings are rotations of each other");
        } else {
            System.out.println("Strings are not rotations of each other");
        }
    }
}
```

### Lexicographic Rank of a String

```java
class Solution {
    static final int CHAR = 256;

    static int fact(int n) {
        return (n <= 1) ? 1 : n * fact(n - 1);
    }

    static int lexRank(String str) {
        int res = 1;
        int n = str.length();
        int mul = fact(n);
        int[] count = new int[CHAR];
        for (int i = 0; i < n; i++)
            count[str.charAt(i)]++;
        for (int i = 1; i < CHAR; i++)
            count[i] += count[i - 1];
        for (int i = 0; i < n - 1; i++) {
            mul = mul / (n - i);
            res = res + count[str.charAt(i) - 1] * mul;
            for (int j = str.charAt(i); j < CHAR; j++)
                count[j]--;
        }
        return res;
    }

    public static void main(String[] args) {
        String str = "STRING";
        System.out.print(lexRank(str));
    }
}
```

### Longest Substring with Distinct Characters

```java
import java.util.*;

class Solution {
    static int longestDistinct(String str) {
        int n = str.length();
        int res = 0;
        int prev[] = new int[256];
        Arrays.fill(prev, -1);
        int i = 0;
        for (int j = 0; j < n; j++) {
            i = Math.max(i, prev[str.charAt(j)] + 1);
            int maxEnd = j - i + 1;
            res = Math.max(res, maxEnd);
            prev[str.charAt(j)] = j;
        }
        return res;
    }

    public static void main(String[] args) {
        String str = "geeksforgeeks";
        int len = longestDistinct(str);
        System.out.print("The length of the longest distinct characters substring is " + len);
    }
}
```
