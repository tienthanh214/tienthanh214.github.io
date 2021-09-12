---
title: "Python trick Note"
excerpt: "Just note some python trick"
show_date: true
tags:
  - python
categories:
  - programming language
toc: true
---

Note một số trick python hay và ngắn

# Array

## Read array in one line
```py
a = list(map(int, input().split()))
```
## Print array split by space
```py
print(' '.join(map(str, a)))
```
## Reverse array
```py
a = a[::-1]
```
## Common value of two array
```py
set(a) & set(b)
```
## Array's histogram
```py
from collections import Counter
print(Counter(a))
```