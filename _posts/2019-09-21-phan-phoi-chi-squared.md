---
date: 2019-05-16 23:48:05
layout: post
title: Continuous Distributions  - Chi-Squared Distribution
description: >-
  Bài viết này sẽ giới thiệu về Student's t Distribution
image: >-
  https://res.cloudinary.com/dzwwhbt1i/image/upload/c_scale,h_300,w_400/v1569008243/1200px-Normal_Distribution_PDF.svg_w2r9gl.png
category: distributions
author: levanpon98
paginate: true
---

Phân phối Chi-Squared là phân phối của tổng bình phương độ lệch chuẩn với tham số $$r$$ là degree of freedom (tạm dịch: Bậc tự do). Phân phối Chi-Squared là một trường hợp đặc biệt của phân phối Gamma và là một trong những phân phối được sử dụng phổ biến nhất trong xác suất thống kê, đặc biệt là trong hypothesis testing và confidence intervals. 

#### 1. Phân phối Gamma

Trước hết, ta xét phân phối Gamma với định nghĩa hàm Gamma $$\Gamma : (0, \infty) \to \mathbb{R}, $$

$$\Gamma(x) = \int_{0}^{\infty} t^{x - 1} e^{-t}$$

Biến ngẫu nhiên X gọi là có phân phối *Gamma*, ký hiệu $$X \sim \Gamma(\alpha, \beta),$$ với $$\alpha, \beta > 0, $$ nếu hàm mật độ xác suất của X là 

$$ f(x) =
   \begin{cases}
   	 \frac{1} {\Gamma(\alpha) \beta^{\alpha}} x^{\alpha - 1}e^{\frac{-x} {\beta}}     & \quad \text{khi } x > 0\\
     0  & \quad \text{khi } x \le 0
   \end{cases}
$$

Trong đó
- Kỳ vọng: $$\mu_x = \alpha \beta$$
- Phương sai: $$\sigma_x^2 = \alpha \beta^2$$

#### 2. Phân phối Chi-Squared

Biến ngẫu nhiên X gọi là phân phối Chi-Squared nếu hàm mật độ xác suất của X là:

$$ f(x) =
   \begin{cases}
   	 \frac{1} {\Gamma(\frac{r} {2}) 2^{\frac{r}{2}}} r^{\frac{r}{2}} e^{\frac{-x}{2}}    & \quad \text{khi } x > 0\\
     0  & \quad \text{khi } x \le 0
   \end{cases}
$$

nghĩa là $$X \sim \Gamma(\frac{r} {2}, 2)$$, trong đó r là degree of freedom (tạm dịch: Bậc tự do)

Trong đó
- Kỳ vọng: $$\mu_x = r$$
- Phương sai: $$\sigma_x^2 = 2r$$