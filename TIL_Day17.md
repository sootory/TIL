# 수업 내용 복습
## python을 활용한 알고리즘(Leetcode_recursion)

1. 509. Fibonacci Number
```python
   class Solution:
    def fib(self, n: int) -> int:
        if n <= 1:
            return n
        # n이 0이나 1이 되기 전까지 fib 함수를 반복
        else:
            return self.fib(n-1) + self.fib(n-2)
```

2. 231. Power of Two
```python
    class Solution:
    def isPowerOfTwo(self, n):
        if n == 1:
            return True
        elif n == 0:
            return False        
        elif n % 2 != 0: # 2의 배수가 아니면 2의 제곱으로 나타낼 수 없음
            return False
        else: # 위의 경우가 모두 아니면, 재귀함수로 n이 1이 될 때까지 2를 계속 나눈 값 리턴 
            return self.isPowerOfTwo(n/2)
```

## PyCaret
> classification, regression, clustering 등 다양한 모델을 지원하여 autoML을 가능하게 하는 python library

```python
# install
pip install pycaret

# load dataset
from pycaret.datasets import get_data
data = get_data('juice')

# init setup
from pycaret.classification import *
s = setup(data, target = 'Purchase', session_id = 123)

# create model
rf = create_model('rf', fold=5) #(model, cross validation 할 데이터 셋 갯수 지정)

# compare models
top5 = compare_models(sort='Accuracy', n_select=5)

## 모델 비교를 먼저하고, lr이나 rf처럼 특정 ML을 선택하여 진행할 수도 있음

#  model tuning & blending
tuned_top5 = [tune_model(i) for i in top5]
blender_top5 = blend_models(estimator_list=tuned_top5)

# prediction
final_model = finalize_model(blender_top5)
prediction = predict_model(final_model, data=dataset)

# check metric
check_metric(prediction['Purchase'], prediction['Label'], metric = 'Accuracy')
```
