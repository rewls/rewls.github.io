---
layout: default
title: Ch3 기계 학습과 인식
parent: AI
grand_parent: School Lecture
nav_order: 3
mathjax: true
mermaid: true
permalink: /docs/ai/ch3
---

# Ch3 기계 학습과 인식
{: .no_toc }

<details markdown="block">
  <summary>
    Table of contents
  </summary>
{: .fs-3 .text-delta }
- TOC
{:toc}
</details>

---

## Preview

- 사람은 끊임없이 주위 환경을 인식

- 주위 환경을 인식하는 인공지능

- 인식 프로그램을 만드는 데 필요한 기계 학습의 기초 지식 공부

---

## 3.1 기계학습 기초

- 기계학습에서의 데이터의 중요성

    - 데이터가 없으면 기계학습 적용 불가능

- 가장 단순한 iris 데이터로 시작

### 3.1.1 데이터셋 읽기

- 사이킷런(scikit-learn) 라이브러리 설치

	```shell
	pip install scikit-learn
	```

- 사이킷런에서 iris 데이터셋 제공

##### iris 데이터셋 읽기

```python
# Program 3-1(a): iris 데이터셋 읽기
from sklearn import datasets

d = datasets.load_iris()  # iris 데이터셋을 읽고
print(d.DESCR)  # 내용을 출력
```

- 출력 분석

    - 샘플 150개

    - 특징 4개

    - 부류 3개

    - 각 특징의 최소, 최대, 평균값

    - etc.

- 기계 학습 용어

    - 샘플로 구성되는 **데이터셋**

    - 특징으로 구성되는 **특징 벡터**(freature vector)

    - **부류**(class)

##### iris 내용 살피기

```python
# Program 3-1(b): iris의 내용 살펴보기
for i in range(0, len(d.data)):  # 샘플을 순서대로 출력
    print(i+1, d.data[i], d.target[i]);
```

- 출력 분석

    - d.data: 특징 벡터

    - d.target: 레이블

##### 기계학습에서 데이터셋의 표현

- 샘플을 특징 벡터와 레이블로 표현

    - 특징 벡터는 $x$로 표기($d$는 특징의 개수로서 특징 벡터의 차원이라 부름)

        - 특징벡터: $x = (x_1, x_2, \cdots, x_d)$

### 3.1.2 기계 학습 적용: 모델링과 예측

- SVM(Support vector machine)이라는 기계 학습 모델 사용

	```python
	# Program 3-1(c): iris에 기계 학습 적용: 모델링과 예측
	from sklearn import svm

	s = svm.SVC(gamma=0.1, C=10)  # svm 분류 모델 SVC 객체 생성
								  # gamma, C: hyper parameter
	s.fit(d.data, d.target)  # fit 메소드로 iris 데이터로 학습
							 # 매개변수: train feature vector, label

	new_d = [[6.4, 3.2, 6.0, 2.5], [7.1, 3.1, 4.7, 1.35]]  # 101번째와 51번째 샘플을 변형하여 새로운 데이터 생성

	res = s.predict(new_d)  # predict 메소드로 예측
	print("새로운 2개 샘플의 부류는", res)
	```

- 훈련 집합과 테스트 집합

	- 훈련 집합: 기계 학습 모델을 학습하는 데 쓰는 데이터. 특징 벡터와 레이블 정보를 모두 제공

	- 테스트 집합: 학습을 마친 모델의 성능을 측정하는 데 쓰는 데이터. 예측할 때는 특징 벡터 정보만 제공하고, 예측 결과에 대해 정확률을 측정할 때 레이블 정보 사용

- 하이퍼 매개변수(hyper parameter): 모델의 동작을 제어하는 데 쓰는 변수

---

## 3.2 인공지능 제품의 설계와 구현

- 데이터를 일고 모델링과 예측을 수행

### 3.2.1 인공지능 설계 사례: 과일 등급을 분류하는 기계

- 사과를 상중하의 세 부류로 분류하는 인공지능 기계의 설계

    1. 데이터 확보

        - 상중하 비율이 비슷하게 수천 개의 사과 수집(편향(data bias) 방지)

    2. 특징 벡터와 레이블 준비

        - 사과의 크기, 색, 표면의 균일도 등의 분별에 도움이 되는 특징을 정리한다.

    3. 학습하는 과정을 프로그래밍(훈련 데이터 사용)

        ```python
        from sklearn import svm
        s = svm.SVC(gamma=0.1, C=10)
        s.fit(apple.data, apple.target)  # apple 데이터로 모델링
        ```

    4. 예측 과정을 프로그래밍(새로 수집한 테스트 데이터 사용)

        ```python
        s.predict(x)  # 새로운 사과에서 추출한 특징 벡터 x를 예측
        ```

