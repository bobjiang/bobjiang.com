---
title: "敏捷估算--Scrum入门基础系列"
date: "2015-05-14"
coverImage: "estimation_all.jpg"
---

本文谈及的均为Scrum中的估算行为，这些方法不是Scrum原创的。

## 为什么要估算

谈估算，我想先从为什么要做估算谈起。

每次在我的培训课上，学员们会给出各种各样的答案。比如为了估计成本、为了设定发布日期、为了知道什么时候可以做完、为了……。但我认为估算最重要的目的是为了

**达成共识**

如果没有进行估算，关于需求或任务会有一些假设或者背景被忽略掉。因此在Scrum中，估算是一个集体行为，而不是某个专家拍拍脑袋出来的结果。

## 如何做估算

估算的方式分为两大类，绝对估算和相对估算。绝对估算耗时更长，并且需要依赖上下文，最后的结果也会产生较大误差。而与之相对，相对估算更快，结果容易达成一致。Scrum中对产品列表（product backlog）的估算常常使用的就是相对估算，估算单位为故事点（没有意义的单位）。【注意：不要将故事点和小时数做一一对应！】最常用的方法就是计划扑克。

计划扑克是由斐波那契数列组成的一串数字扑克，如下图：

[![crispdeck](http://bobjiang.com/wp-content/uploads/2015/05/crispdeck.jpg)](http://bobjiang.com/wp-content/uploads/2015/05/crispdeck.jpg)

对产品列表条目（product backlog item）进行估算的步骤，简单描述如下：

1. 首先估算需要开发团队所有成员参加，每个人手里有一套上图的扑克
2. 取出一个产品列表条目，产品负责人进行描述
3. 每个团队成员根据自己的理解，拿出一张代表估算值的扑克并扣着放在桌面上。（这个过程不要讨论，不要说话，不要把你的结果告诉其他人，具体原因参见百度百科“[锚效应](http://baike.baidu.com/link?url=3iKvloFmsvMtKlbr6a7DRTz9GLihVcb7Yroj37_tqxwjqGnnKD9Qj0TZcnRBX3h4bNCIf07RrykWYNzfcfr2Nq)”）
4. 所有成员出牌完成后，大家同时亮出自己的结果
5. 接下来邀请估算最小的成员解释一下原因，还要邀请估算最大的成员解释一下原因。讨论过程中注意遵守团队礼节。
6. 解释完毕后，重复步骤3到步骤5，直至最后大家的估算结果一致。

相对估算还有另外一种方法，称为三角估算法。

1. 从产品列表中挑选一个较小但不是最小的条目，比如条目A，并设定它的估算值为3 （故事点）
2. 从产品列表的最上面取出一个条目B，和A进行对比。如果比A大，放在A的右边。如果比A小，放在A的左边。如果和A差不多大小，放在A的下面。
3. 继续从产品列表取出条目C，重复步骤2，分别和条目A与条目B进行比较。直到为条目C找到合适的位置。
4. 重复步骤2和步骤3，直至所有的产品列表条目都完成放置。
5. 比较一下A左边的产品列表条目，估算值为2还是1，把左边的所有条目估算值设置为2或1.同样的把A右边的条目，按列标明估算值。
6. 最后的结果如下图：

[![123](http://bobjiang.com/wp-content/uploads/2015/05/123.jpg)](http://bobjiang.com/wp-content/uploads/2015/05/123.jpg)

Scrum入门基础系列：

- [Scrum入门基础系列之Scrum起源](http://bobjiang.com/scrum_history/)
- [Scrum入门基础系列之Scrum框架](http://bobjiang.com/scrum_framework/)
- [Scrum入门基础系列之Scrum角色](http://bobjiang.com/scrum_role/)
- [Scrum入门基础系列之Scrum会议](http://bobjiang.com/scrum_meeting/)
- [Scrum入门基础系列之Scrum工件](http://bobjiang.com/scrum_foundation_artifact/)
- [Scrum入门基础系列之Scrum需求梳理](http://bobjiang.com/scrum_product_backlog_refinement/)
- [Scrum入门基础系列之Scrum估算](http://bobjiang.com/estimation_in_scrum/)
