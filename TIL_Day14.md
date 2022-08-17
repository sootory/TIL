# 알고리즘 특강
## 기본 입출력
1. map(function, iterable)
- 여러 개의 타입 변환
  ```python
  a = int(input())                        정수형 변수 1개 입력 받기
  b, c = map(int, input().split())        정수형 변수 2개 입력 받기
  d = float(input())                      실수형 변수 1개 입력 받기
  e, f, g = map(float, input().split())   실수형 변수 3개 입력 받기
  h = input()                             문자열 변수 1개 입력 받기
  ```

2. 실습
-  개행으로 구분된 두 정수 입력받기(백준, 2558번)
    ```python
    a = int(input())
    b = int(input())
    print(a+b)
    ```

-  테스트 케이스 갯수에 따라 유동적으로 입력받기(백준, 10950번)
   ```python
   Test_case = int(input())
    for data in range(Test_case):
        a, b = map(int,input().split())
        print(a+b)
    ```

 - 특정 형식으로 출력하기 1(백준, 11021번)
    ```python
    Test_case = int(input())
    for x in range(Test_case):
        a, b = map(int,input().split())
        print(f'Case #{x+1}: {a+b}')
    ```

## 문자열(String)
1. 문자열 method
- 자주 사용하는 method로 .split("기준 문자"), .find("찾는 문자"), .index("찾는 문자"), .count("개수를 셀 문자"), .replace("기존 문자", "새로운 문자"), "삽입할 문자".join("삽입 대상 문자열")
- 파이썬에서 문자열은 immutable한 객체임. replace나 join의 결과 값을 사용 하려면 반드시 기존 혹은 새로운 변수에 그 결과 값을 할당 한 후 사용해야 함.

2. 실습
- 태보태보 총난타(백준, 17249번)
```python
taebo = input()
left = taebo[:taebo.index('^0^')]
right = taebo[taebo.index('^0^'):]
print(left.count('@'),right.count('@'))
```
- 유학금지(백준, 2789번)
```python
cam = 'CAMBRIDGE'
word = input()
for x in cam:
    word = word.replace(x,'')
print(word)
```