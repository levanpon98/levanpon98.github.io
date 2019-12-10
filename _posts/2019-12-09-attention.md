---
title: 'Hiểu sâu hơn về mô hình Attention (Code Python Demo)'
date: 2019-12-10
permalink: /posts/2019/12/attention/
tags:
  - nlp
---

Ở bài trước, chúng mình cùng tìm hiểu về mô hình Sequence-To-Sequence. Ngoài những thành công mà mô hình này đem lại trong các bài toán về translation, text sumarization, ..., thì mô hình này vẫn còn nhiều vấn đề, đặc biệt là vấn đề về khả năng đóng gói thông tin, ngữ nghĩa của một câu có thể bị mất nếu câu đó quá dài. Lúc này mô hình attention được sinh ra để giải quyết vấn đề nêu trên. Mình hy vọng qua bài này, các bạn có thể hiểu hơn về mô hình Attention và xem đây như là một tư liệu trong hành trình học tập của mình.

**Note**: Những hình ảnh động bên dưới là video, các bạn có thể dừng video lại để có thể ngồi ngẫm nghĩ quá trình tính toán xảy ra như thế nào nhé.

## Ý tưởng

Chúng ta cùng xét qua một ví dụ để hiểu rõ hơn về ý tưởng của mô hình Attention.

Giả sử bạn đang nhìn vào một bức ảnh lớp học của bạn chụp kỷ yếu cùng với giáo viên. Và một người lạ tới hỏi bạn ai là giáo viên, thì lập tức bạn sẽ tìm một cao hơn, lớn hơn, có thể mặc áo dài. Nói rõ hơn, lúc này bộ não của chúng ta sẽ đưa ra những đặc điểm của một người phù hợp với câu hỏi, và bắt đầu tìm kiếm trong hình. Và nếu người lạ đó tiếp tục hỏi câu khác, thì não bộ của chúng ta sẽ bắt đầu liệt kê các tính năng và tìm kiếm theo tính năng đó. Những phần không thuộc tính năng đó sẽ bị loại bỏ. Hoạt động này chính là sự **chú ý** của não bộ đối với từng đặc điểm.

Ví dụ trên cũng chính là ý tưởng chính của mô hình **Attention**.

## Attention hoạt động như thế nào?

Cùng nhắc lại mô hình seq2seq truyền thống, các hidden state trung gian sẽ bị loại bỏ và chỉ giữ lại hidden state của layer cuối cùng. Đây chính là nguyên nhân chính dẫn đến mô hình seq2seq không thích hợp với những câu dài. Điều này đã được khắc phục trong Attention, khi mà các hidden state của tất cả các layer sẽ được gộp lại thành 1 context vector. Hình động bên dưới sẽ mô tả sơ lược về hoạt động của Attention trước khi đi sâu vào mô hình.

<video width="100%" height="auto" loop="" autoplay="" controls="">
   <source src="/images/seq2seq_7.mp4" type="video/mp4">
   Your browser does not support the video tag.
</video>

Mô hình Attention được chia ra làm 2 loại chính

