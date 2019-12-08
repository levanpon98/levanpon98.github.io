---
title: 'Cùng tìm hiểu về LSTM, GRU'
date: 2015-08-14
permalink: /posts/2019/12/rnn-lstm-gru/
tags:
  - nlp
---

Trong bài viết này, mình sẽ giới thiệu về LSTM's và GRU's, sau đó mình sẽ giải thích chi tiết LSTM's và GRU's, tại sao nó lại tốt hơn RNN và tốt hơn ở điểm nào. Nếu các bạn đang muốn hiểu thật kỹ về 2 networks này thì đây chính là bài viết đáng để đọc.


### Recurrent Neural Networks

Chúng ta cùng bắt đầu với RNN's, đây là một mạng có bộ nhớ ngắn hạn. Nhưng nếu đoạn văn đủ dài, thì thật sự khó để RNN's có thể nhớ toàn bộ thông tin từ bước đầu tiên đến bước cuối cùng. Vì vậy, nếu bạn đang cố gắng xử lí một đoạn văn để thực hiện một số dự đoán, thì rất có thể RNN's đã bỏ qua một số thông tin ngay từ đầu.


Trong quá trình back propagation, RNN's rất dễ gặp phải hiện tượng là **Vanishing Gradients**, đó là hiện tượng mà khi gradients có giá trị nhỏ dần khi đi xuống các layers thấp hơn, thì kết quả của việc cập nhật weights không thay đổi nhiều so với trước đó, khiến chúng không thể hội tụ và mạng sẽ không thu được kết quả tốt.

