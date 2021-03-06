---
layout: post
title: "2019-4-10"
author: "iSika"
---

## 题意
给n层的一个塔涂色，有三种颜色可选，涂R得分为A，涂G得分为A+B，涂B得分为B，不涂得分为0，请问要正好得分k有多少种方式。n的范围是10^5。
## 思路
首先明确，可供我们做出的选择是什么？
```

对于塔的每一层，我们需要从以下四种可能性里选择一种。
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190409231456585.PNG)

由于G的得分恰到好处的等于A+B，这说明它可以用R和B来表示，这一点需要引起我们的注意。
我们将每一层看作涂两种颜色R和B，第一位为1表示涂B，为0表示不涂，第二位为1表示涂R，为0表示不涂，因此我们可以把四种涂色方案规范化为2种涂色方案(涂B或不涂，涂R或不涂)的组合。

设涂B的位置个数为X，涂R的位置个数为Y，X与Y满足等式
```
X*A+Y*B=k
```
移项，可以得到
```
Y=(k-X*a)/B
```
因此，Y和X的关系得到了确认，我们尝试着枚举所有的X，如果能够得到整数的Y，则说明这一对<X,Y>满足题意。
那么问题转化为，涂B的位置个数为X，涂R的位置个数为Y，共有几种涂法。
涂B的位置个数为X的涂法为
```
C(n,X)//从n个里选出x的方案数
```
涂R的位置个数为Y的涂法为
```
C(n,Y)//从n个里选出y的方案数
```
因为涂第一个位置和第二个位置是相互独立的，根据乘法公式
```
Ans=C(n,X)*C(n,Y)
```
对于所有枚举中合法的X与Y，将Ans进行累加即为最终结果
