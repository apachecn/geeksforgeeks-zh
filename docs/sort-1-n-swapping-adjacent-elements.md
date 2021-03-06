# 通过交换相邻元素从 1 到`N`排序

> 原文： [https://www.geeksforgeeks.org/sort-1-n-swapping-adjacent-elements/](https://www.geeksforgeeks.org/sort-1-n-swapping-adjacent-elements/)

给定一个数组`A`，其大小为`N`，由元素 1 到`N`组成。由`N-1`个元素组成的布尔数组`B`表示，如果`B[i]`为 1，则可以将`A[i]`与`A[i + 1]`交换 。

找出是否可以通过交换元素对`A`进行排序。

**示例**：

```
Input : A[] = {1, 2, 5, 3, 4, 6}
        B[] = {0, 1, 1, 1, 0}
Output : A can be sorted
We can swap A[2] with A[3] and then A[3] with A[4].

Input : A[] = {2, 3, 1, 4, 5, 6}
        B[] = {0, 1, 1, 1, 1}
Output : A can not be sorted
We can not sort A by swapping elements as 1 can never be swapped with A[0]=2.

```



在这里，我们只能将`A[i]`与`A[i + 1]`交换。 因此要查找数组是否可以排序。 使用布尔数组`B`，我们可以对`B`的连续序列 1 进行数组排序。最后，我们可以检查`A`是否排序。

## C++ 

```cpp

// CPP program to test whether array 
// can be sorted by swapping adjacent 
// elements using boolean array 
#include <bits/stdc++.h> 
using namespace std; 

// Return true if array can be 
// sorted otherwise false 
bool sortedAfterSwap(int A[], bool B[], int n) 
{ 
    int i, j; 

    // Check bool array B and sorts 
    // elements for continuous sequence of 1 
    for (i = 0; i < n - 1; i++) { 
        if (B[i]) { 
            j = i; 
            while (B[j]) 
                j++; 

            // Sort array A from i to j 
            sort(A + i, A + 1 + j); 
            i = j; 
        } 
    } 

    // Check if array is sorted or not 
    for (i = 0; i < n; i++) { 
        if (A[i] != i + 1) 
            return false; 
    } 

    return true; 
} 

// Driver program to test sortedAfterSwap() 
int main() 
{ 
    int A[] = { 1, 2, 5, 3, 4, 6 }; 
    bool B[] = { 0, 1, 1, 1, 0 }; 
    int n = sizeof(A) / sizeof(A[0]); 

    if (sortedAfterSwap(A, B, n)) 
        cout << "A can be sorted\n"; 
    else
        cout << "A can not be sorted\n"; 

    return 0; 
} 

```

## Java

```java

import java.util.Arrays; 

// Java program to test whether an array 
// can be sorted by swapping adjacent 
// elements using boolean array 

class GFG { 

    // Return true if array can be 
    // sorted otherwise false 
    static boolean sortedAfterSwap(int A[], 
                                   boolean B[], int n) 
    { 
        int i, j; 

        // Check bool array B and sorts 
        // elements for continuous sequence of 1 
        for (i = 0; i < n - 1; i++) { 
            if (B[i]) { 
                j = i; 
                while (B[j]) { 
                    j++; 
                } 
                // Sort array A from i to j 
                Arrays.sort(A, i, 1 + j); 
                i = j; 
            } 
        } 

        // Check if array is sorted or not 
        for (i = 0; i < n; i++) { 
            if (A[i] != i + 1) { 
                return false; 
            } 
        } 

        return true; 
    } 

    // Driver program to test sortedAfterSwap() 
    public static void main(String[] args) 
    { 
        int A[] = { 1, 2, 5, 3, 4, 6 }; 
        boolean B[] = { false, true, true, true, false }; 
        int n = A.length; 

        if (sortedAfterSwap(A, B, n)) { 
            System.out.println("A can be sorted"); 
        } 
        else { 
            System.out.println("A can not be sorted"); 
        } 
    } 
} 

```

## Python3

```py

# Python 3 program to test whether an array 
# can be sorted by swapping adjacent 
# elements using a boolean array 

# Return true if array can be 
# sorted otherwise false 
def sortedAfterSwap(A, B, n) : 

    # Check bool array B and sorts 
    # elements for continuous sequence of 1 
    for i in range(0, n - 1) : 
        if (B[i]== 1) : 
            j = i 
            while (B[j]== 1) : 
                j = j + 1

            # Sort array A from i to j 
            A = A[0:i] + sorted(A[i:j + 1]) + A[j + 1:] 
            i = j 

    # Check if array is sorted or not 
    for i in range(0, n) : 
        if (A[i] != i + 1) : 
            return False

    return True

# Driver program to test sortedAfterSwap() 
A = [ 1, 2, 5, 3, 4, 6 ] 
B = [ 0, 1, 1, 1, 0 ] 
n = len(A) 

if (sortedAfterSwap(A, B, n)) : 
    print("A can be sorted") 
else : 
    print("A can not be sorted") 

# This code is contributed 
# by Nikita Tiwari. 

```

## C# 

```cs

// C# program to test whether array 
// can be sorted by swapping adjacent 
// elements using boolean array 
using System; 
class GFG { 

    // Return true if array can be 
    // sorted otherwise false 
    static bool sortedAfterSwap(int[] A, 
                                bool[] B, 
                                int n) 
    { 
        int i, j; 

        // Check bool array B and sorts 
        // elements for continuous sequence of 1 
        for (i = 0; i < n - 1; i++) { 
            if (B[i]) { 
                j = i; 
                while (B[j]) { 
                    j++; 
                } 
                // Sort array A from i to j 
                Array.Sort(A, i, 1 + j); 
                i = j; 
            } 
        } 

        // Check if array is sorted or not 
        for (i = 0; i < n; i++) { 
            if (A[i] != i + 1) { 
                return false; 
            } 
        } 

        return true; 
    } 

    // Driver Code 
    public static void Main() 
    { 
        int[] A = { 1, 2, 5, 3, 4, 6 }; 
        bool[] B = { false, true, true, true, false }; 
        int n = A.Length; 

        if (sortedAfterSwap(A, B, n)) { 
            Console.WriteLine("A can be sorted"); 
        } 

        else { 
            Console.WriteLine("A can not be sorted"); 
        } 
    } 
} 

// This code is contributed by Sam007 

```

## PHP

```php

<?php 
// PHP program to test whether array 
// can be sorted by swapping adjacent 
// elements using boolean array 

// Return true if array can be 
// sorted otherwise false 
function sortedAfterSwap($A, $B, $n) 
{ 

    // Check bool array B and sorts 
    // elements for continuous sequence of 1 
    for ($i = 0; $i < $n - 1; $i++)  
    { 
        if ($B[$i])  
        { 
            $j = $i; 
            while ($B[$j]) 
                $j++; 

            // Sort array A from i to j 
            sort($A); 
            $i = $j; 
        } 
    } 

    // Check if array is sorted or not 
    for ($i = 0; $i < $n; $i++) 
    { 
        if ($A[$i] != $i + 1) 
            return false; 
    } 

    return true; 
} 

    // Driver Code 
    $A = array(1, 2, 5, 3, 4, 6); 
    $B = array(0, 1, 1, 1, 0); 
    $n = count($A); 

    if (sortedAfterSwap($A, $B, $n)) 
        echo "A can be sorted\n"; 
    else
        echo "A can not be sorted\n"; 

// This code is contributed by Sam007 
?> 

```

**输出**：

```
A can be sorted

```

**替代方法**：

在这里，我们讨论一种非常直观的方法，该方法也为所有情况提供了`O(n)`时间的答案。 这里的想法是，只要二进制数组具有 1，我们就检查数组`A`中的索引是否具有`i + 1`。 如果它不包含`i + 1`，我们只需将`a[i]`与`a[i + 1]`交换即可。

原因是数组应该将`i + 1`存储在索引`i`处。 如果数组是可排序的，则唯一允许的操作是交换。 因此，如果不满足所需条件，我们只需交换。 如果数组是可排序的，交换将使我们更接近正确答案。 并且如预期的那样，如果该数组不可排序，则交换将导致同一数组的另一个未排序版本。

## C++

```cpp

// CPP program to test whether array 
// can be sorted by swapping adjacent 
// elements using boolean array 
#include <bits/stdc++.h> 
using namespace std; 

// Return true if array can be 
// sorted otherwise false 
bool sortedAfterSwap(int A[], bool B[], int n) 
{ 
    for (int i = 0; i < n - 1; i++) { 
        if (B[i]) { 
            if (A[i] != i + 1) 
                swap(A[i], A[i + 1]); 
        } 
    } 

    // Check if array is sorted or not 
    for (int i = 0; i < n; i++) { 
        if (A[i] != i + 1) 
            return false; 
    } 

    return true; 
} 

// Driver program to test sortedAfterSwap() 
int main() 
{ 
    int A[] = { 1, 2, 5, 3, 4, 6 }; 
    bool B[] = { 0, 1, 1, 1, 0 }; 
    int n = sizeof(A) / sizeof(A[0]); 

    if (sortedAfterSwap(A, B, n)) 
        cout << "A can be sorted\n"; 
    else
        cout << "A can not be sorted\n"; 

    return 0; 
} 

```

## Java

```java

// Java program to test whether an array 
// can be sorted by swapping adjacent 
// elements using boolean array 
class GFG 
{ 
    // Return true if array can be 
    // sorted otherwise false 
    static int sortedAfterSwap(int[] A,  
                            int[] B, int n) 
    { 
        int t = 0; 
        for (int i = 0; i < n - 1; i++)  
        { 
            if (B[i] != 0)  
            { 
                if (A[i] != i + 1) 
                    t = A[i]; 
                    A[i] = A[i + 1]; 
                    A[i + 1] = t; 
            } 
        } 

        // Check if array is sorted or not 
        for (int i = 0; i < n; i++) 
        { 
            if (A[i] != i + 1) 
                return 0; 
        } 

        return 1; 
    } 

    // Driver Code 
    public static void main(String[] args) 
    { 
        int[] A = { 1, 2, 5, 3, 4, 6 }; 
        int[] B = { 0, 1, 1, 1, 0 }; 
        int n = A.length; 

        if (sortedAfterSwap(A, B, n) == 0) 
            System.out.println("A can be sorted"); 
        else
            System.out.println("A can not be sorted"); 
    } 
} 

// This code is contributed  
// by Mukul Singh. 

```

## Python3

```py

# Python3 program to test whether array  
# can be sorted by swapping adjacent  
# elements using boolean array  

# Return true if array can be  
# sorted otherwise false  
def sortedAfterSwap(A,B,n): 
    for i in range(0,n-1): 
        if B[i]: 
            if A[i]!=i+1: 
                A[i], A[i+1] = A[i+1], A[i] 

    # Check if array is sorted or not 
    for i in range(n): 
        if A[i]!=i+1: 
            return False
    return True

# Driver program 
if __name__=='__main__': 
    A = [1, 2, 5, 3, 4, 6] 
    B = [0, 1, 1, 1, 0] 
    n =len(A) 
    if (sortedAfterSwap(A, B, n)) : 
        print("A can be sorted")  
    else : 
        print("A can not be sorted")  

# This code is contributed by  
# Shrikant13 

```

## C#

```cs

// C# program to test whether array 
// can be sorted by swapping adjacent 
// elements using boolean array 
using System; 

class GFG 
{ 
    // Return true if array can be 
    // sorted otherwise false 
    static int sortedAfterSwap(int[] A,  
                               int[] B, int n) 
    { 
        int t = 0; 
        for (int i = 0; i < n - 1; i++)  
        { 
            if (B[i] != 0)  
            { 
                if (A[i] != i + 1) 
                    t = A[i]; 
                    A[i] = A[i + 1]; 
                    A[i + 1] = t; 
            } 
        } 

        // Check if array is sorted or not 
        for (int i = 0; i < n; i++) 
        { 
            if (A[i] != i + 1) 
                return 0; 
        } 

        return 1; 
    } 

    // Driver Code 
    public static void Main() 
    { 
        int[] A = { 1, 2, 5, 3, 4, 6 }; 
        int[] B = { 0, 1, 1, 1, 0 }; 
        int n = A.Length; 

        if (sortedAfterSwap(A, B, n) == 0) 
            Console.WriteLine("A can be sorted"); 
        else
            Console.WriteLine("A can not be sorted"); 
    } 
} 

// This code is contributed  
// by Akanksha Rai 

```

## PHP

```php

<?php  
// PHP program to test whether array 
// can be sorted by swapping adjacent 
// elements using boolean array 

// Return true if array can be 
// sorted otherwise false 
function sortedAfterSwap(&$A, &$B, $n) 
{ 
    for ($i = 0; $i < $n - 1; $i++)  
    { 
        if ($B[$i])  
        { 
            if ($A[$i] != $i + 1) 
            { 
                $t = $A[$i]; 
                $A[$i] = $A[$i + 1]; 
                $A[$i + 1] = $t; 
            } 
        } 
    } 

    // Check if array is sorted or not 
    for ($i = 0; $i < $n; $i++)  
    { 
        if ($A[$i] != $i + 1) 
            return false; 
    } 

    return true; 
} 

// Driver Code 
$A = array( 1, 2, 5, 3, 4, 6 ); 
$B = array( 0, 1, 1, 1, 0 ); 
$n = sizeof($A); 

if (sortedAfterSwap($A, $B, $n)) 
    echo "A can be sorted\n"; 
else
    echo "A can not be sorted\n"; 

// This code is contributed by ita_c 
?> 

```

**输出**：

```
A can be sorted

```



* * *

* * *



