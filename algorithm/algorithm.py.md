3sum:
```python
def sum3(nums):
    result = []
    for i in range(len(nums) - 2):
        j = i + 1; k = len(nums) - 1
        while j < k:
            sumResult = nums[i] + nums[j] + nums[k]
            if sumResult == 0:
                result.append("{0},{1},{2}".format(nums[i], nums[j], nums[k]))
                j += 1
                k -= 1
                while j < k and nums[j] == nums[j - 1]:
                    j += 1
                while j < k and nums[k] == nums[k + 1]:
                    k -= 1
            elif sumResult < 0:
                j += 1
            else:
                k -= 1
    return result

sum3([-4, -2, 0, 0, 2, 2, 4])
```
4sum:
```python
def fourSum(nums, target):
    result = []
    for i in range(len(nums) - 3):
        if i != 0 and nums[i] == nums[i - 1]:
            continue
        for j in range(i + 1, len(nums) - 2):
            if j != i + 1 and nums[j] == nums[j - 1]:
                continue
            k = j + 1; l = len(nums) - 1
            while k < l:
                resultSum = nums[i] + nums[j] + nums[k] + nums[l]
                if resultSum == target:
                    result.append("{0},{1},{2},{3}".format(nums[i], nums[j], nums[k], nums[l]))
                    k += 1
                    l -= 1
                    while k < l and nums[k] == nums[k - 1]:
                        k += 1
                    while k < l and nums[l] == nums[l + 1]:
                        l -= 1
                elif resultSum < target:
                    k += 1
                else:
                    l -= 1
    return result

fourSum([-2, -2, -1, 0, 1, 2, 4], 0)
```
Convert Number to Roman:
```python
import math

def convertToRoman(num):
    roman = {
        "M": 1000,
        "CM": 900,
        "D": 500,
        "CD": 400,
        "C": 100,
        "XC": 90,
        "L": 50,
        "XL": 40,
        "X": 10,
        "IX": 9,
        "V": 5,
        "IV": 4,
        "I": 1
    }
    result = ""
    for key in roman:
        numberOf = math.floor(num / roman[key])
        num -= numberOf * roman[key]
        result += key * numberOf
    return result

convertToRoman(435)
```
Convert Roman to Num:
```python
def convertToNumber(string):
    roman = {
        "M": 1000,
        "CM": 900,
        "D": 500,
        "CD": 400,
        "C": 100,
        "XC": 90,
        "L": 50,
        "XL": 40,
        "X": 10,
        "IX": 9,
        "V": 5,
        "IV": 4,
        "I": 1
    }
    result = roman[string[0]]
    for i in range(1, len(string)):
        current = roman[string[i]]
        prev = roman[string[i - 1]]
        if prev < current:
            result += current - prev - prev
        else:
            result += current
    return result

convertToNumber('CDXXXV')
```
Phone Letter Combination:
```python
def letterCombinations(string):
    result = []
    if not string:
        return result
    obj = {
        "1": ["1"],
        "0": ["0"],
        "2": ["a", "b", "c"],
        "3": ["d", "e", "f"],
        "4": ["g", "h", "i"],
        "5": ["j", "k", "l"],
        "6": ["m", "n", "o"],
        "7": ["p", "q", "r", "s"],
        "8": ["t", "u", "v"],
        "9": ["w", "x", "y", "z"]
    }
    def recurse(current, index):
        if len(current) == len(string):
            result.append(current)
            return
        for i in range(len(obj[string[index]])):
            word = obj[string[index]][i]
            recurse(current + word, index + 1)
    recurse("", 0)
    return result

letterCombinations("234")
```
Word Break:
```python
def wordBreak(s, dictionary):
    arr = [False] * (len(s) + 1)
    arr[0] = True
    for i in range(len(s)):
        if arr[i]:
            for j in range(i + 1, len(s) + 1):
                word = s[i:j]
                if word in dictionary:
                    arr[j] = True
    return arr[len(s)]

wordBreak("leetcode", ["leet", "code"])
```
Word Break II:
```python
def dfs(arr, result, s, index):
    if index == 0:
        result.append(s.strip())
        return
    for i in range(len(arr[index])):
        word = arr[index][i]
        dfs(arr, result, word + " " + s, index - len(word))

def wordBreak(s, dictionary):
    arr = [[]] * (len(s) + 1)
    arr[0] = [True]
    for i in range(len(s)):
        if arr[i]:
            for j in range(i + 1, len(s) + 1):
                word = s[i:j]
                if word in dictionary:
                    if arr[j]:
                        arr[j].append(word)
                    else:
                        arr[j] = [word]
    result = []
    if not arr[len(s)]:
        return result
    dfs(arr, result, "", len(s))
    return result

wordBreak("catsanddog", ["cat", "cats", "and", "sand", "dog"])
```
