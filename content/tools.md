---
title: "推荐工具"
date: 2020-02-16T11:23:03+08:00
type: "page"
description: "高效能技术团队工具参考"
---

工欲善其事必先利其器，每个高效能团队的背后都离不开一组精心选择的工具。本页将列出我们一直以来使用的工具集合，同时它也体现了 DTeam 工具选择的哲学：

- 开发效率至上
- 用工具来强化工程规范和约束
- 低门槛
- 重视工具的生态
- 开发性价比优先

同时，随着技术发展和业务拓展，我们也会及时调整这个页面，以反映最新的变化。

## 我们用到的工具

开发语言：

- [Java](https://www.java.com/zh_CN/)
  - 理由：jvm 拥有目前最完善的后端开发生态，并且开发人力资源丰富。
- [Groovy](http://www.groovy-lang.org/)
  - 理由：高生产力、90+% 的 Java 语法兼容、Java 无缝集成、@CompileStatic 可以带来近似 Java 的性能。
- [TypeScript](https://www.typescriptlang.org/)
  - 理由：静态类型，可直接利用 js 当前的生态。
- [Solidity](https://solidity.readthedocs.io/)
  - 理由：最成熟的以太坊智能合约开发语言。
- [Python](https://www.python.org/)
  - 理由：机器学习必选。
- [MarkDown](https://www.markdownguide.org/)
  - 理由：技术写作首选。

开发工具：

- IDE
  - [IntelliJ IDEA CE](https://www.jetbrains.com/idea/)
    - 理由：jvm ide 最佳、android studio 的基础（一致体验，降低学习成本）
  - [VSCode](https://code.visualstudio.com/)
    - 理由：前端 + Python 开发必选、插件丰富
- 框架
  - [Grails](https://grails.org/)
    - 理由：低门槛、高生产力、可无缝融入 Spring 生态、完善的工程支持（测试、Db Migration、Asset Pipeline ）
  - [Angular](https://angular.io/)
    - 理由：大型前端工程案例（Google）、一站式前端工程、开发成本（熟悉 Angular 的前端开发可以快速上手 Ionic ）。
  - [Ionic](https://ionicframework.com/)
    - 理由：开发成本（ ios、android、pwa ）、Angular 集成。
  - [Truffle](https://www.trufflesuite.com/)
    - 理由：以太坊开发首选、完善的工程支持（测试、集成、部署）、生态完善。
  - [TensorFlow](https://www.tensorflow.org/)
    - 理由：完善的工程生态、TF 2.0 门槛大幅降低（兼容 [keras](https://keras.io/) 使用）
- 工具类库
  - [Vert.x](https://vertx.io/)
    - 理由：高性能（异步、反应式）、简单（基本避免直接与线程打交道）
  - [Spring Security](https://spring.io/projects/spring-security)
    - 理由：Spring 生态最完善的权限库、grails 集成
  - [Spring Cloud](https://spring.io/projects/spring-cloud)
    - 理由：Spring 生态下微服务首选、grails 集成
  - [Ethers.js](https://docs.ethers.io/ethers.js/html/)
    - 理由：钱包开发友好、更好的 web3.js
  - [Web3J](https://www.web3labs.com/web3j)
    - 理由：Java 以太坊交互客户端、完善的智能合约工程支持、支持简单的合约审计
  - [Ganache-CLI](https://www.trufflesuite.com/ganache)
    - 理由：私有以太坊测试链
  - [Apache Ignite](https://ignite.apache.org/)
    - 理由：高性能内存网格、支持 jdbc、redis 替代
- 开发基础
  - [Gradle](https://gradle.org/)
    - 理由：Groovy DSL、Android Studio 支持、插件丰富
  - [GitLab](https://gitlab.com/)
    - 理由：类 github 体验、轻量化持续集成（gitlab-ci）
  - [Vagrant](https://www.vagrantup.com/)
    - 理由：虚拟机自动化，消除环境问题
  - [Docker](https://www.docker.com/)
    - 理由：容器首选
  - [Kubernetes](https://kubernetes.io/)
    - 理由：容器协调首选
  - [TestContainer](https://www.testcontainers.org/)
    - 理由：可丢弃的测试环境
  - [Spock](http://spockframework.org/)
    - 理由：Groovy DSL、jvm 下最好用的测试框架
  - [Geb](https://gebish.org/)
    - 理由：Groovy DSL、Spock 集成、易用高效
  - [LiquidBase](https://www.liquibase.org/)
    - 理由：最成熟的 DB Migration 工具、grails 集成
- 消息队列
  - [Kafka](https://kafka.apache.org/)
    - 理由：高性能、良好的生态
- 数据库
  - [PostgreSQL](https://www.postgresql.org/)
    - 理由：完善的 SQL 支持、高稳定性、插件丰富（特别推荐：[TimescaleDB](https://www.timescale.com/)、[Citus](https://www.citusdata.com/)）
  - [HBase](https://hbase.apache.org/)
    - 理由：[Hadoop](http://hadoop.apache.org/) 生态、高效插入和存储压缩
- 基础设施
  - 阿里云
    - 理由：国内占有率第一、生态
  - [Infura](https://infura.io/)
    - 理由：成本（无需维护自己的私有以太坊节点）

技术写作：

- [Hugo](https://gohugo.io/)
  - 理由：性能高、模板丰富、JAMStack 架构
