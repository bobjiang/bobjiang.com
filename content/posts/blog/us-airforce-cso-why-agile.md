---
title: "美国空军国防部企业级DevSecOps启动会探讨"
date: "2019-12-12"
url: "/ama-us-airforce-devsecops/"
tags: [devops, SAFe, devsecops, airforce]
---
本文是针对于最近网上流传的美国空军国防部企业级DevSecOps启动会上，对于敏捷的疑问展开讨论。
欢迎共同来探讨。

The CSO signed a Memorandum for Record on Nov 26th 2019, sent to all PEOs and PMs regarding the use of DevSecOps and Agile and highly discouraging from using rigid, prescriptive frameworks such as the Scaled Agile Framework (SAFe).
CSO（Chief Software Officer）首席软件官于2019年11月26日签署了一份备忘录，该备忘录已发送给所有PEO和PM，涉及使用DevSecOps和Agile以及**强烈不鼓励**使用诸如Scaled Agile Framework（SAFe）之类的严格定义的框架。

为什么？以下是CSO对于上述结论的理由：

1. DoD is still using Waterfall or Water-Agile-Fall so until we can truly implement basic Scrum/Kanban, there is nothing to « SCALE ». Agile should be applied across the entire Program, not just the development team, that includes: Contracting, Program Management, Reporting to leadership (no EVM) etc!
在我们真正实现基本的Scrum / Kanban之前，国防部（DoD）仍在使用Waterfall或Water-Agile-Fall，没有任何可以用来“规模化”（Scale）。 敏捷应该是应用于整个产品（Program），而不仅仅是开发团队，其中包括：合同、产品管理，向领导层报告（无EVM）等！

2. You cannot scale if you don’t have the “basics” right. At best, such frameworks put us at risk to fall back to what we know and go back to Waterfall because of their “mapping”.
如果“基本”（敏捷）没有做对，不可能规模化。SAFe这样的框架顶多让我们冒着风险，采用SAFe的“映射”又回到了我们熟知的瀑布模式。

3. SAFe might potentially be an useful framework for teams which do not use DevOps/DevSecOps but a key principle of DevSecOps is to decouple work and teams and the only synchronization required should be across Product Owners. Teams shouldn’t have to coordinate if they use a Service Mesh/Domain Driven Design/Microservices model. This doesn’t require a rigid framework. If you’re having issues implement this, you’re not implementing the right DevSecOps model.
对于不使用DevOps / DevSecOps的团队来说，SAFe可能是一个有用的框架，但是DevSecOps的关键原则是使工作和团队解耦，并且仅有的同步应该是在产品负责人之间进行的。如果团队使用服务网格（Service Mesh）/领域驱动设计（Domain Driven Design）/微服务模型的话，则团队之间无需协调。这不需要一个严格的框架。如果您在实施此方法时遇到问题，则说明您没有实施正确的DevSecOps模型。
> 译者（Bob）注：这里所说的团队之间无需协调的原则是理想化的，Bob完全同意这个观点。因此在进行团队设计的时候，首要考虑的因素是降低团队之间的耦合度。

4. Take what is best from any framework and make it work for your team! Certifications aren’t always the answer!
从框架中获取最好的部分并应用于你的团队！认证并不总是答案！

5. Fundamentally, the main “goal” of Software development is NOT to be « SAFE », it is to INNOVATE and CREATE. You do not create by not taking risks… it is quite the opposite: 
从根本上讲，软件开发的主要“目标”**不是“安全”**，而是**创新和创造**。您不能通过不冒险来创造……这恰恰相反：

	a. « Continuous Learning: Fail Fast but don’t Fail twice for the same reason! » - Small incremental changes which mitigate risks and create safe conditions to implement rapid changes.
«持续学习：快速失败，但不要犯同样的错误！» - 较小的增量更改，这些更改可以降低风险并为实施快速变更创造安全的条件。

6. SAFe isn’t used by any successful software commercial organization (Facebook, Google, Netflix, etc.).
成功的商业软件公司没有采用SAFe（Facebook, Google, Netflix,等等）。

7. Bloated overhead functions (Waterfall-like)
臃肿的开销部门（就像瀑布模式一样）

8. Looking to coordinate your Product Owners’ work? Multiple models exist such as Scrum of Scrum etc. This shouldn’t impact the developers.
想要和产品负责人进行工作协调？ 存在多种模型，例如Scrum of Scrum等。这不会影响开发人员。
> 译者（Bob）注：我并不推荐Scrum of Scrum，理由可以[参见LeSS中的描述](https://less.works/less/framework/daily-scrum.html)

[下载原文PPT](https://t.zsxq.com/r7QzjEI)

## 关于作者
**BoB Jiang**

- 中国北方的第一位CST（Certified Scrum Trainer）  
- [敏捷变革中心](https://www.c4at.cn/)（Center for Agile Transformation）合伙人  
- [Bob的博客](http://www.bobjiang.com)、《Scrum精髓》译者

## 版权声明

本文采用 [CC BY-NC-SA 3.0 许可协议](https://creativecommons.org/licenses/by-nc-sa/3.0/deed.zh)。  
转载请注明出处！
