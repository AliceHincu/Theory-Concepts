# Socket programming
Be sure to first read the "Socket Programming in C"!!

**Sockets allow communication between two different processes on the same or different machines**. To be more precise, it's a way to talk to other computers using standard Unix file descriptors. In Unix, every I/O action is done by writing or reading a file descriptor. A file descriptor is just an integer associated with an open file and it can be a network connection, a text file, a terminal, or something else. **A Unix Socket is used in a client-server application framework**. A server is a process that performs some functions on request from a client.

# Some theory
This is from [Socket programming docs](https://docs.python.org/3/howto/sockets.html). 

## 1. Creating a socket
Roughly speaking, when you clicked on the link that brought you to this page, your browser did something like the following:
```python
# create an INET, STREAMing socket
s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
# now connect to the web server on port 80 - the normal http port
s.connect(("www.github.com", 80))
```
When the connect completes, the socket s can be used to send in a request for the text of the page. The same socket will read the reply, and then be destroyed. That’s right, destroyed. Client sockets are normally only used for one exchange (or a small set of sequential exchanges).


What happens in the web server is a bit more complex. First, the web server creates a “server socket”:
```python
# create an INET, STREAMing socket
serversocket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
# bind the socket to a public host, and a well-known port
serversocket.bind((socket.gethostname(), 80))
# become a server socket
serversocket.listen(5)
```
A couple things to notice: we used socket.gethostname() so that the socket would be visible to the outside world. If we had used s.bind(('localhost', 80)) or s.bind(('127.0.0.1', 80)) we would still have a “server” socket, but one that was only visible within the same machine. s.bind(('', 80)) specifies that the socket is reachable by any address the machine happens to have.

Finally, the argument to listen tells the socket library that we want it to queue up as many as 5 connect requests (the normal max) before refusing outside connections. If the rest of the code is written properly, that should be plenty.

Now that we have a “server” socket, listening on port 80, we can enter the mainloop of the web server:

```python
while True:
    # accept connections from outside
    (clientsocket, address) = serversocket.accept()
    # now do something with the clientsocket
    # in this case, we'll pretend this is a threaded server
    ct = client_thread(clientsocket)
    ct.run()
```
Each clientsocket is created in response to some other “client” socket doing a connect() to the host and port we’re bound to. As soon as we’ve created that clientsocket, we go back to listening for more connections

## Using a socket (send and recv)
Now we come to the major stumbling block of sockets - **send and recv** operate on the network buffers. They do not necessarily handle all the bytes you hand them (or expect from them), because their major focus is handling the network buffers. In general, they return when the associated network buffers have been filled (send) or emptied (recv). They then tell you how many bytes they handled. It is your responsibility to call them again until your message has been completely dealt with.

When a recv returns 0 bytes, it means the other side has closed (or is in the process of closing) the connection. You will not receive any more data on this connection. Ever. You may be able to send data successfully; I’ll talk more about this later.

A protocol like HTTP uses a socket for only one transfer. The client sends a request, then reads a reply. That’s it. The socket is discarded. This means that a client can detect the end of the reply by receiving 0 bytes.

## Binary data (ntohl, htonl, ntohs, htons)
It is perfectly possible to send binary data over a socket. The major problem is that not all machines use the same formats for binary data. For example, a Motorola chip will represent a 16 bit integer with the value 1 as the two hex bytes 00 01. Intel and DEC, however, are byte-reversed - that same 1 is 01 00. Socket libraries have calls for converting 16 and 32 bit integers - **ntohl, htonl, ntohs, htons where “n” means network and “h” means host, “s” means short and “l” means long**. Where network order is host order, these do nothing, but where the machine is byte-reversed, these swap the bytes around appropriately.

# 2. Practical example
This is from [here](https://realpython.com/python-sockets/)
### server.py
```python
#!/usr/bin/env python3

import socket

HOST = '127.0.0.1'  # Standard loopback interface address (localhost)
PORT = 65432        # Port to listen on (non-privileged ports are > 1023)

with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
    s.bind((HOST, PORT))
    s.listen()
    conn, addr = s.accept()
    with conn:
        print('Connected by', addr)
        while True:
            data = conn.recv(1024)
            if not data:
                break
            conn.sendall(data)
```           

* **socket.socket()** creates a socket object that supports the context manager type, so you can use it in a **with statement**. There’s no need to call s.close().
* The arguments passed to socket() specify the address family and socket type. 
   * AF_INET is the Internet address family for IPv4. 
   * SOCK_STREAM is the socket type for TCP, the protocol that will be used to transport our messages in the network.
* **bind()** is used to associate the socket with a specific network interface and port number. The values passed to bind() depend on the address family of the socket. In this example, we’re using socket.AF_INET (IPv4). So it expects a 2-tuple: (host, port).
* **listen()** enables a server to accept() connections. It makes it a “listening” socket
* **accept()** blocks and waits for an incoming connection. When a client connects, it returns a new socket object representing the connection and a tuple holding the address of the client. The tuple will contain (host, port) for IPv4 connections
* **recv()**  reads whatever data the client sends and echoes it back using **conn.sendall()**.

**If conn.recv() returns an empty bytes object**, b'', then the client closed the connection and **the loop is terminated**. The with statement is used with conn to automatically close the socket at the end of the block.

### client.py
```python
#!/usr/bin/env python3

import socket

HOST = '127.0.0.1'  # The server's hostname or IP address
PORT = 65432        # The port used by the server

with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
    s.connect((HOST, PORT))
    s.sendall(b'Hello, world')
    data = s.recv(1024)

print('Received', repr(data))
```

