---
layout:     post
title:      How to explain Principal Component Analysis in an easy-to-understand way?
subtitle:   
date:       2019-09-15
author:     Feng Ye
header-img: img/post-bg-os-metro.jpg
catalog: true
tags:
    - Matrix
---
## 1. Introduction
PCA (Principal Component Analysis) is a commonly used method for data analysis. 
PCA transforms the original data into a set of linearly independent features through linear transformation, which can be used to extract the main feature components of the data, which is often used for dimensionality reduction of high-dimensional data. 
There are many articles about PCA, but most of them only describe the analysis process of PCA, but not the principle. 
The purpose of this blog is to introduce the basic mathematical principles of PCA and to help readers better understand what the working mechanism of PCA is. 
I don't intend to write this bolg as a purely mathematical article, but I want to describe the mathematical principles of PCA in an intuitive and understandable way. 
I hope that readers can better understand how PCA works after reading this blog. 

## 2. Vector representation of data and dimensionality reduction

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

## 3. Vector representation and basis transformation

Since the data we are facing is abstracted into a set of vectors, it is necessary to study the mathematical properties of some vectors. 
These mathematical properties will be the theoretical basis for the subsequent export of PCA.

### 3.1 Inner product and projection

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

### 3.2 Basis
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

## 4. Matrix representation of basis transformation

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

## 5. Covariance matrix
We discussed above that choosing different bases can give different representations to the same set of data, and if the number of bases is less than the dimension of the vector itself, the dimensionality reduction effect can be achieved. 
But we haven't answered one of the most critical questions: how to choose the basis that can be the best. 
Or, if we have a set of N-dimensional vectors, and now we want to reduce them to K-dimensional (K is less than N), then how should we choose K bases to retain the original information to the greatest extent? 

