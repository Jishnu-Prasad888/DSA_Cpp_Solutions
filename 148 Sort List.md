[148. Sort List](https://leetcode.com/problems/sort-list/)

Given the `head` of a linked list, return _the list after sorting it in **ascending order**_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/09/14/sort_list_1.jpg)

**Input:** head = [4,2,1,3]
**Output:** [1,2,3,4]

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/09/14/sort_list_2.jpg)

**Input:** head = [-1,5,3,4,0]
**Output:** [-1,0,3,4,5]

**Example 3:**

**Input:** head = []
**Output:** []

**Constraints:**

- The number of nodes in the list is in the range `[0, 5 * 104]`.
- `-105 <= Node.val <= 105`

**Follow up:** Can you sort the linked list in `O(n logn)` time and `O(1)` memory (i.e. constant space)?
## Brute Force : Time Limit Exceeded

```cpp
class Solution {
public:
    ListNode* sortList(ListNode* head) {
        if (!head || !head->next) return head;

        ListNode dummy(0);
        dummy.next = head;

        ListNode* prev = &dummy;

        while (prev->next) {
            ListNode* temp = prev->next;
            ListNode* minPrev = prev;
            ListNode* curPrev = temp;

            // Find min node in remaining list
            while (curPrev->next) {
                if (curPrev->next->val < minPrev->next->val) {
                    minPrev = curPrev;
                }
                curPrev = curPrev->next;
            }

            // If min is not already in place, swap nodes
            if (minPrev != prev) {
                ListNode* minNode = minPrev->next;
                ListNode* tempNode = prev->next;

                // detach minNode
                minPrev->next = minNode->next;

                // place minNode at correct position
                minNode->next = tempNode;
                prev->next = minNode;
            }

            prev = prev->next;
        }

        return dummy.next;
    }
};
```

## brute force but much cleaner with insertion sort

```cpp
class Solution {
public:
    ListNode* sortList(ListNode* head) {
        if (!head) return head;

        ListNode dummy(0); // sorted list dummy head
        ListNode* curr = head;

        while (curr) {
            ListNode* nextNode = curr->next; // store next

            // find position in sorted list
            ListNode* prev = &dummy;
            while (prev->next && prev->next->val < curr->val) {
                prev = prev->next;
            }

            // insert curr between prev and prev->next
            curr->next = prev->next;
            prev->next = curr;

            curr = nextNode;
        }

        return dummy.next;
    }
};
```

## merge sort optimal 


```cpp
class Solution {
public:
    ListNode* sortList(ListNode* head) {
        if (!head || !head->next) return head;

        // Step 1: Split list into two halves
        ListNode* mid = getMid(head);
        ListNode* left = head;
        ListNode* right = mid->next;
        mid->next = nullptr;

        // Step 2: Sort both halves
        left = sortList(left);
        right = sortList(right);

        // Step 3: Merge sorted halves
        return merge(left, right);
    }

private:
    // Find middle (slow-fast pointer)
    ListNode* getMid(ListNode* head) {
        ListNode* slow = head;
        ListNode* fast = head->next;

        while (fast && fast->next) {
            slow = slow->next;
            fast = fast->next->next;
        }
        return slow;
    }

    // Merge two sorted lists
    ListNode* merge(ListNode* l1, ListNode* l2) {
        ListNode dummy(0);
        ListNode* tail = &dummy;

        while (l1 && l2) {
            if (l1->val < l2->val) {
                tail->next = l1;
                l1 = l1->next;
            } else {
                tail->next = l2;
                l2 = l2->next;
            }
            tail = tail->next;
        }

        tail->next = l1 ? l1 : l2;
        return dummy.next;
    }
};
```

### How it works (quick intuition)

1. **Split**
    - Use slow/fast pointers to cut list into halves
2. **Recursively sort**
    - Keep dividing until single nodes
3. **Merge**
    - Merge two sorted lists like merge step of merge sort

### Why Merge Sort?

- Linked lists don’t support random access → quicksort/heap sort are inefficient
- Merge sort works by splitting and merging → perfect for pointer manipulation
- **Time:** O(n log n)
- **Space:** O(log n) (recursion stack)


Let’s walk through a **dry run step-by-step** so you can actually _see_ how merge sort works on a linked list.

---

## Example

```
4 → 2 → 1 → 3
```

---

## Step 1: Split the list

Using slow-fast pointers:

```
slow = 2, fast reaches end
```

Split into:

```
Left  = 4 → 2
Right = 1 → 3
```

---

## Step 2: Recursively split further

### Left side: `4 → 2`

Split:

```
4     2
```

Now both are single nodes → already sorted

---

### Right side: `1 → 3`

Split:

```
1     3
```

Already sorted

---

## Step 3: Merge step (this is the core)

### Merge `4` and `2`

Compare:

- 4 vs 2 → pick 2
    
- then 4 remains
    

Result:

```
2 → 4
```

---

### Merge `1` and `3`

Compare:

- 1 vs 3 → pick 1
    
- then 3
    

Result:

```
1 → 3
```

---

## Step 4: Final merge

Now merge:

```
2 → 4
1 → 3
```

Compare step-by-step:

1. 2 vs 1 → pick **1**
    
2. 2 vs 3 → pick **2**
    
3. 4 vs 3 → pick **3**
    
4. 4 remains → pick **4**
    

Final:

```
1 → 2 → 3 → 4
```

---

## What’s actually happening with pointers

At each merge:

- You don’t create new nodes
    
- You just **redirect `next` pointers**
    

Example:

```cpp
tail->next = l1; // or l2
```

So nodes are reused, just rearranged.

---

## Visual recursion tree

```
            4 → 2 → 1 → 3
           /               \
      4 → 2               1 → 3
      /    \             /     \
     4      2           1       3
      \    /             \     /
       2 → 4             1 → 3
             \           /
            1 → 2 → 3 → 4
```

---

## Key intuition

- **Divide** until size = 1 (already sorted)
    
- **Merge** sorted pieces back together
    
- Sorting happens _during merging_, not splitting
    

---

## Why it’s efficient

At every level:

- You process all `n` nodes once (merging)
    
- Number of levels = `log n`
    

So:

```
Total = n × log n
```

---

If you want, I can next show a **pointer-level trace** (like exactly how `next` changes line-by-line), which is where most people finally “get it”.