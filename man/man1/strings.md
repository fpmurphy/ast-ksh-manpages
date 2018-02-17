# NAME

strings - find and display printable strings in files

# SYNOPSIS

`strings` \[ `options` \] \[ file ... \]

# DESCRIPTION

`strings` searches for printable strings in regular files and writes
those strings to the standard output. A printable string is any sequence
of four (by default) or more printable characters terminated by a
newline or NUL character.

# OPTIONS

-`a`, --`all`
:   Scan the entire file. Always enabled in this implementation.

-`l`, --`long-strings`
:   Ignore `newline` characters as string terminators and display
    strings using C character escape sequences. These strings are
    suitably escaped for placement inside C "..." and
    [`ksh`](/web/20141128030251/http://www2.research.att.com/~astopen/man/man1/ksh.html)(1)
    \$'...' string literals.

-`m`, --`multi-byte`
:   Scan for multibyte strings.

-`n`, --`length|bytes`=`number`
:   Set the minimum matched string length to `length`. For compatibility
    -`number` is equivalent to `--length`=`number`. The default value
    is `4`.

-`t`, --`radix|format`=`format`
:   Write each string preceded by its byte offset from the start of
    the file. The offset radix is determined by:

    [`d`]()
    : decimal

    [`o`]()
    : octal

    [`x`]()
    : hexadecimal

-`o`, --`octal`
:   Equivalent to `--radix=o`.

# SEE ALSO

[`grep`](/web/20141128030251/http://www2.research.att.com/~astopen/man/man1/grep.html)(1),
[`nm`](/web/20141128030251/http://www2.research.att.com/~astopen/man/man1/nm.html)(1),
[`what`](/web/20141128030251/http://www2.research.att.com/~astopen/man/man1/what.html)(1)

# IMPLEMENTATION

`version`
:   strings (AT&T Research) 2000-04-01

`author`
:   Glenn Fowler
    &lt;[glenn.s.fowler@gmail.com](https://web.archive.org/web/20141128030251/mailto:glenn.s.fowler@gmail.com)&gt;

`author`
:   David Korn
    &lt;[dgkorn@gmail.com](https://web.archive.org/web/20141128030251/mailto:dgkorn@gmail.com)&gt;

`copyright`
:   Copyright © 1992-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030251/http://www.eclipse.org/org/documents/epl-v10.html)


