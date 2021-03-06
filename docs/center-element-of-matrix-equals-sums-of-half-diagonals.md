# 矩阵中心元素等于半对角线总和

> 原文： [https://www.geeksforgeeks.org/center-element-of-matrix-equals-sums-of-half-diagonals/](https://www.geeksforgeeks.org/center-element-of-matrix-equals-sums-of-half-diagonals/)

给定一个奇数阶矩阵，即`5 * 5`。 任务是检查矩阵的中心元素是否等于所有半对角线的总和。

![](img/768ffc6b905c758cf406b1a20e4af7c5.png)

**示例**：

```
Input : mat[][] = {   2   9   1   4  -2
                      6   7   2  11   4
                      4    2  9   2   4
                      1   9   2    4  4
                      0   2   4    2  5 } 
Output :Yes
Explanation : 
Sum of Half Diagonal 1 = 2 + 7 = 9
Sum of Half Diagonal 2 = 9 + 0 = 9
Sum of Half Diagonal 3 = 11 + -2 = 9
Sum of Half Diagonal 4 = 5 + 4 = 9

Here, All the sums equal to the center element
that is mat[2][2] = 9

```



**简单方法**：

迭代两个循环，找到所有对角线总和，然后检查所有总和是否等于矩阵的中心元素。 如果其中任何一个不等于中心元素，则打印`No`，否则打印`Yes`。

时间复杂度：`O(N * N)`。

**有效方法**：基于[有效方法](https://www.geeksforgeeks.org/efficiently-compute-sums-of-diagonals-of-a-matrix/)在`O(n)`中找到对角线总和。

以下是此方法的实现：

## C++ 

```cpp

// C++ Program to check if the center 
// element is equal to the individual  
// sum of all the half diagonals 
#include <stdio.h> 
#include<bits/stdc++.h> 
using namespace std; 

const int MAX = 100; 

// Function to Check center element  
// is equal to the individual  
// sum of all the half diagonals 
bool HalfDiagonalSums(int mat[][MAX], int n) 
{     
    // Find sums of half diagonals 
    int diag1_left = 0, diag1_right = 0; 
    int diag2_left = 0, diag2_right = 0;     
    for (int i = 0, j = n - 1; i < n; i++, j--) { 

        if (i < n/2) { 
            diag1_left += mat[i][i]; 
            diag2_left += mat[j][i];            
        } 
        else if (i > n/2) { 
            diag1_right += mat[i][i]; 
            diag2_right += mat[j][i];            
        } 
    } 

    return (diag1_left == diag2_right &&  
            diag2_right == diag2_left && 
            diag1_right == diag2_left && 
            diag2_right == mat[n/2][n/2]); 
} 

// Driver code 
int main() 
{ 
    int a[][MAX] = { { 2, 9, 1, 4, -2}, 
                     { 6, 7, 2, 11, 4},  
                     { 4, 2, 9, 2, 4}, 
                     { 1, 9, 2, 4, 4}, 
                     { 0, 2, 4, 2, 5} }; 
        cout << ( HalfDiagonalSums(a, 5) ? "Yes" : "No" ); 
    return 0; 
} 

```

## Java

```java
// Java program to find maximum elements  
// that can be made equal with k updates 
import java.util.Arrays; 
public class GFG { 
      
    static int MAX = 100; 
      
    // Function to Check center element  
    // is equal to the individual  
    // sum of all the half diagonals 
    static boolean HalfDiagonalSums(int mat[][], 
                                          int n) 
    {  
          
        // Find sums of half diagonals 
        int diag1_left = 0, diag1_right = 0; 
        int diag2_left = 0, diag2_right = 0;  
        for (int i = 0, j = n - 1; i < n;  
                                    i++, j--) 
        { 
              
            if (i < n/2) { 
                diag1_left += mat[i][i]; 
                diag2_left += mat[j][i];          
            } 
            else if (i > n/2) { 
                diag1_right += mat[i][i]; 
                diag2_right += mat[j][i];          
            } 
        } 
          
        return (diag1_left == diag2_right &&  
                diag2_right == diag2_left && 
                diag1_right == diag2_left && 
                diag2_right == mat[n/2][n/2]); 
    } 
      
    // Driver code 
    public static void main(String args[])  
    { 
          
        int a[][] = { { 2, 9, 1, 4, -2}, 
                      { 6, 7, 2, 11, 4},  
                      { 4, 2, 9, 2, 4}, 
                      { 1, 9, 2, 4, 4}, 
                      { 0, 2, 4, 2, 5} }; 
                        
        System.out.print ( HalfDiagonalSums(a, 5) 
                                ? "Yes" : "No" ); 
    } 
} 
  
// This code is contributed by Sam007 
```

## Python 3

```py
# Python 3 Program to check if the center 
# element is equal to the individual  
# sum of all the half diagonals 
   
MAX = 100
   
# Function to Check center element  
# is equal to the individual  
# sum of all the half diagonals 
def HalfDiagonalSums( mat,  n): 
  
    # Find sums of half diagonals 
    diag1_left = 0
    diag1_right = 0
    diag2_left = 0
    diag2_right = 0  
    i = 0
    j = n - 1
    while i < n: 
           
        if (i < n//2) : 
            diag1_left += mat[i][i] 
            diag2_left += mat[j][i]            
          
        elif (i > n//2) : 
            diag1_right += mat[i][i] 
            diag2_right += mat[j][i]            
        i += 1
        j -= 1
       
    return (diag1_left == diag2_right and
            diag2_right == diag2_left and
            diag1_right == diag2_left and
            diag2_right == mat[n//2][n//2]) 
   
# Driver code 
if __name__ == "__main__": 
      
    a = [[2, 9, 1, 4, -2], 
         [6, 7, 2, 11, 4],  
         [ 4, 2, 9, 2, 4], 
         [1, 9, 2, 4, 4 ], 
         [ 0, 2, 4, 2, 5]] 
      
    print("Yes") if (HalfDiagonalSums(a, 5)) else print("No" ) 
```

## C#

```cs
// C# program to find maximum  
// elements that can be made  
// equal with k updates 
using System; 
  
class GFG 
{ 
  
    // Function to Check  
    // center element is 
    // equal to the individual  
    // sum of all the half  
    // diagonals 
    static bool HalfDiagonalSums(int [,]mat, 
                                 int n) 
    {  
          
        // Find sums of  
        // half diagonals 
        int diag1_left = 0,  
            diag1_right = 0; 
        int diag2_left = 0,  
            diag2_right = 0;  
        for (int i = 0, j = n - 1;  
                 i < n; i++, j--) 
        { 
              
            if (i < n / 2)  
            { 
                diag1_left += mat[i, i]; 
                diag2_left += mat[j, i];      
            } 
            else if (i > n / 2)  
            { 
                diag1_right += mat[i, i]; 
                diag2_right += mat[j, i];          
            } 
        } 
          
        return (diag1_left == diag2_right &&  
                diag2_right == diag2_left && 
                diag1_right == diag2_left && 
                diag2_right == mat[n / 2, n / 2]); 
    } 
      
    // Driver code 
    static public void Main () 
    { 
        int [,]a = {{ 2, 9, 1, 4, -2}, 
                    { 6, 7, 2, 11, 4},  
                    { 4, 2, 9, 2, 4}, 
                    { 1, 9, 2, 4, 4}, 
                    { 0, 2, 4, 2, 5}}; 
                      
        Console.WriteLine(HalfDiagonalSums(a, 5)?  
                                  "Yes" : "No" ); 
    } 
} 
  
// This code is contributed by ajit 
```

## PHP

```php
<?php 
// PHP Program to check if  
// the center element is  
// equal to the individual  
// sum of all the half diagonals 
$MAX = 100; 
  
// Function to Check center  
// element is equal to the  
// individual sum of all  
// the half diagonals 
function HalfDiagonalSums($mat, $n) 
{  
    global $MAX ; 
      
    // Find sums of  
    // half diagonals 
    $diag1_left = 1; $diag1_right = 1; 
    $diag2_left = 1; $diag2_right = 1;  
    for ($i = 0, $j = $n - 1;  
         $i < $n; $i++, $j--) 
    { 
          
        if ($i < $n / 2)  
        { 
            $diag1_left += $mat[$i][$i]; 
            $diag2_left += $mat[$j][$i];          
        } 
        else if ($i > $n / 2)  
        { 
            $diag1_right += $mat[$i][$i]; 
            $diag2_right += $mat[$j][$i];      
        } 
    } 
      
    return ($diag1_left == $diag2_right &&  
            $diag2_right == $diag2_left && 
            $diag1_right == $diag2_left && 
            $diag2_right == $mat[$n / 2][$n / 2]); 
} 
  
// Driver code 
$a = array(array(2, 9, 1, 4, -2), 
           array(6, 7, 2, 11, 4),  
           array(4, 2, 9, 2, 4), 
           array(1, 9, 2, 4, 4), 
           array(0, 2, 4, 2, 5)); 
if(HalfDiagonalSums($a, 5) == 0) 
    echo "Yes" ; 
else
    echo "No" ; 
          
// This code is contributed 
// by akt_mit 
?> 
```

输出：

```
Yes
```

时间复杂度：`O(N)`。