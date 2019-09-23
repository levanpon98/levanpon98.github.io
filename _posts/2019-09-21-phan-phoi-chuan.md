---
date: 2019-05-16 23:48:05
layout: post
title: Phân phối liên tục (Phần 1) - Phân phối chuẩn
description: >-
  Bài viết này sẽ giới thiệu về Phân phối chuẩn
image: >-
  https://res.cloudinary.com/dzwwhbt1i/image/upload/c_scale,h_300,w_400/v1569008243/1200px-Normal_Distribution_PDF.svg_w2r9gl.png
category: distributions
author: levanpon98
paginate: true
---

### 1. Phân phối chuẩn là gì?

Phân phối chuẩn, còn được gọi là phân phối Gaussian (đối với các nhà vật lý), là phân phối xác suất đối xứng xung quanh giá trị trung bình, nghĩa là dữ liệu gần giá trị trung bình xảy ra thường xuyên hơn so với dữ liệu xa giá trị trung bình. Về hình dạng biểu đồ rất giống với một cái chuông, nên phân phối chuẩn còn được gọi là Bell Curve (đối với các nhà khoa học xã hội).

**Tính chất:** 
- Diện tích khu vực dưới đường cong = 1
- Luôn luôn đối xứng
- mean ($$\mu$$) = median = mode
- Mọi phân phối đều có thể xấp xỉ về phân phối chuẩn nếu tuân theo một tiêu chuẩn nào đó.

### 2. Hàm phân phối xác suất

Phân phối bình thường là loại phân phối phổ biến nhất được giả định trong phân tích thị trường chứng khoán kỹ thuật và trong các loại phân tích thống kê khác. Phân phối chuẩn được đặc trưng bởi hai tham số: giá trị trung bình ($$\mu$$) và độ lệch chuẩn ($$\sigma$$). 

 $$f(x) = \frac{e^{-(x - \mu)^{2}/(2\sigma^{2}) }} {\sigma\sqrt{2\pi}} ,x \in (-\infty, \infty)$$

Trong trường hợp $$\mu = 0$$ và $$\sigma = 1$$ thì phân phối chuẩn còn được gọi là **Standard normal distribution** (tạm dịch: phân phối chuẩn tắc)

$$f(x) = \frac{e^{-x^{2}/2}} {\sqrt{2\pi}} , x \in (-\infty, \infty)$$

Sau đây là biểu đồ của Standard normal distribution 

![alt text](https://res.cloudinary.com/dzwwhbt1i/image/upload/v1569048671/norpdf_svvojx.gif "Standard normal distribution")

### 3. Hàm phân phối tích lũy

Công thức của [Hàm phân phối tích lũy] của Standard normal distribution là

$$F(x) = \int_{-\infty}^{x}  \frac{e^{-x^{2}/2}} {\sqrt{2\pi}} dx$$

![alt text](https://res.cloudinary.com/dzwwhbt1i/image/upload/v1569050430/norcdf_odrdxy.gif "cdf")

### 4. Độ lệch và độ nhọn

#### 4.1. Độ lệch (Skewness)

**Định nghĩa:** Độ lệch (skewness) của một phân phối xác suất đo lường sự đối xứng của phân phối đó. Giá trị tuyệt đối của độ lệch càng cao thì phân phối đó càng bất đối xứng. Một phân phối đối xứng có độ lệch bằng 0.

**Độ lệch dương** có nghĩa là các giá trị cực lớn hơn giá trị trung bình (mean) sẽ ở xa hơn so với giá trị cực nhỏ hơn giá trị trung bình (mean). Một đồ thị điển hình của một phân phối liên tục với độ lệch dương sẽ trông như thế này:


![alt text](https://res.cloudinary.com/dzwwhbt1i/image/upload/c_scale,h_300,w_400/v1569142682/Positively-Skewed-Distribution-Chart_dgaq3v.png "cdf")

Tương tự, một đồ thị điển hỉnh của một phân phối liên tục có độ lệch âm sẽ có hình dạng như sau

![alt text](https://res.cloudinary.com/dzwwhbt1i/image/upload/c_scale,h_300,w_400/v1569142682/Negatively-Skewed-Distribution-Chart_btuwsl.png "cdf")

#### 4.2. Độ nhọn (Kurtosis)

**Định nghĩa:** Độ nhọn (Kurtosis) là một chỉ số để đo lường về đặc điểm hình dáng của một phân phối xác suất. Cụ thể hơn, nó so sánh độ cao phần trung tâm của một phân phối so sánh với một phân phối chuẩn. Phần trung tâm càng cao và nhọn, chỉ số Kurtosis của phân phối đó càng lớn. Hay nói cách khác, kurtosis đo lường độ “béo” phần đuôi của một phân phối xác suất. Cái đuôi càng “béo”, kurtosis càng lớn.

Chúng ta cần chú ý những tính chất như sau:
- Excess kurtosis
- Hình dạng của phân phối xác suất với excess kurtosis dương/âm
- Excess kurtosis bao nhiêu thì được coi là đáng kể

Định nghĩa của excess kurtosis: lấy kurtosis của phân phối trừ đi 3. Excess kurtosis dương có nghĩa là kurtosis của phân phối lớn hơn 3, excess kurtosis âm nghĩa là kurtosis của phân phối nhỏ hơn 3. Cụ thể hơn, phân phối có:
- Excess kurtosis dương được gọi là leptokurtic (“lepto” nghĩa là gầy)
- Excess kurtosis bằng 0 được gọi là mesokurtic
- Excess kurtosis âm được gọi là platykurtic (“platy” nghĩa là “rộng”).

Đồ thị của một phân phối chuẩn chuẩn hóa (µ = 0, σ = 1), một phân phối leptokurtic và một phân phối platykurtic có hình dạng như sau:

![alt text](https://res.cloudinary.com/dzwwhbt1i/image/upload/c_scale,h_300,w_400/v1569143752/Kurtosis-Chart_k58w44.png "cdf")

- Phân phối chuẩn có kurtosis 3.0, hay zero excess kurtosis.
- Phân phối leptokurtic có kurtosis 4.0, hay excess kurtosis +1.0 (= 4.0 – 3.0).
- Phân phối platykurtic có kurtosis of 2.7, hay excess kurtosis -0.3 (= 2.7 – 3.0).


**Lưu ý**:  
- Tuy trên đồ thị không thể hiện rõ lắm, nhưng phân phối leptokurtic có phần đuôi (phần lớn hơn +4 và nhỏ hơn -4) “béo” hơn phân phối chuẩn khoảng gấp đôi, và phân phối platykurtic có phần đuôi “mỏng” hơn phân phối chuẩn khoảng một nửa.
- Excess kurtosis được tính là đáng kể nếu giá trị tuyệt đối của nó lớn hơn hoặc bằng 1.0; vd: kurtosis > 4.0 (excess positive kurtosis > 1.0) hoặc kurtosis < 2.0 (excess negative kurtosis < -1.0).


[hàm phân phối tích lũy]: https://becomedatascientist.github.io/bien-ngau-nhien/#pptl_lt