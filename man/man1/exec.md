# NAME

exec - execute command, open/close and duplicate file descriptors

# SYNOPSIS

`exec` \[ `options` \] \[command \[arg ...\]\]

# DESCRIPTION

`exec` is a special built-in command that can be used to manipulate
file descriptors or to replace the current shell with a new command.

If `command` is specified, then the current shell process will be
replaced by `command` rather than running `command` and waiting for it
to complete. Note that there is no need to use `exec` to enhance
performance since the shell implicitly uses the exec mechanism
internally whenever possible.

If no operands are specified, `exec` can be used to open or close
files, or to manipulate file descriptors from `0` to `9` in the
current shell environment using the standard redirection mechanism
available with all commands. The close-on-exec flags will be set on file
descriptor numbers greater than `2` that are opened this way so that
they will be closed when another program is invoked.

Because `exec` is a special command, any failure will cause the script
that invokes it to exit. This can be prevented by invoking `exec` from
the `command` utility.

`exec` cannot be invoked from a restricted shell to create files or to
open a file for writing or appending.

# OPTIONS

-`c`
: Clear all environment variables before executions except variable
    assignments that are part of the current `exec` command.

-`a` `name`
: `argv\[0\]` will be set to `name` for `command`

# EXIT STATUS

If `command` is specified, `exec` does not return. Otherwise, the exit
status is one of the following:

`0`
: All I/O redirections were successful.

`&gt;0`
: An error occurred.

# SEE ALSO

[`command`](/web/20141128030243/http://www2.research.att.com/~astopen/man/man1/command.html)(1),
[`eval`](/web/20141128030243/http://www2.research.att.com/~astopen/man/man1/eval.html)(1)

# IMPLEMENTATION

`version`
: exec (AT&T Research) 1999-07-10

`author`
: David Korn
    &lt;[dgkorn@gmail.com](https://web.archive.org/web/20141128030243/mailto:dgkorn@gmail.com)&gt;

`copyright`
: Copyright © 1982-2010 AT&T Intellectual Property

`license`
: [http://www.opensource.org/licenses/cpl1.0.txt](https://web.archive.org/web/20141128030243/http://www.opensource.org/licenses/cpl1.0.txt)


