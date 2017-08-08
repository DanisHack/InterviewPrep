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
