---
layout:
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# 差分隐私的承诺

“差分隐私” 描述了数据持有者或管理者对数据主体的承诺：“无论是否存在其他研究、数据集或者信息源，您都不会因数据被用于任何研究或分析而受到不利影响”。理想情况下，满足差分隐私的数据库机制允许我 们对广泛的机密数据，在无需借助于数据净室 (data clean rooms)、数据使用协议、数据保护计划或受限视图的情况下，进行精准分析。尽管如此，数据的可用性最终还是会受到影响：信息恢复的基本规律(Foundamental Law of Information Recovery) 指出，对太多问题作出过于精准的回答会以惊人的方式摧毁隐私[^1]。差分隐私算法研究的目标是竭尽所能地延缓这一必然结果。



[^1]: 这个结果在“重构攻击”中被证明，它不仅适用于差分隐私，也适用于所有隐私保护相关的数据分析技术。
