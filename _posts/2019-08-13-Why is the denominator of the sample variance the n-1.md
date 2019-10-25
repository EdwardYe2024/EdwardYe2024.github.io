---
layout:     post
title:      Why is the denominator of the sample variance the n-1?
subtitle:   
date:       2019-08-13
author:     Feng Ye
header-img: img/post-bg-universe.jpg
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

> to be continued

----------
## Update:

Let's go back to the denominator (n-1) of the Sample Variance. 
Since you are looking at this problem, you already know the formula for calculating the variance:![](https://www.zhihu.com/equation?tex=%5Csigma%5E%7B2%7D%3D+%5Cfrac%7B++%28x_%7B1%7D-%5Cmu%29+%5E%7B2%7D%2B%28x_%7B2%7D-%5Cmu%29+%5E%7B2%7D%2B...%2B%28x_%7Bn%7D-%5Cmu%29+%5E%7B2%7D+%7D+%7Bn%7D)

Let's compare the variance and the sample variance: The variance is an objective fact, an objective description of all the individual data. 
The sample variance is more like an opinion, which is an estimation, or prediction, that we make based on a small sample of individuals. 

Since the sample variance is not a fact, but an opinion, it is an estimate. In order to make this estimate as close as possible to the fact, it is necessary to pay attention to the sample without deviation (Bias).

For example, 


- we can't just sample a batch of products, sample at a specific time. our random sampling must cover all batches as much as possible, and the sampling should have sufficient degrees of freedom and enough randomness. 


- Also note that there is an implicit association between variables in the sample, which we should avoid.
 
Let's look at an example. Suppose there are only two numbers x1 and x2 in the randomly extracted samples. If the two numbers are independent and randomly extracted, you can't guess x2 from x1. For example, I tell you x1=10, what is x2 equal to?
You can't get it at all, because random extraction makes no correlation between x2 and x1. 

However, what we did not expect was that because of the existence of a number, this random sampling produced an implicit relationship. 
This number is the mean of the samples which is needed to calculate the variance of the sample. It reduces the independence and freedom of random extraction by a little. 
Because the sample mean introduces some information, there is no longer a separate relationship between x1 and x2.

According to the mean formula:
![](https://www.zhihu.com/equation?tex=%5Cbar%7Bx%7D%3D%5Cfrac%7Bx_%7B1%7D%2Bx_%7B2%7D%7D%7B2%7D)

As long as you know x1 and the mean, you can calculate the value of x2. 
If x1=10,x_bar=10, then x2=10 Similarly, knowing x2 and the mean, we can calculate the value of x1. 
These two numbers are good and independent. 
In other words, it is not x1 or x2 that is problematic.
The problem is the mean, and the new information which is introduced reduces the independence between the sample data and increases the correlation. 
Or it can be said that with the intervention of the mean, the degrees of freedom of x1 and x2 are reduced. At first, there are two independent numbers. Now there is only one independent, and the other is no longer free.

Similarly, for more sample sizes: 
If the sample number is 3: x1,x2,x3, then if x1, x2, and the mean are known, we can  calculate x3, Independence, or degree of freedom, decrease from 3 to 2. 
If the sample number is 4: x1,x2,x3,x4, then if x1, x2, x3, and the mean are known, we can calculate x4, Independence, or degree of freedom, decrease from 4 to 3. 
... 
If the sample number is n: x1,x2,x3...xn, then if x1, x2, xn-1, and the mean are known, we can calculate xn, Independence or degree of freedom, decrease from n to n-1. 

The mean value reduces the sample's independence or degree of freedom by one, resulting in a bias in the sample.

This is why the denominator of the sample variance is not n, nor is it n-2 or n-3, but  n-1.  

