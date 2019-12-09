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

Mình sẽ chia quá trình tính toán của Attention ra làm 5 bước.

**Bước 1:**



## Các loại Attention



## Code Demo



## Kết luận



## Tài liệu tham khảo

- [https://blog.floydhub.com/attention-mechanism/](https://blog.floydhub.com/attention-mechanism/)
- [http://jalammar.github.io/visualizing-neural-machine-translation-mechanics-of-seq2seq-models-with-attention/](http://jalammar.github.io/visualizing-neural-machine-translation-mechanics-of-seq2seq-models-with-attention/)

