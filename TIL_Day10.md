# 수업 내용 복습
## python을 활용한 알고리즘(Leetcode)

1. 2160. Minimum Sum of Four Digit Number
```python
class Solution:
    def minimumSum(self, num: int) -> int:
        nums = [int(i) for i in str(num)]
        nums = list(nums)
        print(nums)
        
        nums.sort()
        
        Num1 = nums[0] * 10 + nums[2]
        Num2 = nums[1] * 10 + nums[3]
        
        return Num1 + Num2
```

2. 1689. Partitioning Into Minimum Number Of Deci-Binary Numbers

```python
class Solution:
    def minPartitions(self, n: str) -> int:
        # n의 요소들을 list화하고 int로 바꿈
        InputList = [ int(i) for i in list(n) ]
        # 빈 리스트 생성
        MinusList = []
        # 카운터 변수 생성
        nCount = 0
        # while문으로 InputList의 합이 0이 아닐 때까지 아래 식을 반복
        while sum(InputList) != 0:
            Minus = [] # 빈 리스트
            for i, digit in enumerate(InputList): # InputList의 index와 value를 반복
                if digit != 0: # value가 0이 아니면 Minus 리스트에 1을 추가하고, 
                    Minus.append(1) # InputList의 i번째 인덱스 값에서 1을 빼라 
                    InputList[i] -= 1 # 숫자 3이면 1을 추가하고 원 리스트에서 1을 빼기
                elif digit == 0: # value가 0이면 Minus리스트에 0추가
                    Minus.append(0)
                    
            Minus = ''.join([str(i) for i in Minus]) # Minus리스트에 있는 요소들을 문자로 바꾼 다음 합침
            MinusList.append(Minus)
            nCount += 1 # for문 과정 한번씩 완료 때마다 count 
        print(MinusList)
        return nCount
```
