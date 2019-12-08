---
date: 2019-09-22 23:48:05
layout: post
title: Hypothesis Testing
description: >-
  Bài viết này sẽ giới thiệu về khái niệm Hypothesis Testing
image: >-
  https://res.cloudinary.com/dzwwhbt1i/image/upload/c_scale,w_400/v1569086067/aid1345372-v4-728px-Calculate-Probability-Step-2-Version-5_tnweks.jpg
category: statistics
author: levanpon98
paginate: false
---

### 1. Giả thuyết thống kê

Cách tốt nhất để xác định xem một giả thuyết thống kê đưa ra là đúng hay không chính là kiểm tra toàn bộ, tuy nhiên việc kiểm tra toàn bộ dữ liệu lại rất tốn kém và mất rất nhiều thời gian nếu dữ liệu đủ lớn. 
Trên thực tế, các nhà nghiên cứu thường kiểm tra trên một mẫu (sample) ngẫu nhiên trích ra từ tổng thể (population). Nếu dữ liệu mẫu không phù hợp với giả thuyết thống kê, giả thuyết sẽ bị từ chối.

Có hai loại giả thuyết thống kê.

- **Null Hypothesis**:  Ký hiệu bằng $$H_0$$, đây là giả thuyết chỉ ra rằng sẽ không có một ý nghĩa thống kê nào tồn tại trong một tập hợp các quan sát nhất định. Trong công thức toán học của Null Hypothesis thường sẽ có dấu "=". 
Chúng ta thường cố gắng tìm bằng chứng để loại bỏ giả thuyết này.
- **Alternative hypothesis**: Ký hiệu bằng $$H_a$$ hoặc $$H_1$$, ngược lại với Null Hypothesis, đây là giả thuyết phản ánh tập các quan sát có ý nghĩa thống kê. Trong công thức toán học của Alternative Hypothesis thường có dấu bất đẳng thức hoặc dấu "$$\ne$$". Đây là giả thuyết mà chúng ta cố gắng chứng minh.

**Ví dụ: Kết luận xử án**  
Một đợt kiểm định độ tin cậy được tiến hành cho một tội phạm. Bị cáo sẽ chưa bị kết luận là có tội khi tội của anh ta chưa được chứng minh. Nguyên đơn cố gắng chứng minh tội của bị cáo. Chi khi có đủ bằng chứng thì bị cáo mới bị buộc tội.

Bắt đầu đợt kiểm định, có hai giả thuyết $$H_0$$: "bị cáo không có tội", và $$H_a$$: "bị cáo có tội". Giả thuyết thứ nhất được gọi là Null hypothesis, và hiện tại đang được chấp nhận. Giả thuyết thứ 2 được gọi là Alternative hypothesis. Đây là giả thuyết mà nguyên đơn cố gắng chứng minh.

Giả thuyết 1 chỉ được bác bỏ nếu lỗi nói sai rất ít khả năng xảy ra, bởi vì chúng ta không muốn đổ oan cho người vô tội. Lỗi nói sai đó được gọi là lỗi loại một (nghĩa là đổ oan cho người vô tội), và khả năng mắc lỗi này được kiểm soát sao cho ít xảy ra nhất. Vì do chúng ta cố gắng không áp tội cho người khác, nên xảy ra lỗi loại 2 (bỏ thoát tội một người mà thực tế có tội), xác suất lỗi này thường lớn hơn.

_ | Null Hypothesis (H0) là đúng (Anh ta thực sự không có tội) | Alternative Hypothesis (H1) là đúng (Anh ta thực sự có tội)
 --- | --- | ---
 Chấp nhận Null Hypothesis Xóa án | Quyết định đúng | Quyết định sai Lỗi loại II
 Bác bỏ Null Hypothesis Kết án | Quyết định sai (Loại I) | Quyết định đúng
 
 Phiên tòa có thể được coi là một hay cả hai quá trình: có tội với không có tội hoặc bằng chứng với một người ("quá một mức nghi ngờ hợp lý"). Kiểm định giả thuyết ở đây là hoặc kiểm định giả thuyết hoặc kiểm định bằng chứng.

### 2. Kiểm định giả thuyết thống kê (Hypothesis testing)

Đây là một quy trình mà một nhà thống kê phải tuân theo để xác định xem có nên từ chối Null Hypothesis hay không. Quy trình này bao gồm 4 bước:
- Nêu các giả thuyết, điều này liên quan đến việc nêu các Null Hypothesis và Alternative Hypothesis. Các giả thuyết được nêu theo cách mà chúng loại trừ lẫn nhau. Đó là, nếu một cái đúng, cái kia phải sai.
- Tiếp theo là xây dựng một kế hoạch phân tích để đánh giá sự chính xác của Null Hypothesis.
- Trả lời câu hỏi: nếu Null Hypothesis đúng, thì xác suất mà những dữ kiện thu được phù hợp với giả thuyết đảo là bao nhiêu? Xác suất đang nói đến thường được đề cập trong rất nhiều bài báo khoa học và được ký hiệu bằng "P-value". 
Nếu p-value càng nhỏ thì xác suất xảy ra Null Hypothesis sẽ càng giảm, nếu p-value càng cao thì ngược lại. 
- So sánh P-value vừa tìm được với giá trị $$\alpha$$ (significance value). Nếu $$p \leqslant \alpha$$, điều đó có nghĩa rằng số thử nghiệm của chúng ta có ý nghĩa thống kê, Null Hypothesis sẽ bị loại bỏ.

### 3. Ví dụ thực tế về kiểm định giả thuyết thống kê

Ví dụ, nếu một người muốn kiểm tra rằng một đồng xu có chính xác 50% cơ hội là mặt ngửa, thì Null Hypothesis sẽ là có, và Alternative Hypothesis sẽ là không (nó không rơi vào mặt ngửa). Về mặt toán học, Null Hypothesis sẽ được biểu diễn dưới dạng $$H_0$$: P = 0,5. Alternative Hypothesis sẽ được ký hiệu là $$H_a$$: P $$\ne$$

Một mẫu ngẫu nhiên gồm 100 lần tung đồng xu được lấy từ tổng thể và sau đó $$H_0$$ được kiểm tra. Nếu phát hiện ra rằng 100 đồng xu được phân phối là 40 ngửa và 60 sấp, nhà phân tích sẽ cho rằng một đồng xu không có 50% cơ hội mặt ngửa và sẽ từ chối $$H_0$$ và chấp nhận $$H_a$$. Sau đó, một giả thuyết mới sẽ được thử nghiệm, lần này một đồng xu có 40% cơ hội mặt ngửa.

### 4. Các loại lỗi lầm

Trong quá trình đánh giả thuyết, chúng ta thường mắc sai lầm, và nó chia ra làm 2 loại:
- **Type I Error**: Lỗi loại 1 xảy ra khi nhà nghiên cứu bác bỏ $$H_0$$ trong khi $$H_0$$ đúng. Xác suất phạm lỗi loại 1 được gọi là mức ý nghĩa và thường được ký hiệu bằng $$\alpha$$
- **Type II Error**: Lỗi loại 2 xảy ra khi nhà nghiên cứu chấp nhận $$H_0$$ trong khi $$H_0$$ sai. Xác suất phạm lỗi loại 2 được gọi là Beta và thường được ký hiệu bằng $$\beta$$, xác suất không phạm lỗi loại 2 được gọi là "Power of the test"
