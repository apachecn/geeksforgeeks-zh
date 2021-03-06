# 搜索按行和按列排序的矩阵

> 原文： [https://www.geeksforgeeks.org/search-in-row-wise-and-column-wise-sorted-matrix/](https://www.geeksforgeeks.org/search-in-row-wise-and-column-wise-sorted-matrix/)

给定一个`n x n`矩阵和一个数字`x`，找到`x`在矩阵中的位置（如果存在）。 否则，打印`not found`。 在给定的矩阵中，每一行和每一列都按升序排序。 设计的算法应具有线性时间复杂度。

**示例**：

```
Input: mat[4][4] = { {10, 20, 30, 40},
                      {15, 25, 35, 45},
                      {27, 29, 37, 48},
                      {32, 33, 39, 50}};
              x = 29
Output: Found at (2, 1)
Explanation: Element at (2,1) is 29

Input : mat[4][4] = { {10, 20, 30, 40},
                      {15, 25, 35, 45},
                      {27, 29, 37, 48},
                      {32, 33, 39, 50}};
              x = 100
Output : Element not found
Explanation: Element 100 is not found

```



**简单解决方案**：

*   **方法**：简单的想法是遍历数组并逐一搜索元素。

*   **算法**：

    1.  运行嵌套循环，外循环用于行，内循环用于列。

    2.  用`x`检查每个元素，如果找到该元素，则打印`Element found`。

    3.  如果找不到该元素，则打印`Element not found`。

*   **实现**： 

    ```

    // C++ program to search an element in row-wise 
    // and column-wise sorted matrix 
    #include <bits/stdc++.h> 

    using namespace std; 

    /* Searches the element x in mat[][]. If the  
    element is found, then prints its position  
    and returns true, otherwise prints "not found" 
    and returns false */
    int search(int mat[4][4], int n, int x) 
    { 
        if (n == 0) 
            return -1; 

        //traverse through the matrix 
        for(int i = 0; i < n; i++) 
        { 
            for(int j = 0; j < n; j++) 
            //if the element is found 
            if(mat[i][j] == x) 
            { 
                cout<<"Element found at ("<<i<<", "<<j<<")\n"; 
                return 1; 
            } 
        } 

        cout << "n Element not found"; 
        return 0;  
    } 

    // Driver code 
    int main() 
    { 
        int mat[4][4] = { { 10, 20, 30, 40 }, 
                          { 15, 25, 35, 45 }, 
                          { 27, 29, 37, 48 }, 
                          { 32, 33, 39, 50 } }; 
        search(mat, 4, 29); 

        return 0; 
    } 

    ```

    **输出**：

    ```
    Element found at (2, 1)

    ```** 

*   **复杂度分析**：

    *   **时间复杂度**：`O(n^2)`。

        数组的单个遍历需要 `O(n^2)`时间。

    *   **空间复杂度**：`O(1)`。

        不需要多余的空间。

**更好的解决方案**是[使用时间复杂度为`O(n ^ 1.58)`的分治找到元素](https://www.geeksforgeeks.org/divide-conquer-set-6-search-row-wise-column-wise-sorted-2d-array/)。 有关详细信息，[请参考这里](https://www.geeksforgeeks.org/divide-conquer-set-6-search-row-wise-column-wise-sorted-2d-array/)。

**有效解决方案**：

*   **方法**： The simple idea is to remove a row or column in each comparison until an element is found. Start searching from the top-right corner of the matrix. There are three possible cases.

    1.  **给定的数字大于当前的数字**：这将确保当前行中的所有元素都小于给定的数字，因为指针已经在最右边的元素上并且对该行进行了排序 。 因此，整个行将被消除，并在下一行继续搜索。 在这里消除意味着不需要搜索行。

    2.  **给定的数字小于当前数字**：这将确保当前列中的所有元素都大于给定的数字。 因此，整个列将被消除，并继续在前一列（即最左侧的列）中进行搜索。

    3.  **给定的数字等于当前的数字**：这将结束搜索。

    搜索也可以从矩阵的左下角开始。

*   **算法**：

    1.  假设给定元素为`x`，则创建两个变量`i = 0, j = n-1`*`作为行和列的索引。

    2.  执行循环直到`i = 0`。

    3.  检查当前元素是否大于`x`，然后减少`j`的计数。 排除当前列。

    4.  检查当前元素是否小于`x`，然后增加`i`的计数。 排除当前行。

    5.  如果元素相等，则打印位置并结束。

*   **感谢 devendraiiit 建议采用以下方法。**

*   **实现**：

    ## C++ 

    ```

    // C++ program to search an element in row-wise 
    // and column-wise sorted matrix 
    #include <bits/stdc++.h> 

    using namespace std; 

    /* Searches the element x in mat[][]. If the  
    element is found, then prints its position  
    and returns true, otherwise prints "not found" 
    and returns false */
    int search(int mat[4][4], int n, int x) 
    { 
        if (n == 0) 
            return -1; 
        int smallest = a[0][0], largest = a[n - 1][n - 1]; 
        if (x < smallest || x > largest) 
            return -1; 
        // set indexes for top right element 
        int i = 0, j = n - 1;  
        while (i < n && j >= 0) { 
            if (mat[i][j] == x) { 
                cout << "n Found at "
                     << i << ", " << j; 
                return 1; 
            } 
            if (mat[i][j] > x) 
                j--; 
            else // if mat[i][j] < x 
                i++; 
        } 

        cout << "n Element not found"; 
        return 0; // if ( i==n || j== -1 ) 
    } 

    // Driver code 
    int main() 
    { 
        int mat[4][4] = { { 10, 20, 30, 40 }, 
                          { 15, 25, 35, 45 }, 
                          { 27, 29, 37, 48 }, 
                          { 32, 33, 39, 50 } }; 
        search(mat, 4, 29); 

        return 0; 
    } 

    // This code is contributed 
    // by Akanksha Rai(Abby_akku) 

    ```

    ## C

    ```

    // C program to search an element in row-wise 
    // and column-wise sorted matrix 
    #include <stdio.h> 

    /* Searches the element x in mat[][]. If the  
    element is found, then prints its position  
    and returns true, otherwise prints "not found" 
    and returns false */
    int search(int mat[4][4], int n, int x) 
    { 
        if (n == 0) 
            return -1; 
        int smallest = a[0][0], largest = a[n - 1][n - 1]; 
        if (x < smallest || x > largest) 
            return -1; 
        int i = 0, j = n - 1; // set indexes for top right element 
        while (i < n && j >= 0) { 
            if (mat[i][j] == x) { 
                printf("\n Found at %d, %d", i, j); 
                return 1; 
            } 
            if (mat[i][j] > x) 
                j--; 
            else // if mat[i][j] < x 
                i++; 
        } 

        printf("n Element not found"); 
        return 0; // if ( i==n || j== -1 ) 
    } 

    // driver program to test above function 
    int main() 
    { 
        int mat[4][4] = { 
            { 10, 20, 30, 40 }, 
            { 15, 25, 35, 45 }, 
            { 27, 29, 37, 48 }, 
            { 32, 33, 39, 50 }, 
        }; 
        search(mat, 4, 29); 
        return 0; 
    } 

    ```

    ## Java

    ```

    // JAVA Code for Search in a row wise and 
    // column wise sorted matrix 

    class GFG { 

        /* Searches the element x in mat[][]. If the  
    element is found, then prints its position  
    and returns true, otherwise prints "not found" 
    and returns false */
        private static void search(int[][] mat, int n, int x) 
        { 

            int i = 0, j = n - 1; // set indexes for top right 
            // element 

            while (i < n && j >= 0) { 
                if (mat[i][j] == x) { 
                    System.out.print("n Found at " + i + " " + j); 
                    return; 
                } 
                if (mat[i][j] > x) 
                    j--; 
                else // if mat[i][j] < x 
                    i++; 
            } 

            System.out.print("n Element not found"); 
            return; // if ( i==n || j== -1 ) 
        } 
        // driver program to test above function 
        public static void main(String[] args) 
        { 
            int mat[][] = { { 10, 20, 30, 40 }, 
                            { 15, 25, 35, 45 }, 
                            { 27, 29, 37, 48 }, 
                            { 32, 33, 39, 50 } }; 

            search(mat, 4, 29); 
        } 
    } 
    // This code is contributed by Arnav Kr. Mandal. 

    ```

    ## Python3

    ```

    # Python3 program to search an element  
    # in row-wise and column-wise sorted matrix 

    # Searches the element x in mat[][]. If the  
    # element is found, then prints its position  
    # and returns true, otherwise prints "not found" 
    # and returns false 
    def search(mat, n, x): 

        i = 0

        # set indexes for top right element 
        j = n - 1
        while ( i < n and j >= 0 ): 

            if (mat[i][j] == x ): 

                print("n Found at ", i, ", ", j) 
                return 1

            if (mat[i][j] > x ): 
                j -= 1

            # if mat[i][j] < x 
            else:  
                i += 1

        print("Element not found") 
        return 0 # if (i == n || j == -1 ) 

    # Driver Code 
    mat = [ [10, 20, 30, 40], 
            [15, 25, 35, 45], 
            [27, 29, 37, 48], 
            [32, 33, 39, 50] ] 
    search(mat, 4, 29) 

    # This code is contributed by Anant Agarwal. 

    ```

    ## C# 

    ```

    // C# Code for Search in a row wise and 
    // column wise sorted matrix 
    using System; 

    class GFG { 
        /* Searches the element x in mat[][]. If the  
        element is found, then prints its position  
        and returns true, otherwise prints "not found" 
        and returns false */
        private static void search(int[, ] mat, 
                                   int n, int x) 
        { 
            // set indexes for top right 
            // element 
            int i = 0, j = n - 1; 

            while (i < n && j >= 0) { 
                if (mat[i, j] == x) { 
                    Console.Write("n Found at "
                                  + i + ", " + j); 
                    return; 
                } 

                if (mat[i, j] > x) 
                    j--; 
                else // if mat[i][j] < x 
                    i++; 
            } 

            Console.Write("n Element not found"); 
            return; // if ( i==n || j== -1 ) 
        } 
        // driver program to test above function 
        public static void Main() 
        { 

            int[, ] mat = { { 10, 20, 30, 40 }, 
                            { 15, 25, 35, 45 }, 
                            { 27, 29, 37, 48 }, 
                            { 32, 33, 39, 50 } }; 

            search(mat, 4, 29); 
        } 
    } 

    // This code is contributed by Sam007 

    ```

    ## PHP

    ```

    <?php  
    // PHP program to search an  
    // element in row-wise and  
    // column-wise sorted matrix 

    /* Searches the element $x  
    in mat[][]. If the element is  
    found, then prints its position  
    and returns true, otherwise prints 
    "not found" and returns false */
    function search(&$mat, $n, $x) 
    { 
        $i = 0; 
        $j = $n - 1; // set indexes for 
                    // top right element 
        while ($i < $n && $j >= 0) 
        { 
            if ($mat[$i][$j] == $x) 
            { 
                echo "n found at " . $i.  
                            ", " . $j; 
                return 1; 
            } 
            if ($mat[$i][$j] > $x) 
                $j--; 
            else // if $mat[$i][$j] < $x 
                $i++; 
        } 

        echo "n Element not found"; 
        return 0; // if ( $i==$n || $j== -1 ) 
    } 

    // Driver Code 
    $mat = array(array(10, 20, 30, 40), 
                array(15, 25, 35, 45), 
                array(27, 29, 37, 48), 
                array(32, 33, 39, 50)); 
    search($mat, 4, 29); 

    // This code is contributed 
    // by ChitraNayal 
    ?> 

    ```

    **输出**：

    ```
    Found at 2, 1
    ```

*   **复杂度分析**：

*   **时间复杂度**：`O(n)`。

    仅需要一个遍历，即`i`从 0 到`n`，`j`从`n-1`到 0，最多`2 * n`步。

    **上述方法也适用于`m x n`矩阵（不仅适用于`n x n`）。 复杂度为` O(m + n)`。**

*   **空间复杂度**：`O(1)`。

    不需要多余的空间。

**相关文章**：

[排序矩阵中的元素搜索](https://www.geeksforgeeks.org/search-element-sorted-matrix/)

如果您发现上述代码/算法有误，请写评论，或者找到其他解决相同问题的方法。

