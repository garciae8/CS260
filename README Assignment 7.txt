Design for assignment 6 

Node Structure: Stores the value and pointers to left and right children.
BinarySearchTree Class: Manages the root node and provides methods to manipulate the tree.
Attributes:

Node* root: The root node of the BST.
Methods:

Node* addRecursive(Node* current, int value): Helper function to recursively add a value.
Node* removeRecursive(Node* current, int value): Helper function to recursively remove a value.
Node* findMin(Node* node): Helper function to find the minimum value node.
void inOrderRecursive(Node* node): Helper function for in-order traversal.
void preOrderRecursive(Node* node): Helper function for pre-order traversal.
void postOrderRecursive(Node* node): Helper function for post-order traversal.
void breadthFirstTraversal(): Helper function for breadth-first traversal.
void add(int value): Public method to add a value.
void remove(int value): Public method to remove a value.
void inOrderTraversal(): Public method for in-order traversal.
void preOrderTraversal(): Public method for pre-order traversal.
void postOrderTraversal(): Public method for post-order traversal.
void levelOrderTraversal(): Public method for level-order traversal.

Tests
Test add Method:
Add values and verify the structure through in-order traversal.
Test remove Method:
Remove a value and verify the structure through in-order traversal.
Test Traversal Methods:
Verify the correct order of elements after various insertions and deletions for in-order, pre-order, post-order, and level-order traversals.

Explanation

struct Node {
    int data;
    Node* left;
    Node* right;

    Node(int value) : data(value), left(nullptr), right(nullptr) {}
};

This structure defines a Node for storing values and pointers to the left and right children, demonstrating the basic building block of the binary search tree.


void add(int value) {
    root = addRecursive(root, value);
}


This method shows how a new value is added to the BST in the appropriate position, ensuring the tree maintains its ordering properties.


void testAddAndTraversal() {
    BinarySearchTree bst;
    bst.add(5);
    bst.add(3);
    bst.add(7);
    bst.add(2);
    bst.add(4);

    std::cout << "In-order traversal: ";
    bst.inOrderTraversal(); // Expected: 2 3 4 5 7
}

This test demonstrates adding multiple values to the BST and verifies the tree's structure through in-order traversal, showing that elements are inserted correctly.


void remove(int value) {
    root = removeRecursive(root, value);
}

This method demonstrates the process of removing a node from the BST, ensuring the tree's structure is maintained by selecting an appropriate replacement node.

void inOrderTraversal() {
    inOrderRecursive(root);
    std::cout << std::endl;
}

This method is supposed to perform an in-order traversal of the BST, going through the nodes in order, which is a necessary traversal method for binary trees.


void preOrderTraversal() {
    preOrderRecursive(root);
    std::cout << std::endl;
}

This method performs a post-order traversal of the BST, going through the left subtree first, then the right subtree, and the root node last.


void levelOrderTraversal() {
    breadthFirstTraversal();
    std::cout << std::endl;
}


This method performs a level-order traversal of the BST, visiting nodes level by level, which is useful for tasks that require processing nodes in their level order.


void testAllTraversals() {
    BinarySearchTree bst;
    bst.add(5);
    bst.add(3);
    bst.add(7);
    bst.add(2);
    bst.add(4);

    std::cout << "Pre-order traversal: ";
    bst.preOrderTraversal(); // Expected: 5 3 2 4 7

    std::cout << "Post-order traversal: ";
    bst.postOrderTraversal(); // Expected: 2 4 3 7 5

    std::cout << "Level-order traversal: ";
    bst.levelOrderTraversal(); // Expected: 5 3 7 2 4
}


This test demonstrates the correctness of all implemented traversal methods (pre-order, post-order, and level-order) by adding values to the BST and verifying the output of each traversal method.