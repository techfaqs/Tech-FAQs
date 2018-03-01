# logging module

**logging** module defines functions and classes which implement a flexible event
logging system for applications and libraries.

**Simple logger example** (save the script in a `.py` file and run it using `python <file_name>.py`):

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

| LEVEL  | Numerical value <br> *(higher the number higher the priority)* |When it’s used|
| ------ | ------ | ----- |
| NOTSET |   0    | |
| DEBUG  |  10    |Detailed information, typically of interest only when diagnosing problems.|
| INFO   |  20    | Confirmation that things are working as expected. |
| WARN   |  30    | An indication that something unexpected happened, or indicative of some problem in the near future (e.g. ‘disk space low’). The software is still working as expected. |
| ERROR  |  40    | Due to a more serious problem, the software has not been able to perform some function. |
|CRITICAL|  50    | A serious error, indicating that the program itself may be unable to continue running. |

#### Logging variable data

To log variable data, use a format string for the event description message and append the variable data as arguments. For example:

    import logging
    logging.warning('%s before you %s', 'Look', 'leap!')

will display:

    WARNING:root:Look before you leap!

#### Formatting of displayed messages

To change the format which is used to display messages, you need to specify the format you want to use:

    import logging
    logging.basicConfig(format='%(levelname)s:%(message)s', level=logging.DEBUG)
    logging.debug('This message should appear on the console')
    logging.info('So should this')
    logging.warning('And this, too')
which would print:

    DEBUG:This message should appear on the console
    INFO:So should this
    WARNING:And this, too

Notice that the ‘root’ which appeared in earlier examples has disappeared.
Below is the list of attributes can be used to merge data from the record into the format string:

|Attribute name|Format|Description|
|----|----|----|
|args|You shouldn’t need to format this yourself.|The tuple of arguments merged into msg to produce message, or a dict whose values are used for the merge (when there is only one argument, and it is a dictionary).|
|asctime|%(asctime)s|Human-readable time when the LogRecord was created. By default this is of the form ‘2003-07-08 16:49:45,896’ (the numbers after the comma are millisecond portion of the time).|
|created|%(created)f|Time when the LogRecord was created (as returned by time.time()).|
|exc_info|You shouldn’t need to format this yourself.|Exception tuple (à la sys.exc_info) or, if no exception has occurred, None.|
|filename|%(filename)s|Filename portion of pathname.|
|funcName|%(funcName)s|Name of function containing the logging call.|
|levelname|%(levelname)s|Text logging level for the message ('DEBUG', 'INFO', 'WARNING', 'ERROR', 'CRITICAL').|
|levelno|%(levelno)s|Numeric logging level for the message (DEBUG, INFO, WARNING, ERROR, CRITICAL).|
|lineno|%(lineno)d|Source line number where the logging call was issued (if available).|
|module|%(module)s|Module (name portion of filename).|
|msecs|%(msecs)d|Millisecond portion of the time when the LogRecord was created.|
|message|%(message)s|The logged message, computed as msg % args. This is set when Formatter.format() is invoked.|
|msg|You shouldn’t need to format this yourself.|The format string passed in the original logging call. Merged with args to produce message, or an arbitrary object (see Using arbitrary objects as messages).|
|name|%(name)s|Name of the logger used to log the call.|
|pathname|%(pathname)s|Full pathname of the source file where the logging call was issued (if available).|
|process|%(process)d|Process ID (if available).|
|processName|%(processName)s|Process name (if available).|
|relativeCreated|%(relativeCreated)d|Time in milliseconds when the LogRecord was created, relative to the time the logging module was loaded.|
|thread|%(thread)d|Thread ID (if available).|
|threadName|%(threadName)s|Thread name (if available).|

> I see three conflicting styles of ***log formatting***, **which to
> use?**
> 
>     import logging
>     logging = logging.getLogger(__name__)
>     logger.info("%s went %s wrong", 42, 'very')
>     logger.info("{} went {} wrong".format(42, 'very'))
>     logger.info("%s went %s wrong" % (42, 'very'))
>
>  The most performant is the first one, as it doesn't precompute the string before use (or logging).
>  
>   If you only display `WARN` level and higher, your `DEBUG` messages don’t need to be calculated.
>   In case of second or third formatting, they would still be generated.

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