- [Bahdanau Attention](https://arxiv.org/pdf/1409.0473.pdf)
- [Luong Attention](https://arxiv.org/pdf/1508.04025.pdf)

## Bahdanau Attention

![](/images/Slide38.jfif)

Mình sẽ chia quá trình tính toán của Bahanau Attention ra làm 6 giai đoạn.

**Bước 1: Tính hidden state của mỗi layer encoder**

Bộ encoder của Attention tương tự như bộ encoder của mô hình seq2seq. Tuy nhiên, thay vì chỉ sử dụng hidden state cuối thì Attention mode sử dụng toàn bộ các hidden state của encoder.

**Bước 2:** **Tính Alignment Score**

Như đã bàn luận về ý tưởng của Attention, khi predict ra một từ, chúng ta không cần toàn bộ encoder hidden state. Vì thế, trong  những hidden state mà bộ encoder đưa vào, chúng ta cần phải biết được những hidden state nào cần thiết. Một cách đơn giản là chúng ta tính toán điểm số của từng hidden state. 

**Vậy làm sao để tính được điểm số của từng hidden state?**

Phương pháp tính score được đề xuất trong Bahdanau Attention là sử dụng decoder hidden state của bước trước và toàn bộ các encoder hidden state theo công thức:
$$
score = W_{combined} \cdot \tanh(W_{decoder} \cdot H_{decoder} + W_{encoder} \cdot H_{encoder})
$$
$H_{decoder}$ và $H_{encoder}$ sẽ được đưa vào một Linear layer

![](/images/Slide44.jfif)

 Sau đó cộng tổng 2 output lại và đưa vào hàm $\tanh$ activation 

![](/images/Slide45.jfif)

Sau đó nhân với một weight để huấn luyện, kết quả của quá trình nhân là alignment score

![](/images/Slide46-7.jfif)

**Lưu ý**: Khi chúng ta predict từ đầu tiên, bộ decoder không có bất kỳ hidden state nội bộ nào nên chúng ta sẽ xem hidden state cuối cùng của bộ encoder như là previous hidden state của bộ decoder.

**Bước 3: Softmax alignment score**

Khi score đã được sinh ra từ  $h_1, h_2$, chúng ta sẽ đưa các score này vào hàm softmax để tính ra weight attention $\alpha_1, \alpha_2$. Khi chúng ta sử dụng hàm softmax sẽ có một số ưu điểm như sau

- Toàn bộ các trọng số sẽ nằm trong khoản từ 0 đến 1 
- Tổng của các trọng số bằng 1

Do đó, chúng ta sẽ có một xác suất đẹp cho các attention weights

![](/images/Slide47.jfif)

**Bước 4: Tính context vector**

Khi đã tính xong attention weights, chúng ta cần phải tính context vector. Ở bước này, chúng ta sẽ nhân các hidden state của bộ encoder với attention weight tương ứng.

Ví dụ: $\text{context vector} =  \alpha_1 * h_1 + \alpha_2 * h_2$

Dễ dàng nhìn thấy, nếu $\alpha_1$ lớn thì $h_1$ sẽ càng được chú ý, và từ được predict ra sẽ mang thông tin của $h_1$ nhiều hơn.

![](/images/Slide48.jfif)

**Bước 5: Kết hợp context vector với output trước đó**

Cuối cùng, bộ decoder sử dụng hai vectơ đầu vào bên dưới để tạo từ tiếp theo trong chuỗi

- Context vector
- Vector word được predict ra trước đó

Chúng ta chỉ cần ghép hai vectơ này để tạo ra một vecto hợp nhất, sau đó đưa vectơ hợp nhất vào bộ decoder. Lưu ý rằng đối với bước đầu tiên, vì không có đầu ra trước đó, chúng ta sẽ sử dụng mã thông báo < END >.

![](/images/Slide49.jfif)

**Bước 6: Output**

Lúc này bộ decoder sẽ sinh ra từ tiếp theo của chuỗi và hidden state để sử dụng cho việc tính score tiếp theo.

<video width="100%" height="auto" loop="" autoplay="" controls="" __idm_id__="522540035">
   <source src="/images/attention_tensor_dance.mp4" type="video/mp4">
   Your browser does not support the video tag.
</video>

## Luong Attention

![](/images/Slide51.jfif)

Loại thứ hai của mô hình attention được đề xuất bởi Thanh Luong trong bài báo [Effective Approaches to Attention-based Neural Machine Translation](https://arxiv.org/abs/1508.04025). Mô hình này còn được gọi là Multiplicative Attention, nó có 2 điểm khác biệt chính so với mô hình Bahdanau Attention như sau.

- Các tính score 
- Vị trí mà cơ chế Attention được giới thiệu trong bộ decoder.

Có ba cách tính score được đề xuất trong bài báo của Lương so với loại một của Bahdanau. Ngoài ra, cấu trúc attention của bộ encoder trong Luong Attention có một số điểm khác biệt, và context vector chỉ được sử dụng sau khi RNN tạo đầu ra cho bước thời gian đó. Chúng ta sẽ khám phá những khác biệt này một cách chi tiết hơn qua các bước thực hiện của mô hình Luong Attention như sau:

**Bước 1: Tính hidden state của mỗi layer encoder**

Bước này giống như trong Bahdanau Attention

**Bước 2: Decoder RNN**

Không giống như Bahanau Attention, bộ decoder của Luong Attention sẽ sử dụng RNN ở bước đầu tiên của quá trình decode thay vì cuối cùng. RNN network này lấy đầu vào là hidden state ở bước trước và word embedding của từ được predict ra trước đó.	

**Bước 3: Tính Alignment Score**

Trong mô hình Luong Attention, có 3 các tính alignment score được đề xuất trong bài báo

- **Dot**

  Đây là phương pháp tính alignment score đơn giản nhất, chỉ cần lấy decoder hidden state nhân với bộ encoder hidden state, cách tính này sẽ được mô tả bởi công thức bên dưới.
  $$
  score = H_{decoder} \cdot H_{encoder}
  $$
  

- **General**

  Phương pháp thứ hai được gọi là general và tương tự với phương pháp Dot, tuy nhiên sẽ có một ma trân weight được thêm vào phương trình, ma trận này sẽ được đào tạo cùng với mô hình.
  $$
  score = W(H_{decoder} \cdot H_{encoder})
  $$
  

- **Concat**

  Phương thức cuối cùng gần giống như cách tính alignment score của mô hình Bahdanan Attention. Khác biệt nằm ở chỗ, decoder hidden state và encoder hidden state sẽ dùng chung một ma trận weight thay vì sử dụng 2 ma trận weight như trong mô hình Bahdanan Attention.
  $$
  score = W \cdot \tanh(W_{combined}(H_{decoder} + H_{encoder}))
  $$

**Bước 4: Softmax alignment score**

 Bước này sử dụng hàm softmax để đưa score về khoản 0 đến 1

**Bước 5: Tính context vector**

Để tính context vector, ta lấy kết quả của bước 4 đem nhân với bộ encoder hidden state.

**Bước 6: Decoder Ouput**

Sử dụng context vector kết hợp với decoder hidden state chúng ta tạo ra ở bước 2. Sau đó đưa vector kết hợp này một Linear layer có nhiệm vụ như một bộ phân loại để chúng ta có được một xác suất của từ tiếp theo.

## Code Demo

Các bạn có thể xem full code ở [đây](https://bitbucket.org/levanpon1009/attention/) nhé.

Đây là project dịch từ tiếng Việt sang tiếng Anh của mình khi tham dự cuộc thi hackathon AI (mà hổng được giải, haha ^^)

Đầu tiên mình sẽ khởi tạo các hàm để preprocess data nhe.

```python
import tensorflow as tf
import io
import unicodedata



def unicode_to_ascii(s):
    return ''.join(c for c in unicodedata.normalize('NFD', s)
                   if unicodedata.category(c) != 'Mn')


def preprocess_sentence(w):
    exclude = set(string.punctuation) # Set of all special characters
    remove_digits = str.maketrans('', '', string.digits) # Set of all digits
    w = w.lower() # lower casing
    w = re.sub("'", '', w) # remove the quotation marks if any
    w = ''.join(ch for ch in w if ch not in exclude)
    sent = sent.translate(remove_digits) # remove the digits
    w = w.rstrip().strip()
    w = re.sub(" +", " ", w) #remove extra spaces
    w = '<start> ' + w + ' <end>'
    return w


def create_dataset(path, num_examples):
    lines = io.open(path, encoding='UTF-8').read().strip().split('\n')

    word_pairs = [[preprocess_sentence(w) for w in l.split('\t')] for l in lines[:num_examples]]

    return zip(*word_pairs)


def max_length(tensor):
    return max(len(t) for t in tensor)


def tokenize(lang):
    lang_tokenizer = tf.keras.preprocessing.text.Tokenizer(
        filters='')
    lang_tokenizer.fit_on_texts(lang)

    tensor = lang_tokenizer.texts_to_sequences(lang)

    tensor = tf.keras.preprocessing.sequence.pad_sequences(tensor,
                                                           padding='post')

    return tensor, lang_tokenizer


def load_dataset(path, num_examples=None):
    # creating cleaned input, output pairs
    targ_lang, inp_lang = create_dataset(path, num_examples)

    input_tensor, inp_lang_tokenizer = tokenize(inp_lang)
    target_tensor, targ_lang_tokenizer = tokenize(targ_lang)

    return input_tensor, target_tensor, inp_lang_tokenizer, targ_lang_tokenizer
```

Tiếp theo mình sẽ khởi tạo model, mình sử dụng mô hình Bahdanau Attention nhé.

```python
import tensorflow as tf


class BahdanauAttention(tf.keras.Model):
    def __init__(self, units):
        super(BahdanauAttention, self).__init__()
        self.W1 = tf.keras.layers.Dense(units)
        self.W2 = tf.keras.layers.Dense(units)
        self.V = tf.keras.layers.Dense(1)

    def call(self, query, values):
        # hidden shape == (batch_size, hidden size)
        # hidden_with_time_axis shape == (batch_size, 1, hidden size)
        # we are doing this to perform addition to calculate the score
        hidden_with_time_axis = tf.expand_dims(query, 1)

        # score shape == (batch_size, max_length, 1)
        # we get 1 at the last axis because we are applying score to self.V
        # the shape of the tensor before applying self.V is (batch_size, max_length, units)
        score = self.V(tf.nn.tanh(
            self.W1(values) + self.W2(hidden_with_time_axis)))

        # attention_weights shape == (batch_size, max_length, 1)
        attention_weights = tf.nn.softmax(score, axis=1)

        # context_vector shape after sum == (batch_size, hidden_size)
        context_vector = attention_weights * values
        context_vector = tf.reduce_sum(context_vector, axis=1)

        return context_vector, attention_weights


class Encoder(tf.keras.Model):
    def __init__(self, vocab_size, embedding_dim, enc_units, batch_sz):
        super(Encoder, self).__init__()
        self.batch_sz = batch_sz
        self.enc_units = enc_units
        self.embedding = tf.keras.layers.Embedding(vocab_size, embedding_dim)
        self.gru = tf.keras.layers.GRU(self.enc_units,
                                       return_sequences=True,
                                       return_state=True,
                                       recurrent_initializer='glorot_uniform')

    def call(self, x, hidden):
        x = self.embedding(x)
        output, state = self.gru(x, initial_state=hidden)
        return output, state

    def initialize_hidden_state(self):
        return tf.zeros((self.batch_sz, self.enc_units))


class Decoder(tf.keras.Model):
    def __init__(self, vocab_size, embedding_dim, dec_units, batch_sz):
        super(Decoder, self).__init__()
        self.batch_sz = batch_sz
        self.dec_units = dec_units
        self.embedding = tf.keras.layers.Embedding(vocab_size, embedding_dim)
        self.gru = tf.keras.layers.GRU(self.dec_units,
                                       return_sequences=True,
                                       return_state=True,
                                       recurrent_initializer='glorot_uniform')
        self.fc = tf.keras.layers.Dense(vocab_size)

        # used for attention
        self.attention = BahdanauAttention(self.dec_units)

    def call(self, x, hidden, enc_output):
        # enc_output shape == (batch_size, max_length, hidden_size)
        context_vector, attention_weights = self.attention(hidden, enc_output)

        # x shape after passing through embedding == (batch_size, 1, embedding_dim)
        x = self.embedding(x)

        # x shape after concatenation == (batch_size, 1, embedding_dim + hidden_size)
        x = tf.concat([tf.expand_dims(context_vector, 1), x], axis=-1)

        # passing the concatenated vector to the GRU
        output, state = self.gru(x)

        # output shape == (batch_size * 1, hidden_size)
        output = tf.reshape(output, (-1, output.shape[2]))

        # output shape == (batch_size, vocab)
        x = self.fc(output)

        return x, state, attention_weights

```

Tiếp theo mình sẽ tiến hành train mô hình

```python
from __future__ import absolute_import, division, print_function, unicode_literals

from sklearn.model_selection import train_test_split

from utils import *
from model import Encoder, Decoder, BahdanauAttention

import os
import time

# Download the file

path_to_file = "./data/vi-eng.txt"


# Try experimenting with the size of that dataset
num_examples = 118964
input_tensor, target_tensor, inp_lang, targ_lang = load_dataset(path_to_file, num_examples)

# Calculate max_length of the target tensors
max_length_targ, max_length_inp = max_length(target_tensor), max_length(input_tensor)

# Creating training and validation sets using an 80-20 split
input_tensor_train, input_tensor_val, target_tensor_train, target_tensor_val = train_test_split(input_tensor,target_tensor,test_size=0.2)

BUFFER_SIZE = len(input_tensor_train)
BATCH_SIZE = 64
steps_per_epoch = len(input_tensor_train) // BATCH_SIZE
embedding_dim = 256
units = 1024
vocab_inp_size = len(inp_lang.word_index) + 1
vocab_tar_size = len(targ_lang.word_index) + 1

dataset = tf.data.Dataset.from_tensor_slices((input_tensor_train, target_tensor_train)).shuffle(BUFFER_SIZE)
dataset = dataset.batch(BATCH_SIZE, drop_remainder=True)

encoder = Encoder(vocab_inp_size, embedding_dim, units, BATCH_SIZE)
decoder = Decoder(vocab_tar_size, embedding_dim, units, BATCH_SIZE)


optimizer = tf.keras.optimizers.Adam()
loss_object = tf.keras.losses.SparseCategoricalCrossentropy(from_logits=True, reduction='none')


def loss_function(real, pred):
    mask = tf.math.logical_not(tf.math.equal(real, 0))
    loss_ = loss_object(real, pred)

    mask = tf.cast(mask, dtype=loss_.dtype)
    loss_ *= mask

    return tf.reduce_mean(loss_)


checkpoint_dir = './training_checkpoints'
checkpoint_prefix = os.path.join(checkpoint_dir, "ckpt")
checkpoint = tf.train.Checkpoint(optimizer=optimizer,
                                 encoder=encoder,
                                 decoder=decoder)


@tf.function
def train_step(inp, targ, enc_hidden):
    loss = 0

    with tf.GradientTape() as tape:
        enc_output, enc_hidden = encoder(inp, enc_hidden)

        dec_hidden = enc_hidden

        dec_input = tf.expand_dims([targ_lang.word_index['<start>']] * BATCH_SIZE, 1)

        # Teacher forcing - feeding the target as the next input
        for t in range(1, targ.shape[1]):
            # passing enc_output to the decoder
            predictions, dec_hidden, _ = decoder(dec_input, dec_hidden, enc_output)

            loss += loss_function(targ[:, t], predictions)

            # using teacher forcing
            dec_input = tf.expand_dims(targ[:, t], 1)

    batch_loss = (loss / int(targ.shape[1]))

    variables = encoder.trainable_variables + decoder.trainable_variables

    gradients = tape.gradient(loss, variables)

    optimizer.apply_gradients(zip(gradients, variables))

    return batch_loss


EPOCHS = 30

for epoch in range(EPOCHS):
    start = time.time()

    enc_hidden = encoder.initialize_hidden_state()
    total_loss = 0

    for (batch, (inp, targ)) in enumerate(dataset.take(steps_per_epoch)):
        batch_loss = train_step(inp, targ, enc_hidden)
        total_loss += batch_loss

        if batch % 100 == 0:
            print('Epoch {} Batch {} Loss {:.4f}'.format(epoch + 1,
                                                         batch,
                                                         batch_loss.numpy()))
    checkpoint.save(file_prefix=checkpoint_prefix)
    print('Epoch {} Loss {:.4f}'.format(epoch + 1,
                                        total_loss / steps_per_epoch))
    print('Time taken for 1 epoch {} sec\n'.format(time.time() - start))
```

Và cuối cùng là phần predict

```python
from utils import *
from model import Encoder, Decoder, BahdanauAttention
import argparse
import time

parser = argparse.ArgumentParser(description='Creating Classifier')

######################
# Optimization Flags #
######################

parser.add_argument('-m', '--message')
args = parser.parse_args()

path_to_file = "./data/vi-eng.txt"

start = time.time()

num_examples = 118964
input_tensor, target_tensor, inp_lang, targ_lang = load_dataset(path_to_file, num_examples)

# Calculate max_length of the target tensors
max_length_targ, max_length_inp = max_length(target_tensor), max_length(input_tensor)


BATCH_SIZE = 64
embedding_dim = 256
units = 1024
vocab_inp_size = len(inp_lang.word_index) + 1
vocab_tar_size = len(targ_lang.word_index) + 1


encoder = Encoder(vocab_inp_size, embedding_dim, units, BATCH_SIZE)
decoder = Decoder(vocab_tar_size, embedding_dim, units, BATCH_SIZE)

checkpoint_dir = './training_checkpoints'
checkpoint = tf.train.Checkpoint(optimizer=tf.keras.optimizers.Adam(),
                                 encoder=encoder,
                                 decoder=decoder)

checkpoint.restore(tf.train.latest_checkpoint(checkpoint_dir))


def evaluate(sentence):
    sentence = preprocess_sentence(sentence)

    inputs = [inp_lang.word_index[i] for i in sentence.split(' ')]
    print(*inputs)
    inputs = tf.keras.preprocessing.sequence.pad_sequences([inputs],
                                                           maxlen=max_length_inp,
                                                           padding='post')

    inputs = tf.convert_to_tensor(inputs)
    result = ''

    hidden = [tf.zeros((1, units))]
    enc_out, enc_hidden = encoder(inputs, hidden)

    dec_hidden = enc_hidden
    dec_input = tf.expand_dims([targ_lang.word_index['<start>']], 0)

    for t in range(max_length_targ):
        predictions, dec_hidden, attention_weights = decoder(dec_input,
                                                             dec_hidden,
                                                             enc_out)

        # storing the attention weights to plot later on

        predicted_id = tf.argmax(predictions[0]).numpy()

        result += targ_lang.index_word[predicted_id] + ' '

        if targ_lang.index_word[predicted_id] == '<end>':
            return result

        # the predicted ID is fed back into the model
        dec_input = tf.expand_dims([predicted_id], 0)

    return result


def translate(sentence):
    result = evaluate(sentence)

    return result


if __name__ == '__main__':
    # print(args.message)
    translate(args.message)

```

## Kết luận

Ở code trên, mình chỉ sử dụng GRU, nếu các bạn có GPU, thì thay thế hàm GRU thành CuDNNGRU, như vậy tốc độ sẽ training sẽ được tăng lên khá nhiều. Bên cạnh đó, việc thêm Bidirectional encoder sẽ tăng hiệu suất lên đáng kể.

Nhược điểm lớn nhất của Attention đó chính là khó có thể xử lý song song. Để giải quyết vấn đề này, Google Brain đã đưa ra một mô hình "Transformer". Mô hình này chỉ sử dụng Attention và loại bỏ RNN và Convolutional, điều này sẽ làm tăng tính song song và tính hiệu quả. Bài viết tiếp theo mình sẽ đi sâu vào giải thích mô hình Transformer, mong các bạn đón xem nhé.

Bài viết này mình xin kết thúc tại đây. Hẹn gặp lại ^^

## Tài liệu tham khảo

- [http://jalammar.github.io/visualizing-neural-machine-translation-mechanics-of-seq2seq-models-with-attention/](http://jalammar.github.io/visualizing-neural-machine-translation-mechanics-of-seq2seq-models-with-attention/)
- [https://towardsdatascience.com/intuitive-understanding-of-attention-mechanism-in-deep-learning-6c9482aecf4f](https://towardsdatascience.com/intuitive-understanding-of-attention-mechanism-in-deep-learning-6c9482aecf4f)
- [https://arxiv.org/abs/1409.0473](https://arxiv.org/abs/1409.0473)
- [https://medium.com/@shashank7.iitd/understanding-attention-mechanism-35ff53fc328e](https://medium.com/@shashank7.iitd/understanding-attention-mechanism-35ff53fc328e)
- [https://blog.floydhub.com/attention-mechanism/](https://blog.floydhub.com/attention-mechanism/)

