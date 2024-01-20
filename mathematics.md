# Mathematics

## Basic Maths

**Sum of AP :** sum = n/2 \* (2a+(n-1)d)

**Sum of GP** : a(1-r^n)/1-r

**Mean :** sum of all numbers divided by number of numbers

**Median** :

* For **odd** number of numbers : middle number
* For **even** number of numbers : ( mean of middle numbers ) / 2

**LCM** : LCM(a,b) = |a.b|/gcd(a,b)

### GCD or HCF

```cpp
int gcd(int a, int b)
{
    if (a == 0)
    {
        return b;
    }
    return gcd(b % a, a);
}

int main()
{
    cout << gcd(32, 24) << endl;
}
```

### Number of Digits

#### Number of Digits in a number ( iteratively )

```cpp
int number = 123456;
int len = 0;

while (number > 0)
{
    number = number / 10;
    len++;
}

cout << len << "\n";
```

#### Number of Digits in a number ( recursively )

```cpp
int numOfDigits(int num)
{
    if (num == 0)
    {
        return 0;
    }
    return numOfDigits(num / 10) + 1;
}

int main()
{
    int number = 123456;
    cout << numOfDigits(number);
}
```

#### Number of Digits in a number ( mathematically )

```cpp
int number = 1234561;
cout << (int)(log10(number)+1);
```

### First N Prime

```cpp
int number = 200;

for (int i = 0; i < number; i++)
{
    if (i == 0 || i == 1) {
        continue;
    }

    bool flag = 1;

    for (int j = 2; j < sqrt(i); j++) {
        if (i % j == 0) {
            flag = 0;
        }
    }

    if (flag) {
        cout << "Prime : " << i << "\n";
    }
}

```

### Factorial of a number

```cpp
int fact(int n)
{
    if (n == 0)
    {
        return 1;
    }
    return n * fact(n - 1);
}

int main()
{
    cout << fact(7) << endl;
}
```
