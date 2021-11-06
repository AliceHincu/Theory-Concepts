## recvfrom
**Receive data from the socket**. 

```py
bytesAddressPair = UDPServerSocket.recvfrom(bufferSize)
message = bytesAddressPair[0]
address = bytesAddressPair[1]
```

**The return value is a pair (bytes, address)** where bytes is a bytes object representing the data received and address is the address of the socket sending the data

## sendto
Send data to the socket. The socket should not be connected to a remote socket, since the destination socket is specified by address
```py

```
