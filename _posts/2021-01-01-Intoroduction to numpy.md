---
layout: post
title:  "Introduction to Numpy"
date:   2021-01-01 15:12:01 +0530
categories: numpy
permalink: /:categories/:title
---

# Topic to cover 
1. Introduction to Numpy
  - Difference in python list and numpy
  - how to read Documantaion

2. Understanding DataType in Python 
  - How python Data type constructed 
  - creating numpy array  from scratch

3. Basic of NumPy array
  - Attributes of arrays:
    - Determining the size, shape, memory consumption, and data types of arrays
  - Indexing of arrays:
    -  Getting and setting the value of individual array elements
  - Slicing of arrays:
    -  Getting and setting smaller subarrays within a larger array
  - Reshaping of arrays:
    -  Changing the shape of a given array
  - Joining and splitting of arrays:
    - Combining multiple arrays into one, and splitting one array into many

4. Computation on NumPy Arrays: Universal Functions
5. Comparisons, Masks, and Boolean Logic
6. Fancy Indexing


#### Introduction to Numpy 
- Numpy (Numerical Python )
- Numpy, Pandas are  techniques for effectively loading, storing, and manipulating in-memory data in Python.
- Dataset are heterogenious in nature, but we can visualize them as set of array
  - collections of documents,
    - Text can be converted in various ways into numerical representations, perhaps binary digits representing the frequency of certain words or pairs of words.
  - collections of images,
    - two-dimensional arrays of numbers representing pixel brightness across the area.
  - collections of sound clips,
    -  one-dimensional arrays of intensity versus time.
  - collections of numerical measurements

> __For this reason, efficient storage and manipulation of numerical arrays is absolutely fundamental to the process of doing data science.__

- Difference in python list and numpy
  - NumPy arrays provide much more efficient storage and data operations as the arrays grow larger in size.  
  - Numpy array hold similar type objects, while list can store multiple type objects.
  -  NumPy is constrained to arrays that all contain the same type. If types do not match, NumPy will upcast if possible ([1.24,2,3,4,5], integers are up-cast to floating point)
  -  unlike Python lists, NumPy arrays can explicitly be multi-dimensional
  - list slicing will give a new object, while numpy slicing will give views


- how to read Documantaion
  - to display all the contents of the numpy namespace, you can type this:
    - np dot <TAB>
  - to display NumPy's built-in documentation, you can use this
    - np ?



  


```python
import numpy as np
np.__version__
```




    '1.19.5'



#### Understanding the Data Type in Python 
- how arrays of data are handled in the Python language
  - dynamically-typed language like Python skips variable declaration.
  - we can assign any kind of data to any variable: x = 'four', y = 4
  -  how this works is an important piece of learning to analyze data efficiently
    - The standard Python implementation is written in C.
    - every Python object is simply a cleverly-disguised __C structure__.
    -  when we define an integer in Python, such as x = 10000, x is not just a "raw" integer. It's actually a pointer to a compound C structure, which contains several values. 
    - 
    ```
    struct _longobject {
    long ob_refcnt;
    PyTypeObject *ob_type;
    size_t ob_size;
    long ob_digit[1];
};
    ```
      - ob_refcnt, a reference count that helps Python silently handle memory allocation and deallocation
      - ob_type, which encodes the type of the variable
      - ob_size, which specifies the size of the following data members
      - ob_digit, which contains the actual integer value that we expect the Python variable to represent.
  - Similarly python list also contain pointer to multiple pointer, as list might contain another list or tuple



- how NumPy improves on this
  - numpy ufunc (vectorized computation)
  - broadcasting
  - 


```python
# Creating Array from python list 
pylist= [112,123,23,24]
print('type(np.array(pylist)) :\n ',type(np.array(pylist)),'\n',np.array(pylist) )
```

    type(np.array(pylist)) :
      <class 'numpy.ndarray'> 
     [112 123  23  24]



```python
# Creating array from scratch 

# Create a length-10 integer array filled with zeros
print('np.zeros(10, dtype=int) :\n',np.zeros(10, dtype=int))
```

    np.zeros(10, dtype=int) :
     [0 0 0 0 0 0 0 0 0 0]



```python
# Create a 3x5 floating-point array filled with ones
print('np.ones((3, 5), dtype=float) :\n',np.ones((3, 5), dtype=float))
```

    np.ones((3, 5), dtype=float) :
     [[1. 1. 1. 1. 1.]
     [1. 1. 1. 1. 1.]
     [1. 1. 1. 1. 1.]]



