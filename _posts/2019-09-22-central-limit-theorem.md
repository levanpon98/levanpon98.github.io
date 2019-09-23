---
date: 2019-09-22 00:16:10
layout: post
title: Limit Theorem (Phần 1) - Central Limit Theorem
description: >-
  Bài viết này sẽ giới thiệu về Central Limit Theorem
image: >-
  https://res.cloudinary.com/dzwwhbt1i/image/upload/c_scale,h_300,w_400/v1569224466/limit_theorems_mkcxcz.png
category: limittheorems
tags:
  - probability
  - statistics
  - limittheorems
author: levanpon
paginate: true
---

### 1. Định nghĩa

Định lí Central limit theorem (tạm dịch: Định lí giới hạn trung tâm) phát biểu rằng tổng và số bình quân của một tập hợp các biến ngẫu nhiên tuân theo phân phối chuẩn, khi mẫu được chọn có quy mô đủ lớn.

Trong xác suất, định lý giới hạn trung tâm rất nổi tiếng và có vai trò quan trọng. Nó là kết quả về sự hội tụ yếu của một dãy các biến ngẫu nhiên. Với định lý này, ta có kết quả là tổng của các biến ngẫu nhiên độc lập và phân phối đồng nhất theo cùng một phân phối xác suất, sẽ hội tụ về một biến ngẫu nhiên nào đó.

### 2. Chứng minh

Đặt $$X_1, X_2, ... X_N$$ là tập hợp $$N$$ biến ngẫu nhiên độc lập với mỗi $$X_i$$ có phân phối xác suất tùy ý là $$P(X_1, X_2,...,X_N)$$ nhận giá trị kỳ vọng là $$\mu_i$$ và phương sai là $$\sigma_i^2$$. 

$$ \text{Xét tổng } S_N = X_1 + X_2 + ... + X_N$$

Theo như ta thấy từ công thức trên, tổng của các biến ngẫu nhiên sẽ tăng một cách vô định khi số biến ngẫu nhiên tăng. Do đó để có một kết quả hữu hạn, ta hạn chế sự tăng của tổng bằng cách lấy tổng trừ đi giá trị trung bình và rút gọn bằng cách chia cho căn bậc 2 của phương sai. Khi đó ta có phương trình.

$$X_{norm} = \frac{\sum_{i=1}^{N} x_i - \sum_{i=1}^{N} \mu_i} {\sqrt{\sum_{i=1}^{N} \sigma_i^2}}$$

Có hàm phân phối xác suất hội tụ về phân phối chuẩn.

Dưới một số điều kiện, thì hàm mật độ xác suất của $$X_{norm}$$ cũng là một normal với mean $$\mu = 1$$ và variance $$\sigma^2 = 1$$. Khi đó 

$$X \equiv \frac{1} {N} \displaystyle\sum_{i=1}^{N} x_i$$

cũng là một Phân phối chuẩn với $$\mu_X = \mu_x$$ và $$\sigma_X = \frac{\sigma_x} {\sqrt{N}}$$

Áp dụng biến đổi Fourier ngược với $$P_X(f)$$

$$
  \begin{array}
    \mathcal{F}_f^{-1}[P_X(f)](x) &=& \int_{-\infty}^{\infty} e^{2\pi i f X}P(X)d X \\
    &=& \int_{-\infty}^{\infty} \displaystyle\sum_{n=0}^{\infty} \frac{(2\pi if X)^n} {n!} P(X) d X \\
    &=& \displaystyle\sum_{n=0}^{\infty} \frac{(2\pi if)^n} {n!} \int_{-\infty}^{\infty} X^n P(X) d X \\
    &=& \displaystyle\sum_{n=0}^{\infty} \frac{(2\pi if)^n} {n!} \langle X^n \rangle
  \end {array}
$$

Ta có: 

$$ 
  \begin{array}
    \langle X^n \rangle &=& \left\langle \frac{1} {N} \displaystyle\sum_{i=1}^{N} x_i \right\rangle \\
    &=& \int_{-\infty}^{\infty} N^{-n}(x_1 + \cdots + x_N)^{n}P(x_1)\cdots P(x_N)d_{x_1}\cdots d_{x_N}
  \end {array}
$$

Vì vậy ta có:

