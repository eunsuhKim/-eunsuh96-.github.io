---
layout: single #post
title: "SVD from scratch"
date: 2023-10-11
categories: [math]
---

singular value decomposition from scratch with python

얼마 한 arxiv 논문을 읽었는데, \(m\) by \(n\) matrix의 singular value decomposition$($SVD$)$을 활용해서 
저해상도의 이미지를 고해상도로 복원하는 neural net$($구체적으로는 LSTM을 사용$)$을 학습시키는 알고리즘에 관한 것이었다.

실제로 내가 풀어야 하는 문제들은 주로 편미분방정식의 해를 찾거나 $($forward problem$)$, 혹은 해의 data를 활용하여 편미분방정식 파라미터를 infer하는 $($inverse problem$)$ 문제이다.
그래서 이 세팅이 나에게 신선했다. 저자들이 모델을 이용해서 해결하고자 하는 task는 다음과 같다. 

***적은 cost로 얻을 수 있는 low fidelity solution을 만들기만 하면 high fidelity solution으로 바꿔주는 모델을 개발해 보자!!***

이 논문에 관해서 오늘 소개할 것은 아니고, 저자들이 이런 역할을 하는 LSTM neural net을 위한 훈련 데이터 쌍을 구성할 때에 사용된 Singular Value Decomposition $($SVD$)$을 실제로 구현하는 방법에 대하여 알아볼 것이다. python numpy 라이브러리에서 numpy.linalg.svd()라는 함수를 지원하지만, 그것을 바로 쓰기보단 이 함수가 구체적으로 어떤 작업을 하는 것인지 알고 쓰자는 차원에서 이 포스팅을 작성하게 되었다.

특히나 주안점을 둔 부분은 다음과 같다. 

***어떤 임의의 matrix \(A\)가 주어졌을 때 singular value decomposition을 통해서 \(A= U\Sigma V^T\)를 손으로 계산할 수 있을만큼 자세하게 각 step을 구현해 보자.***

그럼 시작해 보자.

# Step 1: Calculate eigenvalues and corresponding eigenvectors
먼저 SVD를 손으로 계산할 수도 있는 예제를 위해서 다음과 같이 \(A\)를 설정하자.

\[A = \begin{bmatrix}1&2&0\\\\0&1&2\end{bmatrix}\]

먼저, \(U\)와 \(V\)의 재료가 될 eigenvector들과 \(\Sigma\)의 재료가 될 eigenvalue들을 구해야 한다. 

어떤 행렬에 대해서냐면, 각각 \(AA^T\)와 \(A^TA\)에 대해서이다. 여기서 기억할 점이 있는데, 이 두 행렬은 같은 non-zero eigenvalue를 공유한다는 사실이다. 즉, 지금은 \(2\times 2\) matrix인 \(AA^T\)의 eigenvalue들은 모두 \(3\times 3\) matrix인 \(A^TA\)의 eigenvalue에 포함된다.

```python
import numpy as np

# 2 by 3 matrix
A = np.array([[1, 2, 0], [0, 1, 2]],dtype=np.float64)
print(f"Given matrix: \n{A}")

# 1. Compute A^T A and A A^T
AtA = np.dot(A.T, A)
AAt = np.dot(A, A.T)

# 2. Compute the eigenvalues and eigenvectors of AtA
eig_vals_v, eig_vecs_v = np.linalg.eig(AtA)

# 3. Compute the eigenvalues and eigenvectors of AAt
eig_vals_u, eig_vecs_u = np.linalg.eig(AAt)
print(eig_vals_u)
print(eig_vecs_u)

# 4. Singular values are the square root of the eigenvalues of AtA
small_dim = np.min(A.shape)
print(f"Smaller dimension: {small_dim}")
if A.shape[0]>A.shape[1]:
    print("hi")
    eig_vals_u = np.maximum(eig_vals_u, 0)
    singular_vals = np.sqrt(eig_vals_u)
else:
    print("hello")
    eig_vals_v = np.maximum(eig_vals_v, 0)
    singular_vals = np.sqrt(eig_vals_v)

print(f"Sigular values:{singular_vals}")

# Ordering V's eigenvectors based on the actual value of singular values
order_v = np.argsort(eig_vals_v)[::-1]
singular_vals = singular_vals[order_v]

eig_vecs_v = eig_vecs_v[:, order_v]

# Ordering U's eigenvectors based on AAt's eigenvalues
order_u = np.argsort(eig_vals_u)[::-1]

eig_vecs_u = eig_vecs_u[:, order_u]


# QR 분해를 사용하여 V 직교화
Qv, Rv = np.linalg.qr(eig_vecs_v)
Qu, Ru = np.linalg.qr(eig_vecs_u)

U = Qu
V = Qv

# Considering only the top 'm' singular values (where 'm' is the number of rows in A)
singular_vals = singular_vals[:small_dim]

Sigma = np.zeros(A.shape)
for i in range(len(singular_vals)):
    Sigma[i, i] = singular_vals[i]

print("U:")
print(U)
print("\nSigma:")
print(Sigma)
print("\nV^T:")
print(V.T)
# print("\n")

print(f"A reconstruction =\n {np.matmul(np.matmul(U,Sigma),V.T)}")

u,sigma,vt = np.linalg.svd(A)
print(f"Result using np.linalg.svd =\n {np.matmul(np.matmul(u,np.concatenate([np.diag(sigma),np.zeros((2,1))],axis=1)),vt)}")
```
