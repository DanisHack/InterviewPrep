Input is an array of integers, reorder its entries so that the even entries appear first:
```javascript
function evenOdd(nums) {
    let even = 0, odd = nums.length - 1;
    while (even < odd) {
        if (nums[even] % 2 === 0) {
            even++;
        } else {
            const temp = nums[even];
            nums[even] = nums[odd];
            nums[odd] = temp;
            odd--;
        }
    }
    return nums;
}

evenOdd([1, 2, 3, 5, 6, 8]); // time complexity: O(n)
```
Takes an array A nad index i into A, and rearranges the elements such that all elements less than A[i]("pivot") appear first, followed by elements equal to the pivot followed by elements greater than the pivot:
```javascript
function rearrange(a, i) {
    const pivot = a[i];
    let smaller = equal = 0, bigger = a.length;
    while (equal < bigger) {
        if (a[equal] < pivot) {
            const temp = a[smaller];
            a[smaller] = a[equal];
            a[equal] = a[bigger];
            equal++;
            smaller++;
        } else if (a[equal] === pivot) {
            equal++;
        } else {
            bigger--;
            const temp = a[equal];
            a[equal] = a[bigger];
            a[bigger] = temp;
        }
    }
    return a;
}

rearrange([0, 1, 2, 0, 2, 1, 1], 3); // [ 0, 0, 2, 2, 1, 1, 1 ]
```
