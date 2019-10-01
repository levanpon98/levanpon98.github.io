---
date: 2019-10-01 00:16:10
layout: post
title: Word Embedding
description: >-
  Bài 
image: >-
  https://res.cloudinary.com/dzwwhbt1i/image/upload/c_scale,h_300,w_400/v1569863989/lstm_n5dznh.png
category: nlp
author: levanpon98
paginate: true
---

Word Embedding là một trong những phương pháp nổi bật nhất để có thể biểu diễn một từ. Nó có khả năng tóm lượt ngữ cảnh của một từ trong đoạn văn, sự tương đồng về ngữ nghĩa và cú pháp, và quan hệ giữa các từ khác...

Vậy chính xác Word Embedding là gì? Nói một cách đơn giản, chúng là những vector số (thường là số thực). Vậy làm như thế nào để một từ có thể chuyển đổi thành một vector, và quan trọng hơn, làm thế nào để vector đó có thể nắm giữ ngữ cảnh.

### Các loại Word Embedding

**Word Embedding** được phân thành 2 loại chính:
- Frequency-based embedding
- Prediction-based embedding

#### Frequency-based embedding

Phương pháp này dựa vào tần suất xuất hiện của từ để tạo ra vector từ, có 3 loại phổ biến:
- One-hot encoding (Count Vector)
- TF-IDF transforming
- Co-occurrence Matrix

Mình sẽ đi chi tiết vào từng loại

##### One-hot encoding (Count Vector)

Đây là phương thức đơn giản nhất để chuyển đổi một từ thành một vector dựa vào sự xuất hiện của từ đó trong tài liệu. Cách tiếp cận này được gọi là countvectorizing hoặc là one-hot encoding.

Ý tưởng chính của phương pháp này là thu thập một tập hợp các câu, văn bản, bài viết rồi sau đó đếm sự xuất hiện của mỗi từ trong đó. 

**Code demo**
```python
>>> from sklearn.feature_extraction.text import CountVectorizer
>>> corpus = [
...     'This is the first document.',
...     'This document is the second document.',
...     'And this is the third one.',
...     'Is this the first document?',
... ]
>>> vectorizer = CountVectorizer()
>>> X = vectorizer.fit_transform(corpus)
>>> print(vectorizer.get_feature_names())
['and', 'document', 'first', 'is', 'one', 'second', 'the', 'third', 'this']
>>> print(X.toarray())  
[[0 1 1 1 0 0 1 0 1]
 [0 2 0 1 0 1 1 0 1]
 [1 0 0 1 1 0 1 1 1]
 [0 1 1 1 0 0 1 0 1]]
```

Như ví dụ trên, chúng ta có 4 documents, và có 9 từ được tìm thấy trong 4 documents này. Tiếp theo là thực hiện việc đếm số lượng xuất hiện của từng từ trong từng document. Và cuối cùng chúng ta vector bên dưới.

##### TF-IDF transforming

Hãy lấy một ví dụ là trong một đoạn văn bản, các từ xuất hiện thường xuyên như "a", "the", 'is', ... tuy nhiên nó lại không mang nhiều thông tin. Nếu sử dụng phương pháp count vector, thì những từ này được xem như quan trọng và mang nhiều thông tin. Vì vậy chúng ta cần làm giảm mức độ quan trọng của những từ này lại bằng phương pháp TF-IDF (Term Frequency – Inverse Document Frequency).

Mình sẽ giải thích TF-IDF từng phần.

**TF là gì?**

TF: Term Frequency(Tần suất xuất hiện của từ) là số lần từ xuất hiện trong văn bản. Vì các văn bản có thể có độ dài ngắn khác nhau nên một số từ có thể xuất hiện nhiều lần trong một văn bản dài hơn là một văn bản ngắn. Như vậy, term frequency thường được chia cho độ dài văn bản( tổng số từ trong một văn bản).

$$tf(t,d) = \frac{f(t,d)} {max{f(w, d) : w \in d}}$$

Trong đó:
- $$tf(t,d):$$ tuần suất xuất hiện của từ $$t$$ trong đoạn văn $$d$$
- $$f(t,d):$$ số lần xuất hiện của từ $$t$$ trong đoạn văn $$d$$
- $$max{f(w, d) : w \in d}:$$ Số lần xuất hiện của từ có số lần xuất hiện nhiều nhất trong văn bản $$d$$

**IDF là gì?**

IDF: Inverse Document Frequency(Nghịch đảo tần suất của văn bản), giúp đánh giá tầm quan trọng của một từ . Khi tính toán TF , tất cả các từ được coi như có độ quan trọng bằng nhau. Nhưng  một số từ như “is”, “of” và “that” thường xuất hiện rất nhiều lần nhưng độ quan trọng là không cao. Như thế chúng ta cần giảm độ quan trọng của những từ này xuống.

$$idf(t, D) = log \frac{|D|} {|{d \in D : t \in d}|}$$

Trong đó:
- $$idf(t, D):$$ là giá trị idf của từ $$t$$ trong tập văn bản
- $$D:$$ Tổng số văn bản trong tập $$D$$
- $${d \in D : t \in d}: $$ Thể hiện số văn bản trong tập $$D$$ có chứa từ $$t$$

