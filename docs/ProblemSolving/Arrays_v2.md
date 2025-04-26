# Arrays

## Largest Elements

### Largest 3 elements in array

Given an array arr[], the task is to find the top three largest distinct integers present in the array.

Note: If there are less than three distinct elements in the array, then return the available distinct numbers in descending order.

```
Input: arr[] = [10, 4, 3, 50, 23, 90]
Output: [90, 50, 23]

Input: arr[] = [10, 9, 9]
Output: [10, 9]
There are only two distinct elements


Input: arr[] = [10, 10, 10]
Output: [10]
There is only one distinct element

Input: arr[] = []
Output: []

```
Algorithm:
```
1. Initialize three variables to store top elements:
   h1 = None   # Highest
   h2 = None   # Second highest
   h3 = None   # Third highest

2. Iterate over each element 'item' in the array:
   
   a. If h1 is None or item > h1:
       - h3 = h2
       - h2 = h1
       - h1 = item

   b. Else if (h2 is None or item > h2) and item != h1:
       - h3 = h2
       - h2 = item

   c. Else if (h3 is None or item > h3) and item != h1 and item != h2:
       - h3 = item

3. Initialize an empty list 'result'

4. Append h1, h2, and h3 to result if they are not None:
   - for x in [h1, h2, h3]:
       if x is not None:
           result.append(x)

5. Return result
```
Code:
```py
l = [10, 10, 10]

h1 = h2 = h3 = None

for item in l:
    if h1 is None or item > h1:
        h3 = h2
        h2 = h1
        h1 = item

    elif (h2 is None or item > h2) and item != h1:
        h3 = h2
        h2 = item

    elif (h3 is None or item > h3) and item != h1 and item != h2:
        h3 = item

result = []
for item in [h1, h2, h3]:
    if item is not None:
        result.append(item)

print(result)
```

### K-largest Element

Given an array arr[] and an integer k, the task is to find k largest elements in the given array. Elements in the output array should be in decreasing order.

```
Examples:
Input:  [1, 23, 12, 9, 30, 2, 50], k = 3
Output: [50, 30, 23]

Input:  [11, 5, 12, 9, 44, 17, 2], k = 2
Output: [44, 17]
```

Approach 1: Sort the array and return first k elements
```py
l = [1, 23, 12, 9, 30, 2, 50]
l = sorted(l)

print(l[:4])
```

Approach 2: Use Using Priority Queue(Min-Heap) #TBL

### Elements that appears N/K times

Given an array arr and an element k. The task is to find the count of elements in the array that appear more than n/k times and n is length of arr.

```
Input: arr = [3, 1, 2, 2, 1, 2, 3, 3], k = 4
Output: 2
Explanation: In the given array, 3 and 2 are the only elements that appears more than n/k times.
Input: arr = [2, 3, 3, 2], k = 3
Output: 2
Explanation: In the given array, 3 and 2 are the only elements that appears more than n/k times. So the count of elements are 2.
```

```py
l = [3, 1, 2, 2, 1, 2, 3, 3]
k = 4
occurrence = len(l)//k

freq = {}

for item in l:
    freq[item] = freq.get(item, 0) + 1

for num, count in freq.items():
    if count > occurrence:
        print(num)
```


## Rotation

### Rotate Array by d position to left

Given an array arr[] of size N, the task is to rotate the array by d position to the left.

```
Input:  arr[] = {1, 2, 3, 4, 5, 6, 7}, d = 2
Output: 3, 4, 5, 6, 7, 1, 2
Explanation: If the array is rotated by 1 position to the left, 
it becomes {2, 3, 4, 5, 6, 7, 1}.
When it is rotated further by 1 position,
it becomes: {3, 4, 5, 6, 7, 1, 2}
Input: arr[] = {1, 6, 7, 8}, d = 3
Output: 8, 1, 6, 7
```

Algorithm:
```
Step 1: reverse elements from i=0 to d-1: {6,1,7,8}
Step 2: reverse elements from d to n-1: {6,1,8,7}
Step 3: reverse elements from i=0 to n-1: {7,8,1,6}
```

