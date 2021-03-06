# 检查节点的元素之和是否等于给定的键值

> 原文：[https://www.geeksforgeeks.org/check-whether-the-sum-of-element-of-a-node-is-equal-to-the-given-key-value/](https://www.geeksforgeeks.org/check-whether-the-sum-of-element-of-a-node-is-equal-to-the-given-key-value/)

给定一个整数`k`和一个链表，链表的每个节点都由一对整数变量`first`和`second`来保存数据，以及一个指向列表中的下一个节点的指针。 任务是查找任何节点的数据变量之和是否等于`k`。 如果是，则打印`Yes`，否则打印`No`。

**示例**：

> **输入**：`(1, 2) -> (2, 3) -> (3, 4) -> (4, 5) -> NULL, k = 5`
>
> **输出**：`Yes`
>
> 对于第二个节点，数据变量的总和为`2 + 3 = 5`。
> 
> **输入**：`(1, 2) -> (2, 3) -> (3, 4) -> (4, 5) -> NULL, k = 15`
>
> **输出**：`No`

**方法**：遍历整个链表，直到节点的元素之和等于键值。 当节点的元素之和等于键值时，则打印`Yes`。 如果没有这样的节点，其元素的总和等于键值，则打印`No`。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation of the approach 
#include <iostream> 
using namespace std; 

// Represents node of the linked list 
struct Node { 
    int first; 
    int second; 
    Node* next; 
}; 

// Insertion in linked list 
void insert(Node** head, int f, int s) 
{ 
    Node* ptr = *head; 
    Node* temp = new Node(); 
    temp->first = f; 
    temp->second = s; 
    temp->next = NULL; 

    if (*head == NULL) 
        *head = temp; 
    else { 
        while (ptr->next != NULL) 
            ptr = ptr->next; 

        ptr->next = temp; 
    } 
} 

// Function that returns true 
// if the sum of element in a node = k 
bool checkK(Node* head, int k) 
{ 

    // Check every node of the linked list 
    while (head != NULL) { 

        // If sum of the data of the current node = k 
        if ((head->first + head->second) == k) 
            return true; 

        // Get to next node in the list 
        head = head->next; 
    } 

    // No matching node found 
    return false; 
} 
// Driver code 
int main() 
{ 
    Node* head = NULL; 
    insert(&head, 1, 2); 
    insert(&head, 2, 3); 
    insert(&head, 3, 4); 
    insert(&head, 4, 5); 
    int k = 5; 

    if (checkK(head, k)) 
        cout << "Yes"; 
    else
        cout << "No"; 

    return 0; 
} 

```

## Java

```java

// Java implementation of the approach 
class GfG { 

    // Represents node of the linked list 
    static class Node { 
        int first; 
        int second; 
        Node next; 
    } 
    static Node head = null; 

    // Insertion in linked list 
    static void insert(int f, int s) 
    { 
        Node ptr = head; 
        Node temp = new Node(); 
        temp.first = f; 
        temp.second = s; 
        temp.next = null; 

        if (head == null) 
            head = temp; 
        else { 
            while (ptr.next != null) 
                ptr = ptr.next; 

            ptr.next = temp; 
        } 
    } 

    // Function that returns true 
    // if the sum of element in a node = k 
    static boolean checkK(Node head, int k) 
    { 

        // Check every node of the linked list 
        while (head != null) { 

            // If sum of the data of the current node = k 
            if ((head.first + head.second) == k) 
                return true; 

            // Get to next node in the list 
            head = head.next; 
        } 

        // No matching node found 
        return false; 
    } 
    // Driver code 
    public static void main(String[] args) 
    { 
        // Node* head = NULL; 
        insert(1, 2); 
        insert(2, 3); 
        insert(3, 4); 
        insert(4, 5); 
        int k = 5; 

        if (checkK(head, k) == true) 
            System.out.println("Yes"); 
        else
            System.out.println("No"); 
    } 
} 

// This code is contributed by Prerna Saini 

```

## C#

```cs

using System; 

// c# implementation of the approach 
public class GfG { 

    // Represents node of the linked list 
    public class Node { 
        public int first; 
        public int second; 
        public Node next; 
    } 
    public static Node head = null; 

    // Insertion in linked list 
    public static void insert(int f, int s) 
    { 
        Node ptr = head; 
        Node temp = new Node(); 
        temp.first = f; 
        temp.second = s; 
        temp.next = null; 

        if (head == null) { 
            head = temp; 
        } 
        else { 
            while (ptr.next != null) { 
                ptr = ptr.next; 
            } 

            ptr.next = temp; 
        } 
    } 

    // Function that returns true 
    // if the sum of element in a node = k 
    public static bool checkK(Node head, int k) 
    { 

        // Check every node of the linked list 
        while (head != null) { 

            // If sum of the data of the current node = k 
            if ((head.first + head.second) == k) { 
                return true; 
            } 

            // Get to next node in the list 
            head = head.next; 
        } 

        // No matching node found 
        return false; 
    } 
    // Driver code 
    public static void Main(string[] args) 
    { 
        // Node* head = NULL; 
        insert(1, 2); 
        insert(2, 3); 
        insert(3, 4); 
        insert(4, 5); 
        int k = 5; 

        if (checkK(head, k) == true) { 
            Console.WriteLine("Yes"); 
        } 
        else { 
            Console.WriteLine("No"); 
        } 
    } 
} 

```

**输出**：

```
Yes

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。