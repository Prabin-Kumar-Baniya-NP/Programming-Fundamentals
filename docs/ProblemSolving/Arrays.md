# Arrays

## Reverse Array

```js
function reverseArray(arr, start, end) {
  while (start <= end) {
    let temp = arr[start];
    arr[start] = arr[end];
    arr[end] = temp;
    start++;
    end--;
  }
}
```

## Array Rotation

### 1. Function to rotate the array by d elements in anti-clockwise direction

```
Input:
1 2 3 4 5
2
Output:
3 4 5 1 2

Time Complexity : O(n)
Auxiliary Space: O(1)
```
```js
function rotateArray(arr, r, n) {
  if (d == 0) return;
  r = r % n; // if rotating factor r is greater than n
  // Reverse the first r elements
  reverseArray(arr, 0, r - 1);
  // Reverse the elements from d to n-1
  reverseArray(arr, r, n - 1);
  // Reverse the entire array
  reverseArray(arr, 0, n - 1);
}

let arr = [1, 2, 3, 4, 5];
rotateArray(arr, 2, arr.length);
console.log(arr);
```

### 2. Function to rotate the array by d elements in anti-clockwise / counter-clockwise direction

```
Input:
1 2 3 4 5 6
2

Output:
5 6 1 2 3 4

Time Complexity : O(n)
Auxiliary Space: O(1)
```
```js

```