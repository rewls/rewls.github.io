---
layout: default
title: Ch3 신경망
parent: Deap Learning from Scratch
nav_order: 3
mathjax: true
mermaid: true
---

# Ch3 신경망
{: .no_toc }

<details open markdown="block">
  <summary>
    Toggle
  </summary>

## Table of contents
{: .no_toc .text-delta }

- TOC
{:toc}
</details>

---

- 앞 장에서는 인간이 적절한 매개변수를 정했지만 신경망을 이용하면 매개변수를 데이터로부터 자동으로 합습할 수 있다.

- 이번 장에서는 신경망의 개요를 설명하고, 신경망이 입력 데이터가 무엇인지 식별하는 처리 과정을 자세히 알아본다.

## 3.1 퍼셉트론에서 신경망으로

### 3.1.1 신경망의 예

<div class="mermaid">
graph LR;
	x1(( )); x2(( )); s1(( )); s2(( )); s3(( )); y1(( )); y2(( ));
	x1 --> s1; x1 --> s2; x1 --> s3;
	x2 --> s1; x2 --> s2; x2 --> s3;
	s1 --> y1; s1 --> y2;
	s2 --> y1; s2 --> y2;
	s3 --> y1; s3 --> y2;
	subgraph input[입력층, 0층];
		x1; x2;
		end;
	subgraph hidden[은닉층, 1층];
		s1; s2; s3;
		end;
	subgraph out[출력층, 2층];
		y1; y2;
		end;
</div>

- 은닉층의 뉴런은 사람 눈에 보이지 않는다.

> 위의 신경망은 모두 3층으로 구성되지만 가중치를 갖는 층은 2개뿐이기 때문에 2층 신경망으로 한다. 경우에 따라 3층 신경망이라 하는 경우도 있으니 주의

### 3.1.2 퍼셉트론 복습

<div class="mermaid">
graph LR;
	x1((x1)); x2((x2)); y((y));
	x1 --w1-->y;
	x2 --w2-->y;
</div>

<div>
$$
y = \begin{cases}
	0~(b + w_1x_1 + w_2x_2 \le 0)\\
	1~(b + w_1x_1 + w_2x_2 > 0)\\
	\end{cases}
$$
</div>

- $b$는 **편향**을 나타내는 매개변수로, 뉴런이 얼마나 쉽게 활성화되느냐를 제어

- $w_1$과 $w_2$는 각 신호의 **가중치**를 나타내는 매개변수로, 각 신호의 영향력을 제어

<div class="mermaid">
graph LR;
	x1((x1)); x2((x2)); 1((1)); y((y));
	1 --b--> y;
	x1 --w1--> y;
	x2 --w2--> y;
</div>

- 편향을 명시한 퍼셉트론 구조

- 가중치가 $b$이고 입력이 1인 뉴런 추가

<div>
$$
y = h(b + w_1x_1 + w_2x_2)
$$
</div>

<div>
$$
h(x) = \begin{cases}
	0~(x \le 0)\\
	1~(x > 0)\\
	\end{cases}
$$
</div>

- 입력 신호의 총합이 $h(x)$라는 함수를 거쳐 변환되어, 그 변환된 값이 $y$의 출력이 된다.

### 3.1.3 활성화 함수의 등장

- 입력 신호의 총합을 출력 신호로 변환하는 함수를 일반적으로 **활성화 함수**$^{\text{activation function}}$라 한다.

	- 입력 신호의 총합이 활성화를 일으키는지 정하는 역할을 한다.

<div>
$$
a = b + w_1x_1 + w_2x_2
$$
</div>

<div>
$$
y = h(a)
$$
</div>

<div class="mermaid">
graph LR;
	x1((x1)); x2((x2)); 1((1)); y(("a --h(x)--> y"));
	1 --b--> y;
	x1 --w1--> y;
	x2 --w2--> y;
</div>

- 활성화 함수 처리 과정 명시한 퍼셉트론 구조

> - **단순 퍼셉트론**은 단층 네트워크에서 계단 함수(임계값을 경계로 출력이 바뀌는 함수)를 활성화 함수로 사용한 모델을 가리킨다.
> - **다층 퍼셉트론**은 신경망(여러 층으로 구성되고 시그모이드 함수 등의 매끈한 활성화 함수를 사용하는 네트워크)을 가리킨다.

---

## 3.2 활성화 함수

<div>
$$
h(x) = \begin{cases}
	0~(x \le 0)\\
	1~(x > 0)\\
	\end{cases}
