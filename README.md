# Apriori

> Apriori算法是一种挖掘关联规则的频繁项集算法，其核心思想是通过候选集生成和情节的向下封闭检测两个阶段来挖掘频繁项集。

## 挖掘步骤：

1. 依据支持度找出所有频繁项集（频度）
2. 依据置信度产生关联规则（强度）

## 基本概念

1. 对于A->B
  * 支持度：P(A ∩ B)，既有A又有B的概率
  * 置信度：P(B|A)，在A发生的事件中同时发生B的概率 p(AB) / P(A)，例如购物篮分析：牛奶 ⇒ 面包
  * 例子：[支持度：3%，置信度：40%]，支持度3%：意味着3%顾客同时购买牛奶和面包；置信度40%：意味着购买牛奶的顾客40%也购买面包
2. 如果事件A中包含k个元素，那么称这个事件A为k项集事件A满足最小支持度阈值的事件称为频繁k项集。
3. 同时满足最小支持度阈值和最小置信度阈值的规则称为强规则

## 实现步骤
1. Apriori算法是一种最有影响的挖掘布尔关联规则频繁项集的算法Apriori使用一种称作逐层搜索的迭代方法，“K-1项集”用于搜索“K项集”。
首先，找出频繁“1项集”的集合，该集合记作L1。L1用于找频繁“2项集”的集合L2，而L2用于找L3。如此下去，直到不能找到“K项集”。
找每个Lk都需要一次数据库扫描。核心思想是：连接步和剪枝步。连接步是自连接，原则是保证前k-2项相同，并按照字典顺序连接。剪枝步，是使任一频繁项集的所有非空子集也必须是频繁的。
反之，如果某个候选的非空子集不是频繁的，那么该候选肯定不是频繁的，从而可以将其从CK中删除。
简单的讲，1、发现频繁项集，过程为（1）扫描（2）计数（3）比较（4）产生频繁项集（5）连接、剪枝，产生候选项集，重复步骤（1）~（5）直到不能发现更大的频集
2、产生关联规则，过程为:根据前面提到的置信度的定义，关联规则的产生如下：
  * 对于每个频繁项集L，产生L的所有非空子集；
  * 对于L的每个非空子集S，如果P（L）/P（S）>= min_conf，则输出规则“S -> L-S”，注：L-S表示在项集L中除去S子集的项集

## 备注
* 个人平日有点微懒，Apriori算法说明也是后来补充的，具体转载自[Apriori算法详解之一](http://blog.csdn.net/lizhengnanhua/article/details/9061755)
* 借由智能信息处理课程的需求，个人基于Java实现的Apriori算法，具有一定的通用性，代码中有相应的注释
* data.txt为apriori算法测试的用例，格式说明：*“T100,I1,I2,I5”*，T100表示购买记录编号，I1, I2, I5表示具体商品
