# Contents Based Recommend System

* 컨텐츠가 비슷한 아이템을 추천한다.
* 사용자가 과거에 경험했던 아이템 중 비슷한 아이템을 현재 시점에 추천한다.
* Information Retrieval과 Machine Learning의 중간지점
  * 정보(아이템)을 찾는 과정과 과거 정보를 활용해서 유저의 성향을 배우는 문제
* Main Ieda
  * 유저 A가 높은 평점을 주거나 큰 관심을 갖은 아이템 x와 유사한 아이템 y를 추천
* 예시
  1. 웹사이트, 블로그, 뉴스: 비슷한 컨텐츠의 게시글(item)을 찾아서 추천
  2. 영화: 같은 배우, 같은 장르, 같은 영화 감독 등 비슷한 특징을 갖는 영화(item)을 찾아서 추천



### Recommend Flow

1. 유저가 과거에 접한 아이템이면서 만족한 아이템
2. 유저가 좋아했던 아이템 중 일부 또는 전체와 비슷한 아이템 선정
3. 선정된 아이템을 유저에게 추천



### 장점

1. 다른 유저의 데이터가 필요하지 않다.
2. 추천할 수 있는 아이템의 범위가 넓다.
   * Unique, New, Unpopular 아이템 모두 가능
3. 추천하는 이유를 제시할 수 있다.
   * 아이템의 features로 컨텐츠 분석 가능
   * 특정 feature가 추천의 이유가 됐다고 설명 가능

### 단점

1. 적절한 features를 찾기가 어렵다.
   * 영화, 사진, 음악, 뉴스(텍스트) 등
2. 새로운 유저를 위한 추천이 어렵다.
   * User Profile이 존재하지 않거나 데이터가 매우 부족하다.
3. 선호하는 특성을 가진 항목을 반복 추천한다.
   * Overspecialization
   * 유저의 다양한 취향 반영 어려움
   * 유저 프로필 외 추천 불가



## 컨텐츠 기반 추천 시스템 Architecture

1. 정보(유저, 아이템) 제공
2. 컨텐츠 분석(Contents Analyzer)
   * 텍스트와 같은 비정형 데이터로부터 관련 있는 정보를 얻는 작업 - feature extraction, vector representation
3. 유저 프로필 파악 (Profile Learner)
   * 유저가 선호하는 아이템, 취향 파악
   * 머신러닝 등 알고리즘을 통해 유저 데이터 일반화
4. 유사 아이템 선택 (Filtering Component)
   * 아이템 중 가장 적절하게 match하는 아이템 선택
   * 관련있는 아이템으로 최종 추천 리스트 만들기
5. 추천 리스트 생성



### 컨텐츠 기반 추천 시스템에서 가장 중요한 것!

* ​	컨텐츠의 내용을 분석하는 **아이템 분석 알고리즘**

  * Clustering, Machine Learning, TF-IDF 등 활용

* 추천 시스템의 성능을 높일 수 있는 **적절한 컨텐츠를 사용**하는 것

  * 영화 추천을 위해 영화 정보를 활용하고, 뉴스 추천을 위해 뉴스 내용을 활용하는 것

    