# 알고리즘 특강
## 리스트
1. 리스트 특징
   - python의 리스트는 배열과 연결리스트의 장점만 합친 것과 같음
   - 배열처럼 인덱스 접근을 통해 데이터에 빠르게 접근 가능
   - 연결리스트처럼 가변적으로 길이를 조절하고, 다양한 데이터 타입을 저장할 수 있음
     
2. 실습_1
```python
# 백준 11720번

N = int(input())
bigNumber = input()
    # 각 인덱스의 데이터를 모두 정수형(int)으로 바꾸기
bigNumber = list(map(int,bigNumber))
print(sum(bigNumber))

#백준 2750번

N = int(input())
    #N개의 줄에 있는 정수를 입력받는 방법
lst = [int(input()) for i in range(N)]
lst = sorted(lst)
for data in lst:
    print(data)
```
3. list comprehension
   - map, filter 함수 대신 사용하기
    ```python
    # map 함수 대신 사용하기

    numbers = [int(i) for i in input().split()]

    print(numbers)
    # [1, 2, 3, 4]

    # filter 함수 대신 사용하기

    odd_numbers = [i for i in range(10) if i % 2 == 1]

    print(odd_numbers)
    # [1, 3, 5, 7, 9]
    ```
4. 실습_2
   ```python
   # 정올 리스트 3_자가진단 1

   N = int(input())
   lst = [x*x for x in range(1,N+1)]
   print(lst)

   # 정올 리스트 3_형성평가 1
   N = int(input())
   lst = [f'No.{x}' for x in range(1,N+1)]
   print(lst)

   # 백준 2462
   #9개의 숫자를 입력받는다.
    lst = [ int(input()) for i in range(9)]
    print(max(lst))
    print(lst.index(max(lst))+1)
    ```
