Convert Col column to Integer where is "A" starts at 1:
```javascript
function decodeStrCol(col) {
    return col.split("").reduce((result, c) => result * 26 + c.charCodeAt() - 64, 0)
}

decodeStrCol("ZZ"); // 702
```
Test palindrome of a sentence:
```javascript
// javascript version
function testPalindrome(str) {
    const arr = str.match(/[a-zA-Z]/ig);
    for (let i = 0; i < Math.floor((arr.length + 1) / 2); i++) {
        if (arr[i].toLowerCase() !== arr[arr.length - i - 1].toLowerCase()) {
            return false;
        }
    }
    return true;
}

testPalindrome("Able was I, ere I saw Elba"); // true
```
```go
// go version
import (
    "regexp"
    "strings"
)

func testPalindrome(str string) bool {
    arr := regexp.MustCompile(`[a-zA-Z]`).FindAllString(str, -1)
    arrLength := len(arr)
    for i := 0; i < int((arrLength + 1) / 2); i++ {
        if strings.ToLower(arr[i]) != strings.ToLower(arr[arrLength - i - 1]) {
            return false
        }
    }
    return true
}

func main() {
    testPalindrome("Able was I, ere I saw Elba")
}
```
Reverse a sentence:
```javascript
function reverseSentence(str) {
    return str.split(" ").reverse().join(" ");
}

reverseSentence("ram is costly");
```
```go
import "strings"

func reverseSentence(str string) string {
    arr := strings.Split(str, " ")
    for i := 0; i < int((len(arr) + 1) / 2); i++ {
        arr[i], arr[len(arr) - i - 1] = arr[len(arr) - i - 1], arr[i]
    }
    return strings.Join(arr, " ")
}

func main() {
    reverseSentence("ram is Costly")
}
```
