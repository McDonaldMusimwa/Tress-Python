# <spa style="color:green"> **Trees**  </span>
1. [Binary Trees](#binary-trees)
2. [Binary Search Trees](#binary-search-tree)
3. [Balanced Binary Search Trees](#balanced-binary-search-trees)  
4. [Binary Search Trees operations](#binary-search-trees-operations)  
5. [Traverse Forwad](#traversing-forward)  

## <spa style="color:green">Characterics</span> 
Linked lists and Trees have this in common they both use pointers in linking to the next node.While Linked list connects you to one node trees connects to multiple nodes.

## <span style="color:green">Types of Trees in this tutorial</span>
1. Binary Tree: A binary tree is a tree data structure in which each node can have at most two children, referred to as the left child and the right child.

2. Binary Search Tree (BST): A binary search tree is a binary tree in which the left child of a node contains a value smaller than the node's value, and the right child contains a value greater than the node's value. It allows for efficient searching, insertion, and deletion operations.

3. Balanced Search Tree (BST): A balanced search tree is a binary search tree in which the depth of left and right node branches is managed to maintained a much more balanced level of branch length. 

    - AVL Tree: An AVL (Adelson-Velskii and Landis) tree is a self-balancing binary search tree. It maintains a balance factor for each node and performs rotations to keep the tree balanced, ensuring efficient operations.  
    - Red-Black Tree: A red-black tree is another self-balancing binary search tree. It uses a set of rules and properties to maintain balance, ensuring that the longest path from the root to a leaf node is no more than twice as long as the shortest path.  

# **Binary Trees**  
In a binary tree you have a node that is linked to no more than 2 other nodes.The starting node is called a <span style="color:yellow">root node</span> the nodes that are not connecting to other node are called <span style="color:yellow">leaf nodes</span>.A node that has connected nodes is called <span style="color:yellow">parent nodes</span>.The nodes connected to the parents node are called <span style="color:yellow">child nodes</span>. 

<span style="color:brown">  

        [ A ]=>root node 
        /   \  
      [ B ] [ C ]=>parent node  
       /  \  
     [D]  [E]=>child node
          / \  
        [G] [F]=>leaf node  
</span>  

# Binary Search Tree  
Binary search tree is a binary tree that follows a structured approach to storing data received.An example of this approach is comparison approach.When we receive data we compare this data with the root of the incoming data is less than the root node then we store the data on the left if its more than we store on the right.By approaching data storage using this route we have the ability to split the job in half recursively results in O(log n). Maintaining sorted data in a BST performs better than other data structures.
  
1. Store 20      
***tree structure***  

         [ 20 ]=>root

2. Store 30  
- evaluate 20 < 30 then store on the right  
   ***tree structure***  
    
        [ 20 ]=>root  
        /    \  
            [ 30 ] => leaf node  

3. Store 15  
- evaluate 20 > 15 then store on the left     
***tree structure***  

          [ 20 ]=> root  
          /    \ 
       [ 15] [ 30 ]=> leaf node  

4. Store 10  
- evaluate 20>10 store on the left  
- evaluate 15>10 store on the left  
***tree structure***  

            [ 20 ] => root  
            /    \  
        [ 15 ]   [ 30 ]=>parent node 
        /     
        [ 10 ] => leaf node

5. Store 40  
- evaluate 20<40 store on the right  
- evaluate 30<40 store on the right  
***tree structure***  


                [ 20 ] => root node 
                /    \  
            [ 15 ]   [ 30 ]=>parent node    
            /             \      
        [ 10 ]            [ 40 ]=>leaf node  

6. Store 17  
- evaluate 20>17 store on the left  
- evaluate 15<17 store on the right  
- evaluate store on the right  
***tree structure***  

                [ 20 ] => root node 
                /    \  
            [ 15 ]   [ 30 ]=>parent node    
            /    \        \      
        [ 10 ]  [ 17 ]   [ 40 ]=>leaf node  


# Balanced-Binary-Search-Trees  
Balanced Binary Search Trees seeks to maintain a balance in the depth of branches such that the difference of height between any two subtrees is not dramatically different this is achieved through the use of algorthyms.This apandage to Binary search trees is the one that gives it a performance of O(log n)  

   - ***AVL*** (Adelson-Velskii and Landis)  
   - ***Red black tree***  

                        [ 20 ] 
                        /    \  
                    [ 15 ]   [ 30 ]    
                    /    \              
                [ 10 ]  [ 17 ] height from 15 is 2  
                /     
             [ 5 ] height from 15 is 3  

**Store 8**  

                        [ 20 ] 
                        /    \  
                    [ 15 ]   [ 30 ]    
                    /    \              
                [ 10 ]  [ 17 ] height from 15 is 2  
                /     
             [ 5 ] height from 15 is 3  
                 \  
                [ 8 ] height from 15 4

AVL will detect that by adding 8 we will have unbalanced tree.A node rotation is performed between 10,5,8 where 8 becomes a parent then 10 and 5 become a leaves.

                        [ 20 ] 
                        /    \  
                    [ 15 ]   [ 30 ]    
                    /    \              
                [ 8 ]   [ 17 ] height from 15 is 2  
                /   \  
             [ 5 ] [ 10] height from 15 is 3  
               

# Binary Search Trees operations  
## Inserting into a BST  
### Inserting into a BST is a recursive operations:

- Smaller problem: Insert a value into either the left subtree or the right subtree based on the value.

- Base case: If there is space to add the node (the subtree is empty), then the correct place has been found and the item can be inserted.  

            def insert(self, data):
                """
                Insert 'data' into the BST.  If the BST
                is empty, then set the root equal to the new 
                node.  Otherwise, use _insert to recursively
                find the location to insert.
                """
                if self.root is None:
                    self.root = BST.Node(data)
                else:
                    self._insert(data, self.root)  # Start at the root  

            def _insert(self, data, node):
        """
        This function will look for a place to insert a node
        with 'data' inside of it.  The current subtree is
        represented by 'node'.  This function is intended to be
        called the first time by the insert function.
        """
        if data < node.data:
            # The data belongs on the left side.
            if node.left is None:
                # We found an empty spot
                node.left = BST.Node(data)
            else:
                # Need to keep looking.  Call _insert
                # recursively on the left subtree.
                self._insert(data, node.left)
        elif data >= node.data:
            # The data belongs on the right side.
            if node.right is None:
                # We found an empty spot
                node.right = BST.Node(data)
            else:
                # Need to keep looking.  Call _insert
                # recursively on the right subtree.
                self._insert(data, node.right)        


# Traversing forward  
We traverse a Binary Search Tree when we want to display all the data that is in the tree.An in order traverse will visit node at each level and pull out the data from the largest to the smallest and display it .  

- Smaller problem: Traverse the left subtree of a node, use the current node, and then traverse the right subtree of the node.

- Base case: If the subtree is empty, then don't recursively traverse or use anything.



            def __reversed__(self):
                """
                Perform a formward traversal (in order traversal) starting from 
                the root of the BST.  This function is called when a the 
                reversed function is called and is frequently used with a for
                loop.

                for value in reversed(my_bst):
                    print(value)

                """        
                yield from self._traverse_backward(self.root)  # Start at the root


        def _traverse_backward(self, node):
            """
            Does a backwards traversal (reverse in-order traversal) through the 
            BST.  If the node that we are given (which is the current
            sub-tree) exists, then we will keep traversing on the right
            side (thus getting the larger numbers first), then we will 
            provide the data in the current node, and finally we will 
            traverse on the left side (thus getting the smaller numbers last).

            This function is intended to be called the first time by 
            the __reversed__ function.        
            """
            if node is None:
                return
            #right traverse
            yield from self._traverse_backward(node.right) # Replace this when you implement your solution

            #yield the data in the current node
            yield node.data

            #left traverse
            yield from self._traverse_backward(node.left)



# Key words  

- ***AVL Tree*** - Adelson-Velskii and Landis Tree. A balanced binary search tree that is checked unbalanced height after every modification to the tree. If the tree is unbalanced, then pre-determined algorithms are used to balance the tree.

- ***balanced*** - A tree is balanced if the the height of the tree from the root to each leaf is consistent for all subtrees. The measure of consistentency will vary between algorithms but usually does not exceed a height difference of 1.

- ***balanced binary search tree*** - A binary search tree which is balanced or restructured to be balanced. A balanced binary search tree has O(log n) performance when searching.

- ***binary search tree*** - A binary tree that puts data less than the root to the left and greater than the root to the right. This type of a tree enables searching algorithms to be efficient.

- ***binary tree*** - A tree that has up to two children for each node.

- ***child*** - A child is a node connected from a parent node.

- ***leaf*** - A leaf is a node that has no children.

- ***node*** - An entry in a tree that contains both the value and pointers to any children nodes.

- ***parent*** - A parent is a node that connects to children nodes.

- ***root*** - The first parent in a tree.

- ***subtree*** - Subset of a tree made by selecting a node to be the root and including all the children from that node.

- ***traverse*** - The process of visiting all nodes (and subsequently their values) in a tree. Used frequently with a binary search tree using recursion to start at the leaf node that contains the smallest value and going to the leaf node that contains the largest value.

- ***trees*** - A data structure that starts with a root node and is subsequently connected to multiple nodes according to a relationship between the nodes. The tree does not have any circular loops or unconnected nodes.







