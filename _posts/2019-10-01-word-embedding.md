---
title: 'Cùng tìm hiểu về Word Embedding (Code Python demo)'
date: 2019-09-27
permalink: /posts/2019/12/word-embedding/
tags:
  - nlp
---

Word Embedding là một trong những phương pháp nổi bật nhất để có thể biểu diễn một từ. Nó có khả năng tóm lượt ngữ cảnh của một từ trong đoạn văn, sự tương đồng về ngữ nghĩa và cú pháp, và quan hệ giữa các từ khác...

Vậy chính xác Word Embedding là gì? Nói một cách đơn giản, chúng là những vector số (thường là số thực). Vậy làm như thế nào để một từ có thể chuyển đổi thành một vector, và quan trọng hơn, làm thế nào để vector đó có thể nắm giữ ngữ cảnh.

**Word Embedding** được phân thành 2 loại chính:

- Frequency-based embedding
- Prediction-based embedding

## Frequency-based embedding

Phương pháp này dựa vào tần suất xuất hiện của từ để tạo ra vector từ, có 3 loại phổ biến:
- One-hot encoding (Count Vector)
- TF-IDF transforming
- Co-occurrence Matrix

Mình sẽ đi chi tiết vào từng loại

### One-hot encoding (Count Vector)

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

### TF-IDF transforming

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

### Co-occurrence Matrix

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

### Glove (Glove: Global Vectors for Word Representation)

Mô hình Glove dựa trên Co-occurrence Matrix và bản chất là xác suất. Việc đào tạo mô hình Glove sẽ cho ra một không gian vector với cấu trúc có ý nghĩa. 

Để có thể lưu trữ thông tin, chúng ta sử dụng một ma trận Co-occurrence $$X$$, mỗi phần tử trong đó tương đương với xác suất xuất hiện của từ $$j$$ trong ngữ cảnh $$i$$. Chúng ta có công thức sau:

$$P_{ij} = P{j|i} = \frac{X_{ij}} {X_i}$$

Trong đó: 
- $$X_{ij}: $$ là số lần xuất hiện của từ $$j$$ trong ngữ cảnh của từ $$i$$
- $$X_i: $$ Là số lần xuất hiện của từ $$i$$ trong ngữ cảnh của toàn bộ các từ còn lại ngoài $$i$$

Từ đây mình sẽ định nghĩa một hàm $$F$$ 

$$F(w_i, w_j, \tilde{w}_k) = \frac{P_{ik}} {P_{jk}}$$

Ý tưởng là, độ tương tự ngữ nghĩa giữa hai từ $$i,j$$ có thể được xác định thông qua độ tương tự ngữ nghĩa giữa từ $$k$$ với mỗi từ $$i,j$$. Để rõ hơn về độ tương tự này, ta lấy 2 vector trừ cho nhau:

$$F(w_i - w_j, \tilde{w}_k) = \frac{P_{ik}} {P_{jk}}$$

Trong phương trình trên, vế phải là vector, tuy nhiên vế trái là một đại lương vô hướng, vì vậy chúng ta cần biến đổi thêm như sau

$$F((w_i - w_j)^T\tilde{w}_k) = \frac{P_{ik}} {P_{jk}}$$

Từ đây chúng ta có thể thay thế xác suất bằng:


$$F((w_i - w_j)^T\tilde{w}_k) = \frac{w_i^T\tilde{w}_k} {w_j^T\tilde{w}_k}$$

Trong đó:

$$F(w_i^T\tilde{w}_k) = P_{ik} = \frac{X_{ik}} {X_i}$$$

Nếu chúng ta giả sử hàm $$F$$ là hàm `exp()`, thì phương trình trên trở thành:

$$w_i^T\tilde{w}_k = log P_{ik} = log X_{ik} - log X_i$$

Để tối ưu ta viết lại:

$$w_i^T\tilde{w}_k + b_i + \tilde{b}_k = log X_{ik}$$

Trong đó: $$b_i ,\tilde{b}_k$$ là các bias tương ứng.

Vậy hàm loss function mà chúng ta đang cố gắng để tối ưu là một hàm linear regression:

$$J = \displaystyle\sum_{i,j=1}^{V} f(X_{ij})(w_i^T\tilde{w}_k + b_i + \tilde{b}_k - log X_{ik})^2$$

Trong đó: $$f$$ là hàm trọng số mà sẽ được định nghĩa sẵn

Code demo:

```python
import itertools
from gensim.models.word2vec import Text8Corpus
from glove import Corpus, Glove
# sentences and corpus from standard library
sentences = list(itertools.islice(Text8Corpus('text8'),None))
corpus = Corpus()
# fitting the corpus with sentences and creating Glove object
corpus.fit(sentences, window=10)
glove = Glove(no_components=100, learning_rate=0.05)
# fitting to the corpus and adding standard dictionary to the object
glove.fit(corpus.matrix, epochs=30, no_threads=4, verbose=True)
glove.add_dictionary(corpus.dictionary)
glove.save('glove.model')
```

## Frequency-based embedding

