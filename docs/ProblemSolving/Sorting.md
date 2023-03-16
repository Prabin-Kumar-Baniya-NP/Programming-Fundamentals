# Sorting Algorithms

## Selection Sort

- Time Complexity : O(n^2)
- Auxiliary Space : O(1)
- Select the minimum element in the unsorted array and swap it with the element at the begining.
- Example for {5,4,3,2,1}
    - Step 1: {5,4,3,2,1} => {1,5,4,3,2}
    - Step 2: {5,4,3,2} => {1,2,5,4,3}
    - Step 3: {5,4,3} => {1,2,3,5,4}
    - Step 4: {5,4} => {1,2,3,4,5}
```js
function selectionSort(arr) {
  for (let i = 0; i < arr.length; i++) {
    let minimum_index = i;
    for (let j = i + 1; j < arr.length; j++) {
      if (arr[j] < arr[i]) {
        minimum_index = j;
      }
    }
    // Swap arr[minimum_index] and arr[i]
    let temp = arr[minimum_index];
    arr[minimum_index] = arr[i];
    arr[i] = temp;
  }
}

let arr = [5, 4, 3, 2, 1];
selectionSort(arr);
console.log(arr);
```

## Bubble Sort

- Time Complexity: O(n^2)
- In bubble sort, we repeatedly swap two adjacent elements if they are in wrong order
- Example for {5,4,3,2,1}
    - Step 1: {5,4,3,2,1} => {4,3,2,1,5}
    - Step 2: {4,3,2,1} => {3,2,1,4,5}
    - Step 3: {3,2,1} => {2,1,3,4,5}
    - Step 4: {2,1} => {1,2,3,4,5}

```js
function bubbleSort(arr) {
  for (let i = 0; i < arr.length; i++) {
    for (let j = 0; j < arr.length - i - 1; j++) {
      if (arr[j] > arr[j + 1]) {
        let temp = arr[j];
        arr[j] = arr[j + 1];
        arr[j + 1] = temp;
      }
    }
  }
}

let arr = [5, 4, 3, 2, 1];
bubbleSort(arr);
console.log(arr);
```

## Insertion Sort

- Divide the array into sorted and unsorted part and move first element of unsorted array into right position in sorted array.
- Example for {5,4,3,2,1}
    - Step 1: {5}, {4,3,2,1} => {4,5}, {3,2,1}
    - Step 2: {4,5}, {3,2,1} => {3,4,5}, {2,1}
    - Step 3: {3,4,5}, {2,1} => {2,3,4,5}, {1}
    - Step 4: {2,3,4,5}, {1} => {1,2,3,4,5}, {}

```js
function insertionSort(arr) {
  for(let i=1; i<arr.length; i++){
    let temp = arr[i];
    let j = i-1; // Sorted Part 0 to j
    while(j>=0 && arr[j] > temp){
        arr[j+1] = arr[j];
        j--;
    }
    arr[j+1] = temp;
  }
}

let arr = [5, 4, 3, 2, 1];
insertionSort(arr);
console.log(arr);
```
