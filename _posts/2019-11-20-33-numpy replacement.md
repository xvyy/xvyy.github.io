---
bg: photo033.jpg
layout: post
title: 替换NumPy数组中大于某个值的所有元素
crawlertitle: python numpy
summary: Python替换NumPy数组中大于某个值的所有元素
date: 2019-11-20 16:00:00 +0800
categories: technology
tags: python
author: vpromise
---

*问题:Python替换NumPy数组中大于某个值的所有元素，本文给出了几种思路*

---

- [问题:Python替换NumPy数组中大于某个值的所有元素](#问题python替换numpy数组中大于某个值的所有元素)
  - [最佳解决思路](#最佳解决思路)
  - [次佳解决思路](#次佳解决思路)
  - [第三种思路](#第三种思路)
  - [第四种思路](#第四种思路)

## 问题:Python替换NumPy数组中大于某个值的所有元素
我有一个2D(二维) NumPy数组，并希望用255.0替换大于或等于阈值T的所有值。据我所知，最基础的方法是：
```python
shape = arr.shape
result = np.zeros(shape)
for x in range(0, shape[0]):
    for y in range(0, shape[1]):
        if arr[x, y] >= T:
            result[x, y] = 255
```            
有更简洁和pythonic的方式来做到这一点吗？
有没有更快(可能不那么简洁和/或不那么pythonic)的方式来做到这一点？
### 最佳解决思路
我认为最快和最简洁的方法是使用Numpy的内置索引。如果您有名为arr的ndarray，则可以按如下所示将所有元素>255替换为值x：
```python
arr[arr > 255] = x
```
我用500 x 500的随机矩阵在我的机器上运行了这个函数，用5替换了所有> 0.5的值，平均耗时7.59ms。
```python
import numpy as np
A = np.random.rand(500, 500)
timeit A[A > 0.5] = 5

100 loops, best of 3: 7.59 ms per loop
```
### 次佳解决思路
因为实际上需要一个不同的数组，arr，其中arr < 255，可以简单地完成：
```python
result = np.minimum(arr, 255)
```
更一般地，对于下限和/或上限：
```python
result = np.clip(arr, 0, 255)
```
如果只是想访问超过255的值，np.clip和np.minimum(或者np.maximum)对你的情况更好更快。
```python
timeit np.minimum(a, 255)

100000 loops, best of 3: 19.6 µs per loop
```
```python
%%timeit
c = np.copy(a)
c[a>255] = 255

10000 loops, best of 3: 86.6 µs per loop
```
如果要执行in-place(即修改arr而不是创建result)，则可以使用np.minimum的out参数：
```python
np.minimum(arr, 255, out=arr)
```
或者
```python
np.clip(arr, 0, 255, arr)
```
(out=名称是可选的，因为参数的顺序与函数的定义相同。)

对于in-place修改，布尔索引加速了很多(不必分别修改和拷贝)，但仍然不如minimum：
```python
%%timeit
a = np.random.randint(0, 300, (100,100))
np.minimum(a, 255, a)

100000 loops, best of 3: 303 µs per loop
```
```python
%%timeit
a = np.random.randint(0, 300, (100,100))
a[a>255] = 255

100000 loops, best of 3: 356 µs per loop
```
比较来看，如果你想限制你的最大值和最小值，没有clip将不得不像下面这样做两次
```python
np.minimum(a, 255, a)
np.maximum(a, 0, a)
```
要么，
```python
a[a>255] = 255
a[a<0] = 0
```
### 第三种思路

可以通过使用where功能来达到最快的速度：

例如，在numpy数组中查找大于0.2的项目，并用0代替它们：
```python
import numpy as np

nums = np.random.rand(4,3)

print np.where(nums > 0.2, 0, nums)
```
### 第四种思路

可以考虑使用numpy.putmask：
```python
np.putmask(arr, arr>=T, 255.0)
```
下面是与Numpy内置索引的性能比较：
```python
import numpy as np
A = np.random.rand(500, 500)

timeit np.putmask(A, A>0.5, 5)
1000 loops, best of 3: 1.34 ms per loop

timeit A[A > 0.5] = 5

1000 loops, best of 3: 1.82 ms per loop
```