In order to avoid too abstract discussions, we still use a concrete example. 
Suppose our data consists of five records, which are represented as a matrix
![](https://www.zhihu.com/equation?tex=%5Cbegin%7Bpmatrix%7D+1+%26+1+%26+2+%26+4+%26+2+%5C%5C+1+%26+3+%26+3+%26+4+%264+%5Cend%7Bpmatrix%7D)

Each of these columns is a data record and each row is each dimension of  records. 
For the convenience of subsequent processing, we first subtract all the values ​​in each row from the row mean, and the result is to change each row to a mean of 0 (the reason and benefits will be seen later)

Let's look at the above data, the first row has a mean of 2, and the second row has a mean of 3, so after the transformation:![](https://www.zhihu.com/equation?tex=%5Cbegin%7Bpmatrix%7D+-1+%26+-1+%26+0+%26+2+%26+0+%5C%5C+-2+%26+0+%26+0+%26+1+%26+1+%5Cend%7Bpmatrix%7D)
We can see how the five pieces of data locate in the plane Cartesian coordinate system:
![](https://pic3.zhimg.com/e01296f282109b59e18086843866f81a_b.png)

Now the question is: If we have to use one dimension to represent this data, and we want to keep the original information as much as possible, how do you choose?

Through the discussion of the base transform in the previous section, we know that this problem is actually to select a direction in the 2D plane, project all the data onto the line in this direction, and use the projection value to represent the original record. 
So how do you choose this direction (or basis) to retain as much of the original information as possible? 
An intuitive view is that you want the projected values ​​after projection to be as scattered as possible.
As shown in the above figure, it can be seen that if you project to the x-axis, the two leftmost points will overlap, and the two middle points will overlap, so there are only two different values ​​left, which is a serious loss of information. Similarly, if the top two points and the two points distributed on the x-axis projected onto the y-axis, they all overlap. So it seems that the x and y axes are not the best projection choices. 
We intuitively visually observe that five points can be distinguished after projection if they are projected obliquely through the first and third quadrants.

We use mathematical methods to express this problem.

### 5.1 Variance
We want the projection values ​​to be as scattered as possible, and the degree of dispersion can be expressed in terms of mathematical variance:
![](https://www.zhihu.com/equation?tex=Var%28a%29%3D%5Cfrac%7B1%7D%7Bm%7D%5Csum_%7Bi%3D1%7D%5Em%7B%28a_i-%5Cmu%29%5E2%7D)
Since we have averaged the mean of each dimension to 0 above, the variance can be directly divided by the sum of the squares of each element by the number of elements:![](https://www.zhihu.com/equation?tex=Var%28a%29%3D%5Cfrac%7B1%7D%7Bm%7D%5Csum_%7Bi%3D1%7D%5Em%7Ba_i%5E2%7D)
So the above problem is formalized as: looking for a basis, so that all data is transformed into the coordinate representation on this basis, the variance value is the largest.

### 5.2 Covariance
For the problem of reducing the 2-dimensional to 1-dimensional above, find the direction that makes the variance the largest. 
However, for higher dimensions, there is still a problem to be solved. Consider the problem of reducing 3-dimensional to 2-dimensional. 
As before, first we want to find a direction so that the projection difference is the largest, thus completing the first direction selection, and then we choose the second projection direction.

If we still only choose the direction with the largest variance, it is obvious that this direction and the first direction should be "almost coincident". Obviously such a dimension is useless, so there should be other constraints. Intuitively, let the two dimensions represent as much original information as possible, we don't want a (linear) correlation between them. Because correlation means that the two dimension are not completely independent, there must be repeated information.
Mathematically, the covariance of two dimensions can be used to indicate their correlation. Since each dimension has been made equal to 0, then:![](https://www.zhihu.com/equation?tex=Cov%28a%2Cb%29%3D%5Cfrac%7B1%7D%7Bm%7D%5Csum_%7Bi%3D1%7D%5Em%7Ba_ib_i%7D)

When the covariance is 0, it means that the two fields are completely independent. 
In order to make the covariance 0, we choose the second basis only in the direction orthogonal to the first basis. 
Therefore the two directions chosen ultimately must be orthogonal.

So far, we have obtained the optimization goal of the dimension reduction problem: reduce a set of N-dimensional vectors to K-dimensional (K is greater than 0, less than N), and the goal is to select K units orthogonal bases, so that after the original data is transformed onto the set of bases, the covariance between the two dimensions is 0, and the variance of every dimension is as large as possible.

### 5.3 Covariance matrix
We have exported the optimization goal above, but this goal does not seem to be directly an operational guide (or algorithm), because it only says what it is, but it does not say how to do it. 
So we have to continue to study the calculation scheme in mathematics.

We see that the ultimate goal is closely related to the variance within every dimension and the covariance between different dimension. 
Therefore, we hope that we can express the two together. We can observe that both can be expressed as the form of inner product, and the inner product is closely related to the matrix multiplication. 
So we came to the inspiration:
Suppose we only have two dimension a and b, then we group them into rows by matrix X:![](https://www.zhihu.com/equation?tex=X%3D%5Cbegin%7Bpmatrix%7D+a_1+%26+a_2+%26+%5Ccdots+%26+a_m+%5C%5C+b_1+%26+b_2+%26+%5Ccdots+%26+b_m+%5Cend%7Bpmatrix%7D)
Then we multiply X by the transpose of X and multiply the factor by 1/m:
![](https://www.zhihu.com/equation?tex=%5Cfrac%7B1%7D%7Bm%7DXX%5E%5Cmathsf%7BT%7D%3D%5Cbegin%7Bpmatrix%7D+%5Cfrac%7B1%7D%7Bm%7D%5Csum_%7Bi%3D1%7D%5Em%7Ba_i%5E2%7D+%26+%5Cfrac%7B1%7D%7Bm%7D%5Csum_%7Bi%3D1%7D%5Em%7Ba_ib_i%7D+%5C%5C+%5Cfrac%7B1%7D%7Bm%7D%5Csum_%7Bi%3D1%7D%5Em%7Ba_ib_i%7D+%26+%5Cfrac%7B1%7D%7Bm%7D%5Csum_%7Bi%3D1%7D%5Em%7Bb_i%5E2%7D+%5Cend%7Bpmatrix%7D)
The miracle has appeared! 
The two elements on the diagonal of this matrix are the variance of the two dimensions, while the other elements are the covariance of a and b. 
The two are unified into a matrix!

## 6. Diagonalization of covariance matrix 

Based on the above derivation, we find that to achieve optimization, it is equivalent to diagonalizing the covariance matrix: that is, the elements other than the diagonal are 0, and the elements are arranged on the diagonal from top to bottom. 
So that we have achieved the goal of optimization. 
This may not be very clear. Let us look further at the relationship between the original matrix and the matrix covariance matrix after the basis transformation:

Let the covariance matrix corresponding to the original data matrix **X** be **C**, and **P** be a matrix of bases in rows. Let **Y=PX**, then **Y** is the data after **X** transforms by **P**. 
Let covariance matrix of **Y** be **D**, let's deduce the relationship between **D** and **C**:![](https://www.zhihu.com/equation?tex=%5Cbegin%7Barray%7D%7Bl+l+l%7D+D+%26+%3D+%26+%5Cfrac%7B1%7D%7Bm%7DYY%5E%5Cmathsf%7BT%7D+%5C%5C+%26+%3D+%26+%5Cfrac%7B1%7D%7Bm%7D%28PX%29%28PX%29%5E%5Cmathsf%7BT%7D+%5C%5C+%26+%3D+%26+%5Cfrac%7B1%7D%7Bm%7DPXX%5E%5Cmathsf%7BT%7DP%5E%5Cmathsf%7BT%7D+%5C%5C+%26+%3D+%26+P%28%5Cfrac%7B1%7D%7Bm%7DXX%5E%5Cmathsf%7BT%7D%29P%5E%5Cmathsf%7BT%7D+%5C%5C+%26+%3D+%26+PCP%5E%5Cmathsf%7BT%7D+%5Cend%7Barray%7D)
Things are very clear now! 
The **P** we are looking for is not the other, but that can diagonalize the original covariance matrix. 
In other words, the optimization goal becomes to find a matrix **P**, which can make **PCP**^T is a diagonal matrix. And the diagonal elements are arranged in order from largest to smallest.
Then the first K rows of **P** are the bases to be searched. Multiplying the matrix consisting of the first K rows of **P** by **X** makes **X** descend from N dimension to K dimension and satisfies the above optimization goal.

At this point, we are only one step away from the "invention"  of PCA!

Now all the focus is on the diagonalization of the covariance matrix. Sometimes, we should really thank the mathematician. It is known from the above that the covariance matrix **C** is ​​a symmetric matrix. In linear algebra, the real symmetric matrix has a series of very good properties such as the eigenvectors corresponding to different eigenvalues ​​of real symmetric matrices must be orthogonal.

A real symmetric matrix of n rows and n columns must find n unit orthogonal eigenvectors:
![](https://www.zhihu.com/equation?tex=E%3D%5Cbegin%7Bpmatrix%7D+e_1+%26+e_2+%26+%5Ccdots+%26+e_n+%5Cend%7Bpmatrix%7D)
Then we have the following conclusion about the covariance matrix **C**:![](https://www.zhihu.com/equation?tex=E%5E+%5Cmathsf%7BT%7DCE%3D%5CLambda%3D%5Cbegin%7Bpmatrix%7D+%5Clambda_1+%26+%26+%26+%5C%5C+%26+%5Clambda_2+%26+%26+%5C%5C+%26+%26+%5Cddots+%26+%5C%5C+%26+%26+%26+%5Clambda_n+%5Cend%7Bpmatrix%7D)
The diagonal element is the eigenvalue corresponding to each eigenvector.

Here, we find that we have found the matrix **P**:![](https://www.zhihu.com/equation?tex=P%3DE%5E%5Cmathsf%7BT%7D)

So far we have completed the discussion of the mathematical principles of the entire PCA. 
In the next section, we will give an example of PCA.

- to be continued ：）


