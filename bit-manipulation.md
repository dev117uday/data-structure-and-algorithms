---
description: on/off
---

# Bit Manipulation

* 12 : 1100 - 5 : 0101 = 0111
  * inverse bits of 5 : 1010 and add 1 : 1011
  * 1100+1011 = 0111 = 7
* & : AND
* \| : OR
* ^ : XOR
* \~ : inverse
* \>> : right shift | a>>1; divide by 2
* << : left shift | a<<1; multiple by 2

### Divide and Multiply

```cpp
int a = 6;
int ans1 = a << 1;
int ans2 = a >> 1;
cout << ans1 << " " << ans2 << endl;
```

### Check if the kth bit is set or not

```cpp
int num = 7; // 0111
int k = 3;

// bring ! in 0!11 to 011! and check for 1

int ans = num >> (k - 1);
if (ans & 1 == 1)
{
    cout << "yes" << endl;
}
```

### Check If The Number is Odd or Even

```cpp
// if last bit if 1, then odd, else even
int num = 5; // 101, 
if (num & 1 == 1)
    cout << "odd\n";
else
    cout << "even\n";
```

### To swap two numbers

```cpp
// it is what it is
int a = 5;
int b = 7;
a = a ^ b;
b = a ^ b;
a = a ^ b;
cout << b << " " << a << "\n";
```

### Check if a number is a power of 2

```java
// 8 = 1000
// 7 = 0111
// & = 0000
int x = 8;
if ((x & (x - 1)) == 0)
    cout << "Yes\n";
else
    cout << "No\n";
```

### Count set bits

<pre class="language-java"><code class="lang-java">int num = 31;
int count = 0;
while (num > 0)
<strong>{
</strong>    if (num &#x26; 1 == 1) // like %2 for odd
    {
        ++count;
    }
    num = num>>1; // like divide by 2
}
cout &#x3C;&#x3C; "Count : " &#x3C;&#x3C; count &#x3C;&#x3C; endl;
</code></pre>
