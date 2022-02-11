---
title: "缓存"
date: 2021-11-25T18:44:17+08:00
weight: 90
description: >
    DNS解析域名缓存对应公有云平台上的DNS解析域名
---

缓存记录即表示DNS解析域名本地与公有云的映射关系。

**缓存列表来源**：

- PrivateZone类型的DNS解析关联VPC后将会为对应平台产生一条缓存记录。
- PublicZone类型的DNS解析通过新建缓存功能为对应平台产生一条缓存记录。