# Maximum Sliding Window Problem Explanation

## Problem Description:
Given an array of integers `nums` and a sliding window size `k`, your task is to find the maximum value in each sliding window as the window moves from left to right across the array.

---

## Approach: Deque (Double-ended Queue)

The key idea is to maintain a **deque** (double-ended queue) that stores the indices of the elements in the array, and for each sliding window:
- The **front** of the deque always contains the index of the maximum element for the current window.
- The **deque maintains elements in decreasing order** within the window.

---

## Steps:

1. **Initialize an empty deque** and an array `result[]` to store the maximums for each window.

2. **Iterate through the array**:
    - For each index `i` in the array, perform the following operations:

3. **Remove elements that are out of the window**:
    - The window is defined from index `i - k + 1` to `i`. If the element at the front of the deque is outside this range (i.e., `deque.peek() == i - k`), remove it from the deque because it is no longer in the current window.

4. **Remove smaller elements in the current window**:
    - Before adding the current element (`nums[i]`), remove all elements from the deque that are smaller than the current element, because they can never be the maximum for any future windows.
    - This ensures that elements in the deque are in decreasing order and the largest element remains at the front.

5. **Add the current element**:
    - After removing all smaller elements, add the current element's index (`i`) to the deque.

6. **Record the maximum**:
    - Once you've processed at least `k` elements (i.e., when `i >= k - 1`), the front of the deque contains the index of the maximum element in the current window. Store `nums[deque.peek()]` in the result array.

7. **Continue this process** for the rest of the array.

---

## Example Walkthrough:

Given `nums = [1, 3, -1, -3, 5, 3, 6, 7]` and `k = 3`, let's go through the steps:

### First Window (`i = 0 to 2`):
- Window: [1, 3, -1]
- Deque: Initially empty.
  - Add index `0` (value `1`).
  - Add index `1` (value `3`) and remove index `0` since `3 > 1`.
  - Add index `2` (value `-1`). Deque = `[1, 2]`.
  - Max value in this window is `nums[1] = 3`.

### Second Window (`i = 1 to 3`):
- Window: [3, -1, -3]
  - Index `1` (value `3`) remains.
  - Add index `3` (value `-3`), no smaller elements to remove.
  - Max value in this window is `nums[1] = 3`.

### Third Window (`i = 2 to 4`):
- Window: [-1, -3, 5]
  - Index `1` is out of the window (i.e., `i - k == 1`), remove it.
  - Add index `4` (value `5`), remove smaller elements at index `2` and `3`.
  - Max value in this window is `nums[4] = 5`.

### Continue the same process for the remaining windows...

---

## Time Complexity:

- Each element is added to the deque exactly once and removed exactly once, leading to an overall **O(n)** time complexity, where `n` is the length of the array.
- This is much more efficient than a brute-force solution, which would require recalculating the maximum for every window, leading to **O(n * k)** time complexity.

---

## Space Complexity:

- The space complexity is **O(k)** because, in the worst case, the deque holds at most `k` indices at any time (since it only holds indices from the current window).
