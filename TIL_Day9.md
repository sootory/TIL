# 수업 내용 복습
## python을 활용한 알고리즘(Leetcode)

1. 15. (Medium) 3Sum
```python
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        Answer = set()
        nums.sort()
        for i in range(len(nums)-2): #j와 k의 자리를 남겨둠
            j, k = i + 1, len(nums)-1
            while j < k:
                if nums[i] + nums[j] + nums[k] == 0:
                    Answer.add( tuple([nums[i], nums[j], nums[k]] ))
                    j, k = j +1, k-1
                elif nums[i] + nums[j] + nums[k] > 0:
                    k -= 1
                else:
                    j += 1
        return list(Answer)
# add, append, tuple, list의 관계 더 공부하자
```

2. 16. 3Sum Closest
```python
class Solution:
    def threeSumClosest(self, nums: List[int], target: int) -> int:
        diff = float('inf')
        nums.sort()
        for idx,a in enumerate(nums): # 세가지 숫자의 인덱스가 모두 달라야 한다는 조건이 없어서 len(nums)-2아니고 그냥?
            l,r = idx +1, len(nums)-1
            while l < r : # Two-pointer
                three_sum = a + nums[l] + nums[r]
                if abs(target - three_sum) < abs(diff):
                    diff = target - three_sum
                if three_sum > target:
                    r -= 1
                else:
                    l += 1
            if diff == 0 :
                break
        return target- diff
```

3. 11.Container water

```python
class Solution:
    def maxArea(self, height: List[int]) -> int:
        i, j = 0, len(height)-1 #index이면서 밑변의 꼭짓점
        MaxWater = -9999
        while i < j:
            Water = (j-i) * min(height[i], height[j]) # 두 막대의 높이 중에 낮은 것
            if Water > MaxWater:
                MaxWater = Water
            if height[i] > height[j]:
                j -= 1
            else:
                i += 1
        return MaxWater
```