---
date: 2019-08-05
layout: post
title: Discrete Distribution - Multinomial Distribution
description: >-
  Bài viết này sẽ giới thiệu về Phân phối Multinomial
image: >-
  https://res.cloudinary.com/dzwwhbt1i/image/upload/c_scale,h_300,w_400/v1569262338/poisson_kecvc9.png
category: distributions
author: levanpon98
paginate: true
---

### 1. Định nghĩa

Multinomial Distribution là phân phối khái quát của Binomial Distribution. Với phân phối Binomial thì chỉ có 2 kết quả nhận được đó là 0 hoặc 1, còn đối với Multinomial thì có nhiều hơn 2 kết quả nhận được. 

Như vậy
- Với số lần thử $$= 1$$ và có 2 kết quả nhận được, ta sẽ dùng phân phối Bernoulli
- Với số lần thử $$> 1$$ và có 2 kết quả nhận được, ta sẽ sử dụng phân phối Binomial 
- Với số lần thử $$> 1$$ và có $$> 2$$ kết quả nhận được, ta sẽ sử dụng phân phối Multinomial

Ta có hàm xác suất:

$$P_N(x_1,x_2, \cdots, x_n) = \frac{N!} {x_1!, x_2!, \cdots,x_n!} p_1^{x_1} p_2^{x_2} \cdots p_n^{x_n}$$


### 2. Tính chất

- Kỳ vọng: \$$\mu_i = Np_i$$
- Phương sai: \$$\sigma_i^2 = N p_i (1 - p_i)$$