---
layout:     post
title:      How to explain Principal Component Analysis in an easy-to-understand way?
subtitle:   
date:       2019-09-15
author:     Feng Ye
header-img: img/post-bg-2015.jpg
catalog: true
tags:
    - Matrix
---
## Introduction
PCA (Principal Component Analysis) is a commonly used method for data analysis. 
PCA transforms the original data into a set of linearly independent features through linear transformation, which can be used to extract the main feature components of the data, which is often used for dimensionality reduction of high-dimensional data. 
There are many articles about PCA, but most of them only describe the analysis process of PCA, but not the principle. 
The purpose of this blog is to introduce the basic mathematical principles of PCA and to help readers better understand what the working mechanism of PCA is. 
I don't intend to write this bolg as a purely mathematical article, but I want to describe the mathematical principles of PCA in an intuitive and understandable way. 
I hope that readers can better understand how PCA works after reading this blog. 

## Vector representation of data and dimensionality reduction

In general, in data mining and machine learning, data is represented as vectors. 
For example, the transactions of an Amazon online store in 2019 can be regarded as a collection of records. The data of each day is a record, and the format is as follows:

(date, pageviews, number of visitors, number of orders, number of transactions, transaction amount)
Where "date" is a record flag rather than a metric, and data mining is mostly concerned with metrics, so if we ignore the date, we get a set of records, each record can be represented as a five-dimensional vector. 
One of them looks like this:![](https://www.zhihu.com/equation?tex=%28500%2C240%2C25%2C13%2C2312.15%29%5E%5Cmathsf%7BT%7D)
Note that I used transpose here because it is customary to use a column vector to represent a record (you will see the reason later), which will be followed later in this article. 
However, for convenience I sometimes omit the transpose symbol, but we say that the vector defaults to the column vector.

We can of course analyze and mine this set of five-dimensional vectors, but we know that the complexity of many machine learning algorithms is closely related to the dimensionality of the data, and even exponentially related to the dimension. 
Of course, the five-dimensional data here may not matter, but it is not uncommon to deal with thousands or even hundreds of thousands of dimensions in actual machine learning. In this case, the resource consumption of machine learning is unacceptable. 
Therefore, we must reduce the dimensionality of the data. 

Dimensionality reduction of course means the loss of information, but given the relevance of the actual data itself, we can find ways to reduce the loss of information while reducing the dimension.

For example, if a student's data has two columns, M and F, The value of column M is that the student takes a value of 1 for a male and 0 for a female; and the F column is a value of 1 for a female, the male takes a value of 0.

At this time, if we count all the student's data, we will find that for any record, F must be 0 when M is 1, and F must be 1 when M is 0. 
In this case, we remove the loss of M or F without any information, because as long as one column is retained, the other column can be completely restored. 
Of course, the above is an extreme situation, and may not appear in reality, but similar situations are still very common. 
For example, the data of the above Amazon shop, from the experience we can know, "views" and "visitors" often have a strong correlation, and "order number" and "number of transactions" also have a strong correlation. 
Here we use the word "correlation", which can be intuitively understood as "When a store has a high (or lower) pageview on a certain day, we should largely think that the number of visitors on this day is also high(or lower)". 
We will give a strict mathematical definition of the correlation in later chapters. 
This situation suggests that if we remove one of the metrics for pageviews or visitors, we should expect not to lose too much information. 
So we can remove one to reduce the complexity of the machine learning algorithm. 
The above is a description of the simple thinking of dimensionality reduction, which can help to understand the motivation and feasibility of dimensionality reduction, but it does not have operational guiding significance. 
For example, what kind of loss information do we delete in the end? 
Or is it simply not to delete a few columns at all, but to transform the raw data into fewer columns with some transformations while minimizing the missing information? 
How do you measure the amount of lost information? 
How to determine the specific dimension reduction steps based on the original data? 
To answer the above questions, we must mathematically and formally discuss the dimension reduction problem. 
PCA is a dimensionality reduction method that has a strict mathematical foundation and has been widely adopted. 
Below I will not directly describe the PCA, but by gradually analyzing the problem, let us re-invent the PCA together.

## Vector representation and base transformation

Since the data we are facing is abstracted into a set of vectors, it is necessary to study the mathematical properties of some vectors. 
These mathematical properties will be the theoretical basis for the subsequent export of PCA.

### Inner product and projection

Let's first look at a vector operation learned in high school: inner product. 
The inner product of two vectors of the same dimension is defined as:![](https://www.zhihu.com/equation?tex=%28a_1%2Ca_2%2C%5Ccdots%2Ca_n%29%5E%5Cmathsf%7BT%7D%5Ccdot+%28b_1%2Cb_2%2C%5Ccdots%2Cb_n%29%5E%5Cmathsf%7BT%7D%3Da_1b_1%2Ba_2b_2%2B%5Ccdots%2Ba_nb_n)

The inner product maps two vectors to a real number. 
The calculation is very easy to understand, but its significance is not obvious. 
Below we analyze the geometric meaning of the inner product. 
For the sake of simplicity, we assume that **A** and **B** both are two-dimensional vectors. Then on a two-dimensional plane **A** and **B** can be represented by two directed segments from the origin, see the following figure:![](https://pic1.zhimg.com/8d64151ceed0eed4d4708d8d9e6374dc_b.png)

Now we draw a vertical line from the point **A** to the line **B**. 
We know that the intersection of the perpendicular line is called the projection, then the length of the vector of the projection is:
![](https://www.zhihu.com/equation?tex=%7CA%7Ccos%28%5Calpha+%29)![](https://www.zhihu.com/equation?tex=%7CA%7C%3D%5Csqrt%7Bx_1%5E2%2By_1%5E2%7D)
We express the inner product as another form we are familiar with:
![](https://www.zhihu.com/equation?tex=A%5Ccdot+B%3D%7CA%7C%7CB%7Ccos%28%5Calpha+%29)

Further, if we assume that:![](https://www.zhihu.com/equation?tex=%7CB%7C%3D1)
then it becomes:![](https://www.zhihu.com/equation?tex=A%5Ccdot+B%3D%7CA%7Ccos%28%5Calpha+%29)

Then the inner product of **A** and **B** is equal to the vector length  of **A** projected to the line **B**! 
This is a geometric interpretation of the inner product and the first important conclusion we have. 
In the following derivation, this conclusion will be used repeatedly.

### Basis
We continue to discuss vectors in a two-dimensional space. 
As mentioned above, a two-dimensional vector can correspond to a directed line segment starting from the origin in a two-dimensional Cartesian coordinate system. 
For example, the following vector:![](https://pic1.zhimg.com/df6a713c1b97cc55bd20afce46ace718_b.png)

In terms of algebraic representation, we often use the point coordinates of the end point of the line to represent the vector. For example, the above vector can be expressed as **(3,2)**, this is a vector representation that we are familiar with.

However, we often ignore that only **(3,2)** is not able to accurately represent a vector. 
Let's take a closer look. The actual representation here is that the projection value of the vector on the x-axis is 3 and the projection value on the y-axis is 2. 
In other words, we implicitly introduce a definition: a vector with a length of 1 in the positive direction on the x and y axes.
Then a vector actually means that the projection on the x-axis is 3 and the projection on the y-axis is 2. 
Note that the projection is a vector, so it can be negative. 

More formally, the vector (x, y) actually represents a linear combination:
![](https://www.zhihu.com/equation?tex=x%281%2C0%29%5E%5Cmathsf%7BT%7D%2By%280%2C1%29%5E%5Cmathsf%7BT%7D)

It is not difficult to prove that all two-dimensional vectors can be represented as such linear combinations. 
Here **(1,0)** and **(0,1)** are called basis in a two-dimensional space.
![](https://pic1.zhimg.com/4533331b5b4b5ea98c90f2abed81d470_b.png)

Therefore, to accurately describe the vector, you first need to determine a set of bases, and then give the projection values ​​on the respective lines where the base is located. 
However, we often omit the first step, and the default is based on **(1,0)** and **(0,1)**.

The reason why we choose **(1,0)** and **(0,1)** as basis by default is that they are the unit vectors in the positive direction of the x and y axes respectively, Thus, the point coordinates and the vector on the two-dimensional plane are one-to-one, which is very convenient. 
But in fact any two linearly independent two-dimensional vectors can be a set of bases. The so-called linear independence can be visually recognized as two vectors that are not in a straight line in a two-dimensional plane. 

For example, **(1,1)** and **(-1,1)** can also be a set of bases. 
In general, we want the module of the basis to be 1, because we can see from the meaning of the inner product that if the module of the basis is 1, then it is convenient to multiply the basis with the vector point and directly obtain the coordinates on the new basis! 
In fact, for any vector, we can always find a vector whose module is 1 in the same direction, as long as the two components are divided by the module. 

Now, we want to obtain the coordinates of **(3, 2)** on the new basis, that is, the projection vector values ​​in the two directions, then according to the geometric meaning of the inner product, we only need to calculate inner product of **(3, 2)** and two bases separately. 
It is not difficult to get new coordinates:![](https://www.zhihu.com/equation?tex=%28%5Cfrac%7B5%7D%7B%5Csqrt%7B2%7D%7D%2C-%5Cfrac%7B1%7D%7B%5Csqrt%7B2%7D%7D%29)
 
The figure below shows the new base and the **(3, 2)** diagram of the coordinates on the new base.
![](https://pic2.zhimg.com/ff47d66fa67d12918e4e83678fa6b78d_b.png)

In addition, it should be noted here that the examples in our example are orthogonal (that is, the inner product is 0, or intuitively perpendicular to each other), but the only requirement that can be a set of bases is linearly independent. 
However, because orthogonal groups have better properties, the bases generally used are orthogonal.

### Matrix representation of base transformation

We find an easy way to represent the base transform.
Or take the above example, think about it, convert **(3, 2)** to the coordinates on the new basis, use **(3, 2)** and the first base to do the inner product operation as the first new coordinate component, and then use **(3, 2)** and the second base to do the inner product operation as the component of the second new coordinate.
In fact, we can use matrix multiplication in the form of compact representation of this transformation:
![](https://www.zhihu.com/equation?tex=%5Cbegin%7Bpmatrix%7D+1%2F%5Csqrt%7B2%7D+%26+1%2F%5Csqrt%7B2%7D+%5C%5C+-1%2F%5Csqrt%7B2%7D+%26+1%2F%5Csqrt%7B2%7D+%5Cend%7Bpmatrix%7D+%5Cbegin%7Bpmatrix%7D+3+%5C%5C+2+%5Cend%7Bpmatrix%7D+%3D+%5Cbegin%7Bpmatrix%7D+5%2F%5Csqrt%7B2%7D+%5C%5C+-1%2F%5Csqrt%7B2%7D+%5Cend%7Bpmatrix%7D)

**beautiful!** 
The two rows of the matrix are respectively two bases, multiplied by the original vector, and the result is just the coordinates of the new base. 
It can be slightly promoted. If we have m two-dimensional vectors, we can get the values ​​of all these vectors under the new base by arranging the two-dimensional vectors into a two-row and m-column matrix by column and then multiplying the matrix. For example, **(1,1)**, **(2,2)**, **(3,3)**:
![](https://www.zhihu.com/equation?tex=%5Cbegin%7Bpmatrix%7D+1%2F%5Csqrt%7B2%7D+%26+1%2F%5Csqrt%7B2%7D+%5C%5C+-1%2F%5Csqrt%7B2%7D+%26+1%2F%5Csqrt%7B2%7D+%5Cend%7Bpmatrix%7D+%5Cbegin%7Bpmatrix%7D+1+%26+2+%26+3+%5C%5C+1+%26+2+%26+3+%5Cend%7Bpmatrix%7D+%3D+%5Cbegin%7Bpmatrix%7D+2%2F%5Csqrt%7B2%7D+%26+4%2F%5Csqrt%7B2%7D+%26+6%2F%5Csqrt%7B2%7D+%5C%5C+0+%26+0+%26+0+%5Cend%7Bpmatrix%7D)

Then the basis transform of a set of vectors is clearly represented as the multiplication of the matrix.

In general, if we have M N-dimensional vectors and want to transform them into new spaces represented by M R-dimensional vectors:

![](https://www.zhihu.com/equation?tex=%5Cbegin%7Bpmatrix%7D+p_1+%5C%5C+p_2+%5C%5C+%5Cvdots+%5C%5C+p_R+%5Cend%7Bpmatrix%7D+%5Cbegin%7Bpmatrix%7D+a_1+%26+a_2+%26+%5Ccdots+%26+a_M+%5Cend%7Bpmatrix%7D+%3D+%5Cbegin%7Bpmatrix%7D+p_1a_1+%26+p_1a_2+%26+%5Ccdots+%26+p_1a_M+%5C%5C+p_2a_1+%26+p_2a_2+%26+%5Ccdots+%26+p_2a_M+%5C%5C+%5Cvdots+%26+%5Cvdots+%26+%5Cddots+%26+%5Cvdots+%5C%5C+p_Ra_1+%26+p_Ra_2+%26+%5Ccdots+%26+p_Ra_M+%5Cend%7Bpmatrix%7D)

where p is row vectors which represent basis and a is a column vector which represents the data record.

It is important to note that R can be less than N, and R determines the dimension of the transformed data. 
That is, we can transform an N-dimensional data into a lower-dimensional space, and the transformed dimension depends on the number of bases. 
Therefore, the representation of such matrix multiplication can also represent the dimensionality reduction transformation.

Finally, the above analysis also finds a physical explanation for matrix multiplication: the meaning of multiplication of two matrices is to transform each column of the vector in the right matrix into the space represented by each row vector in the left matrix. More abstractly, a matrix can represent a linear transformation. 


