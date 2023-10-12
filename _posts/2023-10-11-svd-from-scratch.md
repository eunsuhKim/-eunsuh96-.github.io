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


---

잠시 곁가지로 빠져서 \(AA^T\)와 \(A^TA\)가 같은 non-zero eigenvalue들을 공유하는 이유에 대해서 살펴보자. 여기서 기억해야 할 어떤 행렬 \(M\in\mathbb{R}^{n\times n}\)eigenvector \(\lambda_M\in\mathbb{R}\)의 정의는 "\(Mx=\lambda_M v\) for some nonzero vector \(v\in\mathbb{R}^n\)"이다. $(n$은 자연수이다.$)$

\(A^TA\)의 eigenvalue 하나를 \(\lambda\)라고 하자. 즉 다음이 성립한다.

\[A^TAx = \lambda x\text{ for some nonzero vector }x\in\mathbb{R}^2\]

이제 양변에 \(A\)를 곱하면

\[AA^T(Ax) = \lambda (Ax)\]

이며, \(Ax\)가 만약 zero vector라면 \(A^TAx=A^T\boldsymbol{0}=\boldsymbol{0}=\lambda x\)이어서 \(x\)가 zero vector라는 모순이 나오므로 \(\lambda\)는 \(AA^T\)의 eigenvalue도 된다. 

반대로 \(AA^T\)의 eigenvalue 하나를 \(\lambda\)라고 하자. 즉 다음이 성립한다.

\[AA^Tx = \lambda x\text{ for some nonzero vector }x\in\mathbb{R}^2\]

양변에 \(A^T\)를 곱하면

\[A^TA(A^Tx)=\lambda(A^Tx)\]

이며, \(A^Tx\)가 만약 zero vector라면 \(AA^Tx=A\boldsymbol{0}=\boldsymbol{0}=\lambda x\)이어서 \(x\)가 zero vector라는 모순이 나오므로 \(\lambda\)는 \(A^TA\)의 eigenvalue도 된다. 

따라서 \(AA^T\)와 \(A^TA\)는 non-zero eigenvalue들을 서로 공유할 수밖에 없다. 

---

다시 원래의 eigenvalue & eigenvector 계산 과정으로 돌아가 보자.

사실 아래의 python 코드에서는 numpy linalg 라이브러리의 함수를 써서 계산할 것이지만 우선 손으로 계산한다면 어떤 과정을 거쳐야 하는지를 살펴보자.

위에서 살펴보았듯이 \(AA^T\)와 \(A^TA\)의 non-zero eigenvalue set은 같으므로 두 행렬 중 크기가 작은 행렬을 선택해서 eigen-analysis를 하는 것이 좋다. 지금은 \(A\in\mathbb{R}^{2\times 3}\)이므로 \(2\times 2\)행렬인 \(AA^T=\begin{bmatrix}1&2&0\\\\0&1&2\end{bmatrix}\begin{bmatrix}1&0\\\\2&1\\\\0&2\end{bmatrix}=\begin{bmatrix}5&2\\\\2&5\end{bmatrix}\)를 이용해 보자. 

\[\begin{aligned}\det\begin{bmatrix}5-\lambda&2\\\\2&5-\lambda\end{bmatrix}&=25+\lambda^2-10\lambda-4 \\\\&= \lambda^2-10\lambda+21=0\\\\&\leftrightarrow \lambda=7\text{ or }\lambda=3.\end{aligned}\]

이제 각 non-zero eigenvalue들에 correponding하는 eigenvector를 \(AA^T\)와 \(A^TA\)에 대하여 구해 보자.

## \(AA^T\)의 경우

먼저 $( AA^T-\lambda I )x=\begin{bmatrix}5-7&2\\\\2&5-7\end{bmatrix}x=\boldsymbol{0} $을 만족하는 \(x\)를 하나 찾아보면 \(x=\begin{bmatrix}1\\\\1\end{bmatrix}\)이 있고, 

$( AA^T-\lambda I )x=\begin{bmatrix}5-3&2\\\\2&5-3\end{bmatrix}x=\boldsymbol{0}$을 만족하는 \(x\)를 하나 찾아보면 \(x=\begin{bmatrix}1\\\\-1\end{bmatrix}\)이 있다.

