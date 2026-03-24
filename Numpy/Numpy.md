<div align="center">

# <span style="color:#0A2FA8">NumPy</span>

<sub>NumPy: arrays, indexing, operations, broadcasting, and more</sub>

</div>

---

## <span style="color:#1565C0">1. What is NumPy?</span>

> **Definition:** NumPy (Numerical Python) is a core Python library for numerical computing. It provides the `ndarray` object : a fast, flexible, multi-dimensional array : along with a large collection of mathematical functions to operate on arrays efficiently.

**Why NumPy over Python lists?**

| Feature | Python List | NumPy Array |
|:---|:---:|:---:|
| Speed | Slow (loop-based) | Fast (vectorized C) |
| Memory | High | Low |
| Math operations | Manual loops | Built-in, element-wise |
| Multi-dimensional | Nested lists only | Native nD support |
| Data type | Mixed | Homogeneous |

```python
import numpy as np
```

---

## <span style="color:#1565C0">2. Creating Arrays</span>

### <span style="color:#2E86AB">2.1 From Python Lists</span>

```python
arr = np.array([1, 2, 3, 4])           # 1D array
matrix = np.array([[1, 2], [3, 4]])    # 2D array (matrix)
arr_3d = np.array([[[1,2],[3,4]],[[5,6],[7,8]]])  # 3D array
```

### <span style="color:#2E86AB">2.2 Built-in Creation Functions</span>

| Function | Description | Example |
|:---|:---|:---|
| `np.zeros(n)` | Array of zeros | `np.zeros(5)` → `[0. 0. 0. 0. 0.]` |
| `np.ones((r,c))` | Array of ones | `np.ones((2,3))` → 2×3 matrix of 1.0 |
| `np.full(shape, val)` | Array filled with a value | `np.full((2,2), 7)` |
| `np.eye(n)` | Identity matrix | `np.eye(3)` → 3×3 identity |
| `np.empty(shape)` | Uninitialized array | `np.empty((2,2))` |
| `np.arange(start, stop, step)` | Range of values | `np.arange(0, 10, 2)` → `[0 2 4 6 8]` |
| `np.linspace(start, stop, n)` | n evenly spaced values | `np.linspace(0, 1, 10)` |

```python
np.zeros(5)               # [0. 0. 0. 0. 0.]
np.ones((2, 3))           # 2 rows, 3 cols of 1.0
np.arange(0, 10, 2)       # [0, 2, 4, 6, 8]
np.linspace(0, 1, 10)     # 10 values from 0 to 1 inclusive
```

### <span style="color:#2E86AB">2.3 Random Arrays</span>

| Function | Description |
|:---|:---|
| `np.random.random(n)` | n random floats between 0 and 1 |
| `np.random.randn(n)` | n samples from standard normal distribution (mean=0, std=1) |
| `np.random.randint(low, high, size)` | Random integers in a range |
| `np.random.seed(n)` | Set seed for reproducibility |

```python
np.random.random(5)        # [0.08, 0.91, 0.20, ...]
np.random.randn(5)         # Values from standard normal dist
np.random.randint(1, 10, 5)# 5 random ints between 1–9
np.random.seed(42)         # Reproducible random numbers
```

---

## <span style="color:#1565C0">3. Array Attributes</span>

> **Definition:** Attributes are properties of an array object that describe its structure : they do not require parentheses (no function call needed).

```python
arr = np.array([[1,2,3,4],[5,6,7,8],[9,10,11,12]])
```

| Attribute | Returns | Example Output |
|:---|:---|:---|
| `arr.shape` | Tuple of dimensions | `(3, 4)` |
| `arr.size` | Total number of elements | `12` |
| `arr.ndim` | Number of dimensions | `2` |
| `arr.dtype` | Data type of elements | `dtype('int64')` |
| `arr.itemsize` | Size of each element (bytes) | `8` |
| `arr.nbytes` | Total bytes consumed | `96` |
| `arr.strides` | Bytes to step per dimension | `(32, 8)` |
| `arr.T` | Transposed array | Rows ↔ Columns |
| `arr.real` | Real part of array | Same array (if no complex) |
| `arr.data` | Memory buffer location | `<memory at 0x...>` |

```python
arr.shape      # (3, 4)
arr.size       # 12
arr.ndim       # 2
arr.dtype      # dtype('int64')
arr.strides    # (32, 8)
arr.T          # Transposed matrix
```

