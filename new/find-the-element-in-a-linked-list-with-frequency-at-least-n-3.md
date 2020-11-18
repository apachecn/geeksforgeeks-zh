# 在链表中查找频率至少为N / 3的元素

给定大小为 **N** 的[链表](https://www.geeksforgeeks.org/data-structures/linked-list/)，其中包含字符串作为节点值，任务是查找频率大于 **[N / 3]** 的多数字符串 ]，在链接列表中。
**注意：**确保只有一个多数字符串。

**示例：**

> **输入：**头->怪胎->怪胎-> abcd->游戏->骑士->怪胎->哈利。
> **输出：**怪胎。
> **说明：**
> 链接列表中极客字符串的频率为3，大于[7/3]，即2。
> 
> **输入：**头->热->热->冷->热->热
> **输出：**热
> [ **解释：**
> 链接列表中热字符串的频率为4，大于[5/3]，即1。

**天真的方法：**
将每个字符串的频率存储在[映射](http://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)中。 遍历地图并查找频率为**≥N / 3** 的字符串。
***时间复杂度：** O（N）*
***辅助空间：** O（N）*

**有效方法：**
这个想法基于 [Moore的投票算法](https://www.geeksforgeeks.org/majority-element/)。
找到两个候选人，并检查这两个候选人中的任何一个是否实际上是多数派。

下面是上述方法的实现：

## C ++

```

// C++ program to find an 
// element with frequency 
// of at least N / 3 
// in a linked list 

#include <bits/stdc++.h> 
using namespace std; 

// Structure of a node 
// for the linked list 
struct node { 
    string i; 
    node* next = NULL; 
}; 

// Utility function to 
// create a node 
struct node* newnode(string s) 
{ 
    struct node* temp = (struct node*) 
        malloc(sizeof(struct node)); 
    temp->i = s; 
    temp->next = NULL; 
    return temp; 
} 

// Function to find and return 
// the element with frequency 
// of at least N/3 
string Majority_in_linklist(node* head) 
{ 
    // Candidates for 
    // being the required 
    // majority element 
    string s = "", t = ""; 

    // Store the frequencies 
    // of the respective candidates 
    int p = 0, q = 0; 
    node* ptr = NULL; 

    // Iterate all nodes 
    while (head != NULL) { 
        if (s.compare(head->i) == 0) { 
            // Increase frequency 
            // of candidate s 
            p = p + 1; 
        } 
        else { 
            if (t.compare(head->i) == 0) { 
                // Increase frequency 
                // of candidate t 
                q = q + 1; 
            } 
            else { 
                if (p == 0) { 
                    // Set the new sting as 
                    // candidate for majority 
                    s = head->i; 
                    p = 1; 
                } 
                else { 
                    if (q == 0) { 
                        // Set the new sting as 
                        // second candidate 
                        // for majority 
                        t = head->i; 
                        q = 1; 
                    } 
                    else { 
                        // Decrease the frequency 
                        p = p - 1; 
                        q = q - 1; 
                    } 
                } 
            } 
        } 
        head = head->next; 
    } 
    head = ptr; 
    p = 0; 
    q = 0; 

    // Check the frequency of two 
    // final selected candidate linklist 
    while (head != NULL) { 
        if (s.compare(head->i) == 0) { 
            // Increase the frequency 
            // of first candidate 
            p = 1; 
        } 
        else { 
            if (t.compare(head->i) == 0) { 
                // Increase the frequency 
                // of second candidate 
                q = 1; 
            } 
        } 
        head = head->next; 
    } 
    // Return the string with 
    // higher frequency 
    if (p > q) { 
        return s; 
    } 
    else { 
        return t; 
    } 
} 
// Driver Code 
int main() 
{ 
    node* ptr = NULL; 
    node* head = newnode("geeks"); 
    head->next = newnode("geeks"); 
    head->next->next = newnode("abcd"); 
    head->next->next->next 
        = newnode("game"); 
    head->next->next->next->next 
        = newnode("game"); 
    head->next->next->next->next->next 
        = newnode("knight"); 
    head->next->next->next->next->next->next 
        = newnode("harry"); 
    head->next->next->next->next->next->next 
        ->next 
        = newnode("geeks"); 

    cout << Majority_in_linklist(head) << endl; 

    return 0; 
} 

```

## Python3

```

# Python3 program to find an element 
# with frequency of at least N / 3  
# in a linked list  

# Structure of a node  
# for the linked list 
class Node: 
    def __init__(self, s): 

        self.i = s 
        self.next = None

# Function to find and return  
# the element with frequency  
# of at least N/3  
def Majority_in_linklist(head): 

    # Candidates for  
    # being the required  
    # majority element  
    s, t = "", "" 

    # Store the frequencies  
    # of the respective candidates  
    p, q = 0, 0
    ptr = None

    # Iterate all nodes 
    while head != None: 
        if s == head.i: 

            # Increase frequency  
            # of candidate s  
            p = p + 1
        else: 
            if t == head.i: 

                # Increase frequency  
                # of candidate t  
                q = q + 1
            else: 
                if p == 0: 

                    # Set the new sting as  
                    # candidate for majority  
                    s = head.i 
                    p = 1
                else: 
                    if q == 0: 

                        # Set the new sting as  
                        # second candidate  
                        # for majority 
                        t = head.i 
                        q = 1
                    else: 

                        # Decrease the frequency  
                        p = p - 1
                        q = q - 1

        head = head.next

    head = ptr 
    p = 0
    q = 0

    # Check the frequency of two  
    # final selected candidate linklist  
    while head != None: 
        if s == head.i: 

            # Increase the frequency  
            # of first candidate  
            p = 1
        else: 
            if t == head.i: 

                # Increase the frequency  
                # of second candidate  
                q = 1

        head = head.next

    # Return the string with  
    # higher frequency  
    if p > q: 
        return s 
    else: 
        return t 

# Driver code 
ptr = None
head = Node("geeks")  
head.next = Node("geeks")  
head.next.next = Node("abcd")  
head.next.next.next = Node("game")  
head.next.next.next.next = Node("game")  
head.next.next.next.next.next = Node("knight")  
head.next.next.next.next.next.next = Node("harry")  
head.next.next.next.next.next.next.next = Node("geeks")  

print(Majority_in_linklist(head)) 

# This code is contributed by stutipathak31jan 

```

**Output:**

```
geeks

```

***时间复杂度：** O（N）*
***辅助空间：** O（1）*

注意读者！ 现在不要停止学习。 通过 [**DSA自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的DSA概念，并为行业做好准备。

* * *

* * *

如果您喜欢GeeksforGeeks并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至tribution@geeksforgeeks.org。 查看您的文章出现在GeeksforGeeks主页上，并帮助其他Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。