$$
</div>

- 임계값을 경계로 출력이 바뀌는 함수를 **계단 함수**라고 한다.

- 활성화 함수를 계단 함수에서 다른 함수로 변경하는 것이 신경망의 세계로 나아가는 열쇠!

### 3.2.1 시그모이드 함수

<div>
$$
h(x) = {1 \over 1 + exp(-x)}
$$
</div>

- $exp(-x)$는 $e^{-x}$를 뜻한다.

- 신경망에서는 활성화 함수로 시그모이드 함수를 이용한다.

- 퍼셉트론과 신경망의 주된 차이는 활성화 함수 뿐이다.

### 3.2.2 계단 함수 구현

```python
def step_function(x):
	if x > 0:
		return 1
	else:
		return 0
```

- 이 구현에서 인수 x는 실수(부동소수점)만 받아들이기 때문에 넘파이 배열을 인수로 넣을 수는 없다.

```python
def step_function(x):
	y = x > 0
	return y.astype(np.int)
```

- 넘파이 배열도 인수로 받을 수 있도록 수정한 구현

```python
# interpreter
import numpy as np
x = np.array([-1.0, 1.0, 2.0])
x
y = x > 0
y
y = y.astype(int)
y
```

- 넘파이 배열에 부등호 연산을 수행하면 배열의 각각에 부등호 연산을 수행한 bool 배열이 생성된다.

- `numpy.astype` : 넘파이 배열의 자료형을 변환한다. 인수로 변환할 자료형을 지정한다.

### 3.2.3 계단 함수의 그래프

```python
%matplotlib tk
import numpy as np
import matplotlib.pylab as plt

def step_function(x):
	return np.array(x>0, dtype=int)

x = np.arange(-5.0, 5.0, 0.1)
y = step_function(x)
plt.plot(x, y)
plt.ylim(-0.1, 1.1)	# y축의 범위 지정
plt.show()
```

### 3.2.4 시그모이드 함수 구현하기

```python
%matplotlib tk
import numpy as np
import matplotlib.pylab as plt

def sigmoid(x):
	return 1 / (1 + np.exp(-x))

x = np.arange(-5.0, 5.0, 0.1)
y = sigmoid(x)
plt.plot(x, y)
plt.ylim(-0.1, 1.1)	# y축 범위 지정
plt.show()
```

- 인수로 넘파이 배열이 와도 바르게 계산된다.

- 브로드캐스트를 통해 넘파이 배열과 스칼라값의 연산을 수행한다.

> 시그모이드(sigmoid)란 'S자 모양'이라는 뜻

### 3.2.5 시그모이드 함수와 계단 함수 비교

```python
%matplotlib tk
import numpy as np
import matplotlib.pylab as plt

def sigmoid(x):
	return 1 / (1 + np.exp(-x))

def step_function(x):
	return np.array(x>0, dtype=int)

x = np.arange(-5.0, 5.0, 0.1)
sig_y = sigmoid(x)
step_y = step_function(x)

plt.plot(x, sig_y, label="sigmoid")
plt.plot(x, step_y, linestyle="--", label="step")	# cos 함수 점선으로 그리기

plt.ylim(-0.1, 1.1)	# y축 범위 지정
plt.title('sigmoid & step')
plt.legend()
plt.show()
```

##### 차이점
{: .no_toc }

- 시그모이드 함수는 부드러운 곡선이며 입력에 따라 출력이 연속적으로 변화하고, 계단 함수는 0을 경계로 출력이 갑자기 바뀐다.

- 계단 함수가 0과 1 중 하나의 값만 돌려주는 반면 시그모이드 함수는 실수를 돌려준다.

##### 공통점
{: .no_toc }

- 입력이 작을 때의 출력은 0에 가깝고, 입력이 커지만 출력이 1에 가까워지는 구조이다.

- 0에서 1 사이의 실수를 출력한다.

### 3.2.6 비선형 함수

- 계단 함수와 시그모이드 함수의 중요한 공통점은 **비선형 함수**라는 것

> - 함수에 무언가 입력했을 때 출력이 입력의 상수배만큼 변하는 함수를 **선형 함수**라고 한다.
>	- $f(x) = ax + b$(a, b는 상수)
> - **비선형 함수**는 선형이 아닌 함수

- 신경망에서는 활성화 함수로 비선형 함수를 사용해야 한다.

- 선형 함수를 사용하면 신경망의 층을 깊게 하는 의미가 없어지기 때문

