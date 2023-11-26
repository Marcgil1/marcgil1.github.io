---
title: "Web server"
date: 2021-04-10
draft: false
showTableOfContents: true
showReadingTime: false
---

You may find this project
[here](https://github.com/Marcgil1/web_server).

It was developed for a networking course in my CS bachelors at the begining of
2021, even though I'm making it public on 2023. It being developed 2 years ago
means that code quality, even though decent, could be better. In particular,
functions should follow the 1-screen rule (all their code should fit within 1
screen), and thus the present ones should further subdivide their functionality
amongst several other subprocedures. Furthermore, C being C, Valgrind should be
used for checking whether there are any memory leaks. Despite all of this, the
code itself is quite neat and easy to read. I hope that the following
introduction to the project, as well as the code itself, will support this
assertion.

## Introduction

The present proyect aims to develop a simple, yet functional, web server. For
this matter, the server includes capabilities for handling `GET` request, code
being modular enough for easily being extended to handle other request types.

In its current form, the code cosists of (1) an entry point listening to the
relevan socket and reading information, (2) an HTTP module for parsing HTTP
requests, (3) a debug module including functionality for creating logs during
the execution of the server, and (4) a resource folder which is to be inputed as
a paramater to the server executable and which contains the web content to be
served. This content may have any MIME type whatsoever, and the default content
stored in `content/web` contains a sample web page including HTML, CSS and JS
files, as well as a _favicon_ and a couple of images.

Furthermore, this project abides to the requirements of the course for which it
was developed, which were for it to be implemented in ANSI C, and to store a
cookie in the user's browser holding the number of times the webpage was
visited. Should the user visit the webpage for more than this number of times,
an error message would be sent as response.

## How to execute the server

In order to execute the server, clone the repository linked
[above](https://github.com/Marcgil1/web_server), and execute `make build` and
`make start` this will build the program and execute it over the 8080 port
serving the sample webpage stored in `resources/web`. If you want the server to
run on any other port or to server content in some other folder, just run `make
build` and then call `build/out/main.out [port] [folder]`. Logs created during
execution are stored in `resources/log/webserver.log`.

The current makefile also includes functionality for running unit tests on the
coder. For this matter, run `make build_test` and `make test`.

## A comment on the implementation

### Modularity

An effort has been made for separating logical functionality of the code between
different modules. In particular, all functionality for representing and parsing
HTTP requests has been abstracted into an `http` module. This enables separation
of concerns and facilitates unit testing. Furthermore, the chosen approach of
structuring the module arround the processing of three data types, `http_req_t`,
`http_res_t`, and `http_cookie_t`, in addition to being conceptually pleasant,
lends itself to a very OOP style. Of course, to the extent to which C allows.

If further work were to be carried on the project, one further milestone in this
direction would be to abstract all the socket operations into a `server` module,
which would also offer a good opportunity for refining that code.  Furthermore,
it would be nice to investigate whether any C libraries allow mocking the socket
functionality, since this would greatly simplify testing of this proposed new
module.

### Unit Testing

Unit tests have been implemented for code in the `http` module leveraging the
[UNITY unit testing library](https://github.com/ThrowTheSwitch/Unity). This is a
particularly neat and light-weight library whose only requirement on the testing
code is to start it by calling `UNITY_BEGIN` in a main function, and then
defining and running tests with the macro `RUN_TEST`.

### Logging

All logging functionality has been abstracted into a `debug` module offering
`dg_log`, `dg_wrn` and `dg_err`-level logging. Also, it was decided that this
module would hold the logging file as a global variable. This choice was taken
with the folowing considerations in mind:
1. This approach leads to a particularly simple implementation, its only
   overhead other than calling the log functions being indicating a path to the
   log file and closing it once finished.
2. Should the server become parallel (which is currently not), this approach
   would lead to race conditions when writing the logs, since the logging file
   would then be a shared resource. Should one want to make this server
   parallel, some access control mechanism would have to be implemented in order
   to avoid race conditions.

## Further work

I can see three main lines over which this project may be extended. Roughly in
order of importance, these would be:
1. Making the code more modular by abstracting all external communication into a
   `server` module.
2. Extend the code for also handling other types of HTTP requests.
3. Make the server parallel, by holding a pool of threads to be assigned to
   specific requests, so that several users may be served concurrently.
