# 주말 복습
## 시각화

```python
# 라이브러리 설치
from matplotlib import pyplot as plt
```

1. 막대 그래프

```python
movies = ["Annie Hall", "Ben-Hur", "Casablanca", "Gandhi", "West Side Story"]
num_oscars = [5, 11, 3, 8, 10]

# plt.bar(movies, num_oscars) -> 이걸로 해도 표는 잘 생성됨
plt.bar(range(len(movies)), num_oscars)
plt.xticks(range(len(movies)), movies) #x축 레이블 값 변경
plt.ylabel("Academy Awards") # y축 label 값 
plt.xlabel("Actor Name") # x축 label 값 
# plt.bar([0, 1, 2, 3, 4], num_oscars)
plt.show()
```
- 추가 활용 가능 함수
  ```python
  # 축 범위 설정
  plt.axis([x1,x2, y1, y2])
  # 표 제목
  plt.title()
  ```

2. 히스토그램
> 막대 그래프의 한 종류로 양적 데이터를 범주로 사용할 때 유용하다. 예를 들어, 무게, 길이, 시간, 점수 등

```python
# bar를 활용
plt.bar(np.array(list(histogram.keys()), dtype= np.int64)+5,
        histogram.values(),
        width=10,
        edgecolor = (0,0,0))

plt.xticks(np.arange(0,101,10))
plt.axis([-5, 105, 0, 5])
plt.xlabel("score")
plt.ylabel("of students")
plt.show()

#히스토그램 함수를 활용
plt.hist(grades,
         width=10,
         edgecolor = (0,0,0))


plt.xticks(np.arange(0,101,10))
plt.axis([-5, 105, 0, 5])
plt.xlabel("score")
plt.ylabel("of students")
plt.show()
```

3. 선 그래프
> 선 그래프는 막대 그래프의 상단 중심부를 선분으로 연결하여 범주별 변화를 비교하는 그래프이다. 시계열 데이터에 대한 정보를 전달할 
때 유용하다.

```python
years = [1950, 1960, 1970, 1980, 1990, 2000, 2010]
gdp = [300.2, 543.3, 1075.9, 2862.5, 5979.6, 10289.7, 14958.3]

plt.plot(years, 
         gdp,
         color=(0,0,0), #색상 지정(블랙)
         marker = "*") #포인트
```

4. 산점도
> 두 변수 간의 연관 관계를 2차원 평면 상에서 점으로 찍어 보여 주는 그래프이다.

```python
friends = [ 70,  65,  72,  63,  71,  64,  60,  64,  67]
minutes = [175, 170, 205, 120, 220, 130, 105, 145, 190]
labels =  ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i']

plt.scatter(friends, minutes, s=30) #s는 점의 크기
plt.annotate("a", 
             xy=(70,175))

# 이 외에도 area, color 등 다양하게 지정 가능
# 산점도와 막대그래프는 축 지정 시 유의해야 함