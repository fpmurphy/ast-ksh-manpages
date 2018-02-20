# NAME

ulimit - set or display resource limits

# SYNOPSIS

`ulimit` \[ `options` \] \[limit\]

# DESCRIPTION

`ulimit` sets or displays resource limits. These limits apply to the
current process and to each child process created after the resource
limit has been set. If `limit` is specified, the resource limit is set,
otherwise, its current value is displayed on standard output.

Increasing the limit for a resource usually requires special privileges.
Some systems allow you to lower resource limits and later increase them.
These are called soft limits. Once a hard limit is set the resource can
not be increased.

Different systems allow you to specify different resources and some
restrict how much you can raise the limit of the resource.

The value of `limit` depends on the unit of the resource listed for each
resource. In addition, `limit` can be `unlimited` to indicate no limit
for that resource.

If you do not specify `-H` or `-S`, then `-S` is used for listing
and both `-S` and `-H` are used for setting resources.

If you do not specify any resource, the default is `-f`.

# OPTIONS

-`H`
: A hard limit is set or displayed.

-`S`
: A soft limit is set or displayed.

-`a`
: Displays all current resource limits

-`M`, --`as`
: The address space limit in kbytes.

-`c`, --`core`
: The core file size in blocks.

-`t`, --`cpu`
: The cpu time in seconds.

-`d`, --`data`
: The data size in kbytes.

-`f`, --`fsize`
: The file size in blocks.

-`L`, --`locks`
: The number of file locks.

-`l`, --`memlock`
: The locked address space in kbytes.

-`n`, --`nofile`
: The number of open files.

-`u`, --`nproc`
: The number of processes.

-`p`, --`pipe`
: The pipe buffer size in bytes.

-`m`, --`rss`
: The resident set size in kbytes.

-`b`, --`sbsize`
: The socket buffer size in bytes.

-`s`, --`stack`
: The stack size in kbytes.

-`T`, --`threads`
: The number of threads.

-`v`, --`vmem`
: The process size in kbytes.

# EXIT STATUS

`0`
: Successful completion.

`&gt;0`
: A request for a higher limit was rejected or an error occurred.

# SEE ALSO

[`ulimit`](/web/20141128030252/http://www2.research.att.com/~astopen/man/man2/ulimit.html)(2),
[`getrlimit`](/web/20141128030252/http://www2.research.att.com/~astopen/man/man2/getrlimit.html)(2)

# IMPLEMENTATION

`version`
: ulimit (AT&T Research) 2003-06-21

`author`
: David Korn

`copyright`
: Copyright © 1982-2010 AT&T Intellectual Property

`license`
: [http://www.opensource.org/licenses/cpl1.0.txt](https://web.archive.org/web/20141128030252/http://www.opensource.org/licenses/cpl1.0.txt)


