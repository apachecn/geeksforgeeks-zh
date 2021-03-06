# 计算可能的三角形数量

> 原文： [https://www.geeksforgeeks.org/find-number-of-triangles-possible/](https://www.geeksforgeeks.org/find-number-of-triangles-possible/)

给定一个未排序的正整数数组，找到可以用三个不同的数组元素作为三角形的三个边形成的三角形的数量。 为了使三角形有 3 个值，两个值（或边）中的任何一个之和必须大于第三个值（或第三边）。

**示例**：

```
Input: arr= {4, 6, 3, 7}
Output: 3
Explanation: There are three triangles 
possible {3, 4, 6}, {4, 6, 7} and {3, 6, 7}. 
Note that {3, 4, 7} is not a possible triangle.  

Input: arr= {10, 21, 22, 100, 101, 200, 300}.
Output: 6

Explanation: There can be 6 possible triangles:
{10, 21, 22}, {21, 100, 101}, {22, 100, 101}, 
{10, 100, 101}, {100, 101, 200} and {101, 200, 300}

```



**方法 1（暴力）**：

*   **方法**：暴力方法是运行三个循环并跟踪到目前为止可能出现的三角形数量。 三个循环从数组中选择三个不同的值。 最内层的循环检查是否有三角形属性，该属性指定任意两个边的和必须大于第三边的值。

*   **算法**：

    1.  运行三个嵌套循环，每个循环从上一个循环的索引开始到数组的末尾，即从 0 到`n`运行第一个循环，从`i`到`n`循环`j`，从`j`到`n`循环`k`。

    2.  检查`array[i] + array[j] > array[k]`，`array[i] + array[k] > array[j]`，`array[k] + array[j] > array[i]`，即两侧的和大于第三侧。

    3.  如果所有三个条件都匹配，则增加计数。

    4.  打印计数。

*   **实现**：

    ## C++ 

    ```

    // C++ code to count the number of 
    // possible triangles using brute 
    // force approach 
    #include <bits/stdc++.h> 
    using namespace std; 

    // Function to count all possible 
    // triangles with arr[] elements 
    int findNumberOfTriangles(int arr[], int n) 
    { 
        // Count of triangles 
        int count = 0; 

        // The three loops select three 
        // different values from array 
        for (int i = 0; i < n; i++) { 
            for (int j = i + 1; j < n; j++) { 

                // The innermost loop checks for 
                // the triangle property 
                for (int k = j + 1; k < n; k++) 

                    // Sum of two sides is greater 
                    // than the third 
                    if ( 
                        arr[i] + arr[j] > arr[k] 
                        && arr[i] + arr[k] > arr[j] 
                        && arr[k] + arr[j] > arr[i]) 
                        count++; 
            } 
        } 
        return count; 
    } 

    // Driver code 
    int main() 
    { 
        int arr[] = { 10, 21, 22, 100, 101, 200, 300 }; 
        int size = sizeof(arr) / sizeof(arr[0]); 

        cout 
            << "Total number of triangles possible is "
            << findNumberOfTriangles(arr, size); 

        return 0; 
    } 

    ```

    ## Java

    ```

    // Java code to count the number of 
    // possible triangles using brute 
    // force approach 
    import java.io.*; 
    import java.util.*; 

    class GFG 
    { 

        // Function to count all possible 
        // triangles with arr[] elements 
        static int findNumberOfTriangles(int arr[], int n) 
        { 
            // Count of triangles 
            int count = 0; 

            // The three loops select three 
            // different values from array 
            for (int i = 0; i < n; i++) { 
                for (int j = i + 1; j < n; j++) { 

                    // The innermost loop checks for 
                    // the triangle property 
                    for (int k = j + 1; k < n; k++) 

                        // Sum of two sides is greater 
                        // than the third 
                        if ( 
                            arr[i] + arr[j] > arr[k] 
                            && arr[i] + arr[k] > arr[j] 
                            && arr[k] + arr[j] > arr[i]) 
                            count++; 
                } 
            } 
            return count; 
        } 

        // Driver code 
         public static void main(String[] args) 
        { 
            int arr[] = { 10, 21, 22, 100, 101, 200, 300 }; 
            int size = arr.length; 

            System.out.println( "Total number of triangles possible is "+ 
            findNumberOfTriangles(arr, size)); 
        } 
    } 

    // This code is contributed by shubhamsingh10 

    ```

    ## Python3

    ```

    # Python3 code to count the number of 
    # possible triangles using brute 
    # force approach 

    # Function to count all possible 
    # triangles with arr[] elements 
    def findNumberOfTriangles(arr, n): 

        # Count of triangles 
        count = 0

        # The three loops select three 
        # different values from array 
        for i in range(n): 
            for j in range(i + 1, n): 

                # The innermost loop checks for 
                # the triangle property 
                for k in range(j + 1, n): 

                    # Sum of two sides is greater 
                    # than the third 
                    if (arr[i] + arr[j] > arr[k] and 
                        arr[i] + arr[k] > arr[j] and 
                        arr[k] + arr[j] > arr[i]): 
                        count += 1
        return count 

    # Driver code 
    arr = [ 10, 21, 22, 100, 101, 200, 300 ] 
    size = len(arr) 

    print("Total number of triangles possible is",  
                 findNumberOfTriangles(arr, size)) 

    # This code is contributed by shubhamsingh10 

    ```

    ## C# 

    ```

    // C# code to count the number of 
    // possible triangles using brute 
    // force approach 
    using System; 

    class GFG{ 

        // Function to count all possible 
        // triangles with arr[] elements 
        static int findNumberOfTriangles(int[] arr, int n) 
        { 
            // Count of triangles 
            int count = 0; 

            // The three loops select three 
            // different values from array 
            for (int i = 0; i < n; i++) { 
                for (int j = i + 1; j < n; j++) { 

                    // The innermost loop checks for 
                    // the triangle property 
                    for (int k = j + 1; k < n; k++) 

                        // Sum of two sides is greater 
                        // than the third 
                        if ( 
                            arr[i] + arr[j] > arr[k] 
                            && arr[i] + arr[k] > arr[j] 
                            && arr[k] + arr[j] > arr[i]) 
                            count++; 
                } 
            } 
            return count; 
        } 

        // Driver code 
        static public void Main () 
        { 
            int[] arr = { 10, 21, 22, 100, 101, 200, 300 }; 
            int size = arr.Length; 

            Console.WriteLine("Total number of triangles possible is "+findNumberOfTriangles(arr, size)); 
        } 
    } 

    // This code is contributed by shubhamsingh10 

    ```

*   **输出**：

    ```
    Total number of triangles possible is 6

    ```

*   **复杂度分析**：

    *   **时间复杂度**：`O(N ^ 3)`，其中`N`是输入数组的大小。

    *   **空间复杂度**：`O(1)`。

**方法 2**：这是一种复杂而有效的方法，可以将时间复杂度从 `O(N ^ 3)`降低到`O(N ^ 2)`，三角形的两个边固定，并且可以使用这两个边找到计数。

*   **方法**：首先以升序对数组进行排序。 然后使用两个循环。 固定第一个侧面的外环和固定第二个侧面的内环，然后找到长度小于其他两个侧面的第三侧面的最远索引（大于两个侧面的索引）。 因此，可以找到一系列值的第三边，可以保证其长度大于其他各个边但小于两个边的总和。

*   **算法**： Let a, b and c be three sides. The below condition must hold for a triangle (sum of two sides is greater than the third side)

    i) a + b > c

    ii) b + c > a

    iii) a + c > b

    以下是计算三角形的步骤。

    1.  对数组升序排序。

    2.  现在运行一个嵌套循环。 外循环从头到尾运行，内循环从第一个循环的索引加一到末尾运行。 以第一循环的循环计数器为`i`，第二循环的循环计数器为`j`。 取另一个变量`k = i + 2`。

    3.  现在有两个指针`i`和`j`，其中`array[i]`和`array[j]`表示三角形的两个边。 对于固定的`i`和`j`，找到将满足三角形条件的第三边的数量。 即找到`array[k]`的最大值，使得`array[i] + array[j] > array[k]`。

    4.  因此，当我们获得最大值时，则第三方的计数为`k – j`，然后将其加到总计数中。

    5.  现在总结`i`和`j`的所有有效对，其中`i < j`。

