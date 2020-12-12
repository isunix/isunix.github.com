---
layout: post
title: "对(大)数据分析工作的一些思考"
date: 2019-07-20 08:50:36 +0800
comments: true
categories: Blog
---
如果把之前在Sonata Services做anti spam的工作也算是数据分析的话(确实跟数据分析沾边, 当时招聘的时候，就说懂机器学习是个加分项。 其实我们当时所做的工作，可以用"专家系统"来概括: 通过我们的知识和经验，去写规则和脚本去anti spam), 再加上在华米科技的这3年多做大数据分析的经历，也算是一个在数据分析领域，浸淫了快7年之久的人了， 如果再加上大学四年的"信息与计算科学"这个专业的学习经历的话(其实是3年，因为大一上半年是在农学类专业，大一下学期转到信息与计算科学)，那就是跟数据打交道了快10年的人了。往多了说10年，往少了说3年多， 也是该写点总结了。

BTW, 最近在看<<谁说菜鸟不会数据分析>>这本书， 发现自己的很多思考，跟书中提炼的内容，竟然不谋而合， 看来这本书还是不错的，哈哈哈。

从数据分析的技巧和方式上来看的话，可以分为:
1. 描述性数据分析
2. 探索性数据分析
3. 验证下数据分析

从数分析在日常工作中起到的作用来看的话，可以分为:
1. 现状分析
2. 原因分析
3. 预测分析

在<<谁说菜鸟不会数据分析>>这本书中，作者还总结了数据分析的6步曲:
1. 明确分析目的和思路
2. 数据收集
3. 数据处理
4. 数据分析
5. 数据展现
6. 报告撰写

其实，只要是在企业里做过数据分析的人， 这几步应该都是做过的，或许在报告的撰写这块， 不是每次都需要,尤其是做临时业务分析，并非每次都要写结论报告。

针对上面的6步曲，以我丰富的"描述性数据分析"的经验来看的话, 1-5都不难，只要受到专业的数学或者统计方面的训练， 加上一定的数据分析的专业工具和知识的培训，就可以上手了(如果一个人，连基本的统计概念都不清楚，你会对他做出的数据分析结果有信心么?)， 但是第6点的话， 就比较复杂了， 可能跟我这边"报告"撰写的少有关系，毕竟我们很多都是临时业务分析，不需要出报告， 而且报告的撰写，要有文字功底，要有优秀的思维能力， 要有不错的排版技术，要对业务足够的了解， 要对商业有一定的了解。

接下来说说数据分析的误区(参考自<<谁说菜鸟不会数据分析>>):
1. 分析目的不明确，为分析而分析
2. 缺乏业务知识，分析结果偏离实际
3. 一味追求使用高级方法，热衷研究模型

除了上面的3点，从我的经历中，我还要加上下面几点
1. 收集数据的时候，盲目相信数据的提供者； 比如有同事在找云端问数据在哪里的时候，云端说啥，他就认了，也不仔细思考，为啥用这个表，不用另外一个表？ 两个表有啥区别？ 
2. 分析出了数据，就完事了，也不去跟历史相似的数据，交叉比对，也不去想想我这个分析出来的额结果，有啥用？ 解决了数据需求者的问题了么？

接下来谈谈数据分析师的职业要求, 作者总结了以下几点
1. 懂业务
2. 懂管理
3. 懂分析
4. 懂工具
5. 懂设计

要做好一个数据分析师，难不难？ 很难。 很多人在 "懂分析" 和 "懂工具" 这块，就做的不好了， 而其实"懂分析" 和 "懂工具" 其实应该是做为一个数据分析师的硬性和基本的要求。做过几年数据分析的人，应该都能理解 "懂业务", "懂管理" 和 "懂设计" 对于一个数据分析师来说，也是非常重要的。 "懂分析" 和 "懂工具" 决定了你能不能成为一个分析师，而是不是"懂业务", "懂管理" 和 "懂设计"， 则决定了，你是不是一个好的分析师。 遗憾的是，我自己在后三点上，虽然有意培养自己在这块的能力和意识，但是并非优秀。 

作者也总结了数据分析师的基本素质，列在这里:
1. 态度严谨负责
2. 好奇心强烈
3. 逻辑思维清晰
4. 擅长模仿学习
5. 勇于创新

除了这5点，我想加上我自己的理解，毕竟数据分析师是要在公司或者各种机构里工作的，是要跟人合作的, 应该具备如下的素质:
1. 要有很好的workflow优化意识，很好的自我管理
2. 要有不错的编码能力和规范, 代码管理工具使用能力
3. 扎实的数理知识

看起来很像招聘贴子中的条款是吧？ 是的，但是这个就是现实， 数据分析师要到真实的环境中去，要成为一个合格的team player， 上面说的三点，最好是都具备。要不然，就落入下乘了。

Play with data and have fun!







