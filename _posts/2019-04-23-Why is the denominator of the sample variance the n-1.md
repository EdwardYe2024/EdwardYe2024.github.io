---
layout:     post
title:      Why is the denominator of the sample variance the n-1?
subtitle:   
date:       2019-05-12
author:     Feng Ye
header-img: img/post-bg-2015.jpg
catalog: true
tags:
    - Statistic
---
To answer this question, the lazy way is to go to see the mathematical proof of this equation:
![](https://www.zhihu.com/equation?tex=%5Cmathbb%7BE%7D%5CBig%5B%5Cfrac%7B1%7D%7Bn-1%7D+%5Csum_%7Bi%3D1%7D%5En%5CBig%28X_i+-%5Cbar%7BX%7D%5CBig%29%5E2+%5CBig%5D%3D%5Csigma%5E2)
But this answer is obviously not intuitive enough (the statistician in the textbook has become magical and somehow got the above equation). 
Below I will provide a slightly more friendly explanation.

The purpose of the denominator in the sample variance calculation formula is to make the estimation of the variance unbiased. An unbiased estimator is more intuitive than a biased estimator, although some statisticians think that it is more meaningful to make the mean square error, i.e. MSE, the least. It is intuitively why the denominator must be made instead of making the estimate unbiased. I believe this is the real confusion of the subject.

First, we assume that the mathematical expectation \mu of a random variable ***X*** is known, but the variance is unknown. Under this condition, according to the definition of variance we have![](https://www.zhihu.com/equation?tex=%5Cmathbb%7BE%7D%5CBig%5B%5Cbig%28X_i+-%5Cmu%5Cbig%29%5E2+%5CBig%5D%3D%5Csigma%5E2%2C+%5Cquad%5Cforall+i%3D1%2C%5Cldots%2Cn%2C)
We can get
![](https://www.zhihu.com/equation?tex=%5Cmathbb%7BE%7D%5CBig%5B%5Cfrac%7B1%7D%7Bn%7D+%5Csum_%7Bi%3D1%7D%5En%5CBig%28X_i+-%5Cmu%5CBig%29%5E2+%5CBig%5D%3D%5Csigma%5E2)

Therefore, it is an unbiased estimate of the variance. The denominator in the note is just right **n**!

This result is intuitive and obvious in mathematics. 
Now, we consider the case where the mathematical expectation of a random variable is unknown. 
At this time, we will tend to replace the \mu above formula with the sample mean. What are the consequences of this? 
The consequence is that if you use it directly as an estimate, then you will tend to underestimate the variance!
This is because![](https://www.zhihu.com/equation?tex=%5Cbegin%7Beqnarray%7D%0A%5Cfrac%7B1%7D%7Bn%7D%5Csum_%7Bi%3D1%7D%5En%28X_i-%5Cbar%7BX%7D%29%5E2+%26%3D%26%0A%5Cfrac%7B1%7D%7Bn%7D%5Csum_%7Bi%3D1%7D%5En%5CBig%5B%28X_i-%5Cmu%29+%2B+%28%5Cmu+-%5Cbar%7BX%7D%29+%5CBig%5D%5E2%5C%5C%0A%26%3D%26%0A%5Cfrac%7B1%7D%7Bn%7D%5Csum_%7Bi%3D1%7D%5En%28X_i-%5Cmu%29%5E2+%0A%2B%5Cfrac%7B2%7D%7Bn%7D%5Csum_%7Bi%3D1%7D%5En%28X_i-%5Cmu%29%28%5Cmu+-%5Cbar%7BX%7D%29%0A%2B%5Cfrac%7B1%7D%7Bn%7D%5Csum_%7Bi%3D1%7D%5En%28%5Cmu+-%5Cbar%7BX%7D%29%5E2+%5C%5C%0A%26%3D%26%0A%5Cfrac%7B1%7D%7Bn%7D%5Csum_%7Bi%3D1%7D%5En%28X_i-%5Cmu%29%5E2+%0A%2B2%28%5Cbar%7BX%7D-%5Cmu%29%28%5Cmu+-%5Cbar%7BX%7D%29%0A%2B%28%5Cmu+-%5Cbar%7BX%7D%29%5E2+%5C%5C%0A%26%3D%26%5Cfrac%7B1%7D%7Bn%7D%5Csum_%7Bi%3D1%7D%5En%28X_i-%5Cmu%29%5E2+%0A-%28%5Cmu+-%5Cbar%7BX%7D%29%5E2+%0A%5Cend%7Beqnarray%7D)
In other words, unless the sample mean is just right the mathematical expectation, we must have![](https://www.zhihu.com/equation?tex=%5Cfrac%7B1%7D%7Bn%7D%5Csum_%7Bi%3D1%7D%5En%28X_i-%5Cbar%7BX%7D%29%5E2+%3C%5Cfrac%7B1%7D%7Bn%7D%5Csum_%7Bi%3D1%7D%5En%28X_i-%5Cmu%29%5E2+)

The one on the right side of the inequality is the "correct" estimate of the variance! 
This inequality explains why direct use of ![](https://www.zhihu.com/equation?tex=%5Cfrac%7B1%7D%7Bn%7D+%5Csum_%7Bi%3D1%7D%5En%5CBig%28X_i+-%5Cbar%7BX%7D%5CBig%29%5E2+)can lead to underestimation of the variance.
Then, under the premise of not knowing the true mathematical expectation of random variables, how to estimate the variance correctly? 

The answer is to replace the denominator n in the above formula with n-1. By using this method to "magnify" the original small estimate, we can get the correct estimate of the difference:
![](https://www.zhihu.com/equation?tex=%5Cmathbb%7BE%7D%5CBig%5B%5Cfrac%7B1%7D%7Bn-1%7D+%5Csum_%7Bi%3D1%7D%5En%5CBig%28X_i+-%5Cbar%7BX%7D%5CBig%29%5E2%5CBig%5D%3D%5Cmathbb%7BE%7D%5CBig%5B%5Cfrac%7B1%7D%7Bn%7D+%5Csum_%7Bi%3D1%7D%5En%5CBig%28X_i+-%5Cmu%5CBig%29%5E2+%5CBig%5D%3D%5Csigma%5E2.)

As for why the denominator is n-1 not n-2, or something else, it is best to see the real mathematical proof, because the fundamental purpose of mathematical proof is to tell people "why".

