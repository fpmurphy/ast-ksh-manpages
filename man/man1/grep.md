# NAME

grep - search lines in files for matching patterns

# SYNOPSIS

`grep` \[ `options` \] \[ pattern \] \[ file ... \]

# DESCRIPTION

The `grep` commands search the named input files for lines containing
a match for the given `patterns`. Matching lines are printed by default.
The standard input is searched if no files are given or when the file
`-` is specified.
There are six variants of `grep`, each one using a different form of
`pattern`, controlled either by option or the command path base name.
Details of each variant may be found in
[`regex`](/web/20150328001607/http://www2.research.att.com:80/~astopen/man/man3/regex.html)(3).

`grep`
: The default basic regular expressions (no alternations.)

`egrep`
:   Extended regular expressions (alternations, one or more.)

`pgrep`
:   [`perl`](/web/20150328001607/http://www2.research.att.com:80/~astopen/man/man1/perl.html)(1)
    regular expressions (lenient extended.)

`xgrep`
:   Augmented regular expressions (conjunction, negation.)

`fgrep`
:   Fixed string expressions.

`agrep`
:   Approximate regular expressions (not implemented.)

# OPTIONS

-`G`, --`basic-regexp`
:   `grep` mode (default): basic regular expression `patterns`.

-`E`, --`extended-regexp`
:   `egrep` mode: extended regular expression `patterns`.

-`X`, --`augmented-regexp`
:   `xgrep` mode: augmented regular expression `patterns`.

-`P`, --`perl-regexp`
:   `pgrep` mode:
    [`perl`](/web/20150328001607/http://www2.research.att.com:80/~astopen/man/man1/perl.html)(1)
    regular expression `patterns`.

-`F`, --`fixed-string`
:   `fgrep` mode: fixed string `patterns`.

-`A`, --`approximate-regexp`
:   `agrep` mode: approximate regular expression `patterns`
    (not implemented.)

-`C`, --`context`\[=`before\[,after\]`\]
:   Set the matched line context `before` and `after` count. If ,`after`
    is omitted then it is set to `before`. By default only matched lines
    are printed. The option value may be omitted. The default value is
    `2,2`.

-`c`, --`count`
:   Only print a matching line count for each file.

-`e`, --`expression|pattern|regexp`=`pattern`
:   Specify a matching `pattern`. More than one `pattern`
    implies alternation. If this option is specified then the command
    line `pattern` must be omitted.

-`f`, --`file`=`pattern-file`
:   Each line in `pattern-file` is a `pattern`, placed into a single
    alternating expression.

-`H`, --`filename|with-filename`
:   Prefix each matched line with the containing file name.

-`h`, --`no-filename`
:   Suppress containing file name prefix for each matched line.

-`i`, --`ignore-case`
:   Ignore case when matching.

-`l`, --`files-with-matches`
:   Only print file names with at least one match.

-`L`, --`files-without-matches`
:   Only print file names with no matches.

-`b`, --`highlight`
:   Highlight matches using the ansi terminal bold sequence.

-`v`, --`invert-match|revert-match`
:   Invert the `pattern` match sense.

-`m`, --`label`
:   All patterns must be of the form `label`:`pattern`. Match and count
    output will be prefixed by the corresponding `label`:.

-`O`, --`lenient`
:   Enable lenient `pattern` interpretation. This is the default.

-`x`, --`line-match|line-regexp`
:   Force `patterns` to match complete lines.

-`n`, --`number|line-number`
:   Prefix each matched line with its line number.

-`N`, --`name`=`name`
:   Set the standard input file name prefix to `name`. The default value
    is `empty` .

-`q`, --`quiet|silent`
:   Do not print matching lines.

-`r|R`, --`recursive`
:   Recursively process all files in each named directory. Use `tw -e`
    `expression` `grep ...` to control the directory traversal.

-`S`, --`strict`
:   Enable strict `pattern` interpretation with diagnostics.

-`s`, --`suppress|no-messages`
:   Suppress error and warning messages.

-`t`, --`total`
:   Only print a single matching line count for all files.

-`T`, --`test`=`test`
:   Enable implementation specific tests.

-`w`, --`word-match|word-regexp`
:   Force `patterns` to match complete words.

-`a`
: Ignored for GNU compatibility.

-`Y`, --`color|colour`=`when`
:   Ignored for GNU compatibility.

# DIAGNOSTICS

Exit status 0 if matches were found, 1 if no matches were found, where
`-v` invertes the exit status. Exit status 2 for other errors that are
accompanied by a message on the standard error.

# SEE ALSO

[`ed`](/web/20150328001607/http://www2.research.att.com:80/~astopen/man/man1/ed.html)(1),
[`sed`](/web/20150328001607/http://www2.research.att.com:80/~astopen/man/man1/sed.html)(1),
[`perl`](/web/20150328001607/http://www2.research.att.com:80/~astopen/man/man1/perl.html)(1),
[`tw`](/web/20150328001607/http://www2.research.att.com:80/~astopen/man/man1/tw.html)(1),
[`regex`](/web/20150328001607/http://www2.research.att.com:80/~astopen/man/man3/regex.html)(3)

# CAVEATS

Some expressions of necessity require exponential space and/or time.

# BUGS

Some expressions may use sub-optimal algorithms. For example, don't use
this implementation to compute primes.

# IMPLEMENTATION

`version`
:   grep (AT&T Research) 2012-05-07

`author`
:   Glenn Fowler
    &lt;[glenn.s.fowler@gmail.com](https://web.archive.org/web/20150328001607/mailto:glenn.s.fowler@gmail.com)&gt;

`author`
:   Doug McIlroy
    &lt;[doug@research.bell-labs.com](https://web.archive.org/web/20150328001607/mailto:doug@research.bell-labs.com)&gt;

`copyright`
:   Copyright © 1995-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20150328001607/http://www.eclipse.org/org/documents/epl-v10.html)


