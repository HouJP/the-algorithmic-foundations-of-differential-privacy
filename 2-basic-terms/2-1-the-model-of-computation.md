---
layout:
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# 2.1 计算模型

[![License: CC BY-NC-ND 4.0](https://img.shields.io/badge/License-CC\_BY--NC--ND\_4.0-lightgrey.svg)](https://creativecommons.org/licenses/by-nc-nd/4.0/) [![Status](https://img.shields.io/badge/Github-Editing-yellow.svg?logo=github)](https://github.com/HouJP/the-algorithmic-foundations-of-differential-privacy)

我们假设存在一个可信赖的**管理者** (curator)，他持有数据库 $$D$$ 中的**个人**数据。该数据库通常由 $$n$$ 行数据组成，且每一行对应一个用户。通俗地讲，隐私的目标是在保护每一行数据的同时允许对整个数据库进行统计分析。

在**非交互式**或**离线**模型中，管理者会一次性生成某种对象，比如，“合成数据库 (synthetic database)”，汇总的统计数据集合，或者“无害化数据库 (sanitized database)”。在此次**发布**后，管理者不再扮演任何角色，原始数据可能会被销毁。

一个**查询**指的是一个应用于数据库的函数。**交互式**或**在线**模型允许数据分析人员自适应地提出查询，即根据先前查询的响应决定接下来的查询。
