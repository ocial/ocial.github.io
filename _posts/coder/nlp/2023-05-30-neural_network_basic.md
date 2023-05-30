---
layout: post
title: 신경망의 기본 구성요소
categories: [coder, nlp]
tags:       [coder, nlp]
description: >
  Neural Network basic
---
- Table of Contents
{:toc .large-only}

### Matrix Multiplication

```python
import torch
import torch.nn as nn

x = torch.FloatTensor([[1, 2],
                       [3, 4],
                       [5, 6]])
y = torch.FloatTensor([[1, 2],
                       [1, 2]])

x.size(), y.size()      # torch.Size([3, 2]), torch.Size([2, 2])

z = torch.matmul(x, y)
z.size()                # torch.Size([3, 2])


x = torch.FloatTensor([[[1, 2],
                        [3, 4],
                        [5, 6]],
                       [[7, 8],
                        [9, 10],
                        [11, 12]],
                       [[13, 14],
                        [15, 16], 
                        [17, 18]]])
y = torch.FloatTensor([[[1, 2, 2],
                        [1, 2, 2]],
                       [[1, 3, 3],
                        [1, 3, 3]],
                       [[1, 4, 4],
                        [1, 4, 4]]])

x.size(), y.size()      # torch.Size([3, 3, 2]) torch.Size([3, 2, 3])

z = torch.bmm(x, y)     # batch matrix multiplication
z.size()                # torch.Size([3, 3, 3])
```


### How to use GPU

```python
# Convert CUDA tensor - cuda()
x = torch.cuda.FloatTensor(2, 2)
x           # tensor([[0., 0.],
            #         [0., 0.]], device='cuda:0')

x = torch.FloatTensor(2, 2)

d = torch.device('cuda:0')

x = x.cuda(device=d)
x           # tensor([[0., 0.],
            #         [0., 0.]], device='cuda:0')

x.device    # device(type='cuda', index=0)


# Convert CUDA tensor - to()
d = torch.device('cpu')
x = x.to(device=d)          # x = x.cpu()
x           # tensor([[0., 0.],
            #         [0., 0.]])


# Move model from CPU to GPU
linear = nn.linear(2, 2)

linear = linear.cuda()

linear = linear.cpu()

d = torch.device('cuda:0')
linear = linear.to(d)

p = next(linear.parameters())
p.device                    # device(type='cuda', index=0)

list(linear.parameters())   # iteration
```
