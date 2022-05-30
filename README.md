# KPE-PTransE
**Package**

```markdown
numpy、time、math、copy、random、codecs、matplotlib.pyplot、sys 
```

**Data**

```markdown
Dataset files:

train.txt: training file, format (e1, e2, rel).

valid.txt: validation file, same format as train.txt

test.txt: test file, same format as train.txt.

entity2id.txt: all entities and corresponding ids, one per line.

relation2id.txt: all relations and corresponding ids, one per line.

e1_e2.txt: all top-500 entity pairs mentioned in the task entity prediction.

n-n.txt: can obtained by runing create_n2n.py, which used to count the types of relations. This method is from Lin Yankai, Liu Zhiyuan, Luan Huan-Bo, et al. Modeling relation paths for representation learning of knowledge bases[C]//Proceedings of the 2015 Conference on Empirical Methods in Natural Language Processing. Stroudsburg: ACL, 2015: 705-714.
```

**Experimental Settings**

```markdown
--file_path：the path of dataset
--margin: the margin between postive triples and negative triples, the recommended value is 1
--embedding_dim: the embedding dimension of entities and relations, the recommended value is 100
--learning_rate: learning rate, the recommended value is 0.005
--k: the numbers of neighbors of each relation, the recommended value is 2
--alpha1: the weight of entity similarity, the recommended value is 0.3
--alpha2: the weight of relation similarity, the recommended value is 0.7
--epochs: the iteration times, the recommended value is 1000
--nbatchs: the batch size, the recommended value is 100
--alpha: the threshold to select path, the recommended value is 0.02
```



**Training**

```markdown
For training, You need follow the step below:
1. Data preprocessing: 
PCRA2.py: extract the path of length 2, and calculate the confidence of corresponding path 
PCRA3.py: extract the path of length 3, and calculate the confidence of corresponding path 
create_n2n.py: create n-n.txt
TransE.py: pretrain the entities and relations, and put the result in the dictory ../KG_embedding
KNN.py: obtain the neighbors of each relations by calculate the similarity between the pre-trained vectors, and save it in ../data/FB15K/relation_neighbor.txt
Path_emerging.py: combine and save the paths, according to the obtained neighbors and confidence
2. call KPE_PTransE_Train3.py: in the corresponding directory. ./PathLength3


For testing, You need follow the step below:
call KPE_PTransE_Test3.py: in the corresponding directory. ./PathLength3
It will evaluate on test.txt and report mean rank and Hits@1, the format is tier: head_mean_rank(Raw) head_hit@1(Raw), head_mean_rank(Filter) head_hit@1(Filter), tail_mean_rank(Raw) tail_hit@1(Raw), tail_mean_rank(Filter) tail_hit@1(Filter) relation_mean_rank(Raw) relation_hit@1(Raw), relation_mean_rank(Filter) relation_hit@1(Filter)
```