### 3.2.7 ReLU 함수

- 시그모이드 함수는 신경망 분야에서 오래전부터 이용해왔으나, 최근에는 **ReLU**$^{\text{Rectified Linear Unit, 렐루}}$ 함수를 사용한다.

<div>
$$
h(x) = \begin{cases}
	x~(x > 0) \\
	0~(x \le 0)
	\end{cases}
$$
</div>
```python
%matplotlib tk
import numpy as np
import matplotlib.pylab as plt

def relu(x):
	return np.maximum(0, x)

x = np.arange(-5.0, 5.0, 0.1)
y = relu(x)
plt.plot(x, y)
plt.ylim(-0.1, 5.1)	# y축의 범위 지정
plt.show()
```

- `numpy.maximum` : 두 입력 중 큰 값을 반환

---

## 3.3 다차원 배열의 계산

### 3.3.1 다차원 배열

```python
import numpy as np

A = np.array([1, 2, 3, 4])
print(A)
np.ndim(A)
A.shape
A.shape[0]
```

- `numpy.ndim` : 배열의 차원 수 반환

- `ndarray.shape` : 배열의 형상을 튜플로 반환

```python
B = np.array([[1,2], [3,4], [5,6]])
print(B)
np.ndim(B)
B.shape
```

- $n \times m$ 배열 : 0번째 차원에는 원소가 n개, 1번째 차원에는 원소가 m개 있다는 의미

- 2차원 배열은 **행렬**$^{\text{matrix}}$이라고 부르고 배열의 가로 방향을 **행**$^{\text{row}}$, 세로 방향을 **열**$^{\text{column}}$이라고 한다.

### 3.3.2 행렬의 곱

- 왼쪽 행렬의 행(가로)과 오른쪽 행렬의 열(세로)을 원소별로 곱하고 그 값들을 더해서 계산한다.

- 교환법칙은 성립하지 않는다.

- 첫째 행렬의 1번째 차원의 원소수(열 수)와 둘째 행렬의 0번째 차원의 원소 수(행 수)가 같아야 한다.

<div>
$$
A~~~~~~~~~~~~B~~~~=~~~~C
$$
</div>

<div>
$$
m \times \cancel{n}~~~~\cancel{n} \times p~~~~~m \times p
$$
</div>

<div>
$$
A = \left(
	\begin{matrix}
		a_{11} & \cdots & a_{1n} \\
		\vdots & \ddots & \vdots \\
		a_{m1} & \cdots & a_{mn}
	\end{matrix}
	\right),~

B = \left(
	\begin{matrix}
		b_{11} & \cdots & b_{1p} \\
		\vdots & \ddots & \vdots \\
		b_{n1} & \cdots & b_{np}
	\end{matrix}
	\right)
$$
</div>

<div>
$$
C = AB
$$
</div>

<div>
$$
C = \left(
	\begin{matrix}
		c_{11} & \cdots & c_{1p} \\
		\vdots & \ddots & \vdots \\
		c_{1m} & \cdots & c_{mp}
	\end{matrix}
	\right)
$$
</div>

<div>
$$
c_{ij} = a_{i1}b_{1j} + a_{i2}b_{2j} + \cdots + a_{in}b_{nj} = \sum^n_{k=1}a_{ik}b_{kj}
$$
</div>

<div>
$$
C = \left(
	\begin{matrix}
		a_{11}b_{11} + \cdots + a_{1n}b_{n1} & \cdots & a_{11}b_{1p} + \cdots a_{1n}b_{np} \\
		\vdots & \ddots & \vdots \\
		a_{m1}b_{11} + \cdots + a_{mn}b_{n1} & \cdots & a_{m1}b_{1p} + \cdots + a_{mn}b_{np}
	\end{matrix}
	\right)
$$
</div>

```python
A = np.array([[1,2], [3,4]])
A.shape
B = np.array([[5,6], [7,8]])
B.shape
np.dot(A, B)
```

- `numpy.dot` : 행렬의 곱

### 3.3.3 신경망에서의 행렬 곱

- 편향과 활성화 함수 생략, 가중치만 갖는 신명망 구현

<div class="mermaid">
graph LR;
	x1((x1)); x2((x2)); y1((y1)); y2((y2)); y3((y3));
	x1 --1--> y1;
	x1 --3--> y2;
	x1 --5--> y3;
	x2 --2--> y1;
	x2 --4--> y2;
	x2 --6--> y3;
</div>

