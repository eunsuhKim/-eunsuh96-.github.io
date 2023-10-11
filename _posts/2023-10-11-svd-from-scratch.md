---
layout: single #post
title: "SVD from scratch"
date: 2023-10-11
categories: [math]
---

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