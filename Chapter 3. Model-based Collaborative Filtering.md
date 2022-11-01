# Chapter 3. Model-based Collaborative Filtering



## 1. Nearest Neighbor vs Model-based

## What is Model-based?

* 머신러닝 (and 특징)을 가장 잘 활용한 추천 알고리즘의 일종
* 주어진 데이터를 활용하여 모델 학습
  * 학습 과정(Training)에서 모델이 데이터를 배워서 데이터 정보를 압축한다.
* 항목간 유사성에서 벗어나, 데이터의 패턴을 학습
* 데이터 크기 or 데이터의 특징 (feature)을 동적으로 활용 가능하다.
* 데이터(유저)의 잠재적 특성(선호하는 취향)을 파악하는 모델 (Latent Factor Model)

### Advantages

* 추천 모델(알고리즘)의 크기
  * 수많은 데이털 구성된 행렬(ex. Rating matrix)보다 압축된 형태로 저장
  
* 추천 모델(알고리즘)의 학습과 예측 속도
  * 데이터 전처리와 학습 과정으로 미리 모델 준비 -> 준비된 모델로 예측
  
* 추천 모델(알고리즘)의 과적합 방지
  * 데이터를 다양하게 학습할 수 있으며, 새로운 추천을 할 가능성이 있다.

* Sparse data
  * 유저- 아이템 간 데이터 중 사용 가능한 데이터는 전체 데이터 중 비율이 작다.
  * 유저 - 아이템 간 데이터에서 표시되지 않은 항목은 새로운 추천을 하기 어렵다(Cold-start)
  
* Limited Coverage

  * 공통의 유저 또는 아이템이 선택된 데이터를 확보하기 어렵다.

  * 이웃 기반 협업 필터링의 특성 중 '이웃'의 효과를 보기 어렵다.

    

### Types

* Association Rule Mining
* Matrix Factorization
  * SVD(Singular Value  Decomposition), ALS(Alternating Least Square)
* Probabilistic Models
  * Clustering, Bayes Rules
* Etc.
  * SVM, Regression methods(Logistic Regression), Deep Learning

![image-20221101161807263](C:\Users\SSAFY\Desktop\recommend\assets\image-20221101161807263.png)

Sparse Matrix를 채워서 Dense Matrix로 만드는 과정



## 2. Rule-based Collaborative Filtering

### 상호 연관관계

* 데이터 속에서 상호 연관관계를 찾을 수 있다.

### Association Rule

* 데이터의 모델
  * 데이터의 **관계, 접근과 흐름 파악**을 위한 추상화된 모형
  * 데이터 구조 결정
* **데이터의 여러 특징을 파악해서 모형화 -> 모델**
* 데이터 간의 연관 법칙을 찾는 data mining 기법 중 하나.
* 기존 데이터를 기반으로 Association Rule(연관 규칙)을 만든다.



#### 정의

* Minimum **Support**와 Minimum **Confidence** 값은 넘는 Rule을 찾는 과정

* 데이터에서 흥미로운 관계를 찾는 Rule-based Machine Learning 기법 중 하나

* 특정 measure를 통해 interestingness를 평가 하여 Strong Rules를 찾는 과정

  

#### Support (지지도) 

$support(A \to B) = {Number\ of\ (A\cup B) \over Number \ of \ data(rows)}$

* 데이터 관계 설정을 위해 **아이템이 동시에 발생할 확률**
* 전체 데이터 중 규칙(A, B)를 포함하는 데이터 비율
* 0 to 1, 1: 항상 발생, 0: 발생 x
* $support(A\to B)$와 $support(B\to A)$ 의 차이점 파악이 불가능하다.



#### Confidence(신뢰도)

$confidence(A \to B) = {Number\ of\ (A\cup B) \over Number\ of\  A}$

* 특정 아이템 A가 선택된 상태에서 다른 아이템 B를 선택할 확률
* (A, B)의 관계를 가정하고, A를 선택한 사람이 B를 선택한 확률
* 0 to 1, 1에 가까울 수록 A는 B에 많은 영향을 준다 -> minimum support 중 가장 큰 confidence를 선택한다.
* $support(A\to B)$와 $support(B\to A)$  와 다르게 인과관계 파악이 가능하다.



#### Lift (향상도)

$lift(A\to B) = {confidence(A\to B) \over support(B)} = {Number\ of\ (A\cup B) \over Number\ of \ A}$

* (A, B)의 관계를 직접적으로 나타내는 measurement

  * $lift(A\to B) <\ 1 :$ 상호 대체 -> A와 B는 반비례
  * $lift(A\to B) >\ 1 :$ 상호 보완 -> A와 B는 정비례
  * $lift(A\to B) =\ 1 :$ 독립 -> A와 B는 서로에게 영향을 미치지 않는다.
* 1보다 크면, 이어서 B를 선택할 확률이 높고, 1보다 작다면 확률이 높지 않다.

  

#### More on Association Rule Mining

* Brute Force
  * 모든 아이템에 대한 연관관계를 하나씩 전부 평가한다.
  * Minimum Support Threshold, Minimum Confidence Threshold
* Frequent Itemset Generation
  * 빈도수가 높은 관계 위주로 후보군을 축소하여 Rule Mining을 진행한다.
  * Apriori Principle: 데이터 발생 빈도를 바탕으로 데이터 간의 연관관계 파악에 사용된다.
