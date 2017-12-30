# NumPy - Numeric Python


## Instalation

pip3 install numpy

## Basics

#### Import numpy package:

    import numpy as np
    
#### Create a numpy array:

    >>> npArray = np.array([1.25, 2.2, 3.5])
    >>> npArray
    array([1.25, 2.2, 3.5])
    
NumPy Arrays are quite different from lists, for example:

#### NumPy Array  Addition:

    [1,2,3] + [1,2,3]

In Python Lists, we would get: `[1,2,3,1,2,3]`

In NumPy Arrays, we would get: `array([2,4,6])`


#### Numpy Array multiplication:

    >>> lst1 = np.array([[1, 2, 3], [0.1, 0.2, 0.3], [1.1, 2.1, 3.1], [2.1, 2.2, 2.3]])
    >>> lst2 = np.array([0.0254, 0.453592, 1])
    >>> lst1 * lst2
    array([[  2.54000000e-02,   9.07184000e-01,   3.00000000e+00],
           [  2.54000000e-03,   9.07184000e-02,   3.00000000e-01],
           [  2.79400000e-02,   9.52543200e-01,   3.10000000e+00],
           [  5.33400000e-02,   9.97902400e-01,   2.30000000e+00]])

> Notice how with very little code, you can change all values in your numpy data structure in a very specific way.


### NumPy for Data Science

#### Summerizing data

`mean`, `median`, `mode`, `corrcoef`(to check if two arrays are co-related), `std`(Standard Deviation), `sum`, `sort`, etc.

#### Generate Data

Create data with normal distrbution:

    np.random.normal(<distrib. mean>, <distrib. std. dev.>, <no. of samples>)

for example,

    >>> np.random.normal(1.85, 0.83, 5000)

You may use `round` to round off the decimal precision.

    >>> np.round(np.random.normal(1.85, 0.83, 5), 2)
    array([ 2.01,  2.19,  1.69,  1.51,  1.22])

If you want to stack two arrays as columns,

    >>> np.column_stack(([1, 2, 3], [0.1, 0.2, 0.3]))
    array([[ 1. ,  0.1],
           [ 2. ,  0.2],
           [ 3. ,  0.3]])
           
Check correlation of arrays,

    >>> np.corrcoef(([1, 2, 3], [0.1, 0.6, 0.5]))
    array([[ 1.        ,  0.75592895],
           [ 0.75592895,  1.        ]])
           
