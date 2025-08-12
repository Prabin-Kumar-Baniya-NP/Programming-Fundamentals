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

- **Brute Force Solution (v1)**  
```py
def get_unique_triplet(arr: list) -> list[int]:
    n = len(arr)
    triplet_keys = set()
    result = []

    for i in range(0, n):
        for j in range(i + 1, n):
            for k in range(j + 1, n):
                current_sum = arr[i] + arr[j] + arr[k]
                if current_sum == 0 and (i != j and i != k and j != k):
                    triplet = [arr[i], arr[j], arr[k]]
                    key = "".join([str(item) for item in set(triplet)])
                    if key not in triplet_keys:
                        result.append(triplet)
                        triplet_keys.add(key)

    return result

arr = [-1, 0, 1, 2, -1, -4]
print(get_unique_triplet(arr))
```
```
Time Complexity:  
    - Outer loop: O(n)  
    - Middle loop: O(n)  
    - Inner loop: O(n)  
    - Total: O(n³)

Space Complexity: O(k)  
    - triplet_keys set → O(k)  
    - result list → O(k)  
    - k = number of unique triplets found (worst case k ≤ C(n,3) = O(n³))
```

---

- **Two Pointer with Set for Duplicate Removal (v2)**  
```py
def get_unique_triplet_v2(arr: list) -> list[int]:
    n = len(arr)
    arr.sort()
    triplet_keys = set()
    result = []

    for i in range(0, n):
        j = i + 1
        k = n - 1
        while j < k:
            current_sum = arr[i] + arr[j] + arr[k]
            if current_sum == 0 and (i != j and i != k and j != k):
                triplet = [arr[i], arr[j], arr[k]]
                key = "".join([str(item) for item in set(triplet)])
                if key not in triplet_keys:
                    result.append(triplet)
                    triplet_keys.add(key)
                j += 1
                k -= 1
            elif current_sum < 0:
                j += 1
            else:
                k -= 1
    return result
```
```
Time Complexity:  
    - Sorting: O(n log n)  
    - Outer loop: O(n)  
    - Two-pointer scan per i: O(n) → O(n²) total  
    - Overall: O(n²) (sorting is smaller term)

Space Complexity: O(k)  
    - triplet_keys set → O(k)  
    - result list → O(k)  
    - k = number of unique triplets found (worst case k ≤ O(n²))
```

---

- **Two Pointer with In-Loop Duplicate Skipping (v3)**  
```py
def get_unique_triplet_v3(arr: list) -> list[int]:
    n = len(arr)
    arr.sort()
    result = []

    for i in range(0, n):
        if i > 0 and arr[i] == arr[i - 1]:
            continue
        j = i + 1
        k = n - 1
        while j < k:
            current_sum = arr[i] + arr[j] + arr[k]
            if current_sum == 0 and (i != j and i != k and j != k):
                result.append([arr[i], arr[j], arr[k]])
                j += 1
                k -= 1
                while j < k and arr[j] == arr[j - 1]:
                    j += 1
                while j < k and arr[k] == arr[k + 1]:
                    k -= 1
            elif current_sum < 0:
                j += 1
            else:
                k -= 1
    return result
```
```
Time Complexity:  
    - Sorting: O(n log n)  
    - Outer loop: O(n)  
    - Two-pointer scan per i: O(n) → O(n²) total  
    - Overall: O(n²)

Space Complexity: O(k)  
    - result list → O(k) 
```

## Pattern 2: Sliding Window

### Easy: Maximum Sum Subarray of Size K

- Problem: Given an array of positive numbers and a positive integer k, find the maximum sum of any contiguous subarray of size k.
- Example: Input: arr = [1, 4, 2, 10, 2, 3, 1, 0, 20], K = 3 -> Output: 21 (from subarray [1, 0, 20])
- Approach: Calculate the sum of the first k elements. Then, slide the window: subtract the element leaving the window and add the new element entering the window. Keep track of the maximum sum found.

| Feature              | Contiguous              | Subsequence                    |
| -------------------- | ----------------------- | ------------------------------ |
| **Skip allowed?**    | ❌ No                    | ✅ Yes                          |
| **Order preserved?** | ✅ Yes                   | ✅ Yes                          |
| **Defined by**       | Start index & end index | Selection of elements in order |
| **Example**          | `[2, 3, 4]`             | `[2, 4]`                       |

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

### Hard: Minimum Window Substring

- Problem: Given two strings s and t, find the minimum window substring of s that contains all the characters of t.
- Example: Input: s = "ADOBECODEBANC", t = "ABC" -> Output: "BANC"
- Approach: Use a sliding window and a frequency map for characters in t. Expand the window to include all characters from t, then try to shrink it from the left while maintaining the condition.