* User-based CF & Item-based CF -> Rule-based로 생각해 볼 수 있다.
* 이산형 변수로 데이터 profile을 통해 association rule을 적용할 수 있다.
  * Profile Association Rule



## 3. Latent Factor Model & Matrix Factorization

### Latent Factor Model (잠재된 요소)

* 사용자/아이템 특성을 벡터로 간략화(요약)하는 모델링 (\주성분 분석)
* 사용자/아이템 특성 간 복잡한 관계를 학습한다.
* 사용자/아이템 행렬에서 사용자와 아이템을 Factor로 나타내는 방법
* 사용자와 아이템이 같은 vector 공간에 표현된다.
* 사용자와 아이템을 모르는 차원(dimension)에 표현하고, 몇개의 차원인지 모른다.
* 같은 vector 공간에서 사용자와 아이템이 가까우면 유사, 멀리 떨어져 있으면 유사하지 않음.



### Singular Value Decomposition

$ A\ =\ U\Sigma V^T$

* U는 고유값 분해로 얻은 m X m 직교 행렬
  * $AA^T\ =\ U(\Sigma\Sigma^T)U^T$
  * U의 열벡터는 A의 left singular vector

* V는 고유값 분해로 얻은 n X n 직교 행렬
  * $A^TA = V(\Sigma^T\Sigma)V^T$
  * V의 열벡터는 A의 right singular vector
* $\Sigma$ 는 m X n  대각 행렬
  * 고유값분해해서 나온 eigenvalue의 제곱근이 대각원소
  * 대각 원소 = A의 특이값

* 차원 축소 기법 (Dimensionality Reduction) 중 하나
  * 참고: PCA(Principal Component Analysis, 주성분 분석)

* 사용자와 아이템간 데이터를 행렬 R로 나타낸다.
* 행렬 U는 사용자와 latent factor, V는 아이템과 latent factor

* 행렬 U와 V의 모든 열벡터는 특이벡터(Singular vector), 모든 특이벡터는 서로 직교한다.
* $U^TU\ =\ I,\ V^TV = I$
* 행렬 $\Sigma$의 대각 성분은 M의 특이값
* 사용자와 아이템의 관계를 2차원 직교좌표계로 표현한다.
  * 사용자와 아이템의 고유값 계산 -> 고유값으로 기존 평점 데이터 다시 계산한다.

#### 왜 SVD를 사용하는가?

* 데이터 차원 축소
  * 노이즈 제거, Sparse matrix 형태로 큰 데이터 축소
* 행렬 U는 User와 latent factor간의 관계
* 행렬 V는 Item과 latent factor간의 관계
* 행렬 $\Sigma$는 대각행렬로, latent factor의 중요도
* Latent factor는 user와 item이 공통으로 갖는 특징

* 단, latent factor의 뜻을 이해하기 어렵기 때문에 추천에 대한 구체적인 설명이 어렵다.



### Matrix Factorization

* Latent Factor Model을 구현하는 방법
* Rating Matrix를 분해하는 과정
* $|U| \times |I| : $ user-item rating matrix($rank\ k < n$)
* $P \to |U| \times k :$ matrix of user factors
* $Q \to |I| \times k :$ matrix of item factors



* 분해한 행렬 X와 Y를 곱하여 평점을 예측
*  임의의 차원수 f는 직접 정한다.

* $\hat{r_{ui}} = x_u^T \times y_i$
* R(원래 rating matrix)과 R'(예측 matrix)이 서로 유사하도록 학습하는 과정이다.

#### More on Matrix Factorization

* Matrix Completion 문제 
* Other SVD
  * SVD++, thin SVD, compact SVD, truncated SVD, etc
* Loss Function
  * Latent factor(feature)를 학습한다.
*  Optimization
  * (Stochastic) Gradient Descent, Alternating Least Squares



## 4. Matrix Factorization  by SGD, ALS

* R(원래 rating matrix)과 R'(예측 matrix)이 서로 유사하도록 학습하는 과정이다.
* (true rating - predicted rating)으로 근사값을 추론하는 문제
  * $\hat{r_{ui}} = x_u^T \times y_i$
* predicted rating을 이용한 matrix completion 문제
* (Stochastic) Gradient Descent (경사 하강법), Alternating Least Squares 등을 사용
  * Loss function 최적화를 위해 사용
* 정보를 추가하여 모델링 할 수 있다.
  * Explicit과 Implicit feedback을 Matrix Factorization에 녹여낸다.

### Objective Function(목적 함수)

$min \sum_(u, i)\in T (r_{ui} - x_u^Ty_i)^2 + \lambda(||x_u||^2 + ||y_i||^2)$

* $x_u, y_i$ : user와 item latent vector
* $r_{ui}$ : user u가 item i에 부여한 실제 rating 값
* $\hat{r_{ui}}$ = $x_u^T y_i$ : user u가 item i에 대해서 줄 예측 rating 값
* $\lambda(||x_u||^2 + ||y_i||^2)$ : 정규화
  * 제한적인 학습데이터에 의존하는 Overfitting을 방지하기 위해 error term



### Optimization

#### Stochastic Gradient Descent (경사 하강법)

* 학습 데이터의 모든 rating을 다 훑는 다
* Error term
  * 실제 평점(true rating)과 예측 평점(predicted rating)의 차이를 error항으로 정의
  * $e_{ui} = r_{ui} - x_u^T y_u$
* 현재의 gradient 반대 방향으로 $x_u, y_i$를 update한다.
  * 