# NAME

wait - wait for process or job completion

# SYNOPSIS

`wait` \[ `options` \] \[job ...\]

# DESCRIPTION

`wait` with no operands, waits until all jobs known to the invoking
shell have terminated. If one or more `job` operands are specified,
`wait` waits until all of them have completed.

Each `job` can be specified as one of the following:

`number`
: `number` refers to a process id.

`-``number`
: `number` refers to a process group id.

`%``number`
: `number` refer to a job number.

`%``string`
: Refers to a job whose name begins with `string`.

`%?``string`
: Refers to a job whose name contains `string`.

`%+` or `%%`
: Refers to the current job.

`%-`
: Refers to the previous job.

If one ore more `job` operands is a process id or process group id not
known by the current shell environment, `wait` treats each of them as
if it were a process that exited with status 127.

# EXIT STATUS

If `wait` is invoked with one or more `job`s, and all of them have
terminated or were not known by the invoking shell, the exit status of
`wait` will be that of the last `job`. Otherwise, it will be one of
the following:

`0`
: `wait` utility was invoked with no operands and all processes
    known by the invoking process have terminated.

`127`
: `job` is a process id or process group id that is unknown to the
    current shell environment.

# SEE ALSO

[`jobs`](/web/20141128030253/http://www2.research.att.com/~astopen/man/man1/jobs.html)(1),
[`ps`](/web/20141128030253/http://www2.research.att.com/~astopen/man/man1/ps.html)(1)

# IMPLEMENTATION

`version`
: wait (AT&T Research) 1999-06-17

`author`
: David Korn

`copyright`
: Copyright © 1982-2010 AT&T Intellectual Property

`license`
: [http://www.opensource.org/licenses/cpl1.0.txt](https://web.archive.org/web/20141128030253/http://www.opensource.org/licenses/cpl1.0.txt)


