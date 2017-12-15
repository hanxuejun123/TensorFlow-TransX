# TensorFlow-TransX

The implementation of TransE [1], TransH [2], TransR [3], TransD [4] for knowledge representation learning (KRL). The overall framework is based on TensorFlow. We use C++ to implement some underlying operations such as data preprocessing and negative sampling. For each specific model, it is implemented by TensorFlow with Python interfaces so that there is a convenient platform to run models on GPUs. 

These codes will be gradually integrated into the new framework [[OpenKE]](https://github.com/thunlp/openke).

# Customizing Your Own Model

If you have a new idea and need to implement its code, you just need to change Python interfaces for your customized model. Read these codes, you will find that to change the class TransXModel will meet your needs.

# Evaluation Results

More results about models can be found in ("https://github.com/thunlp/KB2E").

# Data

Datasets are required in the following format, containing three files:

triple2id.txt: training file, the first line is the number of triples for training. Then the follow lines are all in the format (e1, e2, rel).

entity2id.txt: all entities and corresponding ids, one per line. The first line is the number of entities.

relation2id.txt: all relations and corresponding ids, one per line. The first line is the number of relations.

You can download FB15K and WN18 from [[Download]](https://github.com/thunlp/Fast-TransX/tree/master/data), and the more datasets can also be found in ("https://github.com/thunlp/KB2E").

# Compile

bash make.sh

# Train

To train our models based on random initialization:

1. Change class Config in OurModel.py

		class Config(object):
	
			def __init__(self):
				...
				self.testFlag = False
				self.loadFromData = False
				self.L1_flag = True	# True for L1 and False for L2
				self.hidden_sizeE = 100	    # hidden size of entity embedding space
				self.hidden_sizeR = 100	    # hidden size of relation embedding space
				self.nbatches = 100	# the number of mini-batches = totaltriples//batch_size
				self.entity = 0
				self.relation = 0
				self.trainTimes = 600     # training times
				self.margin = 1.0	# margin
				...

2. python OurModel.py

To train models based on pretrained results:

1. Change class Config in OurModel.py

		class Config(object):
	
			def __init__(self):
				...
				...
				self.testFlag = False
				self.loadFromData = True
				self.L1_flag = True	# True for L1 and False for L2
				self.hidden_sizeE = 100	    # hidden size of entity embedding space
				self.hidden_sizeR = 100	    # hidden size of relation embedding space
				self.nbatches = 100	# the number of mini-batches = totaltriples//batch_size
				self.entity = 0
				self.relation = 0
				self.trainTimes = 600     # training times
				self.margin = 1.0	# margin
				...
				...

2. python OurModel.py

# Test

To test your models:

1. Change class Config in OurModel.py
	
		class Config(object):

			def __init__(self):
				...
				...
				self.testFlag = True
				self.loadFromData = True
				self.L1_flag = True	# True for L1 and False for L2
				self.hidden_sizeE = 100	    # hidden size of entity embedding space
				self.hidden_sizeR = 100	    # hidden size of relation embedding space
				self.nbatches = 100	# the number of mini-batches = totaltriples//batch_size
				self.entity = 0
				self.relation = 0
				self.trainTimes = 600     # training times
				self.margin = 1.0	# margin
				...

2. python OurModel.py



# Citation

If you use the code, please kindly cite the papers listed in our reference.

# Reference

[1] Bordes, Antoine, et al. Translating embeddings for modeling multi-relational data. Proceedings of NIPS, 2013.

[2]	Zhen Wang, Jianwen Zhang, et al. Knowledge Graph Embedding by Translating on Hyperplanes. Proceedings of AAAI, 2014.

[3] Yankai Lin, Zhiyuan Liu, et al. Learning Entity and Relation Embeddings for Knowledge Graph Completion. Proceedings of AAAI, 2015.

[4] Guoliang Ji, Shizhu He, et al. Knowledge Graph Embedding via Dynamic Mapping Matrix. Proceedings of ACL, 2015.
