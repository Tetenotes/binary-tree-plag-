Title
Name
Instructor
Institution Affiliation
Course
Date: August 19th,2022


























Making A Binary Search Tree (BST)
We need to build a BST from the array of elements provided.
Following is a suggested procedure:

The following numbers are part of the array we're working with: 70 31 93 14 73 94 7 23 67 99 25 43 56 88 77 95

Here, we'll treat the topmost item, 95, as the primary node. Keeping in mind these qualities, we will now proceed with developing the BST.
Making a tree requires comparing each array item to the first. After that, we'll decide where in the hierarchy the component belongs.

Operations on a Binary Search Tree
In addition to its other capabilities, BST can also perform a number of useful operations. You can see the BST Java APIs in the code. Each of these approaches will be covered independently.

Method/operation Description

Insert
Include something new in the BST without breaking any of its rules.

Delete
Eliminate the specified node from the BST. The node could be the root, an intermediate node, or a leaf.

Search
The BST can be searched for the presence of the provided element. This process verifies if the given key exists in the tree.

Add Something to BST
In BST, an element is consistently inserted as a leaf node

The procedures for adding a new component are detailed below.
Get back to basics.
Verify the insert target against the parent node. If this value is less than root, then either the left or right subtree should be explored.You need to go all the way to the end of the subtree you're interested in. Replace the node with a leaf node in the correct child subtree.

Scanning Procedures in BST
Again, we begin at the root and move left or right across the BST's subtrees depending on whether the element being searched is smaller than or larger than the root.
Evaluate the sought-after component in relation to the tree's top-level node.
If the root element is the key, then the root node will be returned.Alternately, if key is smaller than root, then go to the left subtree.If that doesn't work, then go through the branches on the right.Keep comparing nodes in the subtree until either the key is found or the tree is exhausted.How a search works, illustrated with a real-world scenario. Think about the fact that we need to look for the key = 12. The answer, we determine, is fewer than fifteen. Then, we'll go to node 15's left child nodes. The number 12 is the next left node from the number 15, which is the correct answer. This is when we call it quits and give you the result.

Do Not Include in BST
Three scenarios are detailed below when a node is removed from the BST:
As a Leaf Node, Because it has no parent nodes, deleting a leaf node is as simple as deleting the node itself. 
class BST_class { 
    //node class that defines BST node
    class Node { 
        int key; 
        Node left, right; 
   
        public Node(int data){ 
            key = data; 
            left = right = null; 
        } 
    } 
    // BST root node 
    Node root; 
  
   // Constructor for BST =>initial empty tree
    BST_class(){ 
        root = null; 
    } 
    //delete a node from BST
    void deleteKey(int key) { 
        root = delete_Recursive(root, key); 
    } 
   
    //recursive delete function
    Node delete_Recursive(Node root, int key)  { 
        //tree is empty
        if (root == null)  return root; 
   
        //traverse the tree
        if (key < root.key)     //traverse left subtree 
            root.left = delete_Recursive(root.left, key); 
        else if (key > root.key)  //traverse right subtree
            root.right = delete_Recursive(root.right, key); 
        else  { 
            // node contains only one child
            if (root.left == null) 
                return root.right; 
            else if (root.right == null) 
                return root.left; 
   
            // node has two children; 
            //get inorder successor (min value in the right subtree) 
            root.key = minValue(root.right); 
   
            // Delete the inorder successor 
            root.right = delete_Recursive(root.right, root.key); 
        } 
        return root; 
    } 
   
    int minValue(Node root)  { 
        //initially minval = root
        int minval = root.key; 
        //find minval
        while (root.left != null)  { 
            minval = root.left.key; 
            root = root.left; 
        } 
        return minval; 
    } 
   
    // insert a node in BST 
    void insert(int key)  { 
        root = insert_Recursive(root, key); 
    } 
   
    //recursive insert function
    Node insert_Recursive(Node root, int key) { 
          //tree is empty
        if (root == null) { 
            root = new Node(key); 
            return root; 
        } 
        //traverse the tree
        if (key < root.key)     //insert in the left subtree
            root.left = insert_Recursive(root.left, key); 
        else if (key > root.key)    //insert in the right subtree
            root.right = insert_Recursive(root.right, key); 
          // return pointer
        return root; 
    } 
 
// method for inorder traversal of BST 
    void inorder() { 
        inorder_Recursive(root); 
    } 
   
    // recursively traverse the BST  
    void inorder_Recursive(Node root) { 
        if (root != null) { 
            inorder_Recursive(root.left); 
            System.out.print(root.key + " "); 
            inorder_Recursive(root.right); 
        } 
    } 
     
    boolean search(int key)  { 
        root = search_Recursive(root, key); 
        if (root!= null)
            return true;
        else
            return false;
    } 
   
    //recursive insert function
    Node search_Recursive(Node root, int key)  { 
        // Base Cases: root is null or key is present at root 
        if (root==null || root.key==key) 
            return root; 
        // val is greater than root's key 
        if (root.key > key) 
            return search_Recursive(root.left, key); 
        // val is less than root's key 
        return search_Recursive(root.right, key); 
    } 
}
class Main{
    public static void main(String[] args)  { 
       //create a BST object
        BST_class bst = new BST_class(); 
        /* BST tree example
              45 
           /     \ 
          10      90 
         /  \    /   
        7   12  50   */
        //insert data into BST
        bst.insert(45); 
        bst.insert(10); 
        bst.insert(7); 
        bst.insert(12); 
        bst.insert(90); 
        bst.insert(50); 
        //print the BST
        System.out.println("The BST Created with input data(Left-root-right):"); 
        bst.inorder(); 
        
        //delete leaf node  
        System.out.println("\nThe BST after Delete 12(leaf node):"); 
        bst.deleteKey(12); 
        bst.inorder(); 
        //delete the node with one child
        System.out.println("\nThe BST after Delete 90 (node with 1 child):"); 
        bst.deleteKey(90); 
        bst.inorder(); 
                 
        //delete node with two children  
        System.out.println("\nThe BST after Delete 45 (Node with two children):"); 
        bst.deleteKey(45); 
        bst.inorder(); 
        //search a key in the BST
        boolean ret_val = bst.search (50);
        System.out.println("\nKey 50 found in BST:" + ret_val );
        ret_val = bst.search (12);
        System.out.println("\nKey 12 found in BST:" + ret_val );
     } 
}