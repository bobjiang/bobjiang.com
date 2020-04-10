---
title: "Ruby on Rails里find by和where的区别"
date: "2016-01-06"
coverImage: "ruby-on-rails.jpg"
---

昨晚和丹总在结对写代码的时候碰到一个问题，就是想要查询2个状态的会员如何写。

一开始我们是这么写的：

`registrations = Registration.find\_by\_status(1,2); registrations.each do |attendee| end`

我们本意是想要通过find by获得所有状态为1和2的会员，但rspec里面报错

> 
Failure/Error: short\_message\_batch.save NoMethodError: undefined method \`each' for #<Registration:0x007ff89ebb99c0>

这说明返回的registrations不是集合（数组）呀，查了一下原来find by只能返回符合条件的第一条记录。

看来find by不能满足要求了，那么where能否实现呢。看看如下代码

`registrations = Registration.where(status: \[1,2\]) registrations.each do |attendee| end`

看起来需要用where条件查询返回一个集合（数组）