<div>
$$
W = \left(
	\begin{matrix}
		1 & 3 & 5 \\
		2 & 4 & 6
	\end{matrix}
	\right)
$$
</div>

<div>
$$
X~~~~~~~~~~W~~~=~~~~Y
$$
</div>

<div>
$$
\cancel2~~~~~~~\cancel2 \times 3~~~~~~~~~~3
$$
</div>

```python
# interpreter
X = np.array([1, 2])
X.shape
W = np.array([[1, 3, 5], [2, 4, 6]])
print(W)
W.shape
Y = np.dot(X, W)
print(Y)
```

- 행렬의 곱으로 한번에 계산해주는 기능은 신경망 구현에 매우 중요

---

## 3.4 3층 신경망 구현하기

- 넘파이 배열을 잘 쓰면 아주 적은 코드만으로 신경망의 순방향 처리를 완성할 수 있다.

<div class="mermaid">
graph LR;
	x1((x1)); x2((x2)); h11(( )); h12(( )); h13(( )); h21(( )); h22(( )); y1((y1)); y2((y2));
	x1 --> h11; x1 --> h12; x1 --> h13;
	x2 --> h11; x2 --> h12; x2 --> h13;
	h11 --> h21; h11 --> h22;
	h12 --> h21; h12 --> h22;
	h13 --> h21; h13 --> h22;
	h21 --> y1; h21 --> y2;
	h22 --> y1; h22 --> y2;
</div>

### 3.4.2 각 층의 신호 전달 구현하기

```python
import numpy as np

def sigmoid(x):
	return 1 / (1 + np.exp(-x))

def identity_function(x):
	return x

X = np.array([1.0, 0.5])
W1 = np.array([[0.1, 0.3, 0.5], [0.2, 0.4, 0.6]])
B1 = np.array([0.1, 0.2, 0.3])

print("(W1.shape) :", W1.shape)
print("(X.shape) :", X.shape)
print("(B1.shape) :", B1.shape)

A1 = np.dot(X, W1) + B1
Z1 = sigmoid(A1)

print("(A1) :", A1)
print("(Z1) :", Z1)

W2 = np.array([[0.1, 0.4], [0.2, 0.5], [0.3, 0.6]])
B2 = np.array([0.1, 0.2])

print("(Z1.shape) :", Z1.shape)
print("(W2.shape) :", W2.shape)
print("(B2.shape) :", B2.shape)

A2 = np.dot(Z1, W2) + B2
Z2 = sigmoid(A2)

W3 = np.array([[0.1, 0.3], [0.2, 0.4]])
B3 = np.array([0.1, 0.2])

A3 = np.dot(Z2, W3) + B3
Y = identity_function(A3)
```

> 출력층의 활성화 함수는 풀고자 하는 문제의 성질에 맞게 정한다.
> 일반적으로
> - 회귀에는 항등함수
> - 2클래스 분류에는 시그모이드 함수
> - 다중 클래스 분류에는 소프트맥스 함수
> 를 사용한다.

### 3.4.3 구현 정리

- 신경망 구현의 관례에 따라 가중치만 대문자로 쓰고 그 외 편향과 중간 결과 등은 모두 소문자로 쓴다.

```python
import numpy as np

def sigmoid(x):
	return 1 / (1 + np.exp(-x))

def identity_function(x):
	return x

def init_network():
	network = {}
	network['W1'] = np.array([[0.1, 0.3, 0.5], [0.2, 0.4, 0.6]])
	network['b1'] = np.array([0.1, 0.2, 0.3])
	network['W2'] = np.array([[0.1, 0.4], [0.2, 0.5], [0.3, 0.6]])
	network['b2'] = np.array([0.1, 0.2])
	network['W3'] = np.array([[0.1, 0.3], [0.2, 0.4]])
	network['b3'] = np.array([0.1, 0.2])

	return network

def forward(network, x):
	W1, W2, W3 = network['W1'], network['W2'], network['W3']
	b1, b2, b3 = network['b1'], network['b2'], network['b3']

	a1 = np.dot(x, W1) + b1
	z1 = sigmoid(a1)
	a2 = np.dot(z1, W2) + b2
	z2 = sigmoid(a2)
	a3 = np.dot(z2, W3) + b3
	y = identity_function(a3)

	return y

network = init_network()
x = np.array([1.0, 0.5])
y = forward(network, x)
print(y)
```

- `forward` : 신호가 순방향(입력에서 출력 방향)으로 전달됨(순전파)을 의미

