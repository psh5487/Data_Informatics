# Data_Informatics
2019.1.17 데이터 분석 해결 교내 Informatics Camp

4Wheel팀 : 박소현, 양진혁, 박희강

## 문제
1. 고객만족도조사 데이터를 활용하여 (1)S그룹 점포 상태를 분석하고, (2)점포 재방문율을 높이는 전략을 수학적 or 그래픽 모형을 제시할 것
- 고객 만족도 조사 항목 : 매장 분위기 / 제품 구색 / 동선 편리성 / 서비스 품질 / 직원 응대 태도 / 재방문 의도

2. 2019년도 문재인 대통령 취임사를 (1)텍스트 마이닝 기법을 활용해 분석하고, (2)시사점을 찾아서 제시할 것

## 1.1. 점포 상태 분석
### 평균 및 점수 카운팅
- 각 항목별 평균을 계산하여 각 항목에 대한 전체적인 만족도 확인
<img width="667" src="https://user-images.githubusercontent.com/26567880/91650789-ef6ff880-eabe-11ea-85e6-601501c9ade0.png">

- 재방문의도에 대해 각 점수가 나온 횟수를 카운팅하여 전체적인 만족도 확인
<img width="741" src="https://user-images.githubusercontent.com/26567880/91650868-167afa00-eac0-11ea-93a3-3ce448d07112.png">

### 공분산 분석
- 각 평가 항목에 대한 공분산을 계산하여 전체적인 만족도 확인
<img width="926" src="https://user-images.githubusercontent.com/26567880/91650882-4a561f80-eac0-11ea-8aac-b2ba662d6516.png">

### 상관관계 분석
- 매장분위기/서비스품질/동선편리성/제품다양성/직원응대태도 모두 재방문의도와 양의 상관 관계
<img width="960" src="https://user-images.githubusercontent.com/26567880/91650909-c2bce080-eac0-11ea-83a3-9ce6608892ea.png">

### Decision Tree
- 결정 트리(decision tree) : 의사 결정 규칙과 그 결과들을 트리 구조로 도식화한 의사 결정 지원 도구의 일종
- 정보 엔트로피를 이용하여 불순도를 측정하고, 불순도를 최대한 줄이는 인자를 찾아 분류한다. 결과 도출의 과정을 쉽게 디버깅할 수 있어 유용하다.
<img width="279" alt="트리" src="https://user-images.githubusercontent.com/26567880/91650978-b5ecbc80-eac1-11ea-9111-e2e0ac7bc1cc.png">
<img width="853" alt="결정트리" src="https://user-images.githubusercontent.com/26567880/91650985-c43ad880-eac1-11ea-875c-0ee1975d169c.png">
<img width="500" alt="결정트리2" src="https://user-images.githubusercontent.com/26567880/91650990-d157c780-eac1-11ea-81e2-60830faed71b.png">

- '서비스 점수'가 가장 큰 요인으로 작용한다. 서비스 점수가 높으면 대부분이 높은 점수이다.
- 서비스 점수가 낮으면 '분위기'가 다음으로 중요한 요인으로 작용한다.
- Decision Tree 구축 이후 데이터베이스 외의 값도 예측이 가능하다.

### k-NN Algorithm
- k-최근접 이웃 알고리즘(k-Nearest Neighbor Algorithm)은 데이터로부터 가장 가까운 k개의 데이터를 추출한 뒤, 더 비중이 높은 결과값을 선정하여 예측하는 알고리즘이다.
- 다량의 데이터 집합에 대해서도 kNN 계산이 가능하며, 구현이 쉽다.
- 일관적이지 않은 복합적인 모델에 대해서는 적합하지 않다.
<img width="425" alt="knn" src="https://user-images.githubusercontent.com/26567880/91651094-13353d80-eac3-11ea-8b16-4dda1af8d33d.png">

## 1.2. 재방문율을 높이는 모델

### 재방문율을 높이기 전략
- 재방문율을 판단하는데 가장 중요하게 작용한 요인은 '서비스 -> 분위기 -> 편리성' 순서
- '직원의 응대 태도'는 다른 요인에 비해 적게 작용함
- 서비스를 좋지 못하다 판단한 고객의 경우 '매장 분위기'로 높은 재방문율을 가짐 
- 즉, 서비스와 매장의 분위기를 중점적으로 신경 쓴다면 재방문율이 증가할 것이라 판단

### 예측 모델 비교
- kNN과 결정트리 기법을 사용하여 모델 예측을 한 결과, 약 35%의 비율로 동일한 결과를 도출함
- kNN의 경우, 자신과 비슷한 사람을 찾아나가 예측하는 방식
- 결정트리 기법은 전체적인 경향성을 분석하는 방식
- 두 기법 모두 일리 있는 예측 모델이지만, 서로 다른 결과값을 도출해낸다는 점이 흥미로웠음

### 아쉬운 점
- 모든 인자에 대한 공분산 값이 높다. 다양한 데이터 셋이 주어지지 않아 분석 요인이 적었음
- 데이터가 너무 적었다. 예측 모델의 신뢰도가 많이 떨어질 수 있음


## 2. 신년사 텍스트마이이닝
### konlypy 모듈 사용
- 단어 분리
<img width="112" alt="단어분석" src="https://user-images.githubusercontent.com/26567880/91650527-c863f780-eabb-11ea-928c-8586bd5ef39f.png">

### 1차 plotting
- 자주 나오는 단어 plotting. 불필요한 단어 많음
<img width="592" src="https://user-images.githubusercontent.com/26567880/91650591-753e7480-eabc-11ea-953b-1c4513407627.png">

### 2차 plotting
- 어미, 조사 등 불필요한 단어 제거
- stop_word 사용
<img width="600" alt="2플롯팅" src="https://user-images.githubusercontent.com/26567880/91650617-b6368900-eabc-11ea-8985-d9b215409c35.png">

### Lexical Dispersion plot
- 키워드 사용 위치 파악
<img width="638" alt="키워드위치" src="https://user-images.githubusercontent.com/26567880/91650627-dc5c2900-eabc-11ea-982e-27d9642b2f6b.png">

### '평화' 단어 사용 문맥 파악
- 안보, 한반도, 전쟁, 비핵화, 올림픽 등의 단어와 함께 사용됨
- concordance 명령어 사용
<img width="649" alt="문맥" src="https://user-images.githubusercontent.com/26567880/91650658-2b09c300-eabd-11ea-86d4-c0adcd660583.png">

### wordcloud 만들기1-2018년도 신년사
- 2018 문재인 정부의 방향 : 촛불, 정부의 안정화, 한반도 평화, 일자리, 지원
<img width="388" alt="2018 wordcloud" src="https://user-images.githubusercontent.com/26567880/91650675-820f9800-eabd-11ea-81a4-fa8edeaf35bb.png">

### wordcloud 만들기2-2019년도 신년사
- 2019 문재인 정부의 방향 : 경제, 평화, 기업, 성장, 혁신 
- 경제 안정화
<img width="378" alt="2019 wordcloud" src="https://user-images.githubusercontent.com/26567880/91650677-8b006980-eabd-11ea-8777-3be666dd58e4.png">

### 인공지능 문장 생성
- 완성도는 떨어지지만, 신년사를 바탕으로 문장 생성하기를 시도해 봄
<img width="636" alt="인공" src="https://user-images.githubusercontent.com/26567880/91650718-124ddd00-eabe-11ea-9de8-e8bfe0ecde7a.png">

## 수상
- 3위
<img width="675" alt="수상 결과" src="https://user-images.githubusercontent.com/26567880/91651207-d0746500-eac4-11ea-8f6e-2151149f9acf.png">


