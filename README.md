# Socket Programming in C/C++

## What is socket programming?

Socket programming is a way of connecting two nodes on a network
to communicate with each other. One socket(node) listens on a particular port at an IP,
while other socket reaches out to the other to form a connection.
Server forms the listener socket while client reaches out to the server.

## Stages for server

Socket creation:

```c
int sockfd = socket(domain, type, protocol)
```

> 
> sockfd: socket descriptor, an integer (like a file-handle)
> domain: integer, communication domain e.g., AF_INET (IPv4 protocol) ,
> AF_INET6 (IPv6 protocol)
> type: communication type
> SOCK_STREAM: TCP(reliable, connection oriented)
> SOCK_DGRAM: UDP(unreliable, connectionless)
> protocol: Protocol value for Internet Protocol(IP), which is 0.
> This is the same number which appears on protocol field in the IP header of a packet.(man protocols for more details)
>

Setsockopt:
```c
int setsockopt(int sockfd, int level, int optname,  

               const void *optval, socklen_t optlen);
```

> This helps in manipulating options for the socket referred by the file descriptor sockfd.
> This is completely optional, but it helps in reuse of address and port. Prevents error such as: “address already in use”.
>

Bind:
```c
int bind(int sockfd, const struct sockaddr *addr, 

                      socklen_t addrlen);
```

> After creation of the socket, bind function binds the socket to the address and port number specified in addr(custom data structure). In the example code, we bind the server to the localhost, hence we use INADDR_ANY to specify the IP address.
>

Listen:

```c
int listen(int sockfd, int backlog);
```

> 
> It puts the server socket in a passive mode, where it waits for the client to approach the server to make a connection. The backlog, defines the maximum length to which the queue of pending connections for sockfd may grow. If a connection request arrives when the queue is full, the client may receive an error with an indication of ECONNREFUSED.
>

Accept:

```c
int new_socket= accept(int sockfd, struct sockaddr *addr, socklen_t *addrlen);
```

> 
> It extracts the first connection request on the queue of pending connections for the listening socket,
> sockfd, creates a new connected socket, and returns a new file descriptor referring to that socket. At this point, connection is established between client and server, and they are ready to transfer data.
>

## Stages for Client

Socket connection: Exactly same as that of server’s socket creation
Connect:
```c
int connect(int sockfd, const struct sockaddr *addr,  

                         socklen_t addrlen);
```

Stages for server

Socket creation:

```
int sockfd = socket(domain, type, protocol)
sockfd: socket descriptor, an integer (like a file-handle)
```

> 
> domain: integer, communication domain e.g., AF_INET (IPv4 protocol) , AF_INET6 (IPv6 protocol)
> type: communication type
> SOCK_STREAM: TCP(reliable, connection oriented)
> SOCK_DGRAM: UDP(unreliable, connectionless)
> protocol: Protocol value for Internet Protocol(IP), which is 0. This is the same number which appears on protocol field in the IP header of a packet.(man protocols for more details)
>

Setsockopt:
```c
int setsockopt(int sockfd, int level, int optname,  

               const void *optval, socklen_t optlen);
```

This helps in manipulating options for the socket referred by the file descriptor sockfd. This is completely optional, but it helps in reuse of address and port. Prevents error such as: “address already in use”.

Bind:
```c
int bind(int sockfd, const struct sockaddr *addr, 

                      socklen_t addrlen);
```

After creation of the socket, bind function binds the socket to the address and port number specified in addr(custom data structure). In the example code, we bind the server to the localhost, hence we use INADDR_ANY to specify the IP address.

Listen:
int listen(int sockfd, int backlog);
It puts the server socket in a passive mode, where it waits for the client to approach the server to make a connection. The backlog, defines the maximum length to which the queue of pending connections for sockfd may grow. If a connection request arrives when the queue is full, the client may receive an error with an indication of ECONNREFUSED.

Accept:
int new_socket= accept(int sockfd, struct sockaddr *addr, socklen_t *addrlen);
It extracts the first connection request on the queue of pending connections for the listening socket, sockfd, creates a new connected socket, and returns a new file descriptor referring to that socket. At this point, connection is established between client and server, and they are ready to transfer data.

Stages for Client

Socket connection: Exactly same as that of server’s socket creation
Connect:
int connect(int sockfd, const struct sockaddr *addr,  
                             socklen_t addrlen);
