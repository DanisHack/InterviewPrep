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