## \(A^TA\)의 경우

$(A^TA-\lambda I)x = \begin{bmatrix}1-7&2&0\\\\2&5-7&2\\\\0&2&4-7\end{bmatrix}x=\boldsymbol{0}$을 만족하는 \(x\)를 하나 찾아보면 \(x=\begin{bmatrix}1\\\\3\\\\2\end{bmatrix}\)이 있고,

$(A^TA-\lambda I)x = \begin{bmatrix}1-3&2&0\\\\2&5-3&2\\\\0&2&4-3\end{bmatrix}x=\boldsymbol{0}$을 만족하는 \(x\)를 하나 찾아보면 \(x=\begin{bmatrix}1\\\\1\\\\-2\end{bmatrix}\)이 있고,

$(A^TA-\lambda I)x = \begin{bmatrix}1-0&2&0\\\\2&5-0&2\\\\0&2&4-0\end{bmatrix}x=\boldsymbol{0}$을 만족하는 \(x\)를 하나 찾아보면 \(x=\begin{bmatrix}4\\\\-2\\\\1\end{bmatrix}\)이 있다.

# Step 2 : \(U,V\) construction
위에서 구한 eigenvector들을 활용하여 orthogonal matrix \(U\)를 만들면 된다.
사실 이 과정은 아래 python code 에서는 numpy linalg 라이브러리의 qr decomposition 함수를 사용하여 계산할 것이지만, 이 함수가 어떤 역할을 하는지 구체적으로 살펴 보자.

## \(U\)
Gram-Schmidt algorithm을 활용하여 orthogonalization을 해보자.

위에서 찾은 두 개의 벡터를 \(a_1=[1, 1]^T,a_2=[1, -1]^T\)라고 하자. 

\(q_1 = \frac{a_1}{\parallel a_1\parallel}=[\frac{1}{\sqrt{2}}, \frac{1}{\sqrt{2}}]^T\)

$u_2 = a_2 - (a_2\cdot q_1)q_1 = [1, -1]^T - \begin{bmatrix}    1 \\\\ -1\end{bmatrix}\cdot \begin{bmatrix}\frac{1}{\sqrt{2}}\\\\\frac{1}{\sqrt{2}}\end{bmatrix} = [1,-1]^T$

\(q_2 = \frac{u_2}{\parallel u_2\parallel} = [\frac{1}{\sqrt{2}},-\frac{1}{\sqrt{2}}]^T\)

\(U:=\begin{bmatrix}q_1&q_2\end{bmatrix} = \begin{bmatrix}\frac{1}{\sqrt{2}}&\frac{1}{\sqrt{2}}\\\\ \frac{1}{\sqrt{2}}& -\frac{1}{\sqrt{2}}\end{bmatrix}\)

## \(V\)
마찬가지로 Gram-Schmidt algorithm을 활용하여 orthonormalization을 해보자.

위에서 찾은 세 개의 벡터를 \(a_1=[1, 3, 2]^T,a_2=[1, 1, -2]^T,a_3=[4, -2, 1]^T\)라고 하자.

\(q_1 = \frac{a_1}{\parallel a_1\parallel}=[\frac{1}{\sqrt{14}}, \frac{3}{\sqrt{14}}, \frac{2}{\sqrt{14}}]^T\)

$u_2 = a_2 - (a_2\cdot q_1)q_1 = [1, 1, -2]^T - \begin{bmatrix}    1 \\\\ 1\\\\2\end{bmatrix}\cdot \begin{bmatrix}\frac{1}{\sqrt{14}}\\\\ \frac{3}{\sqrt{14}}\\\\ \frac{2}{\sqrt{14}}\end{bmatrix} = [1,1,-2]^T $

\(q_2 = \frac{u_2}{\parallel u_2\parallel} = [\frac{1}{\sqrt{6}},\frac{1}{\sqrt{6}},-\frac{1}{\sqrt{6}}]^T\)

$u_3 = a_3 - (a_3\cdot q_1)q_1- (a_3\cdot q_2)q_2 = [4, -2, 1]^T - \begin{bmatrix}    4 \\\\ 2\\\\1\end{bmatrix}\cdot \begin{bmatrix}\frac{1}{\sqrt{14}}\\\\ \frac{3}{\sqrt{14}}\\\\ \frac{2}{\sqrt{14}}\end{bmatrix}  -\begin{bmatrix}    4 \\\\ 2\\\\1\end{bmatrix}\cdot \begin{bmatrix}\frac{1}{\sqrt{6}}\\\\ \frac{1}{\sqrt{6}}\\\\ -\frac{2}{\sqrt{6}}\end{bmatrix}  = [4,2,1]^T $

\(q_3 = \frac{u_3}{\parallel u_3\parallel} = [\frac{4}{\sqrt{21}},\frac{2}{\sqrt{21}},\frac{1}{\sqrt{21}}]^T\)


\(V:=\begin{bmatrix}q_1&q_2&q_3\end{bmatrix} = \begin{bmatrix}\frac{1}{\sqrt{14}}&\frac{1}{\sqrt{6}}&\frac{4}{\sqrt{21}}\\\\ \frac{3}{\sqrt{14}}& \frac{1}{\sqrt{6}}&\frac{2}{\sqrt{21}}\\\\ \frac{2}{\sqrt{14}}& -\frac{2}{\sqrt{6}}&\frac{1}{\sqrt{21}}\end{bmatrix}\)

공교롭게도 \(U\)와 \(V\)의 재료인 eigenvector들끼리 서로 orthogonal했어서 각각을 unit vector로만 만들어주면 되었다. 그리고 이 과정에서 \(U\)와 \(V\)의 eigenvector들을, eigenvalue의 크기 순으로 자연스럽게 배열하였다. 아래 코드에서는 QR decomposition을 활용하여 orthonormal matrix \(Q\)를 찾는 위 과정을 대신하였다.

# Step 3 : \(\Sigma\) construction

\(\Sigma\) 행렬을 구하기 위해서는 아래와 같이 diagonal 성분에 큰 순서대로 non-zero eigenvalue들을 넣어주면 된다. 이외의 element들은 0으로 두면 된다.

\[\Sigma = \begin{bmatrix}7&0&0\\\\0&3&0\end{bmatrix}\]


```python
import numpy as np

# 2 by 3 matrix
A = np.array([[1, 2, 0], [0, 1, 2]],dtype=np.float64)
print(f"Given matrix: \n{A}")

# 1. Compute the eigenvalues and eigenvectors of AtA and AAt
AtA = np.dot(A.T, A)
AAt = np.dot(A, A.T)

eig_vals_v, eig_vecs_v = np.linalg.eig(AtA)
eig_vals_u, eig_vecs_u = np.linalg.eig(AAt)


# 2. Singular values are the square root of the eigenvalues of AtA
small_dim = np.min(A.shape)
print(f"Smaller dimension: {small_dim}")
if A.shape[0]>A.shape[1]:
    eig_vals_u = np.maximum(eig_vals_u, 0)
    singular_vals = np.sqrt(eig_vals_u)
else:
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

실행 결과는 다음과 같다. 
```bash
Given matrix: 
[[1. 2. 1.]
 [0. 1. 2.]]
[9.53112887 1.46887113]
[[ 0.74967818 -0.66180256]
 [ 0.66180256  0.74967818]]
Smaller dimension: 2

Sigular values:[3.08725264e+00 1.66249066e-08 1.21196994e+00]
U:
[[-0.74967818 -0.66180256]
 [-0.66180256  0.74967818]]

Sigma:
[[3.08725264 0.         0.        ]
 [0.         1.21196994 0.        ]]

V^T:
[[-0.2428302  -0.70002658 -0.67156256]
 [-0.54605526 -0.47354883  0.69106812]
 [-0.80178373  0.53452248 -0.26726124]]
A reconstruction =
 [[ 1.0000000e+00  2.0000000e+00  1.0000000e+00]
 [-2.5848809e-16  1.0000000e+00  2.0000000e+00]]
Result using np.linalg.svd =
 [[1.00000000e+00 2.00000000e+00 1.00000000e+00]
 [3.27147417e-16 1.00000000e+00 2.00000000e+00]]
 ```