*   **实现**：

    ## C++ 

    ```

    // C++ program to count number of triangles that can be 
    // formed from given array 
    #include <bits/stdc++.h> 
    using namespace std; 

    /* Following function is needed for library function  
    qsort(). Refer  
    http:// www.cplusplus.com/reference/clibrary/cstdlib/qsort/ */
    int comp(const void* a, const void* b) 
    { 
        return *(int*)a > *(int*)b; 
    } 

    // Function to count all possible triangles with arr[] 
    // elements 
    int findNumberOfTriangles(int arr[], int n) 
    { 
        // Sort the array elements in non-decreasing order 
        qsort(arr, n, sizeof(arr[0]), comp); 

        // Initialize count of triangles 
        int count = 0; 

        // Fix the first element. We need to run till n-3 
        // as the other two elements are selected from 
        // arr[i+1...n-1] 
        for (int i = 0; i < n - 2; ++i) { 
            // Initialize index of the rightmost third 
            // element 
            int k = i + 2; 

            // Fix the second element 
            for (int j = i + 1; j < n; ++j) { 
                // Find the rightmost element which is 
                // smaller than the sum of two fixed elements 
                // The important thing to note here is, we 
                // use the previous value of k. If value of 
                // arr[i] + arr[j-1] was greater than arr[k], 
                // then arr[i] + arr[j] must be greater than k, 
                // because the array is sorted. 
                while (k < n && arr[i] + arr[j] > arr[k]) 
                    ++k; 

                // Total number of possible triangles that can 
                // be formed with the two fixed elements is 
                // k - j - 1\. The two fixed elements are arr[i] 
                // and arr[j]. All elements between arr[j+1]/ to 
                // arr[k-1] can form a triangle with arr[i] and arr[j]. 
                // One is subtracted from k because k is incremented 
                // one extra in above while loop. 
                // k will always be greater than j. If j becomes equal 
                // to k, then above loop will increment k, because arr[k] 
                // + arr[i] is always greater than arr[k] 
                if (k > j) 
                    count += k - j - 1; 
            } 
        } 

        return count; 
    } 

    // Driver code 
    int main() 
    { 
        int arr[] = { 10, 21, 22, 100, 101, 200, 300 }; 
        int size = sizeof(arr) / sizeof(arr[0]); 

        cout << "Total number of triangles possible is " << findNumberOfTriangles(arr, size); 

        return 0; 
    } 

    // This code is contributed by rathbhupendra 

    ```

    ## C

    ```

    // C program to count number of triangles that can be 
    // formed from given array 
    #include <stdio.h> 
    #include <stdlib.h> 

    /* Following function is needed for library function 
    qsort(). Refer 
    http:// www.cplusplus.com/reference/clibrary/cstdlib/qsort/ */
    int comp(const void* a, const void* b) 
    { 
        return *(int*)a > *(int*)b; 
    } 

    // Function to count all possible triangles with arr[] 
    // elements 
    int findNumberOfTriangles(int arr[], int n) 
    { 
        // Sort the array elements in non-decreasing order 
        qsort(arr, n, sizeof(arr[0]), comp); 

        // Initialize count of triangles 
        int count = 0; 

        // Fix the first element. We need to run till n-3 
        // as the other two elements are selected from 
        // arr[i+1...n-1] 
        for (int i = 0; i < n - 2; ++i) { 
            // Initialize index of the rightmost third 
            // element 
            int k = i + 2; 

            // Fix the second element 
            for (int j = i + 1; j < n; ++j) { 
                // Find the rightmost element which is 
                // smaller than the sum of two fixed elements 
                // The important thing to note here is, we 
                // use the previous value of k. If value of 
                // arr[i] + arr[j-1] was greater than arr[k], 
                // then arr[i] + arr[j] must be greater than k, 
                // because the array is sorted. 
                while (k < n && arr[i] + arr[j] > arr[k]) 
                    ++k; 

                // Total number of possible triangles that can 
                // be formed with the two fixed elements is 
                // k - j - 1\. The two fixed elements are arr[i] 
                // and arr[j]. All elements between arr[j+1]/ to 
                // arr[k-1] can form a triangle with arr[i] and arr[j]. 
                // One is subtracted from k because k is incremented 
                // one extra in above while loop. 
                // k will always be greater than j. If j becomes equal 
                // to k, then above loop will increment k, because arr[k] 
                // + arr[i] is always greater than arr[k] 
                if (k > j) 
                    count += k - j - 1; 
            } 
        } 

        return count; 
    } 

    // Driver program to test above functionarr[j+1] 
    int main() 
    { 
        int arr[] = { 10, 21, 22, 100, 101, 200, 300 }; 
        int size = sizeof(arr) / sizeof(arr[0]); 

        printf("Total number of triangles possible is %d ", 
               findNumberOfTriangles(arr, size)); 

        return 0; 
    } 

    ```

    ## Java

    ```

    // Java program to count number of triangles that can be 
    // formed from given array 
    import java.io.*; 
    import java.util.*; 

    class CountTriangles { 
        // Function to count all possible triangles with arr[] 
        // elements 
        static int findNumberOfTriangles(int arr[]) 
        { 
            int n = arr.length; 
            // Sort the array elements in non-decreasing order 
            Arrays.sort(arr); 

            // Initialize count of triangles 
            int count = 0; 

            // Fix the first element. We need to run till n-3 as 
            // the other two elements are selected from arr[i+1...n-1] 
            for (int i = 0; i < n - 2; ++i) { 
                // Initialize index of the rightmost third element 
                int k = i + 2; 

                // Fix the second element 
                for (int j = i + 1; j < n; ++j) { 
                    /* Find the rightmost element which is smaller 
                    than the sum of two fixed elements 
                    The important thing to note here is, we use 
                    the previous value of k. If value of arr[i] + 
                    arr[j-1] was greater than arr[k], then arr[i] + 
                    arr[j] must be greater than k, because the 
                    array is sorted. */
                    while (k < n && arr[i] + arr[j] > arr[k]) 
                        ++k; 

                    /* Total number of possible triangles that can be 
                    formed with the two fixed elements is k - j - 1\. 
                    The two fixed elements are arr[i] and arr[j]. All 
                    elements between arr[j+1] to arr[k-1] can form a 
                    triangle with arr[i] and arr[j]. One is subtracted 
                    from k because k is incremented one extra in above 
                    while loop. k will always be greater than j. If j 
                    becomes equal to k, then above loop will increment 
                    k, because arr[k] + arr[i] is always/ greater than 
                    arr[k] */
                    if (k > j) 
                        count += k - j - 1; 
                } 
            } 
            return count; 
        } 

        public static void main(String[] args) 
        { 
            int arr[] = { 10, 21, 22, 100, 101, 200, 300 }; 
            System.out.println("Total number of triangles is " + findNumberOfTriangles(arr)); 
        } 
    } 
    /*This code is contributed by Devesh Agrawal*/

    ```

    ## Python

    ```

    # Python function to count all possible triangles with arr[] 
    # elements 

    def findnumberofTriangles(arr): 

        # Sort array and initialize count as 0 
        n = len(arr) 
        arr.sort() 
        count = 0

        # Fix the first element. We need to run till n-3 as 
        # the other two elements are selected from arr[i + 1...n-1] 
        for i in range(0, n-2): 

            # Initialize index of the rightmost third element 
            k = i + 2

            # Fix the second element 
            for j in range(i + 1, n): 

                # Find the rightmost element which is smaller 
                # than the sum of two fixed elements 
                # The important thing to note here is, we use 
                # the previous value of k. If value of arr[i] + 
                # arr[j-1] was greater than arr[k], then arr[i] + 
                # arr[j] must be greater than k, because the array 
                # is sorted. 
                while (k < n and arr[i] + arr[j] > arr[k]): 
                    k += 1

                # Total number of possible triangles that can be 
                # formed with the two fixed elements is k - j - 1\. 
                # The two fixed elements are arr[i] and arr[j]. All 
                # elements between arr[j + 1] to arr[k-1] can form a 
                # triangle with arr[i] and arr[j]. One is subtracted 
                # from k because k is incremented one extra in above 
                # while loop. k will always be greater than j. If j 
                # becomes equal to k, then above loop will increment k, 
                # because arr[k] + arr[i] is always greater than arr[k] 
                if(k>j): 
                    count += k - j - 1

        return count 

    # Driver function to test above function 
    arr = [10, 21, 22, 100, 101, 200, 300] 
    print "Number of Triangles:", findnumberofTriangles(arr) 

    # This code is contributed by Devesh Agrawal 

    ```

    ## C# 

    ```

    // C# program to count number 
    // of triangles that can be 
    // formed from given array 
    using System; 

    class GFG { 
        // Function to count all 
        // possible triangles 
        // with arr[] elements 
        static int findNumberOfTriangles(int[] arr) 
        { 
            int n = arr.Length; 

            // Sort the array elements 
            // in non-decreasing order 
            Array.Sort(arr); 

            // Initialize count 
            // of triangles 
            int count = 0; 

            // Fix the first element. We 
            // need to run till n-3 as 
            // the other two elements are 
            // selected from arr[i+1...n-1] 
            for (int i = 0; i < n - 2; ++i) { 
                // Initialize index of the 
                // rightmost third element 
                int k = i + 2; 

                // Fix the second element 
                for (int j = i + 1; j < n; ++j) { 
                    /* Find the rightmost element  
                    which is smaller than the sum  
                    of two fixed elements. The  
                    important thing to note here  
                    is, we use the previous value  
                    of k. If value of arr[i] +  
                    arr[j-1] was greater than arr[k],  
                    then arr[i] + arr[j] must be  
                    greater than k, because the 
                    array is sorted. */
                    while (k < n && arr[i] + arr[j] > arr[k]) 
                        ++k; 

                    /* Total number of possible triangles  
                    that can be formed with the two  
                    fixed elements is k - j - 1\. The  
                    two fixed elements are arr[i] and  
                    arr[j]. All elements between arr[j+1]  
                    to arr[k-1] can form a triangle with  
                    arr[i] and arr[j]. One is subtracted  
                    from k because k is incremented one  
                    extra in above while loop. k will  
                    always be greater than j. If j becomes 
                    equal to k, then above loop will  
                    increment k, because arr[k] + arr[i]  
                    is always/ greater than arr[k] */
                    if (k > j) 
                        count += k - j - 1; 
                } 
            } 
            return count; 
        } 

        // Driver Code 
        public static void Main() 
        { 
            int[] arr = { 10, 21, 22, 100, 
                          101, 200, 300 }; 
            Console.WriteLine("Total number of triangles is " + findNumberOfTriangles(arr)); 
        } 
    } 

    // This code is contributed by anuj_67\. 

    ```

    ## PHP

    ```

    <?php 
    // PHP program to count number  
    // of triangles that can be 
    // formed from given array 

    // Function to count all  
    // possible triangles with  
    // arr[] element 
    function findNumberOfTriangles($arr) 
    { 
        $n = count($arr); 

        // Sort the array elements  
        // in non-decreasing order 
        sort($arr); 

        // Initialize count  
        // of triangles 
        $count = 0; 

        // Fix the first element.  
        // We need to run till n-3  
        // as the other two elements 
        // are selected from  
        // arr[i+1...n-1] 
        for ($i = 0; $i < $n - 2; ++$i) 
        { 
            // Initialize index of the  
            // rightmost third element 
            $k = $i + 2; 

            // Fix the second element 
            for ($j = $i + 1; $j < $n; ++$j) 
            { 
                /* Find the rightmost element 
                which is smaller than the sum  
                of two fixed elements. The  
                important thing to note here  
                is, we use the previous value  
                of k. If value of arr[i] + 
                arr[j-1] was greater than  
                arr[k], then arr[i] + 
                arr[j] must be greater than k,  
                because the array is sorted. */
                while ($k < $n && $arr[$i] +  
                                $arr[$j] > $arr[$k]) 
                    ++$k; 

            /* Total number of possible  
                triangles that can be 
                formed with the two fixed  
                elements is k - j - 1\. 
                The two fixed elements are 
                arr[i] and arr[j]. All 
                elements between arr[j+1]  
                to arr[k-1] can form a 
                triangle with arr[i] and  
                arr[j]. One is subtracted 
                from k because k is incremented  
                one extra in above while loop.  
                k will always be greater than j.  
                If j becomes equal to k, then 
                above loop will increment k, 
                because arr[k] + arr[i] is  
                always/ greater than arr[k] */
                if($k>$j) 
                $count += $k - $j - 1; 
            } 
        } 
        return $count; 
    } 

    // Driver code 
    $arr = array(10, 21, 22, 100, 
                101, 200, 300); 
    echo"Total number of triangles is ", 
            findNumberOfTriangles($arr); 

    // This code is contributed by anuj_67\. 
    ?> 

    ```

