# NAME

eval - create a shell command and process it

# SYNOPSIS

`eval` \[ `options` \] \[arg...\]

# DESCRIPTION

`eval` is a shell special built-in command that constructs a command
by concatenating the `arg`s together, separating each with a space. The
resulting string is then taken as input to the shell and evaluated in
the current environment. Note that command words are expanded twice;
once to construct `arg`, and again when the shell executes the
constructed command.

It is not an error if `arg` is not given.

# EXIT STATUS

If `arg` is not specified, the exit status is `0`. Otherwise, it is
the exit status of the command defined by the `arg` operands.

# SEE ALSO

[`exec`](/web/20141128030243/http://www2.research.att.com/~astopen/man/man1/exec.html)(1),
[`trap`](/web/20141128030243/http://www2.research.att.com/~astopen/man/man1/trap.html)(1),
[`.`](/web/20141128030243/http://www2.research.att.com/~astopen/man/man1/..html)(1)

# IMPLEMENTATION

`version`
: eval (AT&T Research) 1999-07-07

`author`
: David Korn
    &lt;[dgkorn@gmail.com](https://web.archive.org/web/20141128030243/mailto:dgkorn@gmail.com)&gt;

`copyright`
: Copyright © 1982-2010 AT&T Intellectual Property

`license`
: [http://www.opensource.org/licenses/cpl1.0.txt](https://web.archive.org/web/20141128030243/http://www.opensource.org/licenses/cpl1.0.txt)


