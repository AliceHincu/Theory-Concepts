# UDP
In UDP, the client does not form a connection with the server like in TCP and instead just sends a datagram. Similarly, the server need not accept a connection and just waits for datagrams to arrive. Datagrams upon arrival contain the address of sender which the server uses to send data to the correct client.

**The entire process can be broken down into following steps :**
### UDP Server
1. Create UDP socket.
2. Bind the socket to server address.
3. Wait until datagram packet arrives from client.
4. Process the datagram packet and send a reply to client.
5. Go back to Step 3.

### UDP Client
1. Create UDP socket.
2. Send message to server.
3. Wait until response from server is received.
4. Process reply and go back to step 2, if necessary.
5. Close socket descriptor and exit.

## Creation of socket
**Creates an unbound socket in the specified domain.**
```c
#include <sys/socket.h>

int socket(int domain, int type, int protocol)
```

* **domain** – Specifies the communication domain ( AF_INET for IPv4/ AF_INET6 for IPv6 )
* **type** – Type of socket to be created ( SOCK_STREAM for TCP / **SOCK_DGRAM for UDP** )
* **protocol** – Protocol to be used by socket. 0 means use default protocol for the address family.
* **returns** - socket file descriptor

## Binding
**Assigns address to the unbound socket.**
```c
#include <sys/socket.h>

int bind(int sockfd, const struct sockaddr *addr, socklen_t addrlen)
```

* **sockfd** – File descriptor of socket to be binded
* **addr** – Structure in which address to be binded to is specified
* **addrlen** – Size of addr structure

## Sending
**Send a message on the socket**
```c
#include <sys/types.h>
#include <sys/socket.h>

ssize_t sendto(int sockfd, const void *buf, size_t len, int flags,
               const struct sockaddr *dest_addr, socklen_t addrlen)
```

* **sockfd** – File descriptor of socket
* **buf** – Application buffer containing the data to be sent
* **len** – Size of buf application buffer
* **flags** – Bitwise OR of flags to modify socket behaviour
* **dest_addr** – Structure containing address of destination
* **addrlen** – Size of dest_addr structure

## Receiving
**Receive a message from the socket.**
```c
#include <sys/types.h>
#include <sys/socket.h>

ssize_t recvfrom(int sockfd, void *buf, size_t len, int flags,
                 struct sockaddr *src_addr, socklen_t *addrlen)
```

* **sockfd** – File descriptor of socket
* **buf** – Application buffer in which to receive data
* **len** – Size of buf application buffer
* **flags** – Bitwise OR of flags to modify socket behaviour
* **src_addr** – Structure containing source address is returned
* **addrlen** – Variable in which size of src_addr structure is returned

## Closing socket
**Close a file descriptor**
```c
#include <unistd.h>

int close(int fd)
```

* **fd** – File descriptor

## bcopy
**The bcopy() function copies n bytes from src to dest. The result is correct, even when both areas overlap. Does not return anything.**
```c
#include <strings.h>

void bcopy(const void *src, void *dest, size_t n);
```

