# 아이디어 
- 모델 라인에 인풋 이미지를 랜덤하게 Preprocess 하는 것 추가 



# 세부 내용 
- #어그먼테이션
data_augmentation = tf.keras.Sequential([
    tf.keras.layers.experimental.preprocessing.RandomTranslation([-0.1, 0.1], [-0.1, 0.1], seed = 777),
    tf.keras.layers.experimental.preprocessing.RandomCrop(224, 224, seed = 777),
    tf.keras.layers.experimental.preprocessing.RandomZoom([-0.1, 0.1], [-0.1, 0.1], seed = 777),
    tf.keras.layers.experimental.preprocessing.RandomRotation([-0.1, 0.1], seed = 777),
    tf.keras.layers.experimental.preprocessing.CenterCrop(224, 224),
])

- 이 라인을 Phase 2 라인 이미지 인풋 받자마자 바로 적용될 수 있게 대입 



- 결과 
- LB 가 0.9007로 미약하게 나마 상승 함 
- 하지만 Rotation Augmentation을 적용하지 않은 모델의 결과 이므로 Augmentation이 적용 될 경우 더 높이 상승할 여지가 있다고 봄 
