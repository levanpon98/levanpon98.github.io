---
date: 2019-10-01 00:16:10
layout: post
title: LSTM's và GRU's 
description: >-
  Bài 
image: >-
  https://res.cloudinary.com/dzwwhbt1i/image/upload/c_scale,h_300,w_400/v1569863989/lstm_n5dznh.png
category: nlp
author: levanpon98
paginate: true
---

Trong bài viết này, mình sẽ giải thích cơ chế hoạt động của LSTM's và GRU's. Nếu bạn thực sự muốn hiểu cụ thể về 2 networks nổi tiếng thì đây chính là nơi bạn đang tìm.

![alt text](https://res.cloudinary.com/dzwwhbt1i/image/upload/v1569869055/1_n-IgHZM5baBUjq0T7RYDBw_tpxeja.gif "LSTM")


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