---

## 3.5 출력층 설계하기

- 일반적으로 회귀에는 항등함수를, 분류에는 소프트맥스 함수를 사용한다.

> 기계학습 문제는 **분류**$^{\text{classification}}$와 **회귀**$^{\text{regression}}$로 나뉜다.

### 3.5.1 항등함수와 소프트맥스 함수 구현하기

##### 항등 함수(identity function)
{: .no_toc }

<div class="mermaid">
graph LR;
	a1((a1)); a2((a2)); a3((a3)); y1((y1)); y2((y2)); y3((y3));
	a1 --"σ()"--> y1;
	a2 --"σ()"--> y2;
	a3 --"σ()"--> y3;
</div>

- 입력을 그대로 출력한다.

##### 소프트맥스 함수(softmax function)
{: .no_toc }

- 분류에서 사용한다.

<div>
$$
y_k = {exp(a_k) \over \sum_{i=1}^n exp(a_i)}
$$
</div>

- $exp(x)$는 $e^x$를 뜻하는 지수 함수(exponential function)이다.

- $a_k$는 $k$번째 입력 신호, $n$은 출력층의 뉴런수, $y_k$는 $k$번째 출력임을 뜻한다.

- 모든 입력 신호를 받아 출력을 계산한다.

<div class="mermaid">
graph LR;
	a1((a1)); a2((a2)); a3((a3)); y1((y1)); y2((y2)); y3((y3));
	a1 --"σ()"--> y1; a1 --"σ()"--> y2; a1 --"σ()"--> y3;
	a2 --"σ()"--> y1; a2 --"σ()"--> y2; a2 --"σ()"--> y3;
	a3 --"σ()"--> y1; a3 --"σ()"--> y2; a3 --"σ()"--> y3;
</div>

```python
a = np.array([0.3, 2.9, 4.0])
exp_a = np.exp(a)
print(exp_a)
sum_exp_a = np.sum(exp_a)
print(sum_exp_a)
y = exp_a / sum_exp_a
print(y)
```

```python
def softmax(a):
	exp_a = np.exp(a)
	sum_exp_a = np.sum(exp_a)
	y = exp_a / sum_exp_a

	return y
```

### 3.5.2 소프트맥스 함수 구현 시 주의점

- 지수함수를 사용하기 때문에 오버플로 주의

- 이 문제를 해결하도록 소프트맥스 함수 구현 개선

<div>
$$
\begin{aligned}
y_k = {exp(a_k) \over \sum_{i=1}^nexp(a_i)} &= {Cexp(a_k) \over C\sum_{i=1}^nexp(a_i)} \\
	&= {exp(a_k + logC) \over \sum_{i=1}^nexp(a_i + logC)} \\
	&= {exp(a_k + C^\prime) \over \sum_{i=1}^nexp(a_i+C^\prime)}
\end{aligned}
$$
</div>

- 소프트맥스의 지수 함수를 계산할 때 어떤 정수를 더해도 (혹은 빼도) 결과는 바뀌지 않는다.

- 오버플로를 막을 목적으로 $C^\prime$에 입력 신호 중 $-최댓값$을 대입하는 것이 일반적

```python
# interpreter
a = np.array([1010, 1000, 990])
np.exp(a) / np.sum(np.exp(a))	# 소프트맥스 함수의 계산 제대로 안 됨
c = np.max(a)
a - c
np.exp(a - c) / np.sum(np.exp(a - c))
```

```python
def softmax(a):
	c = np.max(a)
	exp_a = np.exp(a - c)	# 오버플로 대책
	sum_exp_a = np.sum(exp_a)
	y = exp_a / sum_exp_a

	return y
```

### 3.5.3 소프트맥스 함수의 특징

- 소프트맥스 함수의 출력은 0에서 1.0 사이의 실수

- 소프트맥스 함수 출력의 총합은 1

- 소프트맥스 함수의 출력을 확률로 해석할 수 있다.

- 소프트맥스 함수를 적용해도 각 원소의 대소 관계는 변하지 않는다.

- 현업에서 신경망을 이용한 분류를 할 때 지수 함수 계산에 드는 자원 낭비를 줄이고자 출력층의 소프트맥스 함수는 생략하는 것이 일반적

