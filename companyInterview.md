Interview Question:
```javascript
const items = [
    { type: "iPhone", color: "red", secondary: "gold" },
    { type: "desktop", color: "green", secondary: "gold" },
    { type: "iPhone", color: "blue", secondary: "gold" }
];

const excludes = [
    { key: "color", value: "red" },
    { key: "type", value: "desktop" }
];

function convert(excludes) {
    const obj = {};
    excludes.forEach(e => {
        if (obj[e.key]) {
            obj[e.key][e.value] = true;
        } else {
            obj[e.key] = { [e.value]: true };
        }
    });
    return obj;
}

function filterItems(items, excludes) {
    const newExclude = convert(excludes);
    const res = [];
    items.forEach(e => {
        let addKey = false;
        for (const key in e) {
            if (newExclude[key] && newExclude[key][e[key]] && !addKey) {
                addKey = true;
            }
        }
        if (!addKey) {
            res.push(e);
        }
    });
    return res;
}

filterItems(items, excludes);
```
dependencies
```javascript
const projects = ['a', 'b', 'c', 'd', 'e', 'f'];
const dependencies = [['a', 'd'], ['f', 'b'], ['b', 'd'], ['f', 'a'], ['d', 'c']];

function removeNode(nodes, key) {
    if (!nodes[key]) {
        return;
    }
    nodes[key] = null;
    Object.keys(nodes).forEach(e => {
        if (nodes[e] && nodes[e][key]) {
            const { [key]: value, ...newObj } = nodes[e];
            nodes[e] = newObj;
        }
    });
}

function findNodeWithNoDep(nodes) {
    const arr = Object.keys(nodes);
    for (let i = 0; i < arr.length; i++) {
        const key = arr[i];
        if (nodes[key] && !Object.keys(nodes[key]).length) {
            return key;
        }
    }
    return null;
}

function buildOrder(projects, dependencies) {
    const nodes = {};
    projects.forEach(node => {
        nodes[node] = {};
    });
    dependencies.forEach(dep => {
        nodes[dep[1]][dep[0]] = true;
    });
    const res = [];
    let currNode = findNodeWithNoDep(nodes);
    while (currNode) {
        res.push(currNode);
        removeNode(nodes, currNode);
        currNode = findNodeWithNoDep(nodes);
    }
    return res;
}

buildOrder(projects, dependencies);
```
Isomorphic problem
```javascript
//pop -> bob, boot -> boat

function iso(str1, str2) {
    if (str1.length !== str2.length) {
        return false;
    }
    const obj1 = {}, obj2 = {};
    str1.split("").forEach((e, i) => {
        obj1[e] = str2[i];
        obj2[str2[i]] = e;
    });
    for (let i = 0; i < str1.length; i++) {
        if (str2[i] !== obj1[str1[i]] || str1[i] !== obj2[str2[i]]) {
            return false;
        }
    }
    return true;
}

iso("pop", "boc");
```
Filter Color
```javascript
const colors = ["aliceblue","antiquewhite","aqua","aquamarine","azure","beige","bisque","black","blanchedalmond","blue","blueviolet","brown","burlywood","cadetblue","chartreuse","chocolate","coral","cornflowerblue","cornsilk","crimson","cyan","darkblue","darkcyan","darkgoldenrod","darkgray","darkgreen","darkgrey","darkkhaki","darkmagenta","darkolivegreen","darkorange","darkorchid","darkred","darksalmon","darkseagreen","darkslateblue","darkslategray","darkslategrey","darkturquoise","darkviolet","deeppink","deepskyblue","dimgray","dimgrey","dodgerblue","firebrick","floralwhite","forestgreen","fuchsia","gainsboro","ghostwhite","gold","goldenrod","gray","green","greenyellow","grey","honeydew","hotpink","indianred","indigo","ivory","khaki","lavender","lavenderblush","lawngreen","lemonchiffon","lightblue","lightcoral","lightcyan","lightgoldenrodyellow","lightgray","lightgreen","lightgrey","lightpink","lightsalmon","lightseagreen","lightskyblue","lightslategray","lightslategrey","lightsteelblue","lightyellow","lime","limegreen","linen","magenta","maroon","mediumaquamarine","mediumblue","mediumorchid","mediumpurple","mediumseagreen","mediumslateblue","mediumspringgreen","mediumturquoise","mediumvioletred","midnightblue","mintcream","mistyrose","moccasin","navajowhite","navy","oldlace","olive","olivedrab","orange","orangered","orchid","palegoldenrod","palegreen","paleturquoise","palevioletred","papayawhip","peachpuff","peru","pink","plum","powderblue","purple","red","rosybrown","royalblue","saddlebrown","salmon","sandybrown","seagreen","seashell","sienna","silver","skyblue","slateblue","slategray","slategrey","snow","springgreen","steelblue","tan","teal","thistle","tomato","turquoise","violet","wheat","white","whitesmoke","yellow","yellowgreen"];

function isValid(word, str, index = 0) {
    if (index === str.length) {
        return true;
    }
    const i = word.indexOf(str[index]);
    return i > -1 ? isValid(word.slice(i + 1), str, index + 1) : false
}

function findColor(str) {
    return colors.filter(e => isValid(e, str));
}

console.log(findColor('uqi')); // [ 'darkturquoise', 'mediumaquamarine', 'mediumturquoise', 'paleturquoise', 'turquoise' ]
console.log(findColor('zre')); // [ 'azure' ]
console.log(findColor('gold')); // [ 'darkgoldenrod', 'gold', 'goldenrod', 'lightgoldenrodyellow', 'palegoldenrod' ]
```
Given a sorted dictionary of an alien language, find order of characters
```javascript
function deleteNode(node, key) {
    if (!nodes[key]) {
        return;
    }
    nodes[key] = null;
    Object.keys(nodes).forEach(e => {
        if (nodes[e] && nodes[e][key]) {
            const { [key]: value, ...newObj } = nodes[e];
            nodes[e] = newObj;
        }
    });
}

function findNode(node) {
    const arr = Object.keys(nodes);
    for (let i = 0; i < arr.length; i++) {
        const key = arr[i];
        if (nodes[key] && !Object.keys(nodes[key]).length) {
            return key;
        }
    }
    return null;
}

function alienOrder(dict) {
    const res = [];
    if (dict.length === 0) {
        return res;
    }
    const nodes = {};
    dict.forEach((curr, i) => {
        curr.split("").forEach(e => {
            if (!nodes[e]) {
                nodes[e] = {};
            }
        });
        if (i !== 0) {
            const prev = dict[i - 1];
            let j = 0;
            while (j < prev.length && j < curr.length && prev[j] === curr[j]) {
                j++;
            }
            if (j < curr.length && j < prev.length && !nodes[curr[j]][prev[j]]) {
                nodes[curr[j]][prev[j]] = true;
            }
        }
    });
    let curr = findNode(nodes);
    while (curr) {
        res.push(curr);
        deleteNode(nodes, curr);
        curr = findNode(nodes);
    }
    return res;
}

const words = ["baa", "abcd", "abca", "cab", "cad"];

alienOrder(words); // [ 'b', 'd', 'a', 'c' ]
```
