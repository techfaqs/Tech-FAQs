# Data Types in Hive

### Primitive Types

1. __Integers__
    - TINYINT—1 byte integer
    - SMALLINT—2 byte integer
    - INT—4 byte integer
    - BIGINT—8 byte integer

2. __Boolean type__
    - BOOLEAN—TRUE/FALSE

3. __Floating point numbers__
    - FLOAT—single precision
    - DOUBLE—Double precision

4. __Fixed point numbers__
    - DECIMAL—a fixed point value of user defined scale and precision

5. __String types__
    - STRING—sequence of characters in a specified character set
    - VARCHAR—sequence of characters in a specified character set with a maximum length
    - CHAR—sequence of characters in a specified character set with a defined length

6. __Date and time types__
    - TIMESTAMP— a specific point in time, up to nanosecond precision
    - DATE—a date

7. __Binary types__
    - BINARY—a sequence of bytes


### Complex Types

- __Structs__ : the elements within the type can be accessed using the DOT (.) notation.
  For example, for a column `c` of type `STRUCT {a INT; b INT}`, the `a` field is accessed
   by the expression `c.a`
- __Maps__ (key-value tuples): The elements are accessed using ['element name'] notation.
  For example in a map `M` comprising of a mapping from `'group' -> gid`
   the gid value can be accessed using `M['group']`
- __Arrays__ (indexable lists): The elements in the array have to be of the same type.
  Elements can be accessed using the `[n]` notation where `n` is an index
   (zero-based) into the array.
   For example, for an array `A` having the elements `['a', 'b', 'c']`, `A[1]` retruns `'b'`.
