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

Cùng nhắc lại mô hình seq2seq truyền thống, các hidden state trung gian sẽ bị loại bỏ và chỉ giữ lại hidden state của layer cuối cùng. Đây chính là nguyên nhân chính dẫn đến mô hình seq2seq không thích hợp với những câu dài. Điều nãy đã được khắc phục trong Attention, khi mà các hidden state của tất cả các layer sẽ được gộp lại thành 1 context vector. Hình động bên dưới sẽ mô tả sơ về hoạt động của Attention trước khi đi sâu vào mô hình.

<video width="100%" height="auto" loop="" autoplay="" controls="">
   <source src="/images/seq2seq_7.mp4" type="video/mp4">
   Your browser does not support the video tag.
</video>

Mình sẽ chia quá trình tính toán của Attention ra làm 5 bước.

**Bước 1:** **Tính score của mỗi encoder hidden state**

Khi chúng ta predict từ đầu tiên, bộ decoder không có bất kỳ hidden state nội bộ nào nên chúng ta sẽ xem hidden state cuối cùng của bộ encoder như là previous hidden state của bộ decoder.

Như đã bàn luận về ý tưởng của Attention, khi predict ra một từ, chúng ta không cần toàn bộ encoder state. Vì thế, trong  những hidden state mà bộ encoder đưa vào, chúng ta cần phải lọc ra những hidden state nào cần thiết. Một cách đơn giản là chúng ta tính toán điểm số của từng hidden state. 

**Vậy làm sao để tính được điểm số của từng hidden state?**

Lúc này chúng ta sẽ sử dụng 2 phần (toàn bộ các encoder states và previous hidden state của bộ decoder), và chúng ta sẽ train một mô hình feed forward network đơn giản để tính score cho mỗi encoder states.

Theo ví dụ ở trên, chúng ta sẽ tính được score $e_1, e_2, e_3$ tương ứng với các hidden state $h_1, h_2, h_3$. 

**Bước 2: Tính trọng số attention**

Khi score đã được sinh ra từ  $h_1, h_2, h_3$, chúng ta sẽ đưa các score này vào hàm softmax để tính ra weight attention $\alpha_1, \alpha_2, \alpha_3$. Khi chúng ta sử dụng hàm softmax sẽ có một số ưu điểm như sau

- Toàn bộ các trọng số sẽ nằm trong khoản từ 0 đến 1 
- Tổng của các trọng số bằng 1

Do đó, chúng ta sẽ có một xác suất đẹp cho các attention weights

**Bước 3: Tính context vector**

Khi đã tính xong attention weights, chúng ta cần phải tính context vector. Ở bước này, chúng ta sẽ nhân các hidden state của bộ encoder với attention weight tương ứng

Ví dụ: $\text{context vector} =  \alpha_1 * h_1 + \alpha_2 * h_2 + \alpha_2 * h_2$

Dễ dàng nhìn thấy, nếu $\alpha_1$ lớn thì $h_1$ sẽ càng được chú ý, và từ được predict ra sẽ mang thông tin của $h_1$ nhiều hơn.

**Bước 4: Kết hợp context vector với output trước đó**

Cuối cùng, bộ decoder sử dụng hai vectơ đầu vào bên dưới để tạo từ tiếp theo trong chuỗi

- Context vector
- Vector word được predict ra trước đó

Chúng ta chỉ cần ghép hai vectơ này, sau đó đưa vào một feed forward network (mô hình này sẽ được đào tạo chung) để tạo ra một vecto hợp nhất, sau đó đưa vectơ hợp nhất vào bộ decoder. Lưu ý rằng đối với bước đầu tiên, vì không có đầu ra trước đó, chúng ta sẽ sử dụng mã thông báo < END >.

**Bước 5: Output**

Lúc này bộ decoder sẽ sinh ra từ tiếp theo của chuỗi và hidden state để sử dụng cho việc tính score tiếp theo.

<video width="100%" height="auto" loop="" autoplay="" controls="" __idm_id__="522540035">
   <source src="/images/attention_tensor_dance.mp4" type="video/mp4">
   Your browser does not support the video tag.
</video>

Đây là một cách khác để xem phần nào của câu đầu vào mà chúng ta chú ý đến ở mỗi bước decoder:

<video width="100%" height="auto" loop="" autoplay="" controls="">
  <source src="/images/seq2seq_9.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

## Các loại Attention



## Code Demo



## Kết luận



## Tài liệu tham khảo

- [http://jalammar.github.io/visualizing-neural-machine-translation-mechanics-of-seq2seq-models-with-attention/](http://jalammar.github.io/visualizing-neural-machine-translation-mechanics-of-seq2seq-models-with-attention/)
- [https://towardsdatascience.com/intuitive-understanding-of-attention-mechanism-in-deep-learning-6c9482aecf4f] (https://towardsdatascience.com/intuitive-understanding-of-attention-mechanism-in-deep-learning-6c9482aecf4f)
- [https://arxiv.org/abs/1409.0473] (https://arxiv.org/abs/1409.0473)
- [https://medium.com/@shashank7.iitd/understanding-attention-mechanism-35ff53fc328e] (https://medium.com/@shashank7.iitd/understanding-attention-mechanism-35ff53fc328e)
- [https://blog.floydhub.com/attention-mechanism/] (https://blog.floydhub.com/attention-mechanism/)

