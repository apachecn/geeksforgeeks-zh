# 检查给定矩阵是否为幻方

> 原文： [https://www.geeksforgeeks.org/check-given-matrix-is-magic-square-or-not/](https://www.geeksforgeeks.org/check-given-matrix-is-magic-square-or-not/)

给定一个矩阵，检查它是否为[幻方](https://www.geeksforgeeks.org/magic-square/)。 幻方是从 1 到`n ^ 2`的不同元素的`n x n`矩阵，其中任何行，列或对角线的总和始终等于相同的数字。

例子：

```
Input : n = 3
  2   7   6
  9   5   1
  4   3   8
Output : Magic matrix
Explanation:In matrix sum of each
row and each column and diagonals sum is 
same = 15.

Input : n = 3
  1   2   2 
  2   2   1
  2   1   2
Output : Not a Magic Matrix
Explanation:In matrix sum of each
row and each column and diagonals sum is
not same.

```



1.找到主要对角线和次要对角线的和。

2.计算每行和每列的总和。

3.如果主要对角线和辅助对角线的总和等于每一行的总和和每一列的总和，则它是幻矩阵。

## C++ 

```cpp

// C++ program to check whether a given  
// matrix is magic matrix or not 
#include <bits/stdc++.h> 

#define N 3 
using namespace std; 

// Returns true if mat[][] is magic 
// square, else returns false. 
bool isMagicSquare(int mat[][N]) 
{  
    // calculate the sum of  
    // the prime diagonal 
    int sum = 0,sum2=0;  
    for (int i = 0; i < N; i++) 
        sum = sum + mat[i][i]; 
    // the secondary diagonal 
    for (int i = 0; i < N; i++) 
        sum2 = sum2 + mat[i][N-1-i]; 

    if(sum!=sum2)  
        return false; 

    // For sums of Rows  
    for (int i = 0; i < N; i++) { 

        int rowSum = 0;      
        for (int j = 0; j < N; j++) 
            rowSum += mat[i][j]; 

        // check if every row sum is 
        // equal to prime diagonal sum 
        if (rowSum != sum) 
            return false; 
    } 

    // For sums of Columns 
    for (int i = 0; i < N; i++) { 

        int colSum = 0;      
        for (int j = 0; j < N; j++) 
            colSum += mat[j][i]; 

        // check if every column sum is  
        // equal to prime diagonal sum 
        if (sum != colSum)  
        return false; 
    } 

    return true; 
} 

// driver program to  
// test above function 
int main() 
{ 
    int mat[][N] = {{ 2, 7, 6 }, 
                    { 9, 5, 1 }, 
                    { 4, 3, 8 }}; 

    if (isMagicSquare(mat)) 
        cout << "Magic Square"; 
    else
        cout << "Not a magic Square"; 

    return 0; 
} 

```

## Java

```java

// JAVA program to check whether a given 
// matrix is magic matrix or not 

import java.io.*; 

class GFG { 

    static int N = 3; 

    // Returns true if mat[][] is magic 
    // square, else returns false. 
    static boolean isMagicSquare(int mat[][]) 
    { 

        // calculate the sum of 
        // the prime diagonal 
         int sum = 0,sum2=0;  
        for (int i = 0; i < N; i++) 
            sum = sum + mat[i][i]; 

        // the secondary diagonal 
        for (int i = 0; i < N; i++) 
            sum2 = sum2 + mat[i][N-1-i]; 

        if(sum!=sum2)  
            return false; 

        // For sums of Rows 
        for (int i = 0; i < N; i++) { 

            int rowSum = 0; 
            for (int j = 0; j < N; j++) 
                rowSum += mat[i][j]; 

            // check if every row sum is 
            // equal to prime diagonal sum 
            if (rowSum != sum) 
                return false; 
        } 

        // For sums of Columns 
        for (int i = 0; i < N; i++) { 

            int colSum = 0; 
            for (int j = 0; j < N; j++) 
                colSum += mat[j][i]; 

            // check if every column sum is 
            // equal to prime diagonal sum 
            if (sum != colSum) 
                return false; 
        } 

        return true; 
    } 

    // driver program to 
    // test above function 
    public static void main(String[] args) 
    { 
        int mat[][] = {{ 2, 7, 6 }, 
                       { 9, 5, 1 }, 
                       { 4, 3, 8 }}; 

        if (isMagicSquare(mat)) 
            System.out.println("Magic Square"); 
        else
            System.out.println("Not a magic" + 
                                    " Square"); 
    } 
} 
// This code is contributed by vt_m 

```

## Python3

```py

# Python3 program to check whether a given  
# matrix is magic matrix or not 
N = 3

# Returns true if mat[][] is magic 
# square, else returns false. 
def isMagicSquare( mat) : 

    # calculate the sum of  
    # the prime diagonal 
    s = 0 

    for i in range(0, N) : 
        s = s + mat[i][i] 

    # the secondary diagonal 
    s2 = 0
    for i in range(0, N) : 
        s2 = s2 + mat[i][N-i-1] 

    if(s!=s2) : 
        return False

    # For sums of Rows  
    for i in range(0, N) : 
        rowSum = 0;      
        for j in range(0, N) : 
            rowSum += mat[i][j] 

        # check if every row sum is 
        # equal to prime diagonal sum 
        if (rowSum != s) : 
            return False

    # For sums of Columns 
    for i in range(0, N): 
        colSum = 0
        for j in range(0, N) : 
            colSum += mat[j][i] 

        # check if every column sum is  
        # equal to prime diagonal sum 
        if (s != colSum) : 
            return False

    return True

# Driver Code 
mat = [ [ 2, 7, 6 ], 
        [ 9, 5, 1 ], 
        [ 4, 3, 8 ] ] 

if (isMagicSquare(mat)) : 
    print( "Magic Square") 
else : 
    print( "Not a magic Square") 
# This code is contributed by Nikita Tiwari.     

```

## C# 

```cs

// C# program to check whether a given 
// matrix is magic matrix or not 
using System; 

class GFG  
{ 

    static int N = 3; 

    // Returns true if mat[][] is magic 
    // square, else returns false. 
    static bool isMagicSquare(int[,] mat) 
    { 

        // calculate the sum of 
        // the prime diagonal 
        int sum = 0, sum2 = 0; 

        for (int i = 0; i < N; i++) 
            sum = sum + mat[i, i]; 

        // the secondary diagonal 
        for (int i = 0; i < N; i++) 
            sum2 = sum2 + mat[i, N-1-i]; 

        if(sum!=sum2) 
            return false; 

        // For sums of Rows 
        for (int i = 0; i < N; i++) { 

            int rowSum = 0; 
            for (int j = 0; j < N; j++) 
                rowSum += mat[i, j]; 

            // check if every row sum is 
            // equal to prime diagonal sum 
            if (rowSum != sum) 
                return false; 
        } 

        // For sums of Columns 
        for (int i = 0; i < N; i++)  
        { 

            int colSum = 0; 
            for (int j = 0; j < N; j++) 
                colSum += mat[j,i]; 

            // check if every column sum is 
            // equal to prime diagonal sum 
            if (sum != colSum) 
                return false; 
        } 

        return true; 
    } 

    // Driver Code 
    public static void Main() 
    { 
        int[,] mat =new int [,] {{ 2, 7, 6 }, 
                                 { 9, 5, 1 }, 
                                 { 4, 3, 8 }}; 

        if (isMagicSquare(mat)) 
            Console.WriteLine("Magic Square"); 
        else
            Console.WriteLine("Not a magic" + 
                              " Square"); 
    } 
} 
// This code is contributed by KRV. 

```

## PHP

```php

<?php 
// PHP program to check whether a given  
// matrix is magic matrix or not 

// Returns true if mat[][] is magic 
// square, else returns false. 
function isMagicSquare($mat) 
{ 

    // calculate the sum of  
    // the prime diagonal 
    $sum = 0; $N=3; 
    for($i = 0; $i < $N; $i++) 
        $sum = $sum + $mat[$i][$i]; 

    // the secondary diagonal 
    $sum2 = 0; $N=3; 
    for($i = 0; $i < $N; $i++) 
        $sum2 = $sum2 + $mat[$i][$N-$i-1]; 

    if( $sum != $sum2) 
        return false; 

    // For sums of Rows  
    for($i = 0; $i < $N; $i++)  
    { 

        $rowSum = 0;      
        for ($j = 0; $j < $N; $j++) 
            $rowSum += $mat[$i][$j]; 

        // check if every row sum is 
        // equal to prime diagonal sum 
        if ($rowSum != $sum) 
            return false; 
    } 

    // For sums of Columns 
    for ($i = 0; $i < $N; $i++) 
    { 

        $colSum = 0;      
        for ($j = 0; $j < $N; $j++) 
            $colSum += $mat[$j][$i]; 

        // check if every column sum is  
        // equal to prime diagonal sum 
        if ($sum != $colSum)  
        return false; 
    } 

    return true; 
} 

// Driver Code 
{ 
    $mat = array(array(2, 7, 6), 
                   array(9, 5, 1), 
                 array(4, 3, 8)); 

    if (isMagicSquare($mat)) 
        echo "Magic Square"; 
    else
        echo "Not a magic Square"; 

    return 0; 
} 

?> 
// This code is contributed by nitin mittal 

```

```
Magic square

```



* * *

* * *



