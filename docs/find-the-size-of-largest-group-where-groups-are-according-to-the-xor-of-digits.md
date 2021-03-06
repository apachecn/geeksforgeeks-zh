# 根据数字的异或找到最大组的大小

> 原文：[https://www.geeksforgeeks.org/find-the-size-of-largest-group-where-groups-are-according-to-the-xor-of-digits/](https://www.geeksforgeeks.org/find-the-size-of-largest-group-where-groups-are-according-to-the-xor-of-digits/)

给定整数`N`，任务是在 1 到`N`的范围内找到最大组的大小，其中，如果两个数字的各位异或相等，则两个数字属于同一组。 

**示例**：

> **输入**：`N = 13`
>
> **输出**：2
>
> **说明**：
>
> 共有 10 个组，它们根据其数字的 xor 分组为 1 到 13：`[11] [1, 10] [2, 13] [3, 12] [4] [5] [6] [7] [8] [9]`。
>
> 其中，有 3 个小组的个数最多，为 2。
>
> 
>
> **输入**：`N = 2`
>
> **输出**：1
>
> **说明**：
>
> 共有 2 个组，它们根据其数字的 xor 分组为 1 到 2：`[1] [2]`。
>
> 其中，两组的最大个数均为 1。

**方法**：

要解决上述问题，我们必须使用**哈希映射**存储每个元素从 1 到`N`的数字的异或，并重复它的频率。 然后在哈希映射中找到最大频率，该最大频率将是组的最大大小。 最后，计数与最大组具有相同频率计数的所有组，然后返回计数。

下面是上述方法的实现：

## C++ 14

```

// c++ implementation to Find the
// size of largest group, where groups
// are according to the xor of its digits.
#include <bits/stdc++.h>
using namespace std;

// Function to find out xor of digit
int digit_xor(int x)
{
    int xorr = 0;

    // calculate xor digitwise
    while (x) {
        xorr ^= x % 10;
        x = x / 10;
    }

    // return xor
    return xorr;
}

// Function to find the
// size of largest group
int find_count(int n)
{
    // hash map for counting frquency
    map<int, int> mpp;

    for (int i = 1; i <= n; i++) {

        // counting freq of each element
        mpp[digit_xor(i)] += 1;
    }

    int maxm = 0;
    for (auto x : mpp) {
        // find the maximum
        if (x.second > maxm)

            maxm = x.second;
    }

    return maxm;
}

// Driver code
int main()
{
    // initialise N
    int N = 13;

    cout << find_count(N);

    return 0;
}

```

## Java

```java

// Java implementation to Find the
// size of largest group, where groups
// are according to the xor of its digits.
import java.util.*;
class GFG{

// Function to find out xor of digit
static int digit_xor(int x)
{
    int xorr = 0;

    // calculate xor digitwise
    while (x > 0) 
    {
        xorr ^= x % 10;
        x = x / 10;
    }

    // return xor
    return xorr;
}

// Function to find the
// size of largest group
static int find_count(int n)
{
    // hash map for counting frquency
    HashMap<Integer,
            Integer> mpp = new HashMap<Integer,
                                       Integer>();

    for (int i = 1; i <= n; i++) 
    {
        // counting freq of each element
        if(mpp.containsKey(digit_xor(i)))
            mpp.put(digit_xor(i), 
                    mpp.get(digit_xor(i)) + 1);
        else
            mpp.put(digit_xor(i), 1);
    }

    int maxm = 0;
    for (Map.Entry<Integer,
                   Integer> x : mpp.entrySet())
    {
        // find the maximum
        if (x.getValue() > maxm)

            maxm = x.getValue();
    }
    return maxm;
}

// Driver code
public static void main(String[] args)
{
    // initialise N
    int N = 13;

    System.out.print(find_count(N));
}
}

// This code is contributed by shikhasingrajput

```

## Python3

```py

# Python3 implementation to find the
# size of largest group, where groups
# are according to the xor of its digits.

# Function to find out xor of digit
def digit_xor(x):

    xorr = 0

    # Calculate xor digitwise
    while (x != 0):
        xorr ^= x % 10
        x = x // 10

    # Return xor
    return xorr

# Function to find the
# size of largest group
def find_count(n):

    # Hash map for counting frquency
    mpp = {}

    for i in range(1, n + 1):

        # Counting freq of each element
        if digit_xor(i) in mpp:
            mpp[digit_xor(i)] += 1
        else:
            mpp[digit_xor(i)] = 1

    maxm = 0

    for x in mpp:

        # Find the maximum
        if (mpp[x] > maxm):
            maxm = mpp[x]

    return maxm

# Driver code

# Initialise N
N = 13

print(find_count(N))

# This code is contributed by divyeshrabadiya07

```

## C#

```cs

// C# implementation to Find the
// size of largest group, where groups
// are according to the xor of its digits.
using System;
using System.Collections.Generic;
class GFG{

// Function to find out xor of digit
static int digit_xor(int x)
{
    int xorr = 0;

    // calculate xor digitwise
    while (x > 0) 
    {
        xorr ^= x % 10;
        x = x / 10;
    }

    // return xor
    return xorr;
}

// Function to find the
// size of largest group
static int find_count(int n)
{
    // hash map for counting frquency
    Dictionary<int,
               int> mpp = new Dictionary<int,
                                         int>();

    for (int i = 1; i <= n; i++) 
    {
        // counting freq of each element
        if(mpp.ContainsKey(digit_xor(i)))
            mpp[digit_xor(i)] = 
                mpp[digit_xor(i)] + 1;
        else
            mpp.Add(digit_xor(i), 1);
    }

    int maxm = 0;
    foreach (KeyValuePair<int,
                          int> x in mpp)
    {
        // find the maximum
        if (x.Value > maxm)

            maxm = x.Value;
    }
    return maxm;
}

// Driver code
public static void Main(String[] args)
{
    // initialise N
    int N = 13;

    Console.Write(find_count(N));
}
}

 // This code is contributed by shikhasingrajput

```

**输出**： 

```
2

```



* * *

* * *



