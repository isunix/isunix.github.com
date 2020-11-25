---
layout: post
title: "Gradient Boosting Algorithm"
date: 2019-08-14 13:51:36 +0800
comments: true
categories: Data&ML&AI
---
## 想要了解xgboost，至少需要了解以下的一些概念：
`梯度`, `Boosting`, `分类器`, `决策树`, `概率分布`, `CART`, `损失函数`, `分裂准则`, `加法模型`, `叶子节点`, `分裂点`, `学习率`, `分类`, `回归`, `初始化`, `泰勒公式`, `贪心法`, `信息增益`, `信息增益比`, `特征`, `特征值`, 

## Gradient Boosting Algorithm 算法参考链接：

- [XGBoost: A Scalable Tree Boosting System](https://arxiv.org/pdf/1603.02754v1.pdf)
- [Which algorithm takes the crown: Light GBM vs XGBOOST?](https://www.analyticsvidhya.com/blog/2017/06/which-algorithm-takes-the-crown-light-gbm-vs-xgboost/)
- [Learn Gradient Boosting Algorithm for better predictions (with codes in R)](https://www.analyticsvidhya.com/blog/2015/09/complete-guide-boosting-methods/)
- [Getting smart with Machine Learning – AdaBoost and Gradient Boost](https://www.analyticsvidhya.com/blog/2015/05/boosting-algorithms-simplified/)
- [Quick Introduction to Boosting Algorithms in Machine Learning](https://www.analyticsvidhya.com/blog/2015/11/quick-introduction-boosting-algorithms-machine-learning/)
- [Complete Machine Learning Guide to Parameter Tuning in Gradient Boosting (GBM) in Python](https://www.analyticsvidhya.com/blog/2016/02/complete-guide-parameter-tuning-gradient-boosting-gbm-python/)
- [Complete Guide to Parameter Tuning in XGBoost with codes in Python](https://www.analyticsvidhya.com/blog/2016/03/complete-guide-parameter-tuning-xgboost-with-codes-python/)
- [XGboost数据比赛实战之调参篇](https://segmentfault.com/a/1190000014040317)
- [通俗的将Xgboost的原理讲明白](http://www.sohu.com/a/226265476_609569)
- [决策树](https://blog.csdn.net/app_12062011/article/details/52136117) 和 [决策树源码剖析](https://blog.csdn.net/zhaocj/article/details/50503450)
- [XGBoost 笔记]([http://matafight.github.io/2017/03/14/XGBoost-%E7%AE%80%E4%BB%8B/](http://matafight.github.io/2017/03/14/XGBoost-简介/))
- [XGBoost如何避免过拟合](https://blog.csdn.net/liuzonghao88/article/details/88808408)
- [XGBoost调参笔记](https://blog.csdn.net/u012735708/article/details/83651832)
- [xgboost中的数学原理](https://blog.csdn.net/a358463121/article/details/68617389)
- [xgboost入门与实战](https://blog.csdn.net/sb19931201/article/details/52557382)
- [XGBoost参数调优](https://blog.csdn.net/xiaocong1990/article/details/55107239)
- [xgboost：一个纯小白的学习历程](https://blog.csdn.net/Totoro1745/article/details/53328725)
- [通俗、有逻辑的写一篇说下Xgboost的原理](https://blog.csdn.net/github_38414650/article/details/76061893)
- [Boosting algorithm: GBM](https://towardsdatascience.com/boosting-algorithm-gbm-97737c63daa3)
- [LightGBM 调参方法](https://www.imooc.com/article/43784?block_id=tuijian_wz)
- [Good summary of XGBoost vs CatBoost vs LightGBM](https://www.kaggle.com/c/LANL-Earthquake-Prediction/discussion/89909)
- [LightGBM + XGBoost + Catboost](https://www.kaggle.com/samratp/lightgbm-xgboost-catboost)
- [lightgbm-vs-xgboost-vs-catboost](https://datascience.stackexchange.com/questions/49567/lightgbm-vs-xgboost-vs-catboost)
- [Gradient Boosting Decision trees: XGBoost vs LightGBM (and catboost)](https://medium.com/kaggle-nyc/gradient-boosting-decision-trees-xgboost-vs-lightgbm-and-catboost-72df6979e0bb)
- [CatBoost vs. Light GBM vs. XGBoost](https://towardsdatascience.com/catboost-vs-light-gbm-vs-xgboost-5f93620723db)
- [CatBoost vs. Light GBM vs. XGBoost 的中文翻译](https://blog.csdn.net/LrS62520kV/article/details/79620615)
- [关于lightgbm的安装](https://stackoverflow.com/questions/44937698/lightgbm-oserror-library-not-loaded)
- [Custom Loss Functions for Gradient Boosting](https://towardsdatascience.com/custom-loss-functions-for-gradient-boosting-f79c1b40466d)
- [machine-learning-challenge-winning-solutions-lightgbm-winned](https://github.com/Microsoft/LightGBM/blob/master/examples/README.md#machine-learning-challenge-winning-solutions)
- [LightGBM 如何调参](https://www.jianshu.com/p/b4ac0596e5ef)
- [xgboost调参](https://www.cnblogs.com/ljygoodgoodstudydaydayup/p/6665239.html)
- [为什么负梯度是函数值减小的最快方向](https://zhuanlan.zhihu.com/p/57601606)
- [GBDT原理与Sklearn源码分析-回归篇](https://blog.csdn.net/qq_22238533/article/details/79185969)
- [GBDT原理与Sklearn源码分析-分类篇](https://blog.csdn.net/qq_22238533/article/details/79192579?utm_medium=distribute.pc_relevant.none-task-blog-title-6&spm=1001.2101.3001.4242)
- [GBDT原理与实践-多分类篇](https://blog.csdn.net/qq_22238533/article/details/79199605)
- [XGBoost超详细推导，终于有人讲明白了](https://cloud.tencent.com/developer/article/1513111)
- [珍藏版 | 20道XGBoost面试题](https://mp.weixin.qq.com/s?__biz=MzI1MzY0MzE4Mg==&mid=2247485159&idx=1&sn=d429aac8370ca5127e1e786995d4e8ec&chksm=e9d01626dea79f30043ab80652c4a859760c1ebc0d602e58e13490bf525ad7608a9610495b3d&scene=21#wechat_redirect)
