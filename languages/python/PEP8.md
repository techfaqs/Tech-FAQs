# PEP8 Style Guide List

### Imports

1. Imports should usually be on separate lines, `from` imports  are an
 exception though. For example:

       import os
       import sys
       
       from subprocess import Popen, PIPE

2. Imports are to be put right after the module doc strings or comments and
 before module globals and constants.
     Imports should be grouped in the following order:

      1. standard library imports
      2. related third party imports
      3. local application/library specific imports
    You should put a blank line between each group of imports.
    
3. Absolute imports are recommended, however explicit relative imports are
 an acceptable alternative.
	
	***Better***-
 
	    import mypkg.sibling
	    from mypkg import sibling
	    from mypkg.sibling import example

	***Acceptable***-
	
		from . import sibling
		from .sibling import example
 
4. When importing a class from a class-containing module, it's usually okay to spell this:

       from myclass import MyClass
       from foo.bar.yourclass import YourClass
     
    If this spelling causes local name clashes, then spell them

       import myclass
       import foo.bar.yourclass
    and use `myclass.MyClass` and `foo.bar.yourclass.YourClass`.
 
 
5. Wildcard imports should be avoided, as they make it unclear which names are
  present in the namespace, confusing both readers and many automated tools.
    
		
    
Many more to be added!
