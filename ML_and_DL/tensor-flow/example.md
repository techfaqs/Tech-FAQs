# Tensorflow - Hello World

In the below example,we first create a constant named `hello` with the message to be printed. 

*Constants may not be modified once created.*

Tthen we create an instance of TensorFlow session named `sess` using `tf.Session()`

The `tf.Session()` is a session management class in TensorFlow
which is responsible for running the TensorFlow operations.

To run the TensorFlow operations we will use the method `sess.run()`

    from __future__ import print_function

    import tensorflow as tf

    # Simple hello world using TensorFlow
    hello = tf.constant('Hello, World!')

    # Start tf session
    sess = tf.Session()

    # Run the op
    print(sess.run(hello))


Output:

    b'Hello, World!'
