Implement Hash Table
```javascript
class Table {
    constructor() {
        this.keys = [];
        this.values = [];
    }

    set(key, value) {
        this.keys.push(key);
        this.values.push(value);
    }

    get(lookupKey) {
        for (let i = 0; i < this.keys.length; i++) {
            const key = this.keys[i];
            if (key === lookupKey) {
                return this.values[i];
            }
        }
        return null;
    }
}

class HashTable {
    constructor() {
        this.bucketCount = 100;
        this.buckets = [];
        for (let i = 0; i < this.bucketCount; i++) {
            this.buckets.push(new Table());
        }
    }

    static hashFunction = key => {
        let hash = 0;
        if (!key) {
            return hash;
        }
        for (let i = 0; i < key.length; i++) {
            hash = (hash << 5) - hash;
            hash += key.charCodeAt(i);
            hash &= hash;
        }
        return Math.abs(hash);
    };

    set(key, value) {
        const table = this.buckets[HashTable.hashFunction(key) % this.bucketCount];
        table.set(key, value);
    };

    get(key) {
        const table = this.buckets[HashTable.hashFunction(key) % this.bucketCount];
        return table.get(key);
    }
}

const obj = new HashTable();
obj.set("awesome", 1)
console.log(obj.get("awesome"));
```