```python
# Create a 3x5 array filled with 3.14
print('np.full((3, 5), 3.14) :\n',np.full((3, 5), 3.14))
```

    np.full((3, 5), 3.14) :
     [[3.14 3.14 3.14 3.14 3.14]
     [3.14 3.14 3.14 3.14 3.14]
     [3.14 3.14 3.14 3.14 3.14]]



```python
# Create an array filled with a linear sequence
# Starting at 0, ending at 20, stepping by 2
# (this is similar to the built-in range() function)
np.arange(0, 20, 2)
```




    array([ 0,  2,  4,  6,  8, 10, 12, 14, 16, 18])




```python
# Create an array of five values evenly spaced between 0 and 1
np.linspace(0, 1, 5)
```




    array([0.  , 0.25, 0.5 , 0.75, 1.  ])




```python
# Create a 3x3 array of uniformly distributed random values between 0 and 1
np.random.random((3, 3))
```




    array([[0.16427499, 0.47293302, 0.20152697],
           [0.70306028, 0.57954181, 0.44821527],
           [0.53551163, 0.51949547, 0.64934509]])




```python
# Create a 3x3 array of normally distributed random values
# with mean 0 and standard deviation 1
np.random.normal(0, 1, (3, 3))
```




    array([[-0.79983772,  0.28232463,  1.08844424],
           [-0.45715215, -0.1558073 , -1.56919382],
           [ 0.05284384, -0.08383961,  0.19385037]])




```python
# Create a 3x3 array of random integers in the interval [0, 10)
np.random.randint(0, 10, (3, 3))
```




    array([[9, 7, 8],
           [4, 6, 5],
           [4, 3, 1]])




```python
# Create a 3x3 identity matrix
np.eye(3)
```




    array([[1., 0., 0.],
           [0., 1., 0.],
           [0., 0., 1.]])




```python
# Create an uninitialized array of three integers
# The values will be whatever happens to already exist at that memory location
np.empty(3)
```




    array([1., 1., 1.])



#### Basics Of Numpy array

##### Attributes of arrays:


```python
import numpy as np
np.random.seed(0)  # seed for reproducibility

x1 = np.random.randint(10, size=6)  # One-dimensional array
x2 = np.random.randint(10, size=(3, 4))  # Two-dimensional array
x3 = np.random.randint(10, size=(3, 4, 5))  # Three-dimensional array
```


```python
print("x3 ndim: ", x3.ndim)
print("x3 shape:", x3.shape)
print("x3 size: ", x3.size)
```

    x3 ndim:  3
    x3 shape: (3, 4, 5)
    x3 size:  60



```python
print("dtype:", x3.dtype)
```

    dtype: int64


##### Array Indexing: Accessing Single Elements


```python
print('x1\n',x1)
print('x1[0]\n',x1[0])
print('x1[-1]\n',x1[-1]) #To index from the end of the array, you can use negative indices:

```

    x1
     [5 0 3 3 7 9]
    x1[0]
     5
    x1[-1]
     9



```python
print('x2\n',x2)
print('x2[0, 0]\n',x2[0, 0])
print('x2[2, -1]\n',x2[2, -1])
```

    x2
     [[3 5 2 4]
     [7 6 8 8]
     [1 6 7 7]]
    x2[0, 0]
     3
    x2[2, -1]
     7


#### Array Slicing: Accessing Subarrays
- x[start:stop:step]


```python
x = np.arange(10)
x
```




    array([0, 1, 2, 3, 4, 5, 6, 7, 8, 9])




```python
print(x[:5])  # first five elements
print('\n'*2)

print(x[5:])  # elements after index 5
print('\n'*2)

print(x[4:7])  # middle sub-array
print('\n'*2)

print(x[::2])  # every other element
print('\n'*2)

print(x[1::2])  # every other element, starting at index 1
print('\n'*2)

print(x[::-1])  # all elements, reversed
print('\n'*2)

print(x[5::-2] ) # reversed every other from index 5
```

    [0 1 2 3 4]
    
    
    
    [5 6 7 8 9]
    
    
    
    [4 5 6]
    
    
    
    [0 2 4 6 8]
    
    
    
    [1 3 5 7 9]
    
    
    
    [9 8 7 6 5 4 3 2 1 0]
    
    
    
    [5 3 1]


#### Multi-dimensional subarrays


