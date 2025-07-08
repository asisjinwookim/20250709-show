---
# You can also start simply with 'default'
theme: seriph
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: https://cover.sli.dev

# some information about your slides (markdown enabled)
title: Welcome to Slidev
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
# apply unocss classes to the current slide
class: text-center
# https://sli.dev/features/drawing
drawings:
  persist: false
# slide transition: https://sli.dev/guide/animations.html#slide-transitions
transition: false
footer: '{{page}} / {{total}}'
# enable MDC Syntax: https://sli.dev/features/mdc
mdc: true
# open graph
# seoMeta:
#  ogImage: https://cover.sli.dev
fonts:
  # like font-family in css, you can use `,` to separate multiple fonts for fallback
  sans: 'Helvetica Neue,Robot'
  # mark 'Helvetica Neue' as local font
  local: Helvetica Neue
layout: cover
---

# 태맬옵스: 태어난 김에 MLOps

**일단 <font color="blue">부딪히고</font> 보자**

2025

asisjinwookim

---
layout: default
---

# 본 세션은 핸즈온 세션입니다

* 노트북을 준비해주세요!

---
layout: default
---
<img src="https://i.namu.wiki/i/hdv09iHewp1AZUf1KTi5ND6tPOUDj5aRsafP7cwSG2V7Q0rUJmTrkLmWqrEFMWQEq4LS5IkHhJxi-kC9QdLIVw.webp" style="width: 300px; height: 350px">

* '[태어난 김에 세계일주](https://namu.wiki/w/%ED%83%9C%EC%96%B4%EB%82%9C%20%EA%B9%80%EC%97%90%20%EC%84%B8%EA%B3%84%EC%9D%BC%EC%A3%BC)'라는 프로그램이 있어요.
* 여행지 하나 골라서 무작정 떠나는 프로그램
* 우리도 <font color="blue">AI, MLOps</font>, 잘 모르지만 <font color="red">일단 시작해봅시다</font>

---
layout: default
---

# 뭐부터 해볼까요?

* 데이터 과학자가 다루는 일이 무엇일까요?
* 직접 문제를 풀어보는 겁니다
## 풀어보자 <font color="red">Kaggle!</font>

---
layout: default
---

# 환경 셋업부터 - conda

[https://www.anaconda.com/download/success](https://www.anaconda.com/download/success)

* Command

```sh
$ conda
usage: conda [-h] [-v] [--no-plugins] [-V] COMMAND ...

conda is a tool for managing and deploying applications, environments and packages.
```

* Usage
```sh
# environment.yml로부터 conda 환경 셋업
conda env create -f environment.yml

# environment.yml로부터 conda 환경 업뎃
conda env update -f environment.yml

# 환경 활성화
conda activate {env_name}
```

---
layout: default
---

# Titanic 생존 예측 - 1

* Titanic 문제는 Kaggle의 대표적인 입문 문제
* 데이터 정제와 feature(특성) 엔지니어링, 머신러닝 기법을 두루 실습해볼 수 있음

---
layout: default
---

# Titanic 생존 예측 - 2
* **배경:** 1912년 침몰한 타이타닉호 탑승자 데이터를 기반으로 생존 여부를 예측하는 Kaggle 경진대회 문제.
* **목표:** 주어진 승객 정보를 활용하여 각 승객의 생존(Survived) 여부(0: 사망, 1: 생존)를 예측하는 분류 모델을 개발.
* [링크](https://www.kaggle.com/competitions/titanic)
* **데이터:**
    * `train.csv`: 모델 학습을 위한 훈련 데이터셋. `Survived` 컬럼 포함.
    * `test.csv`: 예측 결과를 제출하기 위한 테스트 데이터셋. `Survived` 컬럼 없음.

---
layout: default
---

# 일단 따라하기 - Titanic with Jupyter Notebook

* 예제를 준비했습니다.
* [20250709-titanic](https://github.com/studyteams/20250709-titanic/blob/main/README.md)
* '1. 개발 환경 설정'부터 '17. 최종 예측 및 제출 파일 생성'까지 <font color="green">핸즈온!</font>
* '개선된 모델'은 쓱 읽어보기

---
layout: default
---

# 데이터 탐색 (EDA) - 1

* **데이터 미리보기 및 기본 정보 확인**
    * `train_df.head()`:
        * PassengerId: 승객 고유 ID
        * Survived: 생존 여부 (0=사망, 1=생존) - **타겟 변수**
        * Pclass: 티켓 등급 (1=1등석, 2=2등석, 3=3등석)
        * Name: 승객 이름
        * Sex: 성별
        * Age: 나이
        * SibSp: 함께 탑승한 형제/배우자 수
        * Parch: 함께 탑승한 부모/자녀 수
        * Ticket: 티켓 번호
        * Fare: 요금
        * Cabin: 객실 번호
        * Embarked: 승선 항구 (C=Cherbourg, Q=Queenstown, S=Southampton)
---
layout: default
---

# 데이터 탐색 (EDA) - 2

* **데이터 미리보기 및 기본 정보 확인**
    * `train_df.info()` 및 `test_df.info()`: 데이터 타입 및 결측치 확인
        * **훈련 데이터셋 결측치**: `Age` (177개), `Cabin` (687개), `Embarked` (2개)
        * **테스트 데이터셋 결측치**: `Age` (86개), `Fare` (1개), `Cabin` (327개)
    * `train_df.describe()`: 수치형 데이터의 기술 통계량 확인

---
layout: default
---

# 데이터 탐색 (EDA) - 3
**`Survived` 컬럼 분포**
* 생존자와 사망자 비율을 한눈에 파악.

**`Pclass`와 `Survived` 관계**
* 티켓 등급이 높을수록 생존율이 높을까? (1등석 > 2등석 > 3등석)

**`Sex`와 `Survived` 관계**
* 여성의 생존율이 남성보다 높을까?

**`Age` 분포**
* 나이 분포를 통해 데이터의 특성 확인. 결측치 존재하는지?

---
layout: default
---

# kaggle에 제출!

<img src="./img/kaggle_submit.png" style="width: 300px; height: 300px;">

* 점수가 나와요

---
layout: default
---

# 실험 건마다의 결과를 어떻게 알지?

* 패키지 버전, 코드 로직, 데이터, 피처가 달라진 걸 비교하고 싶은데?
* Titanic 문제를 [mlflow](https://mlflow.org/)로 관리해 보자

---
layout: default
---

# 일단 따라하기2 - Titanic with MLFlow

* 예제를 준비했습니다.
* [20250709-titanic-mlflow](https://github.com/studyteams/20250709-titanic-mlflow/blob/main/README.md)
* '1. 환경 설정'부터 '4. MLflow UI에서 결과 확인'까지 <font color="green">핸즈온!</font>

---
layout: two-cols
---

# 이미지

* 실험 목록
<img src="./img/mlflow_experiments.png" style="width: 350px; height: 250px;">

::right::
* 실험 디테일
<img src="./img/mlflow_exp_result.png" style="width: 250px; height: 400px;">

---
layout: default
---

# MLFlow on Localhost

```sh
conda activate titanic_mlflow
mlflow ui --port 5050
```

[MLFlow on Localhost](http://localhost:5050)

