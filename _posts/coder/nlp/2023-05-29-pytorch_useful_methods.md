---
layout: post
title: PyTorch 유용한 함수들
categories: [coder, nlp]
tags:       [coder, nlp]
description: >
  Pytorch로 시작하는 딥러닝 입문 (2/2)
---
- Table of Contents
{:toc .large-only}

### Useful Methods
```python
import torch

# expand - 주어진 tensor를 복사후 concate
x = torch.FloatTensor([[[1, 2]],
                       [[3, 4]]])
x.size()               # torch.Size([2, 1, 2])

y = x.expand(*[2, 3, 2])
y.size()               # torch.size([2, 3, 2])

y = torch.cat([x, x, x], dim=1)
y.size()               # torch.size([2, 3, 2])


# randperm - 랜덤 함수, index_select와 활용
rt = torch.randperm(10)
rt.size()                # torch.Size([10])
print(rt)                # tensor([1, 9, 6, 4, 0, 7, 3, 5, 2, 8])
 

# argmax - 최대값을 가지고 있는 index를 반환
x = torch.randperm(3**3).reshape(3, 3, -1)
y = x.argmax(dim = -1)

y.size()                    # torch.Size([3, 3])


# topk - topk와 해당 index를 반환 
values, indices = torch.topk(x, k = 1, dim = -1)
values.size()               # torch.Size([3, 3, 1])

values.squeeze(-1).size()   # torch.Size([3, 3])

x.argmax(dim = -1) == indices.squeeze(-1)   # True

values, indices = torch.topk(x, k = 2, dim = -1)
values.size()               # torch.Size([3, 3, 2])


# 정렬하기1 - topk로 정렬
target_dim = -1
values, indices = torch.topk(x, k = x.size(target_dim), largest = True)

# 정렬하기2 - sort로 정렬
values, indices = torch.sort(x, dim = -1, descending = True)


# masked_fill - mask 처리한 곳(True) 채우기
x = torch.FloatTensor([i for i in range(3**2)]).reshape(3, -1)
x.size()                    # torch.Size([3, 3])

mask = x > 4
print(mask)                 # tensor([[False, False, False],
                            #         [False, False,  True],
                            #         [ True,  True,  True]])

y = x.masked_fill(mask, value = -1)
print(y)                    # tensor([[ 0.,  1.,  2.],
                            #         [ 3.,  4., -1.],
                            #         [-1., -1., -1.]])


# Ones and Zeros
torch.ones(2, 3)
torch.zeros(2, 3)

# (기존 Tensor와 연산하기 위해선 아래 방법이 더 유용함)
x = torch.FloatTensor([[1, 2, 3],
                       [4, 5, 6]])
x.size()                    # torch.Size([2, 3])

torch.ones_like(x)          # torch.ones(2, 3)
torch.zeros_like(x)         # torch.zeros(2, 3)
```