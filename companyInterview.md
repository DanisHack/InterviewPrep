Failed Facebook Interview Question:
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
Uber Interview
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
