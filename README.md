# Creating chat room using C (Socket Programming).
### What does this chatroom do?
So basically this chatroom there will be two main components a *Server* and *Client*.<br>
The server is responsible for connecting the client to the chatroom. And manage the client activity and data flow.
The client is said to be a user Who is chatting.
### Now let's know about the working principle of This Chatroom.
Socket programming is a way of connecting two nodes on a network to communicate with each other. In the context of a chatroom, the basic working principle involves the use of sockets to establish connections between the clients (users) and the server, enabling real-time communication between them.  
## Prerequisites:
As this code is for Linux and iOS-based operating systems so, to create the above project you needed.<br>
--->A Linux or ios Operating system.<br>
--->With gcc compiler.<br>
--->Intermediate knowledge of c language.<br>
The above things will be more than enough<br>
## Let's Start with the project.
### (For the Server side!)
Now you have to create a C file name "Server. c". With the help of the terminal.<br>
To create the file type:
```terminal
gedit Server.c
````
This will open a file and here we write out the code of socket programming in c language.<br>
So, For creating sockets and getting client requests we need to use some of the libraries of C language.
Such as:
```c
#include<stdio.h>
#include<stdlib.h>
#include<unistd.h>
#include<sys/types.h>
#include<sys/socket.h>
#include<netinet/in.h>
#include<string.h>
````
### Let's see the libraries one by one.
The header file is responsible for the standard input-output header file. Ir provides declarations for functions and macros that are used for input and output operations in C. Some of the functions such as 'scanf()','fprintf()'and 'fclose()' etc.
```c
#include<stdio.h>
````

The header file is responsible for the *Standard library*. It provides the declarations for several standard functions, types, and macros that are widely used in c programming for as memory allocation, conversion, random number generation, searching, sorting, etc.

```c
#include<stdlib.h>
````

Again this header file is *Unix standard*. It provides access to various POSIX (Portable Operating system interface) operating system servers. Some functions such as 'fork()' this function create duplicates. 'exec()' exec functions run a new program by replacing the current process image with a new process image obtained from a file in the HFS (hierarchical file system) etc.
```c
#include<unistd.h>
````

The header file defines various data types used in system programming, especially in Unix-like operating systems. One of the common functions are 'size_t' Unsigned integer type used to represent the sizes of objects. and 'pid_t' Integer type used to represent process IDs.
```c
#include<sys/types.h>
````

This header file is responsible for the essential component of socket programming in C language. In other words, this is the most important header file that needs to be included so we can provide the necessary declaration for socket-related functions, constants, and data structures used for communication between processes over the network. For example, we have some *Important functions* such as 'sock_stream' this function is responsible for the implementation of the tcp's.
```c
#include<sys/socket.h>
````

Now, This header file is essential for networking programming in C, particularly for working with IP or we can say internet addresses and sockets. Mainly it works in the field of networks it has a function named 'sockaddr_in' which structure for handling IP addresses and port numbers.
```c
#include<netinet/in.h>
````

We have a basic header file named string it is used for using the functionality about the string link entering a string, finding the length of a string, etc.
```c
#include<string.h>
````

### Let's create the ERROR function.
```c
void error(const char *msg)
     {
        perror(msg);
        exit(1);
     }
````
This is the first line after importing the libraries. So we know that at the time of creating a function, we have to give the type of the function so, here it is void and in its argument, we have the massage pointer as char variable type. Now in the function, we have a line ```perror()```  another function that is used to print the error message to the standard error stream. The 'msg' This is a string that is typically used to provide additional context to the error message. When we see the function we can observe that it is working on recursive Methode.

### Now Let's go for the main function.
```c
int main(int argc,char *argv[])
{
    if(argc<2)
     {
        fprintf(stderr,"Prot no. not prvided. Program terminated\n");
        exit(1);     
     }
```
So, After writing the error function we are on the main function. ```int main(int argc,char *argc[])``` in this line we can see *argc* it stands for argument count. It represents the number of command-line arguments passed to the program when it is executed.
Also, we can see that we have a ```fprintf```. It is used to write formatted data to a file. It's part of the standard I/O library. 
```c
     int sockfd,newsockfd,portno,n;
     char buffer[255];
     struct sockaddr_in serv_addr,cli_addr;
     socklen_t clilen;
     sockfd = socket(AF_INET, SOCK_STREAM,0);
````
Now, In the next part, we are declaring the data types of the variables. As we have ```buffer[255]``` is a char,and ```stuct sockaddr_in  => serv_addr,cli_addr.```This is just an explanation of the structure. 
#### (You no need to code it.)
```c
struct sockaddr_in {
    short            sin_family;   // Address family (e.g., AF_INET)
    unsigned short   sin_port;     // Port number (in network byte order)
    struct in_addr   sin_addr;     // IP address
    char             sin_zero[8];  // Padding to make the structure the same size as struct sockaddr
};
````
And, In the next line, we have ``` socklen_t clilen;``` which represents the length of the socket address structure. When we are dealing with functions like *accept()* or *recvfrom()*, which involve receiving data from the client, you need to specify the size of the client's address structure.
Again, We have another function ```sockfd = socket(AF_INET, SOCK_STREAM,0);```. In the line we can see that *sockfd* is a variable used to create the socket using the socket function. This line of code is used to create the socket.
### Next part of code after declaring the variables and calling functions. We have
```c
if(sockfd<0)
     {
        error("Error opening Socket.");
     }
````
We have an if-else condition which says if we don't have any connection it will show the Error opening Socket.
### Now, after giving the condition.
```c
     bzero((char *) &serv_addr,sizeof(serv_addr));
     portno = atoi(argv[1]);
     serv_addr.sin_family=AF_INET;
     serv_addr.sin_addr.s_addr = INADDR_ANY;
     serv_addr.sin_port = htons(portno);
````
As, We can see in the above code a ```bzero()``` function is used it is used for the initialized memory, particularly for data structs or buffers that will be used in networking operations. Now, bzero() is used in socket programming.<br>1. Memory initialization.<br>
2. Security.<br>
3. Compatibility.<br>
Now the function explanation is:
```c
   #include <stddef.h>
    void bzero(void *s, size_t n)
   {
    char *p = (char *)s;
    while (n-- > 0)
   {
        *p++ = 0;
   }
   }
```











 