*   **输出**：

    ```
    Total number of triangles possible is 6

    ```

*   **复杂度分析**：

    *   **时间复杂度**：`O(N ^ 2)`。

        由于 3 个嵌套循环，因此时间复杂度更高。 可以看出，在最外层循环中，`k`仅初始化一次。 最内层循环对于最外层循环的每次迭代最多执行`O(n)`时间，因为`k`从`i + 2`开始，对于所有`j`值都上升到`n`。 因此，时间复杂度为`O(N ^ 2)`。

    *   **空间复杂度**：`O(1)`。

        不需要多余的空间。 所以空间复杂度是恒定的。

**方法 3**： 仅在两个嵌套循环中使用**两个指针方法**，可以大大降低时间复杂度。

*   **方法**：首先对数组进行排序，然后运行一个嵌套循环，修复一个索引，然后尝试修复一个上下索引，在其中我们可以使用所有长度来与该固定索引形成一个三角形。

*   **算法**：

    1.  对数组进行排序，然后取三个变量`l`，`r`和`i`，分别指向`start`，`end-1`和从数组末尾开始的数组元素。

    2.  从末端（`n-1`到 1）遍历数组，对于每次迭代，保持`l = 0`和`r = i-1`的值。

    3.  现在，如果可以使用`arr[l]`和`arr[r]`形成三角形，那么显然可以从`a[l + 1], a[l + 2] ..... a[r-1], arr[r]`和`a[i]`形成三角形，**因为该数组已排序**，可以使用（`r-l`）直接计算该数组。 然后递减`r`的值并继续循环直到`l`小于`r`。

    4.  如果不能使用`arr[l]`和`arr[r]`形成三角形，则增加`r`的值并继续循环直到`l`小于`r`。

    5.  因此，降低了遍历所有数组元素的总体复杂性。