```python
print(x2)
print('\n'*2)

print('x2[:2, :3] \n',x2[:2, :3] ) # two rows, three columns
print('\n'*2)

print('x2[:3, ::2] \n',x2[:3, ::2])  # all rows, every other column
print('\n'*2)

print('x2[::-1, ::-1]\n',x2[::-1, ::-1])
print('\n'*2)
```

    [[3 5 2 4]
     [7 6 8 8]
     [1 6 7 7]]
    
    
    
    x2[:2, :3] 
     [[3 5 2]
     [7 6 8]]
    
    
    
    x2[:3, ::2] 
     [[3 2]
     [7 8]
     [1 7]]
    
    
    
    x2[::-1, ::-1]
     [[7 7 6 1]
     [8 8 6 7]
     [4 2 5 3]]
    
    
    


#### Subarrays as no-copy views
  - One important–and extremely useful–thing to know about array slices is that they return views rather than copies of the array data. 
This is one area in which NumPy array slicing differs from Python list slicing: in lists, slices will be copies. 

- To cop-up we create  copies of arrays



```python
x2_sub_copy = x2[:2, :2].copy()
print(x2_sub_copy)

x2_sub_copy[0, 0] = 42
print(x2_sub_copy)

print(x2)
```

    [[3 5]
     [7 6]]
    [[42  5]
     [ 7  6]]
    [[3 5 2 4]
     [7 6 8 8]
     [1 6 7 7]]


#### Reshaping of Arrays

- np.array uses continous memory allocation 
- reshape method will use non- continous memory allocation 

- This can be done with the reshape method,
- newaxis keyword within a slice operation


```python
x = np.array([1, 2, 3])

# row vector via reshape
x.reshape((1, 3))
```




    array([[1, 2, 3]])




```python
# row vector via newaxis
x[np.newaxis, :]
```




    array([[1, 2, 3]])




```python
# column vector via newaxis
x[:, np.newaxis]
```




    array([[1],
           [2],
           [3]])



##### Concatenation of arrays
Concatenation, or joining of two arrays in NumPy, is primarily accomplished using the routines 
-  np.concatenate,
-  np.vstack,
-  and np.hstack.

np.concatenate takes a tuple or list of arrays as its first argument, as we can see here:


```python
x = np.array([1, 2, 3])
y = np.array([3, 2, 1])
np.concatenate([x, y])
```




    array([1, 2, 3, 3, 2, 1])




```python
#You can also concatenate more than two arrays at once:

z = [99, 99, 99]
print(np.concatenate([x, y, z]))
```

    [ 1  2  3  3  2  1 99 99 99]



```python
grid = np.array([[1, 2, 3],
                 [4, 5, 6]])


# concatenate along the first axis
print('np.concatenate([grid, grid])\n',np.concatenate([grid, grid]))

# concatenate along the second axis (zero-indexed)
print('np.concatenate([grid, grid], axis=1) \n',np.concatenate([grid, grid], axis=1))
```

    np.concatenate([grid, grid])
     [[1 2 3]
     [4 5 6]
     [1 2 3]
     [4 5 6]]
    np.concatenate([grid, grid], axis=1) 
     [[1 2 3 1 2 3]
     [4 5 6 4 5 6]]



```python
x = np.array([1, 2, 3])
grid = np.array([[9, 8, 7],
                 [6, 5, 4]])

# vertically stack the arrays
np.vstack([x, grid])
```




    array([[1, 2, 3],
           [9, 8, 7],
           [6, 5, 4]])




```python
# horizontally stack the arrays
y = np.array([[99],
              [99]])
np.hstack([grid, y])

#Similary, np.dstack will stack arrays along the third axis.
```




    array([[ 9,  8,  7, 99],
           [ 6,  5,  4, 99]])



##### Splitting of arrays
The opposite of concatenation is splitting, which is implemented by the functions
- np.split,
- np.hsplit, 
- np.vsplit. 


```python
grid = np.arange(16).reshape((4, 4))
grid
```




    array([[ 0,  1,  2,  3],
           [ 4,  5,  6,  7],
           [ 8,  9, 10, 11],
           [12, 13, 14, 15]])




```python
upper, lower = np.vsplit(grid, [2])
print(upper)
print(lower)

```

    [[0 1 2 3]
     [4 5 6 7]]
    [[ 8  9 10 11]
     [12 13 14 15]]



```python
left, right = np.hsplit(grid, [2])
print(left)
print(right)
```

    [[ 0  1]
     [ 4  5]
     [ 8  9]
     [12 13]]
    [[ 2  3]
     [ 6  7]
     [10 11]
     [14 15]]


#### Computation on NumPy Arrays: Universal Functions

This is known as a vectorized operation. This can be accomplished by simply performing an operation on the array, which will then be applied to each element. 