> 기계학습의 문제 풀이는 **학습**과 **추론**$^{\text{inference}}$의 단계를 거쳐 이루어진다.
> 학습 단계에서 모델을 학습하고 추론 단계에서 앞서 학습한 모델로 미지의 데이터에 대해서 추론(분류)를 수행한다.
> 추론 단계에서는 출력층의 소프트맥스 함수를 생략하는 것이 일반적이나, 신경망을 학습시킬 때는 출력층에서 소프트맥스 함수를 사용한다.

---

## 3.6 손글씨 숫자 인식

- 이미 학습된 매개변수를 사용하여 학습 과정은 생략하고 추론 과정만 구현

- 이 추론 과정을 신경망의 **순전파**$^{\text{forward propagation}}$라고도 한다.

> 기계학습과 마찬가지로 신경망도 훈련데이터를 사용해 가중치 매개변수를 학습하고, 추론 단계에서는 앞서 학습한 매개변수를 사용하여 입력 데이터를 분류한다.

### 3.6.1 MNIST 데이터셋

- 기계학습 분야에서 아주 유명한 데이터셋으로 간단한 실험부터 논문으로 발표되는 연구까지 다양한 곳에서 이용됨

- 0부터 9까지의 숫자 이미지로 구성된다.

- 훈련 이미지 60,000장, 시험 이미지 10,000장

- MNIST의 이미지 데이터는 $28 \times 28$ 크기의 회색조 이미지(1채널)이며, 각 픽셀은 0에서 255까지의 값을 취한다.

- 각 이미지에는 이미지가 실제 의미하는 숫자가 레이블로 붙어 있다.

```python
# import sys, os
# sys.path.append(os.pardir)	# 부모 디렉터리의 파일을 가져올 수 있도록 설정
from dataset.mnist import load_mnist

# 처음 한 번은 몇 분 정도 걸림
(x_train, t_train), (x_test, t_test) = \
	load_mnist(flatten=True, normalize=False)

# 각 데이터의 형상 출력
print(x_train.shape)
print(t_train.shape)
print(x_test.shape)
print(t_test.shape)
```

- MNIST 데이터셋을 내려받아 이미지를 넘파이 배열로 변환해주는 파이썬 스크립트

> `📝mnist.py`가 `📁dataset`에  있다고 가정한 스크립트

- `load_mnist`가 MNIST 데이터를 받아와야 하니 최초 실행 시에는 인터넷에 연결된 상태여야 한다. 두 번째부터는 로컬에 저장된 파일(pickle 파일)을 읽기 때문에 빨리 끝난다.

##### load_mnist
{: .no_toc }

###### return
{: .no_toc }

- 읽은 MNIST 데이터를 `(훈련 이미지, 훈련 레이블), (시험 이미지, 시험 레이블)` 형식으로 반환한다.

- 이미지, 레이블 각각은 `ndarray`

###### arguments
{: .no_toc }

- `normalize` : 입력 이미지의 픽셀값을 0.0~1.0 사이의 값으로 정규화할지 정한다.

	- `False`로 설정하면 입력 이미지 픽셀값 그대로 0~255 사이의 값 유지하고 `True`면 255로 나눠 0.0~1.0 범위로 변환한다.

- `flatten` : 입력이미지를 1차원 배열로 만들지 정한다.

	- `False`로 설정하면 입력 이미지를 $1 \times 28 \times 28$의 3차원 배열로, `True`로 설정하면 784개의 원소로 이루어진 1차원 배열로 저장

- `one_hot_label` : 레이블을 **one-hot encoding** 형태로 저장할지 정한다.

	- one-hot encoding : 정답을 뜻하는 원소만 1(hot)이고 나머지는 모두 0인 배열로 저장

	- `False`면 숫자 형태의 레이블을 저장하고 `True`일 때는 레이블을 원-핫 인코딩하여 저장

> 파이썬에는 pickle(피클)이라는 기능이 있다.
> 이는 프로그램 실행 중에 특정 객체를 파일로 저장하는 기능이다.
> 저장해둔 pickle 파일을 로드하면 실행 당시의 객체를 즉시 복원할 수 있다.
> MNIST 데이터셋르 읽는 `load_mnist` 함수에서도 (2번째 이후의 읽기 시) pickle을 이용한다.

```python
import numpy as np
from dataset.mnist import load_mnist
from PIL import Image	# 이미지 표시에 사용하는 모듈 PIL(Python Image Library)

def img_show(img):
	pil_img = Image.fromarray(np.uint8(img))
	pil_img.show()

(x_train, t_train), (x_test, t_test) = \
	load_mnist(flatten=True, normalize=False)

img = x_train[0]
label = t_train[0]
print(label)

print(img.shape)
img = img.reshape(28, 28) # 원래 이미지의 모양으로 변형
print(img.shape)

img_show(img)
```

