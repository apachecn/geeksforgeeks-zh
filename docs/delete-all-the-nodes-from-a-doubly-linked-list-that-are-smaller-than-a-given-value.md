# 从双链表中删除所有小于给定值的节点

> 原文：[https://www.geeksforgeeks.org/delete-all-the-nodes-from-a-doubly-linked-list-that-are-smaller-than-a-given-value/](https://www.geeksforgeeks.org/delete-all-the-nodes-from-a-doubly-linked-list-that-are-smaller-than-a-given-value/)

给定一个包含`N`个节点和数字`K`的双链表，任务是从列表中删除所有小于给定值`K`的节点。

**示例**：

```
Input: 15 <=> 16 <=> 10 <=> 9 <=> 6 <=> 7 <=> 17
       K = 10
Output: 15 <=> 16 <=> 10 <=> 17

Input: 5 <=> 3 <=> 6 <=> 8 <=> 4 <=> 1 <=> 2 <=> 9
       K = 4 
Output: 5 <=> 6 <=> 8 <=> 4 <=> 9

```

**方法**：遍历双链表的节点，并获得数据值小于`K`的节点的指针。 请参阅[从双链表中删除节点](https://www.geeksforgeeks.org/delete-a-node-in-a-doubly-linked-list/)的文章以删除节点。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation to delete all 
// the nodes from the doubly 
// linked list that are smaller than 
// the specified value K 
#include <bits/stdc++.h> 

using namespace std; 

// Node of the doubly linked list 
struct Node { 
    int data; 
    Node *prev, *next; 
}; 

// function to insert a node at the beginning 
// of the Doubly Linked List 
void push(Node** head_ref, int new_data) 
{ 
    // allocate node 
    Node* new_node = (Node*)malloc(sizeof(struct Node)); 

    // put in the data 
    new_node->data = new_data; 

    // since we are adding at the beginning, 
    // prev is always NULL 
    new_node->prev = NULL; 

    // link the old list off the new node 
    new_node->next = (*head_ref); 

    // change prev of head node to new node 
    if ((*head_ref) != NULL) 
        (*head_ref)->prev = new_node; 

    // move the head to point to the new node 
    (*head_ref) = new_node; 
} 

// function to delete a node in a Doubly Linked List. 
// head_ref --> pointer to head node pointer. 
// del  -->  pointer to node to be deleted 
void deleteNode(Node** head_ref, Node* del) 
{ 
    // base case 
    if (*head_ref == NULL || del == NULL) 
        return; 

    // If node to be deleted is head node 
    if (*head_ref == del) 
        *head_ref = del->next; 

    // Change next only if node to be 
    // deleted is NOT the last node 
    if (del->next != NULL) 
        del->next->prev = del->prev; 

    // Change prev only if node to be 
    // deleted is NOT the first node 
    if (del->prev != NULL) 
        del->prev->next = del->next; 

    // Finally, free the memory occupied by del 
    free(del); 

    return; 
} 

// function to delete all the nodes 
// from the doubly linked 
// list that are smaller than the 
// specified value K 
void deletesmallerNodes(Node** head_ref, int K) 
{ 
    Node* ptr = *head_ref; 
    Node* next; 

    while (ptr != NULL) { 
        next = ptr->next; 
        // if true, delete node 'ptr' 
        if (ptr->data < K) 
            deleteNode(head_ref, ptr); 
        ptr = next; 
    } 
} 

// function to print nodes in a 
// given doubly linked list 
void printList(Node* head) 
{ 
    while (head != NULL) { 
        cout << head->data << " "; 
        head = head->next; 
    } 
} 

// Driver program to test above 
int main() 
{ 
    // start with the empty list 
    Node* head = NULL; 

    // create the doubly linked list 
    // 15 <-> 16 <-> 10 <-> 9 <-> 6 <-> 7 <-> 17 
    push(&head, 17); 
    push(&head, 7); 
    push(&head, 6); 
    push(&head, 9); 
    push(&head, 10); 
    push(&head, 16); 
    push(&head, 15); 

    int K = 10; 

    cout << "Original List: "; 
    printList(head); 

    deletesmallerNodes(&head, K); 

    cout << "\nModified List: "; 
    printList(head); 
} 

```

## Java

```java

// Java implementation to delete all  
// the nodes from the doubly  
// linked list that are smaller than  
// the specified value K  
class GFG 
{ 

// Node of the doubly linked list  
static class Node  
{  
    int data;  
    Node prev, next;  
};  

// function to insert a node at the beginning  
// of the Doubly Linked List  
static Node push(Node head_ref, int new_data)  
{  
    // allocate node  
    Node new_node =new Node();  

    // put in the data  
    new_node.data = new_data;  

    // since we are adding at the beginning,  
    // prev is always null  
    new_node.prev = null;  

    // link the old list off the new node  
    new_node.next = (head_ref);  

    // change prev of head node to new node  
    if ((head_ref) != null)  
        (head_ref).prev = new_node;  

    // move the head to point to the new node  
    (head_ref) = new_node; 

    return head_ref; 
}  

// function to delete a node in a Doubly Linked List.  
// head_ref -. pointer to head node pointer.  
// del -. pointer to node to be deleted  
static Node deleteNode(Node head_ref, Node del)  
{  
    // base case  
    if (head_ref == null || del == null)  
        return null;  

    // If node to be deleted is head node  
    if (head_ref == del)  
        head_ref = del.next;  

    // Change next only if node to be  
    // deleted is NOT the last node  
    if (del.next != null)  
        del.next.prev = del.prev;  

    // Change prev only if node to be  
    // deleted is NOT the first node  
    if (del.prev != null)  
        del.prev.next = del.next;  

    return head_ref;  
}  

// function to delete all the nodes  
// from the doubly linked  
// list that are smaller than the  
// specified value K  
static Node deletesmallerNodes(Node head_ref, int K)  
{  
    Node ptr = head_ref;  
    Node next;  

    while (ptr != null) 
    {  
        next = ptr.next; 

        // if true, delete node 'ptr'  
        if (ptr.data < K)  
            deleteNode(head_ref, ptr);  
        ptr = next;  
    }  
    return head_ref; 
}  

// function to print nodes in a  
// given doubly linked list  
static void printList(Node head)  
{  
    while (head != null)  
    {  
        System.out.print( head.data + " ");  
        head = head.next;  
    }  
}  

// Driver code  
public static void main(String args[]) 
{  
    // start with the empty list  
    Node head = null;  

    // create the doubly linked list  
    // 15 <. 16 <. 10 <. 9 <. 6 <. 7 <. 17  
    head=push(head, 17);  
    head=push(head, 7);  
    head=push(head, 6);  
    head=push(head, 9);  
    head=push(head, 10);  
    head=push(head, 16);  
    head=push(head, 15);  

    int K = 10;  

    System.out.print("Original List: ");  
    printList(head);  

    head=deletesmallerNodes(head, K);  

    System.out.print("\nModified List: ");  
    printList(head);  
}  
} 

// This code is contributed by Arnab Kundu 

```

## Python3

```py

# Python3 implementation to delete all 
# the nodes from the doubly 
# linked list that are smaller than 
# the specified value K 
import math 

# Node of the doubly linked list 
class Node:  
    def __init__(self, data):  
        self.data = data  
        self.next = None

# function to insert a node at the beginning 
# of the Doubly Linked List 
def push(head_ref, new_data): 

    # allocate node 
    new_node = Node(new_data) 

    # put in the data 
    new_node.data = new_data 

    # since we are adding at the beginning, 
    # prev is always None 
    new_node.prev = None

    # link the old list off the new node 
    new_node.next = head_ref 

    # change prev of head node to new node 
    if (head_ref != None): 
        head_ref.prev = new_node 

    # move the head to po to the new node 
    head_ref = new_node 
    return head_ref 

# function to delete a node in a Doubly Linked List. 
# head_ref --> poer to head node poer. 
# del --> poer to node to be deleted 
def deleteNode(head_ref, delete): 

    # base case 
    if (head_ref == None or delete == None): 
        return None

    # If node to be deleted is head node 
    if (head_ref == delete): 
        head_ref = delete.next

    # Change next only if node to be 
    # deleted is NOT the last node 
    if (delete.next != None): 
        delete.next.prev = delete.prev 

    # Change prev only if node to be 
    # deleted is NOT the first node 
    if (delete.prev != None): 
        delete.prev.next = delete.next

    # Finally, free the memory occupied by del 
    # free(delete) 
    return head_ref 

# function to delete all the nodes 
# from the doubly linked 
# list that are smaller than the 
# specified value K 
def deletesmallerNodes(head_ref, K): 
    ptr = head_ref 
    next = None

    while (ptr != None) : 
        next = ptr.next

        # if true, delete node 'ptr' 
        if (ptr.data < K): 
            deleteNode(head_ref, ptr) 
        ptr = next

# function to pr nodes in a 
# given doubly linked list 
def prList(head): 
    while (head != None): 
        print(head.data, end = " ") 
        head = head.next

# Driver Code 
if __name__=='__main__':  

    # start with the empty list 
    head = None

    # create the doubly linked list 
    # 15 <. 16 <. 10 <. 9 <. 6 <. 7 <. 17 
    head = push(head, 17) 
    head = push(head, 7) 
    head = push(head, 6) 
    head = push(head, 9) 
    head = push(head, 10) 
    head = push(head, 16) 
    head = push(head, 15) 

    K = 10

    print("Original List: ", end = "") 
    prList(head) 

    deletesmallerNodes(head, K) 

    print("\nModified List: ", end = "") 
    prList(head) 

# This code is contributed by AbhiThakur 

```

## C#

```cs

// C# implementation to delete all  
// the nodes from the doubly  
// linked list that are smaller than  
// the specified value K  
using System; 

class GFG 
{ 

// Node of the doubly linked list  
public class Node  
{  
    public int data;  
    public Node prev, next;  
};  

// function to insert a node at the beginning  
// of the Doubly Linked List  
static Node push(Node head_ref, int new_data)  
{  
    // allocate node  
    Node new_node = new Node();  

    // put in the data  
    new_node.data = new_data;  

    // since we are adding at the beginning,  
    // prev is always null  
    new_node.prev = null;  

    // link the old list off the new node  
    new_node.next = (head_ref);  

    // change prev of head node to new node  
    if ((head_ref) != null)  
        (head_ref).prev = new_node;  

    // move the head to point to the new node  
    (head_ref) = new_node; 

    return head_ref; 
}  

// function to delete a node in a Doubly Linked List.  
// head_ref -. pointer to head node pointer.  
// del -. pointer to node to be deleted  
static Node deleteNode(Node head_ref, Node del)  
{  
    // base case  
    if (head_ref == null || del == null)  
        return null;  

    // If node to be deleted is head node  
    if (head_ref == del)  
        head_ref = del.next;  

    // Change next only if node to be  
    // deleted is NOT the last node  
    if (del.next != null)  
        del.next.prev = del.prev;  

    // Change prev only if node to be  
    // deleted is NOT the first node  
    if (del.prev != null)  
        del.prev.next = del.next;  

    return head_ref;  
}  

// function to delete all the nodes  
// from the doubly linked  
// list that are smaller than the  
// specified value K  
static Node deletesmallerNodes(Node head_ref, int K)  
{  
    Node ptr = head_ref;  
    Node next;  

    while (ptr != null) 
    {  
        next = ptr.next; 

        // if true, delete node 'ptr'  
        if (ptr.data < K)  
            deleteNode(head_ref, ptr);  
        ptr = next;  
    }  
    return head_ref; 
}  

// function to print nodes in a  
// given doubly linked list  
static void printList(Node head)  
{  
    while (head != null)  
    {  
        Console.Write( head.data + " ");  
        head = head.next;  
    }  
}  

// Driver code  
public static void Main(String []args) 
{  
    // start with the empty list  
    Node head = null;  

    // create the doubly linked list  
    // 15 <. 16 <. 10 <. 9 <. 6 <. 7 <. 17  
    head = push(head, 17);  
    head = push(head, 7);  
    head = push(head, 6);  
    head = push(head, 9);  
    head = push(head, 10);  
    head = push(head, 16);  
    head = push(head, 15);  

    int K = 10;  

    Console.Write("Original List: ");  
    printList(head);  

    head=deletesmallerNodes(head, K);  

    Console.Write("\nModified List: ");  
    printList(head);  
}  
} 

// This code contributed by Rajput-Ji 

```

**输出**：

```
Original List: 15 16 10 9 6 7 17 
Modified List: 15 16 10 17

```

**时间复杂度**：`O(n)`，其中`N`是节点总数。



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。