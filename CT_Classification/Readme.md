# CT 이미지와 환자의 정보를 이용한 환자 건강 정보 예측 및 분류 프로젝트

# **Reference - OCC**

# **작업일지**

## **22.02.12** 오늘자 최종 결과물 
- Ver 1 : 베이스라인 구축 
    - 저번 작업 내용 
      - 이미지 갯수 확인
      - 이미지 갯수 19장으로 통일 
      - 엑셀 값들 임베딩 
      - 초기 설정 함수들 Py로 모듈 화 
    - 오늘 작업 내용 
      - 11일에 작업하던 거 문제 생긴거 픽스  
      - 기본 전처리 - shape - model 까지 기본 Pipeline 구축 
      - 계획 초안 작성 - 프로젝트 FUll Plan
      - 관련 자료 조사 진행 

## **22.02.11** 오늘자 최종 결과물 : [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/crimama/DL_project/blob/main/CT_Classification/Daily_Code/22.02.11_1_초기작업.ipynb)

- Ver1 : Preprocessing 작업 진행 
    - 저번 작업 내용 
      - 이미지 directory 정제 해서 dir_df 에 정제 
      - key값들 모두 보정 및 snsb_df 과 통일 
      - 
    - 작업 내용 
      - 이미지 갯수 확인
      - 엑셀 값들 임베딩 (z score -1.0보다 작은 경우 비정상으로 처리) 
      - 초기 설정 함수들 Py로 모듈화 진행 
    - 결과
      - 이미지 갯수를 확인한 뒤 19장 보다 큰 경우 앞 뒤로 갯수 잘라서 19장으로 모두 맞춤 
      - 19장으로 한 이유는 20장인 경우가 가장 많았지만 데이터 증강을 할 수 없는 상황에서 19장을 포함하는 것이 가장 많은 데이터를 남길 수 있었음 
      - 19장보다 작은 경우는 우선은 제외 하고 진행 
    - 문제 사항 
      - 이미지 장수가 19장보다 작은 경우는 어떻게 처리 ? 
      - 추후 이미지 합치는 작업 진행 할 때 이 부분 다시 고민 
      - 우선은 19장 보다 작은 경우 제외하고 진행 
