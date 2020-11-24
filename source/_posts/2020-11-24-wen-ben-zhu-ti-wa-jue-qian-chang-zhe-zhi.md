---
layout: post
title: "文本主题挖掘浅尝辄止"
date: 2020-11-24 17:32:37 +0800
comments: true
categories: Data&ML&AI
---
## 前言:

LDA模型还是有点复杂了，目前完全没有掌握，处于调包侠的阶段.

## 代码:

```python
import re
import sys
import jieba

user_dict_file = "my_dict_watch_77.csv"
jieba.load_userdict(user_dict_file)

stop_words_file = "hit_stopwords.txt"
stopwords = open(stop_words_file, 'r', encoding = 'utf8').readlines()
stopwords = [w.strip() for w in stopwords]

file_to_process = "watch_77.csv"

def word_cut(input_file):
    result_arr = []

    with open(file_to_process, 'r') as f:
    for line in f.readlines():
        line = line.strip()
        if len(line) < 3:
            continue

        out_str = ""
        re_chinese = re.compile(u"[\u4e00-\u9fa5]+")
        w = re.sub(r'[A-Za-z0-9]|\d+', '', str(line)) # removed chars, but what about "app"? 
        seg_list = jieba.lcut(w, cut_all=False)

        for word in seg_list:
            if word not in stopwords and word != '\t' and re_chinese.search(word, 0) and len(word.strip()) >= 2:
                out_str += word
                out_str += " "

        result_arr.append(out_str.strip().split(" "))
    return result_arr

seg_out_file = "out_file_20201124.txt"
result_arr = word_cut(file_to_process)

with open(seg_out_file, 'w',encoding = 'utf-8') as file:
        file.write(str(result_arr))

from jieba import analyse
tfidf = analyse.extract_tags

with open(seg_out_file, 'r', encoding='utf-8') as file:
    texts = file.readlines()
    
keywords = jieba.analyse.extract_tags(str(texts),
                                      topK=150,
                                      withWeight=True,
                                      allowPOS=('nr', 'ns', 'nt', 'nz', 'n', 'vn', 'v'))
for item in keywords:
    print(item)


from gensim import corpora, models, similarities
from gensim.models import LdaModel
from gensim.corpora import Dictionary
import pyLDAvis
import pyLDAvis.gensim

dictionary = corpora.Dictionary(result_arr)
corpus = [dictionary.doc2bow(text) for text in result_arr]

lda = LdaModel(corpus=corpus, id2word=dictionary, num_topics=10)
lda.print_topics(2)

vis_data = pyLDAvis.gensim.prepare(lda, corpus, dictionary)
pyLDAvis.display(vis_data)
```

## 参考:
- [LDA wiki](https://en.wikipedia.org/wiki/Latent_Dirichlet_allocation)
- [文本挖掘之LDA主题模型](https://juejin.cn/post/6844904094771970056)
- [LDA sk-learn](https://scikit-learn.org/dev/auto_examples/applications/plot_topics_extraction_with_nmf_lda.html#sphx-glr-auto-examples-applications-plot-topics-extraction-with-nmf-lda-py)
- [LDA Scala](https://github.com/Nitro/scalda)
- [MiNLP-Tokenizer](https://github.com/XiaoMi/MiNLP/tree/main/minlp-tokenizer)
- [文本主题模型之LDA(一) LDA基础： 刘建平](https://www.cnblogs.com/pinard/p/6831308.html)
- [文本主题模型之LDA](https://zhuanlan.zhihu.com/p/263065290)
- [snownlp](https://github.com/isnowfy/snownlp)
- [文本主题抽取：用gensim训练LDA模型](https://www.cnblogs.com/Luv-GEM/p/10881838.html)
- [jieba](https://github.com/fxsjy/jieba)
- [pkuseg-python](https://github.com/lancopku/pkuseg-python)
- [中文分词处理](https://github.com/kimmy-sil/Python-beginning-practice)
- [Doc2Bow简介与实践Demo](https://blog.csdn.net/qq_16633405/article/details/80578804)
- [Beginners Guide to Topic Modeling in Python](https://www.analyticsvidhya.com/blog/2016/08/beginners-guide-to-topic-modeling-in-python/)
- [主题模型 LDA 入门（附 Python 代码）](https://blog.csdn.net/selinda001/article/details/80446766)
- [中文常用停用词表](https://github.com/goto456/stopwords)
- [Topic Modeling and Latent Dirichlet Allocation (LDA) in Python](https://towardsdatascience.com/topic-modeling-and-latent-dirichlet-allocation-in-python-9bf156893c24)
- [用docsim/doc2vec/LSH比较两个文档之间的相似度](https://blog.csdn.net/vs412237401/article/details/52238248)
- [wordcloud](https://github.com/amueller/word_cloud)
- [pyLDAvis](https://github.com/bmabey/pyLDAvis)
