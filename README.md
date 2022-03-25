# 진행한 개인 프로젝트 & Summary 

## Run-way Functions: Predict Reconfigurations at US Airports (Open Arena)
세부 내용 : (https://github.com/crimama/Airport_Configuration)
주요 포인트 : 100기가 이상의 대용량 csv 데이터를 이용한 모델 개발 
프로젝트 개요 
 - 목적 : 각 공항들의 활주로 조합 최적화를 위해 과거의 조합들을 학습하고 미래에 어떤 활주로가 활성화 될지 예측한다 
 - 데이터 : 미국 10개 공항의 공항 별 이착륙, 활주로 활성화 여부, 기상 데이터 
 - 분석 모델 
   - Input 데이터로 과거 12시간의 활주로 조합 그리고 기상 데이터를 사용(풍향 데이터는 임베딩 레이어를 통해 진행) 
   - 과거 활주로 데이터와 기상 데이터는 각각 multi modal로 Neural network에서 Feature Extraction 됨 
   - 각각 Feature Extraction 된 데이터를 Concat한 후 softmax를 통해 출력 
   - categorical entropy loss 함수를 통해 미래 6시간의 configuration active 될 확률 예측 

## 환자의 Brain mri 이미지 + 환자 정보를 이용한 환자 건강 정보 예측 및 분류 
세부 내용 : (https://github.com/crimama/MRI_classification)
주요 포인트 : MRI 이미지를 처리하기 위해 2.5D 형태(shape :256,256,19)로 가공하였으며, Feature Extraction을 위해 3개의 전이학습 모델 앙상블을 사용 함 
프로젝트 개요  
 - 목적 : 환자 별 MRI 이미지와 정보들을 이용해 건강 정보 예측 및 분류 
 - 데이터 : 각 환자 별 19장의 Brain MRI image와 환자 정보 데이터, 측정 건강 수치 
 - 분석 모델 
   - Input shape로 Mri images : 256,256,19 / 환자 정보 - 나이, 교육 년수 사용 
   - 256,256,19는 네트워크 내부에서 224,224,3 형태로 변형 되고 통해 Feature Extraction 진행 
   - Pretrained model은 Res50V2, VGG19, EFFicientnetV2S를 사용하며 각각 통과한 후 앙상블 됨 
   - Regression을 통해 건강 수치를 예측하고 예측된 값을 기준으로 정상 비정상 분류 

## 전해탈지 시계열 데이터의 이상 탐지 프로젝트 
세부 내용 : (https://github.com/crimama/Project_Anomaly_Detection)
주요 포인트 : 센서 데이터 이상 탐지 
프로젝트 개요 
  - 목적 : 전해탈지 공정 중 발생한 센서 데이터들을 이용해 제품의 품질을 조기 예측 및 이상 감지 
  - 데이터 : 전해탈지 공정 중 발생한 Current, Temperature, pH 데이터 
  - 분석 모델 
    - 센서가 감지한 데이터 뿐만 아니라 기준치(평균)에서 벗어난 정도, 편차를 변수로 사용 
    - 모델은 Isolation Forest 모델 사용 
  
## 농업 환경 변화에 따른 작물 병해 진단 AI 경진대회 
세부 내용 : (https://github.com/crimama/Dacon_LG_AI_Competition_2022)
주요 포인트 : 이미지 데이터와 시계열 데이터를 동시 사용하는 모델 개발 
프로젝트 개요  
  - 목적 : 농작물의 사진과 환경 데이터를 이용해서 농작물 이름 - 병충해 종류 - 병충해 정도를 예측
  - 데이터 : 농작물 사진, 이름, 병충해 종류, 병충해 정도, 사진 촬영 당시 과거 48시간 동안의 환경 데이터 
  - 분석 모델 
    - 농작물의 이미지는 Efficientnet b0, 환경 데이터는 2 Stacked Bidirectional LSTM을 사용한 Double head model 
 

## CNN 을 이용한 웨이퍼 불량 분류 
세부내용: (https://github.com/crimama/Wafer_Classification)
주요 포인트 : 논문 구현 시도 
프로젝트 개요
  - 목적 : Wafer Bin map 이미지를 이용해 웨이퍼의 불량 여부 및 불량 종류를 분류 
  - 데이터 : Kaggle에 공개 된 Wafer Bin map 이미지 
  - 분석 모델 
    - CNN을 사용하였으며 Class 수가 적은 특정 class를 Oversampling 해서 학습 진행 




