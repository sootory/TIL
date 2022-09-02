# 수업 내용 복습
## Segmentation
- 이미지에서 객체가 있는 위치, 해당 객체의 모양, 이미지의 각 픽셀이 어느 클래스에 속하는지 등을 파악하고 싶을 때 활용
- 이미지의 각 픽셀에 레이블이 부여되고, 픽셀 단위의 마스크를 출력하도록 신경망을 훈련
- multiple objects의 분류에 object detection과 같이 많이 활용
- image augmentation도 이전과 달리 elastic deformation 기법을 씀

### 대표 모델
1. U-Net
   - 인코더(다운샘플러)와 디코더(업샘플러)를 포함
   - 미리 훈련된 모델을 인코더로 사용 가능
   - 이미지 분류에서 했던 것처럼 convolution한 이미지를 pooling하여 작아지기 전 결과값을 같은 이미지 사이즈의 업샘플링 단계에서 input으로 추가
  
2. U-Net vs. U-Net 2.0
   - U-Net은 낮은 레이어의 input을 그대로 높은 레이에 추가한다면, 2.0 버전은 중간에 processing layer가 추가됨(이 layer에서 합성곱을 한다고 함)
   - 두 모델의 성능 차이는 크지 않다고 함

참고 자료: [이미지 분할](https://www.tensorflow.org/tutorials/images/segmentation?hl=ko),   
수업 제공 자료