The connect() system call connects the socket referred to by the file descriptor sockfd to the address specified by addr. Server’s address and port is specified in addr.Stages for server

Socket creation:
int sockfd = socket(domain, type, protocol)
sockfd: socket descriptor, an integer (like a file-handle)
domain: integer, communication domain e.g., AF_INET (IPv4 protocol) , AF_INET6 (IPv6 protocol)
type: communication type
SOCK_STREAM: TCP(reliable, connection oriented)
SOCK_DGRAM: UDP(unreliable, connectionless)
protocol: Protocol value for Internet Protocol(IP), which is 0. This is the same number which appears on protocol field in the IP header of a packet.(man protocols for more details)

Setsockopt:
int setsockopt(int sockfd, int level, int optname,  
                   const void *optval, socklen_t optlen);
This helps in manipulating options for the socket referred by the file descriptor sockfd. This is completely optional, but it helps in reuse of address and port. Prevents error such as: “address already in use”.

Bind:
int bind(int sockfd, const struct sockaddr *addr, 
                          socklen_t addrlen);
After creation of the socket, bind function binds the socket to the address and port number specified in addr(custom data structure). In the example code, we bind the server to the localhost, hence we use INADDR_ANY to specify the IP address.

Listen:
int listen(int sockfd, int backlog);
It puts the server socket in a passive mode, where it waits for the client to approach the server to make a connection. The backlog, defines the maximum length to which the queue of pending connections for sockfd may grow. If a connection request arrives when the queue is full, the client may receive an error with an indication of ECONNREFUSED.

Accept:
int new_socket= accept(int sockfd, struct sockaddr *addr, socklen_t *addrlen);
It extracts the first connection request on the queue of pending connections for the listening socket, sockfd, creates a new connected socket, and returns a new file descriptor referring to that socket. At this point, connection is established between client and server, and they are ready to transfer data.

Stages for Client

Socket connection: Exactly same as that of server’s socket creation
Connect:
int connect(int sockfd, const struct sockaddr *addr,  
                             socklen_t addrlen);
The connect() system call connects the socket referred to by the file descriptor sockfd to the address specified by addr. Server’s address and port is specified in addr.Stages for server

Socket creation:
int sockfd = socket(domain, type, protocol)
sockfd: socket descriptor, an integer (like a file-handle)
domain: integer, communication domain e.g., AF_INET (IPv4 protocol) , AF_INET6 (IPv6 protocol)
type: communication type
SOCK_STREAM: TCP(reliable, connection oriented)
SOCK_DGRAM: UDP(unreliable, connectionless)
protocol: Protocol value for Internet Protocol(IP), which is 0. This is the same number which appears on protocol field in the IP header of a packet.(man protocols for more details)

Setsockopt:
int setsockopt(int sockfd, int level, int optname,  
                   const void *optval, socklen_t optlen);
This helps in manipulating options for the socket referred by the file descriptor sockfd. This is completely optional, but it helps in reuse of address and port. Prevents error such as: “address already in use”.

Bind:
int bind(int sockfd, const struct sockaddr *addr, 
                          socklen_t addrlen);
After creation of the socket, bind function binds the socket to the address and port number specified in addr(custom data structure). In the example code, we bind the server to the localhost, hence we use INADDR_ANY to specify the IP address.

Listen:
int listen(int sockfd, int backlog);
It puts the server socket in a passive mode, where it waits for the client to approach the server to make a connection. The backlog, defines the maximum length to which the queue of pending connections for sockfd may grow. If a connection request arrives when the queue is full, the client may receive an error with an indication of ECONNREFUSED.

Accept:
int new_socket= accept(int sockfd, struct sockaddr *addr, socklen_t *addrlen);
It extracts the first connection request on the queue of pending connections for the listening socket, sockfd, creates a new connected socket, and returns a new file descriptor referring to that socket. At this point, connection is established between client and server, and they are ready to transfer data.

Stages for Client

Socket connection: Exactly same as that of server’s socket creation
Connect:
int connect(int sockfd, const struct sockaddr *addr,  
                             socklen_t addrlen);
The connect() system call connects the socket referred to by the file descriptor sockfd to the address specified by addr. Server’s address and port is specified in addr.Stages for server

