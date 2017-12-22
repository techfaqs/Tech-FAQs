# Tensorflow - Hello World



    from __future__ import print_function

    import tensorflow as tf

    # Simple hello world using TensorFlow
    hello = tf.constant('Hello, World!')

    # Start tf session
    sess = tf.Session()

    # Run the op
    print(sess.run(hello))
