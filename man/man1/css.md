# NAME

css - multiplex multiple clients on one connect stream server

# SYNOPSIS

`css` \[ `options` \] connect-stream command \[ arg ... \]

# DESCRIPTION

`css` multiplexes multiple clients on one filter server. A filter
server is a process that reads lines from the standard input and writes
result lines to the standard output. `connect-stream` is the connect
stream path by which the filter service will be known.

# OPTIONS

-`t`, --`timeout`=`time`
:   The service will exit after a `time` period of client inactivity.

# PROTOCOL

A filter service must follow a simple line oriented protocol. All client
lines are split into arguments and a number is inserted in the second
argument position. This number, followed by a space, must be placed at
the beginning of each line written by the filter server for the given
client request.

# SEE ALSO

[`coshell`](/web/20141128030242/http://www2.research.att.com/~astopen/man/man1/coshell.html)(1),
[`cs`](/web/20141128030242/http://www2.research.att.com/~astopen/man/man1/cs.html)(1),
[`ss`](/web/20141128030242/http://www2.research.att.com/~astopen/man/man1/ss.html)(1),
[`cs`](/web/20141128030242/http://www2.research.att.com/~astopen/man/man3/cs.html)(3)

# IMPLEMENTATION

`version`
:   css (AT&T Research) 1998-05-01

`author`
:   Glenn Fowler

`copyright`
:   Copyright © 1990-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030242/http://www.eclipse.org/org/documents/epl-v10.html)


