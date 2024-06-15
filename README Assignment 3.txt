Implementation:

Que and link list
Que and Node struct:

struct Node {  // Line 4
    int data;
    Node* next;
    Node(int val) : data(val), next(nullptr) {}
};

class Queue {  // Line 10
private:
    Node* front;
    Node* rear;

public:
    Queue() : front(nullptr), rear(nullptr) {}
    ~Queue();
    void enqueue(int val);
    int dequeue();
    int peek();
};

Enqueue Method: Added a value back to the the queue

void enqueue(int val) {  // Line 18
    Node* newNode = new Node(val);
    if (rear == nullptr) {
        front = newNode;
        rear = newNode;
    } else {
        rear->next = newNode;
        rear = newNode;
    }
}


Dequeue Method: Remove any value from the queue of the code

int dequeue() {  // Line 28
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


Peek Method implementation: moves a value from the que to front without removing it at all

int peek() {  // Line 41
    if (front == nullptr) {
        std::cout << "Queue is empty." << std::endl;
        return -1;
    }
    return front->data;
}
