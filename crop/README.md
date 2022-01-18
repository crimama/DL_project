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
- 추후 고려사항 : Augmentation, label, overfitting, using image croped by label, Diseases occ 후 multi class classification , stratified k fold 

- **22.01.18** 
  - 내일 작업하기 전에 내일 할 일 step 별로 작성 뒤 그거에 맞춰서 진행 
  - 전체 To do 
    - 어제 작업한 것 정리 
    - Env 데이터 정제 -> LSTM에 돌릴 수 있게 (우선적으로 모델 진행 후 결측치 처리) (fin, 우선 5867,58,9) shape로 정제 -> LSTM에 58,9 shape로 인풋) 
    - Phase 2 코딩 -> image, env, crops -> diseases로 설계 (
    - Env 데이터 + 이미지 + Crop 넣어서 학습 
    - 모델 결과 보고 튜닝 
    - 시간 남으면 Env 결측치 처리 
  - Ver1 작업 및 작업 이슈 
    - 작업 
      - 어제 작업한 것 정리 
      - Env 데이터 LSTM에 도릴 수 있게 정제, 우선 적으로 -1, 58,9 형태의 shape로 정제 -> 추후 Co2 데이터 추가 필요 
      - Phase 2 코딩 -> iamge, env, crops -> diseases 네트웤으로 설계 
      - Env + 이미지+ crop 으로 학습 -> 약 0.86 score 나옴 but class 가 굉장히 imbalance 해서 score가 신뢰성이 낮음 -> 추후에 0-1 -> multi classificaion으로 micro 분리 
    - 작업 중 이슈 
      - Env 데이터를 우선 적으로 -1,58,9의 shape로 정제 해 놓았지만 이렇게 하는 것이 맞는지 의문 
      - Env 데이터에 CO2 데이터를 사용하고 싶지만 결측값이 많음 + 10분 단위로 단위당 2개의 행 데이터가 있는데 이걸 하나로 합칠 수는 없는지 
      - Phase 2 설계는 다 했지만 세부 옵션 (activation, 튜닝, Dense, 등)을 조정할 필요가 있음, 그리고 제대로 설계 햇는지 확인 필요 
      - test데이터 넣어본 결과 0.85정도 나왔는데 class가 imblance 해서 정확도 차이가 심함 
    - 추가 수정 사항 
      - LSTM -> bidirectional  
      - Preprocess try 
      - Node 수 증가 
      - Optimizer 바꾸며 확인 
      - Flatten 이후 Hidden layer 수 통일 
  - Ver2 작업 및 작업 이슈 
    - 작업 
      - 수정사항 적용 (optimizer 제외) : Bidirectonal, batchnormalization, node 수 변경(10->32), 
      - 수정사항 후 확인 -> 성능, 오버피팅 향상 됨, 계속 진행 (optimizer 튜닝은 추후 진행) 
      - preprocesss try -> 적용 했지만 큰 차이 없거나, 성능 미세하게 증가, 일단 계속 적용 
      - 데이터 기본 전처리 -> 전처리 탭에 통합 
      - phase 3 설계 -> 0.94 f1 score 
      - train, test 통합 -> 통합x, 각 pahse마다 필요한 input, output이 다르기 때문 

- **22.01.17** [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/crimama/DL_project/blob/main/22.01.17_작물병해_모델링.ipynb)


  -  처음엔 sample 50, sample 500개를 이용 하여 모델링을 시도 함 
  -  하지만 50개, 500개의 경우 데이터의 양이 적어 제대로 학습이 되지 않음 
  -  그리고 모델링을 할 때 Input : image + label, Output : crop을 해서 모델링을 설계 함, 하지만 label이 crop 예측에 도움 줄 것이라 예측했지만 되려 방해가 됨 
  -  또 label을 json파일로 부터 가져올 때 image의 resize에 맞춰 같이 resize를 해야 했기에 어려웠음 
  -  그래서 방법을 바꿔 Dacon에 올라와 있는 샘플 데이터를 참고 해 다시 진행 함 
  -  Image와 Crop만을 이용 해 예측을 진행 함 
  -  accuracy가 0.95 이상이 될 정도로 높은 정확도를 보임, test데이터 역시 0.95 높게 나타남
    -  우선 모델 설계 가설은 Phase1에선 성공 
