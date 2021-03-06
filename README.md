#Record the knowledge of the recsys

问题:

推荐系统背景

推荐基本算法介绍

推荐系统架构

ranking：pointwise,pairwise,listwise

ctr预估：LR,FM,FMM,gbdt,神经网络深度学习，wide & deep(google),DeepCross(residual network)

可解释性：

评价准则：

用户画像：session

nlp:embedding,ngram,cbow,skip-gram,word2vec


推荐系统基本任务就是联系用户和物品，解决信息过载问题，推荐系统通过挖掘用户行为，找到用户个性化需求，从而将长尾商品准确地推荐给需要它的用户，主要方法有：社会化推荐(基于人口统计学推荐)，基于内容推荐，基于协同过滤推荐以及混合推荐。协同过滤又可进一步分成基于内存的推荐(基于领域的方法)和基于模型的推荐。

协同过滤：item_CF,user_CF,LFM(隐语义模型，LSI,pLSA,LDA,Topic Model);
基于内存的推荐：基于用户的协同过滤推荐，基于物品的协同过滤推荐；
基于模型的推荐：一般用户离线计算，采用机器学习的方法，LFM；


下面是一些参考链接:

#第四范式程晓澄:机器学习如何优化系统#https://mp.weixin.qq.com/s?__biz=MzI1MjQ2OTQ3Ng==&mid=2247486257&idx=1&sn=5302911cb3f22ed56dcf7d655aadea51&chksm=e9e202bade958bacadd1800f3c465c24f7534f5499d79a276acb3c4b1a5061de0c5c2863ac03&mpshare=1&scene=1&srcid=1010FOkRazP4kH2exOpUQdsS&pass_ticket=Kgcwh2pgE0pgjJq7GHdbx3i%2B4xsh0LkxdXwx98oemfr886I3%2F8gthuYxfH6FYMq1#rd
本文介绍了推荐系统发展的历史，算法的演进，以及最新的技术的介绍，包括整个推荐系统框架的介绍（候选集的生成，排序，重排序以及生成推荐列表），十分全面的科普帖。


#1.常用推荐算法简介,http://blog.csdn.net/u014605728/article/details/51274814

本文介绍了各种推荐方法的简介和适用范围

1.1 基于人口统计学的推荐，使用用户的基本信息发现用户的相关程度，然后将相似用户喜欢的其他物品推荐给当前用户。优点在于没有冷启动问题，领域独立。缺点在于太过粗糙。

1.2 基于内容的推荐，根据推荐物品或内容的元数据，发现物品或者内容的相关性，然后基于用户以往的喜好，推荐用户相似的物品，这种推荐多用户咨询累的应用上，针对文件本身抽取一些tag作为该文章的关键字，继而可以通过这些tag来评价两篇文章的相似度。优点在于不需要用户数据因此不存在稀疏性和冷启动，基于物品本身特征推荐，不存在推荐过度热门。缺点在于抽取的特征需要保证准确性，豆瓣人工维护tag。

1.3基于关联规则的推荐，常见与电子商务系统，其实际意义为购买一些物品的用户更倾向与购买另一些物品，挖掘关联规则，目前关联规则挖掘算法主要有Apriori和FP-Growth两个算法演变而来。优点:转化率较高。缺点：计算量大，由于采用用户数据，存在冷启动和稀疏性的问题，存在热门item被过度推荐的问题。

1.4 基于协同过滤的推荐

1.4.1 基于用户的协同过滤，根据所有用户对物品或者信息的偏好，发现与当前用户口味和偏好相似的用户。优点在于推荐物品之间可能完全相关，因此可以发现用户的潜在兴趣，并针对每个用户生成其个性化推荐结果。缺点在于，一般的web系统中，用户的增长速度远远高于物品的增长速度,因此其计算量增长巨大，系统性能容易成为瓶颈，因此业界单独使用基于用户的协同过滤系统较少。

1.4.2 基于物品的协同过滤,使用所有用户对物品或者信息的偏好，发现物品与物品之间的相似度，然后根据用户的历史偏好，将类似的物品推荐给用户。基于物品的协同过滤可以看出是关联规则腿推荐的一种退化，当时协同过滤考虑更多的用户的实际评分。优点,与基于用户的协同过滤相比，基于物品协同过滤推荐更为广泛，扩展性和算法性能更好。缺点，无法提供个性化推荐的推荐结果。item_CF和user_CF，根据user数量和item数量来选择。

