# 快速找到数组的多个左旋转 | 系列 1

> 原文： [https://www.geeksforgeeks.org/quickly-find-multiple-left-rotations-of-an-array/](https://www.geeksforgeeks.org/quickly-find-multiple-left-rotations-of-an-array/)

给定大小为`n`的数组和多个值，我们需要围绕该值左旋转数组。 如何快速找到多个左旋？

**示例**：

```
Input : arr[] = {1, 3, 5, 7, 9}
        k1 = 1
        k2 = 3
        k3 = 4
        k4 = 6
Output : 3 5 7 9 1
         7 9 1 3 5
         9 1 3 5 7
         3 5 7 9 1

Input : arr[] = {1, 3, 5, 7, 9}
        k1 = 14 
Output : 9 1 3 5 7

```



**简单方法**：我们已经在下面的文章中讨论了不同的方法。

1.  [数组的左旋转（简单和花式算法）](https://www.geeksforgeeks.org/array-rotation/)。

2.  [数组旋转的块交换算法](https://www.geeksforgeeks.org/block-swap-algorithm-for-array-rotation/)

3.  [数组旋转的逆向算法](https://www.geeksforgeeks.org/program-for-array-rotation-continued-reversal-algorithm/)

上述方法中的最佳方法需要`O(n)`时间和`O(1)`额外空间。

**高效方法**：

当需要单次旋转时，上述方法效果很好。 这些方法还修改了原始数组。 为了处理数组旋转的多个查询，我们使用大小为`2n`的临时数组并快速处理旋转。

步骤 1：将整个数组复制到`temp[0..2n-1]`数组中两次。

步骤 2：在`temp[]`中旋转`k`次后，数组的起始位置将为`k % n`。 我们执行`k`。

步骤 3：从`k % n`到`k % n + n`打印`temp []`数组。

## C++ 

```cpp

// CPP implementation of left rotation of 
// an array K number of times 
#include<bits/stdc++.h> 
using namespace std; 

// Fills temp[] with two copies of arr[] 
void preprocess(int arr[], int n, int temp[]) 
{ 
    // Store arr[] elements at i and i + n 
    for (int i = 0; i<n; i++) 
         temp[i] = temp[i + n] = arr[i]; 
} 

// Function to left rotate an array k times 
void leftRotate(int arr[], int n, int k, int temp[]) 
{ 
    // Starting position of array after k 
    // rotations in temp[] will be k % n 
    int start = k % n; 

    // Print array after k rotations 
    for (int i = start; i < start + n; i++) 
         cout << temp[i] << " "; 

    cout << endl; 
} 

// Driver program 
int main() 
{ 
    int arr[] = {1, 3, 5, 7, 9}; 
    int n = sizeof(arr) / sizeof(arr[0]); 

    int temp[2*n]; 
    preprocess(arr, n, temp); 

    int k = 2; 
    leftRotate(arr, n, k, temp); 

    k = 3; 
    leftRotate(arr, n, k, temp); 

    k = 4; 
    leftRotate(arr, n, k, temp); 

    return 0; 
} 

```

## Java

```java

// Java implementation of left rotation of 
// an array K number of times 
class LeftRotate 
{ 
    // Fills temp[] with two copies of arr[] 
    static void preprocess(int arr[], int n, 
                                   int temp[]) 
    { 
        // Store arr[] elements at i and i + n 
        for (int i = 0; i<n; i++) 
             temp[i] = temp[i + n] = arr[i]; 
    } 

    // Function to left rotate an array k time 
    static void leftRotate(int arr[], int n, int k,  
                                    int temp[]) 
    { 
        // Starting position of array after k 
        // rotations in temp[] will be k % n 
        int start = k % n; 

        // Print array after k rotations 
        for (int i = start; i < start + n; i++) 
            System.out.print(temp[i] + " "); 

        System.out.print("\n"); 
    } 

    // Driver program 
    public static void main (String[] args) 
    { 
        int arr[] = {1, 3, 5, 7, 9}; 
        int n = arr.length; 

        int temp[] = new int[2*n]; 
        preprocess(arr, n, temp); 

        int k = 2; 
        leftRotate(arr, n, k, temp); 

        k = 3; 
        leftRotate(arr, n, k, temp); 

        k = 4; 
        leftRotate(arr, n, k, temp); 
    } 
} 
/*This code is contributed by Prakriti Gupta*/

```

## Python3

```py

# Python3 implementation of left rotation 
# of an array K number of times 

# Fills temp with two copies of arr 
def preprocess(arr, n): 
    temp = [None] * (2 * n) 

    # Store arr elements at i and i + n 
    for i in range(n): 
        temp[i] = temp[i + n] = arr[i] 
    return temp 

# Function to left rotate an array k times 
def leftRotate(arr, n, k, temp): 

    # Starting position of array after k 
    # rotations in temp will be k % n 
    start = k % n 

    # Print array after k rotations 
    for i in range(start, start + n): 
        print(temp[i], end = " ") 
    print("") 

# Driver program 
arr = [1, 3, 5, 7, 9] 
n = len(arr) 
temp = preprocess(arr, n) 

k = 2
leftRotate(arr, n, k, temp) 

k = 3
leftRotate(arr, n, k, temp) 

k = 4
leftRotate(arr, n, k, temp) 

# This code is contributed by Sanghamitra Mishra  

```

## C# 

```cs

// Java implementation of left rotation of 
// an array K number of times 
using System; 
class LeftRotate 
{ 
    // Fills temp[] with two copies of arr[] 
    static void preprocess(int []arr, int n, 
                                int[] temp) 
    { 
        // Store arr[] elements at i and i + n 
        for (int i = 0; i<n; i++) 
            temp[i] = temp[i + n] = arr[i]; 
    } 

    // Function to left rotate an array k time 
    static void leftRotate(int []arr, int n, int k,  
                                    int []temp) 
    { 
        // Starting position of array after k 
        // rotations in temp[] will be k % n 
        int start = k % n; 

        // Print array after k rotations 
        for (int i = start; i < start + n; i++) 
        Console.Write(temp[i] + " "); 
        Console.WriteLine(); 
    } 

    // Driver program 
    public static void Main () 
    { 
        int []arr = {1, 3, 5, 7, 9}; 
        int n = arr.Length; 

        int []temp = new int[2*n]; 
        preprocess(arr, n, temp); 

        int k = 2; 
        leftRotate(arr, n, k, temp); 

        k = 3; 
        leftRotate(arr, n, k, temp); 

        k = 4; 
        leftRotate(arr, n, k, temp); 
    } 
} 
//This code is contributed by vt_m. 

```

## PHP

```php

<?php  
// PHP implementation of  
// left rotation of an  
// array K number of times 

// Fills $temp with 
// two copies of $arr 
function preprocess(&$arr, $n,  
                    &$temp) 
{ 
    // Store $arr elements 
    // at i and i + n 
    for ($i = 0; $i < $n; $i++) 
        $temp[$i] = $temp[$i + $n] = $arr[$i]; 
} 

// Function to left rotate 
// an array k times 
function leftRotate(&$arr, $n, 
                     $k, &$temp) 
{ 
    // Starting position of  
    // array after k rotations 
    // in temp[] will be k % n 
    $start = $k % $n; 

    // Print array after 
    // k rotations 
    for ($i = $start;  
         $i < $start + $n; $i++) 
        echo $temp[$i] . " "; 

    echo "\n"; 
} 

// Driver Code 
$arr = array(1, 3, 5, 7, 9); 
$n = sizeof($arr); 

$temp[2 * $n] = array(); 
preprocess($arr, $n, $temp); 

$k = 2; 
leftRotate($arr, $n, $k, $temp); 

$k = 3; 
leftRotate($arr, $n, $k, $temp); 

$k = 4; 
leftRotate($arr, $n, $k, $temp); 

// This code is contributed 
// by ChitraNayal 
?> 

```

**输出**：

```
5 7 9 1 3 
7 9 1 3 5 
9 1 3 5 7 

```

注意，查找旋转起始地址的任务需要`O(1)`时间。 它正在打印需要`O(n)`时间的元素。

**优化空间的方法**：上述方法需要额外的空间。 下面给出的是空间优化的解决方案。 感谢 **frenzy77** 提出了这种方法。

## C++

```cpp

// CPP implementation of left rotation of 
// an array K number of times 
#include<bits/stdc++.h> 
using namespace std; 

// Function to left rotate an array k times 
void leftRotate(int arr[], int n, int k) 
{ 
    // Print array after k rotations 
    for (int i = k; i < k + n; i++) 
        cout << arr[i%n] << " "; 
} 

// Driver program 
int main() 
{ 
    int arr[] = {1, 3, 5, 7, 9}; 
    int n = sizeof(arr) / sizeof(arr[0]); 

    int k = 2; 
    leftRotate(arr, n, k); 
    cout << endl; 

    k = 3; 
    leftRotate(arr, n, k); 
    cout << endl; 

    k = 4; 
    leftRotate(arr, n, k); 
    cout << endl; 

    return 0; 
} 

```

## Java

```java

// Java implementation of  
// left rotation of an  
// array K number of times 

import java.io.*; 

class GFG 
{ 

// Function to left rotate 
// an array k times 
static void leftRotate(int arr[],  
                       int n, int k) 
{ 
    // Print array after 
    // k rotations 
    for (int i = k; i < k + n; i++) 
        System.out.print(arr[i % n] + " "); 
} 

// Driver Code 
public static void main (String[] args) 
{ 
    int arr[] = {1, 3, 5, 7, 9}; 
    int n = arr.length; 

    int k = 2; 
    leftRotate(arr, n, k); 
    System.out.println(); 

    k = 3; 
    leftRotate(arr, n, k); 
    System.out.println(); 

    k = 4; 
    leftRotate(arr, n, k); 
    System.out.println();  
} 
} 

// This code is contributed by ajit 

```

## Python 3

```py

# Python3 implementation of  
# left rotation of an array  
# K number of times  

# Function to left rotate 
# an array k times 
def leftRotate(arr, n, k): 

    # Print array  
    # after k rotations 
    for i in range(k, k + n): 
        print(str(arr[i % n]),  
                   end = " ") 

# Driver Code 
arr = [1, 3, 5, 7, 9] 
n = len(arr) 
k = 2; 
leftRotate(arr, n, k) 
print() 

k = 3; 
leftRotate(arr, n, k) 
print() 

k = 4
leftRotate(arr, n, k) 
print() 

# This code is contributed  
# by ChitraNayal 

```

## C#

```cs

// C# implementation of  
// left rotation of an  
// array K number of times 
using System; 

class GFG 
{ 

// Function to left rotate 
// an array k times 
static void leftRotate(int []arr,  
                       int n, int k) 
{ 
    // Print array after 
    // k rotations 
    for (int i = k; i < k + n; i++) 
        Console.Write(arr[i % n] + " "); 
} 

// Driver Code 
static public void Main () 
{ 
int []arr = {1, 3, 5, 7, 9}; 
int n = arr.Length; 

int k = 2; 
leftRotate(arr, n, k); 
Console.WriteLine(); 

k = 3; 
leftRotate(arr, n, k); 
Console.WriteLine(); 

k = 4; 
leftRotate(arr, n, k); 
Console.WriteLine();  
} 
} 

// This code is contributed  
// by akt_mit 

```

## PHP

```php

<?php 

// PHP implementation of left rotation of 
// an array K number of times 

// Function to left rotate an array k times 
function leftRotate($arr, $n, $k) 
{ 

    // Print array after k rotations 
    for ($i = $k; $i < $k + $n; $i++) 
        echo $arr[$i % $n] ," "; 
} 

// Driver program 
$arr = array (1, 3, 5, 7, 9); 
$n = sizeof($arr); 

$k = 2; 
leftRotate($arr, $n, $k); 
echo "\n"; 

$k = 3; 
leftRotate($arr, $n, $k); 
echo "\n"; 

$k = 4; 
leftRotate($arr, $n, $k); 
echo "\n"; 

// This code is contributed by aj_36 
?> 

```

**输出**：

```
5 7 9 1 3 
7 9 1 3 5 
9 1 3 5 7 

```



