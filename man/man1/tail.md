# NAME

tail - output trailing portion of one or more files

# SYNOPSIS

`tail` \[ `options` \] \[file ...\]

# DESCRIPTION

`tail` copies one or more input files to standard output starting at a
designated point for each file. Copying starts at the point indicated by
the options and is unlimited in size.
By default a header of the form `==&gt;` `filename` `&lt;==` is
output before all but the first file but this can be changed with the
`-q` and `-v` options.

If no `file` is given, or if the `file` is `-`, `tail` copies from
standard input. The start of the file is defined as the current offset.

The option argument for `-c` can optionally be followed by one of the
following characters to specify a different unit other than a single
byte:

`b`
: 512 bytes.

`k`
: 1 KiB.

`m`
: 1 MiB.

`g`
: 1 GiB.

For backwards compatibility, `-``number` is equivalent to `-n`
`number` and `+``number` is equivalent to `-n -``number`. `number`
may also have these option suffixes: `b c f g k l m r`.

# OPTIONS

-`n`, --`lines`=`lines`
:   Copy `lines` lines from each file. A negative value for `lines`
    indicates an offset from the end of the file. The default value is
    `10`.

-`b`, --`blocks`
:   Copy units of 512 bytes.

-`c`, --`bytes`\[=`chars`\]
:   Copy `chars` bytes from each file. A negative value for `chars`
    indicates an offset from the end of the file. The option value may
    be omitted.

-`f`, --`forever|follow`
:   Loop forever trying to read more characters as the end of each file
    to copy new data. Ignored if reading from a pipe or fifo.

-`h`, --`headers`
:   Output filename headers. On by default; -`h` means
    --`noheaders`.

-`l`, --`lines`
:   Copy units of lines. This is the default.

-`L`, --`log`
:   When a `--forever` file times out via `--timeout`, verify that
    the curent file has not been renamed and replaced by another file of
    the same name (a common log file practice) before giving up on
    the file.

-`q`, --`quiet`
:   Don't output filename headers. For GNU compatibility.

-`r`, --`reverse`
:   Output lines in reverse order.

-`s`, --`silent`
:   Don't warn about timeout expiration and log file changes.

-`t`, --`timeout`=`timeout`
:   Stop checking after `timeout` elapses with no additional
    `--forever` output. A separate elapsed time is maintained for each
    file operand. There is no timeout by default. The default `timeout`
    unit is seconds. `timeout` may be a catenation of 1 or more
    integers, each followed by a 1 character suffix. The suffix may be
    omitted from the last integer, in which case it is interpreted
    as seconds. The supported suffixes are:

    [`s`]()
    : seconds

    [`m`]()
    : minutes

    [`h`]()
    : hours

    [`d`]()
    : days

    [`w`]()
    : weeks

    [`M`]()
    : months

    [`y`]()
    : years

    [`S`]()
    : scores

-`v`, --`verbose`
:   Always ouput filename headers.

# EXIT STATUS

`0`
: All files copied successfully.

`&gt;0`
:   One or more files did not copy.

# SEE ALSO

[`cat`](/web/20141128030251/http://www2.research.att.com/~astopen/man/man1/cat.html)(1),
[`head`](/web/20141128030251/http://www2.research.att.com/~astopen/man/man1/head.html)(1),
[`rev`](/web/20141128030251/http://www2.research.att.com/~astopen/man/man1/rev.html)(1)

# IMPLEMENTATION

`version`
:   tail (AT&T Research) 2012-06-19

`author`
:   Glenn Fowler

`author`
:   David Korn

`copyright`
:   Copyright © 1992-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030251/http://www.eclipse.org/org/documents/epl-v10.html)


