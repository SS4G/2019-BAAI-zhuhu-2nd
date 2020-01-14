# 2019-BAAI-zhuhu-2nd

队名：Conquer

2019-智源-看山杯-专家发现算法大赛-第二名-代码，文档，ppt

# 1.1概述

知乎是中文互联网知名的综合性社区平台。知乎自 2011 年创办至今，已经成为一个拥有 2.2 亿用户，每天有数以十万计的新问题以及 UGC 内容产生的网站。其中，如何高效的将这些用户新提出的问题邀请其他用户进行解答，以及挖掘用户有能力且感兴趣的问题进行邀请下发，优化邀请回答的准确率，提高问题解答率以及回答生产数，成为知乎最重要的课题之一。

# 1.2数据集介绍

本赛题以知乎app“邀请问题-是否受邀回答”为模式，收集采样app真实数据，并对中文、时间等进行脱敏构成赛题数据。其中：

1、训练集（以下简称train）包括用户近一个月的收到的问题邀请共约948W，其中包括：用户ID，问题ID，用户收到邀请的时间，用户是否回答。

2、测试集(以下简称test)分为AB榜，均为训练集后7天的邀请数据。AB榜数据均为110W左右，其中包括用户ID，问题ID，用户收到邀请的时间，任务为预测用户是否回答。

3、问题信息(以下简称question_info)的每一行给出了每个问题ID所对应的问题创建时间，问题标题字编码、词编码，问题描述内容的字编码、词编码以及问题话题的编码。

4、回答信息(以下简称answer_info)给出了用户近两个月来的回答信息，共约450W条左右，每行为某用户ID以及其回答的问题的ID，回答时间，回答内容的词编码、字编码，以及截止到采样时间该回答是否被标优、回答是否被推荐、回答是否被收入圆桌、是否包含图片、是否包含视频、回答字数、点赞数、取赞数、评论数、收藏数、感谢数、举报数、没有帮助数、反对数。

5、用户信息表(以下简称member_info)给出了涉及到训练集、测试集中所有用户的基本信息（均为脱敏数据），包括用户的性别、创作关键词编码、创作数量等级、创作热度等级、注册类型、注册平台、访问频率以及5个脱敏用户二分类特征、5个脱敏用户多分类特征，用户盐值（知乎app积分）分数，用户关注话题，用户感兴趣的话题以及对该话题喜好程度分数。

6、Embedding主题Embedding(使用Doc2vec训练)，字、词Embedding(使用Word2vec训练)，Embedding均为64维

# 1.3评价指标:AUC

# 1.4难点分析：

1)提供的是用户历史2个月的回答数据，以及历史一个月的邀请回答情况，预测目标为在邀请之后的7天内是否会回答。涉及时间相关性，在提取特征时需要特别小心，极其容易发生泄露。

2)数据量大

3)文本信息脱敏

# 1.5思路简介：

根据这些特征，构建训练集，预测测试集用户收到邀请是否会回答。显然，问题的切入点在于受邀请的用户是否对该问题感兴趣并且了解该问题并可以给出回答。所以针对这种题目，我们首先想到的便是对用户侧和问题侧分别建模，计算其相似度从而确定该用户是否回答。但是实际赛题并没有这么简单，具体请见特征工程篇。

# Fah_code:（0.890）

1.feature开头的文件为特征工程文件

2.creat_last_answerlist创建nn输入文件

3.creat_word2vec_dict将官方词向量转为字典

4.esim_preprocess，lstur_preprocess为nn预处理文件

5.lgb为最终树模型

6.nn_LSTUR，multi_esim最终nn代码

7.Fah部分 staking融合文件

# chizhu_code:（0.860）

知乎-final-chizhu为最终chizhu的所有代码 
