# C++ Custom Data Structures: Dynamic Array and Priority Queue Adapter

This C++ project demonstrates how to build complex data structures by composing simpler ones. It features two main components:
1.  A generic, vector-like dynamic array class (named `Queue`).
2.  A `PriorityQueue` class that uses the first class as its underlying container.

This project serves as an excellent case study in templates, memory management, and the **Adapter design pattern**, where one class's interface is adapted to another.

## Project Structure and Concepts

### 1. The `Queue` Class (Dynamic Array)

This class is a generic container that functions as a **dynamic array**, similar to `std::vector`.
*   **Note on Naming**: Although named `Queue`, its First-In-Last-Out (FILO) behavior (`push_back`/`pop_back`) is that of a stack or dynamic array, not a First-In-First-Out (FIFO) queue.
*   **Features**:
    *   **Generic**: Uses `template<class T>` to store any data type.
    *   **Dynamic Memory**: Manages its own memory, automatically growing and shrinking as needed.
    *   **The Rule of Three**: Correctly implements a copy constructor, copy assignment operator, and destructor to handle resources safely.

### 2. The `PriorityQueue` Class (Adapter)

This class is designed as a wrapper around the `Queue` dynamic array. Its purpose is to provide a "priority queue" interface while using the `Queue` class for the actual data storage.

*   **Concepts Demonstrated**:
    *   **Composition**: The `PriorityQueue` *has a* `Queue` member, showing how to build classes from other classes.
    *   **Interface Adapting**: It maps its methods (`push_back`, `pop`, `front`, etc.) directly to the underlying `Queue` object's methods.

## IMPORTANT: A Lesson in Data Structure Logic

This implementation of `PriorityQueue` is **not a functional priority queue**. This is a critical distinction and a valuable learning opportunity.

*   **How This `PriorityQueue` Behaves**:
    *   `push_back(value)`: Adds an element to the end of the internal array.
    *   `pop()`: Removes the **last element** that was added (LIFO/stack behavior).
    *   `front()`: Returns the **first element** that was added.

*   **How a REAL Priority Queue Should Behave**:
    *   A priority queue is a data structure where every element has a "priority." The most common type is a max-priority queue.
    *   `push(value)`: Adds an element and places it according to its priority (often using a **heap** data structure).
    *   `pop()`: **Always** removes the element with the highest priority (e.g., the largest integer).
    *   `top()` (or `front()`): **Always** returns the element with the highest priority.

**Conclusion**: The included `PriorityQueue` class is a simple adapter and does not implement the necessary logic to manage element priority. To make it a true priority queue, one would need to implement a heap or keep the internal array sorted after every insertion.

## How to Build and Run

You will need a standard C++ compiler (like G++, Clang, or MSVC).

1.  Save the code as a `.cpp` file (e.g., `main.cpp`).
2.  Open a terminal in the directory of the file.
3.  Compile the code:
    ```sh
    g++ main.cpp -o data_structures_app
    ```
4.  Run the application:
    ```sh
    ./data_structures_app
    ```

## Code Walkthrough and Output Analysis

Let's analyze the `main` function to see the actual behavior.

```cpp
int main() {
    PriorityQueue<int> a;
    a.push_back(3); // Internal state:
    a.push_back(5); // Internal state:
    a.push_back(8); // Internal state:

    // Returns the first element added.
    cout << "Front: " << a.front() << endl;

    // Returns the last element added.
    cout << "Back: " << a.back() << endl;

    // Removes the LAST element (8).
    a.pop(); // Internal state:

    // Front is still the first element.
    cout << "Front after pop: " << a.front() << endl;

    // Size is now 2.
    cout << "Size: " << a.size() << endl;
}
```

### Expected Output:
```
Front: 3
Back: 8
Front after pop: 3
Size: 2
```
This output confirms that the `PriorityQueue` acts as a simple wrapper around a dynamic array, not a true priority queue where `front()` would have been `8`.
```
