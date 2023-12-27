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

[![License: CC BY-NC-ND 4.0](https://img.shields.io/badge/License-CC\_BY--NC--ND\_4.0-lightgrey.svg)](https://creativecommons.org/licenses/by-nc-nd/4.0/) [![Status](https://img.shields.io/badge/Github-Ready-lightgrey.svg?logo=github)](https://github.com/HouJP/the-algorithmic-foundations-of-differential-privacy)

我们假设存在一个可信赖的**管理者** (curator)，他持有数据库 $$D$$ 中的**个人**数据。该数据库通常由 $$n$$ 行数据组成，且每一行对应一个用户。通俗地讲，隐私的目标是在保护每一行数据的同时允许对整个数据库进行统计分析。

在**非交互式**或**离线**模型中，管理者会一次性生成某种对象，比如，“合成数据库 (synthetic database)”，汇总的统计数据集合，或者“无害化数据库 (sanitized database)”。在此次**发布**后，管理者不再扮演任何角色，原始数据可能会被销毁。

一个**查询**指的是一个应用于数据库的函数。**交互式**或**在线**模型允许数据分析人员自适应地提出查询，即根据先前查询的响应决定接下来的查询。

可信的管理者可以被用户执行的协议替代，它采用安全多方协议 (secure multiparty protocols) 的加密技术，但大多数情况下我们不会诉诸于加密假设。第12章介绍了这种模型，还探讨了有关文献中的其他相关模型。

在事先知道所有查询时，非交互式模型的准确性应该是最好的，因为它能够在了解查询结构的情况下关联噪音。相反，当事先不知道有关查询的任何信息时，非交互式查询面临着严峻的挑战，因为它必须为所有可能的查询提供答案。正如我们将看到的，为了保护隐私，甚至为了防止隐私灾难，准确性必然会随着提出的查询的数量而降低，提供所有可能查询的准确答案将是不可行的。

一种**隐私机制**（简称一种**机制**）是一个算法，它以一个数据库、数据类型的全集 $$\mathcal{X}$$ (所有可能的数据库行的集合)、随机位以及（可选的）一组查询作为输入，并产生一个字符串作为输出。如果输入中存在查询，那么希望可以从输出的字符串中解码出相对准确的查询答案。如果输入中不存在查询，则属于非交互式类型，目标是得到可解释的输出字符串，为后续查询提供答案。

在某些情况下，我们可能要求输出字符串是一个**合成数据库**。这是一个从所有可能的数据行的全集 $$\mathcal{X}$$ 中抽取的多重集 (multiset)。这种情况下的解码方法是在合成数据库上执行查询，然后进行某种简单的转换，例如乘以一个比例因子，来获得真实查询结果的近似值。