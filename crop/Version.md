# 버전 별 모델 설계 

1. 베이스 라인 
  - Efficient Net + 2 Stacked bidirectional LSTM
  - optimizer : adam, learning rate = 0.0005
  - Augmentation : rotation 0 90 180 270 -> 약 2만장 

2. 베이스 라인 + 오버 샘플링 
  - Efficient Net + 2 Stacked bidirectional LSTM
  - optimizer : adam, learning rate = 0.0005
  - Augmentation : rotation 0 90 180 270 -> 약 2만장 
  - 오버샘플링 - 클래스 수 균형 맞춤 
