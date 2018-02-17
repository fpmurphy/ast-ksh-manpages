# NAME

ed - edit text

# SYNOPSIS

`ed` \[ `options` \] \[ file \]

# DESCRIPTION

`ed` is a line-oriented text editor that has two modes: command mode
and input mode. In command mode characters on the standard input are
interpreted as commands, and in input mode they are interpreted as text.

# OPTIONS

-`h`, --`explain`
:   Explain the details of error conditions rather than the default
    \`\``?`'' on the standard error.

-`o`, --`output`
:   Write output to the standard output and error messages to the
    standard error. By default output is written to the file being
    edited and error messages are printed on the standard output.

-`p`, --`prompt`=`string`
:   Sets the command line prompt to `string`. The default is no prompt.

-`q`, --`test`
:   For testing; enable verbose messages and reset the `QUIT` signal
    handler to the default action.

-`s`, --`silent`
:   Disable verbose messages.

-`O`, --`lenient`
:   Enable lenient regular expression interpretation. This is the
    default if `getconf CONFORMANCE` is not `standard`.

-`S`, --`strict`
:   Enable strict regular expression interpretation. This is the default
    if `getconf CONFORMANCE` is `standard`. You'd be suprised what
    the lenient mode lets by.

# SEE ALSO

[`sed`](/web/20141128030249/http://www2.research.att.com/~astopen/man/man1/sed.html)(1),
[`regex`](/web/20141128030249/http://www2.research.att.com/~astopen/man/man3/regex.html)(3)

# IMPLEMENTATION

`version`
:   ed (AT&T Research) 2004-06-08

`author`
:   Glenn Fowler
    &lt;[glenn.s.fowler@gmail.com](https://web.archive.org/web/20141128030249/mailto:glenn.s.fowler@gmail.com)&gt;

`copyright`
:   Copyright © 1995-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030249/http://www.eclipse.org/org/documents/epl-v10.html)


