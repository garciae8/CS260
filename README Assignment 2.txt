Design

Functions:

enqueue(value): Adds an element to the back of the queue.

dequeue(): Removes and returns the element from the front of the queue.

isEmpty(): Checks if the queue is empty.

Values:

front: A reference to the front node of the queue.

back: A reference to the back node of the queue.

length: The number of elements in the queue.

List Data Structure
Functions:

insert(value, position): Adds an element at the specified position in the list.

delete(position): Removes the element at the specified position in the list.

isEmpty(): Checks if the list is empty.

Values:

head: A reference to the first node of the list.

length: The number of elements in the list.

Psuedo Code

Queue:
    front = null
    back = null
    length = 0

Function enqueue(value):
    newNode = Node(value)
    if isEmpty():
        front = newNode
    else:
        back.next = newNode
    back = newNode
    length = length + 1

Function dequeue():
    if isEmpty():
        return "Queue is empty"
    else:
        value = front.value
        front = front.next
        if front == null:
            back = null
        length = length - 1
        return value

Function isEmpty():
    return length == 0
