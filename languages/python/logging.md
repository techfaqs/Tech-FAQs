# logging module

**logging** module defines functions and classes which implement a flexible event
logging system for applications and libraries.

Import `logging`:

    import logging
    
Create logger:

    logger = logging.getLogger('simple_example')
    logger.setLevel(logging.DEBUG)

Create console handler and set level to debug

    ch = logging.StreamHandler()
    ch.setLevel(logging.DEBUG)
    
Create formatter

    formatter = logging.Formatter('%(asctime)s - %(name)s - %(levelname)s - %(message)s')

Add formatter to ch (console handler object)

    ch.setFormatter(formatter)
    

