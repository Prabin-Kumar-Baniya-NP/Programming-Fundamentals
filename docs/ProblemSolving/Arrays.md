# Arrays

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
numbers: list = [1, 2, 3, 4, 5, 6, 7]
length: int = len(numbers)
result = []

for i in range(0,int(length/2)):
    result.append(numbers[length-i-1])
    result.append(numbers[i])

result.append(numbers[i+1])

print(result)
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