```py
l = [1,6,7,8,9]
d = 2
n = len(l)

def reverse(arr, start, end):
    while(start <= end):
        arr[start], arr[end] = arr[end], arr[start]
        start += 1 
        end -= 1
    return arr
        

# Left Rotate by d 
l = reverse(l, 0, d-1)
l = reverse(l, d, n-1)
l = reverse(l, 0, n-1)
print(l) # [7, 8, 9, 1, 6]

l2 = [1,6,7,8,9,10]
d=2
```
Time Complexity
```
O(d) + O(n - d) + O(n)
= O(d + (n - d) + n)
= O(n + n)
= O(2n)
= O(n) we ignore constant factor
```

### Rotation Count in Rotated Sorted Array

Given an array arr[] having distinct numbers sorted in increasing order and the array has been right rotated (i.e, the last element will be cyclically shifted to the starting position of the array) k number of times, the task is to find the value of k.

```
Input: arr[] = {15, 18, 2, 3, 6, 12}
Output: 2
Explanation: Initial array must be {2, 3, 6, 12, 15, 18}. 
We get the given array after rotating the initial array twice.

Input: arr[] = {7, 9, 11, 12, 5}
Output: 4

Input: arr[] = {7, 9, 11, 12, 15};
Output: 0
```

<b>Approach 1: O(n) - Check if arr[i] > arr[i+1] if yes store k = i+1</b>
```
arr = [7, 9, 11, 12, 15]
k = 0
for i in range(0, len(arr)-1):
    if arr[i] > arr[i+1]:
        k = i+1
        break
print(k)
```

<b>Approach 2: O(log n) - Binary Search</b>

This question is equal to finding the index of the minimum element.

Algorithm
```
Step 1: Store low, high and keep iterating till low <= high
Step 2: In each iteration, find mid index, prev from mid and next from mid
Step 3: if mid is less than prev and mid is less than next -> return mid because it is smallest element
Step 4: If mid is not smallest -> We need to increase/decrease high/low
Step 5: If arr[mid] <= arr[high] => right side is sorted -> Go Left -> high = mid -1
				                 => left side is sorted  -> Go Right -> left = mid + 1
Step 6: Return default value of 0 if array is already sorted
```


```py
def find_rotation_count(arr):
    n = len(arr)
    low, high = 0, n - 1

    while low <= high:
        # Case: Subarray is already sorted
        if arr[low] <= arr[high]:
            return low

        mid = (low + high) // 2
        prev_idx = (mid - 1 + n) % n
        next_idx = (mid + 1) % n

        # Check if mid is the minimum
        if arr[mid] <= arr[prev_idx] and arr[mid] <= arr[next_idx]:
            return mid

        # Right half is sorted → Go left
        if arr[mid] <= arr[high]:
            high = mid - 1
        # Left half is sorted → Go right
        else:
            low = mid + 1

    return 0
```

## Sorting

### Bubble Sort

- Time Complexity: O(n^2)
- In bubble sort, we repeatedly swap two adjacent elements if they are in wrong order.
- We run two loop: 
    - outer loop from 0 to n-1
    - inner loop from 0 to n-1-i. [-i because highest numbers are bubbled out at the end of array]

Algorithm:
```
- Example for {5,4,3,2,1}
    - Step 1: {5,4,3,2,1} => {4,3,2,1,5}
    - Step 2: {4,3,2,1} => {3,2,1,4,5}
    - Step 3: {3,2,1} => {2,1,3,4,5}
    - Step 4: {2,1} => {1,2,3,4,5}
```
Code:
```py
arr = [5,4,3,2,1]
n = len(arr)
for i in range(0, n-1):
    for j in range(0, n-i-1):
        if arr[j] > arr[j+1]:
            arr[j], arr[j+1] = arr[j+1], arr[j]

print(arr)
```

### Selection Sort
- Time Complexity : O(n^2)
- Auxiliary Space : O(1)
- Select minimum element from unsorted array and swap at at the beginning of unsorted array

Algorithm
```
Original Array: [5,4,3,2,1]
i=0: sorted part = [], unsorted part = [1,5,4,3,2], min=1
i=1: sorted part = [1], unsorted part = [5,4,3,2], min=2
i=2: sorted part = [1,2], unsorted part = [5,4,3], min=3
i=3: sorted part = [1,2,3], unsorted part = [5,4], min=4
i=4: sorted part = [1,2,3,4], unsorted part = [5], min=5
i=5: sorted part = [1,2,3,4,5], unsorted part = []
```
Code
```py
arr = [5,4,3,2,1]
n = len(arr)
for i in range(0, n): # Sorted Part
    min_index = i
    for j in range(i+1, n): # Unsorted Part
        if arr[j] < arr[min_index]:
            min_index = j
    
    # Swap element at min_index and element at i
    arr[min_index], arr[i] = arr[i], arr[min_index]

print(arr)
```

