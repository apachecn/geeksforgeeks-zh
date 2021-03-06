# 在给定的按行排序的矩阵的所有行中找到一个公共元素

> 原文： [https://www.geeksforgeeks.org/find-common-element-rows-row-wise-sorted-matrix/](https://www.geeksforgeeks.org/find-common-element-rows-row-wise-sorted-matrix/)

给定一个矩阵，其中每一行都按升序排序。 编写一个在所有行中查找并返回一个公共元素的函数。 如果没有公共元素，则返回-1。

**示例**：

```
Input: mat[4][5] = { {1, 2, 3, 4, 5},
                    {2, 4, 5, 8, 10},
                    {3, 5, 7, 9, 11},
                    {1, 3, 5, 7, 9},
                  };
Output: 5
```

一个`O(m * n * n)`简单解决方案是采用第一行的每个元素并在所有其他行中进行搜索，直到找到一个公共元素。 该解决方案的时间复杂度为`O(m * n * n)`，其中`m`是给定矩阵中的行数，`n`是列数。 如果我们使用[二分搜索](http://geeksquiz.com/binary-search/)而不是线性搜索，则可以将其改进为`O(m * n * log n)`。

我们可以使用类似于[归并排序](http://geeksquiz.com/merge-sort/)的合并方法在`O(mn)`时间中解决此问题。 这个想法是从每一行的最后一列开始。 如果所有最后一列的元素都相同，那么我们找到了公共元素。 否则，我们找到所有最后一列中的最小值。 找到最小元素后，我们知道最后一列中的所有其他元素不能成为公共元素，因此我们会减少所有行的最后一列索引，除了具有最小值的行。 我们一直重复这些步骤，直到当前最后一列的所有元素都不相同，或者最后一列的索引达到 0。

以下是上述想法的实现。

## C++ 

```cpp

// A C++ program to find a common element in all rows of a 
// row wise sorted array 
#include <bits/stdc++.h> 
using namespace std; 

// Specify number of rows and columns 
#define M 4 
#define N 5 

// Returns common element in all rows of mat[M][N]. If there is no 
// common element, then -1 is returned 
int findCommon(int mat[M][N]) 
{ 
    // An array to store indexes of current last column 
    int column[M]; 
    int min_row; // To store index of row whose current 
    // last element is minimum 

    // Initialize current last element of all rows 
    int i; 
    for (i = 0; i < M; i++) 
        column[i] = N - 1; 

    min_row = 0; // Initialize min_row as first row 

    // Keep finding min_row in current last column, till either 
    // all elements of last column become same or we hit first column. 
    while (column[min_row] >= 0) { 
        // Find minimum in current last column 
        for (i = 0; i < M; i++) { 
            if (mat[i][column[i]] < mat[min_row][column[min_row]]) 
                min_row = i; 
        } 

        // eq_count is count of elements equal to minimum in current last 
        // column. 
        int eq_count = 0; 

        // Traverse current last column elements again to update it 
        for (i = 0; i < M; i++) { 
            // Decrease last column index of a row whose value is more 
            // than minimum. 
            if (mat[i][column[i]] > mat[min_row][column[min_row]]) { 
                if (column[i] == 0) 
                    return -1; 

                column[i] -= 1; // Reduce last column index by 1 
            } 
            else
                eq_count++; 
        } 

        // If equal count becomes M, return the value 
        if (eq_count == M) 
            return mat[min_row][column[min_row]]; 
    } 
    return -1; 
} 

// Driver Code 
int main() 
{ 
    int mat[M][N] = { 
        { 1, 2, 3, 4, 5 }, 
        { 2, 4, 5, 8, 10 }, 
        { 3, 5, 7, 9, 11 }, 
        { 1, 3, 5, 7, 9 }, 
    }; 
    int result = findCommon(mat); 
    if (result == -1) 
        cout << "No common element"; 
    else
        cout << "Common element is " << result; 
    return 0; 
} 

// This code is contributed 
// by Akanksha Rai 

```

## C

```c

// A C program to find a common element in all rows of a 
// row wise sorted array 
#include <stdio.h> 

// Specify number of rows and columns 
#define M 4 
#define N 5 

// Returns common element in all rows of mat[M][N]. If there is no 
// common element, then -1 is returned 
int findCommon(int mat[M][N]) 
{ 
    // An array to store indexes of current last column 
    int column[M]; 
    int min_row; // To store index of row whose current 
    // last element is minimum 

    // Initialize current last element of all rows 
    int i; 
    for (i = 0; i < M; i++) 
        column[i] = N - 1; 

    min_row = 0; // Initialize min_row as first row 

    // Keep finding min_row in current last column, till either 
    // all elements of last column become same or we hit first column. 
    while (column[min_row] >= 0) { 
        // Find minimum in current last column 
        for (i = 0; i < M; i++) { 
            if (mat[i][column[i]] < mat[min_row][column[min_row]]) 
                min_row = i; 
        } 

        // eq_count is count of elements equal to minimum in current last 
        // column. 
        int eq_count = 0; 

        // Traverse current last column elements again to update it 
        for (i = 0; i < M; i++) { 
            // Decrease last column index of a row whose value is more 
            // than minimum. 
            if (mat[i][column[i]] > mat[min_row][column[min_row]]) { 
                if (column[i] == 0) 
                    return -1; 

                column[i] -= 1; // Reduce last column index by 1 
            } 
            else
                eq_count++; 
        } 

        // If equal count becomes M, return the value 
        if (eq_count == M) 
            return mat[min_row][column[min_row]]; 
    } 
    return -1; 
} 

// driver program to test above function 
int main() 
{ 
    int mat[M][N] = { 
        { 1, 2, 3, 4, 5 }, 
        { 2, 4, 5, 8, 10 }, 
        { 3, 5, 7, 9, 11 }, 
        { 1, 3, 5, 7, 9 }, 
    }; 
    int result = findCommon(mat); 
    if (result == -1) 
        printf("No common element"); 
    else
        printf("Common element is %d", result); 
    return 0; 
} 

```

## Java

```java

// A Java program to find a common 
// element in all rows of a 
// row wise sorted array 

class GFG { 
    // Specify number of rows and columns 
    static final int M = 4; 
    static final int N = 5; 

    // Returns common element in all rows 
    // of mat[M][N]. If there is no 
    // common element, then -1 is 
    // returned 
    static int findCommon(int mat[][]) 
    { 
        // An array to store indexes 
        // of current last column 
        int column[] = new int[M]; 

        // To store index of row whose current 
        // last element is minimum 
        int min_row; 

        // Initialize current last element of all rows 
        int i; 
        for (i = 0; i < M; i++) 
            column[i] = N - 1; 

        // Initialize min_row as first row 
        min_row = 0; 

        // Keep finding min_row in current last column, till either 
        // all elements of last column become same or we hit first column. 
        while (column[min_row] >= 0) { 
            // Find minimum in current last column 
            for (i = 0; i < M; i++) { 
                if (mat[i][column[i]] < mat[min_row][column[min_row]]) 
                    min_row = i; 
            } 

            // eq_count is count of elements equal to minimum in current last 
            // column. 
            int eq_count = 0; 

            // Traverse current last column elements again to update it 
            for (i = 0; i < M; i++) { 
                // Decrease last column index of a row whose value is more 
                // than minimum. 
                if (mat[i][column[i]] > mat[min_row][column[min_row]]) { 
                    if (column[i] == 0) 
                        return -1; 

                    // Reduce last column index by 1 
                    column[i] -= 1; 
                } 
                else
                    eq_count++; 
            } 

            // If equal count becomes M, 
            // return the value 
            if (eq_count == M) 
                return mat[min_row][column[min_row]]; 
        } 
        return -1; 
    } 

    // Driver code 
    public static void main(String[] args) 
    { 
        int mat[][] = { { 1, 2, 3, 4, 5 }, 
                        { 2, 4, 5, 8, 10 }, 
                        { 3, 5, 7, 9, 11 }, 
                        { 1, 3, 5, 7, 9 } }; 
        int result = findCommon(mat); 
        if (result == -1) 
            System.out.print("No common element"); 
        else
            System.out.print("Common element is " + result); 
    } 
} 

// This code is contributed by Anant Agarwal. 

```

## Python 3

```py

# Python 3 program to find a common element  
# in all rows of a row wise sorted array 

# Specify number of rows  
# and columns 
M = 4
N = 5

# Returns common element in all rows  
# of mat[M][N]. If there is no common  
# element, then -1 is returned 
def findCommon(mat): 

    # An array to store indexes of  
    # current last column 
    column = [N - 1] * M 

    min_row = 0 # Initialize min_row as first row 

    # Keep finding min_row in current last  
    # column, till either all elements of  
    # last column become same or we hit first column. 
    while (column[min_row] >= 0): 

        # Find minimum in current last column 
        for i in range(M): 
            if (mat[i][column[i]] <  
                mat[min_row][column[min_row]]): 
                min_row = i 

        # eq_count is count of elements equal  
        # to minimum in current last column. 
        eq_count = 0

        # Traverse current last column elements 
        # again to update it 
        for i in range(M): 

            # Decrease last column index of a row  
            # whose value is more than minimum. 
            if (mat[i][column[i]] >  
                mat[min_row][column[min_row]]): 
                if (column[i] == 0): 
                    return -1

                column[i] -= 1 # Reduce last column 
                               # index by 1 

            else: 
                eq_count += 1

        # If equal count becomes M, return the value 
        if (eq_count == M): 
            return mat[min_row][column[min_row]] 
    return -1

# Driver Code 
if __name__ == "__main__": 

    mat = [[1, 2, 3, 4, 5], 
           [2, 4, 5, 8, 10], 
           [3, 5, 7, 9, 11], 
           [1, 3, 5, 7, 9]] 

    result = findCommon(mat) 
    if (result == -1): 
        print("No common element") 
    else: 
        print("Common element is", result) 

# This code is contributed by ita_c 

```

## C# 

```cs

// A C# program to find a common 
// element in all rows of a 
// row wise sorted array 
using System; 

class GFG { 

    // Specify number of rows and columns 
    static int M = 4; 
    static int N = 5; 

    // Returns common element in all rows 
    // of mat[M][N]. If there is no 
    // common element, then -1 is 
    // returned 
    static int findCommon(int[, ] mat) 
    { 

        // An array to store indexes 
        // of current last column 
        int[] column = new int[M]; 

        // To store index of row whose 
        // current last element is minimum 
        int min_row; 

        // Initialize current last element 
        // of all rows 
        int i; 
        for (i = 0; i < M; i++) 
            column[i] = N - 1; 

        // Initialize min_row as first row 
        min_row = 0; 

        // Keep finding min_row in current 
        // last column, till either all 
        // elements of last column become 
        // same or we hit first column. 
        while (column[min_row] >= 0) { 

            // Find minimum in current 
            // last column 
            for (i = 0; i < M; i++) { 
                if (mat[i, column[i]] < mat[min_row, column[min_row]]) 
                    min_row = i; 
            } 

            // eq_count is count of elements 
            // equal to minimum in current 
            // last column. 
            int eq_count = 0; 

            // Traverse current last column 
            // elements again to update it 
            for (i = 0; i < M; i++) { 

                // Decrease last column index 
                // of a row whose value is more 
                // than minimum. 
                if (mat[i, column[i]] > mat[min_row, column[min_row]]) { 
                    if (column[i] == 0) 
                        return -1; 

                    // Reduce last column index 
                    // by 1 
                    column[i] -= 1; 
                } 
                else
                    eq_count++; 
            } 

            // If equal count becomes M, 
            // return the value 
            if (eq_count == M) 
                return mat[min_row, 
                           column[min_row]]; 
        } 

        return -1; 
    } 

    // Driver code 
    public static void Main() 
    { 
        int[, ] mat = { { 1, 2, 3, 4, 5 }, 
                        { 2, 4, 5, 8, 10 }, 
                        { 3, 5, 7, 9, 11 }, 
                        { 1, 3, 5, 7, 9 } }; 

        int result = findCommon(mat); 

        if (result == -1) 
            Console.Write("No common element"); 
        else
            Console.Write("Common element is "
                          + result); 
    } 
} 

// This code is contributed by Sam007\. 

```

**输出**：

```
Common element is 5

```

**以上代码**的工作解释让我们理解以下示例的上述代码的工作。

最后一列数组中的初始条目为`N-1`，即：

```
{4, 4, 4, 4}, 
{1, 2, 3, 4, 5}, 
{2, 4, 5, 8, 10}, 
{3, 5, 7, 9, 11}, 
{1, 3, 5, 7, 9}, 
```

`min_row`的值为 0，因此值大于 5 的行的最后一列索引的值将减少 1。 因此 `column[]`变为：

```
{4, 3, 3, 3}, 
{1, 2, 3, 4, 5}, 
{2, 4, 5, 8, 10}, 
{3, 5, 7, 9, 11}, 
{1, 3, 5, 7, 9}, 
```

`min_row`的值保持为 0，值大于 5 的行的最后一列索引的值减小 1。 因此`column[]`变为：

```
{4, 2, 2, 2}, 
{1, 2, 3, 4, 5}, 
{2, 4, 5, 8, 10}, 
{3, 5, 7, 9, 11}, 
{1, 3, 5, 7, 9}, 
```

`min_row`的值保持为 0，值大于 5 的行的最后一列索引的值减小 1。 因此`colomun[]`变为：

```
{4, 2, 1, 2}, 
{1, 2, 3, 4, 5}, 
{2, 4, 5, 8, 10}, 
{3, 5, 7, 9, 11}, 
{1, 3, 5, 7, 9}, 
```

现在，所有行的当前最后一列中的所有值都相同，因此返回 5。

**基于哈希的解决方案**：

我们也可以使用哈希。 即使未对行进行排序，此解决方案也有效。 它可用于打印所有常见元素。

```
Step1:  Create a Hash Table with all key as distinct elements 
        of row1\. Value for all these will be 0.

Step2:  
For i = 1 to M-1
 For j = 0 to N-1
  If (mat[i][j] is already present in Hash Table)
   If (And this is not a repetition in current row.
      This can be checked by comparing HashTable value with
      row number)
         Update the value of this key in HashTable with current 
         row number

Step3: Iterate over HashTable and print all those keys for 
       which value = M 
```

## C++

```cpp

// C++ implementation of the approach 
#include <bits/stdc++.h> 
using namespace std; 

// Specify number of rows and columns 
#define M 4 
#define N 5 

// Returns common element in all rows of mat[M][N]. If there is no 
// common element, then -1 is returned 
int findCommon(int mat[M][N]) 
{ 
    // A hash map to store count of elements 
    unordered_map<int, int> cnt; 

    int i, j; 

    for (i = 0; i < M; i++) { 

        // Increment the count of first 
        // element of the row 
        cnt[mat[i][0]]++; 

        // Starting from the second element 
        // of the current row 
        for (j = 1; j < N; j++) { 

            // If current element is different from 
            // the previous element i.e. it is appearing 
            // for the first time in the current row 
            if (mat[i][j] != mat[i][j - 1]) 
                cnt[mat[i][j]]++; 
        } 
    } 

    // Find element having count equal to number of rows 
    for (auto ele : cnt) { 
        if (ele.second == M) 
            return ele.first; 
    } 

    // No such element found 
    return -1; 
} 

// Driver Code 
int main() 
{ 
    int mat[M][N] = { 
        { 1, 2, 3, 4, 5 }, 
        { 2, 4, 5, 8, 10 }, 
        { 3, 5, 7, 9, 11 }, 
        { 1, 3, 5, 7, 9 }, 
    }; 
    int result = findCommon(mat); 
    if (result == -1) 
        cout << "No common element"; 
    else
        cout << "Common element is " << result; 

    return 0; 
} 

```

## Java

```java

// Java implementation of the approach 
import java.util.*; 

class GFG  
{ 

// Specify number of rows and columns 
static int M = 4; 
static int N = 5; 

// Returns common element in all rows of mat[M][N]. 
// If there is no common element, then -1 is returned 
static int findCommon(int mat[][]) 
{ 
    // A hash map to store count of elements 
    HashMap<Integer,  
            Integer> cnt = new HashMap<Integer,  
                                       Integer>(); 

    int i, j; 

    for (i = 0; i < M; i++)  
    { 

        // Increment the count of first 
        // element of the row 
        if(cnt.containsKey(mat[i][0])) 
        { 
            cnt.put(mat[i][0],  
            cnt.get(mat[i][0]) + 1); 
        } 
        else
        { 
            cnt.put(mat[i][0], 1); 
        } 

        // Starting from the second element 
        // of the current row 
        for (j = 1; j < N; j++)  
        { 

            // If current element is different from 
            // the previous element i.e. it is appearing 
            // for the first time in the current row 
            if (mat[i][j] != mat[i][j - 1]) 
                if(cnt.containsKey(mat[i][j])) 
                { 
                    cnt.put(mat[i][j],  
                    cnt.get(mat[i][j]) + 1); 
                } 
                else
                { 
                    cnt.put(mat[i][j], 1); 
                } 
        } 
    } 

    // Find element having count  
    // equal to number of rows 
    for (Map.Entry<Integer,  
                   Integer> ele : cnt.entrySet()) 
    { 
        if (ele.getValue() == M) 
            return ele.getKey(); 
    } 

    // No such element found 
    return -1; 
} 

// Driver Code 
public static void main(String[] args)  
{ 
    int mat[][] = {{ 1, 2, 3, 4, 5 }, 
                   { 2, 4, 5, 8, 10 }, 
                   { 3, 5, 7, 9, 11 }, 
                   { 1, 3, 5, 7, 9 }}; 
    int result = findCommon(mat); 
    if (result == -1) 
        System.out.println("No common element"); 
    else
        System.out.println("Common element is " + result); 
    } 
} 

// This code is contributed by Rajput-Ji 

```

## Python

```py

# Python3 implementation of the approach 
from collections import defaultdict 

# Specify number of rows and columns 
M = 4
N = 5

# Returns common element in all rows of 
# mat[M][N]. If there is no 
# common element, then -1 is returned 
def findCommon(mat): 
    global M 
    global N 

    # A hash map to store count of elements 
    cnt = dict() 
    cnt = defaultdict(lambda: 0, cnt) 

    i = 0
    j = 0

    while (i < M ):  

        # Increment the count of first 
        # element of the row 
        cnt[mat[i][0]] = cnt[mat[i][0]] + 1

        j = 1

        # Starting from the second element 
        # of the current row 
        while (j < N ) : 

            # If current element is different from 
            # the previous element i.e. it is appearing 
            # for the first time in the current row 
            if (mat[i][j] != mat[i][j - 1]): 
                cnt[mat[i][j]] = cnt[mat[i][j]] + 1
            j = j + 1
        i = i + 1

    # Find element having count equal to number of rows 
    for ele in cnt: 
        if (cnt[ele] == M): 
            return ele 

    # No such element found 
    return -1

# Driver Code 
mat = [[1, 2, 3, 4, 5 ], 
        [2, 4, 5, 8, 10], 
        [3, 5, 7, 9, 11], 
        [1, 3, 5, 7, 9 ],] 

result = findCommon(mat) 
if (result == -1): 
    print("No common element") 
else: 
    print("Common element is ", result) 

# This code is contributed by Arnab Kundu 

```

## C#

```cs

// C# implementation of the approach 
using System; 
using System.Collections.Generic;  

class GFG  
{ 

// Specify number of rows and columns 
static int M = 4; 
static int N = 5; 

// Returns common element in all rows of mat[M,N]. 
// If there is no common element, then -1 is returned 
static int findCommon(int [,]mat) 
{ 
    // A hash map to store count of elements 
    Dictionary<int, 
               int> cnt = new Dictionary<int,  
                                         int>(); 

    int i, j; 

    for (i = 0; i < M; i++)  
    { 

        // Increment the count of first 
        // element of the row 
        if(cnt.ContainsKey(mat[i, 0])) 
        { 
            cnt[mat[i, 0]]= cnt[mat[i, 0]] + 1; 
        } 
        else
        { 
            cnt.Add(mat[i, 0], 1); 
        } 

        // Starting from the second element 
        // of the current row 
        for (j = 1; j < N; j++)  
        { 

            // If current element is different from 
            // the previous element i.e. it is appearing 
            // for the first time in the current row 
            if (mat[i, j] != mat[i, j - 1]) 
                if(cnt.ContainsKey(mat[i, j])) 
                { 
                    cnt[mat[i, j]]= cnt[mat[i, j]] + 1; 
                } 
                else
                { 
                    cnt.Add(mat[i, j], 1); 
                } 
        } 
    } 

    // Find element having count  
    // equal to number of rows 
    foreach(KeyValuePair<int, int> ele in cnt) 
    { 
        if (ele.Value == M) 
            return ele.Key; 
    } 

    // No such element found 
    return -1; 
} 

// Driver Code 
public static void Main(String[] args)  
{ 
    int [,]mat = {{ 1, 2, 3, 4, 5 }, 
                  { 2, 4, 5, 8, 10 }, 
                  { 3, 5, 7, 9, 11 }, 
                  { 1, 3, 5, 7, 9 }}; 
    int result = findCommon(mat); 
    if (result == -1) 
        Console.WriteLine("No common element"); 
    else
        Console.WriteLine("Common element is " + result); 
    } 
}  

// This code is contributed by 29AjayKumar 

```

**输出**：

```
Common element is 5

```

在哈希表中进行搜索和插入需要`O(1)`时间的假设下，上述基于哈希的解决方案的时间复杂度为`O(MN)`。 感谢 Nishant 在下面的评论中建议此解决方案。

**练习**：给定`n`个大小为`m`的已排序数组，请在`O(MN)`时间内找到所有数组中的所有公共元素。

