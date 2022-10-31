# Recommender System

## 추천 시스템이란?

* 사용자  (User)와 상품 (Item)으로 구성된 시스템
* 특정 사용자(User)가 좋아할 상품(Item)을 추천
* 비슷한 상품(Item)을 좋아할 사용자(User)추천
* Item이든 User든 관심 갖을만한 정보를 추천



## 사용자 (User)와 상품(Item)

* 사용자와 아이템 사이의 관계를 분석하고 연관관계를 찾는다.
* 해당 연관 관계를 점수화 한다.
* 사용자의 정보와 아이템의 정보를 활용한다.

**사용자 정보**

* 사용자 고유 정보 (나이, 성별, 지역 등)
* 사용자 로그 분석 (행동 패턴 등)

**아이템 정보** 

* 사용자 고유 정보 (가격, 색상, 내용 등)



**사용자 프로필**

* 사용자 or 사용자 그룹을 분석 가능한 요소로 프로파일링(profiling)
* 사용자를 구분할 수 있는 정보를 활용
  * 사용자 ID: 나이, 성별, 지역, 학력 등 개인 신상정보
  * 쿠키 (cookie)
  * 인터넷 주소
  * 웹 페이지 방문 기록, 클릭 패턴 등 사용자 행동 정보
* 사용자 정보를 수집하기 위한 방법
  * 직접적인(Explicit) 방법: 설문조사, 평가, 피드백 등
  * 간접적인(Implicit) 방법: 웹페이지 머무르는 시간, 클릭 패턴, 검색 로그 등
* 개인별 추천 or 사용자 그룹별 추천 기능



 **아이템 프로필**

* 플랫폼마다 정의하는 아이템의 종류가 다르다.
* 일반적으로 생각해볼 수 있는 추천 아이템 예시
  * 책, 전자제품, 옷 등 웹사이트 내 웹 페이지
  * SNS에서 비슷한 게시글, 관심 있을만한 사진
  * 뉴스, 논문 등 문서
  * 여행지, 음식점 등 지역 또는 장소 정보
  * 영화, 음악, 동영상, TV 프로그램 등 다양한 영상
* 모든 것을 추천해주는 플랫폼은 현재 없다
* 플랫폼마다 관련 있는 상품 또는 아이템만 추천한다
* 아이템 프로필에 속하는 정보
  * 아이템 ID, 아이템 고유 정보(크기, 색, 가격 등), 아이템을 좋아하거나 구매한 사용자 정보 등



##  추천 점수란?

* 분석된 사용자와 아이템 정보를 바탕으로 추천 점수 계산



## 추천 시스템 연구 현황

* 정보 검색(Information Retrieval) 분야와 비슷하지만, 비교적 새로운 연구 분야
* 최근 다양한 형태의 추천시스템 연구 진행중(~ing)
* 여러 기업과 학회에서 다양하게 연구 진행중(~ing)
  * SIGIR, WWW, ACM RecSys, IEEE
* Netflix Prize 추천 대회



## 추천 시스템: 데이터 종류

### Items

* 추천할 항목
* 가치와 데이터의 복잡함에 따라 구분할 수 있다.
* Low: 뉴스, 책, 영화 등
* High: 금융 상품, 직업, 여행 등

### Users

* 여러 목적과 특징을 갖는 집단
* 행동 패턴 등으로 유저 모델링
* 협업 필터링: 여러 아이템에 대한 평점 리스트
* 사회적인 요인을 활용한 추천 시스템

### Transactions

* 유저와 아이템 간의 상호 작용
* 유저가 인터넷에 남긴 로그에서 중요한 정보 추출
* 해시태그, 평점, Implicit,한 정보 모두 활용 가능



## 추천 시스템이 풀고자 하는 문제

### 1. 랭킹 문제

* 특정 유저가 특정 아이템에 대한 평점(or 점수)을 정확하게 예측할 필요 없음

### 2. 예측 문제

* 유저-아이템 조합에서 평점(or 점수)를 예측
* 유저-아이템 행렬을 채우는 문제
* 유저(m명)-아이템(n개)의 m X n 행렬, 그러나 비어있는 부분 존재
  * 관측값은 모델 학습에 사용
  * 결측값은 모델 평가에 사용



