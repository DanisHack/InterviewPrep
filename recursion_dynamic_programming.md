Reverse a Integer without converting to string:
```javascript
function reverse(n) {
	let result = 0, num = n;
	while (num > 0) {
	    result = result * 10 + num % 10;
	    num = Math.floor(num / 10);
	}
	return result;
}

reverse(5432); // 2345
```
Swapping numbers without using a third variable:

```javascript
let a = 157;
let b = 230;

function swap() {
    a = a - b;
    b = b + a;
    a = b - a;
}

swap();
console.log(a, b); // 230, 157
```
Find the maximum without using if/else or comparison operator:
```javascript
function findMax(a, b){
    const diff = a - b;
    const k = (diff >> 31) * -1;
    return a - k * diff;
}

findMax(3, 100); // 100
```
