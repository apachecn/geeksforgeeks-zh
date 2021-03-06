# 将第一个元素加倍，然后将零移动到结尾

> 原文： [https://www.geeksforgeeks.org/double-first-element-move-zero-end/](https://www.geeksforgeeks.org/double-first-element-move-zero-end/)

给定大小为`n`的整数数组。 假设`0`为无效数字，所有其他均为有效数字。 转换数组的方式是，如果下一个数字是有效数字并且与当前数字相同，则将其值加倍，然后用 0 替换下一个数字。修改后，重新排列数组，使所有 0 都移到末尾。

例子：

```
Input : arr[] = {2, 2, 0, 4, 0, 8}
Output : 4 4 8 0 0 0

Input : arr[] = {0, 2, 2, 2, 0, 6, 6, 0, 0, 8}
Output :  4 2 12 8 0 0 0 0 0 0

```

**来源**：[Microsoft IDC 面试经历 | 系列 150](https://www.geeksforgeeks.org/microsoft-idc-interview-experience-set-150-full-time/)



**方法**：首先修改提及的数组，即，如果下一个有效数字与当前数字相同，则将其值加倍，然后将下一个数字替换为 0。

**修改算法**：

```
1\. if n == 1
2\.     return
3\. for i = 0 to n-2
4\.     if (arr[i] != 0) && (arr[i] == arr[i+1])
5\.         arr[i] = 2 * arr[i]
6\.       arr[i+1] = 0
7\.       i++

```

修改数组后，[将所有零移动到数组的末尾](https://www.geeksforgeeks.org/move-zeroes-end-array/)。

## C++ 

```cpp

// C++ implementation to rearrange the array  
// elements after modification 
#include <bits/stdc++.h> 

using namespace std; 

// function which pushes all zeros to end of  
// an array. 
void pushZerosToEnd(int arr[], int n) 
{ 
    // Count of non-zero elements 
    int count = 0; 

    // Traverse the array. If element encountered 
    // is non-zero, then replace the element at  
    // index 'count' with this element 
    for (int i = 0; i < n; i++) 
        if (arr[i] != 0) 

            // here count is incremented 
            arr[count++] = arr[i]; 

    // Now all non-zero elements have been shifted 
    // to front and 'count' is set as index of 
    // first 0\. Make all elements 0 from count 
    // to end. 
    while (count < n) 
        arr[count++] = 0; 
} 

// function to rearrange the array elements 
// after modification 
void modifyAndRearrangeArr(int arr[], int n) 
{ 
    // if 'arr[]' contains a single element 
    // only 
    if (n == 1) 
        return; 

    // traverse the array 
    for (int i = 0; i < n - 1; i++) { 

        // if true, perform the required modification 
        if ((arr[i] != 0) && (arr[i] == arr[i + 1])) { 

            // double current index value 
            arr[i] = 2 * arr[i]; 

            // put 0 in the next index 
            arr[i + 1] = 0; 

            // increment by 1 so as to move two  
            // indexes ahead during loop iteration 
            i++; 
        } 
    } 

    // push all the zeros at the end of 'arr[]' 
    pushZerosToEnd(arr, n); 
} 

// function to print the array elements 
void printArray(int arr[], int n) 
{ 
    for (int i = 0; i < n; i++) 
        cout << arr[i] << " "; 
} 

// Driver program to test above 
int main() 
{ 
    int arr[] = { 0, 2, 2, 2, 0, 6, 6, 0, 0, 8 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 

    cout << "Original array: "; 
    printArray(arr, n); 

    modifyAndRearrangeArr(arr, n); 

    cout << "\nModified array: "; 
    printArray(arr, n); 

    return 0; 
} 

```

## Java

```java

// Java implementation to rearrange the  
// array elements after modification 
class GFG { 

    // function which pushes all  
    // zeros to end of an array. 
    static void pushZerosToEnd(int arr[], int n) 
    { 
        // Count of non-zero elements 
        int count = 0; 

        // Traverse the array. If element  
        // encountered is non-zero, then 
        // replace the element at index 
        // 'count' with this element 
        for (int i = 0; i < n; i++) 
            if (arr[i] != 0) 

                // here count is incremented 
                arr[count++] = arr[i]; 

        // Now all non-zero elements  
        // have been shifted to front and  
        // 'count' is set as index of first 0.  
        // Make all elements 0 from count to end. 
        while (count < n) 
            arr[count++] = 0; 
    } 

    // function to rearrange the array 
    //  elements after modification 
    static void modifyAndRearrangeArr(int arr[], int n) 
    { 
        // if 'arr[]' contains a single element 
        // only 
        if (n == 1) 
            return; 

        // traverse the array 
        for (int i = 0; i < n - 1; i++) { 

            // if true, perform the required modification 
            if ((arr[i] != 0) && (arr[i] == arr[i + 1])) 
            { 

                // double current index value 
                arr[i] = 2 * arr[i]; 

                // put 0 in the next index 
                arr[i + 1] = 0; 

                // increment by 1 so as to move two 
                // indexes ahead during loop iteration 
                i++; 
            } 
        } 

        // push all the zeros at  
        // the end of 'arr[]' 
        pushZerosToEnd(arr, n); 
    } 

    // function to print the array elements 
    static void printArray(int arr[], int n) 
    { 
        for (int i = 0; i < n; i++) 
            System.out.print(arr[i] + " "); 
        System.out.println(); 
    } 

    // Driver program to test above 
    public static void main(String[] args) 
    { 
        int arr[] = { 0, 2, 2, 2, 0, 6, 6, 0, 0, 8 }; 
        int n = arr.length; 

        System.out.print("Original array: "); 
        printArray(arr, n); 

        modifyAndRearrangeArr(arr, n); 

        System.out.print("Modified array: "); 
        printArray(arr, n); 
    } 
} 

// This code is contributed   
// by prerna saini 

```

## Python3

```py

# Python3 implementation to rearrange  
# the array elements after modification 

# function which pushes all zeros  
# to end of an array. 
def pushZerosToEnd(arr, n): 

    # Count of non-zero elements 
    count = 0

    # Traverse the array. If element  
    # encountered is non-zero, then  
    # replace the element at index  
    # 'count' with this element 
    for i in range(0, n): 
        if arr[i] != 0: 

            # here count is incremented 
            arr[count] = arr[i] 
            count+=1

    # Now all non-zero elements have been  
    # shifted to front and 'count' is set 
    # as index of first 0\. Make all  
    # elements 0 from count to end. 
    while (count < n): 
        arr[count] = 0
        count+=1

# function to rearrange the array 
# elements after modification 
def modifyAndRearrangeArr(ar, n): 

    # if 'arr[]' contains a single 
    # element only 
    if n == 1: 
        return

    # traverse the array 
    for i in range(0, n - 1): 

        # if true, perform the required modification 
        if (arr[i] != 0) and (arr[i] == arr[i + 1]): 

            # double current index value 
            arr[i] = 2 * arr[i] 

            # put 0 in the next index 
            arr[i + 1] = 0

            # increment by 1 so as to move two  
            # indexes ahead during loop iteration 
            i+=1

    # push all the zeros at the end of 'arr[]' 
    pushZerosToEnd(arr, n) 

# function to print the array elements 
def printArray(arr, n): 

    for i in range(0, n): 
        print(arr[i],end=" ") 

# Driver program to test above 
arr = [ 0, 2, 2, 2, 0, 6, 6, 0, 0, 8 ] 
n = len(arr)  

print("Original array:",end=" ") 
printArray(arr, n) 

modifyAndRearrangeArr(arr, n) 

print("\nModified array:",end=" ") 
printArray(arr, n) 

# This code is contributed by Smitha Dinesh Semwal 

```

## C# 

```cs

// C# implementation to rearrange the 
// array elements after modification 
using System; 

class GFG { 

    // function which pushes all 
    // zeros to end of an array. 
    static void pushZerosToEnd(int[] arr, int n) 
    { 
        // Count of non-zero elements 
        int count = 0; 

        // Traverse the array. If element 
        // encountered is non-zero, then 
        // replace the element at index 
        // 'count' with this element 
        for (int i = 0; i < n; i++) 
            if (arr[i] != 0) 

                // here count is incremented 
                arr[count++] = arr[i]; 

        // Now all non-zero elements 
        // have been shifted to front and 
        // 'count' is set as index of first 0\. 
        // Make all elements 0 from count to end. 
        while (count < n) 
            arr[count++] = 0; 
    } 

    // function to rearrange the array 
    // elements after modification 
    static void modifyAndRearrangeArr(int[] arr, int n) 
    { 
        // if 'arr[]' contains a single element 
        // only 
        if (n == 1) 
            return; 

        // traverse the array 
        for (int i = 0; i < n - 1; i++) { 

            // if true, perform the required modification 
            if ((arr[i] != 0) && (arr[i] == arr[i + 1])) { 

                // double current index value 
                arr[i] = 2 * arr[i]; 

                // put 0 in the next index 
                arr[i + 1] = 0; 

                // increment by 1 so as to move two 
                // indexes ahead during loop iteration 
                i++; 
            } 
        } 

        // push all the zeros at 
        // the end of 'arr[]' 
        pushZerosToEnd(arr, n); 
    } 

    // function to print the array elements 
    static void printArray(int[] arr, int n) 
    { 
        for (int i = 0; i < n; i++) 
            Console.Write(arr[i] + " "); 
        Console.WriteLine(); 
    } 

    // Driver program to test above 
    public static void Main() 
    { 
        int[] arr = { 0, 2, 2, 2, 0, 6, 6, 0, 0, 8 }; 
        int n = arr.Length; 

        Console.Write("Original array: "); 
        printArray(arr, n); 

        modifyAndRearrangeArr(arr, n); 

        Console.Write("Modified array: "); 
        printArray(arr, n); 
    } 
} 

// This code is contributed by Sam007 

```

Output:

```
Original array: 0 2 2 2 0 6 6 0 0 8
Modified array: 4 2 12 8 0 0 0 0 0 0

```

时间复杂度：`O(n)`。



* * *

* * *