- 데이터 편향은 다양한 형태로 발생한다. 데이터셋이 편향되어 있으면 예측 모델도 편향될 가능성이 높다.

### 3.2.2 규칙기반 vs. 고전적 기계 학습 vs. 딥러닝

- 규칙 기반 방법

    - 분류하는 규칙을 사람이 구현

    - 큰 데이터셋에서는 불가능하고, 데이터가 바뀌면 처음부터 새로 작업해야 하는 비효율성

- 기계 학습 방법

    - 특징 벡터를 추출하고 레이블을 붙이는 과정은 규칙 기반과 동일(수작업 특징(hand-crafted freature)

    - 규칙을 만드는 일은 기계학습 모델을 이용하여 자동으로 수행

- 딥러닝 방법

    - 레이블을 붙이는 과정은 기계 학습과 동일

    - 특징 벡터를 학습과 지능으로 알아냄. **특징 학습**(freature learning) 또는 **표현 학습**(reparesentation learning)을 한다고 말함

##### What is Machine Learning?

- Machine Learning is the science (and art) of programming computers so they can <u>learn from data</u>.

- Here is a slightly more general definition:

    - [Machine Learning is the] field of study that gives computers the ability to <u>learn without being explicitly programmed</u>. —Arthur Samuel, 1959

- And a more engineering-oriented one:

    - A computer program is said to <u>learn from experience E</u> with respect to some <u>task T</u> and some <u>performance measure P</u>, if its performance on T, as measured by P, improves with experience E. —Tom Mitchell, 1997

##### Classes of learning problems

- Supervised learning

    - Data: $(x, y)$

		- $x$ is data, $y$ is label

    - Goal: Learn function to map $x \rightarrow y$

    - Apple example: This thing is an apple

- Unsupervised learning

    - Data: $x$

		- $x$ is data no labels

    - Goal: learn underlying structure

    - Apple example: This thing is like the other thing

- Reinforcement learning

    - Data: state-action pairs

    - Goal: Maximize future rewards over many time steps

    - Apple example: Eat this thing because it will keep you alive

- 원샷 학습(1-shot learning): 레이블이 있는 샘플을 하나만 사용

- 퓨샷 학습(few-shot learning): 몇 개의 샘플만 사용

- 준지도 학습(semi-supervised learning): 레이블이 있는 소량의 샘플과 레이블이 없는 대량의 샘플을 같이 사용

---

## 3.3 데이터에 대한 이해

- 특징 공간에서 데이터 분포를 살펴보고

- sklearn 라이브러리가 제공하는 여러 가지 데이터셋을 소개함

### 3.3.1 특징 공간에서 데이터 분포

- iris 데이터

    - 특징이 4개이므로 4차원 특징 공간을 형성

    - 150개 샘플 각각은 4차원 특징 공간의 한 점

```python
# Program 3-2: iris 데이터의 분포를 특징 공간에 그리기
import plotly.express as px

df = px.data.iris()
fig = px.scatter_3d(df, x='sepal_length', y='sepal_width', z='petal_width', color='species')  # petal_length를 제외하여 3차원 공간 구성
fig.show(renderer="browser")
```

<center markdown="block">
![iris](/assets/ai/img/3-iris-3d.png)
</center>

- 출력 분석

    - petal_width 특징은 분별력(discriminating power)이 뛰어남

	- sepal width 축은 세 부류가 겹쳐 분별력이 낮음

    - 데이터 시각화를 통해 데이터 분포를 관찰하여 분석할 수 있으면 어떤 특징이 더 중요한지를 분석하고 학습의 정확도를 높일 수 있음

    - 분별력이 높은 데이터에 더 집중

- 다차원 특징 공간

    - 일반적으로 d차원 상의 두점의 거리는 $d(x, y) = /sqrt{\sum_{i=1}^d (x_i-y_i)^2}$로 계산

    - 거리에 따라 분별력을 판별

### 3.3.2 영상 데이터 사례: 필기 숫자

- 각 픽셀 하나가 feature가 됨

- 두 가지 필기 숫자 데이터셋

    - sklearn 데이터셋: 8*8 맵(64개 화소), 1797개 샘플, [0,16] 명압값

    - MNIST 데이터셋: 28*28맵(784개 화소), 7만개 샘플, [0, 255] 명암값

<center markdown="block">
![digits-dataset](/assets/ai/img/3-digits-dataset.png)
</center>

- 데이터가 어떤지 알아야 어떤 feature를 더 활용할지, 어떤 모델을 사용할지를 알 수 있다.

- sklearn digits

	```python
	# Program 3-3(a): 필기 숫자 데이터
	from sklearn import datasets
	import matplotlib.pyplot as plt

	digit = datasets.load_digits()

	plt.figure(figsize=(5,5))
	# 0번 샘플 그림
	plt.imshow(digit.images[0], cmap=plt.cm.gray_r, interpolation='nearest')

	plt.show()
	print(digit.data[0])  # 0번 샘플의 화솟값 출력
	print("이 숫자는 ", digit.target[0], "입니다.")
	```

	- 어떤 특징을 사용해야 높은 성능을 얻을 수 있을까?

		- 가장 자리일수록 의미가 없는 흰 데이터일 가능성 높다.

### 3.3.3 영상 데이터 사례: lfw 얼굴 데이터셋

- lfw(labled faces in the wild) 데이터셋

    - 5729명의 유명인의 얼굴 영상 13233장. 50*27맵. [0,255] 명암 값. 흑백

    - 데이터 편향 주의(어린이, 흑인 등이 적어 얼굴 인식 프로그램을 제작하는 데 부적절)

	```python
	%matplotlib tk
	from sklearn import datasets
	import matplotlib.pyplot as plt
	lfw = datasets.fetch_lfw_people(min_faces_per_person=70, resize=0.4) # 데이터셋 읽기

	plt.figure(figsize=(20, 5))

	for i in range(8):  # 처음 8명을 디스플레이
		plt.subplot(1, 8, i+1)
		plt.imshow(lfw.images[i], cmap=plt.cm.bone)
		plt.title(lfw.target_names[lfw.target[i]])

	plt.show()
	```

### 3.3.4 텍스트 데이터 사례

- 20newsgroups 데이터셋

    - 웹에서 수집한 문서를 20개 부류로 구분, 텍스트로 구성되어 샘플의 길이가 다름

    - 시계열 데이터(단어가 나타나는 순서가 중요. 8장의 순환 신경망에서 다룸)

    ```python
    from sklearn import datasets
    news = datasets.fetch_20newsgroups(subset='train')  # 데이터셋 읽기
    print("*****\n", news.data[0], "\n*****")  # 0번 샘플 출력
    print("이 문서의 부류는 <", news.target_names[news.target[0]], "> 입니다.")
    ```

    - iris 데이터는 특징이 독립적이었지만 text 데이터는 단어의 순서가 중요함(시계열 데이터)

---

## 3.4 특징 추출과 표현

- 기계 학습의 전형적인 과정

    - 실제에서는 다양한 형태로 나타남

	- 데이터 수집 $\rightarrow$ 특징 추출 $\rightarrow$ 모델링 $\rightarrow$ 예측

### 3.4.1 특징의 분별력

- 사람은 직관적으로 분별력(discriminating power)이 높은 특징을 사용

- 기계 학습은 높은 분별력을 지닌 특징을 사용해야 함

- 다양한 형태의 특징 공간

![freature-spaces](/assets/ai/img/3-feature-spaces.png)

### 3.4.2 특징 값의 종류

- 수치형 특징

- 범주형 특징

    - 학점, 수능 등급, ...

---

## 3.5 필기 숫자 인식

- 필기숫자 데이터셋을 가지고 프로그래밍 연습

    - 특징 추출을 위한 코드 작성

    - sklearn이 제공하는 fit 함수로 모델링(학습)

    - predict 함수로 예측

### 3.5.1 화소 값을 특징으로 사용

- 화소 각각을 특징으로 간주

    - sklearn의 필기 숫자는 8*8 맵으로 표현되므로 64차원 특징 벡터

    - 2차원 구조를 1차원 구조로 변환

```python
from sklearn import datasets
from sklearn import svm

digit = datasets.load_digits()

# svm의 분류기 모델 SVC를 학습
s = svm.SVC(gamma=0.1, C=10)
s.fit(digit.data, digit.target)  # digit 데이터로 모델링

# 훈련 집합의 앞에 있는 샘플 3개를 새로운 샘플로 간주하고 인식해봄
new_d = [digit.data[0], digit.data[1], digit.data[2]]
res = s.predict(new_d)
print("예측값은", res)
print("참값은", digit.target[0], digit.target[1], digit.target[2])

# 훈련 집한을 테스트 집합으로 간주하여 인식해보고 정확률을 측정
res = s.predict(digit.data)
correct = [i for i in range(len(res)) if res[i]==digit.target[i]]
accuracy = len(correct)/len(res)
print("화소 특징을 사용했을 때 정확률=", accuracy*100, "%")
```

---

## 3.6 성능 측정

- 객관적인 성능 측정의 중요성

	- 모델 선택할 때 중요

- 일반화(generalization) 능력

    - 학습에 사용하지 않았던 새로운 데이터에 대한 성능

- 정확도와 일반화 능력이 중요함

### 3.6.1 혼동 행렬과 성능 측정 기준

- 혼동 행렬(confusion matrix)

    - 부류 별로 옳은 분류와 틀린 분류의 개수를 기록한 행렬

	<center markdown="block">
	![confusion-matrix](/assets/ai/img/3-confusion-matrix.png)
	</center>

- 널리 쓰이는 성능 측정 기준

    - 정확률(accuracy)

        - 부류가 불균형일 때 성능을 제대로 반영하지 못함

        $$
		정확률 = {TP + TN \over TP + FP + TN + FN}
		$$

    - 특이도(specificity)와 민감도(sensitivity)(의료에서 주로 사용)

        $$
		특이도 = {TN \over TN + FP}, 민감도={TP \over TP+FN}
		$$

    - 정밀도(precision)와 재현률(recall)(정보검색에서 주로 사용)

        $$
		정밀도 = {TP \over TP + FP}, 재현률 = {TP \over TP+FN}
		$$

		- 코로나 양성 예측 모델의 경우 확산 방지를 위해 recall을 더 중요하게 봐야 한다.

### 3.6.2 훈련/검증/테스트 집합으로 쪼개기

- 주어진 데이터를 적절한 비율로 훈련, 검증, 테스트 집합으로 나누어 씀

<center markdown="block">
![split-dataset](/assets/ai/img/3-split-dataset.png)
</center>

- 학습하면서 오류를 수정하고 싶을 때 검증 집합 사용

- 데이터셋이 적을 때 검증 집합까지 빼내면 훈련 집합이 편향될 수 있으므로 주의

```python
# Program 3-5: 필기 숫자 인식 - 훈련 집합으로 학습하고 테스트 집합으로 성능 측정
from sklearn import datasets
from sklearn import svm
from sklearn.model_selection import train_test_split
import numpy as np

# 데이터셋을 읽고 훈련 집합과 테스트 집합으로 분별할
digit = datasets.load_digits()
x_train, x_test, y_train, y_test = train_test_split(digit.data, digit.target, train_size=0.6)

# svm의 분류 모델 SVC를 학습
s = svm.SVC(gamma= 0.001)
s.fit(x_train, y_train)

res = s.predict(x_test)

# 혼동 행렬 구함
conf = np.zeros((10, 10))
for i in range(len(res)):
	conf[res[i]][y_test[i]] += 1
print(conf)

# 정확률 측정하고 출력
no_correct = 0
for i in range(10):
	no_correct += conf[i][i]
accuracy = no_correct/len(res)
print("테스트 집합에 대한 정확률은", accuracy*100, "%입니다.")
```

- 분석하는 입장에서 왜 다르게 예측했는지 분석하고 향상시키는 게 필요

	- 이를 쉽게 보기 위해서 confusion matrix 사용

    - train_test_split 함수가 난수를 사용해 데이터를 분할하기 때문에 실행할 때마다 출력이 다르게 나올 수 있음

### 3.6.3 교차 검증

- 훈련/테스트 집합 나누기의 한계

    - 훈련 데이터와 테스트 데이터가 편향되어 나눠질 수 있다.

- k-겹 교차 검증(k-fold cross validation)

    - 훈련 집합을 k개의 부분집합으로 나누어 사용

    - 한 개를 남겨두고 k-1개로 학습한 다음 남겨둔 것으로 성능 측정

    - k개의 성능을 평균하여 신뢰도 높임

	<center markdown="block">
	![k-fold-cross-validation](/assets/ai/img/3-k-fold-cross-validation.png)
	</center>

	- 특정 데이터셋에 대해서 정확률이 높고 낮음을 볼 수도 있음

- digit 데이터에 교차 검증 적용(모델 선택 제외)

	```python
	# Program 3-6: 필기 숫자 인식 - 교차 검증으로 성능 측정
	from sklearn import datasets
	from sklearn import svm
	from sklearn.model_selection import cross_val_score
	import numpy as np

	digit = datasets.load_digits()
	s = svm.SVC(gamma=0.001)
	accuracies = cross_val_score(s, digit.data, digit.target, cv=5)  # 5-겹 교차 검증

	print(accuracies)
	print("정확률(평균) = %0.3f, 표준편차=%0.3f" %(accuracies.mean()*100, accuracies.std()))
	```

    - train, test 셋을 어떻게 나누냐에 따라 정확도가 달라질 수 있다.

    - 정확률이 들쭉날쭉할 수 있기 때문에 한번만 시도하는 건 위험

    - k를 크게 하면 신뢰도가 높아지지만 실행 시간이 더 걸린다.

---

## 3.7 인공지능은 어떻게 인식을 하나

- 지금까지는 모델(분류기)의 원리에 대한 이해 없이 프로그래밍 실슴

	- 동작 원리에 대한 이해가 없으면 성능 향상에 한계가 있음

### 3.7.1 특징 공간을 분할하는 결정 경계

- 인공지능의 인식은 철저히 수학에 의존

    - 샘플은 특징 벡터로 표현되며, 특징 벡터는 특징 공간의 한 점에 해당

    - 특징 공간 변환 예

	<center markdown="block">
    ![feature-space-transform](/assets/ai/img/3-feature-space-transform.png)
	</center>

	- 선형 분리만 가능한 모델은 한계가 있다.

	- 모델을 바꾸거나 차원축을 변경하여 성능을 개선한다.

- 특징 공간을 분할하는 결정 경계(decision boundary)

    - 4차원 이상은 수학적 상상력 필요

	<center markdown="block">
    ![decision-boundary](/assets/ai/img/3-decision-boundary.png)
	</center>

- 현대 기계학습이 다루는 데이터

    - 수백~수만 차원 특징 공간

		- 시각화하기 어렵고 수학적으로 나타내기도 어려움

	- 딥러닝에서 다룸

- 결정 경계를 정하는 문제에서 고려 사항

    - 비선형 분류기(nonlinear classifier) 사용

    - 과잉 적합(overfitting) 회피

        - 과잉 적합은 아웃라이어를 맞히려고 과다하게 복잡한 결정 경계를 만드는 현상

		- 복잡할수록 train data에 대해 정확도가 높아지겠지만 일반화 능력이 떨어지게 된다.

### 3.7.2 SVM의 원리

- SVM의 목적

    - 여백(margin)을 최대화하여 일반화 능력을 극대화

    ![svm](./img/svm.png)

- 기계 학습의 목적은 일반화 능력을 극대화하는 것

    - SVM은 일반화 능력을 높이려 여백(margin)을 최대화하는 결정 경계를 찾는다.

- SVM을 비선형 분류기로 확장

    - 원래 SVM은 선형 분류기

    - 커널 트릭을 사용하여 비선형 분류기로 확장

- 하이퍼 매개변수 C

	- 얼마만큼 오류를 허용할 것인가

    - C를 크게 하면, 잘못 분류한 훈련 집합의 샘플은 적은데 여백이 작아짐(훈련 집합에 대한 정확률은 높지만 일반화 능력 떨어짐)

    - C를 작게 하면, 여백은 큰데 잘못 분류한 샘플이 많아짐(훈련 집합에 대한 정확률은 낮지만 일반화 능력 높아짐)

- 3.1.2 프로그램 중

    ```python
    s = svm.SVC(gamma=0.1, C= 10)  # svm 분류 모델 SVC 객체 생성하고
    ```

---

## Summary

- 3강

    - 기계학습(ML) 기본개념

        - 특징벡터, 분류기 모델(SVM)

        - ML vs DL: **hand-crafted feature** vs. **feature (reparesentation) learning**

    - 데이터 이해: 특히 다차원 특징 공간

    - 특징(feature) 추출/표현 w/ Discriminating power

- Key terms

    - confusion matrix

    - measurement: accuracy, precision, recall

    - Data split: train/validation/test

    - k-fold cross validation

    - Decision boundary issue: overfitting, generalization
