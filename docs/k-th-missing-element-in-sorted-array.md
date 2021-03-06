# 排序数组中的第`k`个缺失元素

> 原文： [https://www.geeksforgeeks.org/k-th-missing-element-in-sorted-array/](https://www.geeksforgeeks.org/k-th-missing-element-in-sorted-array/)

给定一个递增的序列`a[]`，我们需要在递增的序列中找到第`K`个缺失的连续元素，该元素在序列中不存在。 如果没有第`k`个缺失元素，则输出 -1。

**示例**：

```
Input : a[] = {2, 3, 5, 9, 10};   
        k = 1;
Output : 4
Explanation: Missing Element in the increasing 
sequence are {4, 6, 7, 8}. So k-th missing element
is 4

Input : a[] = {2, 3, 5, 9, 10, 11, 12};       
        k = 4;
Output : 8
Explanation: missing element in the increasing 
sequence are {4, 6, 7, 8}  so k-th missing 
element is 8

```



**方法**：开始遍历数组元素，并对每个元素检查下一个元素是否连续，如果不连续，则取这两个元素之间的差，并检查差值是否大于或等于给定的`k`，然后计算`ans = a[i] + count`，否则迭代下一个元素。

## C++ 

```cpp

#include <bits/stdc++.h> 
using namespace std; 

// Function to find k-th  
// missing element 
int missingK(int a[], int k,  
             int n) 
{ 
    int difference = 0,  
        ans = 0, count = k; 
    bool flag = 0; 

    // interating over the array 
    for(int i = 0 ; i < n - 1; i++) 
    {    
        difference = 0; 

        // check if i-th and  
        // (i + 1)-th element  
        // are not consecutive 
        if ((a[i] + 1) != a[i + 1])  
        { 

            // save their difference 
            difference +=  
                (a[i + 1] - a[i]) - 1; 

            // check for difference 
            // and given k 
            if (difference >= count) 
                { 
                    ans = a[i] + count; 
                    flag = 1; 
                    break; 
                } 
            else
                count -= difference; 
        } 
    } 

    // if found 
    if(flag) 
        return ans; 
    else
        return  -1; 
} 

// Driver code 
int main() 
{ 
    // Input array 
    int a[] = {1, 5, 11, 19}; 

    // k-th missing element  
    // to be found in the array 
    int k = 11; 
    int n = sizeof(a) / sizeof(a[0]); 

    // calling function to 
    // find missing element 
    int missing = missingK(a, k, n); 

    cout << missing << endl; 

    return 0; 
} 

```

## Java

```java

// Java program to check for 
// even or odd 
import java.io.*; 
import java.util.*; 

public class GFG { 

    // Function to find k-th  
    // missing element 
    static int missingK(int []a, int k,  
                                 int n) 
    { 
        int difference = 0,  
            ans = 0, count = k; 
        boolean flag = false; 

        // interating over the array 
        for(int i = 0 ; i < n - 1; i++) 
        {  
            difference = 0; 

            // check if i-th and  
            // (i + 1)-th element  
            // are not consecutive 
            if ((a[i] + 1) != a[i + 1])  
            { 

                // save their difference 
                difference +=  
                    (a[i + 1] - a[i]) - 1; 

                // check for difference 
                // and given k 
                if (difference >= count) 
                    { 
                        ans = a[i] + count; 
                        flag = true; 
                        break; 
                    } 
                else
                    count -= difference; 
            } 
        } 

        // if found 
        if(flag) 
            return ans; 
        else
            return -1; 
    } 

    // Driver code 
    public static void main(String args[]) 
    { 

        // Input array 
        int []a = {1, 5, 11, 19}; 

        // k-th missing element  
        // to be found in the array 
        int k = 11; 
        int n = a.length; 

        // calling function to 
        // find missing element 
        int missing = missingK(a, k, n); 

        System.out.print(missing); 
    } 

} 

// This code is contributed by 
// Manish Shaw (manishshaw1) 

```

## Python3

```py

# Function to find k-th  
# missing element 
def missingK(a, k, n) : 

    difference = 0
    ans = 0
    count = k 
    flag = 0

    # interating over the array 
    for i in range (0, n-1) :  
        difference = 0

        # check if i-th and  
        # (i + 1)-th element  
        # are not consecutive 
        if ((a[i] + 1) != a[i + 1]) : 

            # save their difference 
            difference += (a[i + 1] - a[i]) - 1

            # check for difference 
            # and given k 
            if (difference >= count) : 
                    ans = a[i] + count 
                    flag = 1
                    break
            else : 
                count -= difference      

    # if found 
    if(flag) : 
        return ans 
    else : 
        return -1

# Driver code 
# Input array 
a = [1, 5, 11, 19] 

# k-th missing element  
# to be found in the array 
k = 11
n = len(a) 

# calling function to 
# find missing element 
missing = missingK(a, k, n) 

print(missing) 

# This code is contributed by  
# Manish Shaw (manishshaw1) 

```

## C# 

```cs

// C# program to check for 
// even or odd 
using System; 
using System.Collections.Generic; 

class GFG { 

    // Function to find k-th  
    // missing element 
    static int missingK(int []a, int k,  
                                 int n) 
    { 
        int difference = 0,  
            ans = 0, count = k; 
        bool flag = false; 

        // interating over the array 
        for(int i = 0 ; i < n - 1; i++) 
        {  
            difference = 0; 

            // check if i-th and  
            // (i + 1)-th element  
            // are not consecutive 
            if ((a[i] + 1) != a[i + 1])  
            { 

                // save their difference 
                difference +=  
                    (a[i + 1] - a[i]) - 1; 

                // check for difference 
                // and given k 
                if (difference >= count) 
                    { 
                        ans = a[i] + count; 
                        flag = true; 
                        break; 
                    } 
                else
                    count -= difference; 
            } 
        } 

        // if found 
        if(flag) 
            return ans; 
        else
            return -1; 
    } 

    // Driver code 
    public static void Main() 
    { 

        // Input array 
        int []a = {1, 5, 11, 19}; 

        // k-th missing element  
        // to be found in the array 
        int k = 11; 
        int n = a.Length; 

        // calling function to 
        // find missing element 
        int missing = missingK(a, k, n); 

        Console.Write(missing); 
    } 

} 

// This code is contributed by 
// Manish Shaw (manishshaw1) 

```

## PHP

```php

<?php 
// Function to find k-th  
// missing element 
function missingK(&$a, $k, $n) 
{ 
    $difference = 0; 
    $ans = 0; 
    $count = $k; 
    $flag = 0; 

    // interating over the array 
    for($i = 0 ; $i < $n - 1; $i++) 
    {  
        $difference = 0; 

        // check if i-th and  
        // (i + 1)-th element  
        // are not consecutive 
        if (($a[$i] + 1) != $a[$i + 1])  
        { 

            // save their difference 
            $difference += ($a[$i + 1] -  
                            $a[$i]) - 1; 

            // check for difference 
            // and given k 
            if ($difference >= $count) 
                { 
                    $ans = $a[$i] + $count; 
                    $flag = 1; 
                    break; 
                } 
            else
                $count -= $difference; 
        } 
    } 

    // if found 
    if($flag) 
        return $ans; 
    else
        return -1; 
} 

// Driver Code 

// Input array 
$a = array(1, 5, 11, 19); 

// k-th missing element  
// to be found in the array 
$k = 11; 
$n = count($a); 

// calling function to 
// find missing element 
$missing = missingK($a, $k, $n); 

echo $missing; 

// This code is contributed by Manish Shaw 
// (manishshaw1) 
?> 

```

**输出**：

```
14

```

**时间复杂度**：`O(n)`，其中`n`是数组中元素的数量。



* * *

* * *



