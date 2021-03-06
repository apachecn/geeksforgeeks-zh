# 在给定的布尔矩阵中打印唯一行

> 原文： [https://www.geeksforgeeks.org/print-unique-rows/](https://www.geeksforgeeks.org/print-unique-rows/)

给定一个二进制矩阵，打印给定矩阵的所有唯一行。

**示例**：

```
Input:
        {0, 1, 0, 0, 1}
        {1, 0, 1, 1, 0}
        {0, 1, 0, 0, 1}
        {1, 1, 1, 0, 0}
Output:
    0 1 0 0 1 
    1 0 1 1 0 
    1 1 1 0 0 
Explanation: 
The rows are r1={0, 1, 0, 0, 1}, 
r2={1, 0, 1, 1, 0}, r3={0, 1, 0, 0, 1}, 
r4={1, 1, 1, 0, 0}, As r1 = r3, remove r3
and print the other rows.

Input:
        {0, 1, 0}
        {1, 0, 1}
        {0, 1, 0}
Output:
   0 1 0
   1 0 1
Explanation: 
The rows are r1={0, 1, 0}, 
r2={1, 0, 1}, r3={0, 1, 0} As r1 = r3,
remove r3 and print the other rows.

```



**方法 1**：此方法说明解决上述问题的简单方法。

*   **方法**：一种简单的方法是使用所有已处理的行检查每一行。 打印第一行。 现在，从第二行开始，针对每一行，将该行与已处理的行进行比较。 如果该行与任何已处理的行匹配，请跳过该行，否则将其打印出来。

*   **算法**：

    1.  遍历矩阵的行。

    2.  对于每一行，检查是否有比当前索引少的相似行。

    3.  如果任何两行相似，则不要打印该行。

    4.  否则打印该行。

*   **实现**：

    ```

    // Given a binary matrix of M X N of integers,  
    // you need to return only unique rows of binary array  
    #include <bits/stdc++.h> 
    using namespace std; 
    #define ROW 4  
    #define COL 5  

    // The main function that prints  
    // all unique rows in a given matrix. 
    void findUniqueRows(int M[ROW][COL]) 
    { 
        //Traverse through the matrix 
        for(int i=0; i<ROW; i++) 
        { 
            int flag=0; 

            //check if there is similar column 
            //is already printed, i.e if i and  
            //jth column match. 
            for(int j=0; j<i; j++) 
            { 
                flag=1; 

                for(int k=0; k<=COL; k++) 
                if(M[i][k]!=M[j][k]) 
                    flag=0; 

                if(flag==1) 
                break; 
            } 

            //if no row is similar 
            if(flag==0) 
            { 
                //print the row 
                for(int j=0; j<COL; j++) 
                    cout<<M[i][j]<<" "; 
                cout<<endl; 
            } 
        } 
    } 

    // Driver Code 
    int main()  
    {  
        int M[ROW][COL] = {{0, 1, 0, 0, 1},  
                           {1, 0, 1, 1, 0},  
                           {0, 1, 0, 0, 1},  
                           {1, 0, 1, 0, 0}};  

        findUniqueRows(M);  

        return 0;  
    }  

    ```

    **输出**：

    ```
    0 1 0 0 1 
    1 0 1 1 0 
    1 0 1 0 0 

    ```

*   **复杂度分析**：

    *   **时间复杂度**：`O(ROW ^ 2 x COL)`。

        因此，对于每一行，请检查是否还有其他类似的行。 因此，时间复杂度为`O(ROW ^ 2 x COL)`。

    *   **辅助空间**：`O(1)`。由于不需要额外的空间。

**方法 2**：此方法使用[二分搜索树](http://www.geeksforgeeks.org/binary-search-tree-set-1-search-and-insertion/)解决上述操作。 二分搜索树是基于节点的二进制树数据结构，具有以下属性：

*   节点的左子树仅包含键号小于节点键号的节点。

*   节点的右子树仅包含键大于该节点的键的节点。

*   左和右子树也都必须是二叉搜索树。

*   不得有重复的节点。

二分搜索树的上述属性提供了键之间的顺序，因此可以快速完成搜索，最小和最大等操作。 如果没有顺序，那么我们可能必须比较每个键以搜索给定的键。

*   **方法**：该过程必须从找到每行的十进制等效项并将它们插入 BST 开始。 众所周知，BST 的每个节点将包含两个字段，一个字段用于十进制值，另一字段用于行号。 如果节点重复，则不得插入该节点。 最后，遍历 BST 并打印相应的行。

*   **算法**：

    1.  创建一个 BST，在其中不能存储任何重复的元素。 创建一个函数以将行转换为十进制，并将十进制值转换为二进制数组。

    2.  遍历矩阵并将该行插入 BST。

    3.  遍历 BST（有序遍历）并将十进制转换为二进制数组并打印。

*   **实现**：

    ```

    // Given a binary matrix of M X N of integers,  
    // you need to return only unique rows of binary array  
    #include <bits/stdc++.h> 
    using namespace std; 
    #define ROW 4  
    #define COL 5  

    class BST  
    {  
        int data;  
        BST *left, *right;  

        public:  

        // Default constructor.  
        BST();  

        // Parameterized constructor.  
        BST(int);  

        // Insert function.  
        BST* Insert(BST *, int);  

        // Inorder traversal.  
        void Inorder(BST *);  
    };  

    //convert array to decimal 
    int convert(int arr[]) 
    { 
        int sum=0; 

        for(int i=0; i<COL; i++) 
        { 
            sum+=pow(2,i)*arr[i]; 
        } 
        return sum; 
    } 

    //print the column represented as integers 
    void print(int p) 
    { 
        for(int i=0; i<COL; i++) 
        { 
            cout<<p%2<<" "; 
            p/=2; 
        } 
        cout<<endl; 
    } 

    // Default Constructor definition.  
    BST :: BST() : data(0), left(NULL), right(NULL){}  

    // Parameterized Constructor definition.  
    BST :: BST(int value)  
    {  
        data = value;  
        left = right = NULL;  
    }  

    // Insert function definition.  
    BST* BST :: Insert(BST *root, int value)  
    {  
        if(!root)  
        {  
            // Insert the first node, if root is NULL.  
            return new BST(value);  
        }  

        //if the value is present 
        if(value == root->data) 
         return root; 

        // Insert data.  
        if(value > root->data)  
        {  
            // Insert right node data, if the 'value'  
            // to be inserted is greater than 'root' node data.  

            // Process right nodes.  
            root->right = Insert(root->right, value);  
        }  
        else
        {  
            // Insert left node data, if the 'value'  
            // to be inserted is greater than 'root' node data.  

            // Process left nodes.  
            root->left = Insert(root->left, value);  
        }  

        // Return 'root' node, after insertion.  
        return root;  
    }  

    // Inorder traversal function.  
    // This gives data in sorted order.  
    void BST :: Inorder(BST *root)  
    {  
        if(!root)  
        {  
            return;  
        }  
        Inorder(root->left);  
        print( root->data );  
        Inorder(root->right);  
    }  

    // The main function that prints  
    // all unique rows in a given matrix. 
    void findUniqueRows(int M[ROW][COL]) 
    { 

        BST b, *root = NULL; 

        //Traverse through the matrix 
        for(int i=0; i<ROW; i++) 
        { 
            //insert the row into BST 
            root=b.Insert(root,convert(M[i])); 
        } 

        //print  
        b.Inorder(root);  

    } 

    // Driver Code 
    int main()  
    {  
        int M[ROW][COL] = {{0, 1, 0, 0, 1},  
                           {1, 0, 1, 1, 0},  
                           {0, 1, 0, 0, 1},  
                           {1, 0, 1, 0, 0}};  

        findUniqueRows(M);  

        return 0;  
    }  

    ```

    **输出**：

    ```
    1 0 1 0 0 
    1 0 1 1 0 
    0 1 0 0 1 

    ```

*   **复杂度分析**：

    *   **时间复杂度**：`O(ROW x COL + ROW x log(ROW))`。

        要遍历矩阵的时间复杂度为`O(ROW x COL)`，并将其插入 BST 的时间复杂度为每行`O(log ROW)`。 因此，总体时间复杂度为`O(ROW x COL + ROW x log(ROW))`。

    *   **辅助空间**：`O(ROW)`。

        需要存储 BST `O(ROW)`空间。

**方法 3**：此方法使用 [Trie 数据结构](https://www.geeksforgeeks.org/trie-insert-and-search/)解决上述问题。 Trie 是一种有效的信息检索数据结构。 使用 Trie，可以使搜索复杂度达到最佳极限（键长度）。 如果我们将键存储在二分搜索树中，那么均衡的 BST 将需要与`M * log N`成比例的时间，其中`M`是最大字符串长度，`N`是树中键的数量。 使用 Trie，我们可以搜索`O(M)`时间的键。 但是，代价取决于 Trie 的存储要求。

**注意**：如果列数很大，此方法将导致整数溢出。

*   **方法**：

    由于矩阵是布尔型，因此可以使用 Trie 数据结构的变体，其中每个节点将有两个子代，一个为 0，另一个为 1。在 Trie 中插入每一行。 如果该行已经存在，请不要打印该行。 如果该行不在 Trie 中，请将其插入 Trie 并打印。

*   **算法**：

    1.  创建可以存储行的 Trie。

    2.  遍历矩阵并将行插入到 Trie 中。

    3.  Trie 无法存储重复项，因此重复项将被删除。

    4.  遍历 Trie 并打印行。

*   **实现**：

    ## C++ 

    ```

    // Given a binary matrix of M X N of integers,  
    // you need to return only unique rows of binary array  
    #include <bits/stdc++.h> 
    using namespace std; 
    #define ROW 4  
    #define COL 5  

    // A Trie node  
    class Node  
    {  
        public: 
        bool isEndOfCol;  
        Node *child[2]; // Only two children needed for 0 and 1  
    } ;  

    // A utility function to allocate memory 
    // for a new Trie node  
    Node* newNode()  
    {  
        Node* temp = new Node();  
        temp->isEndOfCol = 0;  
        temp->child[0] = temp->child[1] = NULL;  
        return temp;  
    }  

    // Inserts a new matrix row to Trie.  
    // If row is already present,  
    // then returns 0, otherwise insets the row and  
    // return 1  
    bool insert(Node** root, int (*M)[COL],  
                    int row, int col )  
    {  
        // base case  
        if (*root == NULL)  
            *root = newNode();  

        // Recur if there are more entries in this row  
        if (col < COL)  
            return insert (&((*root)->child[M[row][col]]),  
                                            M, row, col + 1);  

        else // If all entries of this row are processed  
        {  
            // unique row found, return 1  
            if (!((*root)->isEndOfCol))  
                return (*root)->isEndOfCol = 1;  

            // duplicate row found, return 0  
            return 0;  
        }  
    }  

    // A utility function to print a row  
    void printRow(int(*M)[COL], int row)  
    {  
        int i;  
        for(i = 0; i < COL; ++i)  
            cout << M[row][i] << " ";  
        cout << endl; 
    }  

    // The main function that prints  
    // all unique rows in a given matrix.  
    void findUniqueRows(int (*M)[COL])  
    {  
        Node* root = NULL; // create an empty Trie  
        int i;  

        // Iterate through all rows  
        for (i = 0; i < ROW; ++i)  

            // insert row to TRIE  
            if (insert(&root, M, i, 0)) 

                // unique row found, print it  
                printRow(M, i);  
    }  

    // Driver Code 
    int main()  
    {  
        int M[ROW][COL] = {{0, 1, 0, 0, 1},  
                           {1, 0, 1, 1, 0},  
                           {0, 1, 0, 0, 1},  
                           {1, 0, 1, 0, 0}};  

        findUniqueRows(M);  

        return 0;  
    }  

    // This code is contributed by rathbhupendra 

    ```

    ## C

    ```

    //Given a binary matrix of M X N of integers, you need to return only unique rows of binary array 
    #include <stdio.h> 
    #include <stdlib.h> 
    #include <stdbool.h> 

    #define ROW 4 
    #define COL 5 

    // A Trie node 
    typedef struct Node 
    { 
        bool isEndOfCol; 
        struct Node *child[2]; // Only two children needed for 0 and 1 
    } Node; 

    // A utility function to allocate memory for a new Trie node 
    Node* newNode() 
    { 
        Node* temp = (Node *)malloc( sizeof( Node ) ); 
        temp->isEndOfCol = 0; 
        temp->child[0] = temp->child[1] = NULL; 
        return temp; 
    } 

    // Inserts a new matrix row to Trie.  If row is already 
    // present, then returns 0, otherwise insets the row and 
    // return 1 
    bool insert( Node** root, int (*M)[COL], int row, int col ) 
    { 
        // base case 
        if ( *root == NULL ) 
            *root = newNode(); 

        // Recur if there are more entries in this row 
        if ( col < COL ) 
            return insert ( &( (*root)->child[ M[row][col] ] ), M, row, col+1 ); 

        else // If all entries of this row are processed 
        { 
            // unique row found, return 1 
            if ( !( (*root)->isEndOfCol ) ) 
                return (*root)->isEndOfCol = 1; 

            // duplicate row found, return 0 
            return 0; 
        } 
    } 

    // A utility function to print a row 
    void printRow( int (*M)[COL], int row ) 
    { 
        int i; 
        for( i = 0; i < COL; ++i ) 
            printf( "%d ", M[row][i] ); 
        printf("\n"); 
    } 

    // The main function that prints all unique rows in a 
    // given matrix. 
    void findUniqueRows( int (*M)[COL] ) 
    { 
        Node* root = NULL; // create an empty Trie 
        int i; 

        // Iterate through all rows 
        for ( i = 0; i < ROW; ++i ) 
            // insert row to TRIE 
            if ( insert(&root, M, i, 0) ) 
                // unique row found, print it 
                printRow( M, i ); 
    } 

    // Driver program to test above functions 
    int main() 
    { 
        int M[ROW][COL] = {{0, 1, 0, 0, 1}, 
            {1, 0, 1, 1, 0}, 
            {0, 1, 0, 0, 1}, 
            {1, 0, 1, 0, 0} 
        }; 

        findUniqueRows( M ); 

        return 0; 
    } 

    ```

    **输出**：

    ```
    0 1 0 0 1 
    1 0 1 1 0 
    1 0 1 0 0 

    ```

*   **复杂度分析**：

    *   **时间复杂度**：`O(ROW x COL)`。

        要遍历矩阵并在树中插入，时间复杂度为`O(ROW x COL)`。 该方法具有更好的时间复杂度。 同样，在打印时可以保持行的相对顺序，但会占用空间。

    *   **辅助空间**：`O(ROW x COL)`。

        需要存储 Trie `O(ROW x COL)`空间复杂度。

**方法 4**：此方法使用[`HashSet`数据结构](https://www.geeksforgeeks.org/hashset-in-java/)解决上述问题。 `HashSet`类实现`Set`接口，该接口由实际上是`HashMap`实例的哈希表支持。 不能保证集合的迭代顺序，这意味着该类不能保证元素随时间的恒定顺序。 此类允许使用`null`元素。 该类为基本操作（如添加，删除，包含和大小）提供恒定的时间性能，并假设哈希函数将元素正确分散在存储桶中。

*   **方法**：在此方法中，将整个行转换为单个字符串，然后检查是否在`HashSet`中已经存在该行。 如果存在该行，则将其保留，否则将打印唯一行并将其添加到`HashSet`中。

*   **算法**：

    1.  创建一个`HashSet`，其中行可以存储为字符串。

    2.  遍历矩阵并将该行作为字符串插入`HashSet`中。

    3.  `HashSet`无法存储重复项，因此重复项将被删除。

    4.  遍历`HashSet`并打印行。

*   **实现**：

    ## C/C++ 

    ```

    // C++ code to print unique row in a  
    // given binary matrix  
    #include<bits/stdc++.h>  
    using namespace std;  

    void printArray(int arr[][5], int row,  
                                  int col)  
    {  
        unordered_set<string> uset;  

        for(int i = 0; i < row; i++)  
        {  
            string s = "";  

            for(int j = 0; j < col; j++)  
                s += to_string(arr[i][j]);  

            if(uset.count(s) == 0)  
            {  
                uset.insert(s);  
                cout << s << endl;  

            }  
        }  
    }  

    // Driver code  
    int main() 
    {  
        int arr[][5] = {{0, 1, 0, 0, 1},  
                        {1, 0, 1, 1, 0},  
                        {0, 1, 0, 0, 1},  
                        {1, 1, 1, 0, 0}};  

        printArray(arr, 4, 5);  
    }  

    // This code is contributed by 
    // rathbhupendra 

    ```

    ## Java

    ```

    // Java code to print unique row in a  
    // given binary matrix 
    import java.util.HashSet; 

    public class GFG { 

        public static void printArray(int arr[][],  
                                   int row,int col) 
        { 

            HashSet<String> set = new HashSet<String>(); 

            for(int i = 0; i < row; i++) 
            { 
                String s = ""; 

                for(int j = 0; j < col; j++)  
                    s += String.valueOf(arr[i][j]); 

                if(!set.contains(s)) { 
                    set.add(s); 
                    System.out.println(s); 

                } 
            } 
        } 

        // Driver code 
        public static void main(String[] args) { 

            int arr[][] = { {0, 1, 0, 0, 1}, 
                            {1, 0, 1, 1, 0}, 
                            {0, 1, 0, 0, 1}, 
                            {1, 1, 1, 0, 0} }; 

            printArray(arr, 4, 5); 
        } 
    } 

    ```

    ## Python3

    ```

    # Python3 code to print unique row in a  
    # given binary matrix 

    def printArray(matrix): 

        rowCount = len(matrix) 
        if rowCount == 0: 
            return

        columnCount = len(matrix[0]) 
        if columnCount == 0: 
            return

        row_output_format = " ".join(["%s"] * columnCount) 

        printed = {} 

        for row in matrix: 
            routput = row_output_format % tuple(row) 
            if routput not in printed: 
                printed[routput] = True
                print(routput) 

    # Driver Code 
    mat = [[0, 1, 0, 0, 1],  
           [1, 0, 1, 1, 0],  
           [0, 1, 0, 0, 1], 
           [1, 1, 1, 0, 0]] 

    printArray(mat) 

    # This code is contributed by myronwalker 

    ```

    ## C# 

    ```

    using System; 
    using System.Collections.Generic; 

    // c# code to print unique row in a   
    // given binary matrix  

    public class GFG 
    { 

        public static void printArray(int[][] arr, int row, int col) 
        { 

            HashSet<string> set = new HashSet<string>(); 

            for (int i = 0; i < row; i++) 
            { 
                string s = ""; 

                for (int j = 0; j < col; j++) 
                { 
                    s += arr[i][j].ToString(); 
                } 

                if (!set.Contains(s)) 
                { 
                    set.Add(s); 
                    Console.WriteLine(s); 

                } 
            } 
        } 

        // Driver code  
        public static void Main(string[] args) 
        { 

            int[][] arr = new int[][] 
            { 
                new int[] {0, 1, 0, 0, 1}, 
                new int[] {1, 0, 1, 1, 0}, 
                new int[] {0, 1, 0, 0, 1}, 
                new int[] {1, 1, 1, 0, 0} 
            }; 

            printArray(arr, 4, 5); 
        } 
    } 

    // This code is contributed by Shrikant13 

    ```

    **输出**：

    ```
    01001
    10110
    11100

    ```

*   **复杂度分析**：

    *   **时间复杂度**：`O(ROW x COL)`。

        要遍历矩阵并将其插入`HashSet`中，时间复杂度为`O(ROW x COL)`。

    *   **辅助空间**：`O(ROW x COL)`。

        要存储`HashSet`，需要`O(ROW x COL)`空间复杂度。

*   **谢谢 Anshuman Kaushik 提出了这种方法。**

