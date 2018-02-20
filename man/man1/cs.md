# NAME

cs - connect stream control

# SYNOPSIS

`cs` \[ `options` \] \[ \[ - \] host | path \[ command ... \] \]

# DESCRIPTION

`cs` displays, initiates, and terminates connect stream services, and
displays the contents of connect stream message files. If no options are
spcified then the connect stream for `path` is opened. If the
corresponding service is not running then it is initiated and the
connection is attempted again. If `command` is specified then it is
executed with the standard input, standard output and standard error
redirected to the `path` connect stream. If `command` is omitted then
the `/dev/` equivalent path for the connect stream is listed on the
standard output.

# OPTIONS

-`a`, --`attribute`=`name`
:   List the attribute `name` for each host. If `name` is `-` then all
    attributes are listed. The hostname attribute is listed without a
    label, all other attributes are listed as `label`=`value`

-`c`, --`cat`
:   Catenate messages in the named `path` operands. If `path` is omitted
    then the standard input is read.

-`d`, --`debug`=`level`
:   Set the debug trace level to `level`. Higher levels produce
    more output.

-`f`, --`continuous`
:   Used with `--cat` to list messages on a `path` or standard input
    that is continuously updated.

-`h`, --`hostenvironment`
:   Lists `HOSTNAME`=`name` `HOSTTYPE`=`type` on the standard output
    for the named `host` operand or the local host if `host` is omitted.
    This is useful for `.profile` initialization.

-`i`, --`interactive`
:   Open an interactive connection to the connect stream. The service is
    initiated if it is not already running.

-`k`, --`kill`=`signal`
:   Send `signal` to the server on the connect stream named by `path`.
    `signal` may be a signal name or signal number.

-`l`, --`list`
:   List the active connect stream services on the standard output.

-`m`, --`mount`
:   List the active connect stream mount directories on the
    standard output.

-`p`, --`process`
:   List the active connect stream process ids on the standard output.

-`q`, --`query`
:   Open an interactive connection to the connect stream if a service is
    already running; fail otherwise.

-`r`, --`raw`
:   Raw mode `--interactive` connection.

-`s`, --`iservice`
:   List details for each active connect stream service on the
    standard output. The output format is similar to an
    [`ls`](/web/20151102030753/http://www2.research.att.com:80/~astopen/man/man1/ls.html)(1)
    `--long` listing, except the size field is the `tcp` or `udp`
    port number, and the service base name appears as a symbolic link to
    the network `/proc` path for the service process.

-`t`, --`translate`
:   `host` name operands are translated to IP address dot notation and
    listed on the standard output. If `host` is omitted then the
    standard input is read for host names, one per line.

-`C`, --`call`=`call-list`
:   Used with `--cat` to list only messages for the calls in
    `call-list`.

-`O`, --`open-flags`=`flags`
:   Set optional
    [`csopen`](/web/20151102030753/http://www2.research.att.com:80/~astopen/man/man3/csopen.html)(3) flags.
    Used by the
    [`cs`](/web/20151102030753/http://www2.research.att.com:80/~astopen/man/man3/cs.html)(3)
    library to initiate remote connections.

-`T`, --`terse`=`call-list`
:   Used with `--cat` to list terse messages for the calls in
    `call-list`

# DATA

Static information for hosts in the local network is in the file
`../share/lib/cs/local` on `\$PATH`. Each line in the `local` file
provides information for a single host. The syntax is: `host-name` \[ `attribute`=`value` ... \]. Attributes for the host `local` are
inherited by all hosts. Locally administered attributes may be added.
`attribute` with predefined semantics are:

`addr`
: The host IP address in dot notation.

`bias`
: The
    [`coshell`](/web/20151102030753/http://www2.research.att.com:80/~astopen/man/man1/coshell.html)(1)
    multiplies the host load by `bias` to prioritize
    host availability. `bias` &gt; 1 makes the host less likely to
    be chosen.

`busy`
: [`coshell`](/web/20151102030753/http://www2.research.att.com:80/~astopen/man/man1/coshell.html)(1)
    jobs running on a host that has remained busy for this amount of
    time are suspended until the host returns to idle status.

`cpu`
: The number of cpus on the host as reported by
    [`package`](/web/20151102030753/http://www2.research.att.com:80/~astopen/man/man1/package.html)(1).

`idle`
: The minimum interactive user idle time before
    [`coshell`](/web/20151102030753/http://www2.research.att.com:80/~astopen/man/man1/coshell.html)(1)
    will schedule a job on the host.

`pool`
: The
    [`coshell`](/web/20151102030753/http://www2.research.att.com:80/~astopen/man/man1/coshell.html)(1)
    attempts to keep `pool` host connections active.

`rating`
:   The host rating as reported by
    [`package`](/web/20151102030753/http://www2.research.att.com:80/~astopen/man/man1/package.html)(1).

`type`
: The host type as reported by
    [`package`](/web/20151102030753/http://www2.research.att.com:80/~astopen/man/man1/package.html)(1).

# FILES

`../share/lib/cs/local`
:   Local host info list on `\$PATH`.

`../share/lib/ss/``host`
:   Host status files on `\$PATH`.

# SEE ALSO

[`coshell`](/web/20151102030753/http://www2.research.att.com:80/~astopen/man/man1/coshell.html)(1),
[`css`](/web/20151102030753/http://www2.research.att.com:80/~astopen/man/man1/css.html)(1),
[`package`](/web/20151102030753/http://www2.research.att.com:80/~astopen/man/man1/package.html)(1),
[`ss`](/web/20151102030753/http://www2.research.att.com:80/~astopen/man/man1/ss.html)(1),
[`cs`](/web/20151102030753/http://www2.research.att.com:80/~astopen/man/man3/cs.html)(3)

# IMPLEMENTATION

`version`
:   cs (AT&T Research) 2006-06-11

`author`
:   Glenn Fowler

`copyright`
:   Copyright © 1990-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20151102030753/http://www.eclipse.org/org/documents/epl-v10.html)


