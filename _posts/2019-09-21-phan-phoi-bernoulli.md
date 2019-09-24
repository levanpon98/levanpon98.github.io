---
date: 2019-08-05
layout: post
title: Discrete Distribution - Bernoulli Distribution
description: >-
  Bài viết này sẽ giới thiệu về Phân phối Bernoulli
image: >-
  https://res.cloudinary.com/dzwwhbt1i/image/upload/c_scale,h_300,w_400/v1569262338/poisson_kecvc9.png
category: distributions
author: levanpon98
paginate: true
---

### 1. Định nghĩa

Phân phối Bernoulli là một phân phối rời rạc của biến ngẫu nhiên chỉ có hai kết quả xảy ra là 0 hoặc 1, trong đó giá trị 1 đạt được với xác suất $$p$$ (thành công) và giá trị 0 đạt được với xác suất $$q = 1 - p$$ (thất bại), $$0 < p < 1$$. Hàm mật độ xác suất của phân phối Bernoulli là:

$$
P(n) = 
 \begin{cases}
      p     & \quad \text{khi } n = 1\\
      1 - p  & \quad \text{khi } n = 0
 \end{cases}
$$

Chúng ta có thể viết lại thành

$$P(n) = p^n(1 - p)^{1 - n}$$

### 2. Tính chất

- Kỳ vọng: \$$\mu = p$$
- Phương sai: \$$\sigma^2 = p(1 - p)$$
- Hệ số đối xứng: \$$\gamma_1 = \frac{1- 2p} {\sqrt{p(1 - p)}}$$
- Hệ số nhọn: \$$\gamma_2 = \frac{6p^2 -6p + 1} {p(1 - p)}$$