> **Note on strides:** `(32, 8)` means moving to the next row costs 32 bytes, moving to the next column costs 8 bytes (since int64 = 8 bytes).

---

## <span style="color:#1565C0">4. Array Methods</span>

### <span style="color:#2E86AB">4.1 Statistical Methods</span>

```python
arr = np.array([[1,2,3],[4,5,6],[7,8,9]])
```

| Method | Description | Result |
|:---|:---|:---|
| `arr.min()` | Minimum value | `1` |
| `arr.max()` | Maximum value | `9` |
| `arr.sum()` | Sum of all elements | `45` |
| `arr.mean()` | Mean (average) | `5.0` |
| `arr.std()` | Standard deviation | `2.58` |
| `arr.var()` | Variance | `6.67` |
| `arr.argmin()` | Index of minimum value | `0` |
| `arr.argmax()` | Index of maximum value | `8` |
| `arr.cumsum()` | Cumulative sum | `[1,3,6,10,...]` |
| `arr.cumprod()` | Cumulative product | `[1,2,6,24,...]` |

```python
arr.min()       # 1
arr.max()       # 9
arr.sum()       # 45
arr.mean()      # 5.0
arr.std()       # 2.581988897471611
arr.argmax()    # 8  (flat index of max element)
```

**Axis-specific operations:**

```python
arr.sum(axis=0)   # Sum along columns → [12, 15, 18]
arr.sum(axis=1)   # Sum along rows    → [6, 15, 24]
arr.min(axis=1)   # Min of each row   → [1, 4, 7]
```

### <span style="color:#2E86AB">4.2 Shape Manipulation Methods</span>

| Method | Description |
|:---|:---|
| `arr.reshape(r, c)` | Reshape to new dimensions (total elements must match) |
| `arr.flatten()` | Flatten to 1D (returns copy) |
| `arr.ravel()` | Flatten to 1D (returns view if possible) |
| `arr.squeeze()` | Remove dimensions of size 1 |
| `arr.expand_dims(axis)` | Add a new axis |
| `arr.resize(shape)` | Resize in-place |

```python
arr.reshape(9, 1)    # 9 rows, 1 column
arr.reshape(1, 9)    # 1 row, 9 columns
arr.reshape(-1)      # Flatten to 1D (-1 = auto-calculate)
arr.flatten()        # [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

<div align="center" style="border: 2px solid #D4A017; border-radius: 8px; padding: 14px 24px; margin: 12px auto; max-width: 480px;">

### <span style="color:#D4A017">reshape(r, c) → r × c must equal arr.size</span>

</div>

---

## <span style="color:#1565C0">5. Indexing and Slicing</span>

### <span style="color:#2E86AB">5.1 1D Array Indexing</span>

```python
arr = np.array([1, 2, 3, 4])
```

| Expression | Result | Meaning |
|:---|:---:|:---|
| `arr[0]` | `1` | First element |
| `arr[-1]` | `4` | Last element |
| `arr[:2]` | `[1, 2]` | First two elements |
| `arr[1:]` | `[2, 3, 4]` | From index 1 onwards |
| `arr[:-1]` | `[1, 2, 3]` | All except last |
| `arr[0:2]` | `[1, 2]` | Index 0 to 1 (stop excluded) |
| `arr[::-1]` | `[4, 3, 2, 1]` | Reversed array |
| `arr[::2]` | `[1, 3]` | Every 2nd element |

<div align="center" style="border: 2px solid #D4A017; border-radius: 8px; padding: 14px 24px; margin: 12px auto; max-width: 480px;">

### <span style="color:#D4A017">arr[start : stop : step]</span>

</div>

### <span style="color:#2E86AB">5.2 2D Array (Matrix) Indexing</span>

```python
arr = np.arange(1, 10).reshape(3, 3)
# [[1 2 3]
#  [4 5 6]
#  [7 8 9]]
```

| Expression | Result | Meaning |
|:---|:---|:---|
| `arr[2]` | `[7, 8, 9]` | Entire last row |
| `arr[1, 1]` | `5` | Row 1, Column 1 |
| `arr[0, :]` | `[1, 2, 3]` | Entire first row |
| `arr[:, 0]` | `[1, 4, 7]` | Entire first column |
| `arr[0:2, 0:2]` | `[[1,2],[4,5]]` | Sub-matrix (first 2×2) |
| `arr[-1, -1]` | `9` | Last element |
| `arr[:, 1]` | `[2, 5, 8]` | Second column |

```python
arr[1, 1]       # 5  : element at row=1, col=1
arr[0:2, 0:2]   # [[1,2],[4,5]] : top-left 2×2 block
arr[:, 0]       # [1, 4, 7]    : first column
```

### <span style="color:#2E86AB">5.3 Boolean (Fancy) Indexing</span>

> **Definition:** Boolean indexing uses a boolean array (True/False mask) to filter elements from an array.

```python
arr = np.arange(1, 13)
boolean_arr = arr > 5       # [F, F, F, F, F, T, T, T, T, T, T, T]
filtered = arr[boolean_arr] # [6, 7, 8, 9, 10, 11, 12]

