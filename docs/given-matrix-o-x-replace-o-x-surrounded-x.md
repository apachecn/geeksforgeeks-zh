# 给定矩阵`O`和`X`，如果被`X`包围，则将`O`替换为`X`

> 原文： [https://www.geeksforgeeks.org/given-matrix-o-x-replace-o-x-surrounded-x/](https://www.geeksforgeeks.org/given-matrix-o-x-replace-o-x-surrounded-x/)

给定一个矩阵，其中每个元素均为`O`或`X`，如果被`X`包围，则将`O`替换为`X`。 如果`O`（或一组`O`）在其下方，上方，左侧和右侧的位置带有`X`，则被`X`包围。

**示例**：

```
Input: mat[M][N] =  {{'X', 'O', 'X', 'X', 'X', 'X'},
                     {'X', 'O', 'X', 'X', 'O', 'X'},
                     {'X', 'X', 'X', 'O', 'O', 'X'},
                     {'O', 'X', 'X', 'X', 'X', 'X'},
                     {'X', 'X', 'X', 'O', 'X', 'O'},
                     {'O', 'O', 'X', 'O', 'O', 'O'},
                    };
Output: mat[M][N] =  {{'X', 'O', 'X', 'X', 'X', 'X'},
                      {'X', 'O', 'X', 'X', 'X', 'X'},
                      {'X', 'X', 'X', 'X', 'X', 'X'},
                      {'O', 'X', 'X', 'X', 'X', 'X'},
                      {'X', 'X', 'X', 'O', 'X', 'O'},
                      {'O', 'O', 'X', 'O', 'O', 'O'},
                    };

```

```
Input: mat[M][N] =  {{'X', 'X', 'X', 'X'}
                     {'X', 'O', 'X', 'X'}
                     {'X', 'O', 'O', 'X'}
                     {'X', 'O', 'X', 'X'}
                     {'X', 'X', 'O', 'O'}
                    };
```

```
Input: mat[M][N] =  {{'X', 'X', 'X', 'X'}
                     {'X', 'X', 'X', 'X'}
                     {'X', 'X', 'X', 'X'}
                     {'X', 'X', 'X', 'X'}
                     {'X', 'X', 'O', 'O'}
                    };
```



这主要是 [Flood-Fill 算法](https://www.geeksforgeeks.org/flood-fill-algorithm-implement-fill-paint/)的应用。 这里的主要区别在于，如果`O`位于以边界结尾的区域中，则不会将其替换为`X`。 以下是执行此特殊洪水填充的简单步骤。

1.  遍历给定的矩阵，并将所有的`O`替换为特殊字符`-`。

2.  遍历给定矩阵的四个边缘，并为边缘上的每个`-`调用[`floodFill('-', 'O')`](https://www.geeksforgeeks.org/flood-fill-algorithm-implement-fill-paint/)。 其余的`-`是表示要用`X`替换的`O`（在原始矩阵中）的字符。

3.  遍历矩阵并将所有的`-`替换为`X`。

 **让我们以示例的形式查看上述算法的步骤。** 令以下为输入矩阵。

```
       mat[M][N] =  {{'X', 'O', 'X', 'X', 'X', 'X'},
                     {'X', 'O', 'X', 'X', 'O', 'X'},
                     {'X', 'X', 'X', 'O', 'O', 'X'},
                     {'O', 'X', 'X', 'X', 'X', 'X'},
                     {'X', 'X', 'X', 'O', 'X', 'O'},
                     {'O', 'O', 'X', 'O', 'O', 'O'},
                    };
```

**步骤 1**：将所有`O`替换为`-`。

```
       mat[M][N] =  {{'X', '-', 'X', 'X', 'X', 'X'},
                     {'X', '-', 'X', 'X', '-', 'X'},
                     {'X', 'X', 'X', '-', '-', 'X'},
                     {'-', 'X', 'X', 'X', 'X', 'X'},
                     {'X', 'X', 'X', '-', 'X', '-'},
                     {'-', '-', 'X', '-', '-', '-'},
                    };
```

**步骤 2**：为所有等于'-'的边缘元素调用`FloodFill('-', 'O')`。

```
       mat[M][N] =  {{'X', 'O', 'X', 'X', 'X', 'X'},
                     {'X', 'O', 'X', 'X', '-', 'X'},
                     {'X', 'X', 'X', '-', '-', 'X'},
                     {'O', 'X', 'X', 'X', 'X', 'X'},
                     {'X', 'X', 'X', 'O', 'X', 'O'},
                     {'O', 'O', 'X', 'O', 'O', 'O'},
                    };
```

**步骤 3**：将所有的`-`替换为`X`。

```
       mat[M][N] =  {{'X', 'O', 'X', 'X', 'X', 'X'},
                     {'X', 'O', 'X', 'X', 'X', 'X'},
                     {'X', 'X', 'X', 'X', 'X', 'X'},
                     {'O', 'X', 'X', 'X', 'X', 'X'},
                     {'X', 'X', 'X', 'O', 'X', 'O'},
                     {'O', 'O', 'X', 'O', 'O', 'O'},
                    };
```

以下是上述算法的实现。

## C++ 

```cpp

// A C++ program to replace all 'O's with 'X''s if surrounded by 'X' 
#include<iostream> 
using namespace std; 

// Size of given matrix is M X N 
#define M 6 
#define N 6 

// A recursive function to replace previous value 'prevV' at  '(x, y)' 
// and all surrounding values of (x, y) with new value 'newV'. 
void floodFillUtil(char mat[][N], int x, int y, char prevV, char newV) 
{ 
    // Base cases 
    if (x < 0 || x >= M || y < 0 || y >= N) 
        return; 
    if (mat[x][y] != prevV) 
        return; 

    // Replace the color at (x, y) 
    mat[x][y] = newV; 

    // Recur for north, east, south and west 
    floodFillUtil(mat, x+1, y, prevV, newV); 
    floodFillUtil(mat, x-1, y, prevV, newV); 
    floodFillUtil(mat, x, y+1, prevV, newV); 
    floodFillUtil(mat, x, y-1, prevV, newV); 
} 

// Returns size of maximum size subsquare matrix 
// surrounded by 'X' 
int replaceSurrounded(char mat[][N]) 
{ 
   // Step 1: Replace all 'O'  with '-' 
   for (int i=0; i<M; i++) 
      for (int j=0; j<N; j++) 
          if (mat[i][j] == 'O') 
             mat[i][j] = '-'; 

   // Call floodFill for all '-' lying on edges 
   for (int i=0; i<M; i++)   // Left side 
      if (mat[i][0] == '-') 
        floodFillUtil(mat, i, 0, '-', 'O'); 
   for (int i=0; i<M; i++)  //  Right side 
      if (mat[i][N-1] == '-') 
        floodFillUtil(mat, i, N-1, '-', 'O'); 
   for (int i=0; i<N; i++)   // Top side 
      if (mat[0][i] == '-') 
        floodFillUtil(mat, 0, i, '-', 'O'); 
   for (int i=0; i<N; i++)  // Bottom side 
      if (mat[M-1][i] == '-') 
        floodFillUtil(mat, M-1, i, '-', 'O'); 

   // Step 3: Replace all '-' with 'X' 
   for (int i=0; i<M; i++) 
      for (int j=0; j<N; j++) 
         if (mat[i][j] == '-') 
             mat[i][j] = 'X'; 

} 

// Driver program to test above function 
int main() 
{ 
    char mat[][N] =  {{'X', 'O', 'X', 'O', 'X', 'X'}, 
                     {'X', 'O', 'X', 'X', 'O', 'X'}, 
                     {'X', 'X', 'X', 'O', 'X', 'X'}, 
                     {'O', 'X', 'X', 'X', 'X', 'X'}, 
                     {'X', 'X', 'X', 'O', 'X', 'O'}, 
                     {'O', 'O', 'X', 'O', 'O', 'O'}, 
                    }; 
    replaceSurrounded(mat); 

    for (int i=0; i<M; i++) 
    { 
      for (int j=0; j<N; j++) 
          cout << mat[i][j] << " "; 
      cout << endl; 
    } 
    return 0; 
} 

```

## Java

```java

// A Java program to replace  
// all 'O's with 'X''s if  
// surrounded by 'X' 
import java.io.*; 

class GFG 
{ 
    static int M = 6; 
    static int N = 6; 
    static void floodFillUtil(char mat[][], int x,  
                              int y, char prevV,  
                              char newV) 
    { 
        // Base cases 
        if (x < 0 || x >= M || 
            y < 0 || y >= N) 
            return; 

        if (mat[x][y] != prevV) 
            return; 

        // Replace the color at (x, y) 
        mat[x][y] = newV; 

        // Recur for north, 
        // east, south and west 
        floodFillUtil(mat, x + 1, y,  
                      prevV, newV); 
        floodFillUtil(mat, x - 1, y,  
                      prevV, newV); 
        floodFillUtil(mat, x, y + 1,  
                      prevV, newV); 
        floodFillUtil(mat, x, y - 1,  
                      prevV, newV); 
    } 

    // Returns size of maximum  
    // size subsquare matrix 
    // surrounded by 'X' 
    static void replaceSurrounded(char mat[][]) 
    { 

    // Step 1: Replace  
    // all 'O' with '-' 
    for (int i = 0; i < M; i++) 
        for (int j = 0; j < N; j++) 
            if (mat[i][j] == 'O') 
                mat[i][j] = '-'; 

    // Call floodFill for  
    // all '-' lying on edges 
    for (int i = 0; i < M; i++) // Left side 
        if (mat[i][0] == '-') 
            floodFillUtil(mat, i, 0,  
                          '-', 'O'); 
    for (int i = 0; i < M; i++) // Right side 
        if (mat[i][N - 1] == '-') 
            floodFillUtil(mat, i, N - 1, 
                          '-', 'O'); 
    for (int i = 0; i < N; i++) // Top side 
        if (mat[0][i] == '-') 
            floodFillUtil(mat, 0, i, 
                          '-', 'O'); 
    for (int i = 0; i < N; i++) // Bottom side 
        if (mat[M - 1][i] == '-') 
            floodFillUtil(mat, M - 1,  
                          i, '-', 'O'); 

    // Step 3: Replace  
    // all '-' with 'X' 
    for (int i = 0; i < M; i++) 
        for (int j = 0; j < N; j++) 
            if (mat[i][j] == '-') 
                mat[i][j] = 'X'; 
    } 

    // Driver Code 
    public static void main (String[] args) 
    { 
        char[][] mat = {{'X', 'O', 'X',  
                         'O', 'X', 'X'}, 
                        {'X', 'O', 'X',  
                         'X', 'O', 'X'}, 
                        {'X', 'X', 'X',  
                         'O', 'X', 'X'}, 
                        {'O', 'X', 'X', 
                         'X', 'X', 'X'}, 
                        {'X', 'X', 'X', 
                         'O', 'X', 'O'}, 
                        {'O', 'O', 'X', 
                         'O', 'O', 'O'}}; 

        replaceSurrounded(mat); 

        for (int i = 0; i < M; i++) 
        { 
            for (int j = 0; j < N; j++) 
                System.out.print(mat[i][j] + " ");  

            System.out.println(""); 
        } 
    } 
} 

// This code is contributed  
// by shiv_bhakt 

```

## C# 

```cs

// A C# program to replace  
// all 'O's with 'X''s if  
// surrounded by 'X' 
using System; 

class GFG 
{ 
    static int M = 6; 
    static int N = 6; 
    static void floodFillUtil(char [,]mat, int x,  
                              int y, char prevV,  
                              char newV) 
    { 
        // Base cases 
        if (x < 0 || x >= M || 
            y < 0 || y >= N) 
            return; 

        if (mat[x, y] != prevV) 
            return; 

        // Replace the color at (x, y) 
        mat[x, y] = newV; 

        // Recur for north, 
        // east, south and west 
        floodFillUtil(mat, x + 1, y,  
                       prevV, newV); 
        floodFillUtil(mat, x - 1, y,  
                       prevV, newV); 
        floodFillUtil(mat, x, y + 1,  
                       prevV, newV); 
        floodFillUtil(mat, x, y - 1,  
                       prevV, newV); 
    } 

    // Returns size of maximum  
    // size subsquare matrix 
    // surrounded by 'X' 
    static void replaceSurrounded(char [,]mat) 
    { 

    // Step 1: Replace  
    // all 'O' with '-' 
    for (int i = 0; i < M; i++) 
        for (int j = 0; j < N; j++) 
            if (mat[i, j] == 'O') 
                mat[i, j] = '-'; 

    // Call floodFill for  
    // all '-' lying on edges 
    for (int i = 0; i < M; i++) // Left side 
        if (mat[i, 0] == '-') 
            floodFillUtil(mat, i, 0,  
                          '-', 'O'); 
    for (int i = 0; i < M; i++) // Right side 
        if (mat[i, N - 1] == '-') 
            floodFillUtil(mat, i, N - 1, 
                          '-', 'O'); 
    for (int i = 0; i < N; i++) // Top side 
        if (mat[0, i] == '-') 
            floodFillUtil(mat, 0, i, 
                          '-', 'O'); 
    for (int i = 0; i < N; i++) // Bottom side 
        if (mat[M - 1, i] == '-') 
            floodFillUtil(mat, M - 1,  
                          i, '-', 'O'); 

    // Step 3: Replace  
    // all '-' with 'X' 
    for (int i = 0; i < M; i++) 
        for (int j = 0; j < N; j++) 
            if (mat[i, j] == '-') 
                mat[i, j] = 'X'; 
    } 

    // Driver Code 
    public static void Main () 
    { 
        char [,]mat = new char[,] 
                        {{'X', 'O', 'X',  
                          'O', 'X', 'X'}, 
                         {'X', 'O', 'X',  
                          'X', 'O', 'X'}, 
                         {'X', 'X', 'X',  
                          'O', 'X', 'X'}, 
                         {'O', 'X', 'X', 
                          'X', 'X', 'X'}, 
                         {'X', 'X', 'X', 
                          'O', 'X', 'O'}, 
                         {'O', 'O', 'X', 
                          'O', 'O', 'O'}}; 

        replaceSurrounded(mat); 

        for (int i = 0; i < M; i++) 
        { 
            for (int j = 0; j < N; j++) 
                Console.Write(mat[i, j] + " ");  

            Console.WriteLine(""); 
        } 
    } 
} 

// This code is contributed  
// by shiv_bhakt 

```

## PHP

```php

<?php  
// A PHP program to replace all  
// 'O's with 'X''s if surrounded by 'X' 

// Size of given  
// matrix is M X N 
$M = 6; 
$N = 6; 

// A recursive function to replace  
// previous value 'prevV' at '(x, y)' 
// and all surrounding values of  
// (x, y) with new value 'newV'. 
function floodFillUtil(&$mat, $x, $y,  
                        $prevV, $newV) 
{ 
    // Base cases 
    if ($x < 0 || $x >= $GLOBALS['M'] ||  
        $y < 0 || $y >= $GLOBALS['N']) 
        return; 
    if ($mat[$x][$y] != $prevV) 
        return; 

    // Replace the color at (x, y) 
    $mat[$x][$y] = $newV; 

    // Recur for north, 
    // east, south and west 
    floodFillUtil($mat, $x + 1, $y, $prevV, $newV); 
    floodFillUtil($mat, $x - 1, $y, $prevV, $newV); 
    floodFillUtil($mat, $x, $y + 1, $prevV, $newV); 
    floodFillUtil($mat, $x, $y - 1, $prevV, $newV); 
} 

// Returns size of maximum  
// size subsquare matrix 
// surrounded by 'X' 
function replaceSurrounded(&$mat) 
{ 

// Step 1: Replace all 'O' with '-' 
for ($i = 0; $i < $GLOBALS['M']; $i++) 
    for ($j = 0; $j < $GLOBALS['N']; $j++) 
        if ($mat[$i][$j] == 'O') 
            $mat[$i][$j] = '-'; 

// Call floodFill for all 
// '-' lying on edges 
for ($i = 0;  
     $i < $GLOBALS['M']; $i++) // Left side 
    if ($mat[$i][0] == '-') 
        floodFillUtil($mat, $i, 0, '-', 'O'); 

for ($i = 0; $i < $GLOBALS['M']; $i++) // Right side 
    if ($mat[$i][$GLOBALS['N'] - 1] == '-') 
        floodFillUtil($mat, $i, 
                      $GLOBALS['N'] - 1, '-', 'O'); 

for ($i = 0; $i < $GLOBALS['N']; $i++) // Top side 
    if ($mat[0][$i] == '-') 
        floodFillUtil($mat, 0, $i, '-', 'O'); 

for ($i = 0; $i < $GLOBALS['N']; $i++) // Bottom side 
    if ($mat[$GLOBALS['M'] - 1][$i] == '-') 
        floodFillUtil($mat, $GLOBALS['M'] - 1,  
                            $i, '-', 'O'); 

// Step 3: Replace all '-' with 'X' 
for ($i = 0; $i < $GLOBALS['M']; $i++) 
    for ($j = 0; $j < $GLOBALS['N']; $j++) 
        if ($mat[$i][$j] == '-') 
            $mat[$i][$j] = 'X'; 

} 

// Driver Code 
$mat = array(array('X', 'O', 'X', 'O', 'X', 'X'), 
             array('X', 'O', 'X', 'X', 'O', 'X'), 
             array('X', 'X', 'X', 'O', 'X', 'X'), 
             array('O', 'X', 'X', 'X', 'X', 'X'), 
             array('X', 'X', 'X', 'O', 'X', 'O'), 
             array('O', 'O', 'X', 'O', 'O', 'O')); 
replaceSurrounded($mat); 

for ($i = 0; $i < $GLOBALS['M']; $i++) 
{ 
    for ($j = 0; $j < $GLOBALS['N']; $j++) 
        echo $mat[$i][$j]." "; 
    echo "\n"; 
} 

// This code is contributed by ChitraNayal 
?> 

```

**输出**：

```
X O X O X X 
X O X X X X 
X X X X X X 
O X X X X X 
X X X O X O 
O O X O O O 
```

上述解决方案的时间复杂度为`O(MN)`。 请注意，矩阵的每个元素最多处理 3 次。

