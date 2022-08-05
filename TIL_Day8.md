# 수업 내용 복습
## python을 활용한 알고리즘(Leetcode)

1. 1. Two Sum
>Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target. You may assume that each input would have exactly one solution, and you may not use the same element twice.

- 풀이 방식 1: 일반적인 for문

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        for i in range(len(nums)-1):
            for j in range(i+1, len(nums)):
                if nums[i] + nums[j] == target:
                    return [i, j]

# 쉽게 생각할 수 있는 방법이지만 시간이 너무 오래 걸림.
```
- 풀이 방식 2: list와 target의 차를 활용한 방법
```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        pairs = [target - num for num in nums]
        for i, pair in enumerate(pairs):
            if pair in nums and i != nums.index(pair):
                return i, nums.index(pair)
# 시간이 조금 줄긴했지만, 여전히 많이 필요
```
- 풀이 방식 3: Hash Table
```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        HashTable = dict()
        for i, value in enumerate(nums):
            # 빈 딕셔너리인 HashTable에 value인 2,7,11,15를 넣으면, 인덱스인 0,1,2,3이 들어감. {2: 0, 7: 1, 11: 2, 15: 3}와 같이 됨.
            HashTable[value] = i
            
        pairs = [target - num for num in nums]
        
        for i, pair in enumerate(pairs): # i는 0,1,2,3 pair는 7,2,-2,-6
            if pair in HashTable and i != HashTable[pair]:
                return i, HashTable[pair] # i는 pair의 인덱스, HashTable[pair]는 그 pair를 원래 리스트인 nums에서 찾아 인덱스를 출력한 것
```

- 풀이 방식 4: two pointer. 더 이해가 필요해 이건 나중에...
            