### Insertion Sort

TBL

### Merge Sort

TBL

### Quick Sort

TBL

### Heap Sort

TBL

## Searching

### Count Possible Triangles

Given an unsorted array of positive integers, the task is to find the number of triangles that can be formed with three different array elements as three sides of triangles.

For a triangle to be possible from 3 values as sides, the sum of the two values (or sides) must always be greater than the third value (or third side). 

```
Input: arr[] = [4, 6, 3, 7]
Output: 3
Explanation: There are three triangles possible [3, 4, 6], [4, 6, 7] and [3, 6, 7]. 
Note that [3, 4, 7] is not a possible triangle.  

Input: arr[] = [10, 21, 22, 100, 101, 200, 300]
Output: 6
Explanation: There can be 6 possible triangles: 
[10, 21, 22], [21, 100, 101], [22, 100, 101], [10, 100, 101], [100, 101, 200] and [101, 200, 300]

Input: arr[] = [1, 2, 3]
Output: 0
Examples: No triangles are possible.
```

<b>Approach 1: O(n^3) - Use 3 nested loop </b>
```py
arr = [10, 21, 22, 100, 101, 200, 300]
arr.sort()
n = len(arr)
result = []

for i in range(n):
    for j in range(i + 1, n):
        for k in range(j + 1, n):
            # Since array is sorted, we only need one condition
            if arr[i] + arr[j] > arr[k]:
                result.append([arr[i], arr[j], arr[k]])

print(len(result))
print(result)
```
<b>Approach 2: O(n^2) - Two Pointer Approach : First Sort it then apply math</b>

- Algorithm
```
Sort the array:
arr = [10, 21, 22, 100, 101, 200, 300]

Initialize count = 0

Outer loop starts (i = 6):

1. Fix largest side: arr[6] = 300
   - left = 0, right = 5
   - arr[0] + arr[5] = 10 + 200 = 210 (Not > 300), move left to 1
   - arr[1] + arr[5] = 21 + 200 = 221 (Not > 300), move left to 2
   - arr[2] + arr[5] = 22 + 200 = 222 (Not > 300), move left to 3
   - arr[3] + arr[5] = 100 + 200 = 300 (Not > 300), move left to 4
   - arr[4] + arr[5] = 101 + 200 = 301 (Valid), count += (right - left) = 1, move right to 4

2. Fix largest side: arr[5] = 200
   - left = 0, right = 4
   - arr[0] + arr[4] = 10 + 101 = 111 (Not > 200), move left to 1
   - arr[1] + arr[4] = 21 + 101 = 122 (Not > 200), move left to 2
   - arr[2] + arr[4] = 22 + 101 = 123 (Not > 200), move left to 3
   - arr[3] + arr[4] = 100 + 101 = 201 (Valid), count += (right - left) = 1, move right to 3

3. Fix largest side: arr[4] = 101
   - left = 0, right = 3
   - arr[0] + arr[3] = 10 + 100 = 110 (Not > 101), move left to 1
   - arr[1] + arr[3] = 21 + 100 = 121 (Valid), count += (right - left) = 2, move right to 2

4. Fix largest side: arr[3] = 100
   - left = 0, right = 2
   - arr[0] + arr[2] = 10 + 22 = 32 (Not > 100), move left to 1
   - arr[1] + arr[2] = 21 + 22 = 43 (Not > 100), move left to 2

Final count = 6 triangles

Output:
6

```
```py
arr = [10, 21, 22, 100, 101, 200, 300]

n = len(arr)
count = 0

for i in range(n - 1, 1, -1):  # Fix the largest side at arr[i]
    left, right = 0, i - 1
    while left < right:
        if arr[left] + arr[right] > arr[i]:
            count += (right - left)
            right -= 1
        else:
            left += 1

print(count)
```

### Element Occurring only Once
Find the number that appears once, and the other numbers twice
```
Example 1:
Input Format: arr[] = {2,2,1}
Result: 1
Explanation: In this array, only the element 1 appear once and so it is the answer.

Example 2:
Input Format: arr[] = {4,1,2,1,2}
Result: 4
Explanation: In this array, only element 4 appear once and the other elements appear twice. So, 4 is the answer.
```

