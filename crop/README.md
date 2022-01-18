Dacon : https://dacon.io/competitions/official/235870/overview/description
# 전체 설계 

- 전체 설계 : 기존의 샘플링 코드에 나온 IMAGE, ENV를 이용해 crop - disease - risk를 한번에 예측하는 것이 아닌 crop, disease, risk를 모델 3개에 나누어 각각 예측한다 
- Phase 1 
  - input을 image, output 을 crop으로 하여 예측 
  - Efficient Net을 Conv layer로 하여 모델 설계 
    - Resnet 50을 사용 했지만 Efficient net이 훨씬 accuracy가 높음 
- Phase 2 
  - input을 image, env, crop으로, output을 disease로 하여 예측 
  - image는 Efficient Net, env는 LSTM, crop은 Dense로 하여 multi head로 진행 
- Phase 3 
  - input을 image, env,crop,disease, output 을 risk로 하여 예측 
  - image : Efficient Net, Env : LSTM, crop : Dense, Disease : Dense로 Multi Head로 진행 
- Phase 4 
  - test 데이터를 이용 해 Phase 1부터 Phase 3까지 진행, 이때 각 crop, disease, risk는 predict를 통해 나온 결과를 이용 
  - 최종 Phase1 ~ Phase 3를 통해 Predict된 crop-disease-risk와 test_y를 비교해 accuracy 측정 
 

# 작업 일지 
- 추후 고려사항 : Augmentation, label, overfitting

- 22.01.18 
  - 내일 작업하기 전에 내일 할 일 step 별로 작성 뒤 그거에 맞춰서 진행 
  - To do 
    - 어제 작업한 것 정리 (fin)
    - Env 데이터 정제 -> LSTM에 돌릴 수 있게 (우선적으로 모델 진행 후 결측치 처리) 
    - Chapter 2 코딩 
    - Env 데이터 + 이미지 + Crop 넣어서 학습 
    - 모델 결과 보고 튜닝 
    - 시간 남으면 Env 결측치 처리 

- 22.01.17 [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/crimama/DL_project/blob/main/22.01.17_작물병해_모델링.ipynb)


  -  처음엔 sample 50, sample 500개를 이용 하여 모델링을 시도 함 
  -  하지만 50개, 500개의 경우 데이터의 양이 적어 제대로 학습이 되지 않음 
  -  그리고 모델링을 할 때 Input : image + label, Output : crop을 해서 모델링을 설계 함, 하지만 label이 crop 예측에 도움 줄 것이라 예측했지만 되려 방해가 됨 
  -  또 label을 json파일로 부터 가져올 때 image의 resize에 맞춰 같이 resize를 해야 했기에 어려웠음 
  -  그래서 방법을 바꿔 Dacon에 올라와 있는 샘플 데이터를 참고 해 다시 진행 함 
  -  Image와 Crop만을 이용 해 예측을 진행 함 
  -  accuracy가 0.95 이상이 될 정도로 높은 정확도를 보임, test데이터 역시 0.95 높게 나타남
    -  우선 모델 설계 가설은 Phase1에선 성공 
