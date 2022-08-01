# 수업 내용 복습
## numpy
1. 기본
- 넘파이는 행렬이나 다차원 배열을 관리하기 위한 ndarray 객체를 사용
- 간단하게 연산 가능
```python
  data = [1, 2, 3]
  result = []
  for i in data:
    result.append(i * 10)
  print(result)

#이를 넘파이로 구현하면 아래와 같이 간단.

import numpy as np

arr = np.array([1, 2, 3])
result = arr * 10
print(result)
```
- 2차원 리스트
  - 넘파이를 사용하면 arr[행 인덱스, 열 인덱스] 또는 arr[행 인덱스][열 인덱스]와 같은 표현을 통해 특정 위치의 원소에 접근할 수 있다.
``` python
# 컬럼 단위의 인덱싱

data2d = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

arr = np.array(data2d)
print(arr[ : , 0])
```
2. ndarray
- 1차원 또는 2차원 리스트를 array 함수에 전달하면 ndarray 객체로 변환 가능.
- 데이터와 데이터 사이에 콤마 구분 기호 없이 출력
- 인스턴스 변수를 사용해 저장된 데이터 정보 조회
```python
print(arr2.shape)  #ndarray의 크기 정보
print(arr2.ndim)   #차원 정보
print(arr2.dtype)  #데이터 타입을 표현

*reshape()
배열의 형상(shape)을 변경할 수 있는 함수.

ndarr1 = np.arange(6) #6개의 원소로 구성된 1차원 배열
ndarr2 = ndarr1.reshape(2, 3) #2행 3열로 변경
print(ndarr2)

> [[0 1 2]
  [3 4 5]]
```
