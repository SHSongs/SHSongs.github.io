---
layout: post
title: "Time Of Crime"
date: 2021-04-08
excerpt: "간단한 경찰청 범죄통계 분석 과정"
tag:
- Data analysis
category: [ Artificial Intelligence ]
feature: ../assets/img/title/basic.jpg
comments: true
---

[경찰범죄통계 사이트](https://www.police.go.kr/www/open/publice/publice03_2018.jsp)

pandas를 이용해 경찰청에서 제공하는 data 분석을 하였다  

pandas를 오랜만에 사용하다 보니 여러 부분에서 막혀서 막힌 부분들을 정리해둔다.  

일단 데이터가 적기에 CSV 파일을 필요한 부분만 가공한 후 pandas를 이용해 DataFrame을 만들었다.  
![](/Images/AI/TimeOfCrime/01_Data.jpg)  

여기서 최종별(2)가 '소계'인 행만 빼내 새로운 판다스 프레임을 만들고 싶다.  

---------------
```py
is_subtotal = df['죄종별(2)'] == '소계'
```
이러면 '소계'이면 true 아니면 false인 Series 반환
![](/Images/AI/TimeOfCrime/02_01.jpg)  

----------------

```py
sub_total = df[is_subtotal]
```
![](/Images/AI/TimeOfCrime/03_01.jpg)  

sub_total <- 이거 이름 바꾸기 
에는 '소계'만 있는 게 나온다.  

하지만 
인덱스가 이상하게 되어서 for i in range를 이용해 인덱스를 순차적으로 접근하면 에러가 난다.   
```
for i in range(1, time.shape[0]):
    y_train = time.loc[i]
```
![](/Images/AI/TimeOfCrime/03_02.jpg)  

--------------------
reset_index 를 사용해 인덱스를 순차적으로 바꿔주자
![](/Images/AI/TimeOfCrime/04_01.jpg)  


```py
for i in range(1, time.shape[0]):
    y_train = time.loc[i]
    nameList.append(str(crimeClass.loc[i,'죄종별(1)']))
    plt.plot(x_train, y_train)

plt.legend(nameList, bbox_to_anchor=(1.05, 1), loc='upper left')
plt.xlabel('Time of crime')
plt.ylabel('Number of crimes')
plt.show()
```
![](/Images/AI/TimeOfCrime/04_02.png)    

-----------------

전체소스  
```py
import pandas as pd
import numpy as np
import matplotlib as mpl
import matplotlib.pyplot as plt

# 그래프에서 마이너스 폰트 깨지는 문제에 대한 대처
mpl.rcParams['axes.unicode_minus'] = False
plt.rcParams["font.family"] = 'NanumBarunGothic'

crimeData = pd.read_csv('CrimeTime.csv')
print(crimeData)

is_subTotal = crimeData['죄종별(2)'] == '소계'
print(is_subTotal)
print(type(is_subTotal))
subTotal = crimeData[is_subTotal]
print(subTotal)
print(type(subTotal))

time = subTotal.iloc[:, 2:6]
print(time)
time = time.reset_index()
time = time.drop(columns='index')
print(time)

crimeClass = subTotal.iloc[:, 0].reset_index().drop(columns='index').astype('str')

x_train = np.array([12, 15, 18, 21])
nameList = []
for i in range(1, time.shape[0]):
    y_train = time.loc[i]
    nameList.append(str(crimeClass.loc[i, '죄종별(1)']))
    plt.plot(x_train, y_train)

plt.legend(nameList, bbox_to_anchor=(1.05, 1), loc='upper left')
plt.xlabel('Time of crime')
plt.ylabel('Number of crimes')
plt.show()
```