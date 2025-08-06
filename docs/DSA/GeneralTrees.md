# General Trees

- A General Tree is a hierarchical data structure in which each node can have any number of children—unlike a binary tree, which limits each node to at most two children.

- It models complex relationships like:
    - File systems (folders can contain files or other folders)
    - Organizational charts (manager with multiple employees)
    - XML/JSON structures

### Tree

- A tree:
    - Has one root node (topmost)
    - All other nodes are its descendants, forming disjoint subtrees
    - It’s acyclic (no loops)
    - Connected (every node is reachable from the root)

- Python Representation of a Node

```py
class TreeNode:
    def __init__(self, value):
        self.value = value
        self.children = []  # list of child TreeNode objects
```

## Terminologies

| Term               | Meaning                                         |
| ------------------ | ----------------------------------------------- |
| **Root**           | Topmost node (only one)                         |
| **Parent / Child** | Direct hierarchical connection                  |
| **Siblings**       | Nodes with the same parent                      |
| **Leaf Node**      | Node with **no children**                       |
| **Internal Node**  | Node with **at least one child**                |
| **Edge**           | Link between parent and child                   |
| **Path**           | Sequence of connected nodes                     |
| **Depth of Node**  | No. of edges from **root to node**              |
| **Height of Node** | No. of edges from **node to a leaf node**       |
| **Height of Tree** | Height of the **root** node                     |
| **Degree of Node** | Number of **children** a node has               |

## Tree Traversals

- Tree traversal is the process of visiting each node in a tree exactly once in a systematic way.

###  1. Depth-First Traversal (DFT)

- Go as deep as possible along one path before backtracking.

- We have two variant for DFT: Pre-Order and Post-Order

#### a. Pre-Order Traversal:
- Visit node first, then recursively visit all its children.
- Node → Child 1 → Subtree of Child 1 → Child 2 → ...

    ```
               1
            /  |   \
           2   3    4
          / \  / \  / \
         5  6 7  8 9  10
    ```
    - Preorder Traversal: 1 2 5 6 3 7 8 4 9 10

    ```py
    def preorder(node):
        if not node:
            return
        print(node.value)  # Visit node
        for child in node.children:
            preorder(child)
    ```

#### b. Post-Order Traversal:

- Visit children first, then the node itself.
- Child 1 → Subtree → ... → Node
    ```
           1
        /  |   \
       2   3    4
      / \  / \  / \
      5  6 7  8 9  10
    ```
    - Postorder Traversal: 5 6 2 7 8 3 9 10 4 1

    ```py
    def postorder(node):
        if not node:
            return
        for child in node.children:
            postorder(child)
        print(node.value)  # Visit after children

    ```

### 2. Breadth-First Traversal (BFT) (aka Level Order Traversal)

- Visit nodes level by level, starting from the root.

- Use a Queue to keep track of nodes to be processed.

    ```
              A
            / | \
           B  C  D
          / \
         E   F
    ```
    - Level Order Output: A B C D E F

    ```py
    from collections import deque

    def level_order(root):
        if not root:
            return
        queue = deque([root])
        while queue:
            node = queue.popleft()
            print(node.value)
            queue.extend(node.children)
    ```

## 🌳 Types of Trees (Simplified)

### 1. General Tree
- Each node can have any number of children.
- Example: Family tree, folder structure.

### 2. Binary Tree
- Each node has at most 2 children: left and right.
- Simple and commonly used in programming.

### 3. Full Binary Tree
- Every node has either 0 or 2 children.
- No node has only 1 child.

### 4. Perfect Binary Tree
- All internal nodes have 2 children.
- All leaves are at the same level.

### 5. Complete Binary Tree
- All levels are filled except maybe the last.
- Last level is filled from left to right.

### 6. Skewed Binary Tree
- All nodes have only one child.
  - Left Skewed: All go to the left.
  - Right Skewed: All go to the right.

### 7. Binary Search Tree (BST)
- Left child < Parent < Right child
- Fast for search, insert, delete (if balanced).

### 8. AVL Tree
- A self-balancing BST.
- Keeps height balanced for better performance.

### 9. Red-Black Tree
- A type of balanced BST using Red/Black rules.
- Used in many libraries and databases.

### 10. B-Tree
- A general tree with many children per node.
- Used in databases for storing large data.

