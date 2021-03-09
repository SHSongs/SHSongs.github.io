---
layout: post
title: "Convolution To Flatten"
date: 2021-02-04
excerpt: ""
tag:
- basic
category: [ Artificial Intelligence ]
feature: ../assets/img/title/basic.jpg
comments: true
---


CNN model 을 만들때 Conv layer 를 Flatten layer 로 통과시키기 위해  
행렬 변환을 해야된다 (1차원으로)  

이때 어떻게 변환해야 될지 헷갈릴 수 있다.  
[Pytorch KR Classifier tutorial](https://tutorials.pytorch.kr/beginner/blitz/cifar10_tutorial.html#sphx-glr-beginner-blitz-cifar10-tutorial-py)

```python
import torch.nn as nn
import torch.nn.functional as F


class Net(nn.Module):
    def __init__(self):
        super(Net, self).__init__()
        self.conv1 = nn.Conv2d(3, 6, 5)
        self.pool = nn.MaxPool2d(2, 2)
        self.conv2 = nn.Conv2d(6, 16, 5)
        self.fc1 = nn.Linear(16 * 5 * 5, 120)
        self.fc2 = nn.Linear(120, 84)
        self.fc3 = nn.Linear(84, 10)

    def forward(self, x):
        x = self.pool(F.relu(self.conv1(x)))
        x = self.pool(F.relu(self.conv2(x)))
        x = x.view(-1, 16 * 5 * 5)
        x = F.relu(self.fc1(x))
        x = F.relu(self.fc2(x))
        x = self.fc3(x)
        return x


net = Net()
```

위 코드는 Pytorch Classifier tutorial의 모델 생성 부분인데
```python
x = x.view(-1, 16 * 5 * 5)
```
딥러닝에 막 입문한 사람은 왜 이렇게 변환해야 되는지 모를 수 있다.

이유는 간단하다.  
[1, 3, 32, 32] 의 이미지를 Model 에 넣으면  
마지막 Conv 에서는 [1, 16, 5, 5]  
이를 x.view(-1, 16 * 5 * 5) 후에는  
[1, 400] 이런 형태가 된다  
  

  

<figure class="half">
    <a href="/Images/AI/DataTransform.PNG"><img src="/Images/AI/DataTransform.PNG"></a>
    <a href="/Images/AI/Data_flatten.PNG"><img src="/Images/AI/Data_flatten.PNG"></a>
    <figcaption>참고자료</figcaption>
</figure>

model 의 forward 부분에 data 의 size 를 직접 출력해 볼 수도 있다.
```python
def forward(self, x):
    x = self.pool(F.relu(self.conv1(x)))
    x = self.pool(F.relu(self.conv2(x)))
    print(x.size())
    x = x.view(-1, 16 * 5 * 5)
    print(x.size())
    x = F.relu(self.fc1(x))
    x = F.relu(self.fc2(x))
    x = self.fc3(x)
    return x

net = Net()
net(torch.randn(1 ,3, 32, 32))

# result
# torch.Size([1, 16, 5, 5])
# torch.Size([1, 400])
```

[1, 16, 5, 5] 의 2, 3, 4의 값을 곱한 값으로 변환 시키면 된다.  
(첫번째 값은 배치 데이터)  


```python
x = x.reshape(x.shape[0], -1)
```
아니면 배치데이터의 크기를 이용해 변환시킬 수도 있다.
