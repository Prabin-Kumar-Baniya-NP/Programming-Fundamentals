# Arrays

- Linear Search Vs Binary Search
    - Linear Search: Use when array is unsorted
    - Binary Search: Use when array is sorted
```py
def linear_search(arr:List, search: int) -> int:
    for index, item in enumerate(arr):
        if item == search:
            return index
    return -1
```
```py
def binary_search(arr: List, target: int) -> int:
    left = 0
    right = len(arr) - 1

    while (left <= right):
        mid = (left+right)//2

        if target == arr[mid]:
            return mid
        elif target < arr[mid]:
            right = mid-1
        elif target > arr[mid]:
            left = mid + 1
    return -1
```

- Sorting Algorithms CheatSheet
```
# 📘 Sorting Algorithms Cheat Sheet

| Algorithm        | Best Time     | Average Time  | Worst Time    | Space       | Stable | In-place |
|------------------|---------------|---------------|---------------|-------------|--------|----------|
| **Bubble Sort**  | O(n)          | O(n²)         | O(n²)         | O(1)        | ✅     | ✅       |
| **Selection Sort | O(n²)         | O(n²)         | O(n²)         | O(1)        | ❌     | ✅       |
| **Insertion Sort | O(n)          | O(n²)         | O(n²)         | O(1)        | ✅     | ✅       |
| **Merge Sort**   | O(n log n)    | O(n log n)    | O(n log n)    | O(n)        | ✅     | ❌       |
| **Quick Sort**   | O(n log n)    | O(n log n)    | O(n²)         | O(log n)*   | ❌     | ✅       |
| **Heap Sort**    | O(n log n)    | O(n log n)    | O(n log n)    | O(1)        | ❌     | ✅       |
| **Counting Sort**| O(n + k)      | O(n + k)      | O(n + k)      | O(k)        | ✅     | ❌       |
| **Radix Sort**   | O(nk)         | O(nk)         | O(nk)         | O(n + k)    | ✅     | ❌       |
| **Bucket Sort**  | O(n + k)      | O(n + k)      | O(n²)         | O(n + k)    | ✅     | ❌       |
| **Tim Sort**     | O(n)          | O(n log n)    | O(n log n)    | O(n)        | ✅     | ✅       |

🔹 Notes:
- `n` = number of elements
- `k` = range of input (for Counting/Radix/Bucket Sort)
- `*` Quick Sort space complexity is O(log n) due to recursion stack
- In sorting algorithms, stability refers to whether the algorithm preserves the relative order of equal elements.
- An in-place algorithm sorts the data without using extra space (or uses only a small, constant amount of additional memory).
```
- Array Vs Subarray Vs Subsequence
```
| Term           | Definition                                                   | Contiguous? | Order Maintained? | Example from `[1, 2, 3, 4]`              |
|----------------|--------------------------------------------------------------|-------------|-------------------|------------------------------------------|
| **Array**      | The entire collection of elements                            | Yes         | Yes               | `[1, 2, 3, 4]`                           |
| **Subarray**   | A continuous part (slice) of the array                       | Yes         | Yes               | `[2, 3]`, `[1, 2, 3]`                    |
| **Subsequence**| Any ordered sequence from the array without being contiguous | No          | Yes               | `[1, 3, 4]`, `[2, 4]`, `[1, 2, 3, 4]`    |

---

### Key Points:
- **Subarray = contiguous slice of the array.**
- **Subsequence = ordered elements, possibly skipping some elements.**
- **Array = the full list itself.**
```

## Pattern 1: Two Pointer Approach

### Easy : Reverse an Array In-place
Problem: Given an array, reverse its elements in-place.
Example: Input: [1, 2, 3, 4, 5] -> Output: [5, 4, 3, 2, 1]



```py
arr = [1, 2, 3, 4, 5]
start = 0
end = len(arr) - 1

while (start <= end):
    arr[start], arr[end] = arr[end], arr[start]
    start += 1
    end -= 1

print(arr)
```
```
Approach: Use one pointer at the start and one at the end. Swap elements and move pointers towards the center until they meet or cross.
Time Complexity: O(n)
```

### Medium: Find a Pair with a Given Sum in a Sorted Array
Problem: 
- Given a sorted array of integers and a target sum, and if there exists a pair of elements that sum up to the target. 
- Return their indices or true/false.
- Example: Input: arr = [2, 7, 11, 15], target = 9 -> Output: [0, 1] or true

```py
from typing import List


def check_sum(arr: List, target_sum: int) -> List | bool:
    left = 0
    right = len(arr) - 1

    while left <= right:
        current_sum = arr[left] + arr[right]
        if current_sum > target_sum:
            right -= 1
        elif current_sum < target_sum:
            left += 1
        elif current_sum == target_sum:
            return [left, right]
    return False


arr = [2, 7, 11, 15]
target_sum = 11
result = check_sum(arr=arr, target_sum=target_sum)
print(result)
```
```
Approach: Use two pointers, left at the beginning and right at the end. 
If arr[left] + arr[right] is less than target, increment left. If greater, decrement right. If equal, you found the pair.

Time Complexity: O(n)
```