## 추천 시스템과 추천 알고리즘

![image-20221027092714237](C:\Users\SSAFY\Desktop\assets\image-20221027092714237.png)

### Contents-based Recommender System(컨텐츠 기반 추천 시스템)

* 사용자가 과거에 좋아했던 아이템을 파악하고, 그 아이템과 비슷한 아이템을 추천
* ex) 스파이더맨에 4.5 평점을 부여한 유저는 -> 타이타닉보다 캡틴 마블을 좋아할 것이다.

1. 유저가 과거에 접한 아이템이면서 만족한 아이템
2. 유저가 좋아한 아이템 중 일부 또는 전체와 비슷한 아이템 선정
3. 선정된 아이템을 유저에게 추천



### Collaborative Filterling(협업 필터링)

* 비슷한 성향 또는 취향을 갖는 다른 유저가 좋아한 아이템을 현재 유저에게 추천
* 간단하면서 수준 높은 정확도를 나타낸다

1. 유저 A와 유저 B 모두 같은 아이템에 대해 비슷한 또는 같은 평가를 했다.
2. 이 때, 유저 A는 다른 아이템에도 비슷한 호감을 나타냈다
3. 따라서 유저 A, B의 성향은 비슷할 것이므로 다른 아이템을 유저 B에게 추천한다.

### Hybrid Recommender System

* Content-based와 Collaborative Filtering의 장, 단점을 상호 보완
* Collaborative Filtering은 새로운 아이템에 대한 추천 부족
* 이에, content-based 기법이 **cold-start 문제**에 도움을 줄 수 있음

### Other Recommendation Algorithms

#### 1. Context-based Recommendation

* Context-aware Recommendation System
* Localtion-based Recommendation System
* Real-time or Time-Sensitive Recommendation System

#### 2. Community-based Recommendation

* 사용자의 친구 또는 속한 커뮤니티의 선호도를 바탕으로 추천
* SNS 등의 뉴스 피트 또는 SNS 네트워크 데이터 등 활용

####  3. Knowledge-based Recommendation

* 특정 도메인 지식을 바탕으로 아이템의 features를 활용한 추천

* Case-based Recommendation

  * 사용자의 니즈 (현재 문제 등)와 해결책 중 가장 적합한 것을 골라서 추천

* Constraint-based Recommendation

  * 사용자에게 추천할 때, 정해진 규칙을 바탕으로 추천

    

![image-20221027093952766](C:\Users\SSAFY\Desktop\assets\image-20221027093952766.png)





## 추천 시스템의 한계

### Scalability

* 실제 서비스 상황은 다양한 종류의 데이터
* 학습 또는 분석에 사용한 데이터와는 전혀 다른 실전 데이터

### Proactive Recommender System

* 특별한 요청이 없어도 사전에 먼저 제공하는 추천 서비스
* 모바일, 인터넷 등 어디서든 유저에게 끊임없이 좋은 정보를 추천할 수 있는 서비스

### Cold-Start Problem

* 추천 서비스를 위한 데이터 부족
* 기본적인 성능을 보장하는 협업필터링 모델 구축이 쉽지 않은 것이 일반적
* 컨텐츠 기반 또는 지식 기반의 방법 역시 서비스로 적용하기 어려움

### Privacy preserving Recommneder System

* 개인정보 등 유저 정보가 가장 중요하지만, 직접적으로 사용하기가 어려움

### Mobile device and Usage Contexts

* Peronal Computing, Location-based Service(LBS)
* 개별 상황 또는 환경 등에 따라 다른 컨텍스트를 사용

### Long-term and Short-term user perference

* 개인 또는 그룹의 단기/장기 관심사항
* 추천받고 싶은 아이템이 현재 또는 과거 중 어느 시기와 관련 있는지 파악하기 어려움

### Generic User models and Cross Domain Recommender System

* 하나의 모델을 여러가지 데이터에 적용하기 어려움
* 비슷한 도메인의 데이터를 활용해도 동일한 성능의 추천 시스템을 기대하기 어려움

### Starvation and Diversity

* Starvation: 필요한 컴퓨터 자원을 끊임없이 가져오지 못하는 상황
* 유저/아이템이 다양하고, 모든 유저/아이템에 더 많은 관심을 부여해야함