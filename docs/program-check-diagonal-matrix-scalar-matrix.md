# 检查对角矩阵和标量矩阵的程序

> 原文： [https://www.geeksforgeeks.org/program-check-diagonal-matrix-scalar-matrix/](https://www.geeksforgeeks.org/program-check-diagonal-matrix-scalar-matrix/)

[**对角矩阵**](https://en.wikipedia.org/wiki/Diagonal_matrix)：

如果矩阵的除主对角线以外的元素为零，则称方阵为对角线矩阵。 平方零矩阵也是主要对角元素为零的对角矩阵。

**示例**：

```
Input : 
Mat[4][0] = {{4, 0, 0, 0},
             {0, 5, 0, 0},
             {0, 0, 2, 0},
         {0, 0, 0, 1}}
Output : Yes

Mat[4][0] = {{6, 10, 12, 0},
             {0, 5, 0, 0},
             {0, 0, 9, 0},
             {0, 0, 0, 1}}
Output : No

```



## CPP

```

// Program to check matrix is diagonal matrix or not. 
#include <bits/stdc++.h> 
#define N 4 
using namespace std; 

// Function to check matrix is diagonal matrix 
// or not. 
bool isDiagonalMatrix(int mat[N][N]) 
{ 
    for (int i = 0; i < N; i++) 
        for (int j = 0; j < N; j++) 

            // condition to check other elements  
            // except main diagonal are zero or not. 
            if ((i != j) && (mat[i][j] != 0)) 
                return false; 
    return true; 
} 

// Driver function 
int main() 
{ 
    int mat[N][N] = { { 4, 0, 0, 0 }, 
                      { 0, 7, 0, 0 }, 
                      { 0, 0, 5, 0 }, 
                      { 0, 0, 0, 1 } }; 

    if (isDiagonalMatrix(mat)) 
        cout << "Yes" << endl; 
    else
        cout << "No" << endl; 
    return 0; 
} 

```

## Java

```java

// Program to check matrix is 
// diagonal matrix or not. 

import java.io.*; 

class GFG { 

    static int N = 4; 

    // Function to check matrix 
    // is diagonal matrix 
    // or not. 
    static boolean isDiagonalMatrix(int mat[][]) 
    { 
        for (int i = 0; i < N; i++) 
            for (int j = 0; j < N; j++) 

                // condition to check 
                // other elements  
                // except main diagonal  
                // are zero or not. 
                if ((i != j) && 
                   (mat[i][j] != 0)) 
                    return false; 

        return true; 
    } 

    // Driver function 
    public static void main(String args[]) 
    { 
        int mat[][] = { { 4, 0, 0, 0 }, 
                          { 0, 7, 0, 0 }, 
                          { 0, 0, 5, 0 }, 
                          { 0, 0, 0, 1 } }; 

        if (isDiagonalMatrix(mat)) 
            System.out.println("Yes"); 
        else
            System.out.println("No" ); 
    } 
} 

// This code is contributed by 
// Nikita Tiwari. 

```

## Python3

```py

# Python3 Program to check if matrix 
# is diagonal matrix or not. 

N = 4

# Function to check matrix 
# is diagonal matrix 
# or not.    
def isDiagonalMatrix(mat) : 
    for i in range(0, N): 
        for j in range(0, N) : 

            # condition to check 
            # other elements  
            # except main diagonal 
            # are zero or not. 
            if ((i != j) and
             (mat[i][j] != 0)) : 
                return False

    return True

# Driver function 
mat = [[ 4, 0, 0, 0 ], 
       [ 0, 7, 0, 0 ], 
       [ 0, 0, 5, 0 ], 
       [ 0, 0, 0, 1 ]] 

if (isDiagonalMatrix(mat)) : 
    print("Yes") 
else : 
    print("No") 

# This code is contributed by Nikita Tiwari. 

```

## C# 

```cs

// Program to check matrix is 
// diagonal matrix or not. 
using System; 

class GFG { 

    static int N = 4; 

    // Function to check matrix 
    // is diagonal matrix 
    // or not. 
    static bool isDiagonalMatrix(int [,]mat) 
    { 
        for (int i = 0; i < N; i++) 
            for (int j = 0; j < N; j++) 

                // condition to check 
                // other elements  
                // except main diagonal  
                // are zero or not. 
                if ((i != j) &&    (mat[i,j] != 0)) 
                    return false; 

        return true; 
    } 

    // Driver function 
    public static void Main() 
    { 
        int [,]mat = { { 4, 0, 0, 0 }, 
                        { 0, 7, 0, 0 }, 
                        { 0, 0, 5, 0 }, 
                        { 0, 0, 0, 1 } }; 

        if (isDiagonalMatrix(mat)) 
            Console.WriteLine("Yes"); 
        else
            Console.WriteLine("No" ); 
    } 
} 

// This code is contributed by 
// vt_m. 

```

## PHP

```php

<?php 
// Program to check matrix is 
// diagonal matrix or not. 

$N= 4; 

// Function to check matrix is 
// diagonal matrix or not. 
function isDiagonalMatrix($mat) 
{ 
    global $N; 
    for ($i = 0; $i < $N; $i++) 
        for ($j = 0; $j < $N; $j++) 

            // condition to check 
            // other elements  
            // except main diagonal 
            // are zero or not. 
            if (($i != $j) &&  
                ($mat[$i][$j] != 0)) 
                return false; 
    return true; 
} 

    // Driver Code 
    $mat = array(array(4, 0, 0, 0), 
                 array(0, 7, 0, 0), 
                 array(0, 0, 5, 0), 
                 array(0, 0, 0, 1)); 

    if (isDiagonalMatrix($mat)) 
        echo "Yes" ,"\n"; 
    else
        echo "No","\n"; 

// This code is contributed by jit_t 
?> 

```

Output:

```
Yes

```

[**标量矩阵**](https://en.wikipedia.org/wiki/Diagonal_matrix#Scalar_matrix)：

如果所有主要对角线元素相等且除主要对角线以外的其他元素均为零，则称方阵为标量矩阵。 标量矩阵也可以`n * I`的形式编写，其中`n`是任何实数，而`I`是单位矩阵。

示例：

```
Input :
Mat[4][4] = {{4, 0, 0, 0},
             {0, 4, 0, 0},
             {0, 0, 4, 0},
             {0, 0, 0, 4}} 
Output : Yes

Mat[4][4] = {{4, 0, 0, 0},
             {0, 4, 0, 0},
             {0, 0, 1, 0},
             {0, 0, 0, 4}} 
Output : No

```

## CPP

```

// Program to check matrix is scalar matrix or not. 
#include <bits/stdc++.h> 
#define N 4 
using namespace std; 

// Function to check matrix is scalar matrix or not. 
bool isScalarMatrix(int mat[N][N]) 
{ 
    // Check all elements except main diagonal are 
    // zero or not. 
    for (int i = 0; i < N; i++) 
        for (int j = 0; j < N; j++) 
            if ((i != j) && (mat[i][j] != 0)) 
                return false; 

    // Check all diagonal elements are same or not. 
    for (int i = 0; i < N - 1; i++) 
        if (mat[i][i] != mat[i + 1][i + 1]) 
            return false; 
    return true; 
} 

// Driver function 
int main() 
{ 
    int mat[N][N] = { { 2, 0, 0, 0 }, 
                      { 0, 2, 0, 0 }, 
                      { 0, 0, 2, 0 }, 
                      { 0, 0, 0, 2 } }; 
    // Function call 
    if (isScalarMatrix(mat)) 
        cout << "Yes" << endl; 
    else
        cout << "No" << endl; 
    return 0; 
} 

```

## Java

```java

// Program to check matrix 
// is scalar matrix or not. 
import java.io.*; 

class GFG { 

    static int N = 4; 
    // Function to check matrix 
    // is scalar matrix or not. 
    static boolean isScalarMatrix(int mat[][]) 
    { 
        // Check all elements 
        // except main diagonal are 
        // zero or not. 
        for (int i = 0; i < N; i++) 
            for (int j = 0; j < N; j++) 
                if ((i != j) 
                  && (mat[i][j] != 0)) 
                    return false; 

        // Check all diagonal elements 
        // are same or not. 
        for (int i = 0; i < N - 1; i++) 
            if (mat[i][i] != mat[i + 1][i + 1]) 
                return false; 
        return true; 
    } 

    // Driver function 
    public static void main(String args[]) 
    { 
        int mat[ ][ ] = { { 2, 0, 0, 0 }, 
                          { 0, 2, 0, 0 }, 
                          { 0, 0, 2, 0 }, 
                          { 0, 0, 0, 2 } }; 
        // Function call 
        if (isScalarMatrix(mat)) 
            System.out.println("Yes"); 
        else
            System.out.println("No"); 
    } 
} 

// This code is contributed 
// by Nikita tiwari. 

```

## Python3

```py

# Program to check matrix 
# is scalar matrix or not. 

N = 4

# Function to check matrix is 
# scalar matrix or not. 
def isScalarMatrix(mat) : 

    # Check all elements  
    # except main diagonal are 
    # zero or not. 
    for i in range(0,N) : 
        for j in range(0,N) : 
            if ((i != j)  
               and (mat[i][j] != 0)) : 
                return False

    # Check all diagonal 
    # elements are same or not. 
    for i in range(0,N-1) : 
        if (mat[i][i] !=
           mat[i + 1][i + 1]) : 
            return False

    return True

# Driver function 
mat = [[ 2, 0, 0, 0 ], 
       [ 0, 2, 0, 0 ], 
       [ 0, 0, 2, 0 ], 
       [ 0, 0, 0, 2 ]] 

# Function call 
if (isScalarMatrix(mat)): 
    print("Yes") 
else : 
    print("No") 

# This code is contributed by 
# Nikita tiwari. 

```

## C#

```cs

// Program to check matrix 
// is scalar matrix or not. 
using System; 

class GFG { 

    static int N = 4; 

    // Function to check matrix 
    // is scalar matrix or not. 
    static bool isScalarMatrix(int [,]mat) 
    { 
        // Check all elements 
        // except main diagonal are 
        // zero or not. 
        for (int i = 0; i < N; i++) 
            for (int j = 0; j < N; j++) 
                if ((i != j) && (mat[i,j] != 0)) 
                    return false; 

        // Check all diagonal elements 
        // are same or not. 
        for (int i = 0; i < N - 1; i++) 
            if (mat[i, i] != mat[i + 1, i + 1]) 
                return false; 
        return true; 
    } 

    // Driver function 
    public static void Main() 
    { 
        int [,]mat = { { 2, 0, 0, 0 }, 
                        { 0, 2, 0, 0 }, 
                        { 0, 0, 2, 0 }, 
                        { 0, 0, 0, 2 } }; 
        // Function call 
        if (isScalarMatrix(mat)) 
            Console.WriteLine("Yes"); 
        else
            Console.WriteLine("No"); 
    } 
} 

// This code is contributed 
// by vt_m. 

```

## PHP

```php

<?php 
// Program to check matrix 
// is scalar matrix or not. 

$N = 4; 

// Function to check matrix  
// is scalar matrix or not. 
function isScalarMatrix($mat) 
{ 
    global $N; 
    // Check all elements except  
    // main diagonal are zero or not. 
    for ($i = 0; $i < $N; $i++) 
        for ($j = 0; $j < $N; $j++) 
            if (($i != $j) && 
                ($mat[$i][$j] != 0)) 
                return false; 

    // Check all diagonal elements  
    // are same or not. 
    for ($i = 0; $i < $N - 1; $i++) 
        if ($mat[$i][$i] != $mat[$i + 1][$i + 1]) 
            return false; 
    return true; 
} 

// Driver Code 
$mat = array(array(2, 0, 0, 0), 
             array(0, 2, 0, 0), 
             array(0, 0, 2, 0), 
             array(0, 0, 0, 2)); 

// Function call 
if (isScalarMatrix($mat)) 
    echo "Yes"; 
else
    echo "No" ; 

// This code is contributed by mits 
?> 

```

**输出**：

```
Yes

```



* * *

* * *



