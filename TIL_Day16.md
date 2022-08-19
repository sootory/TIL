# 알고리즘 특강
## 리스트_2
1. 2차원 리스트
 - list comprehension을 활용
   ```python
   	# 2차원 리스트 입력 받을 때 자주 사용하는 패턴

    n = int(input())
    board = [list(map(int, input())) for _ in range(n)]
    ```
- 실습
  ```python
  # 백준 1100번
  #문자열을 리스트로 바꾸면 한글자씩 쪼개서 리스트로!
    chess = [list(input()) for i in range(8)]
    horse = 0
    for row in range(8):
        for col in range(8):
            # 만약에 (행이 짝수이고 열이 짝수) 또는
            # (행이 홀수이고 열이 홀수) 이면서
            # chess[행][열]=='F' 인 개수를 구하여라
            if (row%2==0 and col%2==0) or (row%2==1 and col%2==1):
                if chess[row][col] == 'F':
                    horse += 1

    print(horse)
```
