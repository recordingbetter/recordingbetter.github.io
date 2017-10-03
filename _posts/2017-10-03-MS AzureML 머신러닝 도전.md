---
title: MS AzureML 머신러닝 도전
slug: MS AzureML 머신러닝 도전
layout: post
categories: ML
---

추석을 맞아 머신러닝 모임인 싸이버스에서 주최한 츄파츄파(추석 파이썬) 스터디에 참가했다.
Microsoft의 Azure Machine Learning에 대한 발표를 들었고 흥미가 생겼다. (해야할 것이 백만개인데...)

데이터를 가지고 이리저리 분석한 다음 원하는 값을 예측할 수 있는 로직을 만들고 그것을 검증하여 예측된 값과 실제 값이 얼마나 일치하는지가 평가의 척도인듯 하다.(케글 등...)

나는 AWS를 많이 이용하는 중이라 찾아보니 AWS의 Machine Learning은 무료 체험이 없다. ㅠㅠ

![]({{ site.rooturl }}/images/MS AzureML-01.png)

Microsoft의 Azure Machine Learning은 테스트(실험) 용도로는 무료 제공하고 있다. 게다가 마치 스크래치처럼 블럭 형식으로 만들 수 있다.
그런 이유때문인지 머신러닝 쪽은 Azure를 많이 사용하는 경향이라고 한다.

## Experiment 해보기

### 1. Experiment 생성

![]({{ site.rooturl }}/images/MS AzureML-02.png)

#### Microsoft Azure Machine Learning Studio에서 `EXPERIMENTS`에서 `NEW` 선택

<br>
<br>

### 2. Dataset 불러오기

![]({{ site.rooturl }}/images/MS AzureML-03.png)

#### 오른쪽 메뉴에서 `Saved Datasets > Samples`에서 데이터셋을 선택하여 드래그한다.

데이터셋 샘플 종류가 많이 제공된다.


<br>
<br>

### 3. 데이터 전처리

![]({{ site.rooturl }}/images/MS AzureML-04.png)

#### `Data Transformation`에서 데이터를 처리할 방법과 옵션을 선택한다.

내가 예측하고자 하는 데이터(목적)을 먼저 정해야 한다.
데이터의 내용에 따라 처리하는 과정이 달라질 수 있다. 
데이터 내용의 도메인 지식이 있으면 작업하기 좋다고 한다.(당연...)

데이터를 처리하는 방법은 생각보다 엄청 많았고 통계학 지식이 있어야 할 것 같다.(공부할거 추가)

<br>
<br>


#### 데이터 전처리 후 트레이닝을 진행한다고 한다. 하지만 오늘은 전처리만 공부했음.

#### 주어진 데이터에서 70%는 트레이닝에 사용하고 30%는 트레이닝된 데이터를 검증, 비교하는데 사용하여 얼마나 일치하는지 확인.


<br>
<br>




