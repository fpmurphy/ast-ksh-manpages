# NAME

sed - stream editor

# SYNOPSIS

`sed` \[ `options` \] \[ file ... \]

# DESCRIPTION

`sed` is a stream editor that reads one or more text files, makes
editing changes according to a script of editing commands, and writes
the results to standard output. The script is obtained from either the
script operand string or a combination of the option-arguments from the
`--expression` and `--file` options.

# OPTIONS

-`b`, --`strip-blanks`
:   Strip leading blanks from `a`, `c`, and `i` text.

-`e`, --`expression`=`script`
:   Append the editing commands in `script` to the end of the the
    editing command script. `script` may contain more than one newline
    separated command.

-`f`, --`file`=`script-file`
:   Append the editing commands in `script-file` to the end of the the
    editing command script.

-`n`, --`quiet|silent`
:   Suppress the default output in which each line, after it is examined
    for editing, is written to standard output. Only lines explicitly
    selected for output will be written.

-`A|X`, --`augmented`
:   Enable augmented regular expressions; this includes negation
    and conjunction.

-`E|r`, --`extended|regexp-extended`
:   Enable extended regular expressions, i.e.,
    [`egrep`](/web/20150817032522/http://www2.research.att.com:80/~astopen/man/man1/egrep.html)(1) style.

-`O`, --`lenient`
:   Enable lenient regular expression interpretation. This is the
    default if `getconf CONFORMANCE` is not `standard`.

-`S`, --`strict|posix`
:   Enable strict regular expression interpretation. This is the default
    if `getconf CONFORMANCE` is `standard`. You'd be suprised what
    the lenient mode lets by.

-`m`
: multi-digit-reference?Enable `\\dd` multi-digit backreferences.

-`d`
: Ignored by this implementation.

-`u`, --`unbuffered`
:   Unbuffered output.

# SEE ALSO

[`awk`](/web/20150817032522/http://www2.research.att.com:80/~astopen/man/man1/awk.html)(1),
[`ed`](/web/20150817032522/http://www2.research.att.com:80/~astopen/man/man1/ed.html)(1),
[`grep`](/web/20150817032522/http://www2.research.att.com:80/~astopen/man/man1/grep.html)(1),
[`regex`](/web/20150817032522/http://www2.research.att.com:80/~astopen/man/man3/regex.html)(3)

# IMPLEMENTATION

`version`
:   sed (AT&T Research) 2012-03-28

`author`
:   Glenn Fowler
    &lt;[glenn.s.fowler@gmail.com](https://web.archive.org/web/20150817032522/mailto:glenn.s.fowler@gmail.com)&gt;

`author`
:   Doug McIlroy
    &lt;[doug@research.bell-labs.com](https://web.archive.org/web/20150817032522/mailto:doug@research.bell-labs.com)&gt;

`copyright`
:   Copyright © 1995-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20150817032522/http://www.eclipse.org/org/documents/epl-v10.html)


