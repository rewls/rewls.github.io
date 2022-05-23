---
layout: default
title: Ch1 Hello Python
parent: Deap Learning from Scratch
grand_parent: Study
nav_order: 1
permalink: /docs/deap/ch1
---

# Ch1 Hello Python
{: .no_toc }

<details open markdown="block">
  <summary>
    Toggle
  </summary>
## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}
</details>

---

## 1.4 파이썬 스크립트 파일

### 1.4.2 클래스

- 독자적인 자료형을 만들 수 있다.

- 전용 함수(메서드)와 속성을 정의할 수 있다.

##### 구조

```python
class 클래스 이름:
	def __init__(self, 인수, ...):		# 생성자
		...
	def 메서드 이름 1(self, 인수, ...):	# 메서드 1
		...
	def 메서드 이름 2(self, 인수, ...):	# 메서드 2
		...
```

##### \_\_init\_\_

- 클래스를 초기화하는 방법을 정의한다.

- 생성자라고도 한다.

- 클래스의 인스턴스가 만들어질 때 한 번만 불린다.

- 메서드의 첫 번째 인수로 자신(자신의 인스턴스)을 나타내는 `self`를 명시적으로 쓴다.

##### 예제

```python
class Man:
	def __init__(self, name):
		self.name = name
		print("Initialized!")

	def hello(self):
		print("Hello " + self.name + "!")

	def goodbye(self):
		print("Good-bye " + self.name + "!")

m = Man("David")
m.hello()
m.goodbye()
```

---

## 1.5 넘파이

- 넘파이의 배열 클래스 `numpy.array`에 배열과 행렬 계산에 편리한 메서드 많음

### 1.5.1 넘파이 가져오기

```python
import numpy as np
```

### 1.5.2 넘파이 배열 생성하기

```python
# interpreter
import numpy as np
x = np.array([1.0, 2.0, 3.0])
print(x)
type(x)
```

- `numpy.array` : 리스트를 인수로 받아 넘파이 배열(`numpy.ndarray`)을 반환한다.

### 1.5.3 넘파이의 산술 연산

```python
# interpreter
x = np.array([1.0, 2.0, 3.0])
y = np.array([2.0, 4.0, 6.0])
x + y
x - y
x * y
x / y
```

- 원소별(element-wise) 산술연산 수행

- 원소 수가 같을 때만 산술 연산할 수 있음

### 1.5.4 넘파이의 N차원 배열

```python
# interpreter
A = np.array([[1, 2], [3, 4]])
print(A)
A.shape
A.dtype
B = np.array([[3, 0], [0, 6]])
A + B
A * B
```

- `ndarray.shape` : 배열의 형상 출력

- `ndarray.dtype` : 배열의 원소의 자료형 출력

> - 1차원 배열 : 벡터(vector)
>
> - 2차원 배열 : 행렬(matrix)
>
> - 벡터와 행렬을 일반화한 것 : 텐서(tensor)

### 1.5.5 브로드캐스트

- 형상이 다른 배열끼리 산술연산할 수 있도록 하는 기능

- 스칼라값과 n차원 배열의 산술연산에서 스칼라값을 n차원 배열로 확장한 후 연산

- 저차원 배열과 고차원 배열의 산술연산에서 저차원 배열을 고차원 배열로 확장한 후 연산

```python
# interpreter
A = np.array([[1, 2], [3, 4]])
B = np.array([10, 20])
A * 10
B * 10
A * B
```

### 1.5.6 원소 접근

```python
# interpreter
X = np.array([[51, 55], [14, 19], [0, 4]])
print(X)
X[0]
X[0][1]
for row in X:
	print(row)
```

- 인덱스로 접근

```python
X = X.flatten()			# X를 1차원 배열로 변환(평탄화)
print(X)
X[np.array([0, 2, 4])]	# 인덱스가 0, 2, 4인 원소 얻기
X > 15
X[X>15]
```

- 인덱스를 배열로 지정해 한 번에 여러 원소에 접근

- 특정 조건을 만족하는 원소를 얻을 수 있다.

- bool 배열을 사용해 True에 해당하는 원소에만 접근할 수 있다.

> 넘파이의 주된 처리는 C와 C++로 구현되어 성능을 해치지 않으면서 파이썬의 편리한 문법을 사용할 수 있다.

---

## 1.6 matplotlib

- 그래프 그리기와 데이터 시각화를 위한 라이브러리

### 1.6.1 단순한 그래프 그리기

```python
%matplotlib tk

import numpy as np
import matplotlib.pyplot as plt

# 데이터 준비
x = np.arange(0, 6, 0.1)	# 0에서 6까지 0.1 간격으로 넘파이 배열 생성
y = np.sin(x)

# 그래프 그리기
plt.plot(x, y)
plt.show()
```

> %matplotlib tk : tkinter UI에 그래프 출력하기 위한 magic command

- `matplotlib.pyplot.plot` : 그래프 그리기

- `matplotlib.pyplot.show` : 그래프를 화면에 출력

### 1.6.2 pyplot의 기능

```python
%matplotlib tk

import numpy as numpy
import matplotlib.pyplot as plt

# 데이터 준비
x = np.arange(0, 6, 0.1)	# 0에서 6까지 0.1 간격으로 생성
y1 = np.sin(x)
y2 = np.cos(x)

# 그래프 그리기
plt.plot(x, y1, label="sin")
plt.plot(x, y2, linestyle="--", label="cos")	# cos 함수 점선으로 그리기
plt.xlabel("x")	# x축 이름
plt.ylabel("y")	# y축 이름
plt.title('sin & cos')	# 제목
plt.legend()	# 그래프 범례 표시
plt.show()
```

### 1.6.3 이미지 표시하기

```python
import matplotlib.pyplot as plt
from matplotlib.image import imread

img = imread('/mnt/c/Users/dajin/Pictures/01 portrait/07 meenoi/6.jpg')	# 이미지 읽어오기

plt.imshow(img)
plt.show()
```

---

## 1.7 정리

### 후속 공부

- 처음 시작하는 파이썬(한빛미디어, 2015)

	- 파이썬 프로그래밍을 기초부터 응용까지 친절하게 설명해주는 실천적인 입문서

- 파이썬 라이브러리를 활용한 데이터 분석(한빛미디어, 2013)

	- 넘파이

- Scipy 강의 노트(웹사이트)

	- 과학 기술에서의 계산을 주제로 넘파이와 matplotlib을 잘 설명함
