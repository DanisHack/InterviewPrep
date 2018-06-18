Edge List - space complexity: O(E), time complexity: O(E)
Adjacency Matrix - space complexity: O(V^2), time complexity: O(1)
Adjacency List - space complexity: O(V + E), time complexity: O(d) where d is the degree of each vertex

Graph DFS and BFS time complexity is O(|V| + |E|), space complexity is O(|V|)

BFS for Adjacency List:
```javascript
const graph = [
    [1, 4],
    [0, 2, 4],
    [1, 3],
    [2, 4, 5],
    [0, 1, 3],
    [3]
];

function buildPath(parent, e) {
    let curr = e;
    const path = [curr];
    while (parent[curr] !== null) {
        curr = parent[curr];
        path.push(curr);
    }
    return path.reverse();
}

function graphBFS(graph, start, goal) {
    const visited = { [start]: true }, queue = [start], parent = { [start]: null };
    const res = [];
    while (queue.length) {
        const curr = queue.shift();
        if (curr === goal) {
            return buildPath(parent, goal);
        }
        graph[curr].forEach(e => {
            if (!visited[e]) {
                visited[e] = true;
                queue.push(e);
                parent[e] = curr;
            }
        });
    }
}

graphBFS(graph, 0, 5);
```
DFS for Adjacency List
```javascript
const graph = [
    [1, 4],
    [0, 2, 4],
    [1, 3],
    [2, 4, 5],
    [0, 1, 3],
    [3]
];

function graphDFS(graph, start, goal) {
    const visited = {}, path = [];
    (function recurse(curr) {
        visited[curr] = true;
        if (curr === goal) {
            path.push(curr);
            return true;
        }
        for (let i = 0; i < graph[curr].length; i++) {
            if (!visited[graph[curr][i]]) {
                if (recurse(graph[curr][i])) {
                    path.push(curr);
                    return true;
                }
            }
        }
        return false;
    })(start);
    return path.reverse();
}

graphDFS(graph, 2, 5);
```
BFS for Adjacency Matrix
```javascript
const graph = [
  [0, 1, 0, 0, 1, 0],
  [1, 0, 1, 0, 1, 0],
  [0, 1, 0, 1, 0, 0],
  [0, 0, 1, 0, 1, 1],
  [1, 1, 0, 1, 0, 0],
  [0, 0, 0, 1, 0, 0]
];

function buildPath(parents, goal) {
    let current = goal;
    const path = [current];
    while (parents[current] !== null) {
        current = parents[current];
        path.push(current);
    }
    return path.reverse();
}

function graphBFS(graph, start, goal) {
	const visited = { [start]: true },
		parent = { [start]: null },
		queue = [start];
    while (queue.length) {
        const curr = queue.shift();
        if (curr === goal) {
            return buildPath(parent, goal);
        }
        graph[curr].forEach((e, i) => {
            if (curr !== i && graph[curr][i] && !visited[i]) {
                visited[i] = true;
                parent[i] = curr;
                queue.push(i);
            }
        });
    }
}

graphBFS(graph, 2, 5);
```
DFS for Adjacency Matrix
```javascript
const graph = [
  [0, 1, 0, 0, 1, 0],
  [1, 0, 1, 0, 1, 0],
  [0, 1, 0, 1, 0, 0],
  [0, 0, 1, 0, 1, 1],
  [1, 1, 0, 1, 0, 0],
  [0, 0, 0, 1, 0, 0]
];

function graphDFS(graph, start, goal) {
    const visited = {}, path = [];
    (function recurse(curr) {
        visited[curr] = true;
        if (curr === goal) {
            path.push(curr);
            return true;
        }
        for (let i = 0; i < graph[curr].length; i++) {
            if (graph[curr][i] && !visited[i]) {
                if (recurse(i)) {
                    path.push(curr);
                    return true;
                }
            }
        }
        return false;
    })(start);
    return path.reverse();
}

graphDFS(graph, 2, 5);
```
