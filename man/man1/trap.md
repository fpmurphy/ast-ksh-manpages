# NAME

trap - trap signals and conditions

# SYNOPSIS

`trap` \[ `options` \] \[action condition ...\]

# DESCRIPTION

`trap` is a special built-in that defines actions to be taken when
conditions such as receiving a signal occur. Also, `trap` can be used
to display the current trap settings on standard output.

If `action` is `-`, `trap` resets each `condition` to the default
value. If `action` is an empty string, the shell ignores each of the
`condition`s if they arise. Otherwise, the argument `action` will be
read and executed by the shell as if it were processed by
[`eval`](/web/20141128030252/http://www2.research.att.com/~astopen/man/man1/eval.html)(1)
when one of the corresponding conditions arise. The action of the trap
will override any previous action associated with each specified
`condition`. The value of `\$?` is not altered by the trap execution.

`condition` can be the name or number of a signal, or one of the
following:

`EXIT`
: This trap is executed when the shell exits. If defined within a
    function defined with the `function` reserved word, the trap is
    executed in the caller's environment when the function returns and
    the trap action is restored to the value it had when it called
    the function.

`0`
: Same as EXIT.

`DEBUG`
: Executed before each simple command is executed but after the
    arguments are expanded.

`ERR`
: Executed whenever `set -e` would cause the shell to exit.

`KEYBD`
: Executed when a key is entered from a terminal device.

Signal names are case insensitive and the `sig` prefix is optional.
Signals that were ignored on entry to a noninteractive shell cannot
trapped or reset although doing so will not report an error. The use of
signal numbers other than `1`, `2`, `3`, `6`, `9`, `14`, and
`15` is not portable.

Although `trap` is a special built-in, specifying a condition that the
shell does not know about causes `trap` to exit with a non-zero exit
status, but does not terminate the invoking shell.

If no `action` or `condition`s are specified then all the current trap
settings are written to standard output.

# OPTIONS

-`p`
: Causes the current traps to be output in a format that can be
    processed as input to the shell to recreate the current traps.

# EXIT STATUS

`0`
: Successful completion.

`&gt;0`
: An error occurred.

# SEE ALSO

[`kill`](/web/20141128030252/http://www2.research.att.com/~astopen/man/man1/kill.html)(1),
[`eval`](/web/20141128030252/http://www2.research.att.com/~astopen/man/man1/eval.html)(1),
[`signal`](/web/20141128030252/http://www2.research.att.com/~astopen/man/man3/signal.html)(3)

# IMPLEMENTATION

`version`
: trap (AT&T Research) 1999-07-17

`author`
: David Korn

`copyright`
: Copyright © 1982-2010 AT&T Intellectual Property

`license`
: [http://www.opensource.org/licenses/cpl1.0.txt](https://web.archive.org/web/20141128030252/http://www.opensource.org/licenses/cpl1.0.txt)


