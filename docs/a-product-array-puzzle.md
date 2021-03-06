# 乘积数组问题

> 原文： [https://www.geeksforgeeks.org/a-product-array-puzzle/](https://www.geeksforgeeks.org/a-product-array-puzzle/)

给定`n`个整数的数组`arr[]`，构造乘积数组`prod[]`（大小相同），以使`prod[i]`等于`arr[]`的所有元素（除`arr[i]`之外）的乘积。 在`O(n)`时间中解决不带除算符。

**示例**：

```
Input: arr[]  = {10, 3, 5, 6, 2}
Output: prod[]  = {180, 600, 360, 300, 900}
3 * 5 * 6 * 2 product of other array 
elements except 10 is 180
10 * 5 * 6 * 2 product of other array 
elements except 3 is 600
10 * 3 * 6 * 2 product of other array 
elements except 5 is 360
10 * 3 * 5 * 2 product of other array 
elements except 6 is 300
10 * 3 * 6 * 5 product of other array 
elements except 2 is 900

Input: arr[]  = {1, 2, 3, 4, 5}
Output: prod[]  = {120, 60, 40, 30, 24 }
2 * 3 * 4 * 5  product of other array 
elements except 1 is 120
1 * 3 * 4 * 5  product of other array 
elements except 2 is 60
1 * 2 * 4 * 5  product of other array 
elements except 3 is 40
1 * 2 * 3 * 5  product of other array 
elements except 4 is 30
1 * 2 * 3 * 4  product of other array 
elements except 5 is 24

```



**朴素的解决方案**：

**方法**：创建两个额外的空间，即两个额外的数组以存储从开始到索引的所有数组元素的乘积，另一个数组则存储从数组末尾开始的所有数组元素的乘积。 该索引的数组。

要获得不包含该索引的乘积，请将前缀乘积（直到索引`i-1`）乘以后缀乘积（直到索引`i + 1`）。

**算法**：

1.  创建两个长度为`n`的数组`prefix`和`subfix`，即原始数组的长度，初始化`prefix[0] = 1`和*`subfix[n-1] = 1`，以及另一个用于存储乘积的数组。

2.  从第二个索引到结束遍历数组。

3.  对于每个索引`i`，将`prefix[i]`更新为`prefix[i] = prefix[i-1] * array[i-1]`，即存储从数组开始到`i - 1`索引的乘积。

4.  从倒数第二个索引开始遍历数组。

5.  对于每个索引`i`，将`subfix[i]`更新为`subfix[i] = subfix[i + 1] * array[i + 1]`，即存储从数组末尾开始直到`i + 1`索引的乘积。

6.  从头到尾遍历数组。

7.  对于每个索引`i`，输出将为`prefix[i] *subfix[i]`，即该元素之外的数组元素的乘积。

## C++ 

```cpp

// C++ implementation of above approach 
#include <bits/stdc++.h> 
using namespace std; 

/* Function to print product array  
for a given array arr[] of size n */
void productArray(int arr[], int n) 
{ 

    // Base case 
    if (n == 1) { 
        cout << 0; 
        return; 
    } 
    /* Allocate memory for temporary  
arrays left[] and right[] */
    int* left = new int[sizeof(int) * n]; 
    int* right = new int[sizeof(int) * n]; 

    /* Allocate memory for the product array */
    int* prod = new int[sizeof(int) * n]; 

    int i, j; 

    /* Left most element of left  
array is always 1 */
    left[0] = 1; 

    /* Rightmost most element of right  
array is always 1 */
    right[n - 1] = 1; 

    /* Construct the left array */
    for (i = 1; i < n; i++) 
        left[i] = arr[i - 1] * left[i - 1]; 

    /* Construct the right array */
    for (j = n - 2; j >= 0; j--) 
        right[j] = arr[j + 1] * right[j + 1]; 

    /* Construct the product array using  
        left[] and right[] */
    for (i = 0; i < n; i++) 
        prod[i] = left[i] * right[i]; 

    /* print the constructed prod array */
    for (i = 0; i < n; i++) 
        cout << prod[i] << " "; 

    return; 
} 

/* Driver code*/
int main() 
{ 
    int arr[] = { 10, 3, 5, 6, 2 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    cout << "The product array is: \n"; 
    productArray(arr, n); 
} 

// This is code is contributed by rathbhupendra 

```

## C

```c

#include <stdio.h> 
#include <stdlib.h> 

/* Function to print product array  
for a given array arr[] of size n */
void productArray(int arr[], int n) 
{ 

    // Base case 
    if (n == 1) { 
        printf("0"); 
        return; 
    } 

    /* Allocate memory for temporary  
arrays left[] and right[] */
    int* left = (int*)malloc( 
        sizeof(int) * n); 
    int* right = (int*)malloc( 
        sizeof(int) * n); 

    /* Allocate memory for the product array */
    int* prod = (int*)malloc( 
        sizeof(int) * n); 

    int i, j; 

    /* Left most element of left array  
is always 1 */
    left[0] = 1; 

    /* Rightmost most element of right  
array is always 1 */
    right[n - 1] = 1; 

    /* Construct the left array */
    for (i = 1; i < n; i++) 
        left[i] = arr[i - 1] * left[i - 1]; 

    /* Construct the right array */
    for (j = n - 2; j >= 0; j--) 
        right[j] = arr[j + 1] * right[j + 1]; 

    /* Construct the product array using  
    left[] and right[] */
    for (i = 0; i < n; i++) 
        prod[i] = left[i] * right[i]; 

    /* print the constructed prod array */
    for (i = 0; i < n; i++) 
        printf("%d ", prod[i]); 

    return; 
} 

/* Driver program to test above functions */
int main() 
{ 
    int arr[] = { 10, 3, 5, 6, 2 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    printf("The product array is: \n"); 
    productArray(arr, n); 
    getchar(); 
} 

```

## Java

```java

class ProductArray { 
    /* Function to print product array  
    for a given array arr[] of size n */
    void productArray(int arr[], int n) 
    { 

        // Base case 
        if (n == 1) { 
            System.out.print(0); 
            return; 
        } 
        // Initialize memory to all arrays 
        int left[] = new int[n]; 
        int right[] = new int[n]; 
        int prod[] = new int[n]; 

        int i, j; 

        /* Left most element of left array  
is always 1 */
        left[0] = 1; 

        /* Rightmost most element of right  
array is always 1 */
        right[n - 1] = 1; 

        /* Construct the left array */
        for (i = 1; i < n; i++) 
            left[i] = arr[i - 1] * left[i - 1]; 

        /* Construct the right array */
        for (j = n - 2; j >= 0; j--) 
            right[j] = arr[j + 1] * right[j + 1]; 

        /* Construct the product array using  
        left[] and right[] */
        for (i = 0; i < n; i++) 
            prod[i] = left[i] * right[i]; 

        /* print the constructed prod array */
        for (i = 0; i < n; i++) 
            System.out.print(prod[i] + " "); 

        return; 
    } 

    /* Driver program to test the aboe function */
    public static void main(String[] args) 
    { 
        ProductArray pa = new ProductArray(); 
        int arr[] = { 10, 3, 5, 6, 2 }; 
        int n = arr.length; 
        System.out.println("The product array is : "); 
        pa.productArray(arr, n); 
    } 
} 

// This code has been contributed by Mayank Jaiswal 

```

## Python3

```py

# Python implementation of the above approach  

# Function to print product array for a given array  
# arr[] of size n  

def productArray(arr, n):  

    # Base case 
    if(n == 1): 
        print(0) 
        return

    # Allocate memory for temporary arrays left[] and right[]  
    left = [0]*n  
    right = [0]*n  

    # Allocate memory for the product array  
    prod = [0]*n  

    # Left most element of left array is always 1  
    left[0] = 1

    # Rightmost most element of right array is always 1  
    right[n - 1] = 1

    # Construct the left array  
    for i in range(1, n):  
        left[i] = arr[i - 1] * left[i - 1]  

    # Construct the right array  
    for j in range(n-2, -1, -1):  
        right[j] = arr[j + 1] * right[j + 1]  

    # Construct the product array using  
    # left[] and right[]  
    for i in range(n):  
        prod[i] = left[i] * right[i]  

    # print the constructed prod array  
    for i in range(n):  
        print(prod[i], end =' ')  

# Driver code  
arr = [10, 3, 5, 6, 2]  
n = len(arr)  
print("The product array is:")  
productArray(arr, n)  

# This code is contributed by ankush_953  

```

## C# 

```cs

using System; 

class GFG { 

    /* Function to print product array  
    for a given array arr[] of size n */
    static void productArray(int[] arr, int n) 
    { 

        // Base case 
        if (n == 1) { 
            Console.Write(0); 
            return; 
        } 
        // Initialize memory to all arrays 
        int[] left = new int[n]; 
        int[] right = new int[n]; 
        int[] prod = new int[n]; 

        int i, j; 

        /* Left most element of left array  
        is always 1 */
        left[0] = 1; 

        /* Rightmost most element of right  
        array is always 1 */
        right[n - 1] = 1; 

        /* Construct the left array */
        for (i = 1; i < n; i++) 
            left[i] = arr[i - 1] * left[i - 1]; 

        /* Construct the right array */
        for (j = n - 2; j >= 0; j--) 
            right[j] = arr[j + 1] * right[j + 1]; 

        /* Construct the product array using  
        left[] and right[] */
        for (i = 0; i < n; i++) 
            prod[i] = left[i] * right[i]; 

        /* print the constructed prod array */
        for (i = 0; i < n; i++) 
            Console.Write(prod[i] + " "); 

        return; 
    } 

    /* Driver program to test the aboe function */
    public static void Main() 
    { 
        int[] arr = { 10, 3, 5, 6, 2 }; 
        int n = arr.Length; 
        Console.Write("The product array is :\n"); 

        productArray(arr, n); 
    } 
} 

// This code is contributed by nitin mittal. 

```

## PHP

```php

<?php  
// Function to print product  
// array for a given array  
// arr[] of size n  
function productArray($arr, $n)  
{  

    // Base case 
    if($n == 1) { 
        echo "0"; 
        return; 
    } 
    // Initialize memory  
    // to all arrays  
    $left = array();  
    $right = array();  
    $prod = array();  

    $i; $j;  

    // Left most element of  
    // left array is always 1  
    $left[0] = 1;  

    // Rightmost most element of  
    // right array is always 1  
    $right[$n - 1] = 1;  

    // Construct the left array  
    for ($i = 1; $i < $n; $i++)  
        $left[$i] = $arr[$i - 1] *  
                    $left[$i - 1];  

    // Construct the right array  
    for ($j = $n - 2; $j >= 0; $j--)  
        $right[$j] = $arr[$j + 1] *  
                    $right[$j + 1];  

    // Construct the product array  
    // using left[] and right[]  
    for ($i = 0; $i < $n; $i++)  
        $prod[$i] = $left[$i] *  
                    $right[$i];  

    // print the constructed prod array  
    for ($i = 0; $i < $n; $i++)  
        echo $prod[$i], " ";  

    return;  
}  

// Driver Code  
$arr = array(10, 3, 5, 6, 2);  
$n = count($arr);  
echo "The product array is : \n";  
productArray($arr, $n);  

// This code has been contributed by anuj_67.  
?>  

```

**输出**：

```
The product array is : 
180 600 360 300 900 

```

**复杂度分析**：

*   **时间复杂度**：`O(n)`。

    数组需要遍历 3 次，因此时间复杂度为`O(n)`。

*   **空间复杂度**：`O(n)`。

    需要两个额外的数组和一个用于存储输出的数组，因此空间复杂度为`O(n)`。

**注意**：可以优化上述方法以在空间复杂度`O(1)`中工作。 感谢 Dileep 提供以下解决方案。

**有效解决方案**：

**方法**：在先前的解决方案中，创建了两个额外的数组来存储前缀和后缀，在此解决方案中，将前缀和后缀乘积存储在输出数组（或乘积数组）本身中。 从而减少了所需的空间。

**算法**：

1.  创建一个数组`prod`，并将其值初始化为 1，并将变量`temp = 1`。

2.  从头到尾遍历数组。

3.  对于每个索引`i`，将`prod[i]`更新为`prod[i] = temp`和`temp = temp * array[i]`， 即从数组开始将产品存储到`i - 1`索引。

4.  初始化`temp = 1`并从最后一个索引开始遍历数组。

5.  对于每个索引`i`，将`prod[i]`更新为`prod[i] = prod[i] * temp`和`temp = temp * array[i]`，即乘以从数组末尾到`i + 1`索引的乘积。

6.  打印乘积数组。

## C++

```cpp

// C++ implementation of above approach 
#include <bits/stdc++.h> 
using namespace std; 

/* Function to print product array  
for a given array arr[] of size n */
void productArray(int arr[], int n) 
{ 

    // Base case 
    if (n == 1) { 
        cout << 0; 
        return; 
    } 

    int i, temp = 1; 

    /* Allocate memory for the product array */
    int* prod = new int[(sizeof(int) * n)]; 

    /* Initialize the product array as 1 */
    memset(prod, 1, n); 

    /* In this loop, temp variable contains product of  
       elements on left side excluding arr[i] */
    for (i = 0; i < n; i++) { 
        prod[i] = temp; 
        temp *= arr[i]; 
    } 

    /* Initialize temp to 1  
    for product on right side */
    temp = 1; 

    /* In this loop, temp variable contains product of  
       elements on right side excluding arr[i] */
    for (i = n - 1; i >= 0; i--) { 
        prod[i] *= temp; 
        temp *= arr[i]; 
    } 

    /* print the constructed prod array */
    for (i = 0; i < n; i++) 
        cout << prod[i] << " "; 

    return; 
} 

// Driver Code 
int main() 
{ 
    int arr[] = { 10, 3, 5, 6, 2 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    cout << "The product array is: \n"; 
    productArray(arr, n); 
} 

// This code is contributed by rathbhupendra 

```

## Java

```java

class ProductArray { 
    void productArray(int arr[], int n) 
    { 

        // Base case 
        if (n == 1) { 
            System.out.print("0"); 
            return; 
        } 

        int i, temp = 1; 

        /* Allocate memory for the product array */
        int prod[] = new int[n]; 

        /* Initialize the product array as 1 */
        for (int j = 0; j < n; j++) 
            prod[j] = 1; 

        /* In this loop, temp variable contains product of 
           elements on left side excluding arr[i] */
        for (i = 0; i < n; i++) { 
            prod[i] = temp; 
            temp *= arr[i]; 
        } 

        /* Initialize temp to 1 for product on right side */
        temp = 1; 

        /* In this loop, temp variable contains product of 
           elements on right side excluding arr[i] */
        for (i = n - 1; i >= 0; i--) { 
            prod[i] *= temp; 
            temp *= arr[i]; 
        } 

        /* print the constructed prod array */
        for (i = 0; i < n; i++) 
            System.out.print(prod[i] + " "); 

        return; 
    } 

    /* Driver program to test above functions */
    public static void main(String[] args) 
    { 
        ProductArray pa = new ProductArray(); 
        int arr[] = { 10, 3, 5, 6, 2 }; 
        int n = arr.length; 
        System.out.println("The product array is : "); 
        pa.productArray(arr, n); 
    } 
} 

// This code has been contributed by Mayank Jaiswal 

```

## Python3

```py

# Python3 program for A Product Array Puzzle 
def productArray(arr, n): 

    # Base case 
    if n == 1: 
        print(0) 
        return

    i, temp = 1, 1

    # Allocate memory for the product array  
    prod = [1 for i in range(n)] 

    # Initialize the product array as 1  

    # In this loop, temp variable contains product of 
    # elements on left side excluding arr[i]  
    for i in range(n): 
        prod[i] = temp 
        temp *= arr[i] 

    # Initialize temp to 1 for product on right side  
    temp = 1

    # In this loop, temp variable contains product of 
    # elements on right side excluding arr[i]  
    for i in range(n - 1, -1, -1): 
        prod[i] *= temp 
        temp *= arr[i] 

    # Print the constructed prod array  
    for i in range(n): 
        print(prod[i], end = " ") 

    return

# Driver Code 
arr = [10, 3, 5, 6, 2] 
n = len(arr) 
print("The product array is: n") 
productArray(arr, n) 

# This code is contributed by mohit kumar 

```

## C#

```cs

using System; 

class GFG { 

    static void productArray(int[] arr, int n) 
    { 

        // Base case 
        if (n == 1) { 
            Console.Write(0); 
            return; 
        } 
        int i, temp = 1; 

        /* Allocate memory for the product 
        array */
        int[] prod = new int[n]; 

        /* Initialize the product array as 1 */
        for (int j = 0; j < n; j++) 
            prod[j] = 1; 

        /* In this loop, temp variable contains 
        product of elements on left side 
        excluding arr[i] */
        for (i = 0; i < n; i++) { 
            prod[i] = temp; 
            temp *= arr[i]; 
        } 

        /* Initialize temp to 1 for product on  
        right side */
        temp = 1; 

        /* In this loop, temp variable contains 
        product of elements on right side  
        excluding arr[i] */
        for (i = n - 1; i >= 0; i--) { 
            prod[i] *= temp; 
            temp *= arr[i]; 
        } 

        /* print the constructed prod array */
        for (i = 0; i < n; i++) 
            Console.Write(prod[i] + " "); 

        return; 
    } 

    /* Driver program to test above functions */
    public static void Main() 
    { 
        int[] arr = { 10, 3, 5, 6, 2 }; 
        int n = arr.Length; 
        Console.WriteLine("The product array is : "); 

        productArray(arr, n); 
    } 
} 

// This code is contributed by nitin mittal. 

```

## PHP

```php

<?php 
// PHP program for  
// A Product Array Puzzle 

function productArray($arr, $n)  
    { 

        // Base case 
        if ($n == 1) { 
            echo "0"; 
            return; 
        } 
        $i; $temp = 1; 

        /* Allocate memory for  
           the productarray */
        $prod = array(); 

        /* Initialize the product  
           array as 1 */
        for( $j = 0; $j < $n; $j++) 
            $prod[$j] = 1; 

        /* In this loop, temp  
           variable contains 
           product of elements 
           on left side 
           excluding arr[i] */
        for ($i = 0; $i < $n; $i++)  
        { 
            $prod[$i] = $temp; 
            $temp *= $arr[$i]; 
        } 

        /* Initialize temp to 1  
           for product on right 
           side */
        $temp = 1; 

        /* In this loop, temp  
           variable contains 
           product of elements  
           on right side  
           excluding arr[i] */
        for ($i = $n - 1; $i >= 0; $i--)  
        { 
            $prod[$i] *= $temp; 
            $temp *= $arr[$i]; 
        } 

        /* print the constructed 
           prod array */
        for ($i = 0; $i < $n; $i++) 
            echo $prod[$i], " "; 

        return; 
    } 

        // Driver Code     
        $arr = array(10, 3, 5, 6, 2); 
        $n = count($arr); 
        echo "The product array is : \n"; 
        productArray($arr, $n); 

// This code is contributed by anuj_67\. 
?> 

```

**输出**：

```
The product array is : 
180 600 360 300 900 

```

**复杂度分析**：

*   **时间复杂度**：`O(n)`。

    原始数组仅需要遍历一次，因此时间复杂度是恒定的。

*   **空间复杂度**：`O(n)`。

    即使删除了多余的数组，空间复杂度仍然为`O(n)`，因为仍然需要乘积数组。

[**乘积数组问题 | 系列 2（`O(1)`空间）**](https://www.geeksforgeeks.org/product-array-puzzle-set-2-o1-space/)

**相关问题**：

[根据数组中所有元素的异或构造，将同一索引处的元素除外](https://www.geeksforgeeks.org/construct-an-array-from-xor-of-all-elements-of-array-except-element-at-same-index/)

如果您发现上述代码/算法有误，请写评论，或者找到解决同一问题的更好方法。