- `flatten=True`로 설정해 이미지를 읽어들였기 때문에 이미지를 표시할 때는 원래 형상인 $28 \times 28$ 크기로 다시 변형해야 한다.

- `ndarray.reshape()` : 원하는 형상을 인수로 지정하면 넘파이 배열의 형상을 바꿀 수 있다.

- `Image.fromarray` : 넘파이로 저장된 이미지 데이터를 PIL용 데이터 객체로 변환

### 3.6.2 신경망의 추론 처리

- 입력층 뉴런 784개(이미지 크기 $28 \times 28$), 출력층 뉴런 10개(0~9 숫자 구분)

- 은닉층은 총 두 개

	- 임의로 첫 번째 은닉층에는 50개의 뉴런을, 두 번째 은닉층에는 100개의 뉴런을 배치할 것이다.

- github `WegraLee/deep-learning-from-scratch`의 `dataset/mnist.py`를 사용

```python
import numpy as np
import pickle
from dataset.mnist import load_mnist
from common.functions import sigmoid, softmax


def get_data():
	(x_train, t_train), (x_test, t_test) = \
		load_mnist(normalize=True, flatten=True, one_hot_label=False)
	return x_test, t_test

def init_network():
	with open("sample_weight.pkl", 'rb') as f:
		network = pickle.load(f)
	return network

def predict(network, x):
	W1, W2, W3 = network['W1'], network['W2'], network['W3']
	b1, b2, b3 = network['b1'], network['b2'], network['b3']

	a1 = np.dot(x, W1) + b1
	z1 = sigmoid(a1)
	a2 = np.dot(z1, W2) + b2
	z2 = sigmoid(a2)
	a3 = np.dot(z2, W3) + b3
	y = softmax(a3)

	return y

# 정확도(accuracy) 평가
x, t = get_data()
network = init_network()

accuracy_cnt = 0
for i in range(len(x)):
	y = predict(network, x[i])
	p = np.argmax(y)	# 확률이 가장 놓은 원소의 인덱스를 얻는다.
	if p == t[i]:
		accuracy_cnt += 1

print("Accuracy:" + str(float(accuracy_cnt) / len(x)))
```

- `init_network` : pickle 파일인 `📝sample_weight.pkl`에 저장된 학습된 가중치 매개변수를 읽는다.

	- github `WegraLee/deep-learning-from-scratch`의 `ch03/sample_weight.pkl` : 가중치와 편향 매개변수가 딕셔너리 변수로 저장되어 있다.

- 데이터를 특정 범위로 변환하는 처리를 **정규화**$^{\text{normalization}}$라고 하고, 신경망의 입력 데이터에 특정 변환을 가하는 것을 **전처리**$^{\text{pre-processing}}$라고 한다.

> 현업에서도 신경망(딥러닝)에 전처리를 활발히 사용한다. 전처리를 통해 식별 능력을 개선하고 학습 속도를 높일 수 있다. 앞의 예에서는 각 픽셀의 값을 255로 나누는 단순한 정규화를 수행했지만, 현업에서는 데이터 전체의 분포를 고려해 전처리하는 경우가 많다. 예를 들어 에이터 전체 평균과 표준편차를 이용하여 데이터들이 0을 중심으로 분포하도록 이동하거나 데이터의 확산 범위를 제한하는 정규화를 수행한다. 그 외에도 전체 데이터를 균일하게 분포시키는 데이터 **백색화**$^{\text{whitening}}$ 등도 있다.

### 3.6.3 배치 처리

- 입력 데이터와 가중치 매개변수의 형상에 주의해서 앞의 구현 다시 살펴보기

```python
# interpreter
x, _ = get_data()
network = init_network()
W1, W2, W3 = network['W1'], network['W2'], network['W3']
x.shape
x[0].shape
W1.shape
W2.shape
W3.shape
```

<div>
$$
X~~~~~~~~~~~~~~W1~~~~~~~~~~~~~~W2~~~~~~~~~~~~~~W3~~~~\rightarrow~~~~Y
$$
$$
{\color{red}\cancel{784}~~~\cancel{784}} \times {\color{green}\cancel{50}~~~\cancel{50}} \times {\color{blue}\cancel{100}~~~\cancel{100}} \times \color{black}{10~~~~~~~~~10}
$$
</div>

