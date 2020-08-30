# DACON-MNIST
## DACON - 글자에 숨겨진 숫자 이미지 예측 (MNIST 변형)
- 일단 l2썼을때 잘되는건 맞는듯
- dropout의 적절한 조절
  - layer가 3층인 경우, 오히려 dropout 0.5를 했을 때 0.2보다 성능 저하 발생
- loss랑 relu도바꿔보기
  - crossentropy일 때보다 SGD일때 성능 저하 발생
- imagedatagenerator 어떤식으로?
  - mnist는 회전이 안좋다는 평이 많음
  - 밝기 조절 했을 때 모든 숫자를 1로 예측하는 문제 발생

---
## 기록
### 0828~0830: efficientnet
- 분류 모델 중 가장 성능이 좋음
- 5번 pooling을 거치므로 최소 32x32의 이미지 필요, 3채널 이미지 필요  
  --> **따라서 내가 가진 mnist(변형)은 28x28x1이라 변형이 필요함** [*참고](https://github.com/qubvel/efficientnet/issues/129)
- 32*32로 만들기 위해 zeropadding을 한 결과 train 정확도가 0.1대에서 멈춤
- 변형 코드 참고
  - https://github.com/fxnnxc/VGG16-RESNET-MNIST/blob/master/src/test.py (사이즈 증가, 3차원으로)  
    --> 여기서 3차원은 (3)=>(3,3,3) 이런식임  
  
