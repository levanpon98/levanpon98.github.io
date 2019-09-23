---
date: 2019-05-16 23:48:05
layout: post
title: Phân phối rời rạc (Phần 1) - Phân phối Poisson
description: >-
  Bài viết này sẽ giới thiệu về Phân phối Poisson
image: >-
  https://res.cloudinary.com/dzwwhbt1i/image/upload/c_scale,h_300,w_400/v1569008243/1200px-Normal_Distribution_PDF.svg_w2r9gl.png
category: distributions
tags:
  - probability
  - statistics
  - distributions
author: levanpon
paginate: true
---

### 1. Định nghĩa

Phân phối Poisson là một phân phối xác suất rời rạc. Nó khác với các phân phối xác suất rời rạc khác ở chỗ thông tin cho biết không phải là xác suất để một sự kiện (event) xảy ra (thành công) trong một lần thử như trong phân phối Bernoulli, hay là số lần mà sự kiện đó xảy ra trong n lần thử như trong phân phối nhị thức, mà chính là trung bình số lần xảy ra thành công của một sự kiện trong một khoảng thời gian nhất định. Giá trị trung bình này được gọi là **lamda**, ký hiệu là $$\displaystyle \lambda$$.

Hàm mật độ của phân phối Poisson có dạng: 

$$
f(x) = 
\begin{cases}
    e^{-\mu} \frac{\mu^x} {x!}      & \quad \text{khi } x = 0,1,...,n,...\\
    0  & \quad \text{khi } x \ne 0,1,...,n,...
  \end{cases}
$$

**Chứng minh công thức:** Cho phân phối Binomial với p là xác suất đạt được chính xác k lần thành công trong N lần thử nghiệm , ta có:

$$
  P_p(k|N) = C_N^k p^k (1 - p)^{N-k} = \frac{N!} {k!(N - k)!} p^k(1-p)^{N-k} 
$$

Với $$\mu = Np$$ không đổi, khi $$N \to \infty$$ ta có

$$
 \begin{array}
  	\lim\limits_{N \to \infty} P &=& \lim\limits_{N \to \infty} \frac{N(N - 1) \cdots (N - k + 1)} {k!} \left(\frac{\mu}{N}\right)^k \left(1 - \frac{\mu}{N}\right)^{N - k} \\
  	&=& \lim\limits_{N \to \infty} \frac{N(N - 1) \cdots (N - k + 1)} {k!} \left(\frac{\mu}{N}\right)^k \left(1 - \frac{\mu}{N}\right)^N \left(1 - \frac{\mu}{N}\right)^{-k} \\
  	&=& \lim\limits_{N \to \infty} \frac{N(N - 1) \cdots (N - k + 1)} {N^k} \frac{\mu^k}{k!} \left(1 - \frac{\mu}{N}\right)^N \left(1 - \frac{\mu}{N}\right)^{-k} \\
  	&=& 1 \times \frac{\mu^k}{k!} \times e^{-\mu} \times 1
  \end{array}
$$

Từ đó suy ra 

$$
	C_N^k p^k (1 - p)^{N-k} \approx e^{-\mu} \frac{\mu^k} {k!}
$$

$$\implies$$ Nếu $$ X \sim B(N;p)$$, trong đó p đủ nhỏ và $$N$$ đủ lớn, thì $$X$$ được xem như có phân phối Poisson $$P(\mu)$$, với $$\mu = Np$$

### 2. Ứng dụng

Phân phối Poisson được áp dụng cho nhiều hiện tượng (có tính rời rạc) (nghĩa là số lần xuất hiện trong một khoảng (thời gian, không gian) cho trước đó phải là số nguyên 0, 1, 2, 3,...) với xác suất để sự kiện (hiện tượng) đó xảy ra là không đổi trong suốt khoảng (thời gian, không gian) đó.

Các ví dụ sau đây được mô hình theo phân phối Poisson:
- Số lượng xe hơi đi ngang qua 1 điểm trên con đường trong một khoảng thời gian cho trước.
- Số lần gõ bị sai của khi đánh máy một trang giấy.
- Số cuộc điện thoại tại một trạm điện thoại trong mỗi phút.
- Số lần truy cập vào một máy chủ web trong mỗi phút.
- Số lần động vật bị chết do xe cộ cán phải trên mỗi đơn vị độ dài của một con đường.
- Số lần đột biến xảy ra trên một đoạn DNA sau khi chịu một lượng bức xạ..
- Số lượng cây thông trên mỗi đơn vị diện tích rừng hỗn hợp.
- Số lượng ngôi sao trong một thể tích không gian vũ trụ.
- Số lượng người lính bị chết do ngựa đá mỗi năm trông mỗi đội của kị binh Phổ. Ví dụ này rất nổi tiếng trong cuốn sách của Ladislaus Josephovich Bortkiewicz (1868–1931).
- Phân phối của các tế bào cảm quang trong võng mạc của mắt.
- Số lượng bóng đèn bị cháy trong một khoảng thời gian xác định.
- Số lượng virut có thể lây nhiễm lên một tế bào trong cấu trúc tế bào.
- Số lưộng phát minh của một nhà sáng chế trong suốt cuộc đời của họ.