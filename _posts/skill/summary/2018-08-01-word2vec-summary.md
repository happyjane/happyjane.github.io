---
---
layout: post
title: "word2vec"
date: 2018-8-01 11:00:00 +0800 
categories: 酱油人生
tag: Word2Vec
---
* content
{:toc}


## 学习资料汇总：
	1.一片对Word2vec解读较好的[知乎文章](https://zhuanlan.zhihu.com/p/26306795)：

	2. [BN](https://www.zhihu.com/question/283715823)
		[Batch Normalization详解](https://blog.csdn.net/qq_34484472/article/details/77982224?locationNum=2&fps=1)
		BN层的作用机制也许是通过平滑隐藏层输入的分布，帮助随机梯度下降的进行，缓解随机梯度下降权重更新对后续层的负面影响。因此，实际上，无论是放非线性激活之前，还是之后，也许都能发挥这个作用。只不过，取决于具体激活函数的不同，效果也许有一点差别（比如，对sigmoid和tanh而言，放非线性激活之前，也许顺便还能缓解sigmoid/tanh的梯度衰减问题，而对ReLU而言，这个平滑作用经ReLU“扭曲”之后也许有所衰弱）

		作者：论智
		链接：https://www.zhihu.com/question/283715823/answer/438882036
		来源：知乎
		著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

		[实践](https://blog.csdn.net/whitesilence/article/details/75667002)
	3. [语言模型概括](https://blog.csdn.net/Losteng/article/details/51912043)