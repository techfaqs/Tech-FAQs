# NumPy - Numeric Python


## Instalation

pip3 install numpy

## Basics

Import numpy package:

    import numpy as np
    
Create a numpy array:

    >>> npArray = np.array([1.25, 2.2, 3.5])
    >>> npArray
    array([1.25, 2.2, 3.5])
    
NumPy Arrays are quite different from lists, for example:

    [1,2,3] + [1,2,3]

In Python Lists, we would get: `[1,2,3,1,2,3]`

In NumPy Arrays, we would get: `array([2,4,6])`

Indexing is very similar to how its done with Python Lists.
`list_name[0]` would fetch you the first element.

You may also do element wise comparisons to get a list of boolens as your result,
for example:

    >>> npArray < 2
    array([ True, False, False], dtype=bool)

Sub-setting with conditions:

    >>> npArray[npArray < 2]
    array([ 1.25])
    
Operations over lists don't require you to iterate over the list,

    >>> npArray * 2
    array([ 2.5,  4.4,  7. ])
    
Element-wise multiplication of lists,
for example -

Lets multiply an array with another, element-wise:

    >>> np_heights=np.array([ 1.8796,  1.8796,  1.8288,  1.905,   1.905,   1.8542])
    >>> np_weights=np.array([ 1.8796,  1.8796,  1.8288,  1.905,   1.905,   1.8542])
    
    >>> bmi = (np_heights) / ((np_weights)**2)
    >>> bmi
    array([ 0.53202809,  0.53202809,  0.54680665,  0.52493438,  0.52493438,
        0.53931615])

