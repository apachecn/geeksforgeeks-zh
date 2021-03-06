# 在数组中查找第二大元素

> 原文： [https://www.geeksforgeeks.org/find-second-largest-element-array/](https://www.geeksforgeeks.org/find-second-largest-element-array/)

给定一个整数数组，我们的任务是编写一个程序，该程序可以有效地找到数组中存在的第二大元素。

 **示例**：

```
Input: arr[] = {12, 35, 1, 10, 34, 1}
Output: The second largest element is 34.
Explanation: The largest element of the 
array is 35 and the second 
largest element is 34

Input: arr[] = {10, 5, 10}
Output: The second largest element is 5.
Explanation: The largest element of 
the array is 10 and the second 
largest element is 5

Input: arr[] = {10, 10, 10}
Output: The second largest does not exist.
Explanation: Largest element of the array 
is 10 there is no second largest element

```



**简单解决方案**：

**方法**：的想法是按降序对数组进行排序，然后从排序数组中返回不等于最大元素的第二个元素。

```

// C program to find second largest 
// element in an array 

#include <bits/stdc++.h> 
using namespace std; 

/* Function to print the second largest elements */
void print2largest(int arr[], int arr_size) 
{ 
    int i, first, second; 

    /* There should be atleast two elements */
    if (arr_size < 2) { 
        printf(" Invalid Input "); 
        return; 
    } 

    // sort the array 
    sort(arr, arr + arr_size); 

    // start from second last element 
    // as the largest element is at last 
    for (i = arr_size - 2; i >= 0; i--) { 
        // if the element is not 
        // equal to largest element 
        if (arr[i] != arr[arr_size - 1]) { 
            printf("The second largest element is %d\n", arr[i]); 
            return; 
        } 
    } 

    printf("There is no second largest element\n"); 
} 

/* Driver program to test above function */
int main() 
{ 
    int arr[] = { 12, 35, 1, 10, 34, 1 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    print2largest(arr, n); 
    return 0; 
} 

```

**输出**：

```
The second largest element is 34

```

**复杂度分析**：

*   **时间复杂度**：`O(N log N)`。

    排序数组所需的时间为`O(N log N)`。

*   **辅助空间**：`O(1)`。

    由于不需要额外的空间。

**更好的解决方案**：

**方法**：方法是遍历数组两次。 在第一个遍历中找到最大元素。 在第二遍历中找到比在第一遍历中获得的元素小的最大元素。

```

// C program to find second largest 
// element in an array 

#include <bits/stdc++.h> 
using namespace std; 

/* Function to print the second largest elements */
void print2largest(int arr[], int arr_size) 
{ 
    int i, first, second; 

    /* There should be atleast two elements */
    if (arr_size < 2) { 
        printf(" Invalid Input "); 
        return; 
    } 

    int largest = second = INT_MIN; 

    // find the largest element 
    for (int i = 0; i < arr_size; i++) { 
        largest = max(largest, arr[i]); 
    } 

    // find the second largest element 
    for (int i = 0; i < arr_size; i++) { 
        if (arr[i] != largest) 
            second = max(second, arr[i]); 
    } 
    if (second == INT_MIN) 
        printf("There is no second largest element\n"); 
    else
        printf("The second largest element is %d\n", second); 
} 

/* Driver program to test above function */
int main() 
{ 
    int arr[] = { 12, 35, 1, 10, 34, 1 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    print2largest(arr, n); 
    return 0; 
} 

```

**输出**：

```
The second largest element is 34

```

**复杂度分析**：

*   **时间复杂度**：`O(n)`。

    需要两次遍历数组。

*   **辅助空间**：`O(1)`。

    由于不需要额外的空间。

**有效解决方案**：在单个遍历中查找第二大元素。

以下是完成此操作的完整算法：

```
1) Initialize two variables first and second to INT_MIN as
   first = second = INT_MIN
2) Start traversing the array,
   a) If the current element in array say arr[i] is greater
      than first. Then update first and second as,
      second = first
      first = arr[i]
   b) If the current element is in between first and second,
      then update second to store the value of current variable as
      second = arr[i]
3) Return the value stored in second.

```

## C++ 

```cpp

// C++ program to find second largest 
// element in an array 
#include <bits/stdc++.h> 
using namespace std; 

// Function to print the second  
// largest elements 
void print2largest(int arr[], int arr_size) 
{ 
    int i, first, second; 

    // There should be atleast two elements 
    if (arr_size < 2) 
    { 
        cout << " Invalid Input "; 
        return; 
    } 

    first = second = INT_MIN; 
    for(i = 0; i < arr_size; i++) 
    { 

       // If current element is greater  
       // than first then update both  
       // first and second  
       if (arr[i] > first) 
       { 
           second = first; 
           first = arr[i]; 
       } 

       // If arr[i] is in between first  
       // and second then update second  
       else if (arr[i] > second && 
                arr[i] != first) 
       { 
           second = arr[i]; 
       } 
    } 
    if (second == INT_MIN) 
        cout << "There is no second largest"
                "element\n"; 
    else
        cout << "The second largest element is "
             << second; 
} 

// Driver code 
int main() 
{ 
    int arr[] = { 12, 35, 1, 10, 34, 1 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 

    print2largest(arr, n); 
    return 0; 
} 

// This code is contributed by shivanisinghss2110 

```

## C

```c

// C program to find second largest 
// element in an array 

#include <limits.h> 
#include <stdio.h> 

/* Function to print the second largest elements */
void print2largest(int arr[], int arr_size) 
{ 
    int i, first, second; 

    /* There should be atleast two elements */
    if (arr_size < 2) { 
        printf(" Invalid Input "); 
        return; 
    } 

    first = second = INT_MIN; 
    for (i = 0; i < arr_size; i++) { 
        /* If current element is greater than first 
           then update both first and second */
        if (arr[i] > first) { 
            second = first; 
            first = arr[i]; 
        } 

        /* If arr[i] is in between first and  
           second then update second  */
        else if (arr[i] > second && arr[i] != first) 
            second = arr[i]; 
    } 
    if (second == INT_MIN) 
        printf("There is no second largest element\n"); 
    else
        printf("The second largest element is %dn", second); 
} 

/* Driver program to test above function */
int main() 
{ 
    int arr[] = { 12, 35, 1, 10, 34, 1 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    print2largest(arr, n); 
    return 0; 
} 

```

## Java

```java

// JAVA Code for Find Second largest 
// element in an array 
class GFG { 

    /* Function to print the second largest 
    elements */
    public static void print2largest(int arr[], 
                                     int arr_size) 
    { 
        int i, first, second; 

        /* There should be atleast two elements */
        if (arr_size < 2) { 
            System.out.print(" Invalid Input "); 
            return; 
        } 

        first = second = Integer.MIN_VALUE; 
        for (i = 0; i < arr_size; i++) { 
            /* If current element is smaller than  
            first then update both first and second */
            if (arr[i] > first) { 
                second = first; 
                first = arr[i]; 
            } 

            /* If arr[i] is in between first and  
               second then update second  */
            else if (arr[i] > second && arr[i] != first) 
                second = arr[i]; 
        } 

        if (second == Integer.MIN_VALUE) 
            System.out.print("There is no second largest"
                             + " element\n"); 
        else
            System.out.print("The second largest element"
                             + " is " + second); 
    } 

    /* Driver program to test above function */
    public static void main(String[] args) 
    { 
        int arr[] = { 12, 35, 1, 10, 34, 1 }; 
        int n = arr.length; 
        print2largest(arr, n); 
    } 
} 
// This code is contributed by Arnav Kr. Mandal. 

```

## Python3

```py

# Python program to 
# find second largest  
# element in an array 

# Function to print the 
# second largest elements  
def print2largest(arr, arr_size): 

    # There should be atleast 
        # two elements  
    if (arr_size < 2): 

        print(" Invalid Input ") 
        return

    first = second = -2147483648
    for i in range(arr_size): 

        # If current element is 
                # smaller than first 
        # then update both 
                # first and second  
        if (arr[i] > first): 

            second = first 
            first = arr[i] 

        # If arr[i] is in 
                # between first and  
        # second then update second  
        elif (arr[i] > second and arr[i] != first): 
            second = arr[i] 

    if (second == -2147483648): 
        print("There is no second largest element") 
    else: 
        print("The second largest element is", second) 

# Driver program to test 
# above function  
arr = [12, 35, 1, 10, 34, 1] 
n = len(arr) 

print2largest(arr, n) 

# This code is contributed 
# by Anant Agarwal. 

```

## C# 

```cs

// C# Code for Find Second largest 
// element in an array 
using System; 

class GFG { 

    // Function to print the 
    // second largest elements 
    public static void print2largest(int[] arr, 
                                     int arr_size) 
    { 
        int i, first, second; 

        // There should be atleast two elements 
        if (arr_size < 2) { 
            Console.WriteLine(" Invalid Input "); 
            return; 
        } 

        first = second = int.MinValue; 
        for (i = 0; i < arr_size; i++) { 
            // If current element is smaller than 
            // first then update both first and second 
            if (arr[i] > first) { 
                second = first; 
                first = arr[i]; 
            } 

            // If arr[i] is in between first 
            // and second then update second 
            else if (arr[i] > second && arr[i] != first) 
                second = arr[i]; 
        } 

        if (second == int.MinValue) 
            Console.Write("There is no second largest"
                          + " element\n"); 
        else
            Console.Write("The second largest element"
                          + " is " + second); 
    } 

    // Driver Code 
    public static void Main(String[] args) 
    { 
        int[] arr = { 12, 35, 1, 10, 34, 1 }; 
        int n = arr.Length; 
        print2largest(arr, n); 
    } 
} 

// This code is contributed by Parashar. 

```

## PHP

```php

<?php 
// PHP program to find second largest  
// element in an array 

// Function to print the  
// second largest elements 
function print2largest($arr, $arr_size) 
{ 

    // There should be atleast  
    // two elements  
    if ($arr_size < 2) 
    { 
        echo(" Invalid Input "); 
        return; 
    } 

    $first = $second = PHP_INT_MIN; 
    for ($i = 0; $i < $arr_size ; $i++) 
    { 

        // If current element is 
        // smaller than first 
        // then update both  
        // first and second  
        if ($arr[$i] > $first) 
        { 
            $second = $first; 
            $first = $arr[$i]; 
        } 

        // If arr[i] is in  
        // between first and  
        // second then update  
        // second  
        else if ($arr[$i] > $second && 
                 $arr[$i] != $first) 
            $second = $arr[$i]; 
    } 
    if ($second == PHP_INT_MIN) 
        echo("There is no second largest element\n"); 
    else
        echo("The second largest element is " . $second . "\n"); 
} 

// Driver Code 
$arr = array(12, 35, 1, 10, 34, 1); 
$n = sizeof($arr); 
print2largest($arr, $n); 

// This code is contributed by Ajit. 
?> 

```

**输出**：

```
The second largest element is 34

```

**复杂度分析**：

*   **时间复杂度**：`O(n)`。

    仅需要遍历数组一次。

*   **辅助空间**：`O(1)`。

    由于不需要额外的空间。

**相关文章**：

[数组](https://www.geeksforgeeks.org/to-find-smallest-and-second-smallest-element-in-an-array/)中最小和第二小的元素。

