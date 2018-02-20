# NAME

jobs - display status of jobs

# SYNOPSIS

`jobs` \[ `options` \] \[job ...\]

# DESCRIPTION

`jobs` displays information about specified `job`s that were started
by the current shell environment on standard output. The information
contains the job number enclosed in \[...\], the status, and the command
line that started the job.

If `job` is omitted, `jobs` displays the status of all stopped jobs,
background jobs, and all jobs whose status has changed since last
reported by the shell.

When `jobs` reports the termination status of a job, the shell removes
the jobs from the list of known jobs in the current shell environment.

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

# OPTIONS

-`l`
: `jobs` displays process id's after the job number in addition to
    the usual information

-`n`
: Only the jobs whose status has changed since the last prompt
    is displayed.

-`p`
: The process group leader id's for the specified jobs are displayed.

# EXIT STATUS

`0`
: The information for each job is written to standard output.

`&gt;0`
: One or more jobs does not exist.

# SEE ALSO

[`wait`](/web/20141128030244/http://www2.research.att.com/~astopen/man/man1/wait.html)(1),
[`ps`](/web/20141128030244/http://www2.research.att.com/~astopen/man/man1/ps.html)(1),
[`fg`](/web/20141128030244/http://www2.research.att.com/~astopen/man/man1/fg.html)(1),
[`bg`](/web/20141128030244/http://www2.research.att.com/~astopen/man/man1/bg.html)(1)

# IMPLEMENTATION

`version`
: jobs (AT&T Research) 2000-04-02

`author`
: David Korn

`copyright`
: Copyright © 1982-2010 AT&T Intellectual Property

`license`
: [http://www.opensource.org/licenses/cpl1.0.txt](https://web.archive.org/web/20141128030244/http://www.opensource.org/licenses/cpl1.0.txt)


