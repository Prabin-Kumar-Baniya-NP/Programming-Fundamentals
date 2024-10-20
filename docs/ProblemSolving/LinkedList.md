# Linked List

- A linked list is a linear data structure that consists of a series of nodes connected by pointers or references.
- Each node contains data and a pointer/reference to the next node in the list.
- Nodes are not stored contiguously in memory.

## Difference between LinkedList and Array

### Linked List
- Data Structure: Non-contiguous
- Memory Allocation: Typically allocated one by one to individual elements
- Insertion/Deletion: Efficient
- Access: Sequential

### Array
- Data Structure: Contiguous
- Memory Allocation: Typically allocated to the whole array
- Insertion/Deletion: Inefficient
- Access: Random

## Implementation in Python

```py
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

class LinkedList:
    def __init__(self, data):
        self.head = Node(data)
    
    def insert_at_beginning(self, data):
        new_node = Node(data)
        new_node.next = self.head
        self.head = new_node
    
    def insert_at_end(self, data):
        new_node = Node(data)
        if not self.head:
            return
        last_node = self.head
        while last_node.next:
            last_node = last_node.next
        last_node.next = new_node
    
    def print_node_data(self):
        current_node = self.head
        while current_node:
            print(current_node.data)
            current_node = current_node.next
        


ll = LinkedList(1)
ll.insert_at_beginning(2)
ll.insert_at_end(10)
ll.print_node_data()
```

## Types of Linked List

### Singly Linked List

- Singly linked list is a linear data structure in which the elements are not stored in contiguous memory locations and each element is connected only to its next element using a pointer.

### Double Linked List

- A doubly linked list is a data structure that consists of a set of nodes, each of which contains a value and two pointers, one pointing to the previous node in the list and one pointing to the next node in the list. 

### Circular Linked List

- A circular linked list is a special type of linked list where all the nodes are connected to form a circle. 

### Circular Double Linked List

- A circular doubly linked list is defined as a circular linked list in which each node has two links connecting it to the previous node and the next node.