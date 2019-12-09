---
title: 'Hiểu sâu hơn về mô hình Attention với bài toán Translate'
date: 2019-12-10
permalink: /posts/2019/12/attention/
tags:
  - nlp
---

Ở bài trước, chúng mình cùng tìm hiểu về mô hình Sequence-To-Sequence. Ngoài những thành công mà mô hình này đem lại trong các bài toán về translation, text sumarization, ..., thì mô hình này vẫn còn nhiều vấn đề, đặc biệt là vấn đề về khả năng đóng gói thông tin, ngữ nghĩa của một câu có thể bị mất nếu câu đó quá dài. Lúc này mô hình attention được sinh ra để giải quyết vấn đề nêu trên. Mình hy vọng qua bài này, các bạn có thể hiểu hơn về mô hình Attention và xem đây như là một tư liệu trong hành trình học tập của mình.

**Note**: Những hình ảnh động bên dưới là video, các bạn có thể dừng video lại để có thể ngồi ngẫm nghĩ quá trình tính toán xảy ra như thế nào nhé.





**Tài liệu tham khảo**

- [https://medium.com/analytics-vidhya/intuitive-understanding-of-seq2seq-model-attention-mechanism-in-deep-learning-1c1c24aace1e](https://medium.com/analytics-vidhya/intuitive-understanding-of-seq2seq-model-attention-mechanism-in-deep-learning-1c1c24aace1e)
- [http://jalammar.github.io/visualizing-neural-machine-translation-mechanics-of-seq2seq-models-with-attention/](http://jalammar.github.io/visualizing-neural-machine-translation-mechanics-of-seq2seq-models-with-attention/)

