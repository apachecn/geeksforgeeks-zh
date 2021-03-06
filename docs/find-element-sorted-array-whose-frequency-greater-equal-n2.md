# 在排序数组中查找频率大于或等于`n / 2`的元素。

> 原文： [https://www.geeksforgeeks.org/find-element-sorted-array-whose-frequency-greater-equal-n2/](https://www.geeksforgeeks.org/find-element-sorted-array-whose-frequency-greater-equal-n2/)

给定长度为`n`的排序数组，请在数组中查找出现大于或等于`n / 2`次的数字。 假定这样的元素总是存在的。

例子：

```
Input :  2 3 3 4
Output : 3

Input :  3 4 5 5 5 
Output : 5

Input : 1 1 1 2 3
Output : 1

```



为了找到该数字，我们遍历数组，并检查数组中每个元素的频率是否大于或等于`n / 2`，但它需要额外的空间，并且时间复杂度为`O(n)`。

但是我们可以看到，如果在排序数组中存在大于或等于`n / 2`次的数字，则该数字必须出现在位置`n / 2`，即`a[n / 2]`。

## C++ 

```cpp

// C++ code to find majority element in a 
// sorted array 
#include <iostream> 
using namespace std; 

int findMajority(int arr[], int n) 
{ 
    return arr[n / 2]; 
} 

int main() 
{ 
    int arr[] = { 1, 2, 2, 3 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    cout << findMajority(arr, n); 
    return 0; 
} 

```

## Java

```java

// Java code to find majority element in a 
// sorted array 
public class Test { 

    public static int findMajority(int arr[], int n) 
    { 
        return arr[n / 2]; 
    } 
    public static void main(String args[]) 
    { 
        int arr[] = { 1, 2, 2, 3 }; 
        int n = arr.length; 
        System.out.println(findMajority(arr, n)); 
    } 
} 

```

## Python 3

```py

# Python 3 code to find 
# majority element in a 
# sorted array 

def findMajority(arr, n): 

    return arr[int(n / 2)] 

# Driver Code 
arr = [1, 2, 2, 3] 
n = len(arr)  
print(findMajority(arr, n)) 

# This code is contributed by Smitha. 

```

## C# 

```cs

// C# code to find majority element in a 
// sorted array 
using System; 

public class GFG { 

    public static int findMajority(int []arr, int n) 
    { 
        return arr[n / 2]; 
    } 

    // Driver code 
    public static void Main() 
    { 

        int []arr = { 1, 2, 2, 3 }; 
        int n = arr.Length; 

        Console.WriteLine(findMajority(arr, n)); 
    } 
} 

// This code is contributed by vt_m.  

```

## PHP

```php

<?php 
// PHP code to find majority  
// element in a sorted array 

function findMajority($arr, $n) 
{ 
    return $arr[intval($n / 2)]; 
} 

    // Driver Code 
    $arr = array(1, 2, 2, 3); 
    $n = count($arr); 
    echo findMajority($arr, $n);      

// This code is contributed by Sam007 
?> 

```

Output:

```
2

```

时间复杂度：`O(1)`。

**相关文章**：

[未排序数组中的多数元素](https://www.geeksforgeeks.org/majority-element/)

[检查排序数组中的多数元素](https://www.geeksforgeeks.org/check-for-majority-element-in-a-sorted-array/)

