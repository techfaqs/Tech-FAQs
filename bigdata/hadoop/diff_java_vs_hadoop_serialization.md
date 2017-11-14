# Difference between Java and Hadoop Serialization

### Java Serializable

Serializable does not assume the class of stored values is known and tags
 instances with its class that is it writes the metadata about the _object_,
 which includes the _class name, field names and types, and its superclass_.
 
`ObjectOutputStream` and `ObjectInputStream` optimize this somewhat,
 so that 5-byte handles are written for instances of a class after the first.
 But object sequences with handles cannot be then accessed randomly,
 since they rely on stream state. This complicates things like sorting.
 
### Hadoop Writable

While defining a __Writable__ you already know the expected class,
so Writables don't store their type in the serialized representation (because
while deserializing, you know what is expected).
For example, if the input key is a LongWritable, an empty `LongWritable`
instance is populated from the input data stream.
As no meta info is needed, none is stored, this results in
considerably more compact binary files, straightforward random access
and higher performance.


>Doug Cutting's reply for __Why Writable over Serializable?__
>
>The Writable interface is subtly different than Serializable. 
>Serializable does not assume the class of stored values is known.  So 
>each instance is tagged with its class.  ObjectOutputStream and 
>ObjectInputStream optimize this somewhat, so that 5-byte handles are 
>written for instances of a class after the first.  But object sequences 
>with handles cannot be then accessed randomly, since they rely on stream 
>state.  This complicates things like sorting.
>
>Writable, on the other hand, assumes that the application knows the 
>expected class.  The application must be able to create an instance in 
>order to call readFields().  So the class need not be stored with each 
>instance.  This results in considerably more compact binary files, 
>straightforward random access and generally higher performance.
>
>Arguably Hadoop could use Serializable.  One could override writeObject 
>or writeExternal for each class whose serialization was performance 
>critical.  (MapReduce is very i/o intensive, so nearly every class's 
>serialization is performance critical.)  One could implement 
>ObjectOutputStream.writeObjectOverride() and 
>ObjectInputStream.readObjectOverride() to use a more compact 
>representation, that, e.g., did not need to tag each top-level instance 
>in a file with its class.  This would probably require as least as much 
>code as Haddop has in Writable, ObjectWritable, etc., and the code would 
>be a bit more complicated, since it would be trying to work around a 
>different typing model.  But it might have the advantage of better 
>built-in version control.  Or would it?
>
>Serializable's version mechanism is to have classes define a static 
>named serialVersionUID.  This permits one to protect against 
>incompatible changes, but does not easily permit one to implement 
>back-compatibility.  For that, the application must explicitly deal with 
>versions.  It must reason, in a class-specific manner, about the version 
>that was written while reading, to decide what to do.  But 
>Serializeable's version mechanism does not support this any more or less 
>than Writable.
>
>See, for example, the "Design Considerations" section of:
>
>http://www.javaworld.com/javaworld/jw-02-2006/jw-0227-control_p.html
>
>So, in summary, I don't think Serializable holds many advantages: it 
>wouldn't substantially reduce the amount of code, and it wouldn't solve 
>versioning.
>
>Doug


Reference: [SO Question](https://stackoverflow.com/questions/16836607/what-are-the-connections-and-differences-between-hadoop-writable-and-java-io-ser)
