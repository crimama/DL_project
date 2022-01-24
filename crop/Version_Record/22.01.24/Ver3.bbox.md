# 아이디어 
- json 파일에 있는 bbox 를 이용 해 image의 feature extraction 진행 
- 라벨 모델에서 인풋으로 img, csv, bbox를 넣고 라벨 분류 


# 세부 내용 
- 모델을 두개를 만듬 
- 첫번째 모델은 이미지로 부터 bbox 4개의 점을 예측 하는 모델
    -  이 때 인풋으로 이미지, 아웃풋으로 bbox를 넣음 
    -  따른 어그먼테이션은 하지 않음 
- 두번째 모델은 첫번째 모델에서 예측한 bbox를 이용 해 label을 예측 함 
    - 여기서도 역시 따른 전처리는 없고 resize와 efficientnet preprocess만 진행 
 
- 모델 학습할 때 50번 진행하고 index다시 섞은 다음에 50번 한번 더 진행함 
  - 일종의 2-fold가 된 셈 


- # 결과 
- LB score = 0.9가 나옴 
- 다음에 preprocess -> color 조작 과 augmentation을 하여 진행 