- 이미지 1장 입력했을 때 흐름

<div>
$$
X~~~~~~~~~~~~~~~~W1~~~~~~~~~~~~~~~~W2~~~~~~~~~~~~~~~~W3~~~~~~\rightarrow~~~~~~Y
$$
$$
100 \times {\color{red}\cancel{784}~~~\cancel{784}} \times {\color{green}\cancel{50}~~~\cancel{50}} \times {\color{blue}\cancel{100}~~~\cancel{100}} \times \color{black}{10~~~~~~~~~~100 \times 10}
$$
</div>

- 이미지 100장 입력했을 때 흐름

- 하나로 묶은 입력 데이터를 **배치**$^{\text{batch}}$라고 한다.

> 배치 처리는 이미지 1장당 처리 시간을 대폭 줄여준다. 배치 처리를 수행함으로써 큰 배열로 이뤄진 계산을 하게 되는데, 컴퓨터에서는 큰 배열을 한꺼번에 계산하는 것이 분할된 작은 배열을 여러 번 계산하는 것보다 빠르다.
> ##### 배치 처리가 더 빠른 이유
> {: .no_toc }
> - 수치 계산 라이브러리 대부분이 큰 배열을 효율적으로 처리할 수 있도록 고도로 최적화되어 있다.
> - 커다란 신경망에서는 데이터 전송이 병목으로 작용하는 경우가 자주 있는데, 배치 처리를 함으로써 버스에 주는 부하를 줄인다.
>	- 병목(bottleneck) 현상: 전체 시스템의 성능이나 용량이 하나의 구성요소로 인해 제한을 받는 현상
>	- 느린 I/O를 통해 데이터를 읽는 횟수가 줄어 빠른 CPU나 GPU로 순수 계산을 수행하는 비율이 높아진다.

```python
import numpy as np
import pickle
from dataset.mnist import load_mnist
from common.functions import sigmoid, softmax


def get_data():
	(x_train, t_train), (x_test, t_test) = \
		load_mnist(normalize=True, flatten=True, one_hot_label=False)
	return x_test, t_test

def init_network():
	with open("sample_weight.pkl", 'rb') as f:
		network = pickle.load(f)
	return network

def predict(network, x):
	W1, W2, W3 = network['W1'], network['W2'], network['W3']
	b1, b2, b3 = network['b1'], network['b2'], network['b3']

	a1 = np.dot(x, W1) + b1
	z1 = sigmoid(a1)
	a2 = np.dot(z1, W2) + b2
	z2 = sigmoid(a2)
	a3 = np.dot(z2, W3) + b3
	y = softmax(a3)

	return y

x, t = get_data
network = init_network()

batch_size = 100 # 배치 크기
accuracy_cnt = 0

for i in range(0, len(x), batch_size):
	x_batch = x[i:i+batch_size]
	y_batch = predict(network, x_batch)
	p = np.argmax(y_batch, axis=1)
	accuracy_cnt += np.sum(p == t[i:i+batch_size])

print("Accuracy:" + str(float(accuracy_cnt) / len(x)))
```

- `ndarray.argmax`의 argument `axis` : 지정된 차원의 최댓값 인덱스를 반환한다.

##### 동작 확인
{: .no_toc }

```python
# interpreter
x = np.array([[0.1, 0.8, 0.1], [0.3, 0.1, 0.6], [0.2, 0.5, 0.3], [0.8, 0.1, 0.1]])
y = np.argmax(x, axis=1)
print(y)
```

```python
# interpreter
y = np.array([1, 2, 1, 0])
t = np.array([1, 2, 0, 0])
print(y==t)
np.sum(y==t)
```

---

## 3.7 정리

### 이번 장에서 배운 내용

- 신경망에서는 활성화 함수로 시그모이드 함수와 ReLU 함수 같은 매끄럽게 변화하는 함수를 이용한다.

- 넘파이의 다차원 배열을 잘 사용하면 신경망을 효율적으로 구현할 수 있다.

- 기계학습의 문제는 크게 회귀와 분류로 나눌 수 있다.

- 출력층의 활성화 함수로는 회귀에서는 주로 항등 함수를, 분류에서는 주로 소프트맥스 함수를 이용한다.

- 분류에서는 출력층의 뉴런 수를 분류하려는 클래스 수와 같게 설정한다.

- 입력 데이터를 묶은 것을 배치라 하며, 추론 처리를 이 배치 단위로 진행하면 결과를 훨씬 빠르게 얻을 수 있다.
