# 将方形矩阵旋转 90 度 | 系列 1

> 原文： [https://www.geeksforgeeks.org/inplace-rotate-square-matrix-by-90-degrees/](https://www.geeksforgeeks.org/inplace-rotate-square-matrix-by-90-degrees/)

给定一个正方形矩阵，将其沿逆时针方向旋转 90 度，而无需使用任何额外空间。

**示例**：

```
Input:
Matrix:
 1  2  3
 4  5  6
 7  8  9
Output:
 3  6  9 
 2  5  8 
 1  4  7 
The given matrix is rotated by 90 degree 
in anti-clockwise direction.

Input:
 1  2  3  4 
 5  6  7  8 
 9 10 11 12 
13 14 15 16 
Output:
 4  8 12 16 
 3  7 11 15 
 2  6 10 14 
 1  5  9 13
The given matrix is rotated by 90 degree 
in anti-clockwise direction.

```



[**在这里**](https://www.geeksforgeeks.org/turn-an-image-by-90-degree/)已经讨论了需要额外空间的方法。

**方法**：要解决此问题而没有任何额外空间，请以正方形形式旋转数组，将矩阵划分为正方形或周期。 例如，一个`4 X 4`矩阵将具有 2 个周期。 第一个循环由其第一行，最后一列，最后一行和第一列组成。 第二周期由第二行，倒数第二列，倒数第二行和第二列组成。 这个想法是针对每个平方周期，沿逆时针方向交换矩阵中与相应单元格有关的元素，即一次从上至左，从左至下，从下至右，从右至上一次，只使用一个临时变量来实现这一目标。

**演示**：

```
First Cycle (Involves Red Elements)
 1  2  3 4 
 5  6  7 8 
 9 10 11 12 
 13 14 15 16 

Moving first group of four elements (First
elements of 1st row, last row, 1st column 
and last column) of first cycle in counter
clockwise. 
 4  2  3 16
 5  6  7 8 
 9 10 11 12 
 1 14  15 13 

Moving next group of four elements of 
first cycle in counter clockwise 
 4  8  3 16 
 5  6  7  15  
 2  10 11 12 
 1  14  9 13 

Moving final group of four elements of 
first cycle in counter clockwise 
 4  8 12 16 
 3  6  7 15 
 2 10 11 14 
 1  5  9 13 

Second Cycle (Involves Blue Elements)
 4  8 12 16 
 3  6 7  15 
 2  10 11 14 
 1  5  9 13 

Fixing second cycle
 4  8 12 16 
 3  7 11 15 
 2  6 10 14 
 1  5  9 13
```

**算法**：

1.  在`N`边的矩阵中有`N / 2`个正方形或周期。一次处理一个正方形。 运行循环以一次循环遍历矩阵，即从 0 循环到`N / 2 – 1`，循环计数器为`i`。

2.  考虑当前正方形 4 组中的元素，一次旋转 4 个元素。 因此，一个循环中此类组的数量为`N – 2 * i`。

3.  因此，在从`x`到`N – x – 1`的每个周期中运行一个循环。循环计数器为`y`。

4.  当前组中的元素是`(x, y)`，`(y, N-1-x)`，`(N-1-x, N-1-y)`，`(N-1-y, x)`，现在旋转这 4 个元素，即`(x, y) <- (y, N-1-x)`，`(y, N-1-x) <- (N-1-x, N-1-y)`，`(N-1-x, N-1-y) <- (N-1-y, x)`，`(N-1-y, x) <- (x, y)`。

5.  打印矩阵。

## C++ 

```cpp

// C++ program to rotate a matrix 
// by 90 degrees 
#include <bits/stdc++.h> 
#define N 4 
using namespace std; 

void displayMatrix( 
    int mat[N][N]); 

// An Inplace function to 
// rotate a N x N matrix 
// by 90 degrees in 
// anti-clockwise direction 
void rotateMatrix(int mat[][N]) 
{ 
    // Consider all squares one by one 
    for (int x = 0; x < N / 2; x++) { 
        // Consider elements in group 
        // of 4 in current square 
        for (int y = x; y < N - x - 1; y++) { 
            // Store current cell in 
            // temp variable 
            int temp = mat[x][y]; 

            // Move values from right to top 
            mat[x][y] = mat[y][N - 1 - x]; 

            // Move values from bottom to right 
            mat[y][N - 1 - x] 
                = mat[N - 1 - x][N - 1 - y]; 

            // Move values from left to bottom 
            mat[N - 1 - x][N - 1 - y] 
                = mat[N - 1 - y][x]; 

            // Assign temp to left 
            mat[N - 1 - y][x] = temp; 
        } 
    } 
} 

// Function to print the matrix 
void displayMatrix(int mat[N][N]) 
{ 
    for (int i = 0; i < N; i++) { 
        for (int j = 0; j < N; j++) 
            printf("%2d ", mat[i][j]); 

        printf("\n"); 
    } 
    printf("\n"); 
} 

/* Driver program to test above functions */
int main() 
{ 
    // Test Case 1 
    int mat[N][N] = { 
        { 1, 2, 3, 4 }, 
        { 5, 6, 7, 8 }, 
        { 9, 10, 11, 12 }, 
        { 13, 14, 15, 16 } 
    }; 

    // Tese Case 2 
    /* int mat[N][N] = { 
                        {1, 2, 3}, 
                        {4, 5, 6}, 
                        {7, 8, 9} 
                    }; 
     */

    // Tese Case 3 
    /*int mat[N][N] = { 
                    {1, 2}, 
                    {4, 5} 
                };*/

    // displayMatrix(mat); 

    rotateMatrix(mat); 

    // Print rotated matrix 
    displayMatrix(mat); 

    return 0; 
} 

```

## Java

```java

// Java program to rotate a 
// matrix by 90 degrees 
import java.io.*; 

class GFG { 
    // An Inplace function to 
    // rotate a N x N matrix 
    // by 90 degrees in 
    // anti-clockwise direction 
    static void rotateMatrix( 
        int N, int mat[][]) 
    { 
        // Consider all squares one by one 
        for (int x = 0; x < N / 2; x++) { 
            // Consider elements in group 
            // of 4 in current square 
            for (int y = x; y < N - x - 1; y++) { 
                // Store current cell in 
                // temp variable 
                int temp = mat[x][y]; 

                // Move values from right to top 
                mat[x][y] = mat[y][N - 1 - x]; 

                // Move values from bottom to right 
                mat[y][N - 1 - x] 
                    = mat[N - 1 - x][N - 1 - y]; 

                // Move values from left to bottom 
                mat[N - 1 - x][N - 1 - y] = mat[N - 1 - y][x]; 

                // Assign temp to left 
                mat[N - 1 - y][x] = temp; 
            } 
        } 
    } 

    // Function to print the matrix 
    static void displayMatrix( 
        int N, int mat[][]) 
    { 
        for (int i = 0; i < N; i++) { 
            for (int j = 0; j < N; j++) 
                System.out.print( 
                    " " + mat[i][j]); 

            System.out.print("\n"); 
        } 
        System.out.print("\n"); 
    } 

    /* Driver program to test above functions */
    public static void main(String[] args) 
    { 
        int N = 4; 

        // Test Case 1 
        int mat[][] = { 
            { 1, 2, 3, 4 }, 
            { 5, 6, 7, 8 }, 
            { 9, 10, 11, 12 }, 
            { 13, 14, 15, 16 } 
        }; 

        // Tese Case 2 
        /* int mat[][] = { 
                            {1, 2, 3}, 
                            {4, 5, 6}, 
                            {7, 8, 9} 
                        }; 
         */

        // Tese Case 3 
        /*int mat[][] = { 
                        {1, 2}, 
                        {4, 5} 
                    };*/

        // displayMatrix(mat); 

        rotateMatrix(N, mat); 

        // Print rotated matrix 
        displayMatrix(N, mat); 
    } 
} 

// This code is contributed by Prakriti Gupta 

```

## Python3

```py

# Python3 program to rotate a matrix by 90 degrees 
N = 4

# An Inplace function to rotate  
# N x N matrix by 90 degrees in 
# anti-clockwise direction 
def rotateMatrix(mat): 

    # Consider all squares one by one 
    for x in range(0, int(N / 2)): 

        # Consider elements in group    
        # of 4 in current square 
        for y in range(x, N-x-1): 

            # store current cell in temp variable 
            temp = mat[x][y] 

            # move values from right to top 
            mat[x][y] = mat[y][N-1-x] 

            # move values from bottom to right 
            mat[y][N-1-x] = mat[N-1-x][N-1-y] 

            # move values from left to bottom 
            mat[N-1-x][N-1-y] = mat[N-1-y][x] 

            # assign temp to left 
            mat[N-1-y][x] = temp 

# Function to print the matrix 
def displayMatrix( mat ): 

    for i in range(0, N): 

        for j in range(0, N): 

            print (mat[i][j], end = ' ') 
        print ("") 

# Driver Code 
mat = [[0 for x in range(N)] for y in range(N)] 

# Test case 1 
mat = [ [1, 2, 3, 4 ], 
        [5, 6, 7, 8 ], 
        [9, 10, 11, 12 ], 
        [13, 14, 15, 16 ] ] 

''' 
# Test case 2 
mat = [ [1, 2, 3 ], 
        [4, 5, 6 ], 
        [7, 8, 9 ] ] 

# Test case 3 
mat = [ [1, 2 ], 
        [4, 5 ] ] 

'''

rotateMatrix(mat) 

# Print rotated matrix 
displayMatrix(mat) 

# This code is contributed by saloni1297 

```

## C# 

```cs

// C# program to rotate a 
// matrix by 90 degrees 
using System; 

class GFG { 
    // An Inplace function to 
    // rotate a N x N matrix 
    // by 90 degrees in anti- 
    // clockwise direction 
    static void rotateMatrix(int N, 
                             int[, ] mat) 
    { 
        // Consider all 
        // squares one by one 
        for (int x = 0; x < N / 2; x++) { 
            // Consider elements 
            // in group of 4 in 
            // current square 
            for (int y = x; y < N - x - 1; y++) { 
                // store current cell 
                // in temp variable 
                int temp = mat[x, y]; 

                // move values from 
                // right to top 
                mat[x, y] = mat[y, N - 1 - x]; 

                // move values from 
                // bottom to right 
                mat[y, N - 1 - x] = mat[N - 1 - x, 
                                        N - 1 - y]; 

                // move values from 
                // left to bottom 
                mat[N - 1 - x, 
                    N - 1 - y] 
                    = mat[N - 1 - y, x]; 

                // assign temp to left 
                mat[N - 1 - y, x] = temp; 
            } 
        } 
    } 

    // Function to print the matrix 
    static void displayMatrix(int N, 
                              int[, ] mat) 
    { 
        for (int i = 0; i < N; i++) { 
            for (int j = 0; j < N; j++) 
                Console.Write(" " + mat[i, j]); 
            Console.WriteLine(); 
        } 
        Console.WriteLine(); 
    } 

    // Driver Code 
    static public void Main() 
    { 
        int N = 4; 

        // Test Case 1 
        int[, ] mat = { 
            { 1, 2, 3, 4 }, 
            { 5, 6, 7, 8 }, 
            { 9, 10, 11, 12 }, 
            { 13, 14, 15, 16 } 
        }; 

        // Tese Case 2 
        /* int mat[][] =  
        { 
            {1, 2, 3}, 
            {4, 5, 6}, 
            {7, 8, 9} 
        }; 
        */

        // Tese Case 3 
        /*int mat[][] =  
        { 
            {1, 2}, 
            {4, 5} 
        };*/

        // displayMatrix(mat); 

        rotateMatrix(N, mat); 

        // Print rotated matrix 
        displayMatrix(N, mat); 
    } 
} 

// This code is contributed by ajit 

```

## PHP

```php

<?php  
// PHP program to rotate a  
// matrix by 90 degrees 
$N = 4; 

// An Inplace function to  
// rotate a N x N matrix 
// by 90 degrees in  
// anti-clockwise direction 
function rotateMatrix(&$mat) 
{ 
    global $N; 

    // Consider all  
    // squares one by one 
    for ($x = 0; $x < $N / 2; $x++) 
    { 
        // Consider elements  
        // in group of 4 in  
        // current square 
        for ($y = $x;  
             $y < $N - $x - 1; $y++) 
        { 
            // store current cell 
            // in temp variable 
            $temp = $mat[$x][$y]; 

            // move values from 
            // right to top 
            $mat[$x][$y] = $mat[$y][$N - 1 - $x]; 

            // move values from 
            // bottom to right 
            $mat[$y][$N - 1 - $x] =  
                $mat[$N - 1 - $x][$N - 1 - $y]; 

            // move values from  
            // left to bottom 
            $mat[$N - 1 - $x][$N - 1 - $y] =  
                         $mat[$N - 1 - $y][$x]; 

            // assign temp to left 
            $mat[$N - 1 - $y][$x] = $temp; 
        } 
    } 
} 

// Function to  
// print the matrix 
function displayMatrix(&$mat) 
{ 
    global $N; 
    for ($i = 0; $i < $N; $i++) 
    { 
        for ($j = 0; $j < $N; $j++) 
            echo $mat[$i][$j] . " "; 

        echo "\n"; 
    } 
    echo "\n"; 
} 

// Driver code 

// Test Case 1 
$mat =  array(array(1, 2, 3, 4), 
              array(5, 6, 7, 8), 
              array(9, 10, 11, 12), 
              array(13, 14, 15, 16)); 

// Tese Case 2 
/* $mat = array(array(1, 2, 3), 
                array(4, 5, 6), 
                array(7, 8, 9)); 
*/

// Tese Case 3 
/*$mat = array(array(1, 2), 
               array(4, 5));*/

// displayMatrix($mat); 
rotateMatrix($mat); 

// Print rotated matrix 
displayMatrix($mat); 

// This code is contributed  
// by ChitraNayal 
?> 

```

**输出**：

```
 4  8 12 16 
 3  7 11 15 
 2  6 10 14 
 1  5  9 13 

```

**复杂度分析**：

*   **时间复杂度**：`O(n * n)`，其中`n`是数组的边。

    需要矩阵的单个遍历。

*   **空间复杂度**：`O(1)`。

    由于需要一个恒定的空间。

**练习**：将 2D 矩阵沿顺时针方向旋转 90 度，而无需使用额外的空间。

[**将矩阵旋转 90 度，而无需使用任何额外空间 | 系列 2**](https://www.geeksforgeeks.org/rotate-matrix-90-degree-without-using-extra-space-set-2/)