Socket creation:
int sockfd = socket(domain, type, protocol)
sockfd: socket descriptor, an integer (like a file-handle)
domain: integer, communication domain e.g., AF_INET (IPv4 protocol) , AF_INET6 (IPv6 protocol)
type: communication type
SOCK_STREAM: TCP(reliable, connection oriented)
SOCK_DGRAM: UDP(unreliable, connectionless)
protocol: Protocol value for Internet Protocol(IP), which is 0. This is the same number which appears on protocol field in the IP header of a packet.(man protocols for more details)

Setsockopt:
int setsockopt(int sockfd, int level, int optname,  
                   const void *optval, socklen_t optlen);
This helps in manipulating options for the socket referred by the file descriptor sockfd. This is completely optional, but it helps in reuse of address and port. Prevents error such as: “address already in use”.

Bind:
int bind(int sockfd, const struct sockaddr *addr, 
                          socklen_t addrlen);
After creation of the socket, bind function binds the socket to the address and port number specified in addr(custom data structure). In the example code, we bind the server to the localhost, hence we use INADDR_ANY to specify the IP address.

Listen:
int listen(int sockfd, int backlog);
It puts the server socket in a passive mode, where it waits for the client to approach the server to make a connection. The backlog, defines the maximum length to which the queue of pending connections for sockfd may grow. If a connection request arrives when the queue is full, the client may receive an error with an indication of ECONNREFUSED.

Accept:
int new_socket= accept(int sockfd, struct sockaddr *addr, socklen_t *addrlen);
It extracts the first connection request on the queue of pending connections for the listening socket, sockfd, creates a new connected socket, and returns a new file descriptor referring to that socket. At this point, connection is established between client and server, and they are ready to transfer data.

Stages for Client

Socket connection: Exactly same as that of server’s socket creation
Connect:
int connect(int sockfd, const struct sockaddr *addr,  
                             socklen_t addrlen);
The connect() system call connects the socket referred to by the file descriptor sockfd to the address specified by addr. Server’s address and port is specified in addr.Stages for server

Socket creation:
int sockfd = socket(domain, type, protocol)
sockfd: socket descriptor, an integer (like a file-handle)
domain: integer, communication domain e.g., AF_INET (IPv4 protocol) , AF_INET6 (IPv6 protocol)
type: communication type
SOCK_STREAM: TCP(reliable, connection oriented)
SOCK_DGRAM: UDP(unreliable, connectionless)
protocol: Protocol value for Internet Protocol(IP), which is 0. This is the same number which appears on protocol field in the IP header of a packet.(man protocols for more details)

Setsockopt:
int setsockopt(int sockfd, int level, int optname,  
                   const void *optval, socklen_t optlen);
This helps in manipulating options for the socket referred by the file descriptor sockfd. This is completely optional, but it helps in reuse of address and port. Prevents error such as: “address already in use”.

Bind:
int bind(int sockfd, const struct sockaddr *addr, 
                          socklen_t addrlen);
After creation of the socket, bind function binds the socket to the address and port number specified in addr(custom data structure). In the example code, we bind the server to the localhost, hence we use INADDR_ANY to specify the IP address.

Listen:
int listen(int sockfd, int backlog);
It puts the server socket in a passive mode, where it waits for the client to approach the server to make a connection. The backlog, defines the maximum length to which the queue of pending connections for sockfd may grow. If a connection request arrives when the queue is full, the client may receive an error with an indication of ECONNREFUSED.

Accept:
int new_socket= accept(int sockfd, struct sockaddr *addr, socklen_t *addrlen);
It extracts the first connection request on the queue of pending connections for the listening socket, sockfd, creates a new connected socket, and returns a new file descriptor referring to that socket. At this point, connection is established between client and server, and they are ready to transfer data.

Stages for Client

Socket connection: Exactly same as that of server’s socket creation
Connect:
int connect(int sockfd, const struct sockaddr *addr,  
                             socklen_t addrlen);
The connect() system call connects the socket referred to by the file descriptor sockfd to the
address specified by addr. Server’s address and port is specified in addr.The connect() system call connects the socket referred to by the file descriptor sockfd to the address specified by addr. Server’s address and port is specified in addr.



