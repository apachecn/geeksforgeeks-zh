# 返回扩展矩阵中的前一个元素

> 原文： [https://www.geeksforgeeks.org/return-previous-element-in-an-expanding-matrix/](https://www.geeksforgeeks.org/return-previous-element-in-an-expanding-matrix/)

我们有一个正方形矩阵，其大小连续扩大 2 倍。给定任意时间点在位置`(i, j)`处存在于矩阵中的序列，我们需要返回在位置`(i, (j + N - 1) % N)`，其中`N`是矩阵的大小。

当我们说矩阵正在扩展时，扩展矩阵是通过将原始`2 x 2`矩阵的每个元素与当前`N x N`矩阵本身相乘而形成的。 扩展矩阵的尺寸为`2N x 2N`。

```
For Instance, consider below 2x2 matrix,
  [a b]
  [c d]

Expanding it will result in a 4x4 matrix as follows:
ax[a b]  bx[a b]      [aa ab ba bb]
  [c d]    [c d]      [ac ad bc bd]
                  --> [ca cb da db]
cx[a b]  dx[a b]      [cc cd dc dd]
  [c d]    [c d]

Expanding it again results in an 8x8 matrix as follows, and so on.

ax[aa ab ba bb]   bx[aa ab ba bb]     [aaa aab aba abb baa bab bba bbb]
  [ac ad bc bd]     [ac ad bc bd]     [aac aad abc abd bac bad bbc bbd]
  [ca cb da db]     [ca cb da db]     [aca acb ada adb bca bcb bda bdb]
  [cc cd dc dd]     [cc cd dc dd]     [acc acd adc add bcc bcd bdc bdd]
                                  --> [caa cab cba cbb daa dab dba dbb]
cx[aa ab ba bb]   dx[aa ab ba bb]     [cac cad cbc cbd dac dad dbc dbd]
  [ac ad bc bd]     [ac ad bc bd]     [cca ccb cda cdb dca dcb dda ddb]
  [ca cb da db]     [ca cb da db]     [ccc ccd cdc cdd dcc dcd ddc ddd]
  [cc cd dc dd]     [cc cd dc dd]
```

基本上，对于给定的序列，我们需要找出刚剩下的序列。 可以假设矩阵是圆形的，即位置`(i, 0)`处的序列应返回位置`(i, N - 1)`处的序列。

**示例**：

```
Input: str = dda
Output: dcb

Input: str = cca
Output: ddb

Input: str = aacbddc
Output: aacbdcd  
```

**我们强烈建议您最小化浏览器，然后自己尝试。**

如果我们仔细分析，我们可以在这里看到一个模式。

**算法**：

我们从最右边的位置开始扫描字符串，并对每个字符执行以下操作–

1.  如果当前字符是`b`或`d`，则分别更改为`a`或`c`并返回字符串。

2.  如果当前字符是`a`或`c`，则分别将其更改为`b`或`d`，然后移至左侧的下一个字符。 对左下一个字符重复步骤 1。

## C++ 

```cpp

// C++ Program to return previous element in an expanding 
// matrix. 
#include <bits/stdc++.h> 
using namespace std; 

// Returns left of str in an expanding matrix of 
// a, b, c, and d. 
string findLeft(string str) 
{ 
    int n = str.length(); 

    // Start from rightmost position 
    while (n--) 
    { 
        // If the current character is 'b' or 'd', 
        // change to 'a' or 'c' respectively and 
        // break the loop 
        if (str[n] == 'd') 
        { 
            str[n] = 'c'; 
            break; 
        } 
        if (str[n] == 'b') 
        { 
            str[n] = 'a'; 
            break; 
        } 

        // If the current character is 'a' or 'c', 
        // change it to 'b' or 'd' respectively 
        if (str[n] == 'a') 
            str[n] = 'b'; 
        else if (str[n] == 'c') 
            str[n] = 'd'; 
    } 

    return str; 
} 

// driver program to test above method 
int main() 
{ 
    string str = "aacbddc"; 
    cout << "Left of " << str << " is "
         << findLeft(str); 
   return 0; 
} 

```

## Java

```java

// Java program to return previous element 
// in an expanding matrix 
import java.io.*; 

class GFG  
{ 
    // Returns left of str in an expanding matrix  
    // of a, b, c  and d. 
    static StringBuilder findLeft(StringBuilder str) 
    { 
        int n = str.length(); 

        // Start from rightmost position 
        while (n > 0) 
        { 
            n--; 

            // If the current character is b or d, 
            // change to a or c respectively and 
            // break the loop 
            if (str.charAt(n) == 'd') 
            { 
                str.setCharAt(n,'c'); 
                break; 
            } 
            if (str.charAt(n) == 'b') 
            { 
                str.setCharAt(n,'a'); 
                break; 
            } 

            // If the current character is a or c, 
            // change it to b or d respectively 
            if (str.charAt(n) == 'a') 
                str.setCharAt(n,'b'); 
            else if (str.charAt(n) == 'c') 
                str.setCharAt(n,'d'); 
        } 

        return str; 
    } 

    // driver program to test above method 
    public static void main (String[] args)  
    { 
        StringBuilder str = new StringBuilder("aacbddc"); 
        System.out.print("Left of " + str + " is " +  
                                    findLeft(str)); 
    } 
} 

// This code is contributed by Prakriti Gupta 

```

## Python3

```py

# Python3 Program to return previous element  
# in an expanding matrix. 

# Returns left of str in an  
# expanding matrix of a, b, c, and d. 
def findLeft(str): 
    n = len(str) - 1; 

    # Start from rightmost position 
    while (n > 0): 

        # If the current character is 'b' or 'd', 
        # change to 'a' or 'c' respectively and 
        # break the loop 
        if (str[n] == 'd'): 
            str = str[0:n] + 'c' + str[n + 1:]; 
            break; 

        if (str[n] == 'b'): 
            str = str[0:n] + 'a' + str[n + 1:]; 
            break; 

        # If the current character is 'a' or 'c', 
        # change it to 'b' or 'd' respectively 
        if (str[n] == 'a'): 
            str = str[0:n] + 'b' + str[n + 1:]; 
        elif (str[n] == 'c'): 
            str = str[0:n] + 'd' + str[n + 1:]; 
        n-=1; 

    return str; 

# Driver Code 
if __name__ == '__main__': 
    str = "aacbddc"; 
    print("Left of", str, "is", findLeft(str)); 

# This code is contributed by PrinciRaj1992 

```

## C# 

```cs

using System; 
using System.Text; 

// C# program to return previous element  
// in an expanding matrix  

public class GFG 
{ 
    // Returns left of str in an expanding matrix   
    // of a, b, c  and d.  
    public static StringBuilder findLeft(StringBuilder str) 
    { 
        int n = str.Length; 

        // Start from rightmost position  
        while (n > 0) 
        { 
            n--; 

            // If the current character is b or d,  
            // change to a or c respectively and  
            // break the loop  
            if (str[n] == 'd') 
            { 
                str[n] = 'c'; 
                break; 
            } 
            if (str[n] == 'b') 
            { 
                str[n] = 'a'; 
                break; 
            } 

            // If the current character is a or c,  
            // change it to b or d respectively  
            if (str[n] == 'a') 
            { 
                str[n] = 'b'; 
            } 
            else if (str[n] == 'c') 
            { 
                str[n] = 'd'; 
            } 
        } 

        return str; 
    } 

    // driver program to test above method  
    public static void Main(string[] args) 
    { 
        StringBuilder str = new StringBuilder("aacbddc"); 
        Console.Write("Left of " + str + " is " + findLeft(str)); 
    } 
} 

// This code is contributed by Shrikant13 

```

## PHP

```php

<?php  
// PHP program to return previous element in an expanding 
// matrix. 

// Returns left of str in an expanding matrix of 
// a, b, c  and d. 
function findLeft($str) 
{ 
    $n = strlen($str); 

    // Start from rightmost position 
    while ($n--) 
    { 
        // If the current character is 'b' or 'd', 
        // change to 'a' or 'c' respectively and 
        // break the loop 
        if ($str[$n] == 'd') 
        { 
            $str[$n] = 'c'; 
            break; 
        } 
        if ($str[$n] == 'b') 
        { 
            $str[$n] = 'a'; 
            break; 
        } 

        // If the current character is 'a' or 'c', 
        // change it to 'b' or 'd' respectively 
        if ($str[$n] == 'a') 
            $str[$n] = 'b'; 
        else if ($str[$n] == 'c') 
            $str[$n] = 'd'; 
    } 

    return $str; 
} 

// Driver Code 
$str = "aacbddc"; 
echo "Left of " . $str . " is "
         . findLeft($str); 
return 0; 
?> 

```

**输出**：

```
Left of aacbddc is aacbdcd
```

