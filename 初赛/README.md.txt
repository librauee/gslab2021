# 运行环境

* Windows
* Python3.7
* 其他库参照requirements.txt

# 运行方法

1. 运行get_dataset1.ipynb以及get_dataset2.ipynb文件；
2. 运行feature1.ipynb以及feature1.ipynb文件；
3. 最终运行train.ipynb进行模型训练与预测。

# 建模方法

* 选取所有黑名单样本，采样白名单样本，共计10000个uin, 每个uin使用所有的击杀数据为基础建模（每600条为一个样本），对每个样本数据做统计，diff后进行统计，包括max、min、mean、std等等，采用Word2Vec的思想对序列进行建模
* 因为样本数量巨大，采用分块读入的方法，分列进行分组等聚合统计