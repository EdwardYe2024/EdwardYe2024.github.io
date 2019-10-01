---
layout:     post
title:      Introduction to Tensor Calculation
subtitle:   Introduction
date:       2019-05-12
author:     Feng Ye
header-img: img/post-bg-2015.jpg
catalog: true
tags:
    - Tensor
---
> “Yeah It's on. ”

# Introduction to Tensor Calculation #

In recent years, tensor decomposition has been well applied in the field of data mining, but some calculations on tensor are quite different from the linear algebra we are familiar with. At the same time, tensor calculation is  more abstract than linear algebra, which makes a lot of readers feel that the content of tensors is "difficult". 
Of course, in terms of linear algebra and multiple linear algebra, the mainstream view will refer to the content of tensor calculation as "multilinear algebra", and consider multiple linear algebra to actually It is an extension of linear algebra. 
In order to facilitate the understanding of tensor calculation, some mathematical foundations needed for tensor decomposition will be systematically introduced. This part mainly includes common Kronecker product, Khatri-Rao product, outer product of vector, inner product, F-norm, the rules of operation of modal products.
<br>
----------

## 1 . Kronecker product

Kronecker product is very common in tensor calculation. It is a bridge between joint matrix calculation and tensor calculation. In fact, the Kronecker product calculation rule is very simple. Given a matrix of size ![](https://www.zhihu.com/equation?tex=m_1%5Ctimes+m_2)and a matrix of size![](https://www.zhihu.com/equation?tex=n_1%5Ctimes+n_2), and the Kronecker product of the matrix A and matrix B is:

![](/img/in-post/Introduction.assets/equation-1569596579451.svg)

It is obvious that the size of the Kronecker product of the matrix A and matrix B is![](https://www.zhihu.com/equation?tex=%5Cleft%28+m_1n_1+%5Cright%29+%5Ctimes+%5Cleft%28+m_2n_2+%5Cright%29+)

for instance：
![](https://www.zhihu.com/equation?tex=A%3D%5Cleft%5B+%5Cbegin%7Barray%7D%7Bcc%7D+1+%26+2+%5C%5C+3+%26+4+%5C%5C+%5Cend%7Barray%7D+%5Cright%5D)![](https://www.zhihu.com/equation?tex=B%3D%5Cleft%5B+%5Cbegin%7Barray%7D%7Bccc%7D+5+%26+6+%26+7%5C%5C+8+%26+9+%26+10+%5C%5C+%5Cend%7Barray%7D+%5Cright%5D)

![](https://www.zhihu.com/equation?tex=A%5Cotimes+B%3D%5Cleft%5B+%5Cbegin%7Barray%7D%7Bcc%7D+1%5Ctimes+%5Cleft%5B+%5Cbegin%7Barray%7D%7Bccc%7D+5+%26+6+%26+7%5C%5C+8+%26+9+%26+10%5C%5C+%5Cend%7Barray%7D+%5Cright%5D+%26+2%5Ctimes+%5Cleft%5B+%5Cbegin%7Barray%7D%7Bccc%7D+5+%26+6+%26+7%5C%5C+8+%26+9+%26+10%5C%5C+%5Cend%7Barray%7D+%5Cright%5D+%5C%5C+3%5Ctimes+%5Cleft%5B+%5Cbegin%7Barray%7D%7Bccc%7D+5+%26+6+%26+7%5C%5C+8+%26+9+%26+10%5C%5C+%5Cend%7Barray%7D+%5Cright%5D+%26+4%5Ctimes+%5Cleft%5B+%5Cbegin%7Barray%7D%7Bccc%7D+5+%26+6+%26+7%5C%5C+8+%26+9+%26+10%5C%5C+%5Cend%7Barray%7D+%5Cright%5D+%5C%5C+%5Cend%7Barray%7D+%5Cright%5D)

so:

![](https://www.zhihu.com/equation?tex=A%5Cotimes+B%3D%5Cleft%5B+%5Cbegin%7Barray%7D%7Bcccccc%7D+5+%26+6+%26+7+%26+10+%26+12+%26+14+%5C%5C+8+%26+9+%26+10+%26+16+%26+18+%26+20+%5C%5C+15+%26+18+%26+21+%26+20+%26+24+%26+28+%5C%5C+24+%26+27+%26+30+%26+32+%26+36+%26+40+%5C%5C+%5Cend%7Barray%7D+%5Cright%5D)

However, $B\otimes A$

