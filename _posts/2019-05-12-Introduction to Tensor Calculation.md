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

# Introduction to Tensor Calculation #

In recent years, tensor decomposition has been well applied in the field of data mining, but some calculations on tensor are quite different from the linear algebra we are familiar with. At the same time, tensor calculation is  more abstract than linear algebra, which makes a lot of readers feel that the content of tensors is "difficult". 
Of course, in terms of linear algebra and multiple linear algebra, the mainstream view will refer to the content of tensor calculation as "multilinear algebra", and consider multiple linear algebra to actually It is an extension of linear algebra. 
In order to facilitate the understanding of tensor calculation, some mathematical foundations needed for tensor decomposition will be systematically introduced. This part mainly includes common Kronecker product, Khatri-Rao product, outer product of vector, inner product, F-norm, the rules of operation of modal products.
<br>


## 1 Kronecker Product

Kronecker product is very common in tensor calculation. It is a bridge between joint matrix calculation and tensor calculation. In fact, the Kronecker product calculation rule is very simple. Given a matrix of siz![](https://www.zhihu.com/equation?tex=m_1%5Ctimes+m_2)and a matrix of size![](https://www.zhihu.com/equation?tex=n_1%5Ctimes+n_2), and the Kronecker product of the matrix A and matrix B is:

![](/img/in-post/Introduction.assets/equation-1569596579451.svg)

It is obvious that the size of the Kronecker product of the matrix A and matrix B is![](https://www.zhihu.com/equation?tex=%5Cleft%28+m_1n_1+%5Cright%29+%5Ctimes+%5Cleft%28+m_2n_2+%5Cright%29+)

for instance：
![](https://www.zhihu.com/equation?tex=A%3D%5Cleft%5B+%5Cbegin%7Barray%7D%7Bcc%7D+1+%26+2+%5C%5C+3+%26+4+%5C%5C+%5Cend%7Barray%7D+%5Cright%5D)![](https://www.zhihu.com/equation?tex=B%3D%5Cleft%5B+%5Cbegin%7Barray%7D%7Bccc%7D+5+%26+6+%26+7%5C%5C+8+%26+9+%26+10+%5C%5C+%5Cend%7Barray%7D+%5Cright%5D)

![](https://www.zhihu.com/equation?tex=A%5Cotimes+B%3D%5Cleft%5B+%5Cbegin%7Barray%7D%7Bcc%7D+1%5Ctimes+%5Cleft%5B+%5Cbegin%7Barray%7D%7Bccc%7D+5+%26+6+%26+7%5C%5C+8+%26+9+%26+10%5C%5C+%5Cend%7Barray%7D+%5Cright%5D+%26+2%5Ctimes+%5Cleft%5B+%5Cbegin%7Barray%7D%7Bccc%7D+5+%26+6+%26+7%5C%5C+8+%26+9+%26+10%5C%5C+%5Cend%7Barray%7D+%5Cright%5D+%5C%5C+3%5Ctimes+%5Cleft%5B+%5Cbegin%7Barray%7D%7Bccc%7D+5+%26+6+%26+7%5C%5C+8+%26+9+%26+10%5C%5C+%5Cend%7Barray%7D+%5Cright%5D+%26+4%5Ctimes+%5Cleft%5B+%5Cbegin%7Barray%7D%7Bccc%7D+5+%26+6+%26+7%5C%5C+8+%26+9+%26+10%5C%5C+%5Cend%7Barray%7D+%5Cright%5D+%5C%5C+%5Cend%7Barray%7D+%5Cright%5D)

so:

![](https://www.zhihu.com/equation?tex=A%5Cotimes+B%3D%5Cleft%5B+%5Cbegin%7Barray%7D%7Bcccccc%7D+5+%26+6+%26+7+%26+10+%26+12+%26+14+%5C%5C+8+%26+9+%26+10+%26+16+%26+18+%26+20+%5C%5C+15+%26+18+%26+21+%26+20+%26+24+%26+28+%5C%5C+24+%26+27+%26+30+%26+32+%26+36+%26+40+%5C%5C+%5Cend%7Barray%7D+%5Cright%5D)

However, because![](https://www.zhihu.com/equation?tex=B%5Cotimes+A%3D%5Cleft%5B+%5Cbegin%7Barray%7D%7Bccc%7D+5%5Ctimes+%5Cleft%5B+%5Cbegin%7Barray%7D%7Bcc%7D+1+%26+2+%5C%5C+3+%26+4+%5C%5C+%5Cend%7Barray%7D+%5Cright%5D+%26+6%5Ctimes+%5Cleft%5B+%5Cbegin%7Barray%7D%7Bcc%7D+1+%26+2%5C%5C+3+%26+4%5C%5C+%5Cend%7Barray%7D+%5Cright%5D+%26+7%5Ctimes+%5Cleft%5B+%5Cbegin%7Barray%7D%7Bcc%7D+1+%26+2%5C%5C+3+%26+4%5C%5C+%5Cend%7Barray%7D+%5Cright%5D+%5C%5C+8%5Ctimes+%5Cleft%5B+%5Cbegin%7Barray%7D%7Bcc%7D+1+%26+2+%5C%5C+3+%26+4+%5C%5C+%5Cend%7Barray%7D+%5Cright%5D+%26+9%5Ctimes+%5Cleft%5B+%5Cbegin%7Barray%7D%7Bcc%7D+1+%26+2+%5C%5C+3+%26+4+%5C%5C+%5Cend%7Barray%7D+%5Cright%5D+%26+10%5Ctimes+%5Cleft%5B+%5Cbegin%7Barray%7D%7Bcc%7D+1+%26+2%5C%5C+3+%26+4%5C%5C+%5Cend%7Barray%7D+%5Cright%5D+%5C%5C+%5Cend%7Barray%7D+%5Cright%5D)

that is ![](https://www.zhihu.com/equation?tex=B%5Cotimes+A%3D%5Cleft%5B+%5Cbegin%7Barray%7D%7Bcccccc%7D+5+%26+10+%26+6+%26+12+%26+7+%26+14+%5C%5C+15+%26+20+%26+18+%26+24+%26+21+%26+28+%5C%5C+8+%26+16+%26+9+%26+18+%26+10+%26+20+%5C%5C+24+%26+32+%26+27+%26+36+%26+30+%26+40+%5C%5C+%5Cend%7Barray%7D+%5Cright%5D)

so, it is obvious that ![](https://www.zhihu.com/equation?tex=B%5Cotimes+A%5Cne+A%5Cotimes+B)
In addition, 
![](https://www.zhihu.com/equation?tex=A%5ET%5Cotimes+B%5ET%3D%5Cleft%5B+%5Cbegin%7Barray%7D%7Bcc%7D+1%5Ctimes+%5Cleft%5B+%5Cbegin%7Barray%7D%7Bcc%7D+5+%26+8%5C%5C+6+%26+9%5C%5C+7+%26+10%5C%5C+%5Cend%7Barray%7D+%5Cright%5D+%26+3%5Ctimes+%5Cleft%5B+%5Cbegin%7Barray%7D%7Bcc%7D+5+%26+8%5C%5C+6+%26+9%5C%5C+7+%26+10%5C%5C+%5Cend%7Barray%7D+%5Cright%5D+%5C%5C+2%5Ctimes+%5Cleft%5B+%5Cbegin%7Barray%7D%7Bcc%7D+5+%26+8%5C%5C+6+%26+9%5C%5C+7+%26+10%5C%5C+%5Cend%7Barray%7D+%5Cright%5D+%26+4%5Ctimes+%5Cleft%5B+%5Cbegin%7Barray%7D%7Bcc%7D+5+%26+8%5C%5C+6+%26+9%5C%5C+7+%26+10%5C%5C+%5Cend%7Barray%7D+%5Cright%5D+%5C%5C+%5Cend%7Barray%7D+%5Cright%5D)
As a result,
![](https://www.zhihu.com/equation?tex=A%5ET%5Cotimes+B%5ET%3D%5Cleft%5B+%5Cbegin%7Barray%7D%7Bcccc%7D+5+%26+8+%26+15+%26+24%5C%5C+6+%26+9+%26+18+%26+27%5C%5C+7+%26+10+%26+21+%26+30%5C%5C+10+%26+16+%26+20+%26+32%5C%5C+12+%26+18+%26+24+%26+36%5C%5C+14+%26+20+%26+28+%26+40%5C%5C+%5Cend%7Barray%7D+%5Cright%5D)
so,![](https://www.zhihu.com/equation?tex=A%5ET%5Cotimes+B%5ET%3D%5Cleft%28+A%5Cotimes+B+%5Cright%29+%5ET)


## 2 Vector Outer Product

Given **a**=(1,2)^T, **b**=(3,4)^T, **c**=(5,6,7)^T. The outer product of **a,b,c** can be denoted as ![](https://www.zhihu.com/equation?tex=%7B%5Cmathcal%7BX%7D%7D%3D%5Cvec+a%5Ccirc+%5Cvec+b%5Ccirc+%5Cvec+c)
That is:
![](https://www.zhihu.com/equation?tex=%7B%5Cmathcal%7BX%7D%7D%5Cleft%28+%3A%2C%3A%2C1%5Cright%29+%3D%5Cleft%5B+%5Cbegin%7Barray%7D%7Bcc%7D+1%5Ctimes+3%5Ctimes+5+%26+1%5Ctimes+4%5Ctimes+5+%5C%5C+2%5Ctimes+3%5Ctimes+5+%26+2%5Ctimes+4%5Ctimes+5+%5C%5C+%5Cend%7Barray%7D+%5Cright%5D%3D%5Cleft%5B+%5Cbegin%7Barray%7D%7Bcc%7D+15+%26+20+%5C%5C+30+%26+40+%5C%5C+%5Cend%7Barray%7D+%5Cright%5D)![](https://www.zhihu.com/equation?tex=%7B%5Cmathcal%7BX%7D%7D%5Cleft%28+%3A%2C%3A%2C2%5Cright%29+%3D%5Cleft%5B+%5Cbegin%7Barray%7D%7Bcc%7D+1%5Ctimes+3%5Ctimes+6+%26+1%5Ctimes+4%5Ctimes+6+%5C%5C+2%5Ctimes+3%5Ctimes+6+%26+2%5Ctimes+4%5Ctimes+6+%5C%5C+%5Cend%7Barray%7D+%5Cright%5D%3D%5Cleft%5B+%5Cbegin%7Barray%7D%7Bcc%7D+18+%26+24+%5C%5C+36+%26+48+%5C%5C+%5Cend%7Barray%7D+%5Cright%5D)![](https://www.zhihu.com/equation?tex=%7B%5Cmathcal%7BX%7D%7D%5Cleft%28+%3A%2C%3A%2C3%5Cright%29+%3D%5Cleft%5B+%5Cbegin%7Barray%7D%7Bcc%7D+1%5Ctimes+3%5Ctimes+7+%26+1%5Ctimes+4%5Ctimes+7+%5C%5C+2%5Ctimes+3%5Ctimes+7+%26+2%5Ctimes+4%5Ctimes+7+%5C%5C+%5Cend%7Barray%7D+%5Cright%5D%3D%5Cleft%5B+%5Cbegin%7Barray%7D%7Bcc%7D+21+%26+28+%5C%5C+42+%26+56+%5C%5C+%5Cend%7Barray%7D+%5Cright%5D)
The value of index(j,j,k) is ![](https://www.zhihu.com/equation?tex=x_%7Bijk%7D%3Da_i%5Ccdot+b_j%5Ccdot+c_k%2Ci%3D1%2C2%2Cj%3D1%2C2%2Ck%3D1%2C2%2C3) and in this case, we can obtain the three-order tensor:![](https://pic1.zhimg.com/80/v2-3847e5e46bc6938dc1c1f08fa1b1bd6c_hd.png)

## 3 Frobenius Norm

Given a tensor ![](https://www.zhihu.com/equation?tex=%7B%5Cmathcal%7B+X%7D%7D%5Cleft%28+%3A%2C%3A%2C1+%5Cright%29+%3D%5Cleft%5B+%5Cbegin%7Barray%7D%7Bcc%7D+1+%26+2+%5C%5C+3+%26+4+%5C%5C+%5Cend%7Barray%7D+%5Cright%5D)![](https://www.zhihu.com/equation?tex=%7B%5Cmathcal%7B+X%7D%7D%5Cleft%28+%3A%2C%3A%2C2+%5Cright%29+%3D%5Cleft%5B+%5Cbegin%7Barray%7D%7Bcc%7D+5+%26+6+%5C%5C+7+%26+8+%5C%5C+%5Cend%7Barray%7D+%5Cright%5D) the frobenius norm is ![](https://www.zhihu.com/equation?tex=%7C%7C%7B%5Cmathcal%7B+X%7D%7D%7C%7C_F%3D%5Csqrt%7B%5Cleft%3C%7B%5Cmathcal%7B+X%7D%7D%2C%7B%5Cmathcal%7B+X%7D%7D%5Cright%3E%7D+)![](https://www.zhihu.com/equation?tex=%3D%5Csqrt%7B1%5E2%2B2%5E2%2B3%5E2%2B4%5E2%2B5%5E2%2B6%5E2%2B7%5E2%2B8%5E2%7D+%3D%5Csqrt%7B204%7D+)

That is, the square of the tensor F-norm is equal to the sum of the squares of all the elements. In this case, many optimization problems involving matrix decomposition or tensor decomposition often lead to the minimization of sum of the squares of the residual matrix or the residuals, and the objective function is also written in the square of the F-norm of the corresponding residual matrix or residual tensor.

- to be continued

