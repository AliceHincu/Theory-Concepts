# Threading
Documentation for python: [here](https://docs.python.org/3/library/threading.html)

## threading.Thread
```threading.Thread(group=None, target=None, name=None, args=(), kwargs={}, *, daemon=None)```

* **group**: should be None; reserved for future extension when a ThreadGroup class is implemented.
* **target**: is the callable object to be invoked by the run() method. Defaults to None, meaning nothing is called.
* **name**: is the thread name. By default, a unique name is constructed of the form “Thread-N” where N is a small decimal number, or “Thread-N (target)” where “target” is target.__name__ if the target argument is specified.
* **args** is the argument tuple for the target invocation. Defaults to ().
* **kwargs** is a dictionary of keyword arguments for the target invocation. Defaults to {}.
* **daemon**: explicitly sets whether the thread is daemonic. If None (the default), the daemonic property is inherited from the current thread.

Example: ```t=threading.Thread(target=myFunction, daemon=True)```
### Daemon thread
A thread can be flagged as a “**daemon thread**”. The significance of this flag is that the entire Python program exits when only daemon threads are left. The initial value is inherited from the creating thread. The flag can be set through the daemon property.

Basically: **The Daemon Thread does not block the main thread from exiting and continues to run in the background.**. [Read more about daemon thread](https://www.geeksforgeeks.org/python-daemon-threads/)

### start()
**Start the thread’s activity.**

It must be called at most once per thread object. It arranges for the object’s run() method to be invoked in a separate thread of control.

This method will raise a RuntimeError if called more than once on the same thread object.

### join()
Wait until the thread terminates. This blocks the calling thread until the thread whose join() method is called terminates – either normally or through an unhandled exception – or until the optional timeout occurs.


## threading.event
Class implementing event objects. An event manages a flag that can be set to true with the set() method and reset to false with the clear() method. The wait() method blocks until the flag is true. The flag is initially false.

### is_set()
Return True if and only if the internal flag is true.

### set()
Set the internal flag to true. All threads waiting for it to become true are awakened. Threads that call wait() once the flag is true will not block at all.

### clear()
Reset the internal flag to false. Subsequently, threads calling wait() will block until set() is called to set the internal flag to true again.

### wait(timeout=None)
Block until the internal flag is true. If the internal flag is true on entry, return immediately. Otherwise, block until another thread calls set() to set the flag to true, or until the optional timeout occurs.

When the timeout argument is present and not None, it should be a floating point number specifying a timeout for the operation in seconds (or fractions thereof).

This method returns True if and only if the internal flag has been set to true, either before the wait call or after the wait starts, so it will always return True except if a timeout is given and the operation times out.

Changed in version 3.1: Previously, the method always returned None.


## threading.get_ident()
Return the ‘thread identifier’ of the current thread. This is a nonzero integer. Its value has no direct meaning; it is intended as a magic cookie to be used e.g. to index a dictionary of thread-specific data. Thread identifiers may be recycled when a thread exits and another thread is created.

## threading.Lock
The class implementing primitive lock objects. Once a thread has acquired a lock, subsequent attempts to acquire it block, until it is released; any thread may release it.

### acquire(blocking=True, timeout=- 1)
**Acquire a lock, blocking or non-blocking.**

* When invoked with the blocking argument set to True (the default), block until the lock is unlocked, then set it to locked and return True.
* When invoked with the blocking argument set to False, do not block. If a call with blocking set to True would block, return False immediately; otherwise, set the lock to locked and return True.
* When invoked with the floating-point timeout argument set to a positive value, block for at most the number of seconds specified by timeout and as long as the lock cannot be acquired. A timeout argument of -1 specifies an unbounded wait. It is forbidden to specify a timeout when blocking is false.
* The return value is True if the lock is acquired successfully, False if not (for example if the timeout expired).

### release()
Release a lock. This can be called from any thread, not only the thread which has acquired the lock.

When the lock is locked, reset it to unlocked, and return. If any other threads are blocked waiting for the lock to become unlocked, allow exactly one of them to proceed.

When invoked on an unlocked lock, a RuntimeError is raised.

There is no return value.
