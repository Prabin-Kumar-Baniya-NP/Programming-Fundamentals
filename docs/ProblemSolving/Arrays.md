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
l = [1,5,2,4,3,6]

l = sorted(l)
k = 2
print(l[len(l) - k])
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
numbers = [1,2,0,0,3,4,5,6,0,9,0]

temp = []

for num in numbers:
    if num != 0:
        temp.append(num)

for i in range(len(numbers)):
    if i < len(temp):
        numbers[i] = temp[i]
    else:
        numbers[i] = 0

print(numbers)
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
numbers = [1,2,3,4,5,6,7]
sorted = []

i = 0
j = len(numbers) -1

while(i<=j):
    if i == j:
        sorted.append(numbers[i])
    elif numbers[i] > numbers[j]:
        sorted.append(numbers[i])
        sorted.append(numbers[j])
    else:
        sorted.append(numbers[j])
        sorted.append(numbers[i])
    i += 1
    j -= 1

print(sorted)
```
```
Time Complexity: O(n)
Space Complexity: O(n)
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

```js
let arr = [1, 9, 8, 4, 0, 0, 2, 7, 0, 6, 0];
let n = arr.length;

let count = 0; // count of non-zero elements
for(let i=0; i<n; i++){
    if (arr[i] != 0){
        arr[count++] = arr[i];
    }
}
while(count < n){
    arr[count] = 0;
    count++;
}

console.log(arr);
```