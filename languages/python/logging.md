# logging module

**logging** module defines functions and classes which implement a flexible event
logging system for applications and libraries.

#### Simple logger example (save the lines in a `.py` file and run it using `python <file_name>.py`):

       import logging
       logging.warning('Watch out!')  # will print a message to the console
       logging.info('I told you so')  # will not print anything

Output:

       WARNING:root:Watch out!

The `INFO` message doesn’t appear because the default level is `WARNING`.
The printed message includes the indication of the level and the description of the event provided in the logging call.


### Logging into a File


A very common situation is that of recording logging events in a file, example-

       import logging
       logging.basicConfig(filename='example.log',level=logging.DEBUG)
       logging.debug('This message should go to the log file')
       logging.info('So should this')
       logging.warning('And this, too')
       
Output:

       DEBUG:root:This message should go to the log file
       INFO:root:So should this
       WARNING:root:And this, too
       
This example also shows how you can set the logging level which acts as the threshold for tracking. In this case, because we set the threshold to DEBUG, all of the messages were printed.

#### The logging levels, in increasing order of importance, are:

| LEVEL  | Numerical value <br> *(higher the number higher the priority)* |
| ------ | ------ |
| NOTSET |   0    |
| DEBUG  |  10    |
| INFO   |  20    |
| WARN   |  30    |
| ERROR  |  40    |
|CRITICAL|  50    |

---

Example of a simple logger, a console handler, and a simple formatter using Python code -

1. Import `logging`:

       import logging
    
2. Create logger:

       logger = logging.getLogger('simple_example')
       logger.setLevel(logging.DEBUG)

4. Create console handler and set level to debug

       ch = logging.StreamHandler()
       ch.setLevel(logging.DEBUG)

5. Create formatter

       formatter = logging.Formatter('%(asctime)s - %(name)s - %(levelname)s - %(message)s')

6. Add formatter to ch (console handler object)

       ch.setFormatter(formatter)
    
7. Add ch to logger

       logger.addHandler(ch)
       
8. Lets log a few messages

       logger.debug('debug message')
       logger.info('info message')
       logger.warn('warn message')
       logger.error('error message')
       logger.critical('critical message')

Output (after running all above statements in a `.py` script):

        2018-01-12 00:27:15,851 - simple_example - DEBUG - debug message
        2018-01-12 00:27:15,851 - simple_example - INFO - info message
        2018-01-12 00:27:15,869 - simple_example - WARNING - warn message
        2018-01-12 00:27:15,871 - simple_example - ERROR - error message
        2018-01-12 00:27:16,421 - simple_example - CRITICAL - critical message

### Reference

1. [PEP 282 - A Logging System](https://www.python.org/dev/peps/pep-0282/)
2. [Logging Advanced tutorial](https://docs.python.org/2.7/howto/logging.html#logging-advanced-tutorial)
