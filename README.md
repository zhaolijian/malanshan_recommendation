# malanshan_recommendation
# 一. 项目介绍
# 给定芒果tv最近30天的user(用户数据)、item(视频数据)、context(用户观看视频数据)实现ctr(点击率预估).


# 二. 特征工程

## 我们的特征工程中主要包括五组特征，下面一一介绍：

### 1.类别编码特征：

### 	这部分主要针对数据中的类别特征进行编码并统计count

### 2.embedding特征：

### 	这部分特征只要包括两大类：

### 		2.1 使用用户的watch信息对用户的观看序列与视频的被观看序列进行word2vector训练，然后对所得的词向量做均值得到did，vid的embedding向量

### 		2.2 使用item表中的stars对每一个vid进行单独的建模，将每个vid的stars序列放入word2vector中训练，然后将所得的词向量取均值作为每个vid的embedding向量

### 3. 交叉特征:

### 	推荐场景下的原始特征大多都是稀疏特征，即离散特征，本次任务提供的数据集也不例外。故从中挑选了['did','vid'],['did','cid']等特征组进行交叉统计

### 4. Group统计特征：

### 	对['vid','did','cid','region','mod','mf']统计了其对应的['vv','ctr','duration','title_length']的各种统计量，其中包括mean,std等。

### 5.目标编码:

###  	对['class_id','vid','cid']和交叉特征进行五折目标编码，计算各个特征的转化率
# 注: watch:用户观看视频数据; stars:视频中出现的明星id; vid:视频id; did:用户id; cid: 视频所属类别id; region:用户地域id; mod:手机型号id; mf:手机厂商id; vv:视频最近几日播放量
# ctr:视频转换率(点击率/曝光数), duration:视频时长; title_length: 视频标题长度


# 三. 模型介绍:

## 	我们这次采用了lightgbm作为我们的模型。lightgbm是一种能够很好地处理类别型特征的梯度提升算法库。相对于Xgboost来说在训练速度和内存上优化很多,而且在本次比赛中同样的特征线上评分也是高于Xgboost的，所以我们选择lightgbm作为我们的最终模型。

## 	线下验证时我们选取了part 26,27,28,29作为训练集，part30作为我们的线下测试集进行线下的评估，然后使用part 26,27,28,29,30一次性训练模型作为我们的线上评估模型。




​		



