---
layout: default
title: Ch2 파이썬으로 시작하는 인공지능
parent: AI
grand_parent: School Lecture
nav_order: 2
mathjax: true
mermaid: true
permalink: /docs/ai/ch2
---

# Ch2 파이썬으로 시작하는 인공지능
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

- 인공지능은 진입장벽이 낮은 편이지만 갈수록 많은 노력이 필요

---

## 2.2 두 가지 프로그래밍 환경

- 클라우드 방식과 스탠드 얼론 방식

### 2.2.1 클라우드 방식과 스탠드얼론 방식

- 클라우드 방식

	- 프로그램과 데이터가 서버에 저장되고 관리

	- 구글의 Colab, 아마존의 SageMaker, 마이크로소프트의 Azure

- 스탠드얼론 방식

	- 자신에 최적인 환경 구축 가능. 프로그램과 데이터가 자신의 컴퓨터에 저장

---

## 2.3 영리한 프로그래밍 환경

- 라이브러리 충돌 가능성

- 가상환경 설치

	- 프로젝트 별로 별도의 가상 환경을 만들어 일관된 환경 유지

---

## 2.4 인공지능 프로그래밍 예제 1: 셈 지능

- 하드웨어에 내장된 기능 사용하여 빠르고 정확

---

## 2.5 인공지능 프로그래밍 예제 2: 인공지능 기자

- 뉴스 기사를 자동으로 작성하는 인공지능

- 분기문, 랜덤 선택 사용

---

## 2.6 인공지능 프로그래밍 예제 3: 더 똑똑한 인공지능 기자

- 언어 처리 라이브러리를 활용

	- TTS(text-to-speech) 기능 활용(gtts 라이브러리)

### 2.6.1 모듈 설치

```shell
pip install gits playsound
```

### 2.6.2 TTS 프로그래밍

```python
from gtts import gtts import gTTS
import playsound

tts = gTTs(text=news, lang="ko")  // 문자열 news를 위한 한국어 옵션 설정
tts.save("new_Son.mp3", TRUE);
playsound.playsound("news_Son.mp", True);
```

---

## 2.7 인공지능 프로그래밍을 위한 파이썬 기초

- 인공지능 프로그래밍에 주로 사용하는 라이브러리

- 파이썬 객체지향 특성과 사용법

### 2.7.1 인공지능 개발에 많이 쓰는 라이브러리

- Numpy

- Matplotlib: machine learning, visualization

- Scikit-learn: machine learning

- TensorFlow, Keras: deep learning, 개발

- PyTorch: deep learning, 연구

### 2.7.2 객체지향 언어를 이용한 인공지능 프로그래밍

- 파이썬 코딩 절차

	1. 모듈에서 클래스를 불러온다.

	2. 클래스의 객체(인스턴스 변수)를 만든다.

	3. 객체의 함수를 호출해 원하는 과업을 달성한다.

---

## Summary

- 프로그래밍 준비

	- 클라우드(colab) vs. 스탠드얼론(local)

- AI 프로그래밍 예시

	- 속도, 자동화

	- 분기문
