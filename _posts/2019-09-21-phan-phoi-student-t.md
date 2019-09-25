---
date: 2019-05-16 23:48:05
layout: post
title: Continuous Distributions  - Student's t Distribution
description: >-
  Bài viết này sẽ giới thiệu về Student's t Distribution
image: >-
  https://res.cloudinary.com/dzwwhbt1i/image/upload/c_scale,h_300,w_400/v1569008243/1200px-Normal_Distribution_PDF.svg_w2r9gl.png
category: distributions
author: levanpon98
paginate: true
---

### 1. Định nghĩa Student's t Distribution

Phân phối Student't s là phân phối liên tục và trông gần giống với Normal Distribution, tuy nhiên ngắn hơn và "béo" hơn, nghĩa là có nhiều giá trị phân bố xa giá trị trung bình hơn phân phối chuẩn. Thường được sử dụng thay cho Normal Distribution khi số lượng mẫu nhỏ hoặc khi chưa biết độ lệch chuẩn. 

Hàm mật độ:

$$
 \begin{array}
 	f(x) &=& \frac{\Gamma[\frac{1}{2} (r + 1)]} {\sqrt{r\pi} \Gamma(\frac{r} {2}) \left(\frac{r + r^2} {r}\right)^{\frac{r + 1}{2}}} \\
 	&=& \frac{ \Gamma[\frac{r} {2} + \frac{1} {2}] \times \Gamma(\frac{1} {2})} {\sqrt{r\pi} \Gamma(\frac{r} {2}) \Gamma(\frac{1} {2}) \left(\frac{r + r^2} {r}\right)^{\frac{r + 1}{2}} } \\
 	&=& \frac{\Gamma(\frac{1} {2}) \left(\frac{r} {r + r^2}\right)^{\frac{r + 1}{2}} } {\sqrt{r\pi} B(\frac{r} {2}, \frac{1} {2})} \\
 	&=& \frac{\Gamma(\frac{1} {2})} {\sqrt{r} B(\frac{r} {2}, \frac{1} {2})}
  \end{array}
$$