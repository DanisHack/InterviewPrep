Simple search algorithm:
Time Complexity: O(log(n))
```javascript
function binarySearch(arr, target) {
    let start = 0;
    let end = arr.length - 1;
    while (start <= end) {
        const middle = Math.floor((start + end) / 2);
        if (arr[middle] === target) {
            return middle;
        } else if (arr[middle] < target) {
            start = middle + 1;
        } else {
            end = middle - 1;
        }
    }
    return -1;
}

binarySearch([1, 2, 3, 4, 5], 2);
```
Merge Sort:
Time Complexity: O(nlog(n))
Space Complexity: O(n)
```javascript
const a = [34, 203, 3, 746, 200, 984, 198, 764, 9];

function merge(a, b) {
    let aLength = a.length - 1, bLength = b.length - 1, mergeLength = a.length + b.length - 1;
    while (aLength >= 0 && bLength >= 0) {
        if (a[aLength] > b[bLength]) {
            a[mergeLength] = a[aLength];
            aLength--;
        } else {
            a[mergeLength] = b[bLength];
            bLength--;
        }
        mergeLength--;
    }
    while (bLength >= 0) {
        a[mergeLength] = b[bLength];
        mergeLength--;
        bLength--;
    }
    return a;
}

function mergeSort(arr) {
    if (arr.length < 2) {
        return arr;
    }
    const middle = Math.floor(arr.length / 2);
    const left = arr.slice(0, middle);
    const right = arr.slice(middle);
    return merge(mergeSort(left), mergeSort(right));
}

mergeSort(a);
```
Quick Sort:
Time Complexity: O(nlog(n)), worst is O(n^2)
Space Complexity: O(log(n))
```javascript
const a = [34, 203, 3, 746, 200, 984, 198, 764, 9];

function partition(arr, left, right) {
    const pivot = Math.floor((left + right) / 2);
    while (left <= right) {
        while (arr[left] < arr[pivot]) {
            left++;
        }
        while (arr[right] > arr[pivot]) {
            right--;
        }
        if (left <= right) {
            const temp = arr[left];
            arr[left] = arr[right];
            arr[right] = temp;
            left++;
            right--;
        }
    }
    return left;
}

function quickSort(arr, left = 0, right = arr.length - 1) {
    if (arr.length < 2) {
        return;
    }
    const index = partition(arr, left, right);
    if (left < index - 1) {
        quickSort(arr, left, index - 1);
    }
    if (index < right) {
        quickSort(arr, index, right);
    }
    return arr;
}

quickSort(a);
```
given an array of strings separated by empty string, find the location of the string
```javascript
function searchString(arr, value) {
    let start = 0, end = arr.length - 1;
    while (start <= end) {
        const middle = Math.floor((start + end) / 2);
        if (arr[middle] === value) {
            return middle;
        } else if (arr[middle] === "") {
            let left = middle, right = middle;
            while ((left > 0 || right < arr.length - 1) && (arr[left] === "" || arr[right] === "")) {
                if (left > 0 && arr[left] === "") {
                    left--;
                }
                if (right < arr.length - 1 && arr[right] === "") {
                    right++;
                }
            }
            if (arr[left] && arr[left].charAt() < value.charAt()) {
                start = right - 1;
            } else if (arr[right] && arr[right].charAt() > value.charAt()) {
                end = left + 1;
            } else {
                start = end + 1;
            }
        } else {
            if (arr[middle].charAt() < value.charAt()) {
                start = middle + 1;
            } else {
                end = middle - 1
            }
        }
    }
    return -1;
}

searchString(['at', '', '', '', 'ball', '', '', 'car', '', '', 'dad', '', ''], "at"); // 0
```
