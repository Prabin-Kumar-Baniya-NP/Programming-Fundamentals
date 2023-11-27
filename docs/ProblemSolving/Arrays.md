# Arrays

## Largest Elements

### Find the largest element in an array

Given an array with all distinct elements, find the largest element.

```
Expected time complexity is O(n) and extra space is O(1).
Input: arr[] = {10, 4, 3, 50, 23, 90}
Output: 90
```

```js
const arr = [10, 4, 3, 50, 23, 90];

let largest = -1;

arr.forEach((item) => {
  if (item > largest) {
    largest = item;
  }
});

console.log(largest);
```

### Find the largest three distinct elements.

Given an array with all distinct elements, find the largest three elements.

```
Expected time complexity is O(n) and extra space is O(1).
Input: arr[] = {10, 4, 3, 50, 23, 90}
Output: 90, 50, 23
```

```js
const arr = [10, 4, 3, 50, 23, 90];
var length = arr.length;

var first = (second = third = -1);

arr.forEach((num) => {
  if (num > first) {
    third = second;
    second = first;
    first = num;
  } else if (num > second) {
    third = second;
    second = num;
  } else {
    third = num;
  }
});

console.log(first, second, third);
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

```js
let arr = [10, 4, 3, 50, 23, 90];

let k = 3;

arr.sort((a, b) => a - b); // a-b for ascending, b-a for descending

console.log(arr[k - 1]);
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

```js
let arr = [3, 1, 2, 2, 1, 2, 3, 3];

const n = arr.length;

const freq = [];

const i = n / 4;

for (let k = 0; k < n; k++) {
  freq[k] = 0;
}

arr.forEach((item, index) => {
  freq[item] += 1;
});

console.log(arr[freq.indexOf(i + 1)]);
```
