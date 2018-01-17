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
/**
Code

A --|

    |-- D --|

B --|       |-- E

    |       |

C --|-------|

Each node is a async job, e.g. setTimeout.
A, B, and C can run at the same time.
D, needs to wait for A and B to be done.
E needs to wait for C and D to be done.

Implement a method, let's call it runTasks that will take a list
of tasks as input and run all tasks according to dependencies.
[A, B, C, (D: A,B), (E: C,D)]
**/

// A, B, C
// A, B -> D
// C, D -> E

class Node {
    constructor(val, task = (callback) => callback(), dependency = null) {
        this.val = val;
        this.done = false;
        this.dependency = dependency;
        this.task = task;
    }

    runTask() {
        return new Promise((resolve, reject) => {
            this.task(() => {
                resolve(true);
            });
        })
    }
}

// const definition = (callback) => {
//     // do work here
//     callback()
// };

const a = new Node("A");
const d = new Node("D", { "A": true, "B": true })

const input = [a, b, c, d];

function finishAsync(task) {
    return new Promise((resolve, reject) => {

    })
}

// second solution
// changed to an async/await approach to make sure that everything before "await" is run before we get to after await
async function runTasks(lists) {
    // holds what task has been finished
    const trackFinished = {};
    // create a new array so to not mutate the original copy
    const queue = [...lists];

    let i = 0;
    while (queue.length) {
        // current task
        const current = queue[i];
        // check if there is any dependicies that needs to be run
        if (current.dependency) {
            // this is the flag, if it is true, that means all dependicies has run and finished
            let allFinished = true;
            for (const key in current.dependency) {
                if (!trackFinished[key]) {
                    // if a task is not finished we break
                    allFinished = false;
                    break;
                }
            }

            if (!allFinised) {
                i++;
                // if we get to the end, and not all the task has finished, we will recycle back to the beginning
                if (i >= queue.length) {
                    i = 0;
                }
                // since not all tasks are finished we go on to the next and come back to it later
                continue;
            } else {
                // if all dependicies is finished, we run the task
                const isDone = await current.runTask().then(done => done);
                // everything after await has to be finished in order to get here
                if (isDone) {
                    trackFinished[current.val] = true;
                    // then we take out the current task from the queue
                    // since we took out the current task from the current queue, no need to increment the index
                    queue.splice(i, 1);
                    if (i >= queue.length) {
                        i = 0;
                    }
                }
            }
        } else {
            const isDone = await current.runTask().then(done => done);
            if (isDone) {
                trackFinished[current.val] = true;
                queue.splice(i, 1);
                if (i >= queue.length) {
                    i = 0;
                }
            }
        }
    }
}
```
