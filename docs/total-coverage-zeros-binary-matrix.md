# 二进制矩阵中所有零的总覆盖率

> 原文： [https://www.geeksforgeeks.org/total-coverage-zeros-binary-matrix/](https://www.geeksforgeeks.org/total-coverage-zeros-binary-matrix/)

给定一个仅包含 0 和 1 的二进制矩阵，我们需要找到矩阵所有零的覆盖率总和，其中特定 0 的覆盖率定义为左，右，上和左零附近的总数。 底部指示。 那些可以在任何地方直到某个方向的拐角点。

**示例**：

```
Input : mat[][] = {0 0 0 0
                   1 0 0 1
                   0 1 1 0
                   0 1 0 0}
Output : 20
First four zeros are surrounded by only 
one 1\.  So coverage for zeros in first 
row is 1 + 1 + 1 + 1
Zeros in second row are surrounded by
three 1's. Note that there is no 1 above.
There are 1's in all other three directions.
Coverage of zeros in second row = 3 + 3\. 
Similarly counting for others also, we get
overall count as below.
1 + 1 + 1 + 1 + 3 + 3 + 2 + 2 + 2 + 2 + 2 = 20

Input : mat[][] = {1 1 1 0
                   1 0 0 1}
Output : 8
Coverage of first zero is 2
Coverages of other two zeros is 3
Total coverage = 2 + 3 + 3 = 8

```



解决此问题的**简单解决方案**是通过对零周围的数字进行独立计数，即对于给定的矩阵，我们在每个方向上针对每个单元在每个方向上运行四次循环。 每当在任何循环中找到 1 时，我们都会中断循环并将结果加 1。

一个**有效的解决方案**如下。

1.  从左到右遍历所有行，如果已经看到 1（在当前遍历中）并且当前元素为 0，则递增结果。

2.  从右向左遍历所有行，如果已经看到 1（在当前遍历中）并且当前元素为 0，则递增结果。

3.  从上到下遍历所有列，如果已经看到 1（在当前遍历中）并且当前元素为 0，则递增结果。

4.  从下到上遍历所有列，如果已经看到 1（在当前遍历中）并且当前元素为 0，则递增结果。

在下面的代码中，采用了布尔变量`isOne`，当在当前遍历中遇到一个布尔变量时，该变量即为真，对于迭代之后的所有零，结果加 1，在所有四个方向上应用相同的过程以获得最终答案。 。 每次遍历后，我们将`isOne`重置为`false`。

## C++ 

```cpp

//  C++ program to get total coverage of all zeros in 
// a binary matrix 
#include <bits/stdc++.h> 
using namespace std; 
#define R 4 
#define C 4 

// Returns total coverage of all zeros in mat[][] 
int getTotalCoverageOfMatrix(int mat[R][C]) 
{ 
    int res = 0; 

    //  looping for all rows of matrix 
    for (int i = 0; i < R; i++) 
    { 
        bool isOne = false;  // 1 is not seen yet 

        // looping in columns from left to right 
        // direction to get left ones 
        for (int j = 0; j < C; j++) 
        { 
            // If one is found from left 
            if (mat[i][j] == 1) 
                isOne = true; 

            // If 0 is found and we have found 
            // a 1 before. 
            else if (isOne) 
                res++; 
        } 

        // Repeat the above process for right to 
        // left direction. 
        isOne = false; 
        for (int j = C-1; j >= 0; j--) 
        { 
            if (mat[i][j] == 1) 
                isOne = true; 
            else if (isOne) 
                res++; 
        } 
    } 

    // Traversing across columms for up and down 
    // directions. 
    for (int j = 0; j < C; j++) 
    { 
        bool isOne = false;  // 1 is not seen yet 
        for (int i = 0; i < R; i++) 
        { 
            if (mat[i][j] == 1) 
                isOne = true; 
            else if (isOne) 
                res++; 
        } 

        isOne = false; 
        for (int i = R-1; i >= 0; i--) 
        { 
            if (mat[i][j] == 1) 
                isOne = true; 
            else if (isOne) 
                res++; 
        } 
    } 
    return res; 
} 

//  Driver code to test above methods 
int main() 
{ 
    int mat[R][C] = {{0, 0, 0, 0}, 
        {1, 0, 0, 1}, 
        {0, 1, 1, 0}, 
        {0, 1, 0, 0} 
    }; 

    cout << getTotalCoverageOfMatrix(mat); 

    return 0; 
} 

```

## Java

```java

// Java program to get total  
// coverage of all zeros in  
// a binary matrix 
import java .io.*; 

class GFG  
{ 
static int R = 4; 
static int C = 4; 

// Returns total coverage 
// of all zeros in mat[][] 
static int getTotalCoverageOfMatrix(int [][]mat) 
{ 
    int res = 0; 

    // looping for all  
    // rows of matrix 
    for (int i = 0; i < R; i++) 
    { 
        // 1 is not seen yet 
        boolean isOne = false;  

        // looping in columns from  
        // left to right direction 
        // to get left ones 
        for (int j = 0; j < C; j++) 
        { 
            // If one is found 
            // from left 
            if (mat[i][j] == 1) 
                isOne = true; 

            // If 0 is found and we  
            // have found a 1 before. 
            else if (isOne) 
                res++; 
        } 

        // Repeat the above  
        // process for right  
        // to left direction. 
        isOne = false; 
        for (int j = C - 1; j >= 0; j--) 
        { 
            if (mat[i][j] == 1) 
                isOne = true; 
            else if (isOne) 
                res++; 
        } 
    } 

    // Traversing across columms 
    // for up and down directions. 
    for (int j = 0; j < C; j++) 
    { 
        // 1 is not seen yet 
        boolean isOne = false;  
        for (int i = 0; i < R; i++) 
        { 
            if (mat[i][j] == 1) 
                isOne = true; 
            else if (isOne) 
                res++; 
        } 

        isOne = false; 
        for (int i = R - 1; i >= 0; i--) 
        { 
            if (mat[i][j] == 1) 
                isOne = true; 
            else if (isOne) 
                res++; 
        } 
    } 
    return res; 
} 

// Driver code  
static public void main (String[] args) 
{ 
    int [][]mat = {{0, 0, 0, 0}, 
                   {1, 0, 0, 1}, 
                   {0, 1, 1, 0}, 
                   {0, 1, 0, 0}}; 

System.out.println( 
           getTotalCoverageOfMatrix(mat)); 
} 
} 

// This code is contributed by anuj_67\. 

```

## Python3

```py

# Python3 program to get total coverage of all zeros in 
# a binary matrix 
R = 4
C = 4

# Returns total coverage of all zeros in mat[][] 
def getTotalCoverageOfMatrix(mat): 
    res = 0

    # looping for all rows of matrix 
    for i in range(R): 

        isOne = False # 1 is not seen yet 

        # looping in columns from left to right 
        # direction to get left ones 
        for j in range(C): 

            # If one is found from left 
            if (mat[i][j] == 1): 
                isOne = True

            # If 0 is found and we have found 
            # a 1 before. 
            elif (isOne): 
                res += 1

        # Repeat the above process for right to 
        # left direction. 
        isOne = False
        for j in range(C - 1, -1, -1): 
            if (mat[i][j] == 1): 
                isOne = True
            elif (isOne): 
                res += 1

    # Traversing across columms for up and down 
    # directions. 
    for j in range(C): 
        isOne = False # 1 is not seen yet 
        for i in range(R): 

            if (mat[i][j] == 1): 
                isOne = True
            elif (isOne): 
                res += 1

        isOne = False
        for i in range(R - 1, -1, -1): 
            if (mat[i][j] == 1): 
                isOne = True
            elif (isOne): 
                res += 1

    return res 

# Driver code 
mat = [[0, 0, 0, 0],[1, 0, 0, 1],[0, 1, 1, 0],[0, 1, 0, 0]] 
print(getTotalCoverageOfMatrix(mat)) 

# This code is contributed by shubhamsingh10 

```

## C# 

```cs

// C# program to get total coverage  
// of all zeros in a binary matrix 
using System; 

class GFG { 

static int R = 4; 
static int C = 4; 

// Returns total coverage of all zeros in mat[][] 
static int getTotalCoverageOfMatrix(int [,]mat) 
{ 
    int res = 0; 

    // looping for all rows of matrix 
    for (int i = 0; i < R; i++) 
    { 
        // 1 is not seen yet 
        bool isOne = false;  

        // looping in columns from left to  
        // right direction to get left ones 
        for (int j = 0; j < C; j++) 
        { 
            // If one is found from left 
            if (mat[i,j] == 1) 
                isOne = true; 

            // If 0 is found and we  
            // have found a 1 before. 
            else if (isOne) 
                res++; 
        } 

        // Repeat the above process for  
        // right to left direction. 
        isOne = false; 
        for (int j = C-1; j >= 0; j--) 
        { 
            if (mat[i,j] == 1) 
                isOne = true; 
            else if (isOne) 
                res++; 
        } 
    } 

    // Traversing across columms 
    // for up and down directions. 
    for (int j = 0; j < C; j++) 
    { 
        // 1 is not seen yet 
        bool isOne = false;  
        for (int i = 0; i < R; i++) 
        { 
            if (mat[i,j] == 1) 
                isOne = true; 
            else if (isOne) 
                res++; 
        } 

        isOne = false; 
        for (int i = R-1; i >= 0; i--) 
        { 
            if (mat[i,j] == 1) 
                isOne = true; 
            else if (isOne) 
                res++; 
        } 
    } 
    return res; 
} 

// Driver code to test above methods 
    static public void Main () 
    { 
        int [,]mat = {{0, 0, 0, 0}, 
                      {1, 0, 0, 1}, 
                      {0, 1, 1, 0}, 
                      {0, 1, 0, 0}}; 

    Console.WriteLine(getTotalCoverageOfMatrix(mat)); 
    } 
} 

// This code is contributed by vt_m. 

```

**输出**：

```
20

```

**时间复杂度**：`O(n^2)`。

**辅助空间**：`O(1)`。



