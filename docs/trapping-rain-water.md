# 雨水井

> 原文： [https://www.geeksforgeeks.org/trapping-rain-water/](https://www.geeksforgeeks.org/trapping-rain-water/)

给定`n`个表示海拔图的非负整数，其中每个条的宽度为 1，计算下雨后它能捕获多少水。

**示例**：

```
Input: arr[]   = {2, 0, 2}
Output: 2
Explanation:
The structure is like below

We can trap 2 units of water in the middle gap.

Input: arr[]   = {3, 0, 2, 0, 4}
Output: 7
Explanation:
Structure is like below

We can trap "3 units" of water between 3 and 2,
"1 unit" on top of bar 2 and "3 units" between 2 
and 4\.  See below diagram also.

Input: arr[] = [0, 1, 0, 2, 1, 0, 1, 3, 2, 1, 2, 1]
Output: 6

Explanation:
The structure is like below

Trap "1 unit" between first 1 and 2, "4 units" between
first 2 and 3 and "1 unit" between second last 1 and last 2 
```

[](https://practice.geeksforgeeks.org/problem-page.php?pid=281)

## 强烈建议您在继续解决方案之前，单击这里进行练习。

**基本见解**：

如果左右两边的条形较高，则数组的元素可以存储水。 可以通过找到左侧和右侧条的高度来找出要存储在每个元素中的水量。 这个想法是计算可以存储在数组的每个元素中的水量。

**示例**：

考虑数组`{3, 0, 0, 2, 0, 4}`，三个单位的水可以存储三个索引 1 和 2，一个单位的水存储在索引 3 中，并且三个水量在索引 4 处。

对于`Array[] = {3, 0, 2, 0, 4}`，存储的水等于`0 + 3 + 1 + 3 + 0 = 7`。

![](img/96e0e6cc9b00f79da825150d711c8c8e.png)

**方法 1**： 这是上述问题的简单解决方案。

*   **方法**：想法是遍历每个数组元素，并在左侧和右侧找到最高的条形。 取两个高度中的较小者。 当前元素的较小高度和高度之间的差是可以存储在此数组元素中的水量。

*   **算法**：

    1.  从头到尾遍历数组。

    2.  对于每个元素，从开始到该索引遍历数组，然后找到最大高度`a`，从当前索引遍历该数组，然后找到最大高度`b`。

    3.  将在此列中存储的水量为`min(a, b) – arr[i]`，将此值添加到存储的总水量中。

    4.  打印存储的水的总量。

*   **实现**：

    ## C++ 

    ```

    // C++ implementation of the approach 
    #include<bits/stdc++.h>  
    using namespace std;  

    // Function to return the maximum 
    // water that can be stored 
    int maxWater(int arr[], int n)  
    { 

        // To store the maximum water  
        // that can be stored 
        int res = 0; 

        // For every element of the array 
        for (int i = 1; i < n-1; i++) { 

            // Find the maximum element on its left 
            int left = arr[i]; 
            for (int j=0; j<i; j++) 
               left = max(left, arr[j]); 

            // Find the maximum element on its right    
            int right = arr[i]; 
            for (int j=i+1; j<n; j++) 
               right = max(right, arr[j]);  

           // Update the maximum water     
           res = res + (min(left, right) - arr[i]);    
        } 

        return res;  
    }  

    // Driver code 
    int main()  
    {  
        int arr[] = {0, 1, 0, 2, 1, 0, 1, 3, 2, 1, 2, 1};  
        int n = sizeof(arr)/sizeof(arr[0]);  

        cout << maxWater(arr, n);  

        return 0;  
    } 

    ```

    ## Python3

    ```

    # Python3 implementation of the approach  

    # Function to return the maximum  
    # water that can be stored  
    def maxWater(arr, n) : 

        # To store the maximum water  
        # that can be stored  
        res = 0;  

        # For every element of the array  
        for i in range(1, n - 1) :  

            # Find the maximum element on its left  
            left = arr[i];  
            for j in range(i) : 
                left = max(left, arr[j]);  

            # Find the maximum element on its right  
            right = arr[i];  

            for j in range(i + 1 , n) :  
                right = max(right, arr[j]); 

            # Update the maximum water 
            res = res + (min(left, right) - arr[i]);  

        return res;  

    # Driver code  
    if __name__ == "__main__" :  

        arr = [0, 1, 0, 2, 1, 0,  
               1, 3, 2, 1, 2, 1];  
        n = len(arr);  

        print(maxWater(arr, n));  

    # This code is contributed by AnkitRai01 

    ```

    **输出**：

    ```
    6

    ```

*   **复杂度分析**：

    *   **时间复杂度**：`O(n^2)`。

        有两个遍历数组的嵌套循环，因此时间复杂度为 `O(n^2)`。

    *   **空间复杂度**：`O(1)`。

        不需要额外的空间。

**方法 2**： 这是解决上述问题的有效方法。

*   **方法**：在先前的解决方案中，要在左侧和右侧找到最高的柱，需要遍历数组，这会降低解决方案的效率。 为了提高效率，必须在线性时间内预先计算每个小节左右两边的最高小节。 然后使用这些预先计算的值查找每个数组元素中的水量。

*   **算法**：

    1.  创建两个数组，`left`，`right`，大小为`n`。 创建一个变量`max_ = INT_MIN`。

    2.  从头到尾运行一个循环。 在每次迭代中，将`max_`更新为`max_ = max(max_, arr[i])`，并赋值`left[i] = max_`。

    3.  更新`max_ = INT_MIN`。

    4.  从头到尾运行另一个循环。 在每次迭代中，将`max_`更新为`max_ = max(max_, arr [i])`，并指定`right[i] = max_`。

    5.  从头到尾遍历数组。

    6.  将在此列中存储的水量为`min(a, b) – array[i]`，（其中`a = left[i]`和`b = right[i]`）将此值加到储水总量。

    7.  打印存储的水的总量。

*   **实现**：

    ## C++ 

    ```

    // C++ program to find maximum amount of water that can 
    // be trapped within given set of bars. 
    #include <bits/stdc++.h> 
    using namespace std; 

    int findWater(int arr[], int n) 
    { 
        // left[i] contains height of tallest bar to the 
        // left of i'th bar including itself 
        int left[n]; 

        // Right [i] contains height of tallest bar to 
        // the right of ith bar including itself 
        int right[n]; 

        // Initialize result 
        int water = 0; 

        // Fill left array 
        left[0] = arr[0]; 
        for (int i = 1; i < n; i++) 
            left[i] = max(left[i - 1], arr[i]); 

        // Fill right array 
        right[n - 1] = arr[n - 1]; 
        for (int i = n - 2; i >= 0; i--) 
            right[i] = max(right[i + 1], arr[i]); 

        // Calculate the accumulated water element by element 
        // consider the amount of water on i'th bar, the 
        // amount of water accumulated on this particular 
        // bar will be equal to min(left[i], right[i]) - arr[i] . 
        for (int i = 0; i < n; i++) 
            water += min(left[i], right[i]) - arr[i]; 

        return water; 
    } 

    // Driver program 
    int main() 
    { 
        int arr[] = { 0, 1, 0, 2, 1, 0, 1, 3, 2, 1, 2, 1 }; 
        int n = sizeof(arr) / sizeof(arr[0]); 
        cout << "Maximum water that can be accumulated is "
             << findWater(arr, n); 
        return 0; 
    }

    ```

    ## Java

    ```

    // Java program to find maximum amount of water that can 
    // be trapped within given set of bars. 

    class Test { 
        static int arr[] = new int[] { 0, 1, 0, 2, 1, 0, 1, 3, 2, 1, 2, 1 }; 

        // Method for maximum amount of water 
        static int findWater(int n) 
        { 
            // left[i] contains height of tallest bar to the 
            // left of i'th bar including itself 
            int left[] = new int[n]; 

            // Right [i] contains height of tallest bar to 
            // the right of ith bar including itself 
            int right[] = new int[n]; 

            // Initialize result 
            int water = 0; 

            // Fill left array 
            left[0] = arr[0]; 
            for (int i = 1; i < n; i++) 
                left[i] = Math.max(left[i - 1], arr[i]); 

            // Fill right array 
            right[n - 1] = arr[n - 1]; 
            for (int i = n - 2; i >= 0; i--) 
                right[i] = Math.max(right[i + 1], arr[i]); 

            // Calculate the accumulated water element by element 
            // consider the amount of water on i'th bar, the 
            // amount of water accumulated on this particular 
            // bar will be equal to min(left[i], right[i]) - arr[i] . 
            for (int i = 0; i < n; i++) 
                water += Math.min(left[i], right[i]) - arr[i]; 

            return water; 
        } 

        // Driver method to test the above function 
        public static void main(String[] args) 
        { 

            System.out.println("Maximum water that can be accumulated is " + findWater(arr.length)); 
        } 
    } 

    ```

    ## Python3

    ```

    # Python program to find maximum amount of water that can 
    # be trapped within given set of bars. 

    def findWater(arr, n): 

        # left[i] contains height of tallest bar to the 
        # left of i'th bar including itself 
        left = [0]*n 

        # Right [i] contains height of tallest bar to 
        # the right of ith bar including itself 
        right = [0]*n 

        # Initialize result 
        water = 0

        # Fill left array 
        left[0] = arr[0] 
        for i in range( 1, n): 
            left[i] = max(left[i-1], arr[i]) 

        # Fill right array 
        right[n-1] = arr[n-1] 
        for i in range(n-2, -1, -1): 
            right[i] = max(right[i + 1], arr[i]); 

        # Calculate the accumulated water element by element 
        # consider the amount of water on i'th bar, the 
        # amount of water accumulated on this particular 
        # bar will be equal to min(left[i], right[i]) - arr[i] . 
        for i in range(0, n): 
            water += min(left[i], right[i]) - arr[i] 

        return water 

    # Driver program 

    arr = [0, 1, 0, 2, 1, 0, 1, 3, 2, 1, 2, 1] 
    n = len(arr) 
    print("Maximum water that can be accumulated is", findWater(arr, n)) 

    # This code is contributed by 
    # Smitha Dinesh Semwal 

    ```

    ## C# 

    ```

    // C# program to find maximum amount of water that can 
    // be trapped within given set of bars. 
    using System; 

    class Test { 
        static int[] arr = new int[] { 0, 1, 0, 2, 1, 0, 1, 3, 2, 1, 2, 1 }; 

        // Method for maximum amount of water 
        static int findWater(int n) 
        { 
            // left[i] contains height of tallest bar to the 
            // left of i'th bar including itself 
            int[] left = new int[n]; 

            // Right [i] contains height of tallest bar to 
            // the right of ith bar including itself 
            int[] right = new int[n]; 

            // Initialize result 
            int water = 0; 

            // Fill left array 
            left[0] = arr[0]; 
            for (int i = 1; i < n; i++) 
                left[i] = Math.Max(left[i - 1], arr[i]); 

            // Fill right array 
            right[n - 1] = arr[n - 1]; 
            for (int i = n - 2; i >= 0; i--) 
                right[i] = Math.Max(right[i + 1], arr[i]); 

            // Calculate the accumulated water element by element 
            // consider the amount of water on i'th bar, the 
            // amount of water accumulated on this particular 
            // bar will be equal to min(left[i], right[i]) - arr[i] . 
            for (int i = 0; i < n; i++) 
                water += Math.Min(left[i], right[i]) - arr[i]; 

            return water; 
        } 

        // Driver method to test the above function 
        public static void Main() 
        { 

            Console.WriteLine("Maximum water that can be accumulated is " + findWater(arr.Length)); 
        } 
    } 

    // This code is contributed by vt_m. 

    ```

    ## PHP

    ```

    <?php 
    // PHP program to find maximum 
    // amount of water that can 
    // be trapped within given set of bars. 

    function findWater($arr, $n) 
    { 

        // left[i] contains height of 
        // tallest bar to the 
        // left of i'th bar including  
        // itself  

        // Right [i] contains height 
        // of tallest bar to the right  
        // of ith bar including itself 
        // $right[$n]; 

        // Initialize result 
        $water = 0; 

        // Fill left array 
        $left[0] = $arr[0]; 
        for ($i = 1; $i < $n; $i++) 
        $left[$i] = max($left[$i - 1], 
                            $arr[$i]); 

        // Fill right array 
        $right[$n - 1] = $arr[$n - 1]; 
        for ($i = $n - 2; $i >= 0; $i--) 
        $right[$i] = max($right[$i + 1],  
                               $arr[$i]); 

        // Calculate the accumulated 
        // water element by element 
        // consider the amount of  
        // water on i'th bar, the 
        // amount of water accumulated 
        // on this particular 
        // bar will be equal to min(left[i],  
        // right[i]) - arr[i] . 
        for ($i = 0; $i < $n; $i++) 
        $water += min($left[$i], $right[$i])  
                                 - $arr[$i]; 

        return $water; 
    } 

        // Driver program 
        $arr = array(0, 1, 0, 2, 1, 0, 1, 3, 2, 1, 2, 1); 
        $n = sizeof($arr); 
        echo "Maximum water that can be accumulated is ", 
            findWater($arr, $n); 

    // This code is contributed by ajit 
    ?> 

    ```

    **输出**：

    ```
    Maximum water that can be accumulated is 6
    ```

*   **复杂度分析**：

    *   **时间复杂度**：`O(n)`。

        只需要遍历数组一次，因此时间复杂度为`O(n)`。

    *   **空间复杂度**：`O(n)`。

        需要两个额外的数组，每个数组的大小为`n`。

*   **用于上述解决方案的空间优化**：代替维护两个大小为`n`的数组来存储每个元素的左右最大值，而是维护两个变量以存储最大值直到该点。 由于在任何元素处捕获的水等于`min(max_left, max_right) – arr[i]`。 首先计算从`Alo`和`Ahi`中捕获的较小元素上的水，然后移动指针，直到`lo`没有越过`hi`。

*   **实现**：

    ## C++ 

    ```

    // C++ program to find maximum amount of water that can 
    // be trapped within given set of bars. 
    // Space Complexity : O(1) 

    #include <iostream> 
    using namespace std; 

    int findWater(int arr[], int n) 
    { 
        // initialize output 
        int result = 0; 

        // maximum element on left and right 
        int left_max = 0, right_max = 0; 

        // indices to traverse the array 
        int lo = 0, hi = n - 1; 

        while (lo <= hi) { 
            if (arr[lo] < arr[hi]) { 
                if (arr[lo] > left_max) 
                    // update max in left 
                    left_max = arr[lo]; 
                else
                    // water on curr element = max - curr 
                    result += left_max - arr[lo]; 
                lo++; 
            } 
            else { 
                if (arr[hi] > right_max) 
                    // update right maximum 
                    right_max = arr[hi]; 
                else
                    result += right_max - arr[hi]; 
                hi--; 
            } 
        } 

        return result; 
    } 

    int main() 
    { 
        int arr[] = { 0, 1, 0, 2, 1, 0, 1, 3, 2, 1, 2, 1 }; 
        int n = sizeof(arr) / sizeof(arr[0]); 
        cout << "Maximum water that can be accumulated is "
             << findWater(arr, n); 
    } 

    // This code is contributed by Aditi Sharma 

    ```

    ## Java

    ```

    // JAVA Code For Trapping Rain Water 
    import java.util.*; 

    class GFG { 

        static int findWater(int arr[], int n) 
        { 
            // initialize output 
            int result = 0; 

            // maximum element on left and right 
            int left_max = 0, right_max = 0; 

            // indices to traverse the array 
            int lo = 0, hi = n - 1; 

            while (lo <= hi) { 
                if (arr[lo] < arr[hi]) { 
                    if (arr[lo] > left_max) 

                        // update max in left 
                        left_max = arr[lo]; 
                    else

                        // water on curr element = 
                        // max - curr 
                        result += left_max - arr[lo]; 
                    lo++; 
                } 
                else { 
                    if (arr[hi] > right_max) 

                        // update right maximum 
                        right_max = arr[hi]; 

                    else
                        result += right_max - arr[hi]; 
                    hi--; 
                } 
            } 

            return result; 
        } 

        /* Driver program to test above function */
        public static void main(String[] args) 
        { 
            int arr[] = { 0, 1, 0, 2, 1, 0, 1, 
                          3, 2, 1, 2, 1 }; 
            int n = arr.length; 

            System.out.println("Maximum water that "
                               + "can be accumulated is "
                               + findWater(arr, n)); 
        } 
    } 
    // This code is contributed by Arnav Kr. Mandal. 

    ```

    ## Python3

    ```

    # Python program to find 
    # maximum amount of water that can 
    # be trapped within given set of bars. 
    # Space Complexity : O(1) 

    def findWater(arr, n): 

        # initialize output 
        result = 0

        # maximum element on left and right 
        left_max = 0
        right_max = 0

        # indices to traverse the array 
        lo = 0
        hi = n-1

        while(lo <= hi):  

            if(arr[lo] < arr[hi]): 

                if(arr[lo] > left_max): 

                    # update max in left 
                    left_max = arr[lo] 
                else: 

                    # water on curr element = max - curr 
                    result += left_max - arr[lo] 
                lo+= 1

            else: 

                if(arr[hi] > right_max): 
                    # update right maximum 
                    right_max = arr[hi] 
                else: 
                    result += right_max - arr[hi] 
                hi-= 1

        return result 

    # Driver program 

    arr = [0, 1, 0, 2, 1, 0, 1, 3, 2, 1, 2, 1] 
    n = len(arr) 

    print("Maximum water that can be accumulated is ", 
            findWater(arr, n)) 

    # This code is contributed 
    # by Anant Agarwal. 

    ```

    ## C# 

    ```

    // C# Code For Trapping Rain Water 
    using System; 

    class GFG { 

        static int findWater(int[] arr, int n) 
        { 
            // initialize output 
            int result = 0; 

            // maximum element on left and right 
            int left_max = 0, right_max = 0; 

            // indices to traverse the array 
            int lo = 0, hi = n - 1; 

            while (lo <= hi) { 
                if (arr[lo] < arr[hi]) { 
                    if (arr[lo] > left_max) 

                        // update max in left 
                        left_max = arr[lo]; 
                    else

                        // water on curr element = 
                        // max - curr 
                        result += left_max - arr[lo]; 
                    lo++; 
                } 
                else { 
                    if (arr[hi] > right_max) 

                        // update right maximum 
                        right_max = arr[hi]; 

                    else
                        result += right_max - arr[hi]; 
                    hi--; 
                } 
            } 

            return result; 
        } 

        // Driver program 
        public static void Main() 
        { 
            int[] arr = { 0, 1, 0, 2, 1, 0, 1, 
                          3, 2, 1, 2, 1 }; 
            int result = Trap.findWater(arr, arr.length); 
            System.out.print(" Total trapping water: " + result); 
        } 
    } 

    // This code is contributed by vt_m. 

    ```

    ## PHP

    ```

    <?php 
    // PHP program to find maximum amount 
    // of water that can be trapped within  
    // given set of bars. 

    // Method to find maximum amount 
    // of water that can be trapped within  
    // given set of bars. 
    function findWater($arr, $n) 
    { 

        // initialize output 
        $result = 0; 

        // maximum element on  
        // left and right 
        $left_max = 0;  
        $right_max = 0; 

        // indices to traverse  
        // the array 
        $lo = 0; $hi = $n - 1; 

        while($lo <= $hi)  
        { 
            if($arr[$lo] < $arr[$hi]) 
            { 
                if($arr[$lo] > $left_max) 

                    // update max in left 
                    $left_max = $arr[$lo]; 

                else

                    // water on curr  
                    // element = max - curr 
                    $result += $left_max - $arr[$lo]; 
                    $lo++; 
            } 
            else
            { 
                if($arr[$hi] > $right_max) 

                    // update right maximum 
                    $right_max = $arr[$hi]; 
                else
                    $result += $right_max - $arr[$hi]; 
                    $hi--; 
            } 
        } 

        return $result; 
    } 

        // Driver Code 
        $arr = array(0, 1, 0, 2, 1, 0,  
                     1, 3, 2, 1, 2, 1); 
        $n = count($arr); 
        echo "Maximum water that can be accumulated is ", findWater($arr, $n);  

    // This code is contributed by anuj_67\. 
    ?> 

    ```

    **输出**：

    ```
    Maximum water that can be accumulated is 6

    ```

*   **复杂度分析**：

    *   **时间复杂度**：`O(n)`。

        仅需要遍历数组一次。

    *   **辅助空间**：`O(1)`。

        由于不需要额外的空间。

*   **感谢 Gaurav Ahirwar 和 Aditi Sharma 提出的上述解决方案。**

**方法 3**：这里显示了另一个有效的解决方案。

*   **方法**：这里的概念是，如果右侧有较大的墙，则可以保留与左侧较小的墙相同高度的水。 如果右侧没有较大的墙，则从左侧开始。 现在左侧必须有一堵更大的墙。 让我们举个例子，如果高度为`{..., 3, 2, 1, 4, ...}`，那么这里 3 和 4 是边界，高度 2 和 1 被淹没并且不能充当边界。 因此，在数组的其余部分中存在更高或相等长度的边界时，在任何点或索引处都知道前一个边界就足够了。 如果不是，则向后遍历数组，现在必须在左侧留一堵更大的墙。

*   **算法**：

    *   从索引 0 到给定数组的末尾执行循环。

    *   如果遇到大于或等于前一个墙的墙，请在称为`prev_index`的变量中记录该墙的索引。

    *   继续将前一堵墙的高度减去当前（`i`）墙的高度添加到可变水量中。

    *   有一个`temp`变量，该变量存储与`water`相同的值。

    *   如果没有发现大于或等于前一个墙的墙，则退出。

    *   如果输入数组的大小大于`prev_index`，则从水中减去`temp`变量，然后从输入数组的末尾循环到`prev_index`，并找到大于或等于前一面的墙（在这种情况下，从后向后的最后一面墙） ）。

*   **实现**：

    ## Java

    ```

    // Java implementation of the approach 
    class GFG { 

        // Function to return the maximum 
        // water that can be stored 
        public static int maxWater(int arr[], int n) 
        { 
            int size = n - 1; 

            // Let the first element be stored as 
            // previous, we shall loop from index 1 
            int prev = arr[0]; 

            // To store previous wall's index 
            int prev_index = 0; 
            int water = 0; 

            // To store the water until a larger wall 
            // is found, if there are no larger walls 
            // then delete temp value from water 
            int temp = 0; 
            for (int i = 1; i <= size; i++) { 

                // If the current wall is taller than 
                // the previous wall then make current 
                // wall as the previous wall and its 
                // index as previous wall's index 
                // for the subsequent loops 
                if (arr[i] >= prev) { 
                    prev = arr[i]; 
                    prev_index = i; 

                    // Because larger or same height wall is found 
                    temp = 0; 
                } 
                else { 

                    // Since current wall is shorter than 
                    // the previous, we subtract previous 
                    // wall's height from the current wall's 
                    // height and add it to the water 
                    water += prev - arr[i]; 

                    // Store the same value in temp as well 
                    // If we dont find any larger wall then 
                    // we will subtract temp from water 
                    temp += prev - arr[i]; 
                } 
            } 

            // If the last wall was larger than or equal 
            // to the previous wall then prev_index would 
            // be equal to size of the array (last element) 
            // If we didn't find a wall greater than or equal 
            // to the previous wall from the left then 
            // prev_index must be less than the index 
            // of the last element 
            if (prev_index < size) { 

                // Temp would've stored the water collected 
                // from previous largest wall till the end 
                // of array if no larger wall was found then 
                // it has excess water and remove that 
                // from 'water' var 
                water -= temp; 

                // We start from the end of the array, so previous 
                // should be assigned to the last element 
                prev = arr[size]; 

                // Loop from the end of array up to the 'previous index' 
                // which would contain the "largest wall from the left" 
                for (int i = size; i >= prev_index; i--) { 

                    // Right end wall will be definitely smaller 
                    // than the 'previous index' wall 
                    if (arr[i] >= prev) { 
                        prev = arr[i]; 
                    } 
                    else { 
                        water += prev - arr[i]; 
                    } 
                } 
            } 

            // Return the maximum water 
            return water; 
        } 

        // Driver code 
        public static void main(String[] args) 
        { 
            int arr[] = { 0, 1, 0, 2, 1, 0, 1, 3, 2, 1, 2, 1 }; 
            int n = arr.length; 
            System.out.print(maxWater(arr, n)); 
        } 
    } 

    ```

    ## Python3

    ```

    # Pythpn3 implementation of the approach 

    # Function to return the maximum 
    # water that can be stored 
    def maxWater(arr, n): 
        size = n - 1

        # Let the first element be stored as 
        # previous, we shall loop from index 1 
        prev = arr[0] 

        # To store previous wall's index 
        prev_index = 0
        water = 0

        # To store the water until a larger wall 
        # is found, if there are no larger walls 
        # then delete temp value from water 
        temp = 0
        for i in range(1, size + 1): 

            # If the current wall is taller than 
            # the previous wall then make current 
            # wall as the previous wall and its 
            # index as previous wall's index 
            # for the subsequent loops 
            if (arr[i] >= prev): 
                prev = arr[i] 
                prev_index = i 

                # Because larger or same height wall is found 
                temp = 0
            else: 

                # Since current wall is shorter than 
                # the previous, we subtract previous 
                # wall's height from the current wall's 
                # height and add it to the water 
                water += prev - arr[i] 

                # Store the same value in temp as well 
                # If we dont find any larger wall then 
                # we will subtract temp from water 
                temp += prev - arr[i] 

        # If the last wall was larger than or equal 
        # to the previous wall then prev_index would 
        # be equal to size of the array (last element) 
        # If we didn't find a wall greater than or equal 
        # to the previous wall from the left then 
        # prev_index must be less than the index 
        # of the last element 
        if (prev_index < size): 

            # Temp would've stored the water collected 
            # from previous largest wall till the end 
            # of array if no larger wall was found then 
            # it has excess water and remove that 
            # from 'water' var 
            water -= temp 

            # We start from the end of the array, so previous 
            # should be assigned to the last element 
            prev = arr[size] 

            # Loop from the end of array up to the 'previous index' 
            # which would contain the "largest wall from the left" 
            for i in range(size, prev_index - 1, -1): 

                # Right end wall will be definitely smaller 
                # than the 'previous index' wall 
                if (arr[i] >= prev): 
                    prev = arr[i] 
                else: 
                    water += prev - arr[i] 

        # Return the maximum water 
        return water 

    # Driver code 
    arr = [0, 1, 0, 2, 1, 0, 1, 3, 2, 1, 2, 1] 
    n = len(arr) 
    print(maxWater(arr, n)) 

    # This code is contributed by Mohit Kumar 

    ```

    **输出**：

    ```
    6

    ```

*   **复杂度分析**：

    *   **时间复杂度**：`O(n)`。

        由于仅需要遍历数组一次。

    *   **辅助空间**：`O(1)`。

        由于不需要额外的空间。

