# 데이터 분석 특강_spyder 활용
## 유형별 문제 풀이

1. 데이터 세트 내 결측값 갯수 확인

```python

import pandas as pd
import numpy as np

# 데이터 파일 읽기
data1 = pd.read_csv('Dataset_01.csv')

# 전반적인 데이터 구성 및 결측치 확인
data1.info()

# 컬럼명 확인
data1.columns

# 결측치 갯수 총합 구하기
data1.isna().sum().sum()

# TV 열에서 결측치 확인
data1[data1.TV.isna()] 

# TV 컬럼에서 결측치 없는 행만 추출
data1[~data1.TV.isna()] 

# 결측치가 포함된 행의 수
data1.isna().any(axis=1).sum()

```
2. 독립변수(TV, Radio, Social Meaia의 마케팅 예산)와 종속변수(매출액)의 상관분석

```python
# 범주형 변수인 influencer 열은 제거하고 상관 분석 실시
data1[['TV', 'Radio', 'Social_Media', 'Sales']].corr() 

# 인플루언서 컬럼 어차피 제거되니까 빼도되고 그냥해도 됨
data1.corr() 

# sales열만 추출
data1.corr()['Sales'] 

# 위 데이터 중에 sales와의 상관 행 지움
data1.corr()['Sales'].drop('Sales') 

# 상관계수의 절대값이 가장 큰 값 출력
data1.corr()['Sales'].drop('Sales').abs().max()

q2=data1.corr()['Sales'].drop('Sales').abs()

q2 >= 0.6

q2[q2 >= 0.6].index

q2.idxmax() # 최대값이 있는 인덱스명을 리턴
q2.argmax() # 최대값이 있는 위치 번호를 리턴

q2.nlargest(2) # 상위 k개의 인덱스명과 값 리턴
```
3. 위의 변수들을 활용한 회귀분석

```python

# statmodel은 모수적 방법 vs. 사이킷런은 각 변수의 영향력(p-value)를 알 수 없음

# 사이킷런 버전
var_list = ['TV', 'Radio', 'Social_Media']

from sklearn.linear_model import LinearRegression
# 결측지 제거, 입력 변수 2D 구조여야 함 -> 행렬구조로 연산되기 때문

# fit_intercept=True는 default. 결측치 제거 전이라 에러뜸
lm1 = LinearRegression(fit_intercept=True).fit(data1[var_list], data1['Sales'])

# 결측치 제거
q3 = data1.dropna()
lm1 = LinearRegression(fit_intercept=True).fit(q3[var_list], q3['Sales'])

# 모델 안에 attributes와 method를 보여줌
dir(lm1)
lm1.coef_
lm1.intercept_

# 원래 array로 리턴되기 때문에 변수명(index)가 사라짐. 그래서 시리즈로 변환하기
pd.Series(lm1.coef_, index=var_list)

# statsmodels_모수적 방법(가설검정)
from statsmodels.formula.api import ols 
# ols(식, 데이터셋).fit() -> 식은 y ~ x1+x2+C(x3)-1 ->여기서 C는 범주형 변수를 더미로 자동화하는

lm2 = ols('Sales ~ TV+Radio+Social_Media', data1).fit() # 결측치 있어도 구조가 2D가 아니어도 작동

dir(lm2)

lm2.summary()
lm2.params

# summary에 있는 coef가 최소자승법을 통한 최선의 회귀식의 계수값임. 이는 오차에 대한 가정을 한 것이기 때문에 회귀식이 적합한지에 대한 평가 필요 -> 잔차 분석(모델에 대한 신뢰 지표) 
# -> 사이킷런은 이를 무시하기 때문에 회귀식의 신뢰 여부를 판단하기 어려움. 그래서 train과 test data를 나눠서 확인
# nonrobust -> 이상치에 민감하다는 말임(산술평균기준으로 최소자승법을 계산하기 때문에)
# R-squared -> 모델의 설명력(분산_y 데이터의 흩어진 정도_을 이용해서 회귀식의 존재 유무와 설명력을 구함->pdf 27p)
# SSR이 커질수록 회귀식의 기울기가 커짐 -> x가 y에 주는 영향이 큼 -> R제곱은 SSR/SST 또는 1-(SSE/SST)
# R제곱은 비선형일 때 제로가 나오는 경우가 있어, 이 값이 0이면 비선형관계인지 확인해봐야 함
# R제곱은 입력 변수가 많아지면 커지는 경향이 있어 아래 조정된 R제곱(여러 모델들 중 평가한다면 이걸로)
# DF는 자유도로 모델에 대한 자유도와 잔차에 대한 자유도 있음
# 샘플 데이터 수가 적으면 과소추정 -> 보정을 해야하는 데 자유도를 적용했을 때 모집단의 분산과 유사해짐. 
# 자유도로 나누면 분산을 구할 수 있는데 SSR->MSR, SSE->MSE임. 
# F통계량은 MSR/MSE? F통계량의 prob는 회귀식이없다(귀무: 모든 베타값이 0 vs. 대립: 여러 베타 중 하나 이상 0 아님)
# SSR의 자유도는 입력 변수의 갯수인 k, SSE는 n-k-1
# skew는 잔차를 가지고 한 통계치 -> 
# Durbin-Watson은 2 근방이면 잔차의 독립. 커지면 양의 관계, 작을수록 음의 관계

lm3 = ols('Sales ~ TV', data1).fit()
lm3.summary()


# bonf값이 0.05 보다 작으면 이상치, 크면 정상
lm3.outlier_test()

q3[lm3.outlier_test()['bonf(p)']<0.05]

# 변수 선택 기법(이 중 하나 이상?)
# 1. 상관계수 2. 회귀분석 후 p-value 3. RFE: 지정한 수의 변수를 선택 4. 자동으로 선택-> Lasso, Ridge 모델(두개 섞은게 elastic)
# kernel ridge regression -> 비선형 모델의 해를 구하는 -> 딥러닝도 이러한 모델의 확장 버전이라고 볼 수 있음
# 다중공선성 -> 머신러닝은 다중공선성이 존재하기 쉬움. 예측 성능이 우선이기 때문에 다중공선성은 크게 고려하지 않음
# 딥러닝은 독립변수들을 합해서 새로운 변수를 만들고 가중치를 찾는 것, 이를 스케일링 하는 것이 활성화 함수, 복잡한 회귀식을 이용하여 데이터의 특징을 찾아가는(y 값을 찾는)
# 딥러닝 데이터가 많으면 많을수록(복잡할수록) 특징을 찾을 수 있기 때문에 파워풀, 데이터 수가 적으면 모델이 복잡해도 단순하니까 성능 떨어짐. 딥러닝도 각 가중치와 변수 특징 확인할 수는 있음.


pip install -U scikit-learn
from sklearn.feature_selection import RFE

# RFE(모델, 변수 수).fit(입력변수, 출력변수) -> 결측치 제거한 q3를 입력변수로

best_lm = RFE(LinearRegression()).fit(q3[var_list], q3['Sales'])
best_lm.predict(q3[var_list])
dir(best_lm)

best_lm.estimator_.coef_

pd.Series(best_lm.ranking_, index = var_list)