### 11. B+ Tree
- Like B-Tree but only stores data in leaf nodes.
- Fast range queries. Used in databases.

### 12. Heap (Binary Heap)
- A complete binary tree:
  - Min-Heap: Parent ≤ Children
  - Max-Heap: Parent ≥ Children
- Used in priority queues.

### 13. Trie (Prefix Tree)
- Tree used to store words or prefixes.
- Each character is a node.
- Fast word search (e.g., autocomplete).

### 14. Segment Tree
- Used to answer range queries (e.g., sum from index 2 to 6).
- Built over an array.

### 15. Fenwick Tree (Binary Indexed Tree)
- Similar to segment tree, but more space-efficient.
- Used for prefix sums and updates.

### 16. N-ary Tree
- Each node has at most N children (e.g., 3-ary, 4-ary).
- Example: File system tree with many folders.

### 17. Suffix Tree
- Stores all suffixes of a string.
- Helps in fast pattern matching (e.g., in DNA search).


## 🌳 In-order vs Pre-order vs Post-order Traversal (3-level Binary Tree)

Let's use the following tree with 3 levels:

```
         1
       /   \
      2     3
     / \   / \
    4   5 6   7
```

All internal nodes (1, 2, 3) have 2 children.

---

### ✅ In-order (Left ➡️ Root ➡️ Right)
1. Traverse left subtree
2. Visit current node
3. Traverse right subtree

🔁 Steps:
- Traverse left subtree of 1 → node 2
- Traverse left of 2 → node 4 ✅
- Visit 2 ✅
- Traverse right of 2 → node 5 ✅
- Visit 1 ✅
- Traverse right subtree of 1 → node 3
- Traverse left of 3 → node 6 ✅
- Visit 3 ✅
- Traverse right of 3 → node 7 ✅

🧭 **In-order Traversal**: `4, 2, 5, 1, 6, 3, 7`

---

### ✅ Pre-order (Root ➡️ Left ➡️ Right)
1. Visit current node
2. Traverse left subtree
3. Traverse right subtree

🔁 Steps:
- Visit 1 ✅
- Traverse left → visit 2 ✅
  - Left of 2 → 4 ✅
  - Right of 2 → 5 ✅
- Traverse right → visit 3 ✅
  - Left of 3 → 6 ✅
  - Right of 3 → 7 ✅

🧭 **Pre-order Traversal**: `1, 2, 4, 5, 3, 6, 7`

---

### ✅ Post-order (Left ➡️ Right ➡️ Root)
1. Traverse left subtree
2. Traverse right subtree
3. Visit current node

🔁 Steps:
- Left of 1 → node 2
  - Left of 2 → 4 ✅
  - Right of 2 → 5 ✅
  - Visit 2 ✅
- Right of 1 → node 3
  - Left of 3 → 6 ✅
  - Right of 3 → 7 ✅
  - Visit 3 ✅
- Visit 1 ✅

🧭 **Post-order Traversal**: `4, 5, 2, 6, 7, 3, 1`


```py
from typing import List
from collections import deque

class TreeNode:
    def __init__(self, val, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

def build_tree(level_order):
    if not level_order or level_order[0] is None:
        return None

    root = TreeNode(level_order[0])
    queue = deque([root])
    i = 1

    while queue and i < len(level_order):
        node = queue.popleft()

        if i < len(level_order) and level_order[i] is not None:
            node.left = TreeNode(level_order[i])
            queue.append(node.left)
        i += 1

        if i < len(level_order) and level_order[i] is not None:
            node.right = TreeNode(level_order[i])
            queue.append(node.right)
        i += 1

    return root

def inorder_traversal(root: TreeNode):
    result = []

    def dfs(node: TreeNode):
        if not node:
            return 
        dfs(node.left)
        result.append(node.val)
        dfs(node.right)
    dfs(node=root)
    return result

def preorderTraversal(root):
    result = []

    def dfs(node):
        if node is None:
            return
        result.append(node.val)   # Visit root first
        dfs(node.left)            # Traverse left subtree
        dfs(node.right)           # Traverse right subtree

    dfs(root)
    return result

def postorderTraversal(root):
    result = []

    def dfs(node):
        if node is None:
            return
        dfs(node.left)            # Traverse left subtree
        dfs(node.right)           # Traverse right subtree
        result.append(node.val)   # Visit root last

    dfs(root)
    return result

```