1. **Stream Sockets**
   Stream sockets provide **reliable two-way** communication similar to when we call someone on the phone. One side initiates the connection to the other, and after the connection is established, either side can communicate to the other.
   In addition, there is immediate confirmation that what we said actually reached its destination. 
   Stream sockets use a **Transmission Control Protocol (TCP)**, which exists on the transport layer of the Open Systems Interconnection (OSI) model. The data is usually transmitted in packets. TCP is designed so that the packets of data will arrive without errors and in sequence. 
   Webservers, mail servers, and their respective client applications all use TCP and stream socket to communicate.

2. ​

3. Datagram Sockets

   Communicating with a datagram socket is more like mailing a letter than making a phone call. The connection is one-way only and unreliable

   ​

   If we mail several letters, we can't be sure that they arrive in the same order, or even that they reached their destination at all. Datagram sockets use User Datagram Protocol (UDP)

   . Actually, it's not a real connection, just a basic method for sending data from one point to another.

   Datagram sockets and UDP are commonly used in networked games and streaming media.

   Though in this section, we mainly put focus on applications that maintain connections to their clients, using connection-oriented TCP, there are cases where the overhead of establishing and maintaining a socket connection is unnecessary.

   For example, just to get the data, a process of creating a socket, making a connection, reading a single response, and closing the connection, is just too much. In this case, we use UDP.

   Services provided by UDP are typically used where a client needs to make a short query of a server and expects a single short response. To access a service from UDP, we need to use the UDP specific system calls, sendto() and recvfrom() instead of read() and write() on the socket.

   UDP is used by app that doesn't want reliability or bytestreams.

   1. Voice-over-ip (unreliable) such as conference call. (visit [VoIP](http://www.bogotobogo.com/VideoStreaming/VoIP.php))
   2. DNS, RPC (message-oriented)
   3. DHCP (bootstrapping)

## Client/Server

The **client-server model** distinguishes between applications as well as devices. **Network clients make requests to a server by sending messages**, and **servers respond to their clients by acting on each request and returning results**.

For example, let's talk about **telnet**. 
When we connect to a remote host on port 23 with telnet (the client), a program on that host (called **telnetd**, the server) springs to life. It handles the incoming telnet connection, sets us up with a login prompt, etc.

One server generally supports numerous clients, and multiple servers can be networked together in a pool to handle the increased processing load as the number of clients grows.

Some of the most popular applications on the Internet follow the client-server model including email, FTP and Web services. Each of these clients features a user interface and a client application that allows the user to connect to servers. In the case of email and FTP, users enter a computer name (or an IP address) into the interface to set up connections to the server.

The steps to establish a socket on the **server** side are:

1. Create a socket with the **socket()** system call. 
2. The server process gives the socket a name. In linux file system, local sockets are given a filename, under /tmp or /usr/tmp directory. For network sockets, the filename will be a service identifier, port number, to which the clients can make connection. This identifier allows to route incoming connections (which has that the port number) to connect server process. A socket is named using **bind()** system call. 
3. The server process then waits for a client to connect to the named socket, which is basically listening for connections with the **listen()** system call. If there are more than one client are trying to make connections, the **listen()** system call make a queue.
   The machine receiving the connection (the server) must bind its socket object to a known port number. A port is a 16-bit number in the range 0-65535 that's managed by the operating system and used by clients to uniquely identify servers. Ports 0-1023 are reserved by the system and used by common network protocols.
4. Accept a connection with the **accept()** system call. At **accept()**, a new socket is created that is distinct from the named socket. This new socket is used solely for communication with this particular client.
   For TCP servers, the socket object used to receive connections is not the same socket used to perform subsequent communication with the client. In particular, the **accept()**system call returns a new socket object that's actually used for the connection. This allows a server to manage connections from a large number of clients simultaneously.
5. Send and receive data.
6. The named socket remains for further connections from other clients. A typical web server can take advantage of multiple connections. In other words, it can serve pages to many clients at once. But for a simple server, further clients wait on the listen queue until the server is ready again.

The steps to establish a socket on the **client** side are:

1. Create a socket with the **socket()** system call. 
2. Connect the socket to the address of the server using the **connect()** system call.
3. Send and receive data. There are a number of ways to do this, but the simplest is to use the **read()** and **write()** system calls.

**TCP communication**

**UDP communication** - clients and servers don't establish a **connection** with each other

*call block, go to [Blocking socket vs non-blocking socket ](http://www.bogotobogo.com/cplusplus/sockets_server_client.php#block_vs_non_blocking).



## Socket Functions

**Sockets**, in C, behaves like files because they use file descriptors to identify themselves. Sockets behave so much like files that we can use the **read()** and **write()** to receive and send data using **socket file descriptors**.

There are several functions, however, specifically designed to handle sockets. These functions have their prototypes defined in 

/usr/include/sys/sockets.h

.

1. **int socket(int domain, int type, int protocol)**

   Used to create a new socket, returns a file descriptor for the socket or -1 on error.
   It takes three parameters: 

   1. domain: the protocol family of socket being requested
   2. type: the type of socket within that family
   3. and the protocol.

   ​

   The parameters allow us to say what kind of socket we want (IPv4/IPv6, stream/datagram(TCP/UDP)).

   ​

   1. The protocol family should be **AF_INET** or **AF_INET6**
   2. and the protocol type for these two families is 
      either **SOCK_STREAM** for TCP/IP or **SOCK_DGRAM** for UDP/IP.
   3. The protocol should usually be set to zero to indicate that the default protocol should be used.

   ​

   ​

2. **int bind(int fd, struct sockaddr \*local_addr, socklen_t addr_length) **

   Once we have a socket, we might have to associate that socket with a port on our local machine.
   The port number is used by the kernel to match an incoming packet to a certain process's socket descriptor.
   A server will call **bind()** with the address of the local host and the port on which it will listen for connections.
   It takes file descriptor (previously established socket), a pointer to (the address of) a structure containing the details of the address to bind to, the value **INADDR_ANY** is typically used for this, and the length of the address structure.
   The particular structure that needs to be used will depend on the protocol, which is why it is passed by the pointer.
   So, this **bind()** call will bind the socket to the current IP address on port, portno
   Returns 0 on success and -1 on error.

3. **int listen(int fd, int backlog_queue_size) **

   Once a server has been bound to an address, the server can then call **listen()** on the socket.
   The parameters to this call are the socket (fd) and the maximum number of queued connections requests up to **backlog_queue_size**.
   Returns 0 on success and -1 on error.

4. **int accept(int fd, struct sockaddr \*remote_host, socklen_t addr_length) **

   Accepts an incoming connection on a bound socket. The address information from the remote host is written into the **remote_host** structure and the actual size of the address structure is written into ***addr_length**.
   In other words, this **accept()** function will write the connecting client's address info into the address structure.
   Then, returns a new socket file descriptor for the accepted connection.
   So, the original socket file descriptor can continue to be used for accepting new connections while the new socket file descriptor is used for communicating with the connected client.
   This function returns a new socket file descriptor to identify the connected socket or -1 on error.

   Here is the description from the man page:
   "It extracts the first connection request on the queue of pending connections for the listening socket, **sockfd**, creates a new connected socket, and returns a new file descriptor referring to that socket. The newly created socket is not in the listening state. The original socket sockfd is unaffected by this call".

   If no pending connections are present on the queue, and the socket is not marked as nonblocking, accept() blocks the caller until a connection is present.

5. **int connect(int fd, struct sockaddr \*remote_host, socklen_t addr_length) **

   Connects a socket (described by file descriptor **fd**) to a remote host. 
   Returns 0 on success and -1 on error.

   This is a blocking call. That's because when we issue a call to connect(), our program doesn't regain control until either the connection is made, or an error occurs. For example, let's say that we're writing a web browser. We try to connect to a web server, but the server isn't responding. So, we now want the connect() API to stop trying to connect by clicking a stop button. But that can't be done. It waits for a return which could be 0 on success or -1 on error.

6. **int send(int fd, void \*buffer, size_t n, int flags) **

   Sends n bytes from ***buffer** to **socket fd**.
   Returns the number of bytes sent or -1 on error.

7. **int receive(int fd, void \*buffer, size_t n, int flags) **

   Reveives n bytes from **socket fd** into ***buffer**.
   Returns the number of bytes received or -1 on error.

   This is another blocking call. In other words, when we call **recv()** to read from a stream, control isn't returned to our program until at least one byte of data is read from the remote site. This process of waiting for data to appear is referred to as **blocking**. The same is true for the write() and the connect() APIs, etc. When we run those blocking APIs, the connection "blocks" until the operation is complete.

http://www.bogotobogo.com/cplusplus/sockets_server_client.php