$$
  \begin{array}
    \mathcal{F}_f^{-1}[P_X(f)](x) &=& \displaystyle\sum_{n=0}^{\infty} \frac{(2\pi if)^n} {n!} \langle X^n \rangle \\
    &=& \displaystyle\sum_{n=0}^{\infty} \frac{(2\pi if)^n} {n!} \int_{-\infty}^{\infty} N^{-n}(x_1 + \cdots + x_N)^{n} \times P(x_1)\cdots P(x_N)d_{x_1}\cdots d_{x_N} \\
    &=& \int_{-\infty}^{\infty} \displaystyle\sum_{n=0}^{\infty} \left[  \frac{2\pi if(x_1 + \cdots + x_n)} {N} \right]^{n} \frac{1} {n!}P(x_1)\cdots P(x_N)d_{x_1}\cdots d_{x_N} \\
    &=& \int_{-\infty}^{\infty} e^{ \frac{2\pi if(x_1 + \cdots + x_n)} {N}} P(x_1)\cdots P(x_N)d_{x_1}\cdots d_{x_N} \\
    &=& \left[\int_{-\infty}^{\infty} e^{ \frac{2\pi if(x_1)} {N}} P(x_1)d_{x_1}\right] \times \cdots \times \left[\int_{-\infty}^{\infty} e^{ \frac{2\pi if(x_n)} {N}} P(x_N)d_{x_N}\right] \\
    &=& \left[\int_{-\infty}^{\infty} e^{ \frac{2\pi if(x_N)} {N}} P(x)d_{x}\right]^{N} \\
    &=& \left\{ \int_{-\infty}^{\infty} \left[1 + \left(\frac{2\pi if} {N}\right)x + \frac{1} {2} \left(\frac{2\pi if} {N}\right)^{2}x^{2} + \cdots \right] P(x)d_{x}\right\}^{N} \\
    &=& \left[1 + \frac{2\pi i f} {N} \langle x \rangle - \frac{(2\pi f)^2} {2N^2} \langle x^2 \rangle + O(N^{-3})  \right]^{N} \\
    &=& exp \left\{ N \times ln\left[1 + \frac{2\pi i f} {N} \langle x \rangle - \frac{(2\pi f)^2} {2N^2} \langle x^2 \rangle + O(N^{-3}) \right]\right\}
  \end {array}

$$

Mà 

$$
ln(1 + x) = x - \frac{1} {2}x^2 + \frac{1} {3}x^3 + \cdots,
$$

Vì thế 

$$
  \begin{array}
    \mathcal{F}_f^{-1}[P_X(f)](x) &\approx & exp \left\{ N \left[\frac{2 \pi i f} {N} \langle x \rangle - \frac{(2\pi f)^2} {2N^2} \langle x^2 \rangle + \frac{1} {2} \frac{(2 \pi f)^2} {N^2} \langle x \rangle^2 + O(N^{-3}) \right]\right\} \\
    &=& exp \left[ 2 \pi i f \langle x \rangle - \frac{(2 \pi f)^2 (\langle x^2 \rangle - \langle x \rangle^2)} {2N} + O(N^{-2})\right] \\
    &\approx & exp \left[2 \pi i f \mu_x - \frac{(2 \pi f)^2 \sigma_x^2} {2N}\right] 
  \end{array}
$$

Trong đó

$$ 
    \mu_x \equiv \langle x \rangle \\
    \sigma_x^2 \equiv  \langle x^2 \rangle - \langle x \rangle^2
  
$$

Lấy biến đổi Fourier

$$
  
  \begin{array}
    \mathrm{P}_X &\equiv & \int_{-\infty}^{\infty} e^{-2 \pi i f x} \mathcal{F}^{-1}[P_X(f)] df \\
    &=& \int_{-\infty}^{\infty} e^{2 \pi i f (\mu_x - x) - \frac{(2 \pi f)^2 \sigma_x^2} {2N}} df
  \end{array}
$$

Ta có:

$$
 \int_{-\infty}^{\infty} e^{i a f - b f^2} df
$$

Trong đó $$a \equiv 2 \pi (\mu_x - x)$$ và $$b \equiv \frac{(2 \pi \sigma_x)^2} {2N}$$. Bởi vì đây là biến đổi Fourier của hàm Gaussian nên:

$$ \int_{-\infty}^{\infty} e^{i a f - b f^2} df = e^{\frac{-a^2} {4b}} \sqrt{\frac{\pi} {b}}$$

Thay vào phương trình $$P_X$$ ta được:

$$
  \begin{array}
    \mathrm{P}_X &=& \sqrt{\frac{\pi} {\frac{(2 \pi f)^2 \sigma_x^2} {2N}}} exp\left\{ \frac{-[2 \pi (\mu_x - x)^2]^2} {4 \frac{(2 \pi f)^2 \sigma_x^2} {2N}}\right\} \\
    &=& \sqrt{\frac{2 \pi N} {4 \pi^2 \sigma_x^2}} exp\left[-\frac{4 \pi^2 (\mu_x - x)^2 2N} {4.4 \pi^2 \sigma_x^2}\right] \\
    &=& \frac{\sqrt{N}} {\sigma_x \sqrt{2 \pi}} e^{-(\mu_x - x)^2 \frac{N} {2\sigma_x^2}}
  \end{array}
$$

Nhưng $$\sigma_X = \frac{\sigma_x} {\sqrt{N}}$$ và $$\mu_X = \mu_x$$, thế vào phương trình trên.

$$
P_X \equiv \frac{1} {\sigma_X \sqrt{2 \pi}} e^{-\frac{(\mu_X -x)^2} {2\sigma_X^2}}
$$

Đến đây ta thấy $$P_X$$ có dạng của hàm phân phối chuẩn
