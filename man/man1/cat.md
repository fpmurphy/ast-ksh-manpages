# NAME

cat - concatenate files

# SYNOPSIS

`cat` \[ `options` \] \[file ...\]

# DESCRIPTION

`cat` copies each `file` in sequence to the standard output. If no
`file` is given, or if the `file` is `-`, `cat` copies from standard
input starting at the current location.

# OPTIONS

-`b`, --`number-nonblank`
:   Number lines as with `-n` but omit line numbers from blank lines.

-`d`, --`dos-input`
:   Input files are opened in `text`mode which removes carriage returns
    in front of new-lines on some systems.

-`e`
: Equivalent to `-vE`.

-`n`, --`number`
:   Causes a line number to be inserted at the beginning of each line.

-`s`
: Equivalent to `-S` for `att` universe and `-B` otherwise.

-`t`
: Equivalent to `-vT`.

-`u`, --`unbuffer`
:   The output is not delayed by buffering.

-`v`, --`show-nonprinting|print-chars`
:   Print characters as follows: space and printable characters as
    themselves; control characters as `\^` followed by a letter of the
    alphabet; and characters with the high bit set as the lower 7 bit
    character prefixed by `M\^` for 7 bit non-printable characters and
    `M-` for all other characters. If the 7 bit character encoding is
    not ASCII then the characters are converted to ASCII to determine
    `high bit set`, and if set it is cleared and converted back to the
    native encoding. Multibyte characters in the current locale are
    treated as printable characters.

-`A`, --`show-all`
:   Equivalent to `-vET`.

-`B`, --`squeeze-blank`
:   Multiple adjacent new-line characters are replace by one new-line.

-`D`, --`dos-output`
:   Output files are opened in `text`mode which inserts carriage returns
    in front of new-lines on some systems.

-`E`, --`show-ends`
:   Causes a `\$` to be inserted before each new-line.

-`R`, --`regress`
:   Regression test defaults: `-v` buffer size 4.

-`S`, --`silent`
:   `cat` is silent about non-existent files.

-`T`, --`show-blank`
:   Causes tabs to be copied as `\^I` and formfeeds as `\^L`.

# SEE ALSO

[`cp`](/web/20150109080056/http://www2.research.att.com:80/~astopen/man/man1/cp.html)(1),
[`getconf`](/web/20150109080056/http://www2.research.att.com:80/~astopen/man/man1/getconf.html)(1),
[`pr`](/web/20150109080056/http://www2.research.att.com:80/~astopen/man/man1/pr.html)(1)

# IMPLEMENTATION

`version`
:   cat (AT&T Research) 2012-05-31

`author`
:   Glenn Fowler
    &lt;[glenn.s.fowler@gmail.com](https://web.archive.org/web/20150109080056/mailto:glenn.s.fowler@gmail.com)&gt;

`author`
:   David Korn
    &lt;[dgkorn@gmail.com](https://web.archive.org/web/20150109080056/mailto:dgkorn@gmail.com)&gt;

`copyright`
:   Copyright © 1992-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20150109080056/http://www.eclipse.org/org/documents/epl-v10.html)


