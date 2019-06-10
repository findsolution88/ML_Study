# 뉴스 자동분류 및 대표기사 추출 서비스
멀티캠퍼스 '딥러닝 기반 빅데이터 예측모델 분석 전문가'과정 실무 프로젝트
<img  src="https://github.com/findsolution88/ML_Study/blob/master/%EB%A9%80%ED%8B%B0%EC%BA%A0%ED%8D%BC%EC%8A%A4%20%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8/4_web/capture/%EC%88%98%EC%83%81.jpg" width="500", hight=350">
<br><br>
## 프로젝트 목표
1. 기업에 대해 검색된 기사에서 기업의 카테고리별 대표 이슈들을 추출하고,
2. 시간순으로 이슈에 대한 대표 키워드를 시각화 하며,
3. 각 이슈에 대한 대표 기사를 추천하는 기능을 구현한다.
<br><br>
## 구현 프로세스
사용 TOOL
- python (jupyter notebook, pycharm)
- SQLite
- Django
#### 1. 데이터 수집
한국언론 진흥재단의 빅카인즈 api를 통해 기사 제목, 본문, 카테고리, 날짜 등을 수집
- 검색어: 미래에셋 대우, 삼성전자, SK, 쏘카, 카카오 등
- 데이커 크기: 검색어 당 10,000건
#### 2. 데이터 전처리
Konlpy패키지를 통한 명사 추출, 불용어 처리 및 단어 사전 구축
#### 3. 유효문서 추출
검색어와 상관 없는 기사를 필터링 하기 위해 제목에 해당 검색어가 포함되며, 본문에 검색어가 3회 이상 포함되는 기사로 추출
#### 4. 카테고리 할당
한국언론진흥재단에서 지정한 뉴스 통합 분류체계 값인 ‘정치‘, ‘사회’, ‘경제’ 등을 활용
#### 5. 토픽 할당
토픽은 카테고리 하위 개념을 말한다. 예를들어 ‘문재인’으로 검색한 ‘정치’라는 카테고리에 ‘남북 정상회담’, ‘패스트트랙 법안 상정’ 등을 토픽이라 칭함
- DBSCAN의 OPTICS
비지도로 토픽을 정하는 프로세스에서 OPTICS를 사용한 이유는 다음과 같다.
1. 군집수를 정할 필요가 없다. 
2. 밀도가 다른 군집이 있을 때, 각 군집의 맞는 밀도를 고려할 수 있다.
#### 6. 대표문서 추출
오픈소스 검색엔진 엘라스틱서치(Elastic Search)의 검색 알고리즘 BM25를 사용
- BM25는 문서 Scoring 방법 중 하나로, 키워드와 문서의 상관성을 계산해 점수를 산출. 토픽 키워드에 대해 BM25 점수가 가장 높은 문서를 대표문서로 선정하는 방식

## 웹 어플리케이션 구현
Django를 통한 웹페이지를 구현하였으며 주요 화면은 다음과 같다.
<img  src="https://github.com/findsolution88/ML_Study/blob/master/%EB%A9%80%ED%8B%B0%EC%BA%A0%ED%8D%BC%EC%8A%A4%20%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8/4_web/capture/1.PNG">
<img  src="https://github.com/findsolution88/ML_Study/blob/master/%EB%A9%80%ED%8B%B0%EC%BA%A0%ED%8D%BC%EC%8A%A4%20%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8/4_web/capture/2.PNG">
<img  src="https://github.com/findsolution88/ML_Study/blob/master/%EB%A9%80%ED%8B%B0%EC%BA%A0%ED%8D%BC%EC%8A%A4%20%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8/4_web/capture/3.PNG">
<img  src="https://github.com/findsolution88/ML_Study/blob/master/%EB%A9%80%ED%8B%B0%EC%BA%A0%ED%8D%BC%EC%8A%A4%20%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8/4_web/capture/4.PNG">
