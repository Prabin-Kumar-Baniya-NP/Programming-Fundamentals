# Arrays

## Search

### Binary Search

```
# Binary Search Implementation

def binarySearch(l, low, high, element):
    while(low <= high):
        mid = low + (high-low)//2
        if(l[mid] == element):
            return mid
        elif element < l[mid]:
            high = mid-1
        else:
            low = mid+1
    return -1

l = [1,2,3,4,5,6,7,8,9]
print(binarySearch(l, 0, len(l)-1, 50))
```

## Largest Elements

### Find the largest element in an array

Given an array with all distinct elements, find the largest element.

```
Expected time complexity is O(n) and extra space is O(1).
Input: arr[] = {10, 4, 3, 50, 23, 90}
Output: 90
```

```py
l = [1,6,3,4,5]
largest = 0

for num in l:
    if num > largest:
        largest = num

print(largest)
```

### Find the largest three distinct elements.

Given an array with all distinct elements, find the largest three elements.

```
Expected time complexity is O(n) and extra space is O(1).
Input: arr[] = {10, 4, 3, 50, 23, 90}
Output: 90, 50, 23
```

```py
l = [1,5,2,4,3,6]

first = second = third = -1

for num in l:
    if num > first:
        third = second
        second = first
        first = num
    elif num > second:
        third = second
        second = num
    elif num > third:
        third = num

print(first, second, third)
```

### Find the second largest element in an array.

Given an array with all distinct elements, find the second largest element in an array.

```
Expected time complexity is O(n) and extra space is O(1).
Input: arr[] = {10, 4, 3, 50, 23, 90}
Output: 50
```

```js
const arr = [10, 4, 3, 50, 70, 23, 90];

let first = (second = -1);

arr.forEach((item) => {
  if (item > first) {
    second = first;
    first = item;
  } else if (item > second) {
    second = item;
  }
});

console.log(second);
```

### Find K largest element in the array

```
Given an integer array nums and an integer k,
return the kth largest element in the array.

Examples :
Input: arr[] = {10, 4, 3, 50, 23, 90}, k=3
Output: 10
```

```py
numbers:list = [1, 23, 12, 9, 30, 2, 50]
k = 3
max_numbers = []
for i in range(len(numbers)):
    if i < k:
        max_numbers.append(numbers[i])
    else:
        min_number = min(max_numbers)
        if numbers[i] > min_number:
            index = max_numbers.index(min_number)
            max_numbers[index] = numbers[i]
print(max_numbers)
```

### Find the element that appears n/k times.

```
Given Array of size n and a number k, find all elements that appear more than n/k times

Input: arr[] = {3, 1, 2, 2, 1, 2, 3, 3}, k = 4
Output: {2, 3}
Explanation: Here n/k is 8/4 = 2, therefore 2 appears 3 times in the array that is greater than 2 and 3 appears 3 times in the array that is greater than 2

Input: arr[] = {9, 8, 7, 9, 2, 9, 7}, k = 3
Output: {9}
Explanation: Here n/k is 7/3 = 2, therefore 9 appears 3 times in the array that is greater than 2.
```

```py
numbers = [3, 1, 2, 2, 1, 2, 3, 3]

occurence = len(numbers) / 4 # 8/4 => 2 => Ans 2,3

frequency = {}

for num in numbers:
    if num not in frequency.keys():
        frequency[num] = 1
    else:
        frequency[num] = frequency[num] + 1

for key, value in frequency.items():
    if value > occurence:
        print(key)
```

### Move all zeros to the end of array

```
You are given an array of integers, your task is to move all the zeros in the array to the end of the array and move non-negative integers to the front by maintaining their order.

Example 1:
Input: 1 ,0 ,2 ,3 ,0 ,4 ,0 ,1
Output: 1 ,2 ,3 ,4 ,1 ,0 ,0 ,0
Explanation: All the zeros are moved to the end and non-negative integers are moved to front by maintaining order

Example 2:
Input: 1,2,0,1,0,4,0
Output: 1,2,1,4,0,0,0
Explanation: All the zeros are moved to the end and non-negative integers are moved to front by maintaining order
```

```py
numbers: list = [1 ,0 ,2 ,3 ,0 ,4 ,0 ,1]

result:list = []
number_of_zero_to_add:int = 0

for item in numbers:
    if item == 0:
        number_of_zero_to_add += 1
    elif item > 0:
        result.append(item)

result.extend([0 for i in range(number_of_zero_to_add)])

print(result)
```

### Rearrange the sorted array in Max-Min form using two pointer approach

