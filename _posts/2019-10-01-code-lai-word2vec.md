---
date: 2019-10-02 15:27:10
layout: post
title: Cùng code lại Word2Vec
description: >-
  Bài 
image: >-
  https://res.cloudinary.com/dzwwhbt1i/image/upload/c_scale,h_300,w_400/v1569863989/lstm_n5dznh.png
category: nlp
author: levanpon98
paginate: true
---

![alt text](https://i.imgur.com/6s4YhKa.png "tanh activation")

Mình mới loi choi sang lĩnh vực NPL vài tuần trước để thử sức. Vây nên hôm nay tranh thủ viết 1 bài, coi như là tổng hợp kiến thức đã học được. Trong bài viết hôm nay, mình sẽ code lại Word2Vec. Mình sẽ không nói nhiều về khái niệm word2vec nữa vì trên google có rất nhiều, cả Anh lẫn Việt.

Trong tutorial này, mình code đơn giản nhất có thể cho dễ hiểu và cũng vì kiến thức mình còn cơ bản, không dám code gì phức tạp quá.

### Tiền xử lí

Trước tiên cần tiền xử lí dữ liệu, bao gồm:
- Lower các từ viết hoa.
- Tách các câu
- Bỏ các kí tự đặc biệt (trong bài này mình chỉ bỏ dấu “.”)

B1: Tách câu, tách từ, tạo dictinary để map giữa word và index của word. Mình sẽ dùng 1 data mẫu kinh điển mà ai đọc về Word2Vec cũng dễ gặp: ‘He is the king. The king is royal . she is the queen. She is the royal’

```python
import numpy as np
import tensorflow as tf

def split_text(corpus_raw):
    split_sequences = []
    sequences = corpus_raw.split('.')
    for s in sequences:
        split_sequences.append(s.split())
    return split_sequences

def get_vocabs(text):
    text = text.replace(".", "")
    words = text.split()
    words = set(words)
    return words

def get_dictinary(words):
    word2int = {}
    int2word = {}
    for i, w in enumerate(words):
        word2int[w] = i
        int2word[i] = w
    return word2int, int2word

raw_text = 'He is the king. The king is royal . she is the queen. She is the royal'
corpus = raw_text.lower()
words = get_vocabs(corpus)
vocab_size = len(words)
word2int, int2word = get_dictinary(words)
```

B2: Với 1 từ xác định word trong dữ liệu mẫu (mình gọi là center_word), lấy tất cả các cặp (center_word, around_word) với around_word là 1 trong những từ xung quanh nó trong phạm vi window_size. Lấy tất cả các cặp có thể trong mẫu:

```python 
def get_word_pair(sequence, word_index, window_size):
    pairs = []
    for nb_word in sequence[max(0, word_index-window_size) : min(word_index + window_size, len(sequence))+1]:
        if(nb_word != sequence[word_index]):
            pairs.append((sequence[word_index], nb_word))
    return pairs
    
def gen_xy_text(sequences, window_size=2):
    word_pairs = []
    for sequence in sequences:
        for word_index, word in enumerate(sequence):
            word_pairs += get_word_pair(sequence, word_index,window_size)
    return word_pairs

word_pairs = gen_xy_text(sequences, 2)

# output = [[he, is] , [he, the], [is, the], [is, king] ]
```

B3: convert word_pairs từ dạng text sang dạng số (và ngược lại), tạo onehot vector -> tạo train_data

```python
# convert to digit
def convert_word_pairs(word_pairs, word2int= word2int):
    digit_pairs = []
    for w_pair in word_pairs:
        digit_pairs.append((word2int[w_pair[0]], word2int[w_pair[1]] ))
    return digit_pairs

# convert to text
def convert_digit_pairs(digit_pairs, int2word=int2word):
    word_pairs = []
    for d_pair in digit_pairs:
        word_pairs.append((int2word[d_pair[0]], int2word[d_pair[1]] ))
    return word_pairs

def to_onehot_vector(value, vocab_size):
    onehot_vector = np.zeros(vocab_size)
    onehot_vector[value] = 1
    return onehot_vector

digit_xy = convert_word_pairs(word_pairs)
x_data = []
y_data = []
for xy in digit_xy:
    x_data.append(to_onehot_vector(xy[0], vocab_size))
    y_data.append(to_onehot_vector(xy[1], vocab_size))
x_data = np.array(x_data)    
y_data = np.array(y_data)
```

### Tạo model để train

Model là 1 shalow net với input là center_word, 1 hidden layer, output là around_word. Model có dạng tương tự auto encoder.

```python
def cross_entropy_loss(y_pre, y_true):
   return tf.reduce_mean( -tf.reduce_sum( y_true * tf.log(y_pre), reduction_indices=[1]))

embed_dim = 4
x = tf.placeholder(tf.float32, shape=(None, vocab_size))
y_true = tf.placeholder(tf.float32, shape=(None, vocab_size))

w_1 = tf.Variable(tf.random_normal([vocab_size, embed_dim]))
b_1 = tf.Variable(tf.random_normal([embed_dim]))

hidden = tf.matmul(x, w_1) + b_1
w_2 = tf.Variable(tf.random_normal([embed_dim, vocab_size]))
b_2 = tf.Variable(tf.random_normal([vocab_size]))
temp_y = tf.matmul(hidden, w_2) + b_2
y_pre = tf.nn.softmax(temp_y)

loss = cross_entropy_loss(y_pre, y_true)

session = tf.Session()
init = tf.global_variables_initializer()
session.run(init)
train = tf.train.GradientDescentOptimizer(0.1).minimize(loss)
iters = 1000

for i in range(iters):
    feed_dict = {x: x_data, y_true: y_data}
    session.run(train, feed_dict=feed_dict)
    loss_val = session.run(loss, feed_dict=feed_dict)
    w1_val = session.run(w_1)

### Embed vector
vectors = session.run(w_1 + b_1)
```

Trong bài viết này mình không đề cập tới validate, tính accuracy, etc.. Vì bài viết của mình nhằm cho người đọc hiểu thuật toán Word2Vec, chứ chắc chắn chất lượng model mình trên sẽ không cao Sau khi train model xong, thứ ta cần là mạng đã được căts bỏ phần sau (chỉ giữ lại hidden layer). Thực chất, ta chỉ cần giữ lại W_1 và b_1 mà thôi. Vì 1 word sẽ tương ứng với 1 dòng trong W_1, minh họa dưới:

![alt text](https://i.imgur.com/kvUpgqJ.png "tanh activation")

### Sử dụng Embed Vector

Một tính chất tuyệt vời của Word2Vec là các embed Vector có thể thể hiện được mỗi quan hệ ngữ nghĩa giữa các từ với nhau: vd khoảng cách giữa embed của ‘he’ sẽ gần ‘she’ . ‘king’ gần ‘queen’. Sau khi đã có được Embed Vector, ta tiến hành 1 vài thuật toán trên nó: tìm từ đồng nghĩa, tính khoảng cách, visualize trên đồ thị 2D.

```python
def eclidean_dist(vec1 , vec2):
    return np.sqrt(np.sum(np.square(vec1 - vec2)))

def closest(word, vectors):
    i_word = word2int[word]
    word_vector = vectors[i_word]
    min_index = 0
    min_dist = 0
    while(True):
        min_index = randint(0, len(vectors)-1)
        if(min_index != i_word):
            min_dist = eclidean_dist(word_vector, vectors[min_index])
            break
    for i, v in enumerate(vectors):
        dist = eclidean_dist(word_vector, v)
        if( i != i_word and dist < min_dist):
            min_index = i
            min_dist = dist
    return min_index, min_dist
word = 'royal'
min_index, min_dist = closest(word, vectors)
print(int2word[min_index])
## expected result: queen
```

Ruduce chiều dữ liệu về 2 chiều -> Visual trên đồ thị:

```python
from sklearn.manifold import TSNE
from sklearn import preprocessing
from matplotlib import pyplot as plt

def plot_space(embed_vector):
    plt.figure()
    plt.ylim(ymax=1,ymin=-1 )
    plt.xlim(xmax=1, xmin=-1)
    for i,v in enumerate(embed_vector):
        plt.annotate(int2word[i], xy=(v[0], v[1]))
    plt.show()


model = TSNE(n_components=2)
normalizer = preprocessing.Normalizer()
x_embed = model.fit_transform(vectors)
x_embed = normalizer.fit_transform(x_embed, 'l2')
plot_space(x_reduce)
```

Nếu model tốt, kết quả của bạn sẽ được như hình dưới đây. Ảnh minh họa kết quả của Word2Vec (của 1 tác giả nào đó trên mạng, not me :p ).

![alt text](https://i.imgur.com/YxMBo2o.jpg "tanh activation")