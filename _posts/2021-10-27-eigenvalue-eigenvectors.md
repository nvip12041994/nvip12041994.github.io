---
layout: post
author: nvip
title: Trị riêng và vector riêng của ma trận
categories: Math
---

# Trị riêng và vector riêng

## **1. Định nghĩa:**
- 
  Cho một ma trận vuông A kích thước $m \times n$, vector cột $v$ có kích thước $n\times1$ và một số vô hướng $\lambda$. Nếu $Av = \lambda v $ thì $v$ là vector riêng của $A$ và $\lambda$ là trị riêng của $A$.

## **2. Cách tìm trị riêng, vector riêng:**
  - Để tìm trị riêng và vector riêng, ta giải phương trình sau:
      $$det |A-\lambda I| = 0$$ (1)
  - Trong đó $I$ là ma trận đơn vị.

## **3. Ví dụ:**
  - Cho ma trận A như sau:
  
    $$
    A=\begin{bmatrix} 5 & 2 \\[0.3em] 9 & 2 \end{bmatrix}
    $$
    
  - Theo (1), ta cần giải phương trình sau:
    $$
    \begin{aligned} det|a-\lambda I| &= det \Bigg|\begin{bmatrix} 5 & 2 \\[0.3em] 9 & 2 \end{bmatrix} - \begin{bmatrix} \lambda & 0 \\[0.3em] 0 & \lambda \end{bmatrix} \Bigg| = det \Bigg| \begin      {bmatrix} 5-\lambda & 2 \\[0.3em] 9 & 2-\lambda \end{bmatrix} \Bigg| \\ &= (5-\lambda)(2-\lambda)-18 = \lambda^2-7\lambda-8=(\lambda-8)(\lambda+1) = 0 \end{aligned}
    $$
  - Ta có 2 trị riêng như sau: $\lambda_1=8,\lambda_2=-1$
    - Với $\lambda_1=8$:
  
        $$
        \begin{aligned} Av &= \begin{bmatrix} 5 & 2 \\[0.3em] 9 & 2 \end{bmatrix} \begin{bmatrix} x \\[0.3em] y \end{bmatrix} = 8 \begin{bmatrix} x \\[0.3em] y \end{bmatrix} \\ &\Rightarrow \begin{bmatrix} 5x+2y \\[0.3em] 9x+2y \end{bmatrix} = 8 \begin{bmatrix} x \\[0.3em] y \end{bmatrix} \end{aligned}
        $$ (2)
    - Từ (2), ta có $y=3x/2$.Ta chọn $x=2,y=3$. Do đó vector riêng ứng với $\lambda_1=8$ sẽ là:

    $$
    \Rightarrow v_1= \begin{bmatrix} 2 \\[0.3em] 3 \end{bmatrix}
    $$

    Chú ý: do (2) là hệ phương trình thuần nhất nên có vô số nghiệm.

    Tương tự với $\lambda_2=-1$
    $$
    \Rightarrow v_2= \begin{bmatrix} 1 \\[0.3em] -3 \end{bmatrix}
    $$

## **4. Hiện thực:**

Đoạn code sau sử dụng thư viện **numpy** của python để tìm trị riêng và vector riêng của một ma trận:

```python
import numpy as np
from numpy import linalg as la

w, v = la.eig(np.array([[5,2],[9,2]]))

# Danh sách trị riêng
print("Eigenvalues: ")
print(w)
# Danh sách vector riêng
print("Eigenvectors: ")
print(v)
```
Kết quả:

```python
Eigenvalues
[ 8. -1.]
Eigenvectors:
[[ 0.5547002  -0.31622777]
[ 0.83205029  0.9486833 ]]
```