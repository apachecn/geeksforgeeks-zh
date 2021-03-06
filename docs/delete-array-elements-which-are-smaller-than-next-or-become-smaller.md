# 删除小于下一个或更小的数组元素

> 原文： [https://www.geeksforgeeks.org/delete-array-elements-which-are-smaller-than-next-or-become-smaller/](https://www.geeksforgeeks.org/delete-array-elements-which-are-smaller-than-next-or-become-smaller/)

给定一个数组`arr[]`和一个数字`k`。 任务是删除小于下一个元素的`k`个元素（即，如果`arr[i] < arr[i + 1]`则删除`arr[i]`）或由于下一个元素被删除而变得小于下一个元素。

例子：

```
Input       : arr[] = { 3, 100, 1 }
              k = 1
Output      : 100, 1
Explanation : arr[0] < arr[1] means 3 is less than
              100, so delete 3

Input       : arr[] = {20, 10, 25, 30, 40}
              k = 2
Output      : 25 30 40
Explanation : First we delete 10 because it follows
              arr[i] < arr[i+1]. Then we delete 20
              because 25 is moved next to it and it
              also starts following the condition.

Input       : arr[] = { 23, 45, 11, 77, 18}
              k = 3
Output      : 77, 18
Explanation : We delete 23, 45 and 11 as they follow  
              the condition arr[i] < arr[i+1]

```



**方法**：[栈](https://www.geeksforgeeks.org/stack-data-structure-introduction-program/)用于解决此问题。 首先，我们将`arr[0]`推入栈`S`，然后将`count`初始化为 0，然后从 1 遍历到`n`，然后检查`s.top() < arr[i]`是否为`true`，然后弹出栈中的元素，如果`count == k`，则增加计数，然后我们停止循环，然后将栈的值存储在另一个数组中，然后打印该数组。

## C++ 

```cpp

// C++ program to delete elements from array. 
#include <bits/stdc++.h> 
using namespace std; 

// Function for deleting k elements 
void deleteElements(int arr[], int n, int k) 
{  
    // Create a stack and push arr[0] 
    stack<int> s; 
    s.push(arr[0]); 

    int count = 0; 

    // traversing a loop from i = 1 to n 
    for (int i=1; i<n; i++) { 

        // condition for deleting an element 
        while (!s.empty() && s.top() < arr[i]  
                            && count < k) {                                      
            s.pop(); 
            count++; 
        } 

        s.push(arr[i]); 
    } 

    // Putting elements of stack in a vector 
    // from end to begin. 
    int m = s.size(); 
    vector<int> v(m); // Size of vector is m 
    while (!s.empty()) { 

        // push element from stack to vector v 
        v[--m] = s.top(); 
        s.pop(); 
    } 

    // printing result 
    for (auto x : v) 
        cout << x << " "; 

    cout << endl; 
} 

// Driver code 
int main() 
{ 
    int n = 5, k = 2; 
    int arr[] = {20, 10, 25, 30, 40};  
    deleteElements(arr, n, k); 
    return 0; 
} 

```

## Java

```java

import java.util.*; 

//Java program to delete elements from array. 
class GFG { 

// Function for deleting k elements 
    static void deleteElements(int arr[], int n, int k) { 
        // Create a stack and push arr[0] 
        Stack<Integer> s = new Stack<>(); 
        s.push(arr[0]); 

        int count = 0; 

        // traversing a loop from i = 1 to n 
        for (int i = 1; i < n; i++) { 

            // condition for deleting an element 
            while (!s.empty() && s.peek() < arr[i] 
                    && count < k) { 
                s.pop(); 
                count++; 
            } 

            s.push(arr[i]); 
        } 

        // Putting elements of stack in a vector 
        // from end to begin. 
        int m = s.size(); 
        Integer[] v = new Integer[m]; // Size of vector is m 
        while (!s.empty()) { 

            // push element from stack to vector v 
            v[--m] = s.peek(); 
            s.pop(); 
        } 

        // printing result 
        for (Integer x : v) { 
            System.out.print(x + " "); 
        }; 

        System.out.println(""); 
    } 

// Driver code 
    public static void main(String[] args) { 
        int n = 5, k = 2; 
        int arr[] = {20, 10, 25, 30, 40}; 
        deleteElements(arr, n, k); 
    } 
} 
// This code is contributed by PrinciRaj1992 

```

## Python3

```py

# Function to delete elements 
def deleteElements(arr, n, k): 

    # create an empty stack st 
    st = [] 
    st.append(arr[0]) 

    # index to mantain the top  
    # of the stack 
    top = 0
    count = 0

    for i in range(1, n): 

        # pop till the present element  
        # is greater than stack's top 
        # element 
        while(len(st) != 0 and count < k 
                   and st[top] < arr[i]): 
            st.pop() 
            count += 1
            top -= 1

        st.append(arr[i]) 
        top += 1

    # print the remaining elements 
    for i in range(0, len(st)): 
        print(st[i], " ", end="") 

# Driver code 
k = 2
arr = [20, 10, 25, 30, 40]  
deleteElements(arr, len(arr), k) 

# This code is contributed by himan085\. 

```

## C# 

```cs

// C# program to delete elements from array. 
using System; 
using System.Collections.Generic; 

class GFG { 

    // Function for deleting k elements 
    static void deleteElements(int []arr, int n, int k)  
    { 
        // Create a stack and push arr[0] 
        Stack<int> s = new Stack<int>(); 
        s.Push(arr[0]); 

        int count = 0; 

        // traversing a loop from i = 1 to n 
        for (int i = 1; i < n; i++) 
        { 

            // condition for deleting an element 
            while (s.Count != 0 && s.Peek() < arr[i] 
                    && count < k)  
            { 
                s.Pop(); 
                count++; 
            } 

            s.Push(arr[i]); 
        } 

        // Putting elements of stack in a vector 
        // from end to begin. 
        int m = s.Count; 
        int[] v = new int[m]; // Size of vector is m 
        while (s.Count != 0)  
        { 

            // push element from stack to vector v 
            v[--m] = s.Peek(); 
            s.Pop(); 
        } 

        // printing result 
        foreach (int x in v)  
        { 
            Console.Write(x + " "); 
        }; 

        Console.Write(""); 
    } 

    // Driver code 
    public static void Main()  
    { 
        int n = 5, k = 2; 
        int []arr = {20, 10, 25, 30, 40}; 
        deleteElements(arr, n, k); 
    } 
} 

// This code is contributed by 29AjayKumar 

```

**输出**：

```
25 30 40 

```



* * *

* * *



