# NAME

cmp - compare two files

# SYNOPSIS

`cmp` \[ `options` \] file1 file2 \[skip1 \[skip2\]\]

# DESCRIPTION

`cmp` compares two files `file1` and `file2`. `cmp` writes no output
if the files are the same. By default, if the files differ, the byte and
line number at which the first difference occurred are written to
standard output. Bytes and lines are numbered beginning with 1.
If `skip1` or `skip2` are specified, or the `-i` option is specified,
initial bytes of the corresponding file are skipped before beginning the
compare. The skip values are in bytes or can have a suffix of `k` for
kilobytes or `m` for megabytes.

If either `file1` or `files2` is `-`, `cmp` uses standard input
starting at the current location.

# OPTIONS

-`b`, --`print-bytes`
:   Print differing bytes as 3 digit octal values.

-`c`, --`print-chars`
:   Print differing bytes as follows: non-space printable characters as
    themselves; space and control characters as `\^` followed by a
    letter of the alphabet; and characters with the high bit set as the
    lower 7 bit character prefixed by `M\^` for 7 bit space and
    non-printable characters and `M-` for all other characters. If the
    7 bit character encoding is not ASCII then the characters are
    converted to ASCII to determine `high bit set`, and if set it is
    cleared and converted back to the native encoding. Multibyte
    characters in the current locale are treated as
    printable characters.

-`d`, --`differences`=`differences`
:   Print at most `differences` differences using `--verbose`
    output format. `--differences=0` is equivalent to `--silent`.

-`i`, --`ignore-initial|skip`=`skip1\[:skip2\]`
:   Skip the the first `skip1` bytes in `file1` and the first `skip2`
    bytes in `file2`. If `skip2` is omitted then `skip1` is used. The
    default value is `0:0`.

-`l`, --`verbose`
:   Write the decimal byte number and the differing bytes (in octal) for
    each difference.

-`n`, --`count|bytes`=`count`
:   Compare at most `count` bytes.

-`s`, --`quiet|silent`
:   Write nothing for differing files; return non-zero exit status only.

# EXIT STATUS

`0`
: The files or portions compared are identical.

`1`
: The files are different.

`&gt;1`
:   An error occurred.

# SEE ALSO

[`comm`](/web/20141128030240/http://www2.research.att.com/~astopen/man/man1/comm.html)(1),
[`diff`](/web/20141128030240/http://www2.research.att.com/~astopen/man/man1/diff.html)(1),
[`cat`](/web/20141128030240/http://www2.research.att.com/~astopen/man/man1/cat.html)(1)

# IMPLEMENTATION

`version`
:   cmp (AT&T Research) 2010-04-11

`author`
:   Glenn Fowler

`author`
:   David Korn

`copyright`
:   Copyright © 1992-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030240/http://www.eclipse.org/org/documents/epl-v10.html)


