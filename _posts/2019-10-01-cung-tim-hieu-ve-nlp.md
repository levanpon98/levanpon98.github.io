---
date: 2019-9-28 00:16:10
layout: post
title: Cùng tìm hiểu về NLP
description: >-
  Bài 
image: >-
  https://res.cloudinary.com/dzwwhbt1i/image/upload/c_scale,h_300,w_400/v1569863989/lstm_n5dznh.png
category: nlp
author: levanpon98
paginate: true
---

## 1.Mô hình ngôn ngữ

Mô hình ngôn ngữ là một phân bố xác suất trên các tập văn bản. Nói đơn giản, mô hình ngôn ngữ có thể cho biết xác suất một câu (hoặc cụm từ) thuộc một ngôn ngữ là bao nhiêu. 

Ví dụ: khi áp dụng mô hình ngôn ngữ cho tiếng Việt: 

P[“hôm qua là thứ năm”]  = 0.001 
P[“năm thứ hôm là qua”]  = 0 

Mô hình ngôn ngữ được áp dụng trong rất nhiều lĩnh vực của xử lý ngôn ngữ tự nhiên như: kiểm lỗi chính tả, dịch máy hay phân đoạn từ... Chính vì vậy, nghiên cứu mô hình ngôn ngữ chính là tiền đề để nghiên cứu các lĩnh vực tiếp theo.

Mô hình ngôn ngữ có nhiều hướng tiếp cận, nhưng chủ yếu được xây dựng theo mô hình Ngram.

<script src="https://ideone.com/e.js/yG0rSF" type="text/javascript" ></script>