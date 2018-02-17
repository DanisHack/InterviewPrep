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
    delete nodes[key];
    for (const val in nodes) {
        if (nodes[val][key]) {
            delete nodes[val][key];
        }
    }
}

function findNodeWithNoDep(nodes) {
    for (const key in nodes) {
        if (!Object.keys(nodes[key]).length) {
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
        if (str2[i] !== obj1[str1[i]]) {
            return false;
        }
        if (str1[i] !== obj2[str2[i]]) {
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