```
Given a sorted array of positive integers, rearrange the array alternately i.e first element should be a maximum value, at second position minimum value, at third position second max, at fourth position second min, and so on.

Examples:

Input: arr[] = {1, 2, 3, 4, 5, 6, 7}
Output: arr[] = {7, 1, 6, 2, 5, 3, 4}

Input: arr[] = {1, 2, 3, 4, 5, 6}
Output: arr[] = {6, 1, 5, 2, 4, 3}
```

```py
l = [1, 2, 3, 4, 5, 6, 7]
left = 0
right = len(l) - 1
result = []

while(left <= right):
    if (left < right):
        result.extend([l[right], l[left]])
    elif left == right:
        result.append(l[left])
    left += 1
    right -= 1

print(result)

Space Complexity: O(N)
```

## Array Rearrangement

### Move all zero to the end of the array

```
Given an array of random numbers,
Push all the zero’s of a given array to the end of the array.
For example,
if the given arrays is {1, 9, 8, 4, 0, 0, 2, 7, 0, 6, 0},
it should be changed to {1, 9, 8, 4, 2, 7, 6, 0, 0, 0, 0}.
The order of all other elements should be same.
Expected time complexity is O(n) and extra space is O(1).
```

```py
# Fill the positive numbers by maintaining a variable and then fill the 0

numbers: list = [1, 9, 8, 4, 0, 0, 2, 7, 0, 6, 0]
num_len = len(numbers)

positive_num_count = 0

# Move all positive numbers to the front by ignoring the 0
for i in range(0, num_len):
    if numbers[i] > 0:
        numbers[positive_num_count] = numbers[i]
        positive_num_count += 1

# Fill the remaining zeros
while(positive_num_count != num_len):
    numbers[positive_num_count] = 0
    positive_num_count += 1
```

### Segregate Even and Odd Number

```
Given an array A[], write a function that segregates even and odd numbers. The functions should put all even numbers first, and then odd numbers.

Example:
Input  = {12, 34, 45, 9, 8, 90, 3}
Output = {12, 34, 8, 90, 45, 9, 3}

In the output, the order of numbers can be changed, i.e., in the above example, 34 can come before 12 and 3 can come before 9.
```

```py
l = [11, 34, 45, 9, 8, 90, 22, 3, 1, 2]

left = 0
right = len(l) - 1
is_even = lambda num: num%2 == 0

while(left<right):
    # Even, Even
    if is_even(l[left]) and is_even(l[right]):
        left += 1
    # Odd, Odd
    elif not is_even(l[left]) and not is_even(l[right]):
        # Find the next even number after left index and swap it with the left index number
        k = left + 1
        while (not is_even(l[k]) and k<right):
            k += 1
        l[k], l[left] = l[left], l[k]
        left += 1
    # Even, Odd
    elif is_even(l[left]) and not is_even(l[right]):
        left += 1
        right -= 1
    # Odd, Even
    elif not is_even(l[left]) and is_even(l[right]):
        l[left], l[right] = l[right], l[left]
        left += 1
        right -= 1
```

### Rearrange Postive and Negative Numbers

```
An array contains both positive and negative numbers in random order.
Rearrange the array elements so that positive and negative numbers are placed alternatively.
A number of positive and negative numbers need not be equal.
If there are more positive numbers they appear at the end of the array.
If there are more negative numbers, they too appear at the end of the array.

Example:

Input: [-1, 2, -3, 4, 5, 6, -7, 8, 9]
Output:[9, -7, 8, -3, 5, -1, 2, 4, 6]

Input: [-1, 3, -2, -4, 7, -5]
Output:[7, -2, 3, -5, -1, -4]
```

```py
numbers: list = [-1, 2, -3, 4, 5, 6, -7, 8, 9]
positive: list = []
negative: list = []

for item in numbers:
    if item >= 0:
        positive.append(item)
    else:
        negative.append(item)


positive_idx_iter: int = 0
negative_idx_iter: int = 0
toggle = True
result = []

while(positive_idx_iter < len(positive) and negative_idx_iter < len(negative)):
    if toggle:
        result.append(positive[positive_idx_iter])
        positive_idx_iter += 1
    else:
        result.append(negative[negative_idx_iter])
        negative_idx_iter += 1
    toggle = not toggle

while positive_idx_iter < len(positive):
    result.append(positive[positive_idx_iter])
    positive_idx_iter += 1

while negative_idx_iter < len(negative):
    result.append(negative[negative_idx_iter])
    negative_idx_iter += 1

print(result)

```

### Sort K sorted array