```py
def initialize_required_char_freq(string: str):
    frequency_map = {}
    for char in string:
        frequency_map[char] = frequency_map.get(char, 0) + 1
    return frequency_map

def is_minimum_char_freq_satisfied(current_freq: dict, required_freq: dict):
    for char, freq in required_freq.items():
        if current_freq.get(char, 0) < freq:
            return False
    return True

def min_window_substring(s: str, t: str) -> str:
    left_pointer = 0
    string_length = len(s)
    current_freq = {}
    required_freq = initialize_required_char_freq(t)
    best_window_indices = [0, 0]
    best_window_length = float("inf")

    for right_pointer in range(string_length):
        current_char = s[right_pointer]
        current_freq[current_char] = current_freq.get(current_char, 0) + 1

        while is_minimum_char_freq_satisfied(current_freq, required_freq):
            current_window_size = right_pointer - left_pointer + 1
            if current_window_size < best_window_length:
                best_window_length = current_window_size
                best_window_indices = [left_pointer, right_pointer + 1]

            # shrink window from the left
            left_char = s[left_pointer]
            current_freq[left_char] -= 1
            if current_freq[left_char] == 0:
                del current_freq[left_char]
            left_pointer += 1

    return "" if best_window_length == float("inf") else s[best_window_indices[0]:best_window_indices[1]]
```
```
Time: O(|s|) — Each character visited at most twice (once by right pointer, once by left pointer).
Space: O(|s| + |t|) in worst case (frequency maps). If fixed alphabet (like ASCII), O(1).
```

## Pattern 3:  Prefix Sum / Suffix Sum 

###  Easy: Range Sum Query - Immutable

- Problem: Given an integer array nums, handle multiple queries of the form sumRange(i, j), which returns the sum of elements between indices i and j (inclusive). 
- Example: Input: nums = [-2, 0, 3, -5, 2, -1], sumRange(0, 2) -> Output: 1 ((−2)+0+3=1) 
- Approach: Create a prefix sum array P where P[i] is the sum of nums[0] through nums[i-1]. Then sumRange(i, j) is simply P[j+1] - P[i].

```
nums = [-2,  0,  3,  -5,  2,  -1]

P[0] = 0
       (No elements yet → sum = 0)

P[1] = P[0] + nums[0]
     = 0 + (-2)
     = -2
       (Covers: -2)

P[2] = P[1] + nums[1]
     = -2 + 0
     = -2
       (Covers: -2, 0)

P[3] = P[2] + nums[2]
     = -2 + 3
     = 1
       (Covers: -2, 0, 3)

P[4] = P[3] + nums[3]
     = 1 + (-5)
     = -4
       (Covers: -2, 0, 3, -5)

P[5] = P[4] + nums[4]
     = -4 + 2
     = -2
       (Covers: -2, 0, 3, -5, 2)

P[6] = P[5] + nums[5]
     = -2 + (-1)
     = -3
       (Covers: -2, 0, 3, -5, 2, -1)

```
```py
def build_prefix(arr: list[int]) -> list[int]:
    n = len(arr)
    prefix_sum = [0] * (n+1)
    for i in range(n):
        prefix_sum[i+1] = prefix_sum[i] + arr[i]
    return prefix_sum

def sumRange(prefix_sum, i, j):
    return prefix_sum[j + 1] - prefix_sum[i]


arr = [-2,  0,  3,  -5,  2,  -1]
print(sumRange(
    prefix_sum=build_prefix(arr=arr),
    i=0,
    j=4
))
```

```
**Time Complexity**
- `build_prefix`: O(n)
- `sumRange`: O(1)
- Overall (n elements, q queries): O(n + q)

**Space Complexity**
- Extra space for prefix array: O(n)
- Query space: O(1)
```

### Medium: Subarray Sum Equals K

- Problem: Given an array of integers nums and an integer k, return the total number of continuous subarrays whose sum equals k. 
- Example: Input: nums = [1, 1, 1], k = 2 -> Output: 2 (subarrays [1,1] from index 0 and [1,1] from index 1) 
- Approach: Use prefix sums and a hash map. Maintain a running sum. For each element, check if current_sum - k exists in the hash map. If it does, add its frequency to the count. Store current_sum and its frequency in the map.

