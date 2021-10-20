# Socket Programming
**Socket programming** is a way of connecting two nodes on a network to communicate with each other. One socket(node) listens on a particular port at an IP, while other socket reaches out to the other to form a connection. Server forms the listener socket while client reaches out to the server.

![](http://media.geeksforgeeks.org/wp-content/uploads/Socket-Programming-in-C-C-.jpg)

## IN CASE OF ADDRESS ALREADY IN USE
* For windows:
```netstat -ano | findstr ":8080"``` (to find pid - last column - for port) and then ```taskkill /F /PID <pid>``` to kill the process with the pid
## Socket creation
**socket() creates an endpoint for communication** and returns a file descriptor that refers to that endpoint.  The file descriptor returned by a successful call will be the lowest-numbered file descriptor not currently open for the process.
```c
#include <sys/socket.h>

int sockfd = socket(domain, type, protocol)
```
* **sockfd**: socket descriptor, an integer (like a file-handle) 
* **domain**: integer, communication domain e.g., **AF_INET (IPv4 protocol)** , AF_INET6 (IPv6 protocol). (P.S: we use af_inet). The domain argument specifies a communication domain; this selects the protocol family which will be used for communication. These families are defined in <sys/socket.h> 
* **type**: communication type
   * SOCK_STREAM: TCP(reliable, connection oriented): Provides sequenced, reliable, two-way, connection-based byte streams.  An out-of-band data transmission mechanism may be supported.
   * SOCK_DGRAM: UDP(unreliable, connectionless) 
* **protocol**: Protocol value for Internet Protocol(IP), which is 0. This is the same number which appears on protocol field in the IP header of a packet.(man protocols for more details) 
* **return value**: 
   * On success, a file descriptor for the new socket is returned.  
   * On error, -1 is returned, and errno is set to indicate the error.
* [manual: socket](https://man7.org/linux/man-pages/man2/socket.2.html)

## Setsockopt:
```c
#include <sys/socket.h>

int setsockopt(int sockfd, int level, int optname, const void *optval, socklen_t optlen);
```
This helps in manipulating options for the socket referred by the file descriptor sockfd. This is completely optional, but it helps in reuse of address and port. Prevents error such as: “address already in use”.

## Bind
```c++
#include <sys/socket.h>

int bind(int sockfd, const struct sockaddr *addr, socklen_t addrlen);
```
After creation of the socket, **bind function binds the socket to the address and port number specified in addr**(custom data structure). In the example code, we bind the server to the localhost, hence we use INADDR_ANY to specify the IP address.

From manual: When a socket is created with socket(2), it exists in a namespace (address family) but has no address assigned to it.  bind() assigns the address specified by **addr** to the socket referred to, by the file descriptor sockfd.  **addrlen** specifies the size, in bytes, of the address structure pointed to by addr. Traditionally, this operation is called **“assigning a name to a socket”**.


* **return value**: 
   * On success, a file descriptor for the new socket is returned.  
   * On error, -1 is returned, and errno is set to indicate the error.
* [manual: bind](https://man7.org/linux/man-pages/man2/bind.2.html)


### sockaddr structure
```c
struct sockaddr {
  uint8_t sa_len;
  sa_family_t sa_family; /* address family: AF_xxx value */
  char sa_data[14];
};

struct sockaddr_in {
  uint8_t sin_len; /* length of structure (16)*/
  sa_family_t sin_family; /* AF_INET*/
  in_port_t sin_port; /* 16 bit TCP or UDP port number */
  struct in_addr sin_addr; /* 32 bit IPv4 address*/
  char sin_zero[8]; /* not used but always set to zero - remaining to 14*/
};

struct in_addr{
  in_addr_t s_addr; /*32 bit IPv4 network byte ordered address*/
};

```

## Listen
**Listen for connections on a socket.**
```c
#include <sys/socket.h>

int listen(int sockfd, int backlog);
```

It puts the server socket in a passive mode, where it waits for the client to approach the server to make a connection. 
* **sockfd**:  a file descriptor that refers to a socket of type SOCK_STREAM or SOCK_SEQPACKET.
* **backlog**: defines the maximum length to which the queue of pending connections for sockfd may grow. If a connection request arrives when the queue is full, the client may receive an error with an indication of ECONNREFUSED or, if the underlying protocol supports retransmission, the request may be ignored so that a later reattempt at connection succeeds.
* **return value**: 
   * On success, a file descriptor for the new socket is returned.  
   * On error, -1 is returned, and errno is set to indicate the error.
* [manual: listen](https://man7.org/linux/man-pages/man2/listen.2.html)

## Accept:
**Accept a connection on a socket**
```c++
#include <sys/socket.h>

int new_socket= accept(int sockfd, struct sockaddr *addr, socklen_t *addrlen);
```

It extracts the first connection request on the queue of pending connections for the listening socket, sockfd, creates a new connected socket, and returns a new file descriptor referring to that socket. At this point, connection is established between client and server, and they are ready to transfer data.
* **return value**: 
   * On success, a file descriptor for the new socket is returned.  
   * On error, -1 is returned, and errno is set to indicate the error.
* [manual: accept](https://man7.org/linux/man-pages/man2/accept.2.html)

## Connect
**Initiate a connection on a socket**
```c
#include <sys/socket.h>

int connect(int sockfd, const struct sockaddr *addr, socklen_t addrlen);
```
The connect() system call connects the socket referred to by the file descriptor **sockfd** to the address specified by **addr**. Server’s address and port is specified in addr.
* **return value**:
   * If the connection or binding succeeds, zero is returned.  
   * On error, -1 is returned, and errno is set to indicate the error.
* [manual: connect](https://man7.org/linux/man-pages/man2/connect.2.html)

Info taken from [here](https://www.geeksforgeeks.org/socket-programming-cc/) and manual.


## Close
**Close a file descriptor**
```c++
#include <unistd.h>

int close(int fd);
```
close() closes a file descriptor, so that it no longer refers to any file and may be reused.  Any record locks (see fcntl(2)) held on the file it was associated with, and owned by the process, are removed (regardless of the file descriptor that was used to obtain the lock).
* **return value**
   * Returns zero on success.  
   * On error, -1 is returned, and errno is set to indicate the error.
* [manual: close](https://man7.org/linux/man-pages/man2/close.2.html)

## Send
**Send a message on a socket**
```c
#include <sys/socket.h>

ssize_t send(int sockfd, const void *buf, size_t len, int flags);
```
The only difference between send() and write(2) is the presence of flags.  With a zero flags argument, send() is equivalent to write(2).
* **sockfd**: file descriptor of the sending socket
* **buf**: the message is found in buf and has length **len**
* **flags**: argument is the bitwise OR of zero or more of some flags.
* **return value**
   * On success, these calls return the number of bytes sent.
   * On error, -1 is returned, and errno is set to indicate the error.
* [manual: send](https://man7.org/linux/man-pages/man2/send.2.html)

## Recv
**Receive a message from a socket**
```c
#include <sys/socket.h>

ssize_t recv(int sockfd, void *buf, size_t len, int flags);
```
They may be used to receive data on both connectionless and connection-oriented sockets.  This page first describes common features of all three system calls, and then describes the differences between the calls. The only difference between recv() and read(2) is the presence of flags.  With a zero flags argument, recv() is generally equivalent to read(2).
* **sockfd**: file descriptor of the sending socket
* **buf**: the message is found in buf and has length **len**
* **return value**
   * On success, these calls return the number of bytes received.
   * On error, -1 is returned, and errno is set to indicate the error.
* [manual: send](https://man7.org/linux/man-pages/man2/recv.2.html)


# Example server.c
```c++
#include <stdio.h>
#include <sys/socket.h>
#include <netinet/ip.h>
#include <string.h>
#include <arpa/inet.h>
#include <unistd.h>

int main() {
    int sock = socket(AF_INET, SOCK_STREAM, 0);
    if (sock == -1) {
        perror("Could not open socket");
        return -3;
    }
    
    if(setsockopt(sock, SOL_SOCKET, SO_REUSEADDR , &(int){1}, sizeof(int))){
        perror("setsock");
        return -10;
    }

    struct sockaddr_in server; // <netinet/ip.h>
    memset(&server, 0, sizeof(server));
    server.sin_port = htons(1234);
    server.sin_family = AF_INET;
    server.sin_addr.s_addr = INADDR_ANY;

    int bind_err = bind(sock, (struct sockaddr *)&server, sizeof(server));
    if (bind_err == -1){
        perror("Could not bind socket");
        return -2;
    }

    if(listen(sock, 7) == -1){
        perror("Could not listen");
        return -1;
    }

    struct sockaddr_in client_addr;
    socklen_t client_addr_len;

    printf("Listening...\n");

    while(1) {
        printf("Listening for new connection...\n");
        
        int client_sock = accept(sock, (struct sockaddr *) &client_addr, &client_addr_len);

        char *client_ip = inet_ntoa(client_addr.sin_addr); 
        if (client_sock == -1) {
            perror("Could not connect to client");
            return -4;
        }

        printf("Client ip: %s", client_ip);
        close(client_sock);
    }

    return 0;
}
```

# Example client.c
```c++
#include <stdio.h>
#include <sys/socket.h>
#include <string.h>
#include <netinet/in.h>
#include <arpa/inet.h>

// gcc -Wall client.c

int main() {
    int sock = socket(AF_INET, SOCK_STREAM, 0);
    if (sock == -1) {
        perror("Could not open socket");
    }

    struct sockaddr_in server;
    memset(&server, 0, sizeof(server));
    server.sin_port = htons(1234);
    server.sin_family = AF_INET;
    server.sin_addr.s_addr = inet_addr("192.168.1.7");

    if (connect(sock, (struct sockaddr *) &server, sizeof(server)) == -1){
        perror("Could not connect to server!");
        return -1;
    }

    printf("YAAAAAY!!\n");
    return 0;
}
```
