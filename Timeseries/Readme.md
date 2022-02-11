# TimeSeries 프로젝트 

# **Reference - OCC**
- https://arxiv.org/pdf/2101.03064.pdf

# **작업일지**

## **22.02.11** 오늘자 최종 결과물 : [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/crimama/DL_project/blob/main/Timeseries/22.02.11_2_전해탈지_시간작업_CM.ipynb)

- Ver1 : Preprocessing 작업 진행 
    - 작업 내용 
      - 기존에 사용하던 변수 대신 평균값 간의 편차를 이용
      - 도메인 써칭 통해서 Target Setting 값과의 차이가 커질 수록 이상 발생 확률이 커짐 
    - 결과
      - 정상데이터들의 Max Softmax Score 분포가 좁혀짐 
      - 이상 데이터 한개 탐지 성공 함+
      - precision = 0.06666666666666667
      - recall = 0.25
- Ver2 : 시간 데이터 작업
    - 작업 내용 
      - 한 Lot의 전해 탈지 걸리는 시간을 변수로 사용 
    - 결과
      - 거의 대부분 동일한 340 이거나 몇개는 341, 하지만 341이 이상 Lot는 아니었음
      - 폐기 
- Ver3 : Valid 비율 조절 
    - 작업 내용 
      - 기존에 450 : 100 : 226 비율 -> 350 : 200 : 226 비율로 진행 
    - 결과
      - valid 비중이 커지는 바람에 train - valid 모두한테 overfitting 이 발생하지만 2개 탐지할 수 있었음 
      - precision = 0.18181818181818182
      - recall = 0.5
