# 수업 내용 복습
## 중간 시험 정리
1. sigmoid 함수
   - 명목형(categoricla) 변수를 예측하는 딥러닝 모델에서 활용 가능
   - sigmoid는 0~1 사이 값으로 분포를 바꾸어 binary/multi-label classification이 가능
   - 마지막 layer에서 활성화 함수로 sigmoid를 활용할 때, binary classification의 경우 unit 1개면 충분하지만 multi-lable classification은 class의 수 만큼 unit이 필요함
   - multi-class label을 예측하는데는 적절하지 않음

2. Model.fit()
   - epoch이 완료될 때마다 validation data에 대한 성능을 측정함

3. Call back()
   - epoch마다 learning rate 조절 가능
   - 학습 과정에 대한 log를 저장하여 tensorboard로 시각화할 수 있음
   - overfitting을 피하기 위한 방법으로, validation set에서 가장 성능이 좋은 모델을 저장
   - call-back 함수는 epoch을 수행할 때마다 실행됨
   - cross-entopy loss의 경우 낮을수록 좋은 모델

4. 1DConv
   - time-series data를 2차원화하여 1D convolution으로 분석할 수 있음
   - Filter의 width는 feature의 dimension값과 같음
   - 하나의 unit이 만들어내는 output은 1차원 vector
   - many to many/many to one 모두 학습 가능
  
5. Text-embedding
   - 컴퓨터가 단어를 학습할 수 있도록 numeric input으로 변형하는 과정(비정형을 정형화)
   - 비슷한 글자끼리의 거리는 가까울수록 좋은 임베딩 알고리즘이라 할 수 있음
   - 자연어 처리에 있어서 모델의 input layer쪽에서 처리해줘야 함
