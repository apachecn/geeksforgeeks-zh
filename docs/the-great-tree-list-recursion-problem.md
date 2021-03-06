# 较大树列表的递归问题

> 原文：[https://www.geeksforgeeks.org/the-great-tree-list-recursion-problem/](https://www.geeksforgeeks.org/the-great-tree-list-recursion-problem/)

由 Varun Bhatia 询问。

**问题**：

编写一个递归函数`treeToList(Node root)`，该函数采用一个有序的二叉树并重新排列内部指针，以从树节点中制成一个循环的双链表。 `prev`指针应存储在`small`字段中，`next`指针应存储在`large`字段中。 该列表的排列方式应使节点按升序排列。 将头指针返回到新列表。

对此进行了很好的解释和实现： [**将二叉树转换为循环双链表**](https://www.geeksforgeeks.org/convert-a-binary-tree-to-a-circular-doubly-link-list/)

**参考**：

[http://cslibrary.stanford.edu/109/TreeListRecursion.html](http://cslibrary.stanford.edu/109/TreeListRecursion.html)

