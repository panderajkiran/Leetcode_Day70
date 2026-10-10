# Leetcode_Day70
# Day 70: Search in Rotated Sorted Array

**LeetCode Problem:** 33. Search in Rotated Sorted Array  
**Difficulty:** Medium  
**Topic:** Binary Search, Arrays  
**Language:** Java

## Problem Statement

Given a sorted array that has been rotated at an unknown index and a target value, return the index of the target if it exists. Otherwise, return `-1`.

The solution must have **O(log n)** time complexity.

## Approach: Modified Binary Search

I solved this problem using a modified binary search algorithm.

Even though the array is rotated, at least one half of the current search range is always sorted because all elements are distinct.

1. Initialize `low` to `0` and `high` to the last index.
2. Calculate the middle index using `low + (high - low) / 2`.
3. If the middle element equals the target, return the middle index.
4. Check which half is sorted:
   - If the left half is sorted, check whether the target lies within that half.
   - Otherwise, the right half is sorted, so check whether the target lies within that half.
5. Eliminate the half that cannot contain the target and repeat.
6. If the target is not found, return `-1`.

## Java Solution

```java
class Solution {
    public int search(int[] nums, int target) {
        int low = 0;
        int high = nums.length - 1;

        while (low <= high) {
            int mid = low + (high - low) / 2;

            if (nums[mid] == target) {
                return mid;
            }

            if (nums[low] <= nums[mid]) {
                if (target >= nums[low] && target < nums[mid]) {
                    high = mid - 1;
                } else {
                    low = mid + 1;
                }
            } else {
                if (target > nums[mid] && target <= nums[high]) {
                    low = mid + 1;
                } else {
                    high = mid - 1;
                }
            }
        }

        return -1;
    }
}
```

## Example

**Input:**
```text
nums = [4,5,6,7,0,1,2]
target = 0
```

**Output:**
```text
4
```

**Explanation:** The target `0` is present at index `4`.

## Complexity Analysis

- **Time Complexity:** O(log n) — Each iteration eliminates approximately half of the remaining search range.
- **Space Complexity:** O(1) — Only a few variables are used.

## What I Learned

- How binary search can work on a rotated sorted array.
- How to identify the sorted half of an array.
- How to decide which half to eliminate based on the target's range.
- Why careful boundary conditions are important in binary search.

## Takeaway

Today's problem taught me that even when things look out of order, there is often a pattern we can use to find our way forward.

Instead of checking everything, identifying the right structure helps us make smarter decisions.

**Day 70 complete — one more problem solved, one more concept understood.**
