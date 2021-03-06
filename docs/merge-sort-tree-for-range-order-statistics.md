# 用于范围顺序统计信息的归并排序树

> 原文： [https://www.geeksforgeeks.org/merge-sort-tree-for-range-order-statistics/](https://www.geeksforgeeks.org/merge-sort-tree-for-range-order-statistics/)

给定一个由`n`个数字组成的数组，任务是回答以下查询：

```
kthSmallest(start, end, k) : Find the Kth smallest 
                             number in the range from array
                             index 'start' to 'end'.

```

例子：

```
Input : arr[] = {3, 2, 5, 1, 8, 9|
     Query 1: start = 2, end = 5, k = 2
     Query 2: start = 1, end = 6, k = 4
Output : 2
         5
Explanation:
[2, 5, 1, 8] represents the range from 2 to 
5 and 2 is the 2nd smallest number 
in the range[3, 2, 5, 1, 8, 9] represents 
the range from 1 to 6 and 5 is the 4th
smallest number in the range

```



关键思想是构建一个[段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)，每个节点上都有一个向量，并且该向量按排序顺序包含子范围的所有元素。 而且，如果我们观察到这种段树结构，则该结构与[归并排序算法](https://www.geeksforgeeks.org/merge-sort/)期间形成的树类似（这就是为什么将其称为归并排序树的原因）

我们使用与[归并排序树（在给定行范围内的较小或相等元素）](https://www.geeksforgeeks.org/merge-sort-tree-smaller-or-equal-elements-in-given-row-range/)中讨论的相同的实现方式。

首先，我们维护一个向量对，其中每个对`{value, index}`使得对的第一个元素代表输入数组的元素，而对的第二个元素代表其出现的索引。

现在，我们基于每个对的第一个元素对对向量进行排序。

在此之后，我们将建立一个归并排序树，其中每个节点都有一个在排序范围内的索引向量。

当我们必须回答一个查询时，我们发现第`K`个最小的数字是在左子树中还是在右子树中。 想法是使用两个二分搜索并找到左侧子树中的元素数量，以使索引位于给定的查询范围内。

令此类索引的数量为`M`。

如果`M >= K`，则意味着我们将能够在左侧子树中找到第`K`个最小的数字，因此我们在左侧子树中进行调用。

否则，第`K`个最小值位于右的子树中，但是这次我们不必寻找第`K`个最小数量，因为我们已经有第`M`个最小的`HT`了。 左子树中的范围，因此我们应该在右子树中寻找剩余部分，即第`KM`个。

这是第`K`个最小数字的索引，该索引处的值是所需的编号。

```

// CPP program to implement k-th order statistics 
#include <bits/stdc++.h> 
using namespace std; 

const int MAX = 1000; 

// Constructs a segment tree and stores tree[] 
void buildTree(int treeIndex, int l, int r,  
       vector<pair<int, int> > &a, vector<int> tree[]) 
{ 

    /* l => start of range, 
        r => ending of a range 
        treeIndex => index in the Segment Tree/Merge  
                     Sort Tree  */

    /* leaf node */
    if (l == r) { 
        tree[treeIndex].push_back(a[l].second); 
        return; 
    } 

    int mid = (l + r) / 2; 

    /* building left subtree */
    buildTree(2 * treeIndex, l, mid, a, tree); 

    /* building left subtree */
    buildTree(2 * treeIndex + 1, mid + 1, r, a, tree); 

    /* merging left and right child in sorted order */
    merge(tree[2 * treeIndex].begin(),  
          tree[2 * treeIndex].end(), 
          tree[2 * treeIndex + 1].begin(),  
          tree[2 * treeIndex + 1].end(), 
          back_inserter(tree[treeIndex])); 
} 

// Returns the Kth smallest number in query range 
int queryRec(int segmentStart, int segmentEnd,  
             int queryStart, int queryEnd, int treeIndex, 
                 int K, vector<int> tree[]) 
{ 
    /* 
        segmentStart => start of a Segment, 
        segmentEnd   => ending of a Segment, 
        queryStart   => start of a query range, 
        queryEnd     => ending of a query range, 
        treeIndex    => index in the Segment  
                        Tree/Merge Sort Tree, 
        K  => kth smallest number to find  */

    if (segmentStart == segmentEnd)  
        return tree[treeIndex][0]; 

    int mid = (segmentStart + segmentEnd) / 2; 

    // finds the last index in the segment  
    // which is <= queryEnd 
    int last_in_query_range =  
            (upper_bound(tree[2 * treeIndex].begin(), 
                          tree[2 * treeIndex].end(), 
                                          queryEnd) 
                    - tree[2 * treeIndex].begin()); 

    // finds the first index in the segment 
    // which is >= queryStart 
    int first_in_query_range =  
                (lower_bound(tree[2 * treeIndex].begin(), 
                            tree[2 * treeIndex].end(), 
                                        queryStart) 
                          - tree[2 * treeIndex].begin()); 

    int M = last_in_query_range - first_in_query_range; 

    if (M >= K) { 

        // Kth smallest is in left subtree, 
        // so recursively call left subtree for Kth  
        // smallest number 
        return queryRec(segmentStart, mid, queryStart,  
                     queryEnd, 2 * treeIndex, K, tree); 
    } 

    else { 

        // Kth smallest is in right subtree, 
        // so recursively call right subtree for the  
        // (K-M)th smallest number 
        return queryRec(mid + 1, segmentEnd, queryStart, 
               queryEnd, 2 * treeIndex + 1, K - M, tree); 
    } 
} 

// A wrapper over query() 
int query(int queryStart, int queryEnd, int K, int n, 
          vector<pair<int, int> > &a, vector<int> tree[]) 
{ 

    return queryRec(0, n - 1, queryStart - 1, queryEnd - 1,  
                                               1, K, tree); 
} 

// Driver code 
int main() 
{ 
    int arr[] = { 3, 2, 5, 1, 8, 9 }; 
    int n = sizeof(arr)/sizeof(arr[0]); 

    // vector of pairs of form {element, index} 
    vector<pair<int, int> > v; 
    for (int i = 0; i < n; i++) { 
        v.push_back(make_pair(arr[i], i)); 
    } 

    // sort the vector 
    sort(v.begin(), v.end()); 

    // Construct segment tree in tree[] 
    vector<int> tree[MAX]; 
    buildTree(1, 0, n - 1, v, tree); 

    // Answer queries 
    // kSmallestIndex hold the index of the kth smallest number 
    int kSmallestIndex = query(2, 5, 2, n, v, tree); 
    cout << arr[kSmallestIndex] << endl; 

    kSmallestIndex = query(1, 6, 4, n, v, tree); 
    cout << arr[kSmallestIndex] << endl; 

    return 0; 
} 

```

**输出**：

```
2
5

```

因此，通过在索引上建立归并排序树，我们可以得到`L`到`R`范围内的第`K`个最小数字的查询，形式为 `O(n(logn)^2)`。



* * *

* * *