Cơ số logarit trong công thức này không thay đổi giá trị idf của từ mà chỉ thu hẹp khoảng giá trị của từ đó. Vì thay đổi cơ số sẽ dẫn đến việc giá trị của các từ thay đổi bởi một số nhất định và tỷ lệ giữa các trọng lượng với nhau sẽ không thay đổi. (nói cách khác, thay đổi cơ số sẽ không ảnh hưởng đến tỷ lệ giữa các giá trị IDF). Việc sử dụng logarit nhằm giúp giá trị tf-idf của một từ nhỏ hơn, do chúng ta có công thức tính tf-idf của một từ trong 1 văn bản là tích của tf và idf của từ đó.

Khi đó công thức tính TF-IDF như sau: 

$$tfidf(t, d, D) = tf(t, d) \times idf(t, D)$$

Những từ có giá trị TF-IDF cao là những từ xuất hiện nhiều trong văn bản này, và xuất hiện ít trong các văn bản khác. Việc này giúp lọc ra những từ phổ biến và giữ lại những từ có giá trị cao (từ khoá của văn bản đó).

**Code demo**

```python 
import math
import pandas as pd

def computeTF(wordDict, words):
    tfDict = {}
    wordsCount = len(words)
    for word, count in wordDict.items():
        tfDict[word] = count/float(wordsCount)
    return tfDict

def computeIDF(docList):
    
    idfDict = {}
    N = len(docList)
    
    idfDict = dict.fromkeys(docList[0].keys(), 0)
    for doc in docList:
        for word, val in doc.items():
            if val > 0:
                idfDict[word] += 1
    
    for word, val in idfDict.items():
        idfDict[word] = math.log10(N / float(val))
        
    return idfDict

def computeTFIDF(tfDocs, idfs):
    tfidf = {}
    for word, val in tfDocs.items():
        tfidf[word] = val*idfs[word]
    return tfidf


docA = "bây giờ mận mới hỏi đào"
docB = "vườn hồng có lối ai vào hay chưa"

wordsA = docA.split()
wordsB = docB.split()

wordSet = set(wordsA).union(set(wordsB))

wordDictA = dict.fromkeys(wordSet, 0) 
wordDictB = dict.fromkeys(wordSet, 0)

for word in wordsA:
    wordDictA[word]+=1
    
for word in wordsB:
    wordDictB[word]+=1


tfdocA = computeTF(wordDictA, wordsA)
tfdocB = computeTF(wordDictB, wordsB)

idfs = computeIDF([wordDictA, wordDictB])

tfidfDocA = computeTFIDF(tfdocA, idfs)
tfidfDocB = computeTFIDF(tfdocB, idfs)

pd.DataFrame([tfidfDocA, tfidfDocB])
```

###### Co-occurrence Matrix

Tuy nhiên, nhược điểm của cả hai phương pháp trên chính là việc nó chỉ chú trọng đến tần số xuất hiện của một từ, dẫn tới nó hầu như không mang ý nghĩa gì về mặt ngữ cảnh, Co-occurrence Matrix phần nào giải quyết vấn đề đó. Co-occurrence Matrix có ưu điểm là bảo tồn mối quan hệ ngữ nghĩa giữa các từ, được xây dựng dựa trên số lần xuất hiện của các cặp từ trong Context Window. Một Context Window được xác định bởi kích thước và hướng của nó. Hình dưới đây là một ví dụ của Context Window:

![alt text](https://images.viblo.asia/84ebc2ec-6880-4aef-aa50-715ea9dab714.PNG "LSTM")

Thông thường, Co-occurrence Matrix là một ma trận vuông đối xứng, mỗi hàng hoặc mỗi cột sẽ chính là vector biểu thị của từ tương ứng. Tiếp tục ví dụ trên ta sẽ có ma trận Co-occurrence Matrix:

![alt text](https://images.viblo.asia/14e51bd2-f2c6-49f9-82bc-19dc63cdbf66.PNG "LSTM")

**Code**

```python

from nltk.tokenize import word_tokenize
from itertools import combinations
from collections import Counter

sentences = ['John is not fat', 'John is thin']
vocab = set(word_tokenize(' '.join(sentences)))
print('Vocabulary:\n',vocab,'\n')
token_sent_list = [word_tokenize(sen) for sen in sentences]
print('Each sentence in token form:\n',token_sent_list,'\n')

co_occ = {ii:Counter({jj:0 for jj in vocab if jj!=ii}) for ii in vocab}
k=2

for sen in token_sent_list:
    for ii in range(len(sen)):
        if ii < k:
            c = Counter(sen[0:ii+k+1])
            del c[sen[ii]]
            co_occ[sen[ii]] = co_occ[sen[ii]] + c
        elif ii > len(sen)-(k+1):
            c = Counter(sen[ii-k::])
            del c[sen[ii]]
            co_occ[sen[ii]] = co_occ[sen[ii]] + c
        else:
            c = Counter(sen[ii-k:ii+k+1])
            del c[sen[ii]]
            co_occ[sen[ii]] = co_occ[sen[ii]] + c

co_occ = {ii:dict(co_occ[ii]) for ii in vocab}
display(co_occ)
```

