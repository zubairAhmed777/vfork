# vfork
A piece of advice first: Don't use vfork(). On a modern system, the advantages of using vfork() over fork() are tiny. The code you show can never work properly with vfork() because it invokes undefined behavior:

POSIX.1:

    The vfork() function has the same effect as fork(), except that the behavior is undefined if the process created by vfork() either modifies any data other than a variable of type pid_t used to store the return value from vfork(), or returns from the function in which vfork() was called, or calls any other function before successfully calling _exit() or one of the exec() family of functions.

So by calling printf() in your child code, your code is already undefined. Note that even a call to exit() would lead to undefined behavior, only _exit() is allowed.
