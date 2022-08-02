# 수업 내용 복습
## python 기초 문법 실습(Leetcode)

1. 1480. Running Sum of 1d Array
> 리스트로 주어지는 정수의 누적 합 구하기
```python
sum = []
nums_1 = 0
for i in nums:
    nums_1 += i
    sum.append(nums_1)
return sum
```

2. 1672. Richest Customer Wealth
> 이중 리스트 중 각 인덱스의 합을 구하여 가장 큰 값을 리턴
```python
Max = -1
for i in range( len( accounts) ):
    currentSum = 0
    for j in range(len(accounts[i])):
        currentSum += accounts[i][j]
        if Max < currentSum:
        Max = currentSum
return Max
```
3. 412. Fizz Buzz
> 각 조건에 맞는 값 출력
```python
Answer = []
for i in range(n):
    if (i+1) % 3 == 0 and (i+1) % 5 == 0:
        Answer.append('FizzBuzz')
    elif (i+1) % 3 == 0:
        Answer.append('Fizz')
    elif (i+1) % 5 == 0:
        Answer.append('Buzz')
    else:
        Answer.append(str(i+1))
return Answer
```

4. 1342. Number of Steps to Reduce a Number to Zero
> Given an integer num, return the number of steps to reduce it to zero. In one step, if the current number is even, you have to divide it by 2, otherwise, you have to subtract 1 from it.

```python
counts = 0
while num != 0:
    if num % 2 ==0:
        num /=2
    else:
        num -=1
    counts +=1
return counts
```

5. 383. Ransom Note
> Given two strings ransomNote and magazine, return true if ransomNote can be constructed by using the letters from magazine and false otherwise. Each letter in magazine can only be used once in ransomNote.

```python
R_list = list(ransomNote)
M_list = list(magazine)
Answer = True
for i in R_list:
    if i not in M_list:
        Answer = False
        break

    else:
        M_list.pop(M_list.index(i))
                
return Answer
```

            