```py
def build_prefix_sum(arr:list[int]) -> list[int]:
    n = len(arr)
    prefix_sum: list[int] = [0] * (n + 1)

    for i in range(n):
        prefix_sum[i+1] = prefix_sum[i] + arr[i]
    return prefix_sum

def sumRange(prefix_sum: list[int], i: int, j: int) -> int:
    return prefix_sum[j + 1] - prefix_sum[i]

def get_subarray_sum_count(arr: list[int], target_sum: int) -> int:
    n = len(arr)
    prefix_sum = build_prefix_sum(arr=arr)
    count = 0

    for i in range(n):
        for j in range(i+1, n):
            if sumRange(prefix_sum=prefix_sum, i=i, j=j) == target_sum:
                count += 1
    return count

# Example
arr = [1, 1, 1]
k = 2
print(get_subarray_sum_count(arr, k))  # Output: 2
```

### Hard: Find Pivot Index / Equilibrium Index 
- Problem: Given an array of integers nums, calculate the pivot index of this array. The pivot index is the index  where the sum of all the numbers strictly to the left of the index is equal to the sum of all the numbers strictly to  the right of the index. 
- Example: Input: nums = [1, 7, 3, 6, 5, 6] -> Output: 3 (At index 3, left sum 1+7+3=11, right sum 5+6=11) 
- Approach: Calculate the total sum of the array. Iterate through the array, maintaining a left_sum. For each element, check if left_sum equals total_sum - left_sum - current_element.

```py
def build_prefix_sum(arr:list[int]) -> list[int]:
    n = len(arr)
    prefix_sum: list[int] = [0] * (n + 1)

    for i in range(n):
        prefix_sum[i+1] = prefix_sum[i] + arr[i]
    return prefix_sum

def sumRange(prefix_sum: list[int], i: int, j: int) -> int:
    return prefix_sum[j + 1] - prefix_sum[i]

def get_pivot_element(arr: list[int]) -> int:
    n = len(arr)
    prefix_sum = build_prefix_sum(arr=arr)

    for k in range(1, n):
        left_sum = sumRange(prefix_sum=prefix_sum, i=0, j=k-1)
        right_sum = sumRange(prefix_sum=prefix_sum, i=k+1, j=n-1)

        if left_sum == right_sum:
            return arr[k]
    return -1

arr = [1, 7, 3, 6, 5, 6]
print(get_pivot_element(arr=arr))
```
```
Time Complexity
build_prefix → O(n)
Loop through each index → O(n)
Each sumRange call is O(1) (because we just do subtraction from the prefix array).
Total: O(n) + O(n) = O(n)

Space Complexity
Prefix sum array: size n+1 → O(n)
A few variables → O(1) extra
Total: O(n)
```

## Pattern 5: In-place Operations / Modifications

### Easy: Remove Duplicates from Sorted Array In-place 
- Problem: Given a sorted array nums, remove the duplicates in-place such that each unique element appears only once. The relative order of the elements should be kept the same. 
- Example: Input: nums = [1,1,2] -> Output: 2, with nums becoming [1,2,_] (underscores denote irrelevant values  beyond the new length). 
- Approach: Use two pointers: one to iterate through the array, and another to keep track of the position of the next unique element. 

```
Given array: [1, 1, 2, 2, 3, 3]

Step 1:
i = 1
Compare arr[1] = 1 with arr[0] = 1
They are equal, no change
unique_pos = 1

Step 2:
i = 2
Compare arr[2] = 2 with arr[1] = 1
They are different
Place arr[2] (2) at arr[unique_pos] -> arr[1] = 2
Increment unique_pos to 2
Array now: [1, 2, 2, 2, 3, 3]

Step 3:
i = 3
Compare arr[3] = 2 with arr[2] = 2
They are equal, no change
unique_pos = 2

Step 4:
i = 4
Compare arr[4] = 3 with arr[3] = 2
They are different
Place arr[4] (3) at arr[unique_pos] -> arr[2] = 3
Increment unique_pos to 3
Array now: [1, 2, 3, 2, 3, 3]

Step 5:
i = 5
Compare arr[5] = 3 with arr[4] = 3
They are equal, no change
unique_pos = 3

Final result:
Length of unique elements = 3
Unique elements = arr[:3] -> [1, 2, 3]
```

```py
arr = [1,1,2,2,2,2,3,4,4,4,5,5,6]

def remove_duplicates(arr: list[int | str]):
    n = len(arr)
    unique_pos = 1

    for i in range(1, n):
        if arr[i] != arr[i-1]:
            arr[unique_pos] = arr[i]
            unique_pos += 1
    return unique_pos

unique_pos = remove_duplicates(arr) # 6
print(arr) # [1, 2, 3, 4, 5, 6, 3, 4, 4, 4, 5, 5, 6]
```

