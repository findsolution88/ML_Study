# Kaggle Study
## 주제: Allstate Claims Severity
https://www.kaggle.com/c/allstate-claims-severity<br>
Allstate사의 보험금 청구비용(loss) 예측 모델을 구축한다.

## 데이터 설명
미국의 개인 보험 회사 Allstate 계약(id)별 보험금 청구액(loss)관련 자료이다.<br>
### 독립변수
컬럼명 cat1,2,3... cont1,2,3... 은 아래와 같이 의미한다.<br>
'cat' - categorical(명목형 변수 116개) <br>
'cont' - continuous (연속형 변수 14개)<br>

cat 데이터는 A,B,C...., LB,DC,CQ...등 유형을 나타내도록 변환되었고, cont 데이터는 0~1 소숫점으로 변환되어 주어진 상태이다.<br>
### 종속변수
보험금 청구액(loss)이며 $단위이다.

## 분석 방법
### 'cat' 변수 
t-test 및 Anova분석을 통해 해당 변수와 loss의 유의미한 차이가 있는지 검정후,
One-Hot-Encoding을 통해 더비변수로 변환
### 'cont'변수
선형회귀의 t-test(p-value)를 통해 변수의 유의성을 검정하고, VIF를 통해 다중공선성을 검정
### 인공신경망 모델
Keras를 통해\allstate_score.png 인공신경망을 구축하였으며 모델에 사용한 인자는 다음과 같다.
활성함수로 'relu', 'linear'를 사용하였고, Optimizer로는 'Adam'을 사용하였다.

## 최종 Score
Private Leaderboard기준 1등은 1109.70772점이며, 
본인의 최종 Score는 1165.02314이다.
<img src="C:\Users\smnoh\Desktop\git\ML_Study\kaggle study\kaggle_allstate-predict\allstate_score.png">