# One-liner version:
arr[arr > 5]    # same result
arr[arr % 2 == 0]  # only even numbers
```

### <span style="color:#2E86AB">5.4 Fancy Indexing (Integer Array Indexing)</span>

```python
arr = np.array([10, 20, 30, 40, 50])
arr[[0, 2, 4]]      # [10, 30, 50] : pick specific indices
arr[[1, 1, 3]]      # [20, 20, 40] : can repeat indices
```

---

## <span style="color:#1565C0">6. Array Operations</span>

### <span style="color:#2E86AB">6.1 Arithmetic Operations (Element-wise)</span>

```python
arr1 = np.array([1, 2, 3, 4, 5])
arr2 = np.array([6, 7, 8, 9, 10])
```

| Operation | Code | Result |
|:---|:---|:---|
| Addition | `arr1 + arr2` | `[7, 9, 11, 13, 15]` |
| Subtraction | `arr1 - arr2` | `[-5, -5, -5, -5, -5]` |
| Multiplication | `arr1 * arr2` | `[6, 14, 24, 36, 50]` |
| Division | `arr1 / arr2` | `[0.16, 0.28, 0.37, 0.44, 0.5]` |
| Floor Division | `arr1 // arr2` | `[0, 0, 0, 0, 0]` |
| Modulo | `arr1 % arr2` | `[1, 2, 3, 4, 5]` |
| Power | `arr1 ** 2` | `[1, 4, 9, 16, 25]` |

### <span style="color:#2E86AB">6.2 Boolean Operations</span>

```python
arr1 > 3         # [False, False, False, True, True]
arr1 == arr2     # Element-wise equality
arr1 != arr2     # Element-wise inequality
(arr1 > 2) & (arr1 < 5)   # AND condition
(arr1 < 2) | (arr1 > 4)   # OR condition
```

### <span style="color:#2E86AB">6.3 Universal Functions (ufuncs)</span>

> **Definition:** Universal functions (ufuncs) are NumPy functions that operate element-wise on arrays, returning a new array.

| ufunc | Description |
|:---|:---|
| `np.sqrt(arr)` | Square root of each element |
| `np.abs(arr)` | Absolute value |
| `np.exp(arr)` | e raised to each element |
| `np.log(arr)` | Natural log |
| `np.log2(arr)` | Log base 2 |
| `np.log10(arr)` | Log base 10 |
| `np.sin(arr)` | Sine |
| `np.cos(arr)` | Cosine |
| `np.ceil(arr)` | Round up |
| `np.floor(arr)` | Round down |
| `np.round(arr, n)` | Round to n decimal places |
| `np.clip(arr, min, max)` | Clip values to a range |

```python
np.sqrt(np.array([1, 4, 9, 16]))  # [1., 2., 3., 4.]
np.log(np.array([1, np.e]))       # [0., 1.]
np.clip(arr, 2, 8)                # Values outside [2,8] become 2 or 8
```

---

## <span style="color:#1565C0">7. Broadcasting</span>

> **Definition:** Broadcasting is NumPy's mechanism for performing operations on arrays of different shapes. The smaller array is "broadcast" across the larger one to match shapes : without copying data.

<div align="center" style="border: 2px solid #D4A017; border-radius: 8px; padding: 14px 24px; margin: 12px auto; max-width: 480px;">

### <span style="color:#D4A017">Broadcasting Rule: Dimensions are compatible if they are equal OR one of them is 1</span>

</div>

```python
arr1 = np.array([1, 2, 3, 4, 5])
arr1 + 10           # [11, 12, 13, 14, 15]  ← scalar broadcast
arr1 * 2            # [2, 4, 6, 8, 10]

# 2D broadcasting
matrix = np.ones((3, 3))
row = np.array([1, 2, 3])
matrix + row        # row is broadcast across all 3 rows
```

