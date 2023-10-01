---
layout: post
title: Python 생산성 향상을 위한 지름길
categories: [coder, python]
tags:       [coder, python]
description: >
  지름길, 커맨드 라인, 그리고 패키지
---
- Table of Contents
{:toc .large-only}

### for문에서 번호를 생성하거든 enumerate 함수를 사용하는 것이 더 좋다.
```python
# 안좋은 예시
beat_list = ['John', 'Paul', 'George', 'Ringo']
for i in range(len(beat_list)):
    print(i, '. ', beat_list[i])

# 좋은 예시
beat_list = ['John', 'Paul', 'George', 'Ringo']
for i, name in enumerate(beat_list, 1):
    print(i, '. ', name)
```

### 다중 대입 / 튜플 대입을 사용한다.
```python
# 다중 대입
a = b = c = d = e = 0

# 튜플 대입
a, b = 1, 0

def fibo(n):
    a, b = 1, 0

    while a <= n:
        print(a, end= ' ')
        a, b = a + b, a

# 고급 튜플 대입
a, *b = 2, 4, 6, 8  # a = 2, b = [4, 6, 8]
```

### 리스트와 문자열 '곱하기'를 사용한다.
```python
my_list = [0] * 1000

trip_list = [1, 2, 3] * 100
len(trip_list)  # 300

divider_str = '_' * 40
```

### 루프와 else 키워드를 사용한다.
```python
# 루프와 else는 try-except 문법으로 사용될 수 있다.
# 루프와 함께 사용한 else는 루프가 break 문을 만나서 일찍 빠져나오지 않았을 때 실행된다.
def find_divisor(n, max):
    for i in range(2, max + 1):
        if n % i == 0:
            print(i, '은/는', n, '의 약수이다.')
            break
    else:
        print('약수를 찾지 못했습니다.')
```

### 불리언과 'not'의 이점을 활용한다.
```python
# 안좋은 예시
if len(my_str) == 0:
    break

# 좋은 예시
if not my_str:
    break
```

### 연결된 비교 연산자를 사용한다.
```python
a, b, c = 5, 10, 15
if 0 < a <= c > b > 1:
    print('모든 비교 연산은 True')
```

### 함수 테이블(딕셔너리)로 switch 문을 모방한다.
```python
menu_dict = {'load':load_fn, 'save':save_fn, 'exit':exit_fn, 'update':update_fn}
(menu_dict[selector])()  # 함수 호출
```

### is 연산자는 정확하게 사용한다.
```python
s1 = 'a b c d e f'
s2 = 'a b c' + ' d e f'
s1 == s2  # True
s1 is s2  # False
```

### 단일 행 for 루프를 사용한다.
```python
# for 변수 in 나열식_데이터: 블록문
for i in range(10): print(i, end=' ')
```

### 여러 문장을 하나의 행으로 줄인다.
```python
for i in range(5): n = i * 2; m = 5; print(n+m, end=' ')

a = 1; b = 2; c = a + b; print(c)

# 참_표현식 if 조건문 else 거짓_표현식
cell = 'X' if turn % 2 else '0'
```

### 큰 번호 안에 언더스코어(_)를 넣는다.
```python
# 안좋은 예시
CEO_salary = 1500000

# 좋은 예시
CEO_salary = 1_500_000
```

### doc string을 작성하고 사용한다.
```python
# doc string은 함수나 클래스 모두에서 등장할 수 있다.

def quad(a, b, c):
    '''Quadratic Formula function.

    This function applies the Quadratic Formula
    to determine the roots of x in a quadratic
    equation of the form ax^2 + bx + c = 0.
    '''
    determin = (b * b - 4 * a * c) ** .5
    x1 = (-b + determin) / (2 * a)
    x2 = (-b - determin) / (2 * a)
    return x1, x2

help(quad)

# 커멘트 라인에서 실행 (queens.py 모듈의 도움말 확인)
# python -m pydoc queens
```

### 제너레이터
```python
# 제너레이터 = 이터레이터를 만드는 가장 쉬운 방법
def make_evens_gen():
    for n in range(2, 11, 2):
        yield n

my_gen = make_evens_gen()
next(my_gen)  # 2
next(my_gen)  # 4
next(my_gen)  # 6

my_gen = make_evens_gen()
list(my_gen)  # [2, 4, 6, 8, 10]
```