Prediction-based Embedding xây dựng các vector từ dựa vào các mô hình dự đoán. Tiêu biểu nhất chính là Word2vec, nó là sự kết hợp của 2 mô hình: CBOW (Continous Bag Of Words) và Skip-gram. Cả hai mô hình này đều được xây dựng dựa trên một mạng neuron gồm 3 lớp:1 Input Layer,1 Hidden Layer và 1 Output Layer. Mục đích chính của các mạng neuron này là học các trọng số biểu diễn vector từ.

### CBOW 

Hoạt động dựa trên cách thức là nó sẽ dự đoán xác suất của một từ được đưa ra theo ngữ cảnh (một ngữ cảnh có thể gồm một hoặc nhiều từ), với input là một hoặc nhiều One-hot vector của các từ ngữ cảnh có chiều dài V (với V là độ lớn của từ điển), output sẽ là một vector xác suất cũng với chiều dài V của từ liên quan hoặc còn thiếu, Hidden Layer có chiều dài N, N cũng chính là độ lớn của vector từ biểu thị. Dưới đây là mô hình CBOW với ngữ cảnh là 1 từ đơn:

![alt text](https://images.viblo.asia/5f0356d3-7548-4bf5-8fc3-770f7e9cdc18.PNG "tanh activation")

Về bộ dữ liệu dùng để train, Input sẽ bao gồm các bộ One-hot vectors ngữ cảnh và các One-hot vectors của từ mong muốn.

Về cách thức hoạt động, ban đầu hai ma trận trọng số Input-Hidden Weights Matrix và Hidden-Output Weights Matrix được khởi tạo ngẫu nhiên, Input sẽ được nhân với Input-Hidden Weights Matrix ra được một kết quả gọi là Hidden Activation, kết quả này sẽ được nhân tiếp với Hidden-Output Weights Matrix và cuối cùng được đưa vào một hàm softmax để ra được Output là 1 vector xác suất, Output này sẽ được so sánh với Output mong muốn và tính toán độ lỗi, dựa vào độ lỗi này mà mạng neuron sẽ lan truyền ngược trở lại để cập nhật các giá trị của các ma trận trọng số. Đối với mô hình CBOW nhiều Input, các thức hoạt động là tương tự, chỉ khác ở chỗ các kết quả thu được khi nhân các Input với Input-Hidden Weights Matrix sẽ được lấy trung bình để ra được Hidden Activation cuối cùng. Các trọng số của Hidden-Output Weights Matrix sau khi học xong sẽ được lấy làm biểu diễn của các vector từ.

### Skip-gram

Mô hình Skip-gram có cấu trúc tương tự như CBOW, nhưng mục đích của nó là dự đoán ngữ cảnh của một từ đưa vào. Dưới đây là hình ảnh của mô hình Skip-gram:

![alt text](https://images.viblo.asia/04e715ad-af63-47b0-946a-b9fa54cb8718.PNG "tanh activation")

Về bộ dữ liệu dùng để train cũng như cách thức hoạt động của mô hình Skip-gram hoàn toàn tương tự với mô hình CBOW 1 Input, chỉ khác ở điểm thay vì chỉ có 1 độ lỗi, ta có nhiều độ lỗi do có nhiều vector Output, các độ lỗi này sẽ được tổng hợp lại thành 1 độ lỗi cuối cùng để lan truyền ngược trở lại cập nhật các trọng số. Các trọng số của Input-Hidden Weights Matrix sau khi học xong sẽ được lấy làm biểu diễn của các vector từ.

### CBOW vs Skip-gram

Ưu điểm của CBOW là nó không tốn nhiều bộ nhớ để lưu trữ các ma trận lớn, cũng như do nó có bản chất là xác suất cho nên việc hiện thực được cho là vượt trội hơn so với phương pháp khác, tuy nhiên vẫn còn tồn tại khuyết điểm các từ giống nhau nhưng nghĩa khác nhau vẫn chỉ được biểu diễn bằng 1 vector từ duy nhất.

### Một chút so sánh giữa Word2vec và GloVe

Về bản chất, rõ ràng Word2vec và GloVe khác nhau do thuộc 2 loại Embedding khác nhau nhưng đều bắt nguồn từ Context Window, Word2vec sử dụng Context Window để tạo ra các tập train cho mạng neuron còn GloVe sử dụng nó để tạo ra Co-occurrence Matrix. Để ý kĩ một chút, ta thấy rằng GloVe mang tính “toàn cục” hơn là Word2vec vì GloVe tính toán xác suất từ dựa trên toàn bộ tập dữ liệu còn Word2vec học dựa trên các ngữ cảnh đơn lẻ, cũng chính vì lý do này mà GloVe có trội hơn Word2vec cũng như vài mô hình khác trong một số task về ngữ nghĩa, nhận dạng thực thể có gắn tên,vv… Ngoài ra, GloVe có độ ổn định trung bình tốt hơn Word2vec, độ ổn định ở đây chính là độ biến thiên của kết quả giữa hai lần ta thực hiện việc học với cùng một điều kiện xác định (cùng bộ dữ liệu, cùng tham số, cùng điều kiện phần cứng,…).


**Tài liệu tham khảo**
- https://www.analyticsvidhya.com/blog/2017/06/word-embeddings-count-word2veec/
- https://viblo.asia/p/so-luoc-word-embedding-gDVK2RAeKLj