**Broadcasting shape rules:**

```
Shape (3, 3) + Shape (3,)     → OK, row broadcast
Shape (3, 1) + Shape (1, 3)   → OK, result is (3, 3)
Shape (3, 2) + Shape (3,)     → ERROR: 2 ≠ 3
```

---

## <span style="color:#1565C0">8. Matrix Operations</span>

### <span style="color:#2E86AB">8.1 Dot Product & Matrix Multiplication</span>

<div align="center" style="border: 2px solid #D4A017; border-radius: 8px; padding: 14px 24px; margin: 12px auto; max-width: 480px;">

### <span style="color:#D4A017">Dot product: a · b = Σ(aᵢ × bᵢ)</span>

</div>

```python
a = np.array([1, 2, 3, 4])
b = np.array([5, 6, 7, 8])

a @ b           # 70  : matrix multiplication / dot product operator
a.dot(b)        # 70  : same as above
np.dot(a, b)    # 70  : function form
```

> `@` is preferred for matrix multiplication (PEP 465). `a @ b` = `a.dot(b)` for 1D and 2D arrays.

### <span style="color:#2E86AB">8.2 Linear Algebra (np.linalg)</span>

| Function | Description |
|:---|:---|
| `np.linalg.det(A)` | Determinant of matrix |
| `np.linalg.inv(A)` | Inverse of matrix |
| `np.linalg.eig(A)` | Eigenvalues and eigenvectors |
| `np.linalg.norm(v)` | Norm (magnitude) of vector |
| `np.linalg.solve(A, b)` | Solve linear system Ax = b |

```python
A = np.array([[1,2],[3,4]])
np.linalg.det(A)         # -2.0
np.linalg.inv(A)         # Inverse matrix
np.linalg.norm(a)        # Magnitude of vector a
```

---

## <span style="color:#1565C0">9. Stacking & Splitting Arrays</span>

### <span style="color:#2E86AB">9.1 Stacking</span>

```python
a = np.array([1, 2, 3, 4])
b = np.array([5, 6, 7, 8])
```

| Function | Description | Output Shape |
|:---|:---|:---|
| `np.vstack((a, b))` | Stack vertically (row-wise) | `(2, 4)` |
| `np.hstack((a, b))` | Stack horizontally (column-wise) | `(8,)` |
| `np.column_stack((a, b))` | Stack as columns | `(4, 2)` |
| `np.concatenate((a,b), axis=0)` | Concatenate along axis | Depends on axis |
| `np.stack((a, b), axis=0)` | New axis stacking | `(2, 4)` |

```python
np.vstack((a, b))         # [[1,2,3,4],[5,6,7,8]]
np.hstack((a, b))         # [1,2,3,4,5,6,7,8]
np.column_stack((a, b))   # [[1,5],[2,6],[3,7],[4,8]]
```

### <span style="color:#2E86AB">9.2 Splitting</span>

| Function | Description |
|:---|:---|
| `np.split(arr, n)` | Split into n equal parts |
| `np.hsplit(arr, n)` | Split horizontally |
| `np.vsplit(arr, n)` | Split vertically |
| `np.array_split(arr, n)` | Split (allows unequal parts) |

```python
np.split(a, 2)         # [array([1,2]), array([3,4])]
np.split(a, [1, 3])    # Split at index 1 and 3
```

---

## <span style="color:#1565C0">10. Copying Arrays</span>

### <span style="color:#2E86AB">10.1 View vs Copy</span>

> **Definition:** A **view** (shallow copy) shares the same memory as the original array : modifying the view modifies the original. A **copy** (deep copy) creates a completely independent array.

| Operation | Type | Modifies original? |
|:---|:---:|:---:|
| `b = a` | Reference | <span style="color:#C0392B">Yes</span> |
| `b = a[1:3]` (slice) | View | <span style="color:#C0392B">Yes</span> |
| `b = a.copy()` | Deep copy | <span style="color:#27AE60">No</span> |
| `b = a.view()` | Shallow view | <span style="color:#C0392B">Yes</span> |

```python
a = np.array([1, 2, 3, 4])

# View (shallow copy) : shares memory
slice_view = a[1:3]
slice_view[0] = 99    # a is now [1, 99, 3, 4]  ← original changed!

# Deep copy : independent
b = a.copy()
b[0] = 0              # a is unchanged
```

