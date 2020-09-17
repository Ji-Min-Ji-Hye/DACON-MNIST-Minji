# DACON-MNIST
## DACON - 글자에 숨겨진 숫자 이미지 예측 (MNIST 변형)
---

repo 수정시 [클릭](https://github.com/Ji-Min-Ji-Hye/DACON-MNIST-minji/compare/master...minji-o-j:master)

---
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
  
  - https://github.com/Jsimluken/pyTraining/blob/b3b6d22a7c6f2c42355657e55548f224fe3196f6/keras/Chick/EfficientNet.ipynb (3차원)  
    --> 여기서 3차원은 (3)=>(1,1,1)  이런식임  
<br>

- 하지만 280*280으로 시도한 결과, train 정확도가 0.86 또는 0.84대에서 멈춤
  - weight를 None/imagenet 둘다 시도해도 특정 지점에서 멈춤  
    - 근데 imagenet의 가중치(학습된 가중치) 사용 불가라고한다.. 기존dataset 불러오는 코드부터 있어야한다고 한다.   

---
### 0830
- train data가 2048개로 test가 20480개인데 비해서 매우 적은 편
- data가 흑백으로 되어있음
- data 바꿔보기(다음주 일욜까지)
---
### 0905
- 전에 padding을 했을 때 정확도가 매우 낮았음 -->특징점이 부족한 것 아닐까 생각
- 다른 github에서 이진화한 데이터로 해보았을 때 매우 낮다고 한 것 발견 --> 이것도 원래 데이터에는 0~255까지 있는것을 0, 255 2개로만으로 바꾸어서 특징이 줄어든것이 아닐까 라는 생각이 들었음
