# Introduction to Tensor Calculation

In recent years, tensor decomposition has been well applied in the field of data mining, but some calculations on tensor are quite different from the linear algebra we are familiar with. At the same time, tensor calculation is  more abstract than linear algebra, which makes a lot of readers feel that the content of tensors is "difficult". 
Of course, in terms of linear algebra and multiple linear algebra, the mainstream view will refer to the content of tensor calculation as "multilinear algebra", and consider multiple linear algebra to actually It is an extension of linear algebra. 
In order to facilitate the understanding of tensor calculation, some mathematical foundations needed for tensor decomposition will be systematically introduced. This part mainly includes common Kronecker product, Khatri-Rao product, outer product of vector, inner product, F-norm, the rules of operation of modal products.

## 1 Kronecker product
Kronecker product is very common in tensor calculation. It is a bridge between joint matrix calculation and tensor calculation. In fact, the Kronecker product calculation rule is very simple. Given a matrix of size ![](2019-05-12-Introduction to Tensor Calculation.assets/equation.svg) and a matrix of size ![](2019-05-12-Introduction to Tensor Calculation.assets/equation-1569595360662.svg), the matrix 
And the Kronecker product of the matrix A and matrix B is:
![](2019-05-12-Introduction to Tensor Calculation.assets/equation-1569596579451.svg)

$$
A\otimes B = \left[ \begin{array}{cccc} a_{11}B & a_{12}B & \cdots & a_{1m_2}B \\ a_{21}B & a_{22}B & \cdots & a_{2m_2}B \\ \vdots & \vdots & \ddots & \vdots \\ a_{m_11}B & a_{m_12}B & \cdots & a_{m_1m_2}B \\ \end{array} \right]
$$

$$
A\otimes B=\left[ \begin{array}{cc} 1\times \left[ \begin{array}{ccc} 5 & 6 & 7\\ 8 & 9 & 10\\ \end{array} \right] & 2\times \left[ \begin{array}{ccc} 5 & 6 & 7\\ 8 & 9 & 10\\ \end{array} \right] \\ 3\times \left[ \begin{array}{ccc} 5 & 6 & 7\\ 8 & 9 & 10\\ \end{array} \right] & 4\times \left[ \begin{array}{ccc} 5 & 6 & 7\\ 8 & 9 & 10\\ \end{array} \right] \\ \end{array} \right]
$$


