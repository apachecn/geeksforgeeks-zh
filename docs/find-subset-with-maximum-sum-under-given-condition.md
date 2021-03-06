# 在给定条件下查找总和最大的子集

> 原文：[https://www.geeksforgeeks.org/find-subset-with-maximum-sum-under-given-condition/](https://www.geeksforgeeks.org/find-subset-with-maximum-sum-under-given-condition/)

给定`n`个项目的`values[]`和`labels[]`和正整数`limit`，我们需要选择这些项目的子集。以这样的方式，子集中相同类型标签的数量应小于等于极限，并且在所有可能的子集中选择中，值的总和最大。

**示例**：

```
Input: values[] = [5, 3, 7, 1, 2],
       labels[] = [5, 7, 7, 7, 6],
       limit = 2
Output: 17
Explanation:
You can select first, second, third 
and Fifth values.
So, there is 1 value of the label 5 -> {5},
    2 value of the label 7 -> {3, 7} ,
    1 value of the label 6 -> {2}.
Final subset = {5, 3, 7, 2}
Sum  = 5 + 3 + 7 + 2 = 17.

Input: values[] = [9, 8, 7, 6, 5],
       labels[] = [5, 7, 7, 7, 6],
       limit = 2
Output: 29

```

**方法**：想法是使用[`Multimap`](https://www.geeksforgeeks.org/multimap-associative-containers-the-c-standard-template-library-stl/)和[`Hashmap`](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)解决此问题。

*   我们将所有值和相应的标签成对存储在`Multimap`中。

*   在`Multimap`中，`{values, labels}`对按升序排序。 因此，我们将反向遍历`Multimap`以获得降序对。

*   现在，我们将在答案中添加值，并将每个标签的出现次数存储在`Hashmap`中，以检查出现次数是否小于或等于限制。

下面是上述方法的实现：

```
// C++ program to Find subset with
// maximum sum under given condition.
#include <bits/stdc++.h>
using namespace std;
[
// Function to return the maximum
// sum of the subset
int MaxSumSubset(vector< int >& values,
vector< int >& labels,
int n, int limit)
{
int res = 0;
multimap< int , int > s;
unordered_map< int , int > map;
if (n == 0)
{
return 0;
}
// Pushing the pair into
// the multimap
for ( [H TG57] i = 0; i < n; i++)
{
s.insert({ values[i],
labels[i] });
}
// Traversing the multimap
// in reverse
for ( auto it = s.rbegin();
it != s.rend() && n > 0; it++)
{
if (++map[it->second] <= limit)
{
res += it->first;
n--;
}
}
return res;
}
// Driver code
int main()
{
vector< int > values = { 5, 3, 7, 1, 2 };
vector< int [HT G110]
int n = sizeof (values) / sizeof (values[0]);
int limit = 2;
cout << MaxSumSubset(values, labels,
n, limit);
return 0;
}
```

**输出**：

```
17

```

**时间复杂度**：`O(n)`，其中`N`是数组的长度。



* * *

* * *



