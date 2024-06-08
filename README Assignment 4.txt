Implementation 

The code below is trying to define a Node structure with data to store the value and next to point to the next node, forming the basis of the linked list.

struct Node {
    int data;
    Node* next;
    Node(int val) : data(val), next(nullptr) {}
};


I'm trying to initializes a Queue class with front and rear pointers, initially set to nullptr, indicating an empty queue.

class Queue {
private:
    Node* front;
    Node* rear;

public:
    Queue() : front(nullptr), rear(nullptr) {}


This is the enqueue method which adds a new node with the given value to the back of the queue. It updates front and rear pointers appropriately, handling both empty and non-empty queue cases.

void enqueue(int val) {
    Node* newNode = new Node(val);
    if (rear == nullptr) {
        front = newNode;
        rear = newNode;
    } else {
        rear->next = newNode;
        rear = newNode;
    }
}


Like before this is the dequeue method which removes the node from the front of the queue and returns its value. It handles the case where the queue is empty by returning -1 and prints a message.

int dequeue() {
    if (front == nullptr) {
        std::cout << "Queue is empty." << std::endl;
        return -1;
    }
    int val = front->data;
    Node* temp = front;
    front = front->next;
    delete temp;
    if (front == nullptr) {
        rear = nullptr;
    }
    return val;
}

The destructor ensures all dynamically allocated nodes are properly deleted, preventing memory leaks Im not really too confident about it 

~Queue() {
    while (front != nullptr) {
        Node* temp = front;
        front = front->next;
        delete temp;
    }
}


Test cases

int main() {
    Queue queue;

    // Test enqueue
    queue.enqueue(10);
    queue.enqueue(20);
    queue.enqueue(30);

    // Test dequeue
    std::cout << "Dequeued: " << queue.dequeue() << std::endl;
    std::cout << "Dequeued: " << queue.dequeue() << std::endl;
    std::cout << "Dequeued: " << queue.dequeue() << std::endl;
    std::cout << "Dequeued: " << queue.dequeue() << std::endl; // for empty queue test

    // Test enqueue and peek
    queue.enqueue(40);
    std::cout << "Peeked: " << queue.peek() << std::endl;

    return 0;
}
