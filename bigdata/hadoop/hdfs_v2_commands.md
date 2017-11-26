# HDFS Version 2 Commands


**appendToFile:** Append single src, or multiple srcs from local file system
 to the destination file system. Also reads input from stdin and appends to
 destination file system. Keep the <localfile> as `-` 

     hdfs dfs -appendToFile [localfile1 localfile2 ..] [/HDFS/FILE/PATH..]


**cat:** Copies source paths to stdout.

     hdfs dfs -cat URI [URI …]


**chgrp:** Changes the group association of files.
 With -R, makes the change recursively by way of the directory structure.
 The user must be the file owner or the superuser.

     hdfs dfs -chgrp [-R] GROUP URI [URI …]

**chmod:** Changes the permissions of files.
 With -R, makes the change recursively by way of the directory structure.
 The user must be the file owner or the superuser

     hdfs dfs -chmod [-R] <MODE[,MODE]... | OCTALMODE> URI [URI …]


**chown:** Changes the owner of files.
 With -R, makes the change recursively by way of the directory structure.
 The user must be the superuser.

     hdfs dfs -chown [-R] [OWNER][:[GROUP]] URI [URI ]


**copyFromLocal:** Works similarly to the put command, except that
 the source is restricted to a local file reference.

     hdfs dfs -copyFromLocal <localsrc> URI


**copyToLocal:** Works similarly to the get command, except that the
 destination is restricted to a local file reference.

     hdfs dfs -copyToLocal [-ignorecrc] [-crc] URI <localdst>


**count:** Counts the number of directories, files, and bytes under
 the paths that match the specified file pattern.

     hdfs dfs -count [-q] [-h] <paths>


**cp:** Copies one or more files from a specified source to a specified destination.
 If you specify multiple sources, the specified destination must be a directory.

     hdfs dfs -cp URI [URI …] <dest>


**du:** Displays the size of the specified file, or the sizes of files and
 directories that are contained in the specified directory.
 If you specify the -s option, displays an aggregate summary of file sizes
 rather than individual file sizes. If you specify the -h option, formats
 the file sizes in a \"human-readable\" way.

     hdfs dfs -du [-s] [-h] URI [URI …]


**dus:** Displays a summary of file sizes; equivalent to hdfs dfs -du –s.

     hdfs dfs -dus <args>


**expunge:** Empties the trash. When you delete a file, it isn't removed
 immediately from HDFS, but is renamed to a file in the /trash directory.
 As long as the file remains there, you can undelete it if you change your mind,
 though only the latest copy of the deleted file can be restored.

     hdfs dfs –expunge


**get:** Copies files to the local file system.
 Files that fail a cyclic redundancy check (CRC) can still be copied if
 you specify the `-ignorecrc` option.
 The CRC is a common technique for detecting data transmission errors.
 CRC checksum files (having the `.crc` extension) are used to verify the
 data integrity of the other file; these files are copied if you specify
 the `-crc` option.

     hdfs dfs -get [-ignorecrc] [-crc] <src> <localdst>


**getmerge:** Concatenates the files in src and writes the result to the
 specified local destination file. To add a newline character at the end
 of each file, specify the addnl option.

     hdfs dfs -getmerge <src> <localdst> [addnl]


**ls:** Returns statistics for the specified files or directories.

     hdfs dfs -ls <args>


**lsr:** Serves as the recursive version of ls; similar to the Unix command ls -R.

     hdfs dfs -lsr <args>


**mkdir:** Creates directories on one or more specified paths.
 Its behavior is similar to the Unix mkdir -p command, which creates all
 directories that lead up to the specified directory if they don't exist already.

     hdfs dfs -mkdir <paths>


**moveFromLocal:** Works similarly to the put command, except that the source is
 deleted after it is copied.

     hdfs dfs -moveFromLocal <localsrc> <dest>


**mv:** Moves one or more files from a specified source to a specified destination.
 If you specify multiple sources, the specified destination must be a directory.
 Moving files across file systems isn't permitted.

     hdfs dfs -mv URI [URI …] <dest>


**put:** Copies files from the local file system to the destination file system.
 This command can also read input from stdin and write to the destination file system.

     hdfs dfs -put <localsrc> ... <dest>


**rm:** Deletes one or more specified files.
 This command doesn't delete empty directories or files.
 To bypass the trash (if it's enabled) and delete the specified files immediately,
 specify the `-skipTrash` option.

     hdfs dfs -rm [-skipTrash] URI [URI …]


**rm r:** Serves as the recursive version of –rm.

     hdfs dfs -rm -r [-skipTrash] URI [URI …]


**setrep:** Changes the replication factor for a specified file or directory.
 With -R, makes the change recursively by way of the directory structure.

     hdfs dfs -setrep <rep> [-R] <path>


**stat:** Displays information about the specified path.

     hdfs dfs -stat URI [URI …]


**tail:** Displays the last kilobyte of a specified file to stdout.
 The syntax supports the Unix `-f` option, which enables the specified
 file to be monitored. As new lines are added to the file by another process,
 tail updates the display.

     hdfs dfs -tail [-f] URI


**test:** Returns attributes of the specified file or directory.
 Specifies `-e` to determine whether the file or directory exists;
 `-z` to determine whether the file or directory is empty;
 and `-d` to determine whether the URI is a directory.

     hdfs dfs -test -[ezd] URI


**text:** Outputs a specified source file in text format.
 Valid input file formats are zip and `TextRecordInputStream`.

     hdfs dfs -text <src>


**touchz:** Creates a new, empty file of size 0 in the specified path.

     hdfs dfs -touchz <path>
