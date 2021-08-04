Stream Redirection
==================

Bash has many ways to redirect the streams of processes.

Process to Process
------------------

Use the pipe key (``|``) to redirect the stdout of one process to another:

``cat file.txt | grep hello``

Process to File
---------------

Use the greater than sign (``>``) to redirect stdout to a file:

``ls > a.txt``

File to Process
---------------

Use the less than sign (``<``) to put file data into stdin:

``grep hello < file.txt``
