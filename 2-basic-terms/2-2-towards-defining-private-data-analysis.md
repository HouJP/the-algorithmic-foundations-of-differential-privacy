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

# 2.2 迈向隐私数据分析的定义

[![License: CC BY-NC-ND 4.0](https://img.shields.io/badge/License-CC\_BY--NC--ND\_4.0-lightgrey.svg)](https://creativecommons.org/licenses/by-nc-nd/4.0/) [![Status](https://img.shields.io/badge/Github-Editing-yellow.svg?logo=github)](https://github.com/HouJP/the-algorithmic-foundations-of-differential-privacy)

在数据分析的背景下，定义隐私的一种自然的方法是要求分析人员在完成数据分析后，对数据集中任何人的了解与之前相比没有增加。通过要求攻击者对个人的先验观点和后验观点（即访问数据库前后的看法）不应“差异太大”，或者通过要求对数据库的访问不应“过多”地改变攻击者对个人的看法，也可以很自然地形式化这个目标。然而，只要我们可以通过数据库学习到任何内容，这种隐私概念就是不切实际的。打个比方，假设攻击者有一个（错误的）先验观点是每个人都有两只左脚。通过访问统计数据库后发现，几乎每个人都有一只左脚和一只右脚。现在，攻击者对于任何特定的受访者是否有两只左脚的观点已经被彻底改变了。