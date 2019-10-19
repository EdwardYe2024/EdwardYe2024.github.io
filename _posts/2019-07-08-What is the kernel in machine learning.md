---
layout:     post
title:      What is the kernel in machine learning?
subtitle:  
date:       2019-07-08
author:     Feng Ye
header-img: img/post-bg-os-metro.jpg
catalog: true
tags:
    - Matrix
---
## Definition
Firstly, I give a definition directly: Kernel function is K(x, y) = <f(x), f(y)>, where x and y are n-dimensional input values, f(·) is a mapping from n-dimensional to m-dimensional (usually, m>>n). And <x, y> is the inner product of x and y. Strictly speaking, it should be called the standard inner product of the Euclid space, which is the dot product that many people often say.

Just look at this definition, you still do not understand what the kernel is... right? Don't worry. A good knowledge sharer will not leave a hollow definition. He or she should tell you the intuition of the concept, then give you some examples, and finally tell you a few application scenarios.

Intuitively, to calculate <f(x), f(y)>, we need to calculate f(x) and f(y) separately firstly, and then calculate their inner product. The  definition above also indicates that after x and y are mapped, the dimension is greatly increased, and the cost of calculating the inner product may be very large. And in the high-dimensional space, the inner product is calculated costly, and the inner product is a scalar. That is to say, it pulls our calculations from high dimensional space back to one dimensional space! So we especially want a "simple algorithm" that helps us calculate the desired inner product without in the high-dimensional space. It’s turn to come to our main character-kernel, it can help us do this.

For instance:
x = (x1, x2, x3, x4); y = (y1, y2, y3, y4);
f(x) = (x1x1, x1x2, x1x3, x1x4, x2x1, x2x2, x2x3, x2x4, x3x1, x3x2, x3x3, x3x4, x4x1, x4x2, x4x3, x4x4); 
Kernel function is K(x, y) = (<x, y>)^2
Next, let's take a few simple numbers and see what the result is.
x = (1, 2, 3, 4); y = (5, 6, 7, 8).
Thus, f(x) = ( 1,   2,   3,   4,   2,   4,   6,  8,  3,   6,   9,  12,  4,  8, 12, 16) ;
f(y) = (25, 30, 35, 40, 30, 36, 42, 48, 35, 42, 49, 56, 40, 48, 56, 64) ;
<f(x), f(y)> = 25+60+105+160+60+144+252+384+105+252+441+672+160+384+672+1024 = **4900**.

Mapping data in four-dimensional space into sixteen-dimensional space, you must feel tired, right?
But what if we use a kernel function?
K(x, y) = (5+12+21+32)^2 = 70^2 = **4900**.
**That's it!**

So now you can see it, the kernel is actually a "simple algorithm" that saves us from tedious calculations in high-dimensional space. Even, it can solve the problem that infinite dimensional space can't be calculated! Because sometimes f(·) will map n-dimensional space to infinite dimensional space, we often do nothing about it unless we use kernel, especially the RBF kernel:
![](/img/in-post/RBF.png)