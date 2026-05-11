---

---
Note: the logic of Numpy arrays also applies to tensors in`torch.tensor()`
- **Scalar** (1D vector of length 1)

```python
>>> import numpy as np
>>> a = np.array(3)
>>> a.shape
()
>>> a.ndim
0
```
- **1D vector**

```python
>>> import numpy as np
>>> a = np.array([3,6,7])
>>> a.shape
(3,)
>>> a.ndim
1
```
Note that `np.array([3])` is still a 1d vector of length 1
- 2D vector

```python
>>> a = np.array([[3,5,7],
									[11,13,17]])
>>> a.shape
(2,3)
>>> a.ndim
2

>>> a = np.array([[3,5,7]])
>>> a.shape
(1,3)
>>> a.ndim
2
# still a 2D vector (column vector)


>>> a = np.array([[3]])
>>> a.shape
(1,1)
>>> a.ndim
2
# still a 2D vector
```
## Difference between 1d and 2d arrays
- 90 degree transformation

```python
# 1D array
>>> a = np.array([3,6,7])
>>> a.T
array([3,6,7])

# 2D array
>>> a = np.array([[3,6,7]])
>>> a.T
array([[3],
			 [6],
			 [7]])
```
- Broadcasting

```python
>>> a = np.array([[3,5,7],
    							[11,13,17]])
>>> a.shape
(2,3)

>>> b = np.array([0.1, 0.2, 0.3])
>>> b.shape
(3,)


>>> a + b
array([[ 3.1,  5.2,  7.3],
       [11.1, 13.2, 17.3]])
# a 2d array of shape (1,3) would broadcast fine       
>>> b = np.array([[0.1],
                  [0.2],
                  [0.3]])
>>> b.shape
(3,1)

>>> a + b
ValueError: operands could not be broadcast together with shapes (2,3) (3,1) 
```
