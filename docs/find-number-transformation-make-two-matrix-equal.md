# 查找使两个矩阵相等的变换数

> 原文： [https://www.geeksforgeeks.org/find-number-transformation-make-two-matrix-equal/](https://www.geeksforgeeks.org/find-number-transformation-make-two-matrix-equal/)

给定`n * m`阶的两个矩阵`A`和`B`。 任务是找到所需的转换步骤数，以使两个矩阵都相等，如果不可能，则打印 -1。

转换步骤如下：

1.  从两个矩阵中选择任意一个矩阵。

2.  选择所选矩阵的行/列。

3.  将所选行/列的每个元素加 1。

**示例**：

```
Input : 
A[2][2]: 1 1
         1 1
B[2][2]: 1 2
         3 4
Output : 3
Explanation :
1 1   ->   1 2   ->   1 2   ->   1 2
1 1   ->   1 2   ->   2 3   ->   3 4

Input :
A[2][2]: 1 1
         1 0
B[2][2]: 1 2
         3 4
Output : -1
Explanation : No transformation will make A and B equal.

```



解决此问题的关键步骤是：

将`A[][]`的任何行递增与将`B[][]`的同一行递减相同。 因此，在仅对一个矩阵递增或递减转换之后，我们便可以得到解决方案。

```
So make A[i][j] = A[i][j] - B[i][j].
For example,
If given matrices are,
A[2][2] : 1 1  
          1 1
B[2][2] : 1 2
          3 4
After subtraction, A[][] becomes,
A[2][2] : 0 -1
         -2 -3 

```

对于每个转换，第一行/第一列元素都必须更改，其他第`i`行/列也是如此。

如果`A[i][j] – A[i][0] – A[0][j] + A[0][0] != 0`，那么解不存在。

第 1 行和第 1 列的元素仅导致结果。

```
// Update matrix A[][]
// so that only A[][]
// has to be transformed
for (i = 0; i < n; i++)
    for (j = 0; j < m; j++)
        A[i][j] -= B[i][j];

// Check necessary condition
// For condition for 
// existence of full transformation
for (i = 1; i < n; i++)
    for (j = 1; j < m; j++)
        if (A[i][j] - A[i][0] - A[0][j] + A[0][0] != 0)
            return -1;

// If transformation is possible
// calculate total transformation
result = 0;
for (i = 0; i < n; i++)
    result += abs(A[i][0])
for (j = 0; j < m; j++)
    result += abs(A[0][j] - A[0][0]);
return abs(result);

```


## C++ 

```cpp

// C++ program to find 
// number of countOpsation 
// to make two matrix equals 
#include <bits/stdc++.h> 
using namespace std; 

const int MAX = 1000; 

int countOps(int A[][MAX], int B[][MAX],  
             int m, int n) 
{ 
    // Update matrix A[][] 
    // so that only A[][] 
    // has to be countOpsed 
    for (int i = 0; i < n; i++) 
        for (int j = 0; j < m; j++) 
            A[i][j] -= B[i][j]; 

    // Check necessary condition 
    // for condition for 
    // existence of full countOpsation 
    for (int i = 1; i < n; i++) 
    for (int j = 1; j < m; j++) 
        if (A[i][j] - A[i][0] -  
            A[0][j] + A[0][0] != 0) 
        return -1; 

    // If countOpsation is possible 
    // calculate total countOpsation 
    int result = 0; 
    for (int i = 0; i < n; i++) 
        result += abs(A[i][0]); 
    for (int j = 0; j < m; j++) 
        result += abs(A[0][j] - A[0][0]); 
    return (result); 
} 

// Driver code 
int main() 
{ 
    int A[MAX][MAX] = { {1, 1, 1}, 
                        {1, 1, 1}, 
                        {1, 1, 1}}; 
    int B[MAX][MAX] = { {1, 2, 3}, 
                        {4, 5, 6}, 
                        {7, 8, 9}}; 
    cout << countOps(A, B, 3, 3) ; 
    return 0; 
} 

```

## Java

```java

// Java program to find number of 
// countOpsation to make two matrix 
// equals 
import java.io.*; 

class GFG  
{ 

    static int countOps(int A[][], int B[][], 
                        int m, int n) 
    { 

        // Update matrix A[][] so that only 
        // A[][] has to be countOpsed 
        for (int i = 0; i < n; i++) 
            for (int j = 0; j < m; j++) 
                A[i][j] -= B[i][j]; 

        // Check necessary condition for  
        // condition for existence of full 
        // countOpsation 
        for (int i = 1; i < n; i++) 
            for (int j = 1; j < m; j++) 
                if (A[i][j] - A[i][0] -  
                    A[0][j] + A[0][0] != 0) 
                    return -1; 

        // If countOpsation is possible 
        // calculate total countOpsation 
        int result = 0; 

        for (int i = 0; i < n; i++) 
            result += Math.abs(A[i][0]); 

        for (int j = 0; j < m; j++) 
            result += Math.abs(A[0][j] - A[0][0]); 

        return (result); 
    } 

    // Driver code 
    public static void main (String[] args) 
    { 
        int A[][] = { {1, 1, 1}, 
                      {1, 1, 1}, 
                      {1, 1, 1} }; 

        int B[][] = { {1, 2, 3}, 
                      {4, 5, 6}, 
                      {7, 8, 9} }; 

        System.out.println(countOps(A, B, 3, 3)) ; 

    } 
} 

// This code is contributed by KRV. 

```

## Python3

```py

# Python3 program to find number of 
# countOpsation to make two matrix 
# equals 
def countOps(A, B, m, n): 

    # Update matrix A[][] so that only 
    # A[][] has to be countOpsed 
    for i in range(n): 
        for j in range(m): 
            A[i][j] -= B[i][j]; 

    # Check necessary condition for  
    # condition for existence of full 
    # countOpsation 
    for i in range(1, n): 
        for j in range(1, n): 
            if (A[i][j] - A[i][0] -
                A[0][j] + A[0][0] != 0): 
                return -1; 

    # If countOpsation is possible 
    # calculate total countOpsation 
    result = 0; 

    for i in range(n): 
        result += abs(A[i][0]); 

    for j in range(m): 
        result += abs(A[0][j] - A[0][0]); 

    return (result); 

# Driver code 
if __name__ == '__main__': 
    A = [[1, 1, 1], 
         [1, 1, 1], 
         [1, 1, 1]]; 

    B = [[1, 2, 3], 
         [4, 5, 6], 
         [7, 8, 9]]; 

    print(countOps(A, B, 3, 3)); 

# This code is contributed by Rajput-Ji 

```

## C# 

```cs

// C# program to find number of 
// countOpsation to make two matrix 
// equals 
using System; 

class GFG  
{ 

    static int countOps(int [,]A, int [,]B, 
                        int m, int n) 
    { 

        // Update matrix A[][] so that only 
        // A[][] has to be countOpsed 
        for (int i = 0; i < n; i++) 
            for (int j = 0; j < m; j++) 
                A[i, j] -= B[i, j]; 

        // Check necessary condition for  
        // condition for existence of full 
        // countOpsation 
        for (int i = 1; i < n; i++) 
            for (int j = 1; j < m; j++) 
                if (A[i, j] - A[i, 0] -  
                    A[0, j] + A[0, 0] != 0) 
                    return -1; 

        // If countOpsation is possible 
        // calculate total countOpsation 
        int result = 0; 

        for (int i = 0; i < n; i++) 
            result += Math.Abs(A[i, 0]); 

        for (int j = 0; j < m; j++) 
            result += Math.Abs(A[0, j] - A[0, 0]); 

        return (result); 
    } 

    // Driver code 
    public static void Main () 
    { 
        int [,]A = { {1, 1, 1}, 
                     {1, 1, 1}, 
                     {1, 1, 1} }; 

        int [,]B = { {1, 2, 3}, 
                     {4, 5, 6}, 
                     {7, 8, 9} }; 

    Console.Write(countOps(A, B, 3, 3)) ; 

    } 
} 

// This code is contributed by nitin mittal. 

```

## PHP

```php

<?php 
// PHP program to find 
// number of countOpsation 
// to make two matrix equals 

function countOps($A, $B,  
                  $m, $n) 
{ 
    $MAX = 1000; 

    // Update matrix A[][] 
    // so that only A[][] 
    // has to be countOpsed 
    for ($i = 0; $i < $n; $i++) 
        for ($j = 0; $j < $m; $j++) 
            $A[$i][$j] -= $B[$i][$j]; 

    // Check necessary condition 
    // for condition for 
    // existence of full countOpsation 
    for ($i = 1; $i < $n; $i++) 
    for ($j = 1; $j < $m; $j++) 
        if ($A[$i][$j] - $A[$i][0] -  
            $A[0][$j] + $A[0][0] != 0) 
        return -1; 

    // If countOpsation is possible 
    // calculate total countOpsation 
    $result = 0; 
    for ($i = 0; $i < $n; $i++) 
        $result += abs($A[$i][0]); 
    for ($j = 0; $j < $m; $j++) 
        $result += abs($A[0][$j] - $A[0][0]); 
    return ($result); 
} 

    // Driver code 
    $A = array(array(1, 1, 1), 
               array(1, 1, 1), 
               array(1, 1, 1)); 

    $B = array(array(1, 2, 3), 
               array(4, 5, 6), 
               array(7, 8, 9)); 
    echo countOps($A, $B, 3, 3) ; 

// This code is contributed by nitin mittal. 
?> 

```

 **输出**：

```
12

```

时间复杂度：`O(n * m)`。