![alt text](https://res.cloudinary.com/dzwwhbt1i/image/upload/c_scale,w_901/v1569865527/1_PYiQa_bNzM8ugYz_D1yvgw_uq3uwc.png "Vanishing Gradients")

Vì vậy, các layers được cập nhập nhỏ sẽ ngừng học, và các layers lớn hơn có thể quên nó, vì thế RNN's có bộ nhớ ngắn hạn. Nếu muốn biết thêm về cơ chế hoạt động của RNN's, thì bạn có thể đọc tại **đây**.

### LSTM's, GRU's ra đời

LSTM's và GRU's ra đời để giải quyết các vấn đề của RNN's với một cơ chế được gọi là **cổng** để có thể điều chỉnh được luồng thông tin.

![alt text](https://res.cloudinary.com/dzwwhbt1i/image/upload/v1569865829/1_yBXV9o5q7L_CvY7quJt3WQ_r9gtsq.png "LSTM's and GRU's")

Những cổng này có thể phát hiện trong chuỗi những từ, dữ liệu nào cần được giữ lại hoặc quên đi, và chuyển những thông tin liên quan để đi đến dự đoán. Chính vì có thể giữ lại được một số thông tin quan trọng, LSTM's và GRU's được sử dụng trong rất nhiều ứng dụng quan trọng như nhận diện giọng nói, chuyển giọng nói thành văn bản, hoặc thậm chí là tạo chú thích cho video.

Trước khi đi đến giải thích cách hoạt động của LSTM's và GRU's, mình cùng nhau test một số chứng năng của bộ não nhé. Trước tiên, bạn hãy đọc dòng bình luận về sản phẩm ngũ cốc và cố xác định xem bình luận đó là khen hay chê sản phẩm.

![alt text](https://res.cloudinary.com/dzwwhbt1i/image/upload/v1569866520/1_YHjfAgozQaghcsEvsBEu2g_pltqcs.png "comment")

Khi bạn đọc bình luận trên, bộ não của bạn chỉ nhớ các từ khóa quan trọng. Bạn nhớ những từ như "amazing" và "perfectly balanced breakfast", và bạn không quan tâm những từ như "this" "gave" "all" "should". Nếu vài giờ nữa, một người bạn hỏi bạn về nội dung bài đánh giá, thì bạn không thể nhớ toàn bộ từng chữ, bạn chỉ có thể nhớ những nội dung của nó.

![alt text](https://res.cloudinary.com/dzwwhbt1i/image/upload/v1569866519/1_ygAgowqTZjR6ABzZHd8Bqg_qonlu2.gif "gif")

Và đây cũng chính là cách hoạt động của LSTM và GRU. Hai mạng này có thể học và giữ lại những thông tin quan trọng và sử dụng những thông tin đó trong việc dự đoán. 

### Nhắc lại cách hoạt động của RNN's

Để hiểu cách hoạt động của LSTM's và GRU's thì chúng ta phải hiểu RNN's trước, vì LSTM's là một cải tiến của RNN mà thôi. 

Đầu tiên, các từ sẽ được chuyển đổi sang vector để computer có thể hiểu được (Embedding, bạn có thể đọc một số kỹ thuật embedding tại **đây**). Sau đó RNN sẽ xử lý từng vector một.

![alt text](https://res.cloudinary.com/dzwwhbt1i/image/upload/v1569866518/1_AQ52bwW55GsJt6HTxPDuMA_omgiex.gif "gif")
*Xử lý từng vector một*

Trong khi xử lý, nó sẽ chuyển các hidden state cho bước tiếp theo, hidden state hoạt động giống như một bộ nhớ, giúp cho dữ liệu trước đó được giữ lại.

![alt text](https://res.cloudinary.com/dzwwhbt1i/image/upload/v1569866519/1_o-Cq5U8-tfa1_ve2Pf3nfg_zulbzz.gif "gif")
*Chuyển hidden state sang bước tiếp theo*

Hãy nhìn vào cell trong RNN để thấy cách chúng ta có thể tính hidden state. Đầu tiên, vector biểu diễn của từ và hidden state trước sẽ được kết hợp lại thành một vector, vector này sẽ chứa những thông tin cần thiết và tiếp tục đi qua hàm Tanh activation, và output là một hidden state mới

![alt text](https://res.cloudinary.com/dzwwhbt1i/image/upload/v1569866519/1_WMnFSJHzOloFlJHU6fVN-g_iq0phl.gif "gif")
*RNN Cell*

#### Tanh activation

Hàm Tanh activation được sử dụng để có thể điều chỉnh giá trị về khoảng -1 đến 1.

![alt text](https://res.cloudinary.com/dzwwhbt1i/image/upload/v1569866518/1_iRlEg1GBKRzGTre5aOQUCg_skzuao.gif "tanh activation")

Vậy tại sao phải sử dụng Tanh activation. Hãy tưởng tượng nếu một vector đi qua một neral network, nó sẽ trải qua nhiều biến đổi, khi đi qua nhiều mạng neural network, thì một số dữ liệu sẽ rất lớn, khiến cho các giá trị khác dường như không đáng kể

![alt text](https://res.cloudinary.com/dzwwhbt1i/image/upload/v1569866518/1_LgbEFcGiUpseZ--M7wuZhg_fmihaz.gif "tanh activation")
*Khi không sử dụng hàm Tanh*

Và hàm Tanh đảm bảo rằng các giá trị đó luôn luôn nằm trong khoảng từ -1 đến 1.

![alt text](https://res.cloudinary.com/dzwwhbt1i/image/upload/v1569866518/1_gFC2bTg3uihp1klknWU0qg_v0zrhw.gif "tanh activation")
*Khi sử dụng hàm Tanh*

Đây chính là hoạt động của RNN, nó rất phù hợp với những chuỗi dạng ngắn, và sử dụng ít tài nguyên hơn nhiều so với các biến thể của nó như LSTM và GRU

### LSTM

Một cell LSTM có một luồng điều khiển tương tự như một cell RNN, nó xử lý dữ liệu rồi truyền thông tin về phía trước. Sự khác biệt của LSTM là quá trình xử lý bên trong của cell.

![alt text](https://res.cloudinary.com/dzwwhbt1i/image/upload/v1569866517/1_0f8r3Vd-i4ueYND1CUrhMA_bzafkt.png "tanh activation")

Các hoạt động trong cell của LSTM cho phép các thông tin được lưu trữ, bây giờ mình sẽ đi từng bước giải thích cách hoạt động của từng thành phần trong cell LSTM

#### Ý tưởng chính

Ý tưởng LSTM sẽ dùng cell state, và một số cổng khác nhau. Cell state hoạt động giống như một đường cao tốc vận chuyển thông tin, các thông tin khi qua các cổng sẽ được loại bỏ hoặc giữ lại và tiếp tục cập nhập lên cell state, cell state sẽ cùng với embedding vector kế tiếp làm input cho cell tiếp theo, chính vì thế nó có thể mang những thông tin từ cell này qua cell khác.

#### Sigmoid

Các cổng sử dụng hàm Sigmoid activations. Hàm sigmoid gần giống với hàm tanh, thay vì scale dữ liệu về khoảng từ -1 đến 1 thì hàm sigmoid scale dữ liệu về khoảng 0 dến 1, điều này thực sự hữu ích cho việc loại bỏ dữ liệu vì nếu dữ liệu càng mang ít thông tin thì nó càng gần về 0, khi qua hàm sigmoid thì dữ liệu rất nhỏ, và dễ bị loại bỏ. 

![alt text](https://res.cloudinary.com/dzwwhbt1i/image/upload/v1569866520/1_rOFozAke2DX5BmsX2ubovw_aoeqxz.gif "tanh activation")

#### Forget gate

Đầu tiên chính là cổng forget, đây là công quyết định dữ liệu nào được giữ lại hoặc bị vứt bỏ. Thông tin từ hidden state trước đó sẽ kết hợp với dữ liệu input đầu vào, rồi chúng sẽ đi qua hàm sigmoid theo công thức. 

$$f_t = \sigma(W_f \cdot [h_{t - 1}, x_t] + b_f)$$

![alt text](https://res.cloudinary.com/dzwwhbt1i/image/upload/v1569866518/1_GjehOa513_BgpDDP6Vkw2Q_gp0huw.gif "tanh activation")

#### Input Gate

Bước tiếp theo là chúng ta sẽ quyết định những thông tin nào sẽ được lưu trữ trong cell state. Quá trình này có 2 phần: 
- Đầu tiên, một lớp sigmoid được gọi là 'input gate layer' quyết định giá trị nào sẽ được cập nhật. Tiếp theo, một lớp Tanh activation sẽ tạo ra một vector gồm những giá trị tìm năng mới mà có thể được thêm vào cell state. 
- Cuối dùng là combine 2 vector đó lại để có thể cập nhật vào cell state.

$$ i_t = \sigma(W_i \cdot [h_{t - 1}, x_t] + b_i) \\
\tilde{C}_t = \tanh(W_C \cdot [h_{t - 1}, x_t] + b_C)
$$
![alt text](https://res.cloudinary.com/dzwwhbt1i/image/upload/v1569866521/1_TTmYy7Sy8uUXxUXfzmoKbA_gaykpb.gif "tanh activation")

#### Cell State

Bây giờ chúng ta nên có đủ thông tin để tính toán cell state. Đầu tiên, cell state được nhân theo chiều của forget vector. Điều này sẽ dẫn đến một số dữ liệu sẽ bị mất đi nếu nó được nhân với các giá trị gần 0. Sau đó, mình sẽ lấy đầu ra từ cổng input và thực hiện bổ sung, cập nhật cell state thành các giá trị mới mà mạng neural thấy có liên quan. Điều đó cho chúng ta một cell state mới.

$$C_t = f_t * C_{t - 1} + i_t * \tilde{C}_t$$


![alt text](https://res.cloudinary.com/dzwwhbt1i/image/upload/v1569866519/1_S0rXIeO_VoUVOyrYHckUWg_on8dwa.gif "tanh activation")

#### Output Gate

Cuối cùng chúng ta có cổng output, cổng này sẽ quyết định thông tin nào của cell state sẽ được xuất ra.
- Đầu tiên chúng ta đưa dữ liệu qua một hàm sigmoid để lọc.
- Tiếp theo đưa cell state mới qua một hàm Tanh.
- Nhận 2 vector nhận được lại với nhau, ta được vector output đã được lọc
$$
o_t = \sigma(W_o [h_{t - 1}, x_t] + b_o) \\
h_t = o_t * \tanh(C_t)
$$

![alt text](https://res.cloudinary.com/dzwwhbt1i/image/upload/v1569866519/1_VOXRGhOShoWWks6ouoDN3Q_dyfifs.gif "tanh activation")

#### Code demo

```python
#single lstm cell
def lstm_cell(batch_dataset, prev_activation_matrix, prev_cell_matrix, parameters):
    #get parameters
    fgw = parameters['fgw']
    igw = parameters['igw']
    ogw = parameters['ogw']
    ggw = parameters['ggw']
    
    #concat batch data and prev_activation matrix
    concat_dataset = np.concatenate((batch_dataset,prev_activation_matrix),axis=1)
    
    #forget gate activations
    fa = np.matmul(concat_dataset,fgw)
    fa = sigmoid(fa)
    
    #input gate activations
    ia = np.matmul(concat_dataset,igw)
    ia = sigmoid(ia)
    
    #output gate activations
    oa = np.matmul(concat_dataset,ogw)
    oa = sigmoid(oa)
    
    #gate gate activations
    ga = np.matmul(concat_dataset,ggw)
    ga = tanh_activation(ga)
    
    #new cell memory matrix
    cell_memory_matrix = np.multiply(fa,prev_cell_matrix) + np.multiply(ia,ga)
    
    #current activation matrix
    activation_matrix = np.multiply(oa, tanh_activation(cell_memory_matrix))
    
    #lets store the activations to be used in back prop
    lstm_activations = dict()
    lstm_activations['fa'] = fa
    lstm_activations['ia'] = ia
    lstm_activations['oa'] = oa
    lstm_activations['ga'] = ga
    
    return lstm_activations,cell_memory_matrix,activation_matrix
```


### GRU

Chúng ta đã biết một LSTM hoạt động như thế nào, một biến thể khác của LSTM là GRU với ít cổng hơn, vì thế tốc độ tính toán, train khi sử dụng GRU cũng nhanh hơn nhiều so với LSTM. GRU không sử dụng cell state mà sử dụng hidden state để vận chuyển thông tin. GRU có 2 cổng, cổng reset và cổng update.

![alt text](https://res.cloudinary.com/dzwwhbt1i/image/upload/v1569866518/1_jhi5uOm9PvZfmxvfaCektw_zjz2hc.png "tanh activation")

#### Update gate

Cổng update hoạt động tương tự như cổng forget và cổng input của LSTM. Nó quyết định những thông tin cần vứt bỏ và những thông tin mới để thêm.

#### Reset gate

Cổng reset là một cổng khác được sử dụng để quyết định quên bao nhiêu thông tin trong quá khứ.


### Tổng kết

Tóm lại, RNN rất tốt để xử lý dữ liệu chuỗi cho các dự đoán nhưng bị bộ nhớ ngắn hạn. LSTM và GRU được tạo ra như một phương pháp để khắc phục bộ nhớ ngắn hạn bằng cách sử dụng các cơ chế gọi là cổng. Cổng  chỉ là mạng lưới thần kinh điều chỉnh luồng thông tin chảy qua chuỗi. LSTM và GRU, được sử dụng trong các ứng dụng Deep learning hiện đại như nhận dạng giọng nói, tổng hợp giọng nói, hiểu ngôn ngữ tự nhiên, v.v.





#### Tài liệu tham khảo

[1]: https://towardsdatascience.com/illustrated-guide-to-lstms-and-gru-s-a-step-by-step-explanation-44e9eb85bf21	"Illustrated guide to LSTM and GRU"

