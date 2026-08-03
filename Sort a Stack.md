
**Problem Statement:** You are given a stack of integers. Your task is to sort the stack in descending order using recursion, such that the top of the stack contains the greatest element. You are not allowed to use any loop-based sorting methods (e.g., quicksort, mergesort). You may only use recursive operations and the standard stack operations (push, pop, peek/top, and isEmpty).

**Examples**

**Example 1:****Input:** stack = [4, 1, 3, 2]
**Output:** [4, 3, 2, 1]
**Explanation:** After sorting, the largest element (4) is at the top, and the smallest (1) is at the bottom.

**Example 2:****Input:** stack = [1]
**Output:** [1]
**Explanation:** A single-element stack is already sorted.

Approach

```cpp
#include <iostream>
#include <stack>
using namespace std;

void insertSorted(stack<int>& st, int x) {
    if (st.empty() || st.top() <= x) {
        st.push(x);
        return;
    }

    int temp = st.top();
    st.pop();

    insertSorted(st, x);

    st.push(temp);
}

void sortStack(stack<int>& st) {
    if (st.empty()) {
        return;
    }

    int temp = st.top();
    st.pop();

    sortStack(st);

    insertSorted(st, temp);
}

int main() {
    stack<int> numbers;

    numbers.push(10);
    numbers.push(30);
    numbers.push(20);
    numbers.push(50);

    sortStack(numbers);

    while (!numbers.empty()) {
        cout << numbers.top() << endl;
        numbers.pop();
    }
}
```