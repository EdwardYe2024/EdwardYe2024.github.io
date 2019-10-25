---
layout:     post
title:      What is the nature of matrix multiplication?
subtitle:   
date:       2019-04-12
author:     Feng Ye
header-img: img/post-bg-2015.jpg
catalog: true
tags:
    - Statistic
---

In machine learning algorithms, matrix multiplication is very common. Analysis of the underlying operations of matrix multiplication can sometimes help us better understand the algorithm. How should we understand the nature of matrix multiplication?

For ![](https://www.zhihu.com/equation?tex=%5Cbm%7BA%7D_%7Bm%5Ctimes+n%7D%5Cbm%7BB%7D_%7Bn%5Ctimes+p%7D%3D%5Cbm%7BC%7D_%7Bm%5Ctimes+p%7D), I can explain it in two ways:

1. The matrix to the left of the multiplication is used as a set of m n-dimensional row vectors, and the matrix on the right is treated as a set of p n-dimensional column vectors. The matrix multiplication is to make the dot product of the left row vector and the right column vector one by one (inner product). The final result is stored in a new matrix of m*p corresponding to the location.
2. Multiplication is a collection of column vectors. 
The matrix on the right is still a set of p n-dimensional column vectors, and the matrix on the left is the base vector of the m-dimensional coordinate system. This operation is to "give a set of bases to the matrix on the right", or the absolute coordinates of the n-dimensional space points in the space represented by a set of m-dimensional basis. The is similar with ![](https://www.zhihu.com/equation?tex=%5Cbm%7Bp%7D%3Dx%5Cbm%7Bi%7D%2By%5Cbm%7Bj%7D%2Bz%5Cbm%7Bk%7D).

But these two explanations are not intuitive. Now I am going to explain more specifically.

Firstly, we need to know:
1. A space must first have an absolute coordinate system, and then a new set of base vectors representing the absolute coordinate system. The set of base vectors form a coordinate system, and represent the coordinates of a point or vector in the coordinate system. For instance, basis of the absolute coordinate system can be [1 0 0]^T, [0 1 0]^T and [0 0 1]^T.
2. A matrix can be regarded as a set of data points, or as a coordinate system (a set of bases), or as a transformation.
3. Whether the data is represented as a row vector or a column vector is up to you, and directly affects whether the data is placed on the left or right in the operation.
4. Data is best understood as the coefficients of the basis, which are actually ![](https://www.zhihu.com/equation?tex=%5Cbm%7Bp%7D%3Dx%5Cbm%7Bi%7D%2By%5Cbm%7Bj%7D%2Bz%5Cbm%7Bk%7D) Usually, they are represented by default on [1 0 0]^T, [0 1 0]^T and [0 0 1]^T. So by default, the absolute position of the data vector is itself. 
But if the coordinate system you take is not a unit matrix, you need to understand which basis the data is represented on.

Specifically speaking, firstly we assume that the space is a 3-dimensional one, and the data is represented as a column vector, that set of data is a 3 * p matrix![](https://www.zhihu.com/equation?tex=%5Cbm%7BP%7D+%3D+%5Cbegin%7Bbmatrix%7D+b_%7B11%7D%26+b_%7B12%7D%26b_%7B13%7D%26...%26+b_%7B1p%7D%5C%5C+b_%7B21%7D%26+b_%7B22%7D%26b_%7B23%7D%26...%26+b_%7B2p%7D%5C%5C+b_%7B31%7D%26+b_%7B32%7D%26b_%7B33%7D%26...%26+b_%7B3p%7D+%5Cend%7Bbmatrix%7D_%7B3%5Ctimes+p%7D)
The "transformation" of the data is a 3-dimensional row vector set, i.e. m*3 matrix:![](https://www.zhihu.com/equation?tex=%5Cbm%7BT%7D%3D%5Cbegin%7Bbmatrix%7D+a_%7B11%7D%26+a_%7B12%7D%26a_%7B13%7D%5C%5C+a_%7B21%7D%26+a_%7B22%7D%26a_%7B23%7D%5C%5C+a_%7B31%7D%26+a_%7B32%7D%26a_%7B33%7D%5C%5C+...%26...%26...%26%5C%5C+%5Cend%7Bbmatrix%7D_%7Bm%5Ctimes+3%7D)
In this way, in this actual model, the matrix multiplication is generally on the right and the transformation is on the left.

The magical difference of matrix multiplication is that it has many kinds of interpretations. For different appearances of ![](https://www.zhihu.com/equation?tex=%5Cbm%7BA%7D%5Cbm%7BB%7D%3D%5Cbm%7BC%7D), there are many kinds of interpretations (for the sake of intuition, set the dimension n=3):

For ![](https://www.zhihu.com/equation?tex=%5Cbm%7BT%7D_%7B3%5Ctimes+3%7D%5Cbm%7BP%7D_%7B3%5Ctimes+p%7D)

This is the direct operation of the data in 3-dimensional space, and the result is still the 3*P data set. According to the different understanding of *T*, it can be interpreted in three ways:

1. T, as a transformation matrix (as a set of row vectors): The space can be represented by three mutually perpendicular unit basis vectors, the coordinate system is unchanged. All points in the space is being "linearly" rotated, translated, and stretched with the three base vectors. 
2. T, as the basis of the coordinate system (as a set of column vectors), this is to find the absolute coordinates of the data set (absolute coordinates based on the unit basis),  like doing the opeartion of ![](https://www.zhihu.com/equation?tex=%5Cbm%7Bp%7D%3Dx%5Cbm%7Bi%7D%2By%5Cbm%7Bj%7D%2Bz%5Cbm%7Bk%7D) 
