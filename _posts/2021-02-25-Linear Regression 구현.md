---
layout: post
title: "Linear Regression 구현"
date: 2021-02-25
excerpt: "Linear Regression 구현"
tag:
- Ai
- Math
- Gradient Descent
category: [ Artificial Intelligence ]
feature: ../assets/img/title/basic.jpg
comments: true
---

## LinearRegression 구현

[LinearRegression 시각화 글](https://shsongs.github.io/Linear-Regression/)  
[Github Source](https://github.com/SHSongs/MinimalAI/tree/main/AI/Linear%20regression)

### 선행지식 : 기울기 (수치미분), numpy 기초

저번글에서는 선형회귀를 시각화해보았다면 이번글은 python을 이용해 선형회귀를 구현해본다.  



일단 실제(정답) 데이터를 만들어준다.
```python
x_train = np.array([0, 1, 2, 3, 4])
y_train = np.array([0, 1, 2, 3, 4])
```
그리고 y를 예측하기 위해서는 w와 b가 필요하다 (y = w*x + b)
```python
weight = 0.0
bias = 0.0
```

그리고 학습속도를 조절과 몇번 학습할지도 있어야한다.
```python
learning_rate = 0.01 # 학습비율
epochs = 1000 # 몇번 학습할것인지
```

epochs = 1000 이라고 했는데 같은 데이터를 1000번 학습한다는 것이다.  



이제 학습을 위한 준비는 끝났다. epochs 만큼 반복문을 돌려서 학습을 하면 된다.

```python
for i in range(epochs):
    풀기()
    확인하기()
    배우기()
```

일단 배우기 전에 자신이 알고있는 지식으로 문제를 풀어 봐야한다. 
```python
def 풀기():
    h = 0.001

    hypothesis = x_train * W + b # 가설

    hypothesis_w_up = x_train * (W + h) + b    
    hypothesis_w_down = x_train * (W - h) + b

    hypothesis_b_up = x_train * W + (b + h)
    hypothesis_b_down = x_train * W + (b - h)

```
행렬연산으로  
hypothesis의 형태는 [?, ?, ?, ?, ?]  
이 된다.  
여기서 왜 h를 w와 b별로 더하고 빼는지 의문이 들 수 있는데 그래프를 봐보자  

<img src="/Images/AI/LRV/06_0.png" height="400">  

이 그래프를 보면 w와 b의 값에 따른 기울기를 알기 위해 구한다.


이제 푼 문제가 정답과 얼마나 유사한지 확인해야 한다.
```python
def 확인하기():
    cost = np.sum((hypothesis - y_train) ** 2) / n_data

    cost_w_up = np.sum((hypothesis_w_up - y_train) ** 2) / n_data
    cost_b_up = np.sum((hypothesis_b_up - y_train) ** 2) / n_data

    cost_w_down = np.sum((hypothesis_w_down - y_train) ** 2) / n_data
    cost_b_down = np.sum((hypothesis_b_down - y_train) ** 2) / n_data
```
cost = 각 데이터별 거리의 합 / 데이터의 개수  
마찬가지로 w와 b 따로 cost(loss)를 구해준다.

그리고 배워야한다. 
```python
def 배우기():
    numerical_grad_w = (cost_w_up - cost_w_down) * 2 / h
    numerical_grad_b = (cost_b_up - cost_b_down) * 2 / h

    W -= learning_rate * numerical_grad_w
    b -= learning_rate * numerical_grad_b

```
w와 b 별로 기울기를 후한 후 w와 b에 learning_rate만큼 적용시켜준다.


### 문제점
이런식으로 파라미터(여기서는 w,b)마다 수치미분으로 loss를 구해주면 느리기때문에 다음글에서는 오차 역전파법을 통해 고속으로 구해보자  



## 전체코드

[Github Source](https://github.com/SHSongs/MinimalAI/tree/main/AI/Linear%20regression)

```python
import numpy as np
import matplotlib.pyplot as plt

x_train = np.array([1., 2., 3., 4., 5., 6.])
y_train = np.array([5., 14., 20., 34., 35., 40.])

W = 0.0
b = 0.0

n_data = len(x_train)

epochs = 1000
learning_rate = 0.01

for i in range(epochs):
    h = 0.001

    hypothesis = x_train * W + b
    cost = np.sum((hypothesis - y_train) ** 2) / n_data

    hypothesis_w_up = x_train * (W + h) + b
    hypothesis_b_up = x_train * W + (b + h)

    hypothesis_w_down = x_train * (W - h) + b
    hypothesis_b_down = x_train * W + (b - h)

    cost_w_up = np.sum((hypothesis_w_up - y_train) ** 2) / n_data
    cost_b_up = np.sum((hypothesis_b_up - y_train) ** 2) / n_data

    cost_w_down = np.sum((hypothesis_w_down - y_train) ** 2) / n_data
    cost_b_down = np.sum((hypothesis_b_down - y_train) ** 2) / n_data

    numerical_grad_w = (cost_w_up - cost_w_down) * 2 / h
    numerical_grad_b = (cost_b_up - cost_b_down) * 2 / h

    W -= learning_rate * numerical_grad_w
    b -= learning_rate * numerical_grad_b

    if i % 100 == 0:
        print('Epoch ({:10d}/{:10d}) cost: {:10f}, W: {:10f}, b:{:10f}'.format(i, epochs, cost, W, b))

print('W: {:10f}'.format(W))
print('b: {:10f}'.format(b))
print('result : ')
print(x_train * W + b)

x_predict = np.array(list(range(1, 7)))
y_predict = x_predict * W + b

plt.plot(x_train, y_train, 'or', label='origin data')
plt.plot(x_predict, y_predict, 'b', label='predict')
plt.legend(['origin', 'predict'])
plt.show()
```










