---
layout:     post
title:      What is the meaning of the p value in the statistical hypothesis test?
subtitle:   
date:       2019-04-23
author:     Feng Ye
header-img: img/post-bg-os-metro.jpg
catalog: true
tags:
    - Matrix
---

When it comes to probability and statistics, we must start by throwing coins. 

## 1. What is a hypothesis test?

You say that your coin is fair, that is, the probability of "head" and "tail" appearing is similar.

Then, you want to bet with me, but how can I believe your words. Thus, I propose to check if your coin is fair. What if you have two sides of "head"? 

You look nervous, and do not let me check, then we put forward a compromise plan, throw a few coins to see if the result is fair.

Throwed a total of twice, all "head" face up. Although the probability is 0.5*0.5 = 0.25, but it is normal. So we continue to throw the coin.

I throw it a total of four times, and all of them are "head" facing up. The probability is 0.5^4 = 0.0625. I feel a bit abnormal, but what if it is luck? 
Continue to throw.

I throw it a total of ten times, and all of them are "head" facing up. Then I think it is very likely that your coin is not fair.

This is the **hypothesis test**:
- You make the hypothesis: your coin is fair
- I propose to test your hypothesis: throw ten times and see if the result of the experiment matches your hypothesis.

## 2. P value
In order to complete the hypothesis test, we need to define a concept: P value. 
Let us explain what is the P value here?

According to the above description, the idea of ​​the hypothesis test here is:
- Hypothesis: the coin is fair
- Test: if the hypothesis is true, then throw it ten times to see if the result matches the hypothesis

Throwing coins repeatedly should conform to the binomial distribution, that is:

![](/img/in-post/Pvalue/bn.png)

where the number n is times the coin is thrown and miu the probability that the "head" is facing up.

On the premise that we believe the coin is fair, throwing 10 coins should match the following distribution:

![](/img/in-post/Pvalue/bn1.svg)



