Dacon : https://dacon.io/competitions/official/235870/overview/description
# 전체 설계 
- 베이스 라인 [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/crimama/DL_project/blob/main/crop/crop_diseases_classifcation_baseline)
 
# 작업 일지 
- 추후 고려사항 : Augmentation, label, overfitting, using image croped by label, Diseases occ 후 multi class classification , stratified k fold 

## **22.01.20**
- To do : 베이스라인 정리, 자료 써칭 
  - 우선 stacked LSTM + Efficient Net 모델 베이스라인으로 정리
  - 그 후 적용 가능한 기법들 써칭 해서 정리 -> 하나 씩 적용 
  - 버전 별 적용 사항 같이 기록 
 - **버전 별 기록**
   - 22.01.20_ver1 : 오버샘플링_베이스라인 
     - 모델 자체 성능은 val_accuracy 0.9989 가 나옴, 테스트 accuracy 도 1이 나옴 
     - 하지만 문제 : train,test, valid 중복들이 있어서 성능이 높게 나오는 것으로 생각 됨 -> oversampling 시킨 데이터들의 조작 필요 
     - 결과 : 제출 : 0.82 -> 오버샘플링 하면서 중복되는 데이터들이 너무 많아 되려 오버피팅이 심해진 것으로 예측 됨
   - 22.01.21_ver2 : 랜덤어그먼테이션_베이스라인
     - stacked LSTM + Efficient Net, 이미지 rotate augmentation + random augmentation
     - submission F1 score 0.88 나옴, 파기 
   - 22.01.21_ver3 : 베이스라인 다시 진행 
     - stacked LSTM + Efficient Net, 이미지 rotate augmentation

## **22.01.19**
  - 개별 모델 occ - multi class 진행 한번 해보고 안되면 통합 모델로 진행 
  - 오늘 설계 : Phase1에는 모두 들어감, Phase2-0 에선 Disease 가 0인지 1인지만 구분, Phase2-1 에선 1들만 갖고 
- **버전 별 기록**
  - Ver1 작업 및 작업 이슈 
    - disease 인코딩 - 디코딩 
    - Phase 2 다시 설계 -> 실패, 파기 
    - envs 정규화 -> val_acc 감소 함 : 파기 
    - envs co2 사용 -> 보류 
    - csvs 정제 
    - shape 확인 
    - 이미지 median filter 
    - rotated image multi head 로 
  - Ver2 작업 및 작업 이슈 
    - 22.01.19_작물병해_통합라벨모델링_2 <- csv 파일 정제에 집중
    - 단순하게 결측치를 매꾸는 것은 불가능 
    - 하지만 이슬점, CO2 매우 중요한 변수들 -> 논문들에서 보면 이슬점과 CO2가 작물 재배에 영향을 줌 
    - 따라서 선형 또는 예측 모델을 이용 해서 CO2 변수를 채우고 이를 다시 시계열 예측을 통해 shape를 맞춰 최종 모델 학습에 이용 
    - 필요 모델 
    - 이슬점 결측치  -> ffill
    - co2 예측 
         

## **22.01.18** 
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
      - submission 데이터 로드 -> 용량이 너무 큼, 데이터 5만개 
      - 버그 발견 : csv로드 잘못 가져옴 -> 결측치 처리 필요 
      - csv 결측치 : '-'는 0으로 처리하고, 사이즈 294,9로 통일 (cv2.resize를 활용)
    - 작업 이슈 
      - csv reshape 관련 
  - Ver3 작업 및 작업 이슈 
    - 작업
      -  test 데이터 이용 해서 submission 만들기
      -  5만개 한번에 하지말고 1만개씩 혹은 5천개씩
      -  submissiono 1만개씩 나눠서 해서 성공 
      -  하지만 정확도가 굉장히 낮음 
      -  crop-disease-risk간 한정된 경우의 수가 있는데, 모델 학습 시 이 경우의 수 보다 더 많게 경우의 수가 계산 됨 -> 오차 증가 
      -  경우의 수를 제한 시킬 필요가 있음 

## **22.01.17** [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/crimama/DL_project/blob/main/22.01.17_작물병해_모델링.ipynb)


  -  처음엔 sample 50, sample 500개를 이용 하여 모델링을 시도 함 
  -  하지만 50개, 500개의 경우 데이터의 양이 적어 제대로 학습이 되지 않음 
  -  그리고 모델링을 할 때 Input : image + label, Output : crop을 해서 모델링을 설계 함, 하지만 label이 crop 예측에 도움 줄 것이라 예측했지만 되려 방해가 됨 
  -  또 label을 json파일로 부터 가져올 때 image의 resize에 맞춰 같이 resize를 해야 했기에 어려웠음 
  -  그래서 방법을 바꿔 Dacon에 올라와 있는 샘플 데이터를 참고 해 다시 진행 함 
  -  Image와 Crop만을 이용 해 예측을 진행 함 
  -  accuracy가 0.95 이상이 될 정도로 높은 정확도를 보임, test데이터 역시 0.95 높게 나타남
    -  우선 모델 설계 가설은 Phase1에선 성공 
