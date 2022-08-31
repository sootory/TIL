# 수업 내용 복습
## 1D CNN(1D Convolutional Neural Networks)
> 1D convolution layer creates a convolution kernel that is convolved with the layer input over a single spatial (or temporal) dimension to produce a tensor of outputs.

- 특징
  - 커널(필터)의 너비는 벡터의 차원과 동일하게 설정(곧, 2D 합성곱과는 달리 너비 방향이 아닌 아래로만 움직일 수 있음). 커널의 크기는 자유롭게 설정 가능함
  -> 필터가 벡터의 차원과 동일하지 않은 예제도 있으니 더 확인 필요
  - 1D CNN에서도 합성곱 연산과 활성화 함수 다음에는 풀링 단계를 거침(max 또는 average pooling을 많이 씀)
  - 여러 필터를 통해 연산을 한 후 벡터를 도출하고, 해당 벡터를 풀링한 후 얻은 스칼라 값을 연결하여 하나의 벡터로 만듦
  
- 예시

![Kernel sliding over accelerometer data](https://miro.medium.com/max/700/1*JMt3BwFFyyIO780dDIN4Uw.png)

  ```python
  import keras

  from keras.layers import Conv1D

  model = keras.models.Sequential()

  # input_shape: 120 time-step과 각 step별 3의 data point가 있음
  # 커널의 너비는 3, 크기는 5
  model.add(Conv1D(1, kernel_size=5, input_shape = (120, 3)))

  model.summary()
  ```

참고 자료 및 출처: 
[Understanding 1D and 3D Convolution Neural Network | Keras](https://towardsdatascience.com/understanding-1d-and-3d-convolution-neural-network-keras-9d8f76e29610)   
[Conv1D layer](https://keras.io/api/layers/convolution_layers/convolution1d/)   
(도서) 딥 러닝을 이용한 자연어 처리 입문 
