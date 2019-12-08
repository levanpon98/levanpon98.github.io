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
comments: true
---

### 1. Định nghĩa Student's t Distribution

Phân phối Student't s là phân phối liên tục và trông gần giống với Normal Distribution, tuy nhiên ngắn hơn và "béo" hơn, nghĩa là có nhiều giá trị phân bố xa giá trị trung bình hơn phân phối chuẩn. Thường được sử dụng thay cho Normal Distribution khi số lượng mẫu nhỏ hoặc khi chưa biết độ lệch chuẩn. 

Hàm mật độ:

$$
 \begin{array}
 	\mathrm{f}(t) &=& \frac{\Gamma[\frac{1}{2} (r + 1)]} {\sqrt{r\pi} \Gamma(\frac{r} {2}) \left(\frac{r + r^2} {r}\right)^{\frac{r + 1}{2}}} \\
 	&=& \frac{ \Gamma[\frac{r} {2} + \frac{1} {2}] \times \Gamma(\frac{1} {2})} {\sqrt{r\pi} \Gamma(\frac{r} {2}) \Gamma(\frac{1} {2}) \left(\frac{r + r^2} {r}\right)^{\frac{r + 1}{2}} } \\
 	&=& \frac{\Gamma(\frac{1} {2}) \left(\frac{r} {r + r^2}\right)^{\frac{r + 1}{2}} } {\sqrt{r\pi} B(\frac{r} {2}, \frac{1} {2})} \\
 	&=& \frac{\Gamma(\frac{1} {2})} {\sqrt{r} B(\frac{r} {2}, \frac{1} {2})}
  \end{array}
$$

### 2. Tính chất

- Kỳ vọng: \$$\mu = 0$$
- Phương sai: \$$\sigma^2 = \frac {r} {r - 2}$$
- Hệ số đối xứng: \$$\gamma_1 = 0$$
- Hệ số nhọn: \$$\gamma_2 = \frac{6} {r - 4}$$

### 3. Ứng dụng 

Phân phối Student được dùng trong thống kê suy luận phương sai tổng thể khi thổng thể được giả thiết là có phân phối chuẩn, đặc biệt khi cỡ mẫu nhỏ. Ngoài ra ta còn dùng phân phối Student trong kiểm định giả thiết về trung bình khi phương sai tổng thể chưa biết,.. 