```python
x = np.arange(4)
print("x     =", x)
print("x + 5 =", x + 5)
print("x - 5 =", x - 5)
print("x * 2 =", x * 2)
print("x / 2 =", x / 2)
print("x // 2 =", x // 2)  # floor division
```

    x     = [0 1 2 3]
    x + 5 = [5 6 7 8]
    x - 5 = [-5 -4 -3 -2]
    x * 2 = [0 2 4 6]
    x / 2 = [0.  0.5 1.  1.5]
    x // 2 = [0 0 1 1]


- np.add	Addition (e.g., 1 + 1 = 2)
-	np.subtract	Subtraction (e.g., 3 - 2 = 1)
-	np.negative	Unary negation (e.g., -2)
-	np.multiply	Multiplication (e.g., 2 * 3 = 6)
-	np.divide	Division (e.g., 3 / 2 = 1.5)
-	np.floor_divide	Floor division (e.g., 3 // 2 = 1)
-	np.power	Exponentiation (e.g., 2 ** 3 = 8)
-	np.mod


```python
x = np.arange(1, 6)
np.add.reduce(x)
```




    15



##### Aggregations: Min, Max, and Everything In Between




```python
L = np.random.random(100)
sum(L)

# The syntax is quite similar to that of NumPy's sum function, and the result is the same in the simplest case:
```




    52.12818058833704




```python
np.sum(L)

# However, because it executes the operation in compiled code, NumPy's version of the operation is computed much more quickly:
```




    52.12818058833702




```python
#### Broadcasting
a = np.array([0, 1, 2])
b = np.array([5, 5, 5])
a + b
```




    array([5, 6, 7])




```python
a = np.arange(3)
b = np.arange(3)[:, np.newaxis]

print(a)
print(b)
```

    [0 1 2]
    [[0]
     [1]
     [2]]


#### Rules of Broadcasting
- Rule 1: If the two arrays differ in their number of dimensions, the shape of the one with fewer dimensions is padded with ones on its leading (left) side.
- Rule 2: If the shape of the two arrays does not match in any dimension, the array with shape equal to 1 in that dimension is stretched to match the other shape.
- Rule 3: If in any dimension the sizes disagree and neither is equal to 1, an error is raised.


```python
M = np.ones((2, 3))
a = np.arange(3)
print(M + a)
```

    [[1. 2. 3.]
     [1. 2. 3.]]



```python
M = np.ones((3, 2))
a = np.arange(3)
print(M + a)
```


    ---------------------------------------------------------------------------

    ValueError                                Traceback (most recent call last)

    <ipython-input-43-2e7962548b2a> in <module>()
          1 M = np.ones((3, 2))
          2 a = np.arange(3)
    ----> 3 print(M + a)
    

    ValueError: operands could not be broadcast together with shapes (3,2) (3,) 



```python
# In the previous section, we saw that ufuncs allow a NumPy user to remove the need to explicitly write slow Python loops.
# Broadcasting extends this ability. One commonly seen example is when centering an array of data.
# Imagine you have an array of 10 observations, each of which consists of 3 values. 
# Using the standard convention (see Data Representation in Scikit-Learn), we'll store this in a 10×3 array:

X = np.random.random((10, 3))
#We can compute the mean of each feature using the mean aggregate across the first dimension:

Xmean = X.mean(0)
Xmean
```




    array([0.45028642, 0.44632147, 0.53663802])



#### Comparisons, Masks, and Boolean Logic


```python
x = np.array([1, 2, 3, 4, 5])
print(x < 3 ) # less than)
```

    [ True  True False False False]



```python
print((2 * x) == (x ** 2))
```

    [False  True False False False]



```python
# how many values less than 6 in each row?
x= np.arange(1,13).reshape(3,4)
np.sum(x < 6, axis=1)
```




    array([4, 1, 0])



##### mask

it returns a one-dimensional array filled with all the values that meet this condition; in other words, all the values in positions at which the mask array is True.


```python
x
```




    array([[ 1,  2,  3,  4],
           [ 5,  6,  7,  8],
           [ 9, 10, 11, 12]])




```python
x < 5
```




    array([[ True,  True,  True,  True],
           [False, False, False, False],
           [False, False, False, False]])




```python
x[x < 5]
```




    array([1, 2, 3, 4])



#### Fancy Indexing


```python
X = np.arange(12).reshape((3, 4))
X
```




    array([[ 0,  1,  2,  3],
           [ 4,  5,  6,  7],
           [ 8,  9, 10, 11]])




```python
row = np.array([0, 1, 2])
col = np.array([2, 1, 3])
X[row, col]
```




    array([ 2,  5, 11])




```python
X[2, [2, 0, 1]]
```




    array([10,  8,  9])




```python

```
