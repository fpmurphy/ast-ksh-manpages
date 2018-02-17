# NAME

xargs - construct arg list and execute command

# SYNOPSIS

`xargs` \[ `options` \] \[ command \[ argument ... \] \]

# DESCRIPTION

`xargs` constructs a command line consisting of the `command` and
`argument` operands specified followed by as many arguments read in
sequence from standard input as will fit in length and number
constraints specified by the options and the local system. `xargs`
executes the constructed command and waits for its completion. This
sequence is repeated until an end-of-file condition is detected on
standard input or an invocation of a constructed command line returns an
exit status of 255. If `command` is omitted then the equivalent of
`/bin/echo` is used.
Arguments in the standard input must be separated by unquoted blank
characters, or unescaped blank characters or newline characters. A
string of zero or more non-double-quote and non-newline characters can
be quoted by enclosing them in double-quotes. A string of zero or more
non-apostrophe and non-newline characters can be quoted by enclosing
them in apostrophes. Any unquoted character can be escaped by preceding
it with a backslash. The utility will be executed one or more times
until the end-of-file is reached. The results are unspecified if
`command` attempts to read from its standard input.

# OPTIONS

-`e`, --`eof`\[=`string`\]
:   Set the end of file string. The first input line matching this
    string terminates the input list. There is no eof string if `string`
    is omitted. The default eof string is `\_` if neither `--eof`
    nor `-E` are specified. For backwards compatibility `string` must
    immediately follow the `-e` option flag; `-E` follows standard
    option syntax. The option value may be omitted.

-`i`, --`insert|replace`\[=`string`\]
:   Replace occurences of `string` in the command arguments with names
    read from the standard input. Implies `--exit` and `--lines=1`.
    For backwards compatibility `string` must immediately follow the
    `-i` option flag; `-I` follows standard option syntax. The
    option value may be omitted. The default value is `{}`.

-`l`, --`lines|max-lines`\[=`lines`\]
:   Use at most `lines` lines from the standard input. Lines with
    trailing blanks logically continue onto the next line. For backwards
    compatibility `lines` must immediately follow the `-l` option
    flag; `-L` follows standard option syntax. The option value may
    be omitted. The default value is `1`.

-`n`, --`args|max-args`=`args`
:   Use at most `args` arguments per command line. Fewer than `args`
    will be used if `--size` is exceeded.

-`p`, --`interactive|prompt`
:   Prompt to determine if each command should execute. A `y` or `Y`
    recsponse executes, otherwise the command is skipped. Implies
    `--verbose`.

-`N|0`, --`null`
:   The file name list is NUL terminated; there is no other special
    treatment of the list.

-`s`, --`size|max-chars`=`chars`
:   Use at most `chars` characters per command. The default is as large
    as possible.

-`t`, --`trace|verbose`
:   Print the command line on the standard error before executing it.

-`x`, --`exit`
:   Exit if `--size` is exceeded.

-`X`, --`exact`
:   If `--args=``args` was specified then terminate before the last
    command if it would run with less than `args` arguments.

-`z`, --`nonempty|no-run-if-empty`
:   If no file names are found then do not execute the command. By
    default the command is executed at least once.

-`E` `string`
:   Equivalent to `--eof=string`.

-`I` `string`
:   Equivalent to `--insert=string`.

-`L` `number`
:   Equivalent to `--lines=number`.

# EXIT STATUS

`0`
: All invocations of `command` returned exit status 0.

`1-125`
:   A command line meeting the specified requirements could not be
    assembled, one or more of the invocations of `command` returned
    non-0 exit status, or some other error occurred.

`126`
: `command` was found but could not be executed.

`127`
: `command` was not found.

# SEE ALSO

[`find`](/web/20141128030254/http://www2.research.att.com/~astopen/man/man1/find.html)(1),
[`tw`](/web/20141128030254/http://www2.research.att.com/~astopen/man/man1/tw.html)(1)

# IMPLEMENTATION

`version`
:   xargs (AT&T Research) 2012-04-11

`author`
:   Glenn Fowler
    &lt;[glenn.s.fowler@gmail.com](https://web.archive.org/web/20141128030254/mailto:glenn.s.fowler@gmail.com)&gt;

`copyright`
:   Copyright © 1989-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030254/http://www.eclipse.org/org/documents/epl-v10.html)