<div align="center" style="border: 2px solid #D4A017; border-radius: 8px; padding: 14px 24px; margin: 12px auto; max-width: 480px;">

### <span style="color:#D4A017">Always use .copy() when you don't want to affect the original array</span>

</div>

---

## <span style="color:#1565C0">11. Reshaping & Flattening</span>

```python
arr = np.arange(1, 13)   # [1,2,3,...,12]

arr.reshape(3, 4)        # 3 rows × 4 columns
arr.reshape(4, 3)        # 4 rows × 3 columns
arr.reshape(2, 2, 3)     # 3D: 2 blocks of 2×3
arr.reshape(-1, 4)       # Auto-calculate rows, 4 columns
arr.reshape(3, -1)       # 3 rows, auto-calculate columns

arr.flatten()            # 1D copy: [1,2,3,...,12]
arr.ravel()              # 1D view (faster than flatten)
```

> `-1` in reshape tells NumPy to automatically compute that dimension from the remaining dimensions.

---

## <span style="color:#1565C0">12. Sorting & Searching</span>

### <span style="color:#2E86AB">12.1 Sorting</span>

```python
arr = np.array([3, 1, 4, 1, 5, 9, 2, 6])

np.sort(arr)             # Returns sorted copy: [1,1,2,3,4,5,6,9]
arr.sort()               # Sorts in-place
np.sort(arr)[::-1]       # Descending order
np.argsort(arr)          # Indices that would sort the array
```

### <span style="color:#2E86AB">12.2 Searching</span>

```python
arr = np.array([1, 2, 3, 4, 5])

np.where(arr > 3)            # (array([3, 4]),) : indices where condition is True
np.where(arr > 3, arr, 0)    # Replace where False with 0
np.searchsorted(arr, 3)      # Index where 3 would be inserted
np.nonzero(arr)              # Indices of non-zero elements
```

---

## <span style="color:#1565C0">13. Data Type (dtype) Handling</span>

> **Definition:** NumPy arrays are homogeneous : every element has the same data type. The `dtype` determines how data is stored and what operations are valid.

| dtype | Description |
|:---|:---|
| `int8`, `int16`, `int32`, `int64` | Signed integers (8–64 bit) |
| `uint8`, `uint16`, `uint32`, `uint64` | Unsigned integers |
| `float16`, `float32`, `float64` | Floating point |
| `complex64`, `complex128` | Complex numbers |
| `bool` | Boolean |
| `str_` | Fixed-length strings |
| `object` | Python objects |

```python
arr = np.array([1, 2, 3])
arr.dtype                       # dtype('int64')

arr = np.array([1.0, 2.0])
arr.dtype                       # dtype('float64')

arr = np.array([1, 2, 3], dtype=np.float32)   # Force dtype
arr.astype(np.float64)          # Convert dtype (returns new array)
arr.astype(int)                 # Convert to integer
```

---

## <span style="color:#1565C0">14. Aggregation with Axis</span>

> **Definition:** The `axis` parameter controls the direction of aggregation. `axis=0` operates along rows (down), `axis=1` operates along columns (across).

```python
arr = np.array([[1, 2, 3],
                [4, 5, 6]])
```

<div align="center" style="border: 2px solid #D4A017; border-radius: 8px; padding: 14px 24px; margin: 12px auto; max-width: 480px;">

### <span style="color:#D4A017">axis=0 → collapse rows (per column) | axis=1 → collapse columns (per row)</span>

</div>

```python
arr.sum(axis=0)    # [5, 7, 9]   : sum of each column
arr.sum(axis=1)    # [6, 15]     : sum of each row
arr.max(axis=0)    # [4, 5, 6]   : max of each column
arr.mean(axis=1)   # [2., 5.]    : mean of each row
```

---

## <span style="color:#1565C0">15. Useful Utility Functions</span>

| Function | Description | Example |
|:---|:---|:---|
| `np.unique(arr)` | Unique values | `np.unique([1,2,2,3])` → `[1,2,3]` |
| `np.count_nonzero(arr)` | Count non-zero elements | |
| `np.any(arr > 5)` | True if any element satisfies | |
| `np.all(arr > 0)` | True if all elements satisfy | |
| `np.isnan(arr)` | Boolean mask of NaN values | |
| `np.isinf(arr)` | Boolean mask of Inf values | |
| `np.nan_to_num(arr)` | Replace NaN/Inf with numbers | |
| `np.flip(arr)` | Reverse array along axis | |
| `np.tile(arr, n)` | Repeat array n times | |
| `np.repeat(arr, n)` | Repeat each element n times | |
| `np.delete(arr, idx)` | Delete element at index | |
| `np.insert(arr, idx, val)` | Insert value at index | |
| `np.append(arr, val)` | Append value(s) | |

