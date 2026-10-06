# delivery-time-prediction

Kaggle [Amazon Delivery Dataset](https://www.kaggle.com/datasets/sujalsuthar/amazon-delivery-dataset)으로
배달 소요 시간(분)을 예측하는 머신러닝 회귀 실습이에요. (인공지능개론)

## 문제 정의

| 질문 | 답 |
|---|---|
| 입력(X) | 배달원 나이·평점, 가게↔배달지 거리(좌표로 계산), 주문 시각·요일, 픽업 대기 시간, 날씨, 교통, 이동수단, 지역, 상품 카테고리 |
| 목표(Y) | `Delivery_Time` (분) |
| 문제 유형 | 회귀 (Regression) |
| 학습 목표 | 거리·교통·날씨·배달원 상태 등과 배달 시간 사이의 관계를 학습해 새 주문의 소요 시간을 예측 |
| 예상 문제점 | 결측치(`Agent_Rating`, `Weather` 등), 좌표 이상치, 시간 형식, 범주형 인코딩, 스케일 차이, 데이터 누수, 데이터에 없는 요인(조리 시간 등) |

## 폴더 구조

```
.
├── data/                  # amazon_delivery.csv 를 여기에 넣어요 (Git에는 올리지 않음)
├── notebooks/
│   └── delivery_time_prediction.ipynb
├── requirements.txt
└── README.md
```

## 실행 방법

1. 의존성 설치

   ```bash
   python -m venv .venv
   source .venv/bin/activate        # Windows: .venv\Scripts\activate
   pip install -r requirements.txt
   ```

2. Kaggle에서 `amazon_delivery.csv`를 내려받아 `data/` 폴더에 넣어요.
3. `jupyter lab` 실행 후 `notebooks/delivery_time_prediction.ipynb`를 위에서부터 실행해요.

## 노트북 구성

1. 데이터 불러오기와 첫 확인 (결측, 중복, 범주 값)
2. 목표 변수 분포
3. 정제와 파생변수 (문자열 정리, 하버사인 거리, 시간 파생)
4. EDA (범주별 박스플롯, 거리-시간 산점도, 상관관계)
5. 학습/테스트 분할 (전처리 전에 분할해서 데이터 누수 방지)
6. 전처리 파이프라인과 모델 비교 (평균 기준선, 선형회귀, 랜덤포레스트, HistGradientBoosting)
7. 결과 해석 (실제 vs 예측, 잔차, permutation importance)
8. 정리 (직접 채워 보기)

## 참고

- 저장소의 노트북은 **실행 결과가 비어 있는 상태**예요. 직접 실행해서 결과를 확인하세요.
- 이상 거리 기준(`MAX_DISTANCE_KM`)이나 픽업 대기 시간 상한(180분)은 임의로 정한 값이에요.
  실제 데이터 분포를 보고 조정하세요.
- 결과표는 아직 없어요. 실제 데이터로 실행한 뒤 이 README에 정리할 예정이에요.