```
Sort a nearly sorted (or K sorted) array
Given an array of N elements, where each element is at most K away from its target position,
devise an algorithm that sorts in O(N log K) time.

Examples:

Input: arr[] = {6, 5, 3, 2, 8, 10, 9}, K = 3
Output: arr[] = {2, 3, 5, 6, 8, 9, 10}

Input: arr[] = {10, 9, 8, 7, 4, 70, 60, 50}, k = 4
Output: arr[] = {4, 7, 8, 9, 10, 50, 60, 70}
```

```py
def bubble_sort():
    pass

def swap_using_pointers(start, end):
    while (start <= end):
        numbers[start], numbers[end] = numbers[end], numbers[start]
        start += 1
        end -= 1
numbers: list = [6, 5, 3, 2, 8, 10, 9]
k = 3
start = 0
end = k
swap_using_pointers(start, end)
start = k + 1
end = len(numbers) - 1
bubble_sort(start, end)
print(numbers)
```

### Rearrange an array such that arr[i] = i

```
Given an array of elements of length N, ranging from 0 to N – 1.
All elements may not be present in the array.
If the element is not present then there will be -1 present in the array.
Rearrange the array such that A[i] = i and if i is not present, display -1 at that place.

Examples:

Input : arr = {-1, -1, 6, 1, 9, 3, 2, -1, 4, -1}
Output : [-1, 1, 2, 3, 4, -1, 6, -1, -1, 9]

Input : arr = {19, 7, 0, 3, 18, 15, 12, 6, 1, 8,
              11, 10, 9, 5, 13, 16, 2, 14, 17, 4}
Output : [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10,
         11, 12, 13, 14, 15, 16, 17, 18, 19]
```

```py
numbers: list = [-1, -1, 6, 1, 9, 3, 2, -1, 4, -1]
result: list = []
for i in range(0, len(numbers)):
    if i in numbers:
        result.append(i)
    else:
        result.append(-1)

print(result)
```

## Array Rotation

### Rotate array by d factor in left side

```
Given an array arr[] of size N, the task is to rotate the array by d position to the left.

Examples:

Input:  arr[] = {1, 2, 3, 4, 5, 6, 7}, d = 2
Output: 3, 4, 5, 6, 7, 1, 2
Explanation: If the array is rotated by 1 position to the left,
it becomes {2, 3, 4, 5, 6, 7, 1}.
When it is rotated further by 1 position,
it becomes: {3, 4, 5, 6, 7, 1, 2}

Input: arr[] = {1, 6, 7, 8}, d = 3
Output: 8, 1, 6, 7
```

```py
l = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
d = 4

def reverse(l, start, end):
    while(start <= end):
        l[start], l[end] = l[end], l[start]
        start += 1
        end -= 1
    return l

def leftRotate(l, d):
    # reverse l from 0 to d-1
    reverse(l, 0, d-1)
    # reverse l from d to n-1
    reverse(l, d, len(l)-1)
    # reverse entire l
    reverse(l, 0, len(l)-1)

leftRotate(l,d)
print(l)
```

### Find by how much factor an array is rotated

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

```py
l = [15, 18, 2, 3, 6, 12]

def getRotatedCount(l):
    for i in range(0, len(l)-1):
        if l[i] > l[i+1]:
            return i+1
    return 0
```

## Array Sorting

### Bubble Sort

- The largest element gets bubbled out at the end
- Best Case: O(N)
- Avg/Worst Case: O(N^2)

```py
def bubbleSort(num:list):
    swapped = False
    n = len(num)
    for i in range(n):
        for j in range(n-i-1):
            if num[j] > num[j+1]:
                num[j], num[j+1] = num[j+1], num[j]
                swapped = True
        if not swapped:
            break
    return num

num = [0,1,2,3,4,5]
bubbleSort(num)
print(num)
```

### Selection Sort

- Select the smallest element from the unsorted portion of the list and swap it with the item at the beginning of the unsorted portion.
- Best/Avg/Worst Case: O(N^2)

```py
def selectionSort(num:list):
    min_index = 0
    n = len(num)
    for i in range(n):
        min_index = i
        for j in range(i+1, n):
            if num[j] < num[min_index]:
                min_index = j
        
        num[min_index], num[i] = num[i], num[min_index]
```

### Insertion Sort

- Pick an item from the unsorted portion of the list and put it in the right place in the sorted array.

- Best Case: O(N), Avg/Worst Case: O(N^2)

```py
def insertionSort(arr):
    for i in range(1, len(arr)):
        key = arr[i]
        j = i - 1

        # Move elements of arr[0..i-1], that are
        # greater than key, to one position ahead
        # of their current position
        while j >= 0 and key < arr[j]:
            arr[j + 1] = arr[j]
            j -= 1
        arr[j + 1] = key
```