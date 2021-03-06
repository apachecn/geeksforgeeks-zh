# 查找给定总和的子数组 | 系列 1（负数）

> 原文： [https://www.geeksforgeeks.org/find-subarray-with-given-sum/](https://www.geeksforgeeks.org/find-subarray-with-given-sum/)

给定一个非排序的非负整数数组，找到一个连续的子数组，该数组加到给定的数字上。

**示例**：

```
Input: arr[] = {1, 4, 20, 3, 10, 5}, sum = 33
Ouptut: Sum found between indexes 2 and 4
Sum of elements between indices
2 and 4 is 20 + 3 + 10 = 33

Input: arr[] = {1, 4, 0, 0, 3, 10, 5}, sum = 7
Ouptut: Sum found between indexes 1 and 4
Sum of elements between indices
1 and 4 is 4 + 0 + 0 + 3 = 7

Input: arr[] = {1, 4}, sum = 0
Output: No subarray found
There is no subarray with 0 sum

```

可能有多个子数组，且`sum`为给定的`sum`。 以下解决方案将首先打印此类子数组。



**简单方法**： 一个简单的解决方案是一个一个地考虑所有子数组并检查每个子数组的总和。 以下程序实现简单的解决方案。 运行两个循环：外部循环选择起点`i`，内部循环尝试从`i`开始的所有子数组。

**算法**：

1.  从头到尾遍历数组。

2.  从每个索引开始，从`i`到数组末尾的另一个循环将使所有子数组从`i`开始，并保持一个变量总和以计算总和。

3.  对于内循环更新中的每个索引`sum = sum + array[j]`。

4.  如果总和等于给定总和，则打印子数组。

## C++ 

```cpp

/* A simple program to print subarray  
with sum as given sum */
#include <bits/stdc++.h> 
using namespace std; 

/* Returns true if the there is a subarray  
of arr[] with sum equal to 'sum' otherwise  
returns false. Also, prints the result */
int subArraySum(int arr[], int n, int sum) 
{ 
    int curr_sum, i, j; 

    // Pick a starting point 
    for (i = 0; i < n; i++) { 
        curr_sum = arr[i]; 

        // try all subarrays starting with 'i' 
        for (j = i + 1; j <= n; j++) { 
            if (curr_sum == sum) { 
                cout << "Sum found between indexes "
                     << i << " and " << j - 1; 
                return 1; 
            } 
            if (curr_sum > sum || j == n) 
                break; 
            curr_sum = curr_sum + arr[j]; 
        } 
    } 

    cout << "No subarray found"; 
    return 0; 
} 

// Driver Code 
int main() 
{ 
    int arr[] = { 15, 2, 4, 8, 9, 5, 10, 23 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    int sum = 23; 
    subArraySum(arr, n, sum); 
    return 0; 
} 

// This code is contributed 
// by rathbhupendra 

```

## C

```c

/* A simple program to print  
subarray with sum as given sum */
#include <stdio.h> 

/* Returns true if the there is a subarray  
of arr[] with a sum equal to 'sum' 
   otherwise returns false.  Also, prints  
the result */
int subArraySum(int arr[], int n, int sum) 
{ 
    int curr_sum, i, j; 

    // Pick a starting point 
    for (i = 0; i < n; i++) { 
        curr_sum = arr[i]; 

        // try all subarrays starting with 'i' 
        for (j = i + 1; j <= n; j++) { 
            if (curr_sum == sum) { 
                printf( 
                    "Sum found between indexes %d and %d", 
                    i, j - 1); 
                return 1; 
            } 
            if (curr_sum > sum || j == n) 
                break; 
            curr_sum = curr_sum + arr[j]; 
        } 
    } 

    printf("No subarray found"); 
    return 0; 
} 

// Driver program to test above function 
int main() 
{ 
    int arr[] = { 15, 2, 4, 8, 9, 5, 10, 23 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    int sum = 23; 
    subArraySum(arr, n, sum); 
    return 0; 
} 

```

## Java

```java

class SubarraySum { 
    /* Returns true if the there is a  
subarray of arr[] with a sum equal to 
       'sum' otherwise returns false.   
Also, prints the result */
    int subArraySum(int arr[], int n, int sum) 
    { 
        int curr_sum, i, j; 

        // Pick a starting point 
        for (i = 0; i < n; i++) { 
            curr_sum = arr[i]; 

            // try all subarrays starting with 'i' 
            for (j = i + 1; j <= n; j++) { 
                if (curr_sum == sum) { 
                    int p = j - 1; 
                    System.out.println( 
                        "Sum found between indexes " + i 
                        + " and " + p); 
                    return 1; 
                } 
                if (curr_sum > sum || j == n) 
                    break; 
                curr_sum = curr_sum + arr[j]; 
            } 
        } 

        System.out.println("No subarray found"); 
        return 0; 
    } 

    public static void main(String[] args) 
    { 
        SubarraySum arraysum = new SubarraySum(); 
        int arr[] = { 15, 2, 4, 8, 9, 5, 10, 23 }; 
        int n = arr.length; 
        int sum = 23; 
        arraysum.subArraySum(arr, n, sum); 
    } 
} 

// This code has been contributed by Mayank Jaiswal(mayank_24) 

```

## Python3

```py

# Returns true if the 
# there is a subarray 
# of arr[] with sum 
# equal to 'sum'  
# otherwise returns 
# false. Also, prints 
# the result  
def subArraySum(arr, n, sum): 

    # Pick a starting  
    # point 
    for i in range(n): 
        curr_sum = arr[i] 

        # try all subarrays 
        # starting with 'i' 
        j = i + 1
        while j <= n: 

            if curr_sum == sum: 
                print ("Sum found between") 
                print("indexes % d and % d"%( i, j-1)) 

                return 1

            if curr_sum > sum or j == n: 
                break

            curr_sum = curr_sum + arr[j] 
            j += 1

    print ("No subarray found") 
    return 0

# Driver program  
arr = [15, 2, 4, 8, 9, 5, 10, 23] 
n = len(arr) 
sum = 23

subArraySum(arr, n, sum) 

# This code is Contributed by shreyanshi_arun. 

```

## C# 

```cs

// C# code to Find subarray 
// with given sum 
using System; 

class GFG { 
    // Returns true if the there is a 
    // subarray of arr[] with sum 
    // equal to 'sum' otherwise returns 
    // false. Also, prints the result 
    int subArraySum(int[] arr, int n, 
                    int sum) 
    { 
        int curr_sum, i, j; 

        // Pick a starting point 
        for (i = 0; i < n; i++) { 
            curr_sum = arr[i]; 

            // try all subarrays 
            // starting with 'i' 
            for (j = i + 1; j <= n; j++) { 
                if (curr_sum == sum) { 
                    int p = j - 1; 
                    Console.Write("Sum found between "
                                  + "indexes " + i + " and " + p); 
                    return 1; 
                } 
                if (curr_sum > sum || j == n) 
                    break; 
                curr_sum = curr_sum + arr[j]; 
            } 
        } 

        Console.Write("No subarray found"); 
        return 0; 
    } 

    // Driver Code 
    public static void Main() 
    { 
        GFG arraysum = new GFG(); 
        int[] arr = { 15, 2, 4, 8, 9, 5, 10, 23 }; 
        int n = arr.Length; 
        int sum = 23; 
        arraysum.subArraySum(arr, n, sum); 
    } 
} 

// This code has been contributed 
// by nitin mittal 

```

## PHP

```php

<?php 
// A simple program to print subarray 
// with sum as given sum  

/* Returns true if the there is 
   a subarray of arr[] with  
   sum equal to 'sum' 
   otherwise returns false.  
   Also, prints the result */
function subArraySum($arr, $n, $sum) 
{ 
    $curr_sum; $i; $j; 

    // Pick a starting point 
    for ($i = 0; $i < $n; $i++) 
    { 
        $curr_sum = $arr[$i]; 

        // try all subarrays  
        // starting with 'i' 
        for ($j = $i + 1; $j <= $n; $j++) 
        { 
            if ($curr_sum == $sum) 
            { 
                echo "Sum found between indexes ", $i, " and ", $j-1 ; 
                return 1; 
            } 
            if ($curr_sum > $sum || $j == $n) 
                break; 
        $curr_sum = $curr_sum + $arr[$j]; 
        } 
    } 

    echo "No subarray found"; 
    return 0; 
} 

    // Driver Code 
    $arr= array(15, 2, 4, 8, 9, 5, 10, 23); 
    $n = sizeof($arr); 
    $sum = 23; 
    subArraySum($arr, $n, $sum); 
    return 0; 

// This code is contributed by AJit 
?> 

```

**输出**：

```
Sum found between indexes 1 and 4

```

**复杂度分析**：

*   **时间复杂度**：最坏情况下`O(n ^ 2)`。

    嵌套循环用于遍历数组，因此时间复杂度为`O(n ^ 2)`。

*   **空间复杂度**：`O(1)`。

    由于需要恒定的额外空间。

**有效方法**： 有一个想法，即数组的所有元素都是正数。 如果子数组的总和大于给定的总和，则不可能将元素添加到当前子数组中，总和为`x`（给定总和）。 想法是对滑动窗口使用类似的方法。 从一个空的子数组开始，向该子数组添加元素，直到总和小于`x`为止。 如果总和大于`x`，则从当前子数组的开头删除元素。

**算法**：

1.  创建三个变量`l = 0, sum = 0`。

2.  从头到尾遍历数组。

3.  通过添加当前元素来更新变量`sum`，`sum = sum + array[i]`。

4.  如果总和大于给定总和，则将变量总和更新为`sum = sum – array[l]`，并将`l`更新为`l++`。

5.  如果总和等于给定总和，则打印子数组并中断循环。

## C++

```cpp

/* An efficient program to print  
subarray with sum as given sum */
#include <iostream> 
using namespace std; 

/* Returns true if the there is a subarray of  
arr[] with a sum equal to 'sum' otherwise  
returns false. Also, prints the result */
int subArraySum(int arr[], int n, int sum) 
{ 
    /* Initialize curr_sum as value of  
    first element and starting point as 0 */
    int curr_sum = arr[0], start = 0, i; 

    /* Add elements one by one to curr_sum and  
    if the curr_sum exceeds the sum, 
    then remove starting element */
    for (i = 1; i <= n; i++) { 
        // If curr_sum exceeds the sum, 
        // then remove the starting elements 
        while (curr_sum > sum && start < i - 1) { 
            curr_sum = curr_sum - arr[start]; 
            start++; 
        } 

        // If curr_sum becomes equal to sum, 
        // then return true 
        if (curr_sum == sum) { 
            cout << "Sum found between indexes "
                 << start << " and " << i - 1; 
            return 1; 
        } 

        // Add this element to curr_sum 
        if (i < n) 
            curr_sum = curr_sum + arr[i]; 
    } 

    // If we reach here, then no subarray 
    cout << "No subarray found"; 
    return 0; 
} 

// Driver Code 
int main() 
{ 
    int arr[] = { 15, 2, 4, 8, 9, 5, 10, 23 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    int sum = 23; 
    subArraySum(arr, n, sum); 
    return 0; 
} 

// This code is contributed by SHUBHAMSINGH10 

```

## C

```c

/* An efficient program to print  
subarray with sum as given sum */
#include <stdio.h> 

/* Returns true if the there is a  
subarray of arr[] with a sum  
equal to 'sum' otherwise returns  
false.  Also, prints the result */
int subArraySum(int arr[], int n, int sum) 
{ 
    /* Initialize curr_sum as  
       value of first element and  
starting point as 0 */
    int curr_sum = arr[0], start = 0, i; 

    /* Add elements one by one to  
curr_sum and if the curr_sum  
       exceeds the sum, then remove  
starting element */
    for (i = 1; i <= n; i++) { 
        // If curr_sum exceeds the sum, 
        // then remove the starting elements 
        while (curr_sum > sum && start < i - 1) { 
            curr_sum = curr_sum - arr[start]; 
            start++; 
        } 

        // If curr_sum becomes equal to sum, 
        // then return true 
        if (curr_sum == sum) { 
            printf( 
                "Sum found between indexes %d and %d", 
                start, i - 1); 
            return 1; 
        } 

        // Add this element to curr_sum 
        if (i < n) 
            curr_sum = curr_sum + arr[i]; 
    } 

    // If we reach here, then no subarray 
    printf("No subarray found"); 
    return 0; 
} 

// Driver program to test above function 
int main() 
{ 
    int arr[] = { 15, 2, 4, 8, 9, 5, 10, 23 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    int sum = 23; 
    subArraySum(arr, n, sum); 
    return 0; 
} 

```

## Java

```java

class SubarraySum { 
    /* Returns true if the there is  
a subarray of arr[] with sum equal to 
       'sum' otherwise returns false.   
Also, prints the result */
    int subArraySum(int arr[], int n, int sum) 
    { 
        int curr_sum = arr[0], start = 0, i; 

        // Pick a starting point 
        for (i = 1; i <= n; i++) { 
            // If curr_sum exceeds the sum, 
            // then remove the starting elements 
            while (curr_sum > sum && start < i - 1) { 
                curr_sum = curr_sum - arr[start]; 
                start++; 
            } 

            // If curr_sum becomes equal to sum, 
            // then return true 
            if (curr_sum == sum) { 
                int p = i - 1; 
                System.out.println( 
                    "Sum found between indexes " + start 
                    + " and " + p); 
                return 1; 
            } 

            // Add this element to curr_sum 
            if (i < n) 
                curr_sum = curr_sum + arr[i]; 
        } 

        System.out.println("No subarray found"); 
        return 0; 
    } 

    public static void main(String[] args) 
    { 
        SubarraySum arraysum = new SubarraySum(); 
        int arr[] = { 15, 2, 4, 8, 9, 5, 10, 23 }; 
        int n = arr.length; 
        int sum = 23; 
        arraysum.subArraySum(arr, n, sum); 
    } 
} 

// This code has been contributed by Mayank Jaiswal(mayank_24) 

```

## Python3

```py

# An efficient program  
# to print subarray 
# with sum as given sum  

# Returns true if the  
# there is a subarray  
# of arr[] with sum 
# equal to 'sum'  
# otherwise returns  
# false. Also, prints  
# the result. 
def subArraySum(arr, n, sum): 

    # Initialize curr_sum as 
    # value of first element 
    # and starting point as 0  
    curr_sum = arr[0] 
    start = 0

    # Add elements one by  
    # one to curr_sum and  
    # if the curr_sum exceeds  
    # the sum, then remove  
    # starting element  
    i = 1
    while i <= n: 

        # If curr_sum exceeds 
        # the sum, then remove 
        # the starting elements 
        while curr_sum > sum and start < i-1: 

            curr_sum = curr_sum - arr[start] 
            start += 1

        # If curr_sum becomes 
        # equal to sum, then 
        # return true 
        if curr_sum == sum: 
            print ("Sum found between indexes") 
            print ("% d and % d"%(start, i-1)) 
            return 1

        # Add this element  
        # to curr_sum 
        if i < n: 
            curr_sum = curr_sum + arr[i] 
        i += 1

    # If we reach here,  
    # then no subarray 
    print ("No subarray found") 
    return 0

# Driver program 
arr = [15, 2, 4, 8, 9, 5, 10, 23] 
n = len(arr) 
sum = 23

subArraySum(arr, n, sum) 

# This code is Contributed by shreyanshi_arun. 

```

## C#

```cs

// An efficient C# program to print 
// subarray with sum as given sum 
using System; 

class GFG { 

    // Returns true if the 
    // there is a subarray of 
    // arr[] with sum equal to 
    // 'sum' otherwise returns false. 
    // Also, prints the result 
    int subArraySum(int[] arr, int n, 
                    int sum) 
    { 
        int curr_sum = arr[0], 
            start = 0, i; 

        // Pick a starting point 
        for (i = 1; i <= n; i++) { 
            // If curr_sum exceeds 
            // the sum, then remove 
            // the starting elements 
            while (curr_sum > sum && start < i - 1) { 
                curr_sum = curr_sum - arr[start]; 
                start++; 
            } 

            // If curr_sum becomes equal to 
            // sum, then return true 
            if (curr_sum == sum) { 
                int p = i - 1; 
                Console.WriteLine("Sum found between "
                                  + "indexes " + start + " and " + p); 
                return 1; 
            } 

            // Add this element to curr_sum 
            if (i < n) 
                curr_sum = curr_sum + arr[i]; 
        } 
        Console.WriteLine("No subarray found"); 
        return 0; 
    } 

    // Driver code 
    public static void Main() 
    { 
        GFG arraysum = new GFG(); 
        int[] arr = new int[] { 15, 2, 4, 8, 
                                9, 5, 10, 23 }; 
        int n = arr.Length; 
        int sum = 23; 
        arraysum.subArraySum(arr, n, sum); 
    } 
} 

// This code has been contributed by KRV. 

```

## PHP

```php

<?php 
/* An efficient program to print  
subarray with sum as given sum */

/* Returns true if the there is a  
subarray of arr[] with sum equal  
to 'sum' otherwise returns false.  
Also, prints the result */
function subArraySum($arr, $n, $sum) 
{ 
    /* Initialize curr_sum as  
    value of first element 
    and starting point as 0 */
    $curr_sum = $arr[0];  
    $start = 0; $i; 

    /* Add elements one by one to  
    curr_sum and if the curr_sum  
    exceeds the sum, then remove 
    starting element */
    for ($i = 1; $i <= $n; $i++) 
    { 
        // If curr_sum exceeds the sum,  
        // then remove the starting elements 
        while ($curr_sum > $sum and 
               $start < $i - 1) 
        { 
            $curr_sum = $curr_sum -  
                        $arr[$start]; 
            $start++; 
        } 

        // If curr_sum becomes equal  
        // to sum, then return true 
        if ($curr_sum == $sum) 
        { 
            echo "Sum found between indexes", 
                             " ", $start, " ",  
                           "and ", " ", $i - 1; 
            return 1; 
        } 

        // Add this element 
        // to curr_sum 
        if ($i < $n) 
        $curr_sum = $curr_sum + $arr[$i]; 
    } 

    // If we reach here, 
    // then no subarray 
    echo "No subarray found"; 
    return 0; 
} 

// Driver Code 
$arr = array(15, 2, 4, 8,  
              9, 5, 10, 23); 
$n = count($arr); 
$sum = 23; 
subArraySum($arr, $n, $sum); 

// This code has been 
// contributed by anuj_67\. 
?> 

```

**输出**：

```
Sum found between indexes 1 and 4

```

**复杂度分析**：

*   **时间复杂度**：`O(n)`。

    仅需要遍历数组一次。 因此，时间复杂度为`O(n)`。

*   **空间复杂度**：`O(1)`。

    由于需要恒定的额外空间。

上述解决方案无法处理负数。 我们可以使用哈希处理负数。 请参阅下面的系列 2。

*   [查找具有给定总和的子数组 | 系列 2（处理负数）](https://www.geeksforgeeks.org/find-subarray-with-given-sum-in-array-of-integers/)

*   [查找具有给定总和且在恒定空间中允许带有负数的子数组](https://www.geeksforgeeks.org/find-subarray-with-given-sum-with-negatives-allowed-in-constant-space/)

