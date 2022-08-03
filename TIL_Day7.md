# 수업 내용 복습
## python 기초 문법 실습(Leetcode_string)

1. 125. Valid Palindrome
>Given a string s, return true if it is a palindrome, or false otherwise.

```python
class Solution:
    def isPalindrome(self, s: str) -> bool:
        char = ''.join(ch for ch in s if ch.isalnum())
        char2 = char.lower()
        reverse_sentence = ''
        for rever in char2:
            reverse_sentence = rever + reverse_sentence
            
        return char2 == reverse_sentence
 ```

 2. 2108. Find First Palindromic String in the Array
> Given an array of strings words, return the first palindromic string in the array. If there is no such string, return an empty string "". A string is palindromic if it reads the same forward and backward.

```python
class Solution:
    def checkPalindrome(self, s: str) -> bool:
        s = ''.join(filter(str.isalnum, s))
        s = s.lower()
        s_reverse = s[::-1]
        return s == s_reverse

    
    def firstPalindrome(self, words: List[str]) -> str:
        for s in words:
            if self.checkPalindrome(s):
                return s
        return ""
 ```

 3. 344. Reverse String
> Write a function that reverses a string. The input string is given as an array of characters s. You must do this by modifying the input array in-place with O(1) extra memory.       

```python
class Solution:
    def reverseString(self, s: List[str]) -> None:
        """
        Do not return anything, modify s in-place instead.
        """

        i, j = 0, len(s)-1
        while i < j:
            s[i], s[j] = s[j], s[i]
            # 1번과 달리, s[i]와 s[j]를 둘다 바꾸는 이유에 대해 잊지말기!
            i, j = i+1, j-1
        return s
```

4. 819. Most Common Word
> Given a string paragraph and a string array of the banned words banned, return the most frequent word that is not banned. It is guaranteed there is at least one word that is not banned, and that the answer is unique.

```python

class Solution:
    def mostCommonWord(self, paragraph: str, banned: List[str]) -> str:
        paragraph = paragraph.replace(',', ' ')
        paragraph = paragraph.replace('  ', ' ')
        words = paragraph.lower().split(' ')
        
        wordList = []
        for s in words:
            wordList.append(''.join(filter(str.isalnum, s)))
            
        for ban in banned:
            while ban in wordList:
                wordList.pop(wordList.index(ban))
        
        return max(wordList,key=wordList.count)
```

5. 2032. Two Out of Three
> Given three integer arrays nums1, nums2, and nums3, return a distinct array containing all the values that are present in at least two out of the three arrays. You may return the values in any order.

``` python
class Solution:
    def twoOutOfThree(self, nums1: List[int], nums2: List[int], nums3: List[int]) -> List[int]:
        all = list(set(nums1)) +  list(set(nums2)) +  list(set(nums3))
        dict = Counter(all).items()
        
        answer = []
        
        for key, value in dict:
            if value >= 2 :
                answer.append(key)
                
        return answer
```

