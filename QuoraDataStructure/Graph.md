Find all possible words in a board of characters
```javascript
const dictionary = ['GEEKS', 'FOR', 'QUIZ', 'GO'];
const arr = [
    ['G', 'I', 'Z'],
    ['U', 'E', 'K'],
    ['Q', 'S', 'E']
];

function boggle(dict, arr) {
    const res = [], visited = {};
    function findWord(i, j, str = "") {
        const key = `${i}${j}`;
        if (i < 0 || j < 0 || visited[key]) {
            return;
        }
        visited[key] = true;
        const newStr = str + arr[i][j];
        if (dict.includes(newStr)) {
            res.push(newStr);
        }
        for (let row = i - 1; row <= i + 1 && row < arr.length; row++) {
            for (let col = j - 1; col <= j + 1 && col < arr[i].length; col++) {
                findWord(row, col, newStr);
            }
        }
        visited[key] = false;
    }
    arr.forEach((e, i) => {
        e.forEach((d, j) => {
            findWord(i, j);
        });
    });
    return res;
}

boggle(dictionary, arr);
```
