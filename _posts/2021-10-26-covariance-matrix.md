---
layout: post
author: nvip
title: Cách tính và ý nghĩa ma trận hiệp phương sai (covariance matrix)
categories: Math
---
# Note
Bài viết này mình không nói sâu về lý thuyết mà tập trung giải thích về các bước tính toán ma trận hiệp phương sai, cũng như giải thích ý nghĩa của ma trận này để bạn cảm thấy dễ nhớ hơn là việc học thuộc công thức. Cách hiểu này cũng sẽ hỗ trợ bạn trong việc ứng dụng, khi nào áp dụng việc tính toán covariance matrix trong quá trình làm nghiên cứu.

# 1. Ma trận hiệp phương sai là gì?

> `Ma trận hiệp phương sai` của tập hợp m biến ngẫu nhiên là một ma trận vuông hạng (m × m), trong đó các phần tử nằm trên đường chéo (từ trái sang phải, từ trên xuống dưới) lần lượt là phương sai tương ứng của các biến này (ta chú ý rằng Var(X) = Cov(X,X)), trong khi các phần tử còn lại (không nằm trên đường chéo) là các hiệp phương sai của đôi một hai biến ngẫu nhiên khác nhau trong tập hợp.

Nguồn: [Ma trận hiệp phương sai - Wikipedia](https://vi.wikipedia.org/wiki/Ma_tr%E1%BA%ADn_hi%E1%BB%87p_ph%C6%B0%C6%A1ng_sai)

# 2. Ví dụ cách tính ma trận hiệp phương sai

Định nghĩa ma trận hiệp phương sai có vẻ khó hiểu, nhưng khi ta xem xét một bài toán cụ thể thì sẽ dễ hiểu hơn. Ta xem xét ví dụ sau và cách tính toán ma trận hiệp phương sai.
Ta có 3 mẫu dữ liệu sau:

A = (-2, -2) B = (-1, 4) C = (2, 3)

Như vậy ta có N mẫu dữ liệu (N=3), và mỗi mẫu dữ liệu là một điểm trên không gian 2 chiều (m=2). Nếu trực quan hóa thì 3 điểm dữ liệu A, B, C sẽ nằm như sau trên trục tọa độ:
<img src='/assets/img/20211026_covariance_matrix/2D_ABC_3dots.png' width="600px" style="display:block; margin-left:auto; margin-right:auto"/>
Để tính toán ma trận hiệp phương sai kích thước mxm (2x2), ta làm như sau:

`I. Sắp mẫu dữ liệu thành ma trận m x N`
Với 3 mẫu dữ liệu trên, ta tìm cách sắp chúng lại thành ma trận có kích thước m x N (2 dòng, 3 cột). Để làm điều đó dễ dàng, ta sắp chúng thành ma trận có kích thước N x m trước, sau đó chuyển vị để được ma trận m x N.
Nhắc lại:

A = (-2, -2) B = (-1, 4) C = (2, 3)

Ma trận N x m:

$$\begin{bmatrix}-2&-2\\-1&4\\2&3\end{bmatrix}$$

Chuyển vị ma trận N x m thành ma trận m x N, đặt tên là K:

$$K = \begin{bmatrix}-2&-1&2\\-2&4&3\end{bmatrix}$$

Ma trận K có kích thước m x N (2x3) với m là số chiều của mẫu dữ liệu, N là số mẫu dữ liệu.

`II. Tính mẫu trung bình`

Do mỗi điểm của chúng ta nằm trên không gian 2 chiều (m=2), do đó khi ta tìm trọng tâm M (giá trị trung bình của N mẫu trên không gian m chiều, tạm gọi nó là mẫu trung bình) thì trọng tâm này cũng là 2 chiều.

Mx = ((-2) + (-1) + 2) / 3 = -1/3 = -0.33 (đã làm tròn)

My = ((-2) + 4 + 3) / 3 = 5/3 = 1.67 (đã làm tròn)

M = (Mx, My) = (-0.33, 1.67)

Nói cách khác, để tính M, ta tính trung bình trên từng dòng của ma trận K. Kết quả biểu diễn dưới dạng ma trận:

$$K = \begin{bmatrix}-2&-1&2\\-2&4&3\end{bmatrix}, M = \begin{bmatrix}-0.33\\1.67\end{bmatrix}$$

`III. Trừ mỗi mẫu với giá trị trung bình để tìm độ lệch`

Ta nhân bản ma trận M thành tương ứng N mẫu được ma trận M2:

$$M_2 = \begin{bmatrix}-0.33&-0.33&-0.33\\1.67&1.67&1.67\end{bmatrix}$$

Sau đó trừ từng phân tử của ma trận M với từng phân tử tương ứng của ma trận M2:

$$D = K - M_2 = \begin{bmatrix}-1.67&-0.67&2.33\\-3.67&2.33&1.33\end{bmatrix}$$

`IV. Tính ma trận hiệp phương sai m x m`

Ma trận hiệp phương sai C:


$$C = \frac{1}{N-1} * D * D^T = \frac{1}{3-1} \begin{bmatrix}-1.67&-0.67&2.33\\-3.67&2.33&1.33\end{bmatrix} * \begin{bmatrix}-1.67&-3.67\\-0.67&2.33\\2.33&1.33\end{bmatrix} = \frac{1}{2} \begin{bmatrix}c_{11} & c_{12} \\ c_{21} & c_{22}\end{bmatrix}$$

Nhắc lại phép nhân ma trận:
Ma trận A có kích thước **m x N**, ma trận B có kích thước **N x m** => ma trận kết quả **C = A * B** có kích thước **m x m**.

$$c_{12} = (-1.67)*(-3.67) + (-0.67)*(2.33) + (2.33)*(1.33) = 7.67$$
$$c_{11} = (-1.67)*(-1.67) + (-0.67)*(-0.67) + (2.33)*(2.33) = 8.67$$
$$c_{21} = (-3.67)*(-1.67) + (2.33)*(-0.67) + (1.33)*(2.33) = 7.67$$
$$c_{22} = (-3.67)*(-3.67) + (2.33)*(2.33) + (1.33)*(1.33) = 20.67$$

Vậy ma trận hiệp phương sai C là:

$$C = \frac{1}{2} \begin{bmatrix} 8.67 & 7.67 \\ 7.67 & 20.67 \end{bmatrix} = \begin{bmatrix} 4.33 & 3.835 \\ 3.835 & 10.33 \end{bmatrix}$$


`V. Nhận xét ma trận hiệp phương sai (covariance matrix)`

- $$c_{11}$$ và $$c_{22}$$ lần lượt là phương sai (variance) của trục X và trục Y. Nói cách khác, các phần tử trên đường chéo chính của ma trận hiệp phương sai là các phương sai của các mẫu dữ liệu.
- Ma trận hiệp phương sai có tính chất đối xứng qua đường chéo chính. Lý do: bạn sẽ để ý rằng  $$c_{11}$$ và $$c_{22}$$  được tính bởi tích vô hướng của 2 vector $$r_1*r_2$$  và $$r_2*r_1$$ đều cho ra kết quả tính toán như nhau.

# 3. Ý nghĩa ma trận hiệp phương sai

Đây là nhận xét chủ quan của mình đúc kết về **ý nghĩa của ma trận hiệp phương sai** dựa trên quá trình tính toán trong ví dụ phía trên.
- Các phần tử trên đường chéo chính của ma trận hiệp phương sai lần lượt là các phương sai của các mẫu dữ liệu theo từng chiều trong không gian m chiều.
- Ma trận hiệp phương sai có tính chất đối xứng qua đường chéo chính.
- Có thể tạm hiểu rằng, độ lớn về giá trị của mỗi phần tử  $$c_{xy}$$ trong ma trận hiệp phương sai thể hiện mức độ tương quan (thể hiện bởi phép nhân vô hướng, tiếng Anh: dot product) về độ lệch (thao tác trừ cho giá trị trung bình => mình tạm gói nó là "độ lệch") của các mẫu dữ liệu theo chiều $$x$$ (dòng thứ x trong ma trận hiệp phương sai) và chiều $$y$$  (cột thứ y trong ma trận hiệp phương sai)

# 4. Kiểm chứng kết quả tính toán ma trận hiệp phương sai bằng lập trình (covariance matrix)

Ta có thể dùng ngôn ngữ lập trình Python và thư viện hỗ trợ Numpy để kiểm chứng kết quả tính toán ma trận hiệp phương sai bằng đoạn code như sau:

```python

import numpy as np

x = np.array([[-2, -2], [-1, 4], [2, 3]])
cov = np.cov(x.T)
print('cov:')
print(cov)

$ python cov.py
cov
[[ 4.33333333  3.83333333]
 [ 3.83333333 10.33333333]]

```
