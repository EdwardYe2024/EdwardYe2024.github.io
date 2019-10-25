---
layout:     post
title:      What is the meaning of the p value in the statistical hypothesis test?
subtitle:   
date:       2019-07-18
author:     Feng Ye
header-img: img/404-bg.jpg
catalog: true
tags:
    - Statistic
---

When it comes to probability and statistics, we must start by throwing coins. 

## 1. What is a hypothesis test?

You say that your coin is fair, that is, the probability of 'head' and 'tail' appearing is similar.

Then, you want to bet with me, but how can I believe your words. Thus, I propose to check if your coin is fair. What if you have two sides of "head"? 

You look nervous, and do not let me check, then we put forward a compromise plan, throw a few coins to see if the result is fair.

Thrown a total of twice, all 'head' face up. Although the probability is 0.5*0.5 = 0.25, but it is normal. So we continue to throw the coin.

I throw it a total of four times, and all of them are 'head' facing up. The probability is 0.5^4 = 0.0625. I feel a bit abnormal, but what if it is luck? 
Continue to throw.

I throw it a total of ten times, and all of them are "head" facing up. Then I think it is very likely that your coin is not fair.

This is the **hypothesis test**:
- You make the hypothesis: your coin is fair
- I propose to test your hypothesis: throw ten times and see if the result of the experiment matches your hypothesis.

## 2. P-value
In order to complete the hypothesis test, we need to define a concept: P-value. 
Let us explain what is the P value here?

According to the above description, the idea of ​​the hypothesis test here is:
- Hypothesis: the coin is fair
- Test: if the hypothesis is true, then throw it ten times to see if the result matches the hypothesis

Throwing coins repeatedly should conform to the binomial distribution, that is:

![](https://www.zhihu.com/equation?tex=X%5Csim+B%28n%2C%5Cmu+%29%5C%5C)

where the number n is times the coin is thrown and miu the probability that the 'head' is facing up.

On the premise that we believe the coin is fair, throwing 10 coins should match the following distribution:

![](https://www.zhihu.com/equation?tex=X%5Csim+B%2810%2C+0.5%29%5C%5C)

The figure below shows the distribution map if the coin is fair:

![](/img/in-post/Pvalue/bn2.jpg)

The result I got after throwing it ten times was that there were eight 'head':

![](/img/in-post/Pvalue/bn3.jpg)

At this time, there is a mathematician that defines a concept called p-value:

![](/img/in-post/Pvalue/bn4.jpg)

Add eight 'head' probabilities to the more extreme nine and ten 'head' probabilities:

![](/img/in-post/Pvalue/bn5.jpg)

What is obtained is (single-sided P value):

![](https://www.zhihu.com/equation?tex=%5Ctext+%7Bp-value%7D%3DP%288%5Cleq+X%5Cleq+10%29%3D0.05%5C%5C)

In fact, the probability of two 'head', one 'head', zero 'head' is also extremely extreme:
![](https://pic2.zhimg.com/50/v2-f3e94c81ba5e5e9b460628d245735bc9_hd.jpg)

Thus, two-sided P-value:
![](https://www.zhihu.com/equation?tex=%5Ctext+%7Bp-value%7D%3DP%280%5Cleq+X%5Cleq+2%29%2BP%288%5Cleq+X%5Cleq+10%29%3D0.1%5C%5C)

### 2.1 Why adding more extreme situations? ###

According to the example of throwing coins, you may feel that I know that eight times of 'head' appearances are not normal. Why do you want to add nine or ten times?

I think there is such a real reason, for example, I have to throw 1000 coins to test whether the hypothesis is correct.

It is very troublesome to calculate the possibility with binomial distribution when the coin is thrown 1000 times. According to the central limit theorem, we know that we can approximate with a normal distribution.

![](https://pic2.zhimg.com/80/v2-a3570c77ffb6c1459cf84ed22d89992d_hd.jpg)

For example, I threw 1000 times and got 530 'head'. It is easier to calculate with a normal distribution.

However, for a normal distribution, I have no way to calculate the probability of a single point (the probability of a single point of continuous distribution is 0), I can only take one interval to calculate the limit. So I can take the interval of 530 and more extreme points.
![](https://pic4.zhimg.com/80/v2-1edee362d8d7c580de010ee7dca8fc6b_hd.jpg)

## 3. Significance level

After throwing a total of 10 coins, is it 7 times 'head' or 9 times, I can confirm that "coins are unfair".

We generally think:![](https://www.zhihu.com/equation?tex=%5Ctext+%7Bp-value%7D%5Cleq+0.05%5C%5C)
It can be assumed that the hypothesis is incorrect.

The standard of 0.05 is a significant level, of course, the choice of how much as a significant level is also subjective.

For example, if the above example of coin tossing takes a one-sided P-value, then according to our calculation, if you throw 10 times, there are 9 positive 'head':
![](https://www.zhihu.com/equation?tex=%5Ctext+%7Bp-value%7D%3DP%289%5Cleq+X%5Cleq+10%29%3D0.01%5Cleq+0.05%5C%5C)

This condition is 'significant', that is, "coins are unfair."

## 4. Relationship with confidence intervals

Knowledge needs to be linked, it can help us better understand these concepts.

Confidence interval, the purpose is to construct an interval based on the sample, and then hope that this interval can include the true value, but we do not know what the true value is.

The hypothesis test is to assume what the true value is, and then test whether this hypothesis may be true.

The reason why we feel that they are related is probably because they all mentioned 0.05.

The relationship between them is also simple. If the hypothesis we propose is within the confidence interval of the sample, the hypothesis is true.

![](https://pic1.zhimg.com/80/v2-6704ace6b06b1ebe0356ca5c23bdae18_hd.jpg)

On the contrary, it cannot pass the hypothesis test.

![](https://pic3.zhimg.com/80/v2-64103ea87cbd4d54e046bc164832032d_hd.jpg)

