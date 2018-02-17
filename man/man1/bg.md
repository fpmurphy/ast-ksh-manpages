# NAME

bg - resume jobs in the background

# SYNOPSIS

`bg` \[ `options` \] \[job ...\]

# DESCRIPTION

`bg` places the given `job`s into the background and sends them a
`CONT` signal to start them running.

If `job` is omitted, the most recently started or stopped background job
is resumed or continued in the background.

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

`0`
: If all background jobs are started.

`&gt;0`
: If one more jobs does not exist or there are no background jobs.

# SEE ALSO

[`wait`](/web/20141128030239/http://www2.research.att.com/~astopen/man/man1/wait.html)(1),
[`fg`](/web/20141128030239/http://www2.research.att.com/~astopen/man/man1/fg.html)(1),
[`disown`](/web/20141128030239/http://www2.research.att.com/~astopen/man/man1/disown.html)(1),
[`jobs`](/web/20141128030239/http://www2.research.att.com/~astopen/man/man1/jobs.html)(1)

# IMPLEMENTATION

`version`
: bg (AT&T Research) 2000-04-02

`author`
: David Korn
    &lt;[dgkorn@gmail.com](https://web.archive.org/web/20141128030239/mailto:dgkorn@gmail.com)&gt;

`copyright`
: Copyright © 1982-2010 AT&T Intellectual Property

`license`
: [http://www.opensource.org/licenses/cpl1.0.txt](https://web.archive.org/web/20141128030239/http://www.opensource.org/licenses/cpl1.0.txt)


