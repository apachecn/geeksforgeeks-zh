# 排序从 0 到`n ^ 2 – 1`的数字矩阵的最低成本

> 原文： [https://www.geeksforgeeks.org/minimum-cost-sort-matrix-numbers-0-n2-1/](https://www.geeksforgeeks.org/minimum-cost-sort-matrix-numbers-0-n2-1/)

给定一个`n x n`矩阵，其中包含 0 到`n ^ 2 - 1`范围内的所有数字。 问题是要计算以严格递增的顺序重新排列矩阵中所有数字所需的总能量，即，重新排列后，第一行包含从 0 到`n-1`的`n`个数字，然后第二行包含从`n`到`2n - 1`，依此类推，直到最后一行或第`n`行。 可以从当前位置向左，向右，顶部或底部四个方向移动数字，以在最终修改的矩阵中到达目标。 将数字从当前位置转移到所需目的地的步数是数字移动所需的能量。 例如，在`4 x 4`矩阵中，数字 6 出现在位置`(2, 3)`。 它在修改后的矩阵中的目标位置是`(1, 1)`。 因此，6 向左移动 2 步，向上移动 1 步到达位置`(1, 1)`。 共移动了 3 步，因此 6 所需的能量为 3 个单位。 这样，我们必须总结所有数字的移动/重新排列所需的所有能量。

**示例**：

```
Input : mat[][] = { {3, 0},
                    {2, 1} }
Output : 4 units
For number '3':
Move it one step right and one step down.
Total 2 steps thus energy required = 2 units.

For number '0':
Move it one step left.
Total 1 step thus energy required = 1 unit.

For number '1':
Move it one step up.
Total 1 step thus energy required = 1 unit.

Total energy required = 4 units.

Input : mat[][] = { {4, 7, 10, 3},
                {8, 5, 6, 1},
                  {9, 11, 10, 2},
            {15, 13, 14, 12} }                      
Output : 22 units

```



**算法**：

```
calculateEnergy(mat, n)
    Declare i_des, j_des, q
    Initialize tot_energy = 0
    for i = 0 to n-1
        for j = 0 to n-1
        q = mat[i][j] / n
        i_des = q
        j_des = mat[i][j] - (n * q)
        tot_energy += abs(i_des - i) + abs(j_des - j)    
    return tot_energy

```

## C++ 

```cpp

// C++ implementation to find the total energy 
// required to rearrange the numbers 
#include <bits/stdc++.h> 

using namespace std; 

#define SIZE 100 

// function to find the total energy 
// required to rearrange the numbers 
int calculateEnergy(int mat[SIZE][SIZE], int n) 
{ 
    int i_des, j_des, q; 
    int tot_energy = 0; 

    // nested loops to access the elements 
    // of the given matrix 
    for (int i = 0; i < n; i++) { 
        for (int j = 0; j < n; j++) { 
            // store quotient 
            q = mat[i][j] / n; 

            // final destination location (i_des, j_des) of 
            // the element mat[i][j] is being calculated 
            i_des = q; 
            j_des = mat[i][j] - (n * q); 

            // energy required for the movement of the 
            // element mat[i][j] is calculated and then 
            // accumulated in the 'tot_energy' 
            tot_energy += abs(i_des - i) + abs(j_des - j); 
        } 
    } 

    // required total energy 
    return tot_energy; 
} 

// Driver program to test above 
int main() 
{ 
    int mat[SIZE][SIZE] = { { 4, 7, 0, 3 }, 
                            { 8, 5, 6, 1 }, 
                            { 9, 11, 10, 2 }, 
                            { 15, 13, 14, 12 } }; 
    int n = 4; 

    cout << "Total energy required = "
         << calculateEnergy(mat, n) << " units"; 

    return 0; 
} 

```

## Java

```java

// Java implementation to find 
// the total energy required  
// to rearrange the numbers 

import java.util.*; 
import java.lang.*; 

public class GfG{ 

    private final static int SIZE  = 100; 

    // function to find the total energy 
    // required to rearrange the numbers 
    public static int calculateEnergy(int mat[][], 
    int n) 
    { 
        int i_des, j_des, q; 
        int tot_energy = 0; 

        // nested loops to access the elements 
        // of the given matrix 
        for (int i = 0; i < n; i++) { 

            for (int j = 0; j < n; j++) { 

                // store quotient 
                q = mat[i][j] / n; 

                // final destination location 
                // (i_des, j_des) of 
                // the element mat[i][j] is 
                // being calculated 
                i_des = q; 
                j_des = mat[i][j] - (n * q); 

                // energy required for the 
                // movement of the 
                // element mat[i][j] is 
                // calculated and then 
                // accumulated in the 'tot_energy' 
                tot_energy += Math.abs(i_des - i) + 
                Math.abs(j_des - j); 
            } 
        } 

        // required total energy 
        return tot_energy; 
    } 

    // Driver function 
    public static void main(String argc[]){ 

        int[][] mat = new int[][] {{ 4, 7, 0, 3 }, 
                                   { 8, 5, 6, 1 }, 
                                   { 9, 11, 10, 2 }, 
                                   { 15, 13, 14, 12 }}; 

        int n = 4; 

    System.out.println("Total energy required = "
         + calculateEnergy(mat, n) + " units"); 
    } 

} 
// This code is contributed by Sagar Shukla  

```

## Python3

```py

# implementation to find the total 
# energy required to rearrange the 
# numbers 
n = 4

# function to find the total energy 
# required to rearrange the numbers 
def calculateEnergy(mat,n): 

    tot_energy = 0

    # nested loops to access the  
    # elements of the given matrix 
    for i in range(n): 
        for j in range(n): 

            #store quotient 
            q = mat[i][j]//n 

            # final destination location 
            # (i_des, j_des) of the  
            # element mat[i][j] is being 
            # calculated 
            i_des = q 
            j_des = mat[i][j]- (n*q) 

            # energy required for the 
            # movement of the element 
            # mat[i][j] is calculated  
            # and then accumulated in 
            # the 'tot_energy' 
            tot_energy += (abs(i_des-i)  
                         + abs(j_des-j)) 

    # required total energy 
    return tot_energy 

# Driver Program 
mat = [[4, 7, 0, 3], 
       [8, 5, 6, 1], 
         [9, 11, 10, 2], 
       [15, 13, 14, 12]] 
print("Total energy required = ", 
        calculateEnergy(mat,n), "units") 

# This code is contributed by Shrikant13\. 

```

## C# 

```cs

// C# implementation to find 
// the total energy required 
// to rearrange the numbers 
using System; 

class GFG { 

    // function to find the total energy 
    // required to rearrange the numbers 
    public static int calculateEnergy(int[, ] mat, 
                                            int n) 
    { 
        int i_des, j_des, q; 
        int tot_energy = 0; 

        // nested loops to access the elements 
        // of the given matrix 
        for (int i = 0; i < n; i++) { 

            for (int j = 0; j < n; j++) { 

                // store quotient 
                q = mat[i, j] / n; 

                // final destination location 
                // (i_des, j_des) of 
                // the element mat[i][j] is 
                // being calculated 
                i_des = q; 
                j_des = mat[i, j] - (n * q); 

                // energy required for the 
                // movement of the 
                // element mat[i][j] is 
                // calculated and then 
                // accumulated in the 'tot_energy' 
                tot_energy += Math.Abs(i_des - i) +  
                              Math.Abs(j_des - j); 
            } 
        } 

        // required total energy 
        return tot_energy; 
    } 

    // Driver function 
    public static void Main() 
    { 

        int[, ] mat = new int[, ]{ { 4, 7, 0, 3 }, 
                                   { 8, 5, 6, 1 }, 
                                   { 9, 11, 10, 2 }, 
                                   { 15, 13, 14, 12 } }; 

        int n = 4; 

        Console.Write("Total energy required = " +  
              calculateEnergy(mat, n) + " units"); 
    } 
} 

// This code is contributed by Sam007 

```

## PHP

```php

<?php 
// PHP implementation to find  
// the total energy required  
// to rearrange the numbers 

// function to find the total energy 
// required to rearrange the numbers 
function calculateEnergy($mat, $n) 
{ 
    $i_des; $j_des; $q; 
    $tot_energy = 0; 

    // nested loops to access the  
    // elements of the given matrix 
    for ($i = 0; $i < $n; $i++)  
    { 
        for ($j = 0; $j < $n; $j++)  
        { 
            // store quotient 
            $q = (int)($mat[$i][$j] / $n); 

            // final destination location  
            // (i_des, j_des) of the element 
            // mat[i][j] is being calculated 
            $i_des = $q; 
            $j_des = $mat[$i][$j] - ($n * $q); 

            // energy required for the movement  
            // of the element mat[i][j] is  
            // calculated and then accumulated  
            // in the 'tot_energy' 
            $tot_energy += abs($i_des - $i) +  
                           abs($j_des - $j); 
        } 
    } 

    // required total energy 
    return $tot_energy; 
} 

// Driver Code 
$mat = array(array (4, 7, 0, 3), 
             array (8, 5, 6, 1), 
             array (9, 11, 10, 2), 
             array (15, 13, 14, 12)); 
$n = 4; 

echo "Total energy required = ", 
calculateEnergy($mat, $n) , " units"; 

// This code is contributed by ajit 
?> 

```

**输出**：

```
Total energy required = 22 units

```

**时间复杂度**：`O(n^2)`。



