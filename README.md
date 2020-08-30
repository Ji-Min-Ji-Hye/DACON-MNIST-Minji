# DACON-MNIST
## DACON - 글자에 숨겨진 숫자 이미지 예측 (MNIST 변형)
- 일단 l2썼을때 잘되는건 맞는듯
- dropout의 적절한 조절
  - layer가 3층인 경우, 오히려 dropout 0.5를 했을 때 0.2보다 성능 저하 발생
- loss랑 relu도바꿔보기
  - crossentropy일 때보다 SGD일때 성능 저하 발생
- imagedatagenerator 어떤식으로?
  - mnist는 회전이 안좋다는 평이 많음
  - 밝기 조절 했을 때 모든 숫자를 1로 예측하는 문제 

---
## 기록
### 0828~0830: efficientnet
- 분류 모델 중 가장 성능이 좋음
