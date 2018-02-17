# NAME

fg - move jobs to the foreground

# SYNOPSIS

`fg` \[ `options` \] \[job ...\]

# DESCRIPTION

`fg` places the given `job`s into the foreground in sequence and sends
them a `CONT` signal to start each running.

If `job` is omitted, the most recently started or stopped background job
is moved to the foreground.

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

# EXIT STATUS

If `fg` brings one or more jobs into the foreground, the exit status
of `fg` will be that of the last `job`. If one or more jobs does not
exist or has completed, `fg` will return a non-zero exit status.

# SEE ALSO

[`wait`](/web/20141128030243/http://www2.research.att.com/~astopen/man/man1/wait.html)(1),
[`bg`](/web/20141128030243/http://www2.research.att.com/~astopen/man/man1/bg.html)(1),
[`jobs`](/web/20141128030243/http://www2.research.att.com/~astopen/man/man1/jobs.html)(1)

# IMPLEMENTATION

`version`
: fg (AT&T Research) 2000-04-02

`author`
: David Korn
    &lt;[dgkorn@gmail.com](https://web.archive.org/web/20141128030243/mailto:dgkorn@gmail.com)&gt;

`copyright`
: Copyright © 1982-2010 AT&T Intellectual Property

`license`
: [http://www.opensource.org/licenses/cpl1.0.txt](https://web.archive.org/web/20141128030243/http://www.opensource.org/licenses/cpl1.0.txt)