*   **实现**：

    ## C++ 

    ```

    // C++ implementation of the above approach 
    #include <bits/stdc++.h> 
    using namespace std; 

    void CountTriangles(vector<int> A) 
    { 

        int n = A.size(); 

        sort(A.begin(), A.end()); 

        int count = 0; 

        for (int i = n - 1; i >= 1; i--) { 
            int l = 0, r = i - 1; 
            while (l < r) { 
                if (A[l] + A[r] > A[i]) { 

                    // If it is possible with a[l], a[r] 
                    // and a[i] then it is also possible 
                    // with a[l+1]..a[r-1], a[r] and a[i] 
                    count += r - l; 

                    // checking for more possible solutions 
                    r--; 
                } 
                else

                    // if not possible check for 
                    // higher values of arr[l] 
                    l++; 
            } 
        } 
        cout << "No of possible solutions: " << count; 
    } 
    int main() 
    { 

        vector<int> A = { 4, 3, 5, 7, 6 }; 

        CountTriangles(A); 
    } 

    ```

    ## Java

    ```

    // Java implementation of the above approach 
    import java.util.*; 

    class GFG { 
        static void CountTriangles(int[] A) 
        { 
            int n = A.length; 

            Arrays.sort(A); 

            int count = 0; 

            for (int i = n - 1; i >= 1; i--) { 
                int l = 0, r = i - 1; 
                while (l < r) { 
                    if (A[l] + A[r] > A[i]) { 

                        // If it is possible with a[l], a[r] 
                        // and a[i] then it is also possible 
                        // with a[l+1]..a[r-1], a[r] and a[i] 
                        count += r - l; 

                        // checking for more possible solutions 
                        r--; 
                    } 
                    else // if not possible check for 
                    // higher values of arr[l] 
                    { 
                        l++; 
                    } 
                } 
            } 
            System.out.print("No of possible solutions: " + count); 
        } 

        // Driver Code 
        public static void main(String[] args) 
        { 
            int[] A = { 4, 3, 5, 7, 6 }; 

            CountTriangles(A); 
        } 
    } 

    // This code is contributed by PrinciRaj1992 

    ```

    ## Python3

    ```

    # Python implementation of the above approach 
    def CountTriangles( A): 

        n = len(A); 

        A.sort();  

        count = 0; 

        for i in range(n - 1, 0, -1): 
            l = 0; 
            r = i - 1; 
            while(l < r): 
                if(A[l] + A[r] > A[i]): 

                    # If it is possible with a[l], a[r] 
                    # and a[i] then it is also possible 
                    # with a[l + 1]..a[r-1], a[r] and a[i] 
                    count += r - l;  

                    # checking for more possible solutions 
                    r -= 1;  

                else: 

                    # if not possible check for  
                    # higher values of arr[l] 
                    l += 1;  
        print("No of possible solutions: ", count); 

    # Driver Code 
    if __name__ == '__main__': 

        A = [ 4, 3, 5, 7, 6 ];  

        CountTriangles(A); 

    # This code is contributed by PrinciRaj1992 

    ```

    ## C# 

    ```

    // C# implementation of the above approach 
    using System; 

    class GFG { 
        static void CountTriangles(int[] A) 
        { 
            int n = A.Length; 

            Array.Sort(A); 

            int count = 0; 

            for (int i = n - 1; i >= 1; i--) { 
                int l = 0, r = i - 1; 
                while (l < r) { 
                    if (A[l] + A[r] > A[i]) { 

                        // If it is possible with a[l], a[r] 
                        // and a[i] then it is also possible 
                        // with a[l+1]..a[r-1], a[r] and a[i] 
                        count += r - l; 

                        // checking for more possible solutions 
                        r--; 
                    } 
                    else // if not possible check for 
                    // higher values of arr[l] 
                    { 
                        l++; 
                    } 
                } 
            } 
            Console.Write("No of possible solutions: " + count); 
        } 

        // Driver Code 
        public static void Main(String[] args) 
        { 
            int[] A = { 4, 3, 5, 7, 6 }; 

            CountTriangles(A); 
        } 
    } 

    // This code is contributed by Rajput-Ji 

    ```

*   **输出**：

    ```
    No of possible solutions: 9

    ```

*   **复杂度分析**：

    *   **时间复杂度**：`O(n ^ 2)`。

        由于使用了两个嵌套循环，但是与上述方法相比，整体迭代大大减少了。

    *   **空间复杂度**：`O(1)`。

        由于不需要额外的空间，因此空间复杂度是恒定的。

来源： [http://stackoverflow.com/questions/8110538/total-number-of-possible-triangles-from-n-numbers](http://stackoverflow.com/questions/8110538/total-number-of-possible-triangles-from-n-numbers)

[https://www.geeksforgeeks.org/two-pointers-technique/](https://www.geeksforgeeks.org/two-pointers-technique/)

