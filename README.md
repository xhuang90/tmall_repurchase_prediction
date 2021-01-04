[TOC]



赛题链接：[天猫复购预测之挑战Baseline](https://tianchi.aliyun.com/competition/entrance/231576/introduction)

# 赛题背景

商家有时会在特定日期，例如Boxing-day，黑色星期五或是双十一（11月11日）开展大型促销活动或者发放优惠券以吸引消费者，然而很多被吸引来的买家都是一次性消费者，这些促销活动可能对销售业绩的增长并没有长远帮助，因此为解决这个问题，商家需要识别出哪类消费者可以转化为重复购买者。通过对这些潜在的忠诚客户进行定位，商家可以大大降低促销成本，提高投资回报率（Return on Investment, ROI）。众所周知的是，在线投放广告时精准定位客户是件比较难的事情，尤其是针对新消费者的定位。不过，利用天猫长期积累的用户行为日志，

我们或许可以解决这个问题。我们提供了一些商家信息，以及在“双十一”期间购买了对应产品的新消费者信息。你的任务是预测给定的商家中，哪些新消费者在未来会成为忠实客户，即需要预测这些新消费者在6个月内再次购买的概率。



# 数据描述

数据集包含了匿名用户在 "双十一 "前6个月和"双十一 "当天的购物记录，标签为是否是重复购买者。出于隐私保护，数据采样存在部分偏差，该数据集的统计结果会与天猫的实际情况有一定的偏差，但不影响解决方案的适用性。训练集和测试集数据见文件data_format2.zip，数据详情见下表。

|   字段名称   |   描述   |
| ---- | ---- |
|   user_id   |   购物者的唯一ID编码   |
|   age_range   |  用户年龄范围。<18岁为1；[18,24]为2； [25,29]为3； [30,34]为4；[35,39]为5；[40,49]为6； > = 50时为7和8; 0和NULL表示未知    |
|   gender   |   用户性别。0表示女性，1表示男性，2和NULL表示未知   |
|   merchant_id   |   商家的唯一ID编码   |
|   label   |   取值集合为{0, 1, -1, NULL}。取1表示'user_id'是'merchant_id'的重复买家，取0则反之。取-1表示'user_id'不是给定商家的新客户，因此不在我们预测范围内，但这些记录可能会提供额外信息。测试集这一部分需要预测，因此为NULL。   |
|   activity_log   |   {user_id, merchant_id}之间的每组交易中都记录有item_id, category_id, brand_id, time，用#分隔。记录不按任何特定顺序排序。   |



以"prediction.csv"作为文件名提交，提交格式如下：

|   字段名称   |   描述   |
| ---- | ---- |
|   user_id  | 购物者的唯一ID编码 |
| merchant_id |  商家的唯一ID编码prob给定客户是给定商家的重复购买者的概率，取值在[0, 1] |



## 其他格式数据

我们还以另一种格式提供了相同数据集，可能更方便做特征工程，详情见data_format1.zip文件夹（内含4个文件），数据描述如下。

## 用户行为日志


|   字段名称   |   描述   |
| ---- | ---- |
|   user_id  | 购物者的唯一ID编码 |
| item_id |  商品的唯一编码 |
| cat_id |  商品所属品类的唯一编码 |
| merchant_id |  商家的唯一ID编码 |
| brand_id |  商品品牌的唯一编码 |
| time_tamp |  购买时间（格式：mmdd） |
| action_type |  包含{0, 1, 2, 3}，0表示单击，1表示添加到购物车，2表示购买，3表示添加到收藏夹 |


## 用户画像
|   字段名称   |   描述   |
| ---- | ---- |
|   user_id  | 购物者的唯一ID编码 |
| age_range |  用户年龄范围。<18岁为1；[18,24]为2； [25,29]为3； [30,34]为4；[35,39]为5；[40,49]为6； > = 50时为7和8; 0和NULL表示未知 |
| gender |  用户性别。0表示女性，1表示男性，2和NULL表示未知 |


## 训练数据和测试数据
|   字段名称   |   描述   |
| ---- | ---- |
|   user_id  | 购物者的唯一ID编码 |
| merchant_id |  商家的唯一ID编码 |
| label |  包含{0, 1}，1表示重复买家，0表示非重复买家。测试集这一部分需要预测，因此为空。  |