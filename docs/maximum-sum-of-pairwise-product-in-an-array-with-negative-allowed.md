# 允许负数的数组中的偶对乘积的最大和

> 原文： [https://www.geeksforgeeks.org/maximum-sum-of-pairwise-product-in-an-array-with-negative-allowed/](https://www.geeksforgeeks.org/maximum-sum-of-pairwise-product-in-an-array-with-negative-allowed/)

给定`n`个元素的数组。 查找成对乘法的最大和。 总和可以更大，所以取`10 ^ 9 + 7`为模。 如果存在奇数个元素，则可以将任意一个元素（不成对）相加。

**示例**：

```
Input : arr[] = {-1, 4, 5, -7, -4, 9, 0}
Output : 77
So to get the maximum sum, the arrangement will 
be {-7, -4}, {-1, 0}, {9, 5} and {4}.
So the answer is (-7*(-4))+((-1)*0)+(9*5)+(4) ={77}.

Input : arr[] = {8, 7, 9}
Output : 79
Answer is (9*8) +(7) = 79.

```



1-对给定的数组进行排序。

2-首先，将负数从头开始成对相乘，然后将其加到`total_sum`中。

3-第二，将正数从最后一个乘以`total_sum`。

4-检查负数和正数两个计数是否均为奇数，然后加上最后一对的乘积，即最后一个负数和正数左。

5-或如果一个计数中的任何一个为奇数，则在左侧添加该元素。

6-返回和。

## C++ 

```cpp

// C++ program for above implementation 
#include <bits/stdc++.h> 
#define Mod 1000000007 
using namespace std; 

// Function to find the maximum sum 
long long int findSum(int arr[], int n) 
{ 
    long long int sum = 0; 

    // Sort the array first 
    sort(arr, arr + n); 

    // First multiply negative numbers pairwise 
    // and sum up from starting as to get maximum  
    // sum.  
    int i = 0; 
    while (i < n && arr[i] < 0) { 
        if (i != n - 1 && arr[i + 1] <= 0) { 
            sum = (sum + (arr[i] * arr[i + 1]) % Mod) % Mod; 
            i += 2; 
        } 
        else
            break; 
    } 

    // Second multiply positive numbers pairwise 
    // and summed up from the last as to get maximum  
    // sum. 
    int j = n - 1; 
    while (j >= 0 && arr[j] > 0) { 
        if (j != 0 && arr[j - 1] > 0) { 
            sum = (sum + (arr[j] * arr[j - 1]) % Mod) % Mod; 
            j -= 2; 
        } 
        else
            break; 
    } 

    // To handle case if positive and negative 
    // numbers both are odd in counts. 
    if (j > i) 
        sum = (sum + (arr[i] * arr[j]) % Mod) % Mod; 

    // If one of them occurs odd times 
    else if (i == j) 
        sum = (sum + arr[i]) % Mod; 

    return sum; 
} 

// Drivers code 
int main() 
{ 
    int arr[] = { -1, 9, 4, 5, -4, 7 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    cout << findSum(arr, n); 
    return 0; 
} 

```

## Java

```java
// Java program for above implementation 
import java.io.*; 
import java.util.*; 
  
class GFG { 
  
static int Mod = 1000000007; 
  
// Function to find the maximum sum 
static long findSum(int arr[], int n) { 
    long sum = 0; 
  
    // Sort the array first 
    Arrays.sort(arr); 
  
    // First multiply negative numbers  
    // pairwise and sum up from starting  
    // as to get maximum sum. 
    int i = 0; 
    while (i < n && arr[i] < 0) { 
    if (i != n - 1 && arr[i + 1] <= 0) { 
        sum = (sum + (arr[i] * arr[i + 1]) % Mod) % Mod; 
        i += 2; 
    }  
    else
        break; 
    } 
  
    // Second multiply positive numbers  
    // pairwise and summed up from the  
    // last as to get maximum sum. 
    int j = n - 1; 
    while (j >= 0 && arr[j] > 0) { 
    if (j != 0 && arr[j - 1] > 0) { 
        sum = (sum + (arr[j] * arr[j - 1]) % Mod) % Mod; 
        j -= 2; 
    } else
        break; 
    } 
  
    // To handle case if positive and negative 
    // numbers both are odd in counts. 
    if (j > i) 
    sum = (sum + (arr[i] * arr[j]) % Mod) % Mod; 
  
    // If one of them occurs odd times 
    else if (i == j) 
    sum = (sum + arr[i]) % Mod; 
  
    return sum; 
} 
  
// Drivers code 
public static void main(String args[]) { 
    int arr[] = {-1, 9, 4, 5, -4, 7}; 
    int n = arr.length; 
    System.out.println(findSum(arr, n)); 
} 
} 
  
/*This code is contributed by Nikita Tiwari.*/
```

## Python3

```py
# Python3 code for above implementation 
Mod= 1000000007
  
# Function to find the maximum sum 
def findSum(arr, n): 
    sum = 0
      
    # Sort the array first 
    arr.sort() 
      
    # First multiply negative numbers  
    # pairwise and sum up from starting 
    # as to get maximum sum. 
    i = 0
    while i < n and arr[i] < 0: 
        if i != n - 1 and arr[i + 1] <= 0: 
            sum = (sum + (arr[i] * arr[i + 1])  
                                 % Mod) % Mod 
            i += 2
        else: 
            break
          
    # Second multiply positive numbers 
    # pairwise and summed up from the  
    # last as to get maximum sum. 
    j = n - 1
    while j >= 0 and arr[j] > 0: 
        if j != 0 and arr[j - 1] > 0: 
            sum = (sum + (arr[j] * arr[j - 1]) 
                                 % Mod) % Mod 
            j -= 2
        else: 
            break
          
    # To handle case if positive  
    # and negative numbers both 
    # are odd in counts. 
    if j > i: 
        sum = (sum + (arr[i] * arr[j]) % Mod)  
                                       % Mod 
          
    # If one of them occurs odd times 
    elif i == j: 
        sum = (sum + arr[i]) % Mod 
      
    return sum
  
# Driver code 
arr = [ -1, 9, 4, 5, -4, 7 ] 
n = len(arr)  
print(findSum(arr, n)) 
  
# This code is contributed by "Sharad_Bhardwaj".
```

## C#

```cs
// C# program for above implementation 
using System; 
  
class GFG { 
  
    static int Mod = 1000000007; 
  
    // Function to find the maximum sum 
    static long findSum(int[] arr, int n) 
    { 
        long sum = 0; 
  
        // Sort the array first 
        Array.Sort(arr); 
  
        // First multiply negative numbers 
        // pairwise and sum up from starting 
        // as to get maximum sum. 
        int i = 0; 
        while (i < n && arr[i] < 0) { 
            if (i != n - 1 && arr[i + 1] <= 0) { 
                sum = (sum + (arr[i] * arr[i + 1]) % Mod) % Mod; 
                i += 2; 
            } 
            else
                break; 
        } 
  
        // Second multiply positive numbers 
        // pairwise and summed up from the 
        // last as to get maximum sum. 
        int j = n - 1; 
        while (j >= 0 && arr[j] > 0) { 
            if (j != 0 && arr[j - 1] > 0) { 
                sum = (sum + (arr[j] * arr[j - 1]) % Mod) % Mod; 
                j -= 2; 
            } 
            else
                break; 
        } 
  
        // To handle case if positive and negative 
        // numbers both are odd in counts. 
        if (j > i) 
            sum = (sum + (arr[i] * arr[j]) % Mod) % Mod; 
  
        // If one of them occurs odd times 
        else if (i == j) 
            sum = (sum + arr[i]) % Mod; 
  
        return sum; 
    } 
  
    // Drivers code 
    public static void Main() 
    { 
        int[] arr = { -1, 9, 4, 5, -4, 7 }; 
        int n = arr.Length; 
        Console.WriteLine(findSum(arr, n)); 
    } 
} 
  
/*This code is contributed by vt_m.*/
```

## PHP

```php
<?php 
// PHP program for above implementation 
  
$Mod = 1000000007; 
  
// Function to find the maximum sum 
function findSum(&$arr, $n) 
{ 
    global $Mod; 
    $sum = 0; 
  
    // Sort the array first 
    sort($arr); 
  
    // First multiply negative numbers  
    // pairwise and sum up from starting  
    // as to get maximum sum.  
    $i = 0; 
    while ($i < $n && $arr[$i] < 0)  
    { 
        if ($i != $n - 1 && $arr[$i + 1] <= 0)  
        { 
            $sum = ($sum + ($arr[$i] * 
                    $arr[$i + 1]) % $Mod) % $Mod; 
            $i += 2; 
        } 
        else
            break; 
    } 
  
    // Second multiply positive numbers pairwise 
    // and summed up from the last as to get  
    // maximum sum. 
    $j = $n - 1; 
    while ($j >= 0 && $arr[$j] > 0) 
    { 
        if ($j != 0 && $arr[$j - 1] > 0) 
        { 
            $sum = ($sum + ($arr[$j] *  
                    $arr[$j - 1]) % $Mod) % $Mod; 
            $j -= 2; 
        } 
        else
            break; 
    } 
  
    // To handle case if positive and negative 
    // numbers both are odd in counts. 
    if ($j > $i) 
        $sum = ($sum + ($arr[$i] *  
                $arr[$j]) % $Mod) % $Mod; 
  
    // If one of them occurs odd times 
    else if ($i == $j) 
        $sum = ($sum + $arr[$i]) % Mod; 
  
    return $sum; 
} 
  
// Driver code 
$arr = array (-1, 9, 4, 5, -4, 7 ); 
$n = sizeof($arr); 
echo findSum($arr, $n); 
  
// This code is contributed by ita_c 
?>
```

输出：

```
87
```

