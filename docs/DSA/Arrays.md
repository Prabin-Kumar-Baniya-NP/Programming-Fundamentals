# Arrays

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

arr = [-1, 0, 1, 2, -1, -1]

unique_keys = set()

def unique_triplet(arr: List):
    n = len(arr)

    # Sort the array to avoid duplicates
    arr.sort()
    triplets = []
    for i in range(0, n):

        if i > 0 and arr[i] == arr[i - 1]:
            continue  # skip duplicate values for i

        left = i + 1
        right = n - 1

        while (left < right):
            total = arr[i] + arr[left] + arr[right]

            if total == 0:
                # This is a vaid triplet
                triplets.append([arr[i], arr[left], arr[right]])
                left += 1
                right -= 1

                # Also Hanlde case for duplicate left and duplicate right
                # skip duplicates on both sides
                while left < right and arr[left] == arr[left - 1]:
                    left += 1
                while left < right and arr[right] == arr[right + 1]:
                    right -= 1

            elif total > 0:
                right -= 1
            
            elif total < 0:
                left += 1

    
    return triplets
```
```
Time Complexity: 
    - nums.sort() → O(n log n)
    - O(n log n + n^2) = O(n²)

Space Complexity: O(k)
    - K is the number of triplets returned from the array
```