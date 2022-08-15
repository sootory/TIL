# 시험 대비
## 머신러닝, 딥러닝 기초 학습(시험 위주로 정리)

1. box plot
> A box plot (or box-and-whisker plot) shows the distribution of quantitative data in a way that facilitates comparisons between variables or across levels of a categorical variable. The box shows the quartiles of the dataset while the whiskers extend to show the rest of the distribution, except for points that are determined to be “outliers” using a method that is a function of the inter-quartile range.

 - 주요 개념
   - x축은 범주형(categorical), y축은 연속형(numeric) 변수
   - 데이터의 분포를 4분위수(quartile)로 나타냄
   - 이상치(outlier)는 4분위수 범위 안에 포함하지 않음

2. 선형회귀분석(Linear Regression)

   > 종속 변수 y와 한 개 이상의 독립 변수 (또는 설명 변수) X와의 선형 상관 관계를 모델링하는 회귀분석 기법
- 주요 개념
   - 주로 x,y 둘다 연속형 변수를 대상으로 하나, x가 연속형이 아닐 때는 reference를 설정한 후 더미화함
   - p-value(유의확률): 귀무가설을 가정하였을 때 표본 이상으로 극단적인 결과를 얻을 확률. 0.05 미만을 통계적 유의함의 기준으로 삼는 경우가 많고, 각 대표적인 기준에 따라 결과 보고하는 경우가 다수임
   - coefficient는 기울기로 더미 변수에서는 레퍼런스과 비교한 값으로 해석할 수 있음
    
3. Keras Logit Model Fitting
  ```python
# input_shape -> 독립변수의 수, activation은 activation function 의미
  model.add(Dense(3, activation = 'linear', input_shape=(2,)))

# 로짓 분석이기 때문에 마지막은 로직 분석을 위한 sigmoid 함수를 지정. 단 하나의 정답이 존재할 때는(multi class classification) softmax라는 함수를 사용
  model.add(Dense(1, activation = 'sigmoid'))

# 로지스틱은 loss를 아래와 같이하는데, 선형회귀와 같은 연속변수일 때는 MSE로 지정함.
  model.complile(loss='binary_crossentropy', optimizer=Adam(learning_rate=0.01))

# CALLBACK: 1 epoch가 모두 fit되었을 때 실행되는 함수. CP는 modelcheckpoint로 성능을 고려하여 현재 모델의 weight(가중치)를 저장함. val_acc가 monitor이면 mode = 'max', val_loss가 monitor이면 mode = 'min'으로 설정. LR는 reduceLROnPlateau로 learning rate는 학습을 해가면서 줄이는 것이 바람직함

CALLBACK = CP,TB, LR
```

4. CNN(Convolutional Neural Network)
   > n deep learning, a convolutional neural network (CNN, or ConvNet) is a class of artificial neural network (ANN), most commonly applied to analyze visual imagery
- 주요 개념
  - Convolutional layers: After passing through a convolutional layer, the image becomes abstracted to a feature map, also called an activation map, with shape: (number of inputs) x (feature map height) x (feature map width) x (feature map channels). Convolutional layers convolve the input and pass its result to the next layer.
  
  - Pooling layers: Pooling layers reduce the dimensions of data by combining the outputs of neuron clusters at one layer into a single neuron in the next layer. 