### Hard: 3 Sum

- Given an integer array nums, find all the unique triplets [nums[i], nums[j], nums[k]] such that i != j, i != k, and j != k, and their sum is equal to zero (nums[i] + nums[j] + nums[k] == 0).

- Key Constraints:
    - The indices i, j, and k must be distinct.
    - The solution set must not contain duplicate triplets. This means that even if different indices produce the same set of three numbers, that triplet should only be included once in the output. 
    - For example, if nums = [-1, 0, 1, 2, -1, -4], the triplet [-1, 0, 1] can be formed in multiple ways, but it should only appear once in the final result.

- Brute Force Solution
```py
from typing import List

def three_sum(arr: List):
    n = len(arr)
    unique_triplet_keys = set() 
    result = []
    for i in range(0, n):
        for j in range(i+1, n):
            for k in range(j+1, n):
                if (arr[i] + arr[j] + arr[k]) == 0:
                    triplets = {arr[i], arr[j], arr[k]}
                    key = "".join([str(item) for item in triplets])
                    if key not in unique_triplet_keys:
                        result.append([arr[i], arr[j], arr[k]])
                        unique_triplet_keys.add(key)
    return result

arr = [-1, 0, 1, 2, -1, -4]
print(three_sum(arr))

```
```
Time Complexity: 0(n^3)
Space Complexity: 0(n)

Note:
- We sort the array to avoid duplicate triplets. Example: [-1, 3, -2] and [-2, 3, -1] after sorting will be equivalent to [-3, -1, 2]
```

- Two Pointer Approach
```py
from typing import List

def unique_triplet(arr: List[int]) -> List[List[int]]:
    n = len(arr)
    arr.sort()
    triplets = []

    for i in range(n):
        if i > 0 and arr[i] == arr[i - 1]:
            continue  # skip duplicates for i

        left, right = i + 1, n - 1

        while left < right:
            total = arr[i] + arr[left] + arr[right]

            if total == 0:
                triplets.append([arr[i], arr[left], arr[right]])
                left += 1
                right -= 1

                # skip duplicates on the left
                while left < right and arr[left] == arr[left - 1]:
                    left += 1
                # skip duplicates on the right
                while left < right and arr[right] == arr[right + 1]:
                    right -= 1

            elif total < 0:
                left += 1
            else:
                right -= 1

    return triplets
```
```
Time Complexity: 
    - nums.sort() → O(n log n)
    - O(n log n + n^2) = O(n²)

Space Complexity: O(k)
    - K is the number of triplets returned from the array
```

### Pattern 2: Sliding Window

### Easy: Maximum Sum Subarray of Size K

- Problem: Given an array of positive numbers and a positive integer k, find the maximum sum of any contiguous subarray of size k.
- Example: Input: arr = [1, 4, 2, 10, 2, 3, 1, 0, 20], K = 3 -> Output: 21 (from subarray [1, 0, 20])
- Approach: Calculate the sum of the first k elements. Then, slide the window: subtract the element leaving the window and add the new element entering the window. Keep track of the maximum sum found.

```py
from typing import List

arr = [1, 4, 2, 10, 2, 3, 1, 0, 20]
k = 3

def max_sum_subarray(arr: List, k: int):
    left = 0
    right = k - 1
    max_sum = -1
    while (right < len(arr)):
        current_sum = sum([arr[i] for i in range(left, right+1)])

        max_sum = max(max_sum, current_sum)
        
        left += 1
        right += 1
        
    return max_sum
```
```
Time Complexity: O(n - k) ≈ O(n)
Space Complexity: 0(1)
```

### Medium: Longest Substring with K Distinct Characters
- Problem: Given a string (or character array) and an integer k, find the length of the longest substring in it that contains no more than k distinct characters.
- Example: Input: str = "araaci", K = 2 -> Output: 4 (for "araa")
- Approach: Use a sliding window and a hash map to keep track of character frequencies. Expand the window until it contains more than k distinct characters, then shrink from the left until the condition is met again.

```py
def longest_substring_with_k_distinct(s: str, k: int) -> int:
    if k == 0 or not s:
        return 0
    
    left = 0
    right = 0
    char_freq = {}
    max_len = 0

    for right in range(len(s)):
        char = s[right]
        char_freq[char] = char_freq.get(char, 0) + 1

        while len(char_freq) > k:
            left_char = s[left]
            char_freq[left_char] -= 1

            if char_freq[left_char] == 0:
                del char_freq[left_char]
            left += 1

        max_len = max(max_len, right-left+1)
    
    return max_len
```

```
Time Complexity: 0(n)
Space Complexity: 0(k)
```