<b>Approach 1: Use a Frequency Counter</b>

- Time Complexity: O(n)
- Space Complexity: O(k) where k is number of unique items in array
```py
arr = [4,1,2,1,2]
freq = {}

for item in arr:
    freq[item] = freq.get(item, 0) + 1 

for num, count in freq.items():
    if count == 1:
        print(num)
```
<b>Approach 2: Use XOR Property</b>

- Time Complexity: 0(n)
- Space Complexity: 0(1)

```
XOR of two same numbers is always 0 i.e. a ^ a = 0. ←Property 1.
XOR of a number with 0 will result in the number itself i.e. 0 ^ a = a.  ←Property 2

Assume the given array is: [4,1,2,1,2]
XOR of all elements = 4^1^2^1^2
      = 4 ^ (1^1) ^ (2^2)
      = 4 ^ 0 ^ 0 = 4^0 = 4
```
```py
arr = [4,1,2,1,2]

def get_single_element(arr):
    xor=0
    for item in arr:
        xor = xor ^ item
    return xor

print(get_single_element(arr))
```

### Leaders in an array

Given an array arr[] of size n, the task is to find all the Leaders in the array. An element is a Leader if it is greater than or equal to all the elements to its right side.

Note: The rightmost element is always a leader.

```
Input: arr[] = [16, 17, 4, 3, 5, 2]
Output: [17 5 2]
Explanation: 17 is greater than all the elements to its right i.e., [4, 3, 5, 2], therefore 17 is a leader. 5 is greater than all the elements to its right i.e., [2], therefore 5 is a leader. 2 has no element to its right, therefore 2 is a leader.

Input: arr[] = [1, 2, 3, 4, 5, 2]
Output: [5 2]
Explanation: 5 is greater than all the elements to its right i.e., [2], therefore 5 is a leader. 2 has no element to its right, therefore 2 is a leader.
```
Approach 1: Using Two Pointer Algorithm
Time Complexity: O(n^2)
Space Complexity: 0(1)
```py
arr = [16, 17, 4, 3, 5, 2]

n = len(arr)
for i in range(0, n):
    right_sum = arr[i]
    j = i+1 
    while(j<n):
        right_sum += arr[j]
        j+=1
    
    if arr[i] >= (right_sum - arr[i]):
        print(arr[i])
```
<b>Approach 2: Iterating from right side and Checking max element </b>
- Time Complexity: O(n)
- Space Complexity: 0(1)

```arr = [16, 17, 4, 3, 5, 2]
Start from right → left
Track maximum element seen so far

Step-by-step:

Index     arr[i]     max_element     Action
-----     ------     ------------    ----------------------
5         2          -9999           2 > -9999 → print(2), max_element = 2
4         5          2               5 > 2    → print(5), max_element = 5
3         3          5               3 <= 5   → skip
2         4          5               4 <= 5   → skip
1         17         5               17 > 5   → print(17), max_element = 17
0         16         17              16 <= 17 → skip

✅ Final Output: 2, 5, 17 (in reverse order of appearance)
```
```py
i = len(arr) - 1
max_element = -9999
while i >=0:
    if arr[i] > max_element:
        print(arr[i])
        max_element = arr[i]
    i -= 1
```

### Missing Number in Array

You are given an array arr[] of size n - 1 that contains distinct integers in the range from 1 to n (inclusive). This array represents a permutation of the integers from 1 to n with one element missing. Your task is to identify and return the missing element.

```
Input: arr[] = [1, 2, 3, 5]
Output: 4
Explanation: All the numbers from 1 to 5 are present except 4.

Input: arr[] = [8, 2, 4, 5, 3, 7, 1]
Output: 6
Explanation: All the numbers from 1 to 8 are present except 6.
```
<b>Approach 1: Using Factorial </b>
- Time Complexity: 0(n) + O(n) = O(2n) = O(n)
- Space Complexity: 0(1)

Algorithm
```
Factorial 5 is 5*4*3*2*1:
So, get max number from array and calculate its factorial
Now, keep dividing that factorial by each element and you will get missing number
```

```py
def factorial(num, fact=1):
    if num==0:
        return fact
    return factorial(num-1, fact*num)
    
    
arr = [8, 2, 4, 5, 3, 7, 1]
max_number = max(arr)
factorial = factorial(max_number)

for item in arr:
    factorial = factorial // item

print(factorial)

```

### LCM and HCF

- Least Common Multiple
```
LCM of 4 and 5:

    Multiples of 4: 4, 8, 12, 16, 20, 24, 28, 32, ...

    Multiples of 5: 5, 10, 15, 20, 25, 30, 35, ...

The smallest common multiple is 20. Hence, LCM(4, 5) = 20.
```

- HCF (Highest Common Factor) / GCD (Greatest Common Divisor)

```
HCF of 12 and 15:

    Factors of 12: 1, 2, 3, 4, 6, 12

    Factors of 15: 1, 3, 5, 15

The largest common factor is 3. Hence, HCF(12, 15) = 3.
```

## Missing Number

### Smallest Positive Missing Number

- Given an unsorted array arr[] with both positive and negative elements, the task is to find the smallest positive number missing from the array.
- Note: You can modify the original array.

```
Examples:

Input: arr[] = {2, -3, 4, 1, 1, 7}
Output: 3
Explanation: 3 is the smallest positive number missing from the array.


Input: arr[] = {5, 3, 2, 5, 1}
Output: 4
Explanation: 4 is the smallest positive number missing from the array.


Input: arr[] = {-8, 0, -1, -4, -3}
Output: 1 
Explanation: 1 is the smallest positive number missing from the array.
```

<b> Approach 1: Mark Presence of Number </b>

- Time Complexity: O(n)
- Space Complexity: O(1)

```
1. Segregate Positives:** `[2, 4, 1, 1, 7, -3]` (`positive_boundary = 5`)

2. Mark Presence:
- `arr[0]=2`: `arr[1]` becomes `-4` -> `[2, -4, 1, 1, 7, -3]`
- `arr[1]=-4`: abs=4, `arr[3]` becomes `-1` -> `[2, -4, 1, -1, 7, -3]`
- `arr[2]=1`: `arr[0]` becomes `-2` -> `[-2, -4, 1, -1, 7, -3]`
- `arr[3]=-1`: abs=1, `arr[0]` already negative.
- `arr[4]=7`: out of bound, ignore.

3. Find Missing:** First positive in `[-2, -4, 1, -1, 7]` is `1` at index 2. Missing = `2 + 1 = 3`.

Output: `3`
```
```py
def find_smallest_missing_positive(arr):
    n = len(arr)

    positive_boundary = 0
    for i in range(n):
        if arr[i] > 0:
            arr[i], arr[positive_boundary] = arr[positive_boundary], arr[i]
            positive_boundary += 1

    
    for i in range(positive_boundary):
        num = abs(arr[i])
        
        if 1 <= num <= positive_boundary and arr[num - 1] > 0:
            arr[num - 1] *= -1

    
    for i in range(positive_boundary):
        if arr[i] > 0:
            return i + 1

   
    return positive_boundary + 1

```

## Sub-Array

### Sub array with given sum

```
Input: arr[] = [15, 2, 4, 8, 9, 5, 10, 23], target = 23
Output: [2, 5]
Explanation: Sum of subarray arr[2…5] is 2 + 4 + 8 + 9 = 23.


Input: arr[] = [1, 10, 4, 0, 3, 5], target = 7
Output: [3, 5]
Explanation: Sum of subarray arr[3…5] is 4 + 0 + 3 = 7.


Input: arr[] = [1, 4], target = 0
Output: [-1]
Explanation: There is no subarray with 0 sum.
```

<b> Approach 1: Use Nested Loop </b>

- Time Complexity: 0(n^2)
- Space Complexity: 0(1)

```
arr = [15, 2, 4, 8, 9, 5, 10, 23]
target = 23
result = []
n = len(arr)

for i in range(n):
    current_sum = arr[i]
    for j in range(i+1, n):
        current_sum += arr[j]
        
        if current_sum == target:
            result.append((i,j))
            break

print(result)
```

<b> Approach 2: Sliding Window Technique </b>

- Time Complexity: 0(n)
- Space Complexity: 0(1)
```
Think of having a magnifying glass (our window) moving across your numbers.

[ 15 ]  2   4   8   9   5  10  23
<--> (window starts here, sum is 15)


1. **Make the window bigger:** Slide the right side of the glass to include more numbers, and add them to our total.

[ 15 ] [ 2 ]  4   8   9   5  10  23
<-----> (window now includes 15 and 2, sum is 17)


2. **Make the window smaller (if the total is too big):** Slide the left side of the glass to remove numbers from the beginning, and subtract them from our total.

15  [ 2 ] [ 4 ]  8   9   5  10  23
<-----> (window now includes 2 and 4, sum is 6 - if target was smaller)


3. **Check the total:** At each step, see if the total inside our magnifying glass equals the sum we're looking for.

... [ 4 ] [ 8 ] [ 9 ] ...
<-----> (if sum of 4+8+9 equals our target)


We keep adjusting the window's size and position until we find a set of connected numbers that add up to our target, or we run out of numbers.
```

```
def subarray_with_given_sum(arr, target):
    n = len(arr)
    left = 0 
    right = 0 
    current_sum = 0
    
    while right < n:
        current_sum += arr[right]
        
        if current_sum > target:
            current_sum -= arr[left]
            left += 1
        
        if current_sum == target:
            return [left, right]
        
        right += 1
            
    return [-1]

arr = [15, 2, 4, 8, 9, 5, 10, 23]
print(subarray_with_given_sum(arr, 23))
```

### Maximum sum of sub array

```
Input: arr[] = {2, 3, -8, 7, -1, 2, 3}
Output: 11
Explanation: The subarray {7, -1, 2, 3} has the largest sum 11.


Input: arr[] = {-2, -4}
Output: –2
Explanation: The subarray {-2} has the largest sum -2.


Input: arr[] = {5, 4, 1, 7, 8}
Output: 25
Explanation: The subarray {5, 4, 1, 7, 8} has the largest sum 25.
```

<b> Approach 1: Use Nested Loop</b>

- Time Complexity: 0(n^2)
- Space Complexity: O(1)

```py
arr = [5, 4, 1, 7, 8]
n = len(arr)
max_sum = arr[0]
for i in range(n):
    current_sum = arr[i]
    
    for j in range(i+1, n):
        current_sum += arr[j]
        max_sum = max(current_sum, max_sum)

print(max_sum)
```

<b> Kadane’s Algorithm </b>

- Time Complexity: O(n)
- Space Complexity: 0(1)

```
arr = [ 2,  3, -8,  7, -1,  2,  3 ]
^
max_sum = 2
max_ending = 2


**Iteration 1 (item = 3):**

arr = [ 2,  3, -8,  7, -1,  2,  3 ]
^
item = 3
max_ending = max(2 + 3, 3) = max(5, 3) = 5
max_sum = max(5, 2) = 5


**Iteration 2 (item = -8):**

arr = [ 2,  3, -8,  7, -1,  2,  3 ]
^
item = -8
max_ending = max(5 + (-8), -8) = max(-3, -8) = -3
max_sum = max(-3, 5) = 5


**Iteration 3 (item = 7):**

arr = [ 2,  3, -8,  7, -1,  2,  3 ]
^
item = 7
max_ending = max(-3 + 7, 7) = max(4, 7) = 7
max_sum = max(7, 5) = 7


**Iteration 4 (item = -1):**

arr = [ 2,  3, -8,  7, -1,  2,  3 ]
^
item = -1
max_ending = max(7 + (-1), -1) = max(6, -1) = 6
max_sum = max(6, 7) = 7


**Iteration 5 (item = 2):**

arr = [ 2,  3, -8,  7, -1,  2,  3 ]
^
item = 2
max_ending = max(6 + 2, 2) = max(8, 2) = 8
max_sum = max(8, 7) = 8


**Iteration 6 (item = 3):**

arr = [ 2,  3, -8,  7, -1,  2,  3 ]
^
item = 3
max_ending = max(8 + 3, 3) = max(11, 3) = 11
max_sum = max(11, 8) = 11
```

```py
def maximum_sum(arr):
    n = len(arr)
    
    max_sum = arr[0]
    max_ending = arr[0]
    
    for item in arr[1:]:
        max_ending = max(max_ending + item, item)
        max_sum = max(max_ending, max_sum)
        
    return max_sum
    
arr = [2, 3, -8, 7, -1, 2, 3]
print(maximum_sum(arr))
```



