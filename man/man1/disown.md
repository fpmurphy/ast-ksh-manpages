# NAME

disown - disassociate a job with the current shell

# SYNOPSIS

`disown` \[ `options` \] \[job ...\]

# DESCRIPTION

`disown` prevents the current shell from sending a `HUP` signal to
each of the given `job`s when the current shell terminates a login
session.

If `job` is omitted, the most recently started or stopped background job
is used.

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
: If all jobs are successfully disowned.

`&gt;0`
: If one more `job`s does not exist.

# SEE ALSO

[`wait`](/web/20141128030242/http://www2.research.att.com/~astopen/man/man1/wait.html)(1),
[`bg`](/web/20141128030242/http://www2.research.att.com/~astopen/man/man1/bg.html)(1),
[`jobs`](/web/20141128030242/http://www2.research.att.com/~astopen/man/man1/jobs.html)(1)

# IMPLEMENTATION

`version`
: disown (AT&T Research) 2000-04-02

`author`
: David Korn
    &lt;[dgkorn@gmail.com](https://web.archive.org/web/20141128030242/mailto:dgkorn@gmail.com)&gt;

`copyright`
: Copyright © 1982-2010 AT&T Intellectual Property

`license`
: [http://www.opensource.org/licenses/cpl1.0.txt](https://web.archive.org/web/20141128030242/http://www.opensource.org/licenses/cpl1.0.txt)


