# 使用 STL 的第`K`个最小/最大元素

> 原文： [https://www.geeksforgeeks.org/kth-smallestlargest-element-using-stl/](https://www.geeksforgeeks.org/kth-smallestlargest-element-using-stl/)

给定一个数组和一个数`k`（其中`k`小于数组的大小），我们需要找到给定数组中第`k`个最小的元素。

例子：

```
Input : arr[] = {7, 10, 4, 3, 20, 15}
            k = 2
Output : 4
Smallest element is 3\. Second smallest
is 4.

Input : arr[] = {7, 10, 4, 3, 3, 15}
            k = 2
Output : 4
Even if there are more than one occurrences
of 3, answer should be 4.

Input :arr[] = {7, 10, 4, 3, 20, 15}
          k = 4
Output : 10

```



我们使用在 C++ STL 中的集合。

1.  将所有元素插入集合。

2.  [遍历设置并打印第`k`个元素。](https://www.geeksforgeeks.org/set-in-cpp-stl/)

```

// STL based C++ program to find k-th smallest 
// element. 
#include <bits/stdc++.h> 
using namespace std; 

int kthSmallest(int arr[], int n, int k) 
{ 
    // Insert all elements into the set 
    set<int> s; 
    for (int i = 0; i < n; i++) 
        s.insert(arr[i]); 

    // Traverse set and print k-th element 
    auto it = s.begin(); 
    for (int i = 0; i < k - 1; i++) 
        it++; 
    return *it; 
} 

int main() 
{ 
    int arr[] = { 12, 3, 5, 7, 3, 19 }; 
    int n = sizeof(arr) / sizeof(arr[0]), k = 2; 
    cout << "K'th smallest element is "
         << kthSmallest(arr, n, k); 
    return 0; 
} 

```

输出：

```
K'th smallest element is 5 

```

上述解决方案的时间复杂度为`O(N log N)`。 请注意，STL 中的`set`在内部使用自平衡 BST，因此搜索和插入操作的时间复杂度为`O(log n)`。

**相关文章**：

[未排序数组中第`K`个最小/最大元素 | 系列 1](https://www.geeksforgeeks.org/kth-smallestlargest-element-unsorted-array/)

[未排序数组中第`K`个最小/最大元素 | 系列 2（预期线性时间](https://www.geeksforgeeks.org/kth-smallestlargest-element-unsorted-array-set-2-expected-linear-time/)

[未排序数组中第`K`个最小/最大元素 | 系列 3（最坏情况的线性时间）](https://www.geeksforgeeks.org/kth-smallestlargest-element-unsorted-array-set-3-worst-case-linear-time/)

