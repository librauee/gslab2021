# 运行环境

* Windows
* Python3.7
* 其他库参照requirements.txt

# 运行方法

1. 运行get_dataset1.ipynb以及get_dataset2.ipynb文件批次读入数据；
2. 运行feature1_100.ipynb、feature1_200.ipynb、feature1_300.ipynb、feature1_400.ipynb、feature2_100.ipynb、feature2_200.ipynb、feature2_300.ipynb、feature2_400.ipynb、feature_test.ipynb、add_rolling_feature.ipynb文件分批次提取训练集与测试集特征；
3. 运行train1.ipynb进行一阶段模型训练与预测；
5. 运行train2.ipynb进行二阶段模型训练与预测；

# 建模方法

* 因为存在标签不纯的困难问题，我采用两阶段的训练模式，第一阶段选取所有出现在黑白名单中的用户, 每个uin使用所有的击杀数据为基础建模（每600条为一个样本），此阶段使用auc作为评价指标，旨在尽可能地划分黑白样本；
* 第二阶段选取每个黑名单用户的击杀样本oof概率最大的一次击杀样本以及每个白名单用户的概率最小的一次击杀样本形成每个用户作为一个样本的训练数据，此阶段使用binary error作为评价指标，旨在得到更高的f1分数；
* 本方案特征的提取包括对每个样本数据做统计，diff后进行统计，包括max、min、mean、std等等，采用Word2Vec的思想对序列进行建模，还使用rolling的方法对type标识前后的数据做滑窗统计等等；
* 因为样本数量巨大，采用分块读入的方法，分列进行分组等聚合统计；
* 受限于机器与时间，所做的特征工程相对较为简略，高阶差分统计等特征未能够加入模型之中。