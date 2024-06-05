# Webserv

This README provides detailed information about the "Webserv" project, including its objectives, instructions, and requirements.

## Summary
This project is about writing your own HTTP server. You will be able to test it with an actual browser. HTTP is one of the most used protocols on the internet, and knowing its intricacies will be useful, even if you won’t be working on a website.

## Contents
1. [Introduction](#introduction)
2. [General Rules](#general-rules)
3. [Mandatory Part](#mandatory-part)
4. [Bonus Part](#bonus-part)

## Introduction
The Hypertext Transfer Protocol (HTTP) is an application protocol for distributed, collaborative, hypermedia information systems. It is the foundation of data communication for the World Wide Web, where hypertext documents include hyperlinks to other resources that users can easily access.

HTTP was developed to facilitate hypertext and the World Wide Web. The primary function of a web server is to store, process, and deliver web pages to clients. The communication between client and server takes place using HTTP.

## General Rules
- Your program should not crash in any circumstances (even when it runs out of memory) and should not quit unexpectedly. If it happens, your project will be considered non-functional and you will receive a grade of 0.
- You have to turn in a Makefile which will compile your source files. It must not relink.
- Your Makefile must at least contain the rules: `$(NAME)`, `all`, `clean`, `fclean`, and `re`.
- Compile your code with `c++` and the flags `-Wall`, `-Wextra`, `-Werror`.
- Your code must comply with the C++ 98 standard. Then, it should still compile if you add the flag `-std=c++98`.
- Try to always develop using the most C++ features you can. You are allowed to use C functions, but always prefer their C++ versions if possible.
- Any external library and Boost libraries are forbidden.

## Mandatory Part
### Program Name
`webserv`

### Turn-in Files
`Makefile`, `*.{h, hpp}`, `*.cpp`, `*.tpp`, `*.ipp`, configuration files

### Makefile
`NAME`, `all`, `clean`, `fclean`, `re`

### Arguments
[A configuration file]

### External Functions
Everything in C++ 98, including:
- `execve`
- `dup`, `dup2`
- `pipe`
- `strerror`, `gai_strerror`, `errno`
- `fork`
- `socketpair`
- `htons`, `htonl`, `ntohs`, `ntohl`
- `select`, `poll`, `epoll` (epoll_create, epoll_ctl, epoll_wait), `kqueue` (kqueue, kevent)
- `socket`, `accept`, `listen`, `send`, `recv`
- `chdir`, `bind`, `connect`, `getaddrinfo`, `freeaddrinfo`, `setsockopt`, `getsockname`, `getprotobyname`
- `fcntl`, `close`, `read`, `write`, `waitpid`, `kill`, `signal`, `access`, `stat`, `open`, `opendir`, `readdir`, `closedir`

### Libft Authorized
n/a

### Description
A HTTP server in C++ 98. Your executable will be run as follows: `./webserv [configuration file]`

### Requirements
- Your program has to take a configuration file as an argument or use a default path.
- You can’t execve another web server.
- Your server must never block, and the client can be bounced properly if necessary.
- It must be non-blocking and use only 1 poll() (or equivalent) for all the I/O operations between the client and the server (listen included).
- poll() (or equivalent) must check read and write at the same time.
- You must never do a read or a write operation without going through poll() (or equivalent).
- Checking the value of errno is strictly forbidden after a read or a write operation.
- You don’t need to use poll() (or equivalent) before reading your configuration file.
- A request to your server should never hang forever.
- Your server must be compatible with the web browser of your choice.
- Your HTTP response status codes must be accurate.
- Your server must have default error pages if none are provided.
- You can’t use fork for something else than CGI (like PHP, or Python, etc.).
- You must be able to serve a fully static website.
- Clients must be able to upload files.
- You need at least GET, POST, and DELETE methods.
- Stress test your server. It must stay available at all costs.
- Your server must be able to listen to multiple ports (see Configuration file).

### For MacOS Only
Since MacOS doesn’t implement write() the same way as other Unix OSes, you are allowed to use fcntl(). You must use file descriptors in non-blocking mode to get a behavior similar to that of other Unix OSes. However, you are only allowed to use fcntl() with the following flags: `F_SETFL`, `O_NONBLOCK`, and `FD_CLOEXEC`. Any other flag is forbidden.

### Configuration File
You can get some inspiration from the 'server' part of NGINX configuration file. In the configuration file, you should be able to:
- Choose the port and host of each 'server'.
- Setup the server_names or not.
- The first server for a host:port will be the default for this host:port.
- Setup default error pages.
- Limit client body size.
- Setup routes with one or multiple of the following rules/configuration (routes won’t be using regexp):
  - Define a list of accepted HTTP methods for the route.
  - Define a HTTP redirection.
  - Define a directory or a file from where the file should be searched.
  - Turn on or off directory listing.
  - Set a default file to answer if the request is a directory.
  - Execute CGI based on certain file extension.
  - Make it work with POST and GET methods.
  - Make the route able to accept uploaded files and configure where they should be saved.

## Bonus Part
Here are the extra features you can add:
- Support cookies and session management (prepare quick examples).
- Handle multiple CGI.
