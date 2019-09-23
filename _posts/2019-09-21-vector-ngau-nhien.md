---
date: 2019-09-22 00:16:10
layout: post
title: Vector ngẫu nhiên
description: >-
  Bài viết này sẽ giới thiệu về vector ngẫu nhiên
image: >-
  https://res.cloudinary.com/dzwwhbt1i/image/upload/c_scale,w_400/v1569086067/aid1345372-v4-728px-Calculate-Probability-Step-2-Version-5_tnweks.jpg
category: statistics
author: levanpon98
paginate: true
---

## Mục lục
- [1. Vector ngẫu nhiên rời rạc](#vector_rr)
  - [1.1. Mật độ đồng thời](#mddt_rr)
  - [1.2. Mật độ thành phần](#mdtp_rr)
  - [1.3. Mật độ có điều kiện](#mdcdk_rr)
  - [1.4. Biến ngẫu nhiên độc lập](#bnndl_rr)
- [2. Vector ngẫu nhiên liên tục](#vector_lt)
  - [2.1. Mật độ đồng thời](#mddt_lt)
  - [2.2. Mật độ thành phần](#mdtp_lt)
  - [2.3. Mật độ có điều kiện](#mdcdk_lt)
  - [2.4. Biến ngẫu nhiên độc lập](#bnndl_lt)
- [3. Tham số đặc trưng vector ngẫu nhiên](#thamso)
  - [3.1. Trung bình thành phần](#tbtp)
  - [3.2. Phương sai thành phần](#pstp)
  - [3.3. Hệ số tương quan và hiệp phương sai](#hstq)
- [4. Kết luận](#ketluan)

### 1. Vector ngẫu nhiên rời rạc <a name="vector_rr"></a>

Xét một vector ngẫu nhiên $$V = (X,Y)$$. Giả sử $$X, Y$$ lần lượt lấy các giá trị 

$$ X = x_1, x_2, x_3, ... \\
Y = y_1, y_2, y_3, .... $$

Đặt   $$p_{ij} = P(X = x_i; Y = y_i)$$

Ta có bảng phân phối xác xuất

$$X, Y$$ | $$y_1$$ | $$y_2$$ | $$...$$ | $$P_X$$ 
--- | --- | --- | --- | --- | --- 
$$x_1$$ | $$p_{11}$$ | $$p_{12}$$ | $$...$$ | $$p_{1.}$$
$$x_2$$ | $$p_{21}$$ | $$p_{22}$$ | $$...$$ | $$p_{2.}$$
$$...$$ | $$...$$ | $$...$$ | $$...$$ | $$...$$
$$P_Y$$ | $$p_{.1}$$ | $$p_{.2}$$ | $$...$$ | $$1$$

#### 1.1. Mật độ đồng thời <a name="mddt_rr"></a>

Hàm số:

$$f(x,y) =
  \begin{cases}
    p_{ij}      & \quad \text{khi } (x, y) = (x_i, y_j)\\
    0  & \quad \text{khi } (x, y) \ne (x_i, y_j) \forall i, j
  \end{cases}
$$

Được gọi là hàm *mật độ đồng thời* của $$V(X, Y)$$.

Từ định nghĩa, ta có 
- \$$f(x,y) \ge 0, \forall (x,y) $$
- \$$\displaystyle\sum_{x,y}^{} f(x,y) = 1$$

#### 1.2. Mật độ thành phần <a name="mdtp_rr"></a>

Từ bảng phân phối sác xuất của $$V(X, Y)$$, ta có bảng phân phối xác suất cho $$X$$:

$$X$$ | $$x_1$$ | $$x_2$$ | $$...$$  
--- | --- | --- | --- 
$$P$$ | $$p_{1.}$$ | $$p_{2.}$$ | $$...$$ 

Và hàm mật độ của $$X$$

$$f_X(x) \equiv \displaystyle\sum_{y}^{} f(x, y)$$

được gọi là *hàm mật độ thành phần X* của $$V$$

Tương tự, ta có bảng phân phối xác suất cho $$Y$$

$$Y$$ | $$y_1$$ | $$y_2$$ | $$...$$  
--- | --- | --- | --- 
$$P$$ | $$p_.1$$ | $$p_.2$$ | $$...$$ 

Và hàm mật độ của $$Y$$

$$f_Y(y) \equiv \displaystyle\sum_{x}^{} f(x, y)$$

được gọi là *hàm mật độ thành phần Y* của $$V$$

#### 1.3. Mật độ có điều kiện <a name="mdcdk_rr"></a>

Để khảo sát biến ngẫu nhiên $$X$$ khi đã biết $$Y$$ xảy ra, ta cần tính xác suất có điều kiện $$P(X \| Y)$$:

$$P(X = x_i | Y = y_j) = \frac{P(X = x_i ; Y = y_j)} {P(Y = y_j)} = \frac{p_{ij}} {p_{.j}}$$

Và ta có bảng phân phối xác suất của $$ X \| (Y = y_j)$$

$$X$$ | $$x_1$$ | $$x_2$$ | $$...$$  
--- | --- | --- | --- 
$$P$$ | $$\frac{p_{1j}} {p_{.j}}$$ | $$\frac{p_{2j}} {p_{.j}}$$ | $$...$$ 

và hàm số 

$$f_{X|Y}(x) = \frac{f(x, y)} {f_Y(y)}$$

được gọi là *hàm mật độ có điều kiện* của $$X$$, khi biết $$Y = y$$

Tương tự, hàm số: 

$$f_{Y|X}(y) = \frac{f(x, y)} {f_X(x)}$$

được gọi là *hàm mật độ có điều kiện* của $$Y$$, khi biết $$X = x$$

#### 1.4. Biến ngẫu nhiên độc lập <a name="bnndl_rr"></a>

Với hai biến ngẫu nhiên $$X, Y$$, ta nói $$X$$ *độc lập* với Y nếu hàm mật độ có điều kiện của $$X$$, khi biết $$Y = y$$, không phụ thuộc vào $$y$$, nghĩa là: 

$$f_X|Y(x) = f_X(x)$$

do đó

$$f(x,y) = f_X(x)f_Y(y)$$

Từ đó suy ra

$$f_Y(y) = \frac{f(x,y)} {f_X(x)} = f_Y|X(y)$$

và do đó, $$Y$$ cũng độc lập với $$X$$

### 2. Vector ngẫu nhiên liên tục <a name="vector_lt"></a>

#### 2.1. Mật độ đồng thời <a name="mddt_lt"></a>

Hàm số $$f(x,y)$$ được gọi là *hàm mật độ đồng thời* của $$V(X, Y)$$, nếu $$\forall a,b,c,d \in \mathbb{R}, a \le b, c le d$$, ta có:

$$P(a \le X \le b; c \le Y \le d) = \int_{c}^{d} \int_{a}^{b} f(x, y) dxdy$$

Từ định nghĩa, ta có:
- \$$f(x,y) \ge 0, \forall (x,y)$$
- \$$\iint\limits_{-\infty}^{\infty} f(x, y) dxdy = 1$$

#### 2.2. Mật độ thành phần <a name="mdtp_lt"></a>

*Hàm mật độ thành phần* $$X$$ và $$Y$$ của $$V$$ được lần lượt xác định theo hàm mật độ đồng thời $$f(x, y)$$ của $$V$$ bởi

$$ 
f_X(x) = \int\limits_{-\infty}^{\infty} f(x,y) dy, \\ 
f_Y(y) = \int\limits_{-\infty}^{\infty} f(x,y) dx, \\ 
$$

#### 2.3. Mật độ có điều kiện <a name="mdcdk_lt"></a>

*Hàm mật độ có điều kiện* của $$X$$, khi biết $$Y = y$$ và *hàm mật độ có điều kiện* của $$Y$$ khi biết $$X = x$$ lần lượt cho bởi

$$f_{X|Y}(x) = \frac{f(x,y)}{f_Y(y)} \\
f_{Y|X}(y) = \frac{f(x,y)}{f_X(x)}
$$

#### 2.4. Biến ngẫu nhiên độc lập <a name="bnndl_lt"></a>

Với hai biến ngẫu nhiên $$X, Y$$, ta nói $$X$$ *độc lập* với Y nếu hàm mật độ có điều kiện của $$X$$, khi biết $$Y = y$$, không phụ thuộc vào $$y$$, nghĩa là:

$$f_X|Y(x) = f_X(x)$$

do đó

$$f(x,y) = f_X(x)f_Y(y)$$

Từ đó suy ra

$$f_Y(y) = \frac{f(x,y)} {f_X(x)} = f_Y|X(y)$$

và do đó, $$Y$$ cũng độc lập với $$X$$

### 3. Tham số đặc trưng vector ngẫu nhiên <a name="thamso"></a>

#### 3.1. Trung bình thành phần <a name="tbtp"></a>

Để tính trung bình của $$X$$ và $$Y$$, ta có thể sử dụng các công thức cho biến ngẫu nhiên bằng cách dùng các hàm mật độ thành phần $$f_X(x)$$ và $$f_Y(y)$$. 

Trung bình của $$X$$:

$$\mu_X = 
  \begin{cases}
    \displaystyle\sum_{x,y}^{} xf(x, y)  & \quad \text{Nếu X là biến ngẫu nhiên rời rạc} \\
    \iint\limits_{-\infty}^{+\infty} xf(x,y) dxdy & \quad \text{Nếu X là biến ngẫu nhiên liên tục}\\
  \end{cases}
$$

Tương tự cho $$\mu_Y$$

#### 3.2. Phương sai thành phần <a name="pstp"></a>

Phương sai của $$X$$: 

$$\sigma_X^2 = 
  \begin{cases}
    \displaystyle\sum_{x,y}^{} (x - \mu_X)^2 f(x, y) & \quad \text{Nếu X là biến ngẫu nhiên rời rạc} \\
    \iint\limits_{-\infty}^{+\infty} (x - \mu_X)^2 f(x, y)  dxdy & \quad \text{Nếu X là biến ngẫu nhiên liên tục}\\
  \end{cases}
$$

Tương tự với $$\sigma_X^2$$
#### 3.3. Hệ số tương quan và hiệp phương sai <a name="hstq"></a>

##### a. Hiệp phương sai (Covariance)
**Định nghĩa** thể hiện mối quan hệ giữa các biến với nhau, có thể là đồng biến hoặc nghịch biến

**Công thức:**
$$cov(X,Y)= 
  \begin{cases}
    \displaystyle\sum_{x,y}^{} (x - \mu_X)(y - \mu_Y) f(x, y) & \quad \text{Nếu X,Y là biến ngẫu nhiên rời rạc} \\
    \iint\limits_{-\infty}^{+\infty} (x - \mu_X)(y - \mu_Y) f(x, y)  dxdy & \quad \text{Nếu X, Y là biến ngẫu nhiên liên tục}\\
  \end{cases}
$$


##### b. Hệ số tương quan (Correlation)

**Định nghĩa:** Thể hiện mối quan hệ giữa 2 biến là “mạnh” hay “yếu”, chúng ta sử dụng correlation thay cho covariance. 

**Công thức:**

$$\rho(X, Y) = \frac{cov(X, Y)} {\sigma_X\sigma_Y}$$

##### c. So sánh giữa covariance và correlation 
- Cả covariance và correlation đều thể hiện mối quan hệ giữa hai biến.
- Covariance có range từ $$-\infty$$ đến $$\infty$$, correlation nằm trong khoảng từ - 1 đến 1.
- Covariance thể hiện mối quan hệ giữa hai biến, correlation thể hiện được mối quan hệ giữa hai hoặc nhiều biến.

### 4. Kết luận <a name="ketluan"></a>

Bài này mình đã chia sẻ những hiểu biết của mình về **Vector ngẫu nhiên** và một số tham số rất quan trọng: covariance, correlation 

*Còn bây giờ, nếu có thắc mắc hay góp ý gì thì đừng quên để lại bình luận phía dưới cho mình nhé!*




