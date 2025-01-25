# Context: 

So there was a tweet the other day...

![[traversal-binary-tree.jpg]]
https://x.com/vikhyatk/status/1873033432705712304



And apparently it's hard? - off the rip I can't code this, but I got the answer "right" at first from the top of my head, but for some reason due to how the tweet and replies were phrased I had thought that the given output was incorrect, so I made up an alternate answer: 

```
1
12
13
124
135
136
```

So I figured it's time for a refresher as I'm not the best leet-coder - and I could honestly give less of a fuck for caring about this - but I thought it'd make good dev content purely because of this quoted tweet: 

![[traversal-binary-tree-kubernetes.jpg]]
https://x.com/glcst/status/1873575831047733421

This posed as an interesting challenge, as I've no idea how'd you do it in any of those 3. It'd be good experience and something I can brag/advertise on my resume.






# Challenge: Do it in Go, Kubernetes, & SQLite

## RTFM: How to do Binary Tree Level Order Traversal

SO the first order of business is to Google how tf to do it correctly; I didn't want to use any AI because I wanted to be sure that the info was correct, so geeksforgeeks it is, then. I also didn't want to use AI because that's too easy, despite the temptation and despite the unnecessary need for "knowing" how to do it myself. I'm trying to *learn* and *understand* HOW.

Geeksforgeeks has info on how to do it in C++: 

```
https://www.geeksforgeeks.org/binary-tree-level-order-traversal-in-cpp/ 

Binary Tree Level Order Traversal in C++

Last Updated : 02 May, 2024

Trees are the type of data structure that stores the data in the form of nodes having a parent or children or both connected through edges. 
It leads to a hierarchical tree-like structure that can be traversed in multiple ways such as —preorder, inorder, postorder, and level order. 
A binary tree is a tree data structure a node can only have 2 children at max.

Level Order Traversal of Binary Tree in C++

The level order traversal is a type of Breadth First Traversal (BFS) in which we 
traverse all the nodes in the current level and then move to the next level. 
It starts from the root level and goes to the last level. Consider the below example:

            1  
          /  \  
        2      3  
     /   \       \  
   4      5       6

The level order traversal of the given tree will be: 1 2 3 4 5 6
```
https://www.geeksforgeeks.org/binary-tree-level-order-traversal-in-cpp/
![[level-order-in-cpp---animated 1.gif]]

Ok yea, top to bottom, left to right - simple. 


### This is the meat & potatoes (how it works)
GFG says the way to implement a "queue data structure" is to

#### The Logic
1. Start by pushing the root node into the queue 
	* In this case, it's 1
2. While the queue is not empty, repeat: 
	* dequeue node from front of queue
	* visit the node (typically, process or print the node's value)
	* put the left-most "child" (of the root) in the queue (if it exists)
	* put the right-most child in the queue (if it exists)
###### But what if...
*I don't know what to do if there's more in the middle, say there's 3 child nodes after the root: I'll probably get to that later*

e.g
```

             1  
          /  |  \  
        2    3    4  
      /   \   \    \  
     5     6   7    8
```

*or what do you do when there's just the 1 -> 3 and no child after 3 in the middle? We went over this in data structures, but I forget :p *



#### C++ version **with a queue**
Ok here's GFG's way to do binary traversal in C++ *with a queue*

```
// C++ program to illustrate how to implement
#include <iostream>
#include <queue>
using namespace std;

// treenode
struct Node {
    int data;
    Node* left;
    Node* right;
    Node(int value): data(value),
    left(nullptr), right(nullptr){}
};

// function for level order traversal
void levelOrderTraversal(Node* root)
{
    // checking if the tree is empty or not
    if (root == nullptr)
        return;

    // creating and initializing queue with root as first
    // element
    queue<Node*> q;
    q.push(root);

    // loop that will run till the q is empty
    while (!q.empty()) {

        // visiting current node which is nothing but
        // q.front()
        Node* node = q.front();
        q.pop();
        cout << node->data << " ";

        // pushing left child and rightchild if they exists.
        if (node->left != nullptr)
            q.push(node->left);
        if (node->right != nullptr)
            q.push(node->right);
    }
}

// driver code
int main()
{
    Node* root = new Node(1);
    root->left = new Node(2);
    root->right = new Node(3);
    root->left->left = new Node(4);
    root->left->right = new Node(5);
    root->right->right = new Node(6);

    cout << "Level Order Traversal of Binary Tree: ";
    levelOrderTraversal(root);
    return 0;
}


Output: Level Order Traversal of Binary Tree: 1 2 3 4 5 6
```

### Explaining... fyi this is an unnecessary but a useful rabbit hole

Include needed class libraries & make a namespace scope
```
// C++ program to illustrate how to implement
#include <iostream>
#include <queue>
using namespace std;
```
###### **Need of*** [**Namespace***](https://www.geeksforgeeks.org/namespace-in-c/) ***in C++***
*As the same name can’t be given to multiple [variables](https://www.geeksforgeeks.org/variables-and-keywords-in-c/), [functions](https://www.geeksforgeeks.org/functions-in-c/), [classes](https://www.geeksforgeeks.org/c-classes-and-objects/), etc. in the same scope. So, to overcome this situation, namespace is introduced.*


"Make" a tree
```
// treenode
struct Node {                          <--- structure named Node
    int data;                          <--- int variable named data
    Node* left;                        <--- pointer named left that can hold the address of another Node object
    Node* right;                       <--- pointer named right holds address of Node object
    Node(int value): data(value),      <--- Node's constructor, takes value as an argument & data(value) initializes the value to constructor
    left(nullptr), right(nullptr){}    <--- Node has no children at first
};
```

```
struct Node {
```
*Unlike Arrays, ***Structures in C++*** *are user defined data types which are used to store group of items of non-similar data types.*

```
    Node* left;
    Node* right;
```

*The asterisk (`*`) indicates that `left` is a **pointer** to a `Node`. In this context:* 
- *`Node` is the name of the structure being defined.*
- *`Node*` means that `left` is a pointer that can hold the address of another `Node` object.*

```
    Node(int value): data(value),
```
*A **constructor** for the `Node` structure. A constructor is a special function that initializes objects of the structure when they are created.*
- *`Node(int value)` takes an integer `value` as an argument.*
- *`: data(value)` is an **initializer list**, which initializes the `data` member with the value passed to the constructor. For example, if you call `Node(10)`, the `data` member will be initialized to `10`.*

```
    left(nullptr), right(nullptr)
```
*This part of the initializer list sets the `left` and `right` pointers to `nullptr`, indicating that the node has no children when it is first created. `nullptr` is a special value representing an invalid or empty pointer.*


```
// function for level order traversal
void levelOrderTraversal(Node* root)                 <--- new function
{
   // checking if the tree is empty or not
    if (root == nullptr)
        return;

    // creating and initializing queue with root as first
    // element
    queue<Node*> q;
    q.push(root);

    // loop that will run till the q is empty
    while (!q.empty()) {

        // visiting current node which is nothing but
        // q.front()
        Node* node = q.front();
        q.pop();
        cout << node->data << " ";

        // pushing left child and rightchild if they exists.
        if (node->left != nullptr)
            q.push(node->left);
        if (node->right != nullptr)
            q.push(node->right);
    }
}
```

yea just kidding im too lazy to explain this shit so i just asked Grok this time here it is read it - I want to move on to actually doing the binary tree i wanted to do

"
Here's a line-by-line analysis of the provided C++ code for level order traversal of a binary tree:

```cpp
void levelOrderTraversal(Node* root)                 <--- new function
```

- This line declares a function named levelOrderTraversal that takes a pointer to a Node as an argument. The function is void because it doesn't return anything; it prints directly to the console.

```cpp
    if (root == nullptr)
        return;
```

- Checks if the root node is null. If so, there's no tree to traverse, so the function returns immediately to avoid processing.

```cpp
    queue<Node*> q;
```

- Declares a queue to hold pointers to Node. This will be used for breadth-first traversal.

```cpp
    q.push(root);
```

- Adds the root node to the queue. This is the starting point of the traversal.

```cpp
    while (!q.empty()) {
```

- Begins a loop that continues as long as there are nodes in the queue. This ensures all levels of the tree are processed.


```cpp
        Node* node = q.front();
```

- Retrieves the front node of the queue without removing it. This node is the next to be processed.

```cpp
        q.pop();
```

- Removes the front node from the queue after processing, preparing for the next node.

```cpp
        cout << node->data << " ";
```

- Prints the data of the current node. The space after data ensures nodes are separated in output.

```cpp
        if (node->left != nullptr)
            q.push(node->left);
```

- Checks if there's a left child. If it exists, it's added to the queue for later processing. This ensures all children of a node are processed after the parent.

```cpp
        if (node->right != nullptr)
            q.push(node->right);
```

- Similar to the left child check, this adds the right child to the queue if it exists.


This function implements a level order traversal (or breadth-first traversal) where nodes at the same depth are visited before moving to the next depth level. It uses a queue to manage which nodes to visit next, ensuring that all nodes on one level are processed before moving to nodes on the next level.

"