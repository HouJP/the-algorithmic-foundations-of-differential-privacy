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

# 2.3 形式化差分隐私

[![License: CC BY-NC-ND 4.0](https://img.shields.io/badge/License-CC\_BY--NC--ND\_4.0-lightgrey.svg)](https://creativecommons.org/licenses/by-nc-nd/4.0/) [![Status](https://img.shields.io/badge/Github-Editing-yellow.svg?logo=github)](https://github.com/HouJP/the-algorithmic-foundations-of-differential-privacy)

我们将从差分隐私的专业定义开始，然后对其进行解读。差分隐私通过特定的**过程** (process) 来提供隐私保护，特别是会引入随机性。通过随机过程保护隐私的一个早期例子是**随机响应** (randomized response)，这是社会科学中为收集不当或不法行为的统计信息而开发的一项技术，不当或不法行为通过是否具备属性 $$P$$ 来判定。参与研究的受访者被要求根据以下步骤报告自己是否具备属性 $$P$$：

1. 抛掷一枚硬币。
2. 如果是**反面**，则如实回答。
3. 如果是**正面**，则抛掷第二枚硬币，如果是正面则回答“是”，如果是反面则回答“否”。

该技术对“隐私”的保护来自于受访者存在合理否认任何结果的可能性；特别是，如果具备属性 $$P$$ 意味着参与了非法行为，即使回答“是”也无法证明受访者有罪，因为无论受访者是否具备属性 $$P$$，他们回答“是”的概率至少有 $$1/4$$。准确性 (accuracy) 来自于对噪音生成过程（随机引入伪造的答案“是”和“否”）的理解：回答 “是” 的人数的期望等于不具备属性 $$P$$ 的人数的 $$1/4$$ 加上具备属性 $$P$$ 的人数的 $$3/4$$。因此，如果 $$p$$ 表示具备属性 $$P$$ 的受访者的真实比例，则回答 “是” 的预期人数为 $$(1/4)(1 − p) + (3/4)p = (1/4) + p/2$$。这样，我们可以估计 $$p$$ 的值为回答 “是” 的人数的两倍再减去 $$1/2$$，即 $$2((1/4) + p/2) − 1/2$$。