```python
np.unique([1,1,2,2,3])       # [1, 2, 3]
np.any(arr > 5)               # True or False
np.all(arr > 0)               # True or False
np.isnan(np.array([1, np.nan, 3]))  # [False, True, False]
np.tile([1,2], 3)             # [1, 2, 1, 2, 1, 2]
np.repeat([1,2], 3)           # [1, 1, 1, 2, 2, 2]
```

---

## <span style="color:#1565C0">16. Loading & Saving Arrays</span>

```python
# Save and load single array
np.save('myarray.npy', arr)
arr = np.load('myarray.npy')

# Save and load multiple arrays
np.savez('arrays.npz', a=arr1, b=arr2)
data = np.load('arrays.npz')
data['a']    # access arr1

# Text files (CSV-style)
np.savetxt('data.csv', arr, delimiter=',')
arr = np.loadtxt('data.csv', delimiter=',')
```

---

## <span style="color:#1565C0">17. Quick Reference Cheat Sheet</span>

### <span style="color:#2E86AB">Array Creation Summary</span>

```
np.array([...])           → from list
np.zeros(n)               → all zeros (float)
np.ones((r,c))            → all ones
np.eye(n)                 → identity matrix
np.arange(s, e, step)     → range of integers/floats
np.linspace(s, e, n)      → n evenly spaced values
np.random.random(n)       → random floats [0, 1)
np.random.randn(n)        → standard normal distribution
np.random.randint(l,h,n)  → random integers
```

### <span style="color:#2E86AB">Indexing Summary</span>

```
arr[i]          → single element (1D)
arr[i, j]       → element at row i, col j (2D)
arr[i:j]        → slice from i to j-1
arr[::-1]       → reversed
arr[arr > x]    → boolean filter
arr[[0,2,4]]    → fancy indexing
```

### <span style="color:#2E86AB">Key Methods Summary</span>

```
.shape   .size    .ndim    .dtype
.min()   .max()   .sum()   .mean()   .std()
.argmin()  .argmax()
.reshape()  .flatten()  .ravel()  .T
.copy()   .astype()   .sort()
```

### <span style="color:#2E86AB">Operations Summary</span>

```
+  -  *  /  //  %  **     → element-wise arithmetic
@  or .dot()               → matrix multiplication / dot product
np.sqrt()  np.exp()  np.log()  np.abs()
np.where() np.sort()  np.unique()
np.vstack()  np.hstack()  np.split()
```

---

## <span style="color:#1565C0">18. Common Mistakes to Avoid</span>

| Mistake | Problem | Fix |
|:---|:---|:---|
| `arr[1:3] * 10` without assignment | Doesn't modify array | `arr[1:3] = arr[1:3] * 10` |
| Slice modifies original | Slices are views | Use `.copy()` |
| Reshape with wrong size | `ValueError` | Ensure `r × c == arr.size` |
| Mixed types in array | dtype cast to `object` | Use explicit `dtype=` |
| Using Python `sum()` on array | Slow | Use `arr.sum()` |
| `axis` confusion | Wrong aggregation direction | Remember: `axis=0` → rows collapsed |

---

<div align="center">

<sub>NumPy Reference Notes : Covering Arrays, Indexing, Operations, Broadcasting & More</sub>

</div>

---

<div align="center">

<sub>These notes were written and compiled by</sub>

### **Sagar Bhadra**

<sub>Connect with me on</sub>

<br>

[![GitHub](https://img.shields.io/badge/GitHub-SagarBhadra01-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/SagarBhadra01)&nbsp;
[![X (Twitter)](https://img.shields.io/badge/Twitter-SagarBhadra01-000000?style=for-the-badge&logo=x&logoColor=white)](https://x.com/SagarBhadra01)&nbsp;
[![LinkedIn](https://img.shields.io/badge/LinkedIn-sagarbhadra01-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/sagarbhadra01)&nbsp;
[![Gmail](https://img.shields.io/badge/Gmail-sagarbhadra404@gmail.com-D14836?style=for-the-badge&logo=gmail&logoColor=white)](mailto:sagarbhadra404@gmail.com)

</div>