1.4.3 隐语义模型LFM,该算法最早在文本挖掘领域被提出，用于找到文本潜在的主题或者分类，主要算法有LSI,pLAS,LDA,隐含类别模型，隐含主题模型，MF矩阵分解。

1.4.3.1 LSA，潜在语义分析，LSA(LSI)使用SVD来对单词-文档矩阵进行分解。SVD可以看作是从单词-文档矩阵中发现不相关的索引变量(因子)，将原来的数据映射到语义空间内。在单词-文档矩阵中不相似的两个文档，可能在语义空间内比较相似。http://www.cnblogs.com/bentuwuying/p/6219970.html

1.4.3.2 pLAS(Probabilistic Latent Senmantic Analysis),对于语言学，容易想到的词包括：语法，句子，主语等；对于概率统计，容易想到的词包括：概率，模型，均值等；对于计算机，容易想到的词包括：内存，硬盘，编程等。我们之所以能想到这些词，是因为这些词在对应的主题下出现的概率很高。我们可以很自然的看到，一篇文章通常是由多个主题构成的，而每一个主题大概可以用与该主题相关的频率最高的一些词来描述。以上这种想法由Hofmann于1999年给出的pLSA模型中首先进行了明确的数学化。Hofmann认为一篇文章（Doc）可以由多个主题（Topic）混合而成，而每个Topic都是词汇上的概率分布，文章中的每个词都是由一个固定的Topic生成的。下图是英语中几个Topic的例子。

1.4.3.3,LDA(latent Dirichlet Allocation),主题模型，认为一篇问丈夫的每个词都是通过“以一定的概率选择某个主题，并从这个主题中以一定的概率选择某个词语”，http://blog.csdn.net/huagong_adu/article/details/7937616

1.4.3.4,MF，矩阵分解，


#2.实时推荐系统的三种方式#http://www.jianshu.com/p/356656ce2901 作者：出版圈郭志敏、

简介：目前的商用推荐系统，当用户数和商品数达到一定数目时，推荐算法都面临严重的可扩展性问题，推荐的实效性变得非常差，如何在算法和架构上提高推荐速度是很多公司不得不思考的问题。目前，在算法上主要通过引入聚类技术和改进实时协同过滤算法提高推荐速度；在架构上，目前实时推荐主要有基于Spark、Kiji框架和Storm的流式计算3种方法。

1. 聚类技术和实时协同过滤算法
聚类技术：EM,K-means,层次聚类,吉布斯采样，模糊聚类
2. 基于spark的方式
3. 基于Kiji架构的方式
4. 基于storm的方式

#3.介绍矩阵分解在推荐系统中的应用#http://blog.csdn.net/sun_168/article/details/20637833

简介:矩阵分解属于协同过滤中的基于模型推荐，矩阵分解目标就是把用户-项目评分矩阵R分解成用户因子矩阵和项目因子矩阵乘的形式，
即R=UV，这里R是n×m， n =6， m =7，U是n×k，V是k×m；用户i对项目j的评分r_ij =innerproduct(u_i, v_j)，更一般的情况是r_ij =f(U_i, V_j)

目标函数L:均方误差

优化方法：交叉最小二乘法(als,alternative least squares)，随机梯度下降法

迭代停止条件：
a)设置一个阈值，当L函数值小于阈值时就停止迭代，不常用
b)设置一个阈值，当前后两次函数值变化小于阈值时，停止迭代
c)设置固定迭代次数

过拟合：
当用户-项目评分矩阵R非常稀疏时，就会出现过拟合（overfitting）的问题，过拟合问题的解决方法就是正则化（regularization）。正则化其实就是在目标函数中加上用户因子向量和项目因子向量的二范数，当然也可以加上一范数。至于加上一范数还是二范数要看具体情况，一范数会使很多因子为0，从而减小模型大小，而二范数则不会它只能使因子接近于0，而不能使其为0，关于这个的介绍可参考论文Regression Shrinkage and Selection via the Lasso。

