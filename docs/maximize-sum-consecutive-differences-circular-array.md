# 最大化循环数组中的连续差之和

> 原文： [https://www.geeksforgeeks.org/maximize-sum-consecutive-differences-circular-array/](https://www.geeksforgeeks.org/maximize-sum-consecutive-differences-circular-array/)

给定`n`个元素的数组。 将数组视为圆形数组，即`a[1]`为`a[n]`之后的元素。 任务是找到允许重排数组元素的连续元素之间的差的最大和，即在元素查找重排之后`|a[1] - a[2]| + |a[2] - a[3]| + ... + |a[n-1] - a[n]| + |a[n] - a[1]|`。

例子：

```
Input : arr[] = { 4, 2, 1, 8 }
Output : 18
Rearrange given array as : { 1, 8, 2, 4 }
Sum of difference between consecutive element
= |1 - 8| + |8 - 2| + |2 - 4| + |4 - 1|
= 7 + 6 + 2 + 3
= 18.

Input : arr[] = { 10, 12, 15 }
Output : 10

```



这个想法是使用贪婪方法，并尝试将具有更大差异的元素拉近。

考虑给定数组的排序排列`a[1], a[1], a[2], ..., a[n-1], a[n]`使得`a[1] < a[2] < a[3] < ... < a[n-1] < a[n]`。

现在，要获得在连续元素之间具有最大差异之和的答案，请按以下方式排列元素：

`a[1], a[n], a[2], a[n-1], ..., a[n/2], a[n/2+1]`

该安排产生了最佳答案，因为所有`a[1], a[2], ..., a[n/2-1], a[n/2]`减去两次，而`a[n/2+1], ..., a[n]`被添加两次。

注`a[n/2+1]`仅对偶数`n`考虑此项，因为对于奇数`n`，它被加一次并相减一次，因此被抵消。

## C++ 

```cpp

// C++ program to maximize the sum of difference 
// between consecutive elements in circular array 
#include <bits/stdc++.h> 
using namespace std; 

// Return the maximum Sum of difference between 
// consecutive elements. 
int maxSum(int arr[], int n) 
{ 
    int sum = 0; 

    // Sorting the array. 
    sort(arr, arr + n); 

    // Subtracting a1, a2, a3,....., a(n/2)-1, an/2 
    // twice and adding a(n/2)+1, a(n/2)+2, a(n/2)+3,. 
    // ...., an - 1, an twice. 
    for (int i = 0; i < n/2; i++) 
    { 
        sum -= (2 * arr[i]); 
        sum += (2 * arr[n - i - 1]); 
    } 

    return sum; 
} 

// Driver Program 
int main() 
{ 
    int arr[] = { 4, 2, 1, 8 }; 
    int n = sizeof(arr)/sizeof(arr[0]); 
    cout << maxSum(arr, n) << endl; 
    return 0; 
} 

```

## Java

```java
// Java program to maximize the sum of difference 
// between consecutive elements in circular array 
import java.io.*; 
import java.util.Arrays; 
   
class MaxSum 
{ 
    // Return the maximum Sum of difference between 
    // consecutive elements. 
    static int maxSum(int arr[], int n) 
    { 
        int sum = 0; 
   
        // Sorting the array. 
        Arrays.sort(arr); 
       
        // Subtracting a1, a2, a3,....., a(n/2)-1,  
        // an/2 twice and adding a(n/2)+1, a(n/2)+2,  
        // a(n/2)+3,....., an - 1, an twice. 
        for (int i = 0; i < n/2; i++) 
        { 
            sum -= (2 * arr[i]); 
            sum += (2 * arr[n - i - 1]); 
        } 
       
        return sum; 
    } 
  
    // Driver Program 
    public static void main (String[] args) 
    { 
        int arr[] = { 4, 2, 1, 8 }; 
        int n = arr.length; 
        System.out.println(maxSum(arr, n)); 
    } 
} 
/*This code is contributed by Prakriti Gupta*/
```

## Python3

```py
# Python3 program to maximize the sum of difference 
# between consecutive elements in circular array 
  
# Return the maximum Sum of difference  
# between consecutive elements 
def maxSum(arr, n): 
    sum = 0
  
    # Sorting the array 
    arr.sort() 
  
    # Subtracting a1, a2, a3,....., a(n/2)-1, an/2 
    # twice and adding a(n/2)+1, a(n/2)+2, a(n/2)+3,. 
    # ...., an - 1, an twice. 
    for i in range(0, int(n / 2)) : 
        sum -= (2 * arr[i]) 
        sum += (2 * arr[n - i - 1]) 
  
    return sum
  
  
# Driver Program 
arr = [4, 2, 1, 8] 
n = len(arr) 
print (maxSum(arr, n)) 
  
# This code is contributed by Shreyanshi Arun. 
```

## C#

```cs
// C# program to maximize the sum of difference 
// between consecutive elements in circular array 
using System; 
  
class MaxSum { 
      
    // Return the maximum Sum of difference  
    // between consecutive elements. 
    static int maxSum(int[] arr, int n) 
    { 
        int sum = 0; 
  
        // Sorting the array. 
        Array.Sort(arr); 
  
        // Subtracting a1, a2, a3, ....., a(n/2)-1, 
        // an/2 twice and adding a(n/2)+1, a(n/2)+2, 
        // a(n/2)+3, ....., an - 1, an twice. 
        for (int i = 0; i < n / 2; i++) { 
            sum -= (2 * arr[i]); 
            sum += (2 * arr[n - i - 1]); 
        } 
  
        return sum; 
    } 
  
    // Driver Program 
    public static void Main() 
    { 
        int[] arr = { 4, 2, 1, 8 }; 
        int n = arr.Length; 
        Console.WriteLine(maxSum(arr, n)); 
    } 
} 
  
//This Code is contributed by vt_m. 
```

输出：

```
18
```

时间复杂度：`O(nlogn)`。

辅助空间：`O(1)`。