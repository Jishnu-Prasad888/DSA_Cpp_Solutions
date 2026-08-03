

# Implementation of queue using array

## Circular queue

```cpp

class Queue {
    int *arr;
    int front;
    int rear;
    int currentSize;
    int capacity;

public:
    Queue(int c) {
        capacity = c;
        arr = new int[capacity];
        front = 0;
        rear = 0;
        currentSize = 0;
    }

    bool isEmpty() {
        return currentSize == 0;
    }

    bool isFull() {
        return currentSize == capacity;
    }

    void enQueue(int x) {
        if (isFull())
            return;

        arr[rear] = x;
        rear = (rear + 1) % capacity;
        currentSize++;
    }

    void deQueue() {
        if (isEmpty())
            return;

        front = (front + 1) % capacity;
        currentSize--;
    }

    int getFront() {
        if (isEmpty())
            return -1;
        return arr[front];
    }

    int getRear() {
        if (isEmpty())
            return -1;

        int index = (rear - 1 + capacity) % capacity;
        return arr[index];
    }
};
```



## Linear Queue

```cpp
class Queue {
    int *arr;
    int currentSize;
    int end;
    int capacity;

public:
    Queue(int c) {
        capacity = c;
        arr = new int[capacity];
        currentSize = 0;
        end = 0;
    }

    bool isEmpty() {
        return currentSize == 0;
    }

    bool isFull() {
        return currentSize == capacity;
    }

    void enQueue(int x) {
        if (isFull())
            return;

        arr[end] = x;
        end++;
        currentSize++;
    }

    void deQueue() {
        if (isEmpty())
            return;

        for (int i = 1; i < end; i++) {
            arr[i - 1] = arr[i];
        }

        end--;
        currentSize--;
    }

    int front() {
        if (isEmpty())
            return -1;
        return arr[0];
    }
};
```


