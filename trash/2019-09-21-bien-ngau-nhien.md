---
date: 2019-09-21 23:48:05
layout: post
title: Random Variable
description: >-
  Bài viết này sẽ giới thiệu về biến ngẫu nhiên và phân phối xác suất
image: >-
  https://res.cloudinary.com/dzwwhbt1i/image/upload/c_scale,w_400/v1569086067/aid1345372-v4-728px-Calculate-Probability-Step-2-Version-5_tnweks.jpg
category: statistics
author: levanpon98
paginate: true
---

### Mục lục
- [1. Biến ngẫu nhiên](#bien_ngau_nhien)
- [2. Xác định biến ngẫu nhiên](#xac_dinh_bien_ngau_nhien)
	- [2.1. Bảng phân phối xác suất](#bang_phan_phoi_sac_xuat)
	- [2.2. Hàm mật độ xác suất (Biến ngẫu nhiên rời rạc)](#mdxs_rr)
	- [2.3. Hàm phân phối tích lũy (Biến ngẫu nhiên rời rạc)](#pptl_rr)
	- [2.4. Hàm mật độ xác suất (Biến ngẫu nhiên liên tục)](#mdxs_lt)
	- [2.5. Hàm phân phối tích lũy (Biến ngẫu nhiên liên tục)](#pptl_lt)
- [3. Tham số đặc trưng của biến ngẫu nhiên](#parameters)
	- [3.1. Kỳ vọng](#kv)
	- [3.2. Phương sai](#ps)
	- [3.3. Độ lệch chuẩn](#dlc)
	- [3.4. Mode](#mode)
	- [3.5. Trung vị](#tv)
	- [3.6. Hệ số đối xứng và hệ số nhọn](#hsdx)
	- [3.7. Mômen](#mm)

### 1. Biến ngẫu nhiên <a name="bien_ngau_nhien"></a>

**Khái niệm:** Xét phép thử  $$\tau$$ với không gian mẫu $$\Omega$$. Giả sử, ứng với mỗi biến số sơ cấp  $$\omega \in \Omega$$. ta liên kết với một số thực $$X(\omega) \in \mathbb{R}$$, thì $$X$$ được gọi là một biến ngẫu nhiên. Mỗi giá trị nhận được $$x$$ của biến ngẫu nhiên $$X$$ được gọi là một thể hiện của $$X$$, đây cũng là kết quả của phép thử hay còn được hiểu là một sự kiện. Tổng quát lên thì biến ngẫu nhiên $$X$$ của phép thử $$\tau$$ với không gian mẫu $$\Omega$$ là một ánh xạ:
$$ X: \Omega \to \mathbb{R} \\
	\omega \mapsto X(\omega)
	$$
Biến ngẫu nhiên có 2 dạng

* Biến ngẫu nhiên rời rạc: khi $$X(\omega)$$ là một tập hữu hạn $$\{x_1, x_2,...,x_k \}$$ hay một dãy $$\{x_1, x_2,...,x_k \}$$
* Biến ngẫu nhiên liên tục: khi $$X(\omega)$$ là một khoản của $$\mathbb{R}$$ hay cả $$\mathbb{R}$$

### 2. Xác định biến ngẫu nhiên <a name="xac_dinh_bien_ngau_nhien"></a>

Để xác định một biến ngẫu nhiên rời rạc, ta cần xác định các giá trị $$x_i, i = 1,2,...$$ có thể nhận được bởi biến ngẫu nhiên này và đồng thời cũng cần xác định xác suất $$X$$ nhận giá trị này là bao nhiêu. Ta cần có:
#### 1.1. Bảng phân phối xác suất <a name="bang_phan_phoi_sac_xuat"></a>
Bảng phân phối xác suất sẽ có dạng:

 $$X$$ | $$x_1$$ | $$x_2$$ | $$...$$ | $$x_n$$ | $$...$$ 
| --- | --- | --- | --- | --- | --- 
 $$P$$ | $$p_1$$ | $$p_2$$ | $$...$$ | $$p_n$$ | $$...$$ 

Với $$p_i = P(X=x_i)$$

**Ví dụ:** Thảy hai đồng xu, nếu được một sấp một ngửa thì được 10đ, nếu được hai mặt sấp thì mất 4đ, hai mặt ngửa thì mất 5đ

<center>Giải</center>
Gọi $$X$$ để chỉ số tiền được hay mất. Ta có $$X$$ là biến ngẫu nhiên nhận các giá trị là $$-5, -4, 10$$, với
	$$ P(X=-5) = P(NN) = \frac{1} {4} = 0,25, \\
		P(X=-4) = P(SS) = \frac{1} {4} = 0,25, \\
		P(X=10) = P(\{SN, NS\}) = \frac{2} {4} = 0,5
		$$
Và ta nhận được bảng phân phối xác suất của $$X$$ như sau

$$X$$ | $$-5$$ | $$-4$$ | $$10$$ 
--- | --- | --- | --- 
$$P$$ | $$0,25$$ | $$0,25$$ | $$0,5$$ 

#### 1.2. Hàm mật độ xác suất (Biến ngẫu nhiên rời rạc) <a name="mdxs_rr"></a>

Ta có hàm số
$$f(x) =
  \begin{cases}
    p_i      & \quad \text{khi } x = x_i\\
    0  & \quad \text{khi } x \ne x_i
  \end{cases}
$$
được gọi là hàm mật độ xác suất. 

Từ tính chất của bảng phân phối xác suất, dễ thấy rằng
- \$$\forall x \in \mathbb{R}, f(x) \ge 0$$
- \$$ \sum_{x}^{} f(x)  = 1$$

**Ví dụ:** Tung đồng xu 3 lần. Gọi X là số mặt sấp nhận được. Ta có không gian mẫu

$$\Omega = \{ SSS,SSN,SNS,SNN,NSS,NSN,NNS,NNN\} \text{và},\\
X(\Omega) = \{0,1,2,3\}, \text{với} \\
P(X = 0) = P(\{NNN\}) = \frac{1} {8}, \\
P(X = 1) = P(\{SNN,NSN,NNS\}) = \frac{3} {8}, \\ 
P(X = 2) = P(\{SSN,SNS,NSS\}) = \frac{3} {8}, \\
P(X = 3) = P(\{SSS\}) = \frac{1} {8} $$

Và ta có bảng phân phối xác suất

$$X$$ | $$0$$ | $$1$$ | $$2$$ | $$3$$
--- | --- | --- | --- | ---  
$$P$$ | $$\frac{1} {8}$$ | $$\frac{3} {8}$$ | $$\frac{3} {8}$$ | $$\frac{1} {8}$$

#### 1.3. Hàm phân phối tích lũy (Biến ngẫu nhiên rời rạc) <a name="pptl_rr"></a>

Với $$f(x)$$ là hàm mật độ của biến ngẫu nhiên rời rạc X, hàm số:

$$F(x) = P(X \le x) = \sum_{x_i \le x}^{} f(x_i)$$

Được gọi là hàm phân phối tích lũy, hay gọi tắt là hàm phân phối.

Bằng cách liệt kê các giá trị của $$X(\Omega)$$ theo thứ tự tăng dần, khi $$X$$ chỉ lấy hữu hạn các giá trị $$\{x_1 < x_2 < ... < x_k\}$$ thì ta có hàm phân phối:

$$F(x) =
  \begin{cases}
  	0  & \quad \text{khi } x < x_1 \\
    f(x_1) + f(x_2) + ... + f(x_{k-1})      & \quad \text{khi } x_{k-1} \le x < x_k \\
    1  & \quad \text{khi } x \ge x_n
  \end{cases}
$$

Và khi $$X$$ lấy giá trị tạo thành một dãy $$\{x_1 < x_2 < ... < x_n < ...\}$$ thì ta có hàm phân phối

$$F(x) =
  \begin{cases}
  	0  & \quad \text{khi} x < x_1 \\
    f(x_1) + f(x_2) + ... + f(x_{n-1})      & \quad \text{khi} x_{n-1} \le x < x_n \\
    1  & \quad \text{khi} x \ge x_n, \forall n
  \end{cases}
$$

Từ tính chất của hàm mật độ và định nghĩa của hàm phân phối ta có:
- \$$0 \le F(x) \le 1, \forall x \in \mathbb{R}$$
- \$$\lim\limits_{x \to -\infty} F(x) = 0 \text{và} \lim\limits_{x \to +\infty} F(x) = 1$$
- $$F$$ là hàm tăng và $$F$$ liên tục bên phải tại $$\forall x \in \mathbb{R}$$

**Ví dụ:**
Với biến $$X$$ được cho ở ví dụ trên, ta có hàm phân phối 

$$F(x) =
  \begin{cases}
  	0  & \quad \text{khi } x < 0 \\
    \frac{1} {8}  & \quad \text{khi } 0 \le x < 1 \\
    \frac{4} {8}  & \quad \text{khi } 1 \le x < 2 \\
    \frac{7} {8}  & \quad \text{khi } 2 \le x < 3 \\
    \frac{1} {8}  & \quad \text{khi }  x \le 3 \\
  \end{cases}
$$

#### 1.4. Hàm mật độ xác suất (Biến ngẫu nhiên liên tục) <a name="mdxs_lt"></a>

Hàm mật độ xác suất của biến ngẫu nhiên liên tục có dạng:

$$ P(a \le X \le b) = \int_{a}^{b} f(x) dx, (\forall a, \forall b \in \mathbb{R}, a \le b) $$

Từ định nghĩa, dễ dàng suy ra
- \$$\forall x \in \mathbb{R}, f(x) \ge 0,$$
- \$$ \int_{-\infty}^{\infty} f(x) dx = 1$$

#### 1.5. Hàm phân phối tích lũy (Biến ngẫu nhiên liên tục) <a name="pptl_lt"></a>

Hàm $$F$$ được gọi là hàm phân phối tích lũy của biến ngẫu nhiên liên tục $$X$$ với định dạng:

$$F(x) = P(X \le x),  \forall x \in \mathbb{R}$$

Trực tiếp từ định nghĩa, ta được:
- \$$ 0 \le F(x) \le 1, \forall x \in \mathbb{R}, $$
- \$$\lim\limits_{x \to -\infty} F(x) = 0 \text{ và } \lim\limits_{x \to +\infty} F(x) = 1$$
- $$F$$ là hàm tăng và $$F$$ liên tục bên phải tại $$\forall x \in \mathbb{R}$$
Hơn nữa, ta được sự liên hệ giữa hàm mật độ $$f(x)$$ và hàm phân phối $$F(x)$$ của biến ngẫu nhiên liên tục $$X$$ như sau
$$F(x) = \int_{-\infty}^{x} f(x) dx, \forall x \in \mathbb{R}$$

**Ví dụ:** Cho X là biến ngẫu nhiên liên tục có hàm mật độ xác suất

$$f(x) =
  \begin{cases}
  	0  & \quad \text{khi } x < 0 \\
    x  & \quad \text{khi } 0 < x \le 1 \\
    2 - x  & \quad \text{khi } 1 < x \le 2 \\
    0  & \quad \text{khi } 2 < x \\
  \end{cases}
$$

$$a)$$ Tìm hàm phân phối xác suất của X

$$b)$$ Tính $$P(X < \frac{1} {2})$$

<center>Giải</center>

Ta có $$F(x) = P(X \le x) = \int_{-\infty}^{x} f(t) dt$$. Do đó 

Khi $$x \le 0, F(x) = 0$$,

Khi $$0 < x \le 1, F(x) = \int_{0}^{x} tdt = \frac{x^{2}} {2}$$

Khi $$1 < x \le 2, F(x) = \int_{0}^{1}tdt + \int_{1}^{x} (2 - 1)dt = -\frac{x^{2}} {2} + 2x - 1; $$

Khi $$2 < x, F(x) = \int_{0}^{1}tdt + \int_{1}^{2} (2 - 1)dt = 1$$

Do đó, ta được hàm phân phối xác suất cho $$X$$ là:

$$F(x) =
  \begin{cases}
  	0  & \quad \text{khi } x < 0 \\
    \frac{x^{2}} {2} & \quad \text{khi } 0 < x \le 1 \\
    -\frac{x^{2}} {2} + 2x - 1  & \quad \text{khi } 1 < x \le 2 \\
    1  & \quad \text{khi } 2 < x \\
  \end{cases}
$$

Và ta được $$P(X < \frac{1} {2}) = F(\frac{1} {2}) = \frac{1} {2} (\frac{1} {2})^{2} = \frac{1} {8}$$

### 3. Tham số đặc trưng của biến ngẫu nhiên  <a name="parameters"></a>

#### 3.1. Kỳ vọng ($$\mu$$) <a name="kv"></a>
**Định nghĩa:** Cho $$X$$ là biến ngẫu nhiên với hàm mật độ xác suất $$f(x)$$ và $$u(x=X)$$ là một hàm theo biến ngẫu nhiên $$X$$. **Kỳ Vọng** (mean) của $$u(X)$$ được xác định là:

$$E(u(X)) = 
	\begin{cases}
  	\sum_{i}^{} u(x_i)f(x_i)  & \quad \text{Nếu X là biến ngẫu nhiên rời rạc} \\
    \int_{-\infty}^{+\infty} u(x)f(x)dx & \quad \text{Nếu X là biến ngẫu nhiên liên tục}\\
  \end{cases}
$$

**Ví dụ:** Cho một hộp đựng 3 bi đỏ và 7 bi trắng. Mỗi lần lấy 1 bi (rồi trả lại vào hộp). Nếu được bi đỏ thì thưởng 5000đ, nếu được bi trắng thì phạt 2300đ. Xét xem có nên tham gia trò chơi này nhiều lần hay không?
<center>Giải</center>
Gọi $$X$$ là số tiền nhận được sau mỗi lần lấy bi. X là biến ngẫu nhiên với bảng phân phối xác suất sau

$$X$$ | $$-2300$$ | $$5000$$ 
--- | --- | --- 
$$P$$ | $$\frac{7}{10}$$ | $$\frac{3}{10}$$

Trung bình của $$X$$ là:
$$\mu = -2300 \times \frac{7}{10} + 5000 \times \frac{3}{10} = -110$$

Điều này có nghĩa là nếu ta chơi nhiều lần thì bình quân mỗi lần lấy một bi, ta lỗ 110đ. Vậy, không nên chơi trò chơi này nhiều lần.

#### 3.2. Phương sai ($$\sigma_X^2$$) <a name="ps"></a>
**Định nghĩa:** **Phương sai** (variance) được ký hiệu là $$\sigma_X^2$$, chính là con số cho ta hình dung được mức độ phân tán của các số liệu so với kỳ vọng: nếu $$\sigma_X^2$$ càng nhỏ, các số liệu càng tập trung xung quanh trung bình của chúng. Công thức của phương sai là:

$$\sigma_X^2 = E((X - \mu_X^2)^2) = 
	\begin{cases}
  	\displaystyle\sum_{i}^{} (x_i - \mu_X^2)^2 f(x_i)  & \quad \text{Nếu X là biến ngẫu nhiên rời rạc} \\
    \int_{-\infty}^{+\infty} (x - \mu_X^2)^2 f(x)dx & \quad \text{Nếu X là biến ngẫu nhiên liên tục}\\
  \end{cases}
$$

**Ví dụ:** Cho X là biến ngẫu nhiên với hàm mật độ xác suất

$$f(x) =
  \begin{cases}
  	\frac{3}{4} (1-x^2)  & \quad \text{khi } |x| \le 1 \\
    0  & \quad \text{khi } |x| > 1 \\
  \end{cases}
$$, Tính $$\mu_X$$ và $$\sigma_X^2$$

<center>Giải</center>

$$
\mu_X = \int_{-\infty}^{+\infty} xf(x)dx = \int_{-1}^{1} \frac{3x}{4} \left(1 - x^2\right)dx = 0, \\
\sigma_X^2 = \int_{-\infty}^{+\infty} (x - \mu_X^2)^2 f(x)dx = \int_{-1}^{1} \frac{3x^{2}}{4} \left(1 - x^2\right)dx \\
= 2\int_{1}^{0} \frac{3x^{2}}{4} \left(1 - x^2 \right)dx = 2\left(\frac{3}{4} \left.\left(\frac{x^3}{3} - \frac{x^5}{5}\right)\right|_0^1 \right) = \frac{1}{5}
$$

**Mệnh đề**: Cho $$X$$ là biến ngẫu nhiên với trung bình $$E(x) = \mu_X$$. Ta có
$$\sigma_X^2 = E(X^2) - \mu_X^2$$

*Chứng minh*: Do $$E$$ tuyến tính, nghĩa là 
$$E(\alpha X + \beta Y) = \alpha E(X) + \beta E(Y), \\
\text{Ta suy ra: } \\
\sigma_X^2 = E\left(\left(X - \mu_X^2\right)^2\right) \\
= E\left(X^2 - 2X\mu_X + \mu_X^2 \right) \\
= E\left(X^2\right) - 2\mu_xE(X) + \mu_X^2 \\
= E\left(X^2\right) - \mu_X^2
 $$

<!-- 
			   E(\alphaX + \betaY) = \alphaE(X) + \betaE(Y), \\
	\text{Ta suy ra:} \\
	\sigma_X^2 & \quad = E\left(\left(X - \mu_X^2\right)^2\right) \\
			   & \quad = E\left(X^2 - 2X\mu_X + \mu_X^2 \right) \\
			   & \quad = E\left(X^2\right) - 2\mu_xE(X) + \mu_X^2 \\
			   & \quad = E\left(X^2\right) - \mu_X^2 -->

#### 3.3. Độ lệch chuẩn ($$\sigma$$) <a name="dlc"></a>
**Khái niệm:** Độ lệch chuẩn (standard deviation) là đại lượng thường được sử dụng để phản ánh mức độ phân tán của một biến số xung quanh số bình quân. Nói cách khác, độ lệch chuẩn dùng để đo mức độ phân tán của một tập dữ liệu đã được lập thành bảng tần số. Có thể tính ra độ lệch chuẩn bằng cách lấy căn bậc hai của phương sai.

**Ý nghĩa:** Độ lệch chuẩn đo tính biến động của giá trị mang tính thống kê. Nó cho thấy sự chênh lệch về giá trị của từng thời điểm đánh giá so với giá trị trung bình. Tính biến động cũng như độ lệch chuẩn sẽ cao hơn nếu giá đóng cửa và giá đóng cửa trên trung bình khác nhau đáng kể. 

Nếu sự chênh lệch không đáng kể thì độ lệch chuẩn và tính biến động ở mức thấp. Sự đảo chiều xu thế tạo các vùng đáy hoặc đỉnh của thị trường được xác định thời cơ bằng các mức độ biến động cao. Những xu thế mới của giá sau thời kỳ thoái trào của thị trường (tức là giai đoạn điều chỉnh) thường được xác định thời cơ bằng những mức độ biến động thấp. Sự thay đổi đáng kể về dữ liệu giá đem lại giá trị độ lệch chuẩn cao và dữ liệu giá ổn định hình thành độ lệch chuẩn ở mức thấp.

#### 3.4. Mode <a name="mode"></a>
Mode của đại lượng ngẫu nhiên rời rạc $$X$$, kí hiệu là $$Mod(x)$$, là giá trị $$x_0$$ của X mà $$P(X = x_0)$$ là lớn nhất. Người ta còn nói rằng $$Mod(x)$$ là *giá trị tin chắc nhất* của $$X$$. Trong trường hợp $$X$$ là biến ngẫu nhiên liên tục với hàm mật độ $$f(x)$$, thì $$Mod(x)$$ là giá trị $$x_0$$ của $$X$$ sao cho $$f(x)$$ là lớn nhất.

#### 3.5. Trung vị <a name="tv"></a>
**Định nghĩa:** Trung vị (median) của đại lượng ngẫu nhiên (rời rạc hay liên tục), ký hiệu là $$Med(x)$$, là giá trị $$x_0$$ của $$X$$ sao cho:

$$P(X \le x_0) = P(X \ge x_0)$$

*Chú ý*: Mode cũng như Median của một đại lượng ngẫu nhiên thì không duy nhất.

#### 3.6. Hệ số đối xứng và hệ số nhọn <a name="hsdx"></a>
Với X là biến ngẫu nhiên với trung bình $$\mu_X$$ và phương sai $$\sigma_X^2$$

**Hệ số đối xứng** có công thức như sau:

$$\gamma_1 = \frac{E\left( \left(X - \mu_X\right)^3\right)} {\sigma_X^3}$$

**Hệ số nhọn** có công thức sau: 

$$\gamma_2 = \frac{E\left( \left(X - \mu_X\right)^4\right)} {\sigma_X^4}$$

**Nhận xét**
- $$\gamma_1(X) = 0$$ thì phân phối của X là đối xứng; lệch phải khi $$\gamma_1(X) > 0$$ và lệch trái khi $$\gamma_1(X) < 0$$
- $$\gamma_2(X)$$ càng lớn thì phân phối của X càng nhọn

#### 3.7. Mômen <a name="momen"></a>
Với X là biến ngẫu nhiên có trung bình $$\mu_X$$, kì vọng của $$X^k$$ được gọi là *mômen gốc* cấp k của $$X$$, kí hiệu $$m_k$$,
$$m_k = E(X^k)$$ 
Và kỳ vọng của $$(X - \mu_X)^k$$ được gọi là *mômen quy tâm* cấp k của $$X$$, ký hiệu $$t_k$$
$$t_k = E\left((X - \mu_X)^k\right)$$ 
Chú ý rằng $$m_1 = \mu_X \text{và } t_2 = \sigma_X^2$$
