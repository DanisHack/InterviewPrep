Create own bind function
```javascript
const obj = {
    a: "Hello"
};

function Awesome(val) {
    return `${this.a} ${val}`
}

Function.prototype.customBind = function (context) {
    const func = this;
    let args = Array.prototype.slice.call(arguments, 1);
    return function () {
        args = args.concat(Array.prototype.slice.call(arguments));
        return func.apply(context, args);
    }
}

Awesome.customBind(obj, "World")() // "Hello World";
```
Create own Reduce Function
```javascript
const arr = [1, 2, 3, 4];

Array.prototype.customReduce = function (callback, initial) {
    let res = initial;
    for (let i = 0; i < this.length; i++) {
        res = callback(res, this[i]);
    }
    return res;
}

arr.customReduce((acc, curr) => {
    return acc + curr
}, 2);
```
