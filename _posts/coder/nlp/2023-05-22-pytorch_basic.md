---
layout: post
title: PyTorch 기본
categories: [coder, nlp]
tags:       [coder, nlp]
description: >
  Pytorch로 시작하는 딥러닝 입문
---
- Table of Contents
{:toc .large-only}

### 텐서 조작하기
```python
import torch
import numpy as np

# 1차원 텐서, 벡터
t = torch.FloatTensor([0., 1., 2., 3., 4., 5., 6.])

t.dim()   # 1 (rank, 차원)
t.size()  # torch.Size([7]) (shape)


# 2차원 텐서, 행렬
t = torch.FloatTensor([[1., 2., 3.],
                       [4., 5., 6.],
                       [7., 8., 9.],
                       [10., 11., 12.]
                      ])

t.dim()   # 2 (rank, 차원)
t.size()  # torch.Size([4, 3]) (shape)
t[:, 1]   # tensor([2., 5., 8., 11.[) (모든 행, 인덱스가 1인 열)


# 브로드캐스팅
m1 = torch.FloatTensor([[1, 2]])
m2 = torch.FloatTensor([3])       # [3] -> [3, 3]
print(m1 + m2)                    # tensor([[4., 5.]])


# 차원 변경 뷰(View)
t = np.array([[[0, 1, 2],
               [3, 4, 5]],
              [[6, 7, 8],
               [9, 10, 11]]])
ft = torch.FloatTensor(t)

ft.shape                    # torch.Size([2, 2, 3])
ft.view([-1, 3]).shape      # torch.Size([4, 3])
ft.view([3, -1]).shape      # torch.Size([3, 4])
ft.view([-1, 1, 3]).shape   # torch.Size([4, 1, 3]) 


# 1인 차원 제거 스퀴즈(Squeeze)
ft = torch.FloatTensor([[0], [1], [2]])

ft.shape              # torch.Size([3, 1])
ft.squeeze().shape    # torch.Size([3])


# 타입 캐스팅
lt = torch.LongTensor([1, 2, 3, 4])   # long 타입
lt.float()                            # float 타입 tensor([1., 2., 3., 4.])

bt = torch.ByteTensor([True, False, False, True])
bt          # tensor([1, 0, 0, 1], dtype=torch.unit8)
bt.long()   # tensor([1, 0, 0, 1])


# 연결하기(concatenate)
x = torch.FloatTensor([[1, 2], [3, 4]])
y = torch.FloatTensor([[5, 6], [7, 8]])

torch.cat([x, y], dim=0)
# tensor([[1., 2.],
#         [3., 4.],
#         [5., 6.],
#         [7., 8.]])

torch.cat([x, y], dim=1)
# tensor([[1., 2., 5., 6.],
#         [3., 4., 7., 8.]])

x = torch.FloatTensor([1, 4])
y = torch.FloatTensor([2, 5])
z = torch.FloatTensor([3, 6])

torch.stack([x, y, z])
# tensor([[1., 4.],
#         [2., 5.],
#         [3., 6.]])

torch.stack([x, y, z], dim=1)
# tensor([[1., 2., 3.],
#         [4., 5., 6.]])


# 0 or 1로 채워진 텐서
x = torch.FloatTensor([[0, 1, 2], [2, 1, 0]])

torch.ones_like(x)
# tensor([[1., 1., 1.],
#         [1., 1., 1.]])

torch.zeros_like(x)
# tensor([[0., 0., 0.],
#         [0., 0., 0.]])


# 덮어쓰기 연산
x = torch.FloatTensor([[1, 2], [3, 4]])

x.mul(2.)
x         # tensor([[1., 2.], [3., 4.]])

x.mul_(2.)
x         # tensor([[2., 4.], [6., 8.]])
```