优缺点：
矩阵分解算法目前在推荐系统中应用非常广泛，对于使用RMSE作为评价指标的系统尤为明显，因为矩阵分解的目标就是使RMSE取值最小。但矩阵分解有其弱点，就是解释性差，不能很好为推荐结果做出解释。

#4.矩阵分解在协同过滤推荐算法中的应用#http://www.cnblogs.com/pinard/p/6351319.html

本文介绍了三种用于矩阵分解的算法，分别为FunkSVD,BaisSVD,SVD++,第三篇文章介绍的矩阵分解的方法实际上就是FunkSVD,矩阵分解适合小型推荐系统。

#ctr预估相关

相关术语：
CPC:cost per click,每次点击花费
CPA:cost per action,按广告投放效果收费
CVR:click value rate,转化率
CTR:click through rate,点击率
PV, page view, 访问量
....

预估CTR/CVR，业界常用的方法有人工特征工程 + LR(Logistic Regression)、GBDT(Gradient Boosting Decision Tree) + LR[1][2][3]、FM（Factorization Machine）[2][7]和FFM（Field-aware Factorization Machine）[9]模型。在这些模型中，FM和FFM近年来表现突出，分别在由Criteo和Avazu举办的CTR预测竞赛中夺得冠军[4][5]。随着深度学习的发展，使用深度学习的方法预估ctr也逐渐发展(http://www.mamicode.com/info-detail-1465813.html，wide & deep(google),DeepCross(residual network))。


#5.深入理解FFM原理与实践#http://geek.csdn.net/news/detail/59793

FM(Factorization Machine)是由Konstanz大学Steffen Rendle（现任职于Google）于2010年最早提出的，旨在解决稀疏数据下的特征组合问题。根据model-based的协同过滤中，一个rating矩阵能够分解为user矩阵和item矩阵，FM将特征组合的权重矩阵W分解W = VTV的形式，优化方式也与MF的训练相同，使用als或者是sgd。

FFM(Field-aware Factorization Machine)最初的概念来自Yu-Chin Juan（阮毓钦，毕业于中国台湾大学，现在美国Criteo(Criteo是一家在纳斯达克上市的全球性的效果营销的科技公司,于2005年在法国巴黎成立。该公司目前的核心业务是重定向广告）与其比赛队员，是他们借鉴了来自Michael Jahrer的论文中的field概念提出了FM的升级版模型。通过引入field的概念，FFM把相同性质的特征归于同一个field。github上源码地址https://github.com/guestwalk/libffm，下载,保证gcc版本大于4.2.2,make即可，会生成fft-train和fft-predict,libffm源码解析可以参考链接http://blog.csdn.net/zc02051126/article/details/54614230。

#6.用户画像#https://www.zhihu.com/question/26758348

用户画像又称用户角色，作为一种勾画目标用户、联系用户诉求与设计方向的有效工具，用户画像在各领域得到了广泛的应用。主要有两种用户画像User Persiona 和User Profile.

User Persiona:主要面向产品设计人员和运营人员，例如，在用户调研阶段，产品经理经过调查问卷、客户访谈了解用户的共性与差异，汇总成不同的虚拟用户；在产品原型设计、开发阶段，产品经理围绕这些虚拟用户的需求、场景，研究设计产品用户体验与使用流程；当产品设计出现分歧时，产品经理能够借助用户画像（User Persona）跳出离散的需求，聚焦到目标用户，不是再讨论这个功能到底要不要保留，而是讨论用户可能需要这个功能，如何使用这个功能等等。当产品用户群体扩大后，单纯靠User Persona效果便有所局限。所以就会用到User Profile.

User Profile:为了解决上述问题，同时为了更加精细化的深入理解用户，我们自然会希望通过产品积累的用户行为数据来为产品运营提供更好的支持，由此诞生了一些新的功能，例如根据用户的浏览记录向用户提供个性化行为数据。User Profile就是根据用户在产品中的行为数据，产出描述用户标签的集合。例如猜测用户的性别，生活所在地，喜欢什么明星，要买什么东西,时间，是否节假日，是否新用户，留存和召回的考虑，用户兴趣变化快慢等。