### Medium: Rotate Array 
- Problem: Given an integer array nums, rotate the array to the right by k steps, where k is non-negative. Perform the rotation in-place. 
- Example: Input: nums = [1,2,3,4,5,6,7], k = 3 -> Output: [5,6,7,1,2,3,4] 

```
Steps:
[1,2,3,4,5,6,7], k=3

1. Reverse 0 to k: [1,2,3,4] => [4,3,2,1]
2. Reverse k to n: [5,6,7] => [7,6,5]
3. Reverse entire array: [4,3,2,1,7,6,5] => [5,6,7,1,2,3,4]
```
### Hard: First Missing Positive 
- Problem: Given an unsorted integer array nums, return the smallest missing positive integer. You must implement an algorithm that runs in O(N) time and uses O(1) auxiliary space. 
- Example: Input: nums = [3,4,-1,1] -> Output: 2 
- Approach: Use the array itself as a hash map. Try to place each positive number x at index x-1. Iterate and find the first index i where nums[i] != i+1.

## Pattern 6: Hashing / Frequency Counting

### Easy: Contains Duplicate 
- Problem: Given an integer array nums, return true if any value appears at least twice in the array, and return false if every element is distinct. 
- Example: Input: nums = [1,2,3,1] -> Output: true 
- Approach: Use a hash set to store seen elements. Iterate through the array; if an element is already in the set, return true. Otherwise, add it.

```py
def is_duplicate_exists(arr: list) -> bool:
    freq = {}
    for item in arr:
        freq[item] = freq.get(item, 0) + 1
    
    for item, count in freq.items():
        if count >= 2:
            return True
    return False

nums = [1,2,3,4]
print(is_duplicate_exists(arr=nums))
```

### Medium: Group Anagrams 
- Problem: Given an array of strings strs, group the anagrams together. You can return the answer in any order. 
- An Anagram is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once. 
- Example: Input: strs = ["eat","tea","tan","ate","nat","bat"] -> Output: [["bat"],["nat","tan"],["ate","eat","tea"]] 
- Approach: For each string, create a canonical representation (e.g., sorted string or character count array). Use this representation as a key in a hash map, and store lists of anagrams as values.

```py
def group_anagrams(strs: list[str]) -> list[list[str]]:
    word_keys: dict[str, list] = {}
    
    for item in strs:
        chars: list = sorted(item)
        key = "".join(chars)

        if key not in word_keys.keys():
            word_keys[key] = [item]
        else:
            word_keys[key].append(item)
    return list(word_keys.values())

strs = ["eat","tea","tan","ate","nat","bat"]
print(group_anagrams(strs=strs))
```

### Hard: Longest Consecutive Elements Sequence
- Problem: Given an unsorted array of integers nums, return the length of the longest consecutive elements sequence. 
- You must write an algorithm that runs in O(N) time. 
- Example: Input: nums = [100,4,200,1,3,2] -> Output: 4 (The longest consecutive sequence is [1, 2, 3, 4]) 
- Approach: Store all numbers in a hash set for O(1) lookups. Iterate through the set. For each number, check if number - 1 exists. If not, it's a potential start of a sequence. Then count the consecutive numbers from there by checking number + 1, number + 2, etc.

```py
def get_longest_consecutive(arr: list[int]) -> int:
    num_set = set(arr)
    longest_consecutive = 0
    current_sequence_length = 0

    for num in num_set:
        current_num = num
        current_sequence_length = 1

        while current_num + 1 in num_set:
            current_num += 1
            current_sequence_length += 1
        
        longest_consecutive = max(longest_consecutive, current_sequence_length)
    return longest_consecutive

nums = [100,4,4,200,201,202,203,204,205,1,2]
```
```
Time Complexity: 0(n^2)
We are re-checking for sequence for every single element in the array.
```

- Optimized approach - run while loop only when sequence is started
```
nums = [1,2,3,4,5,10,11,16,17,18,19,20,21,22,23]

1 - run the while loop
1-1=0 and 0 in num_Set = No

10 - run the while loop
(10-1) = 9 and 9 in num set = No

16 - run the while loop
(16-1) = 15 and 15 in num set = No

3-1=2 and 2 in num set = Yes


num-1 not in num_set:
    while loop
```
```py
def get_longest_consecutive(arr: list[int]) -> int:
    num_set = set(arr)
    longest_consecutive = 0
    current_sequence_length = 0

    for num in num_set:
        if num-1 not in num_set:
            current_num = num
            current_sequence_length = 1

            while current_num + 1 in num_set:
                current_num += 1
                current_sequence_length += 1
        longest_consecutive = max(longest_consecutive, current_sequence_length)
    return longest_consecutive

nums = [1,2,3,4,5,10,11,16,17,18,19,20,21,22,23]
```