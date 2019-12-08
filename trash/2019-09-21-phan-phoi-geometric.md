---
date: 2019-08-07
layout: post
title: Discrete Distribution - Geometric Distribution
description: >-
  Bài viết này sẽ giới thiệu về Phân phối Geometric
image: >-
  https://res.cloudinary.com/dzwwhbt1i/image/upload/c_scale,h_300,w_400/v1569262338/poisson_kecvc9.png
category: distributions
author: levanpon98
paginate: true
---

### 1. Định nghĩa

Phân phối Geometric $$X \sim Geo(p)$$ là phân phối xác suất rời rạc cho biết xác suất suất hiện lần đầu tiên của sự kiện $$A$$ trong phép thử Bernoulli. $$p$$ là xác suất của sự kiện $$A$$ trong mỗi phép thử, với $$0 < p < 1$$.

Hàm mật độ xác suất:

$$f(x) = p(1 - p)^x$$

Hàm phân phối tích lũy: 

$$F(x;p) = 1 - (1 - p)^{x + 1}$$

### 2. Tính chất

- Kỳ vọng: \$$\mu = \frac{1 - p} {p}$$
- Phương sai: \$$\sigma^2 = \frac{1 - p} {p^2}$$
- Hệ số đối xứng: \$$\gamma_1 = \frac{2 - p} {\sqrt{(1 - p)}}$$
- Hệ số nhọn: \$$\gamma_2 = \frac{p^2 -6p + 6} {1 - p}$$