---
date: 2019-08-07
layout: post
title: Discrete Distribution - Negative Binomial Distribution
description: >-
  Bài viết này sẽ giới thiệu về Phân phối Negative Binomial
image: >-
  https://res.cloudinary.com/dzwwhbt1i/image/upload/c_scale,h_300,w_400/v1569262338/poisson_kecvc9.png
category: distributions
author: levanpon98
paginate: true
---

### 1. Định nghĩa

Phân phối Negative Binomial, hay còn gọi là phân phối Pascal hoặc phân phối Pólya, là phân phối xuất hiện thứ $$r$$ của sự kiện $$A$$ trong phép thử Bernoulli. Có thể nói, phân phối Geometric là trường hợp đặt biệt của phân phối Negative Binomial khi $$r = 1$$. 

Hàm mật độ xác suất: 

$$f(x) = left(\!
    \begin{array}{c}
      x + r - 1 \\
      r - 1
    \end{array}
  \!\right) p^r (1 - p)^x $$

Hàm phân phối tích lũy:

$$F(x;r,p) = \displaystyle\sum_{n=0}^{x} left(\!
    \begin{array}{c}
      x + r - 1 \\
      r - 1
    \end{array}
  \!\right) p^r (1 - p)^x $$

### 2. Tính chất

- Kỳ vọng: \$$\mu = r(1 - p)$$
- Phương sai: \$$\sigma^2 = \frac{r(1 - p)} {p^2}$$
- Hệ số đối xứng: \$$\gamma_1 = \frac{2 -p} {\sqrt{r(1 - p)}}$$
- Hệ số nhọn: \$$\gamma_2 = \frac{p^2 -6p + 6} {r (1 - p)}$$