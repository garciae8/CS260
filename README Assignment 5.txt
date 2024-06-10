
struct Node {
    int data;
    Node* next;
    Node(int val) : data(val), next(nullptr) {}
};

This Node struct represents each element in the linked list, containing the data and a pointer to the next node.


class SortedLinkedList {
private:
    Node* head;
public:
    SortedLinkedList() : head(nullptr) {}


This is the SortedLinkedList class manages the linked list with functions to insert elements in sorted order and search for elements efficiently.


void insert(int val) {
    Node* newNode = new Node(val);
    if (!head || val < head->data) {
        newNode->next = head;
        head = newNode;
    } else {
        Node* current = head;
        while (current->next && current->next->data < val) {
            current = current->next;
        }
        newNode->next = current->next;
        current->next = newNode;
    }
}


The insert function inserts a new node with the given value in the correct sorted position within the linked list.


bool search(int val) {
    Node* current = head;
    while (current) {
        if (current->data == val) {
            return true;
        }
        current = current->next;
    }
    return false;
}

The search function traverses the linked list to find if a specific value exists in the list.

int main() {
    SortedLinkedList list;
    list.insert(5);
    list.insert(3);
    list.insert(7);

    std::cout << "Search 3: " << (list.search(3) ? "Found" : "Not Found") << std::endl;
    std::cout << "Search 8: " << (list.search(8) ? "Found" : "Not Found") << std::endl;

    return 0;
}

In The main function demonstrates inserting elements into the sorted linked list and performing search operations to verify the correctness of the insertion and search functionalities.