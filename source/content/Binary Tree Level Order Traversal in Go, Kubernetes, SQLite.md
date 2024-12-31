# Context: 

So there was a tweet the other day...

![[traversal-binary-tree.jpg]]
https://x.com/vikhyatk/status/1873033432705712304

And apparently it's hard - off the rip I can't code this, but I got the answer "right" at first from the top of my head, but for some reason due to how the tweet and replies were phrased I had thought that the given output was incorrect, so I made up an alternate answer: 

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

SO the first order of business is to Google how tf to do it correctly; I didn't want to use any AI because I wanted to be sure that the info was correct, so geeksforgeeks it is, then.

Geeksforgeeks has info on how to do it in C++: 

```
https://www.geeksforgeeks.org/binary-tree-level-order-traversal-in-cpp/ 

Binary Tree Level Order Traversal in C++

Last Updated : 02 May, 2024

Trees are the type of data structure that stores the data in the form of nodes having a parent or children or both connected through edges. It leads to a hierarchical tree-like structure that can be traversed in multiple ways such as —preorder, inorder, postorder, and level order. A binary tree is a tree data structure a node can only have 2 children at max.

Level Order Traversal of Binary Tree in C++

The level order traversal is a type of Breadth First Traversal (BFS) in which we traverse all the nodes in the current level and then move to the next level. It starts from the root level and goes to the last level. Consider the below example:

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

