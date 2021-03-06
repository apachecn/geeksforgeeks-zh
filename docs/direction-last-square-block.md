# 最后一个方块的方向

> 原文： [https://www.geeksforgeeks.org/direction-last-square-block/](https://www.geeksforgeeks.org/direction-last-square-block/)

给定`R x C`（`1 <= R`，`C <= 1000000000`）网格，初始位置为左上角，方向为东。 现在，我们开始向前移动并交叉矩阵的每个正方形块。 每当发现死角或到达已被访问的单元格时，我们就采取正确的态度，因为我们无法再次越过被访问的方块。 告诉方向我们什么时候将到达最后一个方块。

**例如**：考虑`R = 3`，`C = 3`的情况。遵循的路径将是`(0, 0)—(0, 1)—(0, 2)— (1, 2)-(2, 2)-(2, 1)-(2, 0)-(1, 0)-(1, 1)`。 至此，所有广场均已访问，并朝右。

**示例**：

```
Input  :  R = 1, C = 1
Output :  Right

Input   :  R = 2, C = 2
Output  :  Left

Input   :  R = 3, C = 1
Output  :  Down

Input  :  R = 3, C = 3
Output :  Right

```



**简单解决方案**：一个简单的解决方案是使`R x C`矩阵初始化为零，并以螺旋形式遍历它，并采用变量`Dir`指示当前方向 。 每当我们在任何行和列的末尾时，都请选择`"Right"`并根据您当前的方向更改`Dir`的值。 现在遵循给定条件：

*   如果您要遍历第一行，则当前方向为`"Right"`。

*   如果您是对的话，那么您当前的方向是`"Down"`。

*   如果您要遍历底行，则当前方向为`"Left"`。

*   如果您正在横穿左廊，那么您当前的方向是`"Up"`。

当我们到达最后一个方块时，只需打印当前方向即可； `Dir`变量的值。

此问题的时间和空间复杂度为`O(R x C)`，这仅适用于`R`，`C`的较小值，但这里`R`和`C`太大，因此无法针对太大的值创建`R x C`矩阵`R`和`C`。

**高效方法**：这种方法几乎不需要观察，并且需要一些笔纸工作。 在这里，我们必须考虑`R`和`C`的所有可能情况，然后只需要为所有可能情况设置`IF`条件。 在这里，我们具备所有可能的条件：

1.  `R != C`，`R`为偶数，`C`为奇数，`R < C`，方向为`"Left"`。

2.  `R != C`，`R`为奇数，`C`为偶数，`R < C`，方向为`"Right"`。

3.  `R != C`，`R`为偶数，`C`为偶数，`R < C`，方向为`"Left"`。

4.  `R != C`，`R`为奇数，`C`为奇数，`R < C` 方向为`"Right"`。

5.  `R != C`，`R`为偶数，`C`为奇数，`R > C`，方向为`"Down"`。

6.  `R != C`，`R`为奇数，`C`为偶数，`R > C`，方向为`"Up"`。

7.  `R != C`，`R`为偶数，`C`为偶数，`R > C`，方向为`"Up"`。

8.  `R != C`，`R`为奇数，`C`为奇数，`R > C`，方向为`"Down"`。

9.  `R == C`，`R`为偶数，`C`为偶数，方向为`"Left"`。

0.  `R == C`，`R`为奇数，`C`为奇数，方向为`"Right"`。

以下是上述想法的实现。

## C++ 

```cpp

// C++ program to tell the Current direction in 
// R x C grid 
#include <iostream> 
using namespace std; 
typedef long long int ll; 

// Function which tells the Current direction 
void direction(ll R, ll C) 
{ 
    if (R != C && R % 2 == 0 && C % 2 != 0 && R < C) { 
        cout << "Left" << endl; 
        return; 
    } 
    if (R != C && R % 2 != 0 && C % 2 == 0 && R > C) { 
        cout << "Up" << endl; 
        return; 
    } 
    if (R == C && R % 2 != 0 && C % 2 != 0) { 
        cout << "Right" << endl; 
        return; 
    } 
    if (R == C && R % 2 == 0 && C % 2 == 0) { 
        cout << "Left" << endl; 
        return; 
    } 
    if (R != C && R % 2 != 0 && C % 2 != 0 && R < C) { 
        cout << "Right" << endl; 
        return; 
    } 
    if (R != C && R % 2 != 0 && C % 2 != 0 && R > C) { 
        cout << "Down" << endl; 
        return; 
    } 
    if (R != C && R % 2 == 0 && C % 2 == 0 && R < C) { 
        cout << "Left" << endl; 
        return; 
    } 
    if (R != C && R % 2 == 0 && C % 2 == 0 && R > C) { 
        cout << "Up" << endl; 
        return; 
    } 
    if (R != C && R % 2 == 0 && C % 2 != 0 && R > C) { 
        cout << "Down" << endl; 
        return; 
    } 
    if (R != C && R % 2 != 0 && C % 2 == 0 && R < C) { 
        cout << "Right" << endl; 
        return; 
    } 
} 

// Driver program to test the Cases 
int main() 
{ 
    ll R = 3, C = 1; 
    direction(R, C); 
    return 0; 
} 

```

## Java

```java
// Java program to tell the Current direction in 
// R x C grid 
import java.io.*; 
  
class GFG { 
  
    // Function which tells the Current direction     
    static void direction(int R, int C) 
    { 
        if (R != C && R % 2 == 0 && C % 2 != 0 && R < C) { 
            System.out.println("Left"); 
            return; 
        } 
        if (R != C && R % 2 != 0 && C % 2 == 0 && R > C) { 
            System.out.println("Up"); 
            return; 
        } 
        if (R == C && R % 2 != 0 && C % 2 != 0) { 
            System.out.println("Right"); 
            return; 
        } 
        if (R == C && R % 2 == 0 && C % 2 == 0) { 
            System.out.println("Left"); 
            return; 
        } 
        if (R != C && R % 2 != 0 && C % 2 != 0 && R < C) { 
            System.out.println("Right"); 
            return; 
        } 
        if (R != C && R % 2 != 0 && C % 2 != 0 && R > C) { 
            System.out.println("Down"); 
            return; 
        } 
        if (R != C && R % 2 == 0 && C % 2 == 0 && R < C) { 
            System.out.println("Left"); 
            return; 
        } 
        if (R != C && R % 2 == 0 && C % 2 == 0 && R > C) { 
            System.out.println("Up"); 
            return; 
        } 
        if (R != C && R % 2 == 0 && C % 2 != 0 && R > C) { 
            System.out.println("Down"); 
            return; 
        } 
        if (R != C && R % 2 != 0 && C % 2 == 0 && R < C) { 
            System.out.println("Right"); 
            return; 
        } 
    } 
  
    // Driver code 
    public static void main(String[] args) 
    { 
        int R = 3, C = 1; 
          
        direction(R, C); 
    } 
} 
  
// This code is contributed by KRV.
```

## Python3

```py
# Python3 program to tell the Current  
# direction in R x C grid 
  
# Function which tells the Current direction 
def direction(R, C): 
    if (R != C and R % 2 == 0 and
        C % 2 != 0 and R < C): 
        print("Left") 
        return
  
    if (R != C and R % 2 == 0 and 
        C % 2 == 0 and R > C): 
        print("Up") 
        return
  
    if R == C and R % 2 != 0 and C % 2 != 0: 
        print("Right") 
        return
  
    if R == C and R % 2 == 0 and C % 2 == 0: 
        print("Left") 
        return
  
    if (R != C and R % 2 != 0 and 
        C % 2 != 0 and R < C): 
        print("Right") 
        return
  
    if (R != C and R % 2 != 0 and 
        C % 2 != 0 and R > C): 
        print("Down") 
        return
  
    if (R != C and R % 2 == 0 and 
        C % 2 != 0 and R < C): 
        print("Left") 
        return
  
    if (R != C and R % 2 == 0 and 
        C % 2 == 0 and R > C): 
        print("Up") 
        return
  
    if (R != C and R % 2 != 0 and 
        C % 2 != 0 and R > C): 
        print("Down") 
        return
  
    if (R != C and R % 2 != 0 and 
        C % 2 != 0 and R < C): 
        print("Right") 
        return
  
# Driver code 
R = 3; C = 1
direction(R, C) 
  
# This code is contributed by Shrikant13
```

## C#

```cs
// C# program to tell the Current 
// direction in R x C grid 
using System; 
  
class GFG 
{ 
      
    // Function which tells  
    // the Current direction  
    static void direction(int R, int C) 
    { 
        if (R != C && R % 2 == 0 &&  
            C % 2 != 0 && R < C)  
        { 
            Console.WriteLine("Left"); 
            return; 
        } 
        if (R != C && R % 2 != 0 &&  
            C % 2 == 0 && R > C)  
        { 
            Console.WriteLine("Up"); 
            return; 
        } 
        if (R == C && R % 2 != 0 &&  
            C % 2 != 0)  
        { 
            Console.WriteLine("Right"); 
            return; 
        } 
        if (R == C && R % 2 == 0 &&  
            C % 2 == 0)  
        { 
            Console.WriteLine("Left"); 
            return; 
        } 
        if (R != C && R % 2 != 0 && 
            C % 2 != 0 && R < C)  
        { 
            Console.WriteLine("Right"); 
            return; 
        } 
        if (R != C && R % 2 != 0 &&  
            C % 2 != 0 && R > C)  
        { 
            Console.WriteLine("Down"); 
            return; 
        } 
        if (R != C && R % 2 == 0 &&  
            C % 2 == 0 && R < C)  
        { 
            Console.WriteLine("Left"); 
            return; 
        } 
        if (R != C && R % 2 == 0 && 
            C % 2 == 0 && R > C)  
        { 
            Console.WriteLine("Up"); 
            return; 
        } 
        if (R != C && R % 2 == 0 &&  
            C % 2 != 0 && R > C)  
        { 
            Console.WriteLine("Down"); 
            return; 
        } 
        if (R != C && R % 2 != 0 &&  
            C % 2 == 0 && R < C)  
        { 
            Console.WriteLine("Right"); 
            return; 
        } 
    } 
  
    // Driver code 
    static public void Main () 
    { 
        int R = 3, C = 1; 
          
        direction(R, C); 
    } 
} 
  
// This code is contributed by m_kit
```

## PHP

```php
<?php 
// PHP program to tell the Current  
// direction in R x C grid 
  
// Function which tells 
// the Current direction 
function direction($R, $C) 
{ 
    if ($R != $C && $R % 2 == 0 &&  
                    $C % 2 != 0 && $R < $C)  
    { 
        echo "Left" ,"\n"; 
        return; 
    } 
    if ($R != $C && $R % 2 != 0 &&  
                    $C % 2 == 0 && $R > $C)  
    { 
        echo "Up" ,"\n"; 
        return; 
    } 
    if ($R == $C && $R % 2 != 0  
                 && $C % 2 != 0)  
    { 
        echo "Right" ,"\n"; 
        return; 
    } 
    if ($R == $C && $R % 2 == 0  
                 && $C % 2 == 0)  
    { 
        echo "Left" ,"\n"; 
        return; 
    } 
    if ($R != $C && $R % 2 != 0 &&  
                    $C % 2 != 0 && $R < $C)  
    { 
        echo "Right" ,"\n"; 
        return; 
    } 
    if ($R != $C && $R % 2 != 0 &&  
                    $C % 2 != 0 && $R > $C)  
    { 
        echo "Down" ,"\n"; 
        return; 
    } 
    if ($R != $C && $R % 2 == 0 &&  
                    $C % 2 == 0 && $R < $C)  
    { 
        echo "Left" ,"\n"; 
        return; 
    } 
    if ($R != $C && $R % 2 == 0 &&  
                    $C % 2 == 0 && $R > $C) 
    { 
        echo "Up" ,"\n"; 
        return; 
    } 
    if ($R != $C && $R % 2 == 0 &&  
                    $C % 2 != 0 && $R > $C)  
    { 
        echo "Down" ,"\n"; 
        return; 
    } 
    if ($R != $C && $R % 2 != 0 &&  
                    $C % 2 == 0 && $R < $C) 
    { 
        echo "Right" ,"\n"; 
        return; 
    } 
} 
  
// Driver Code 
$R = 3; $C = 1; 
direction($R, $C); 
  
// This code is contributed by aj_36 
?>
```

输出：

```
 Down
```

时间复杂度：`O(1)`。

辅助空间：`O(1)`。

参考：<http://www.spoj.com/problems/TRGRID/>。