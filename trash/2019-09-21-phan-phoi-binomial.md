---
date: 2019-08-07
layout: post
title: Discrete Distribution - Binomial Distribution
description: >-
  Bài viết này sẽ giới thiệu về Phân phối Binomial
image: >-
  https://res.cloudinary.com/dzwwhbt1i/image/upload/c_scale,h_300,w_400/v1569262338/poisson_kecvc9.png
category: distributions
author: levanpon98
paginate: true
---

### 1. Định nghĩa

Phân phối Binomial $$X \sim Bin(n, p)$$ là phân phối rời rạc cho biết xác suất xảy ra đúng $$n$$ lần trong $$N$$ lần thử nghiệm (trong đó chỉ có 2 giá trị nhận được là 1 và 0, xác suất đạt được 1 là $$p$$, 0 là $$q = 1 - p$$). Từ đó ta có công thức:

$$P_p(n|N) = \left(
    \begin{array}
      \mathrm{N} \\
      n
    \end{array}
    \right) p^n (1 - p)^{N - n} $$

Trong đó $$\left(
    \begin{array}
      \mathrm{N} \\
      n
    \end{array}
    \right)$$ được gọi là hệ số Binomial. Như vậy ta thấy phép thử Bernoulli được coi là một trường hợp đặt biệt của phân phối Binomial với $$n = 1$$, nên phân phối Bernoulli có thể được ký hiệu là $$X \sim Bin(1, p)$$

### 2. Tính chất

- Kỳ vọng: \$$\mu = Np$$
- Phương sai: \$$\sigma^2 = Np(1 - p)$$
- Hệ số đối xứng: \$$\gamma_1 = \frac{1- 2p} {\sqrt{N p (1 - p)}}$$
- Hệ số nhọn: \$$\gamma_2 = \frac{6p^2 -6p + 1} {N p (1 - p)}$$