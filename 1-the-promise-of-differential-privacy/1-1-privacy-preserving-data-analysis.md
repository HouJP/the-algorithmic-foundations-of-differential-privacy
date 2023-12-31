# 1.1 面向隐私保护的数据分析

[![License: CC BY-NC-ND 4.0](https://img.shields.io/badge/License-CC\_BY--NC--ND\_4.0-lightgrey.svg)](https://creativecommons.org/licenses/by-nc-nd/4.0/)

差分隐私是针对“如何在进行数据分析的同时保护隐私”这一问题提出的隐私定义。我们简明扼要地解决了其他方法在处理该问题时存在的一些不足。

**数据无法完全匿名并保持可用性**。一般来讲，数据越丰富，它的可用性就越高且越值得挖掘。这引出了“匿名化”和“删除个人身份信息”的概念，其目的是隐藏部分数据记录，公开其余部分并用于分析。然而，数据的丰富性使得有时候可以通过一组出人意料的字段或者属性来 “识别” 一个人，例如邮政编码、出生日期和性别的组合，甚至是三部电影的名称以及相应的大致观看日期。这种 “识别” 能力可被用于链接攻击 (linkage attack)，来将“匿名” 记录与不同数据集中的非匿名记录进行匹配。例如，有研究者通过把匿名医疗数据与公开可用的选民登记记录进行匹配，从而破解了美国马萨诸塞州州长的医疗记录。此外，网飞公司 (Netflix) 因将用户的历史观看数据匿名公开在一个电影数据集中用作推荐竞赛的训练数据，而被研究者通过链接互联网电影数据库 (IMDb) 的方式识别出该公司的订阅用户。

**“匿名”记录的再识别 (re-identification) 并非唯一的风险**。我们显然不希望看到“匿名”的数据记录被重新识别，不仅是因为再识别本身会揭示数据集中成员的身份，同时也因为记录中可能包含敏感信息，如果将其与个人相关联，有可能对个人造成损害。从特定紧急护理中心收集的指定日期的医疗记录可能只包含有限的病症或诊断记录。一条附近居民在这段时间访问该护理中心的额外信息，足以将该居民的病情状况缩小到相当狭窄的范围。虽然无法将特定记录与该居民匹配，但这对他的隐私保护作用微乎其微。

**对大型集合的查询无法充分保护隐私**。针对特定个体的查询无法提供安全且准确的回答，实际上人们可能希望直接屏蔽此类查询（如果能够识别它们）。如下面的差分攻击 (differencing attack) 所示，强制在大型集合上查询也并非灵丹妙药。假设已知X先生在某医疗数据库中，将两个针对大型数据集的查询“数据库中有多少人具有镰状细胞性状？”和“数据库中，除了X先生以外，有多少人具有镰状细胞性状？”的答案综合起来，就可以得出X先生的镰状细胞性状情况。

**查询审计 (query auditing) 存在问题**。人们可能会试图审计查询序列和响应序列，目的是在考虑历史记录的情况下，若回答当前查询会危及隐私，则禁止提供任何响应。例如，审计员会查找可能构成差分攻击的查询对。然而，这种方法存在两个困难。首先，拒绝回答查询的行为本身就可能泄漏信息。其次，查询审计在计算上也许是行不通的；实际上，如果查询语言足够丰富，甚至可能不存在用于判断一对查询是否构成差分攻击的算法程序。

**汇总统计 (summary statistics) 并不“安全”**。从某种意义上讲，汇总统计是一种失败的隐私保护解决方案，因为它无法抵御上述差分攻击。汇总统计还在存在其它问题，包括无法抵御针对数据库的各种重构攻击 (reconstruction attacks)，其中，数据库中的每个人有一个需要保护的“机密位 (secret bit)”。从实用性的角度来看，我们希望允许诸如“满足属性 \\(P\\) 的人中有多少人的机密位的值为 \\(1\\)？”的查询。而另一方面，攻击者的目标则是显著提高猜中个人机密位的机会。第8.1节描述的重构攻击表明，即使是线型数量的此类查询也难以防御：除非引入足够的误差，否则几乎所有的机密位都可以被重构出来。

发布汇总的统计数据存在风险，一个明显的例证是通过统计技术的应用可以判断一个人是否参与了某项全基因组关联研究，该技术最初的用途是在法医鉴定中确认某个人的 DNA 是否存在于生物混合物样本中。根据人类基因组计划的网站，“单核苷酸多态性，或 SNPs (发音为“snips”)，指的是当基因组序列中的一个单核苷酸 (A、T、C 或 G) 发生改变时产生的 DNA 序列变种。例如，一个 SNP 可能会将 DNA 序列 AAGGCTAA 改变为 ATGGCTAA。” 在这种情况下，我们称有两个等位基因: A 和 T。对于这样的 SNP，我们可以抛出一个问题：在特定的参考群体中，两个可能的等位基因的频率分别是多少？在已知参考群体中 SNPs 的等位基因频率的情况下，我们可以研究患有特定疾病的亚群（即“病例”组）中这些频率有何不同，从而寻找与该疾病相关的等位基因。出于这个原因，全基因组关联研究中可能包含病例组的大量 SNPs 的等位基因频率。根据定义，这些等位基因频率只是汇总后的统计数据，并且研究人员的假设是（当然，该假设是错误的），通过汇总的方式，隐私可以得到保护。然而，从理论上讲，如果拥有个人的基因组数据，就有可能确定该个体是否属于病例组（也就是，是否患有对应的疾病）。为了应对这个问题，美国国立卫生研究院和惠康基金会不再允许公众访问他们资助的全基因组关联研究的汇总频率数据。

即使对于差分隐私而言，这也是一个颇具挑战的难题，因为涉及的基因测量数量巨大（数十万甚至上百万），而任一病例组中的个体数量相对较少。

**“寻常”的事实并不“安全”**。如果数据主体被长期追踪，“寻常”的事实，例如购买面包，也可能会泄露隐私。例如，参考 T 先生，他年复一年地定期购买面包，直到突然变得很少买面包。分析师也许会得出结论，T 先生很有可能被诊断患有2型糖尿病。分析师的结论可能是正确的，也可能是错误的；无论哪种情况，T 先生的隐私都会受到损害。

**牺牲“少数人”**。在某些情况下，特定技术实际上可以为数据集中的“典型”成员，或更一般地讲，为“大多数”成员提供隐私保护。在这种情况下，人们经常听到这样的论点，即该技术足够好了，因为它只会泄露“少数几个”参与者的隐私。如果我们抛开对极端情况（被放弃的人的隐私刚好最重要）的担忧，牺牲“少数人”的理念并不完全没有价值：只需在权衡成本和收益的基础上，让社会各界达成共识。与牺牲“少数人”的理念相匹配的隐私定义尚未被提出；不过，对于单个数据集，可以通过随机选择一些数据行组成子集并公开它们来模拟“少数人”的隐私被泄漏
(第4章，引理 4.3)。随机子集中用来描述统计分析质量的采样边界 (sampling bounds) 决定了要公开的行数。当牺牲“少数人”的理念不被接受时，差分隐私成为了另外一种选择。