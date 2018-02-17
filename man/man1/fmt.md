# NAME

fmt - simple text formatter

# SYNOPSIS

`fmt` \[ `options` \] \[ file ... \]

# DESCRIPTION

`fmt` reads the input files and left justifies space separated words
into lines `width` characters or less in length and writes the lines to
the standard output. The standard input is read if `-` or no files are
specified. Blank lines and interword spacing are preserved in the
output. Indentation is preserved, and lines with identical indentation
are joined and justified.
`fmt` is meant to format mail messages prior to sending, but may also
be useful for other simple tasks. For example, in
[`vi`](/web/20141128030244/http://www2.research.att.com/~astopen/man/man1/vi.html)(1)
the command `:!}fmt` will justify the lines in the current paragraph.

# OPTIONS

-`c`, --`crown-margin`
:   Preserve the indentation of the first two lines within a paragraph,
    and align the left margin of each subsequent line with that of the
    second line.

-`o`, --`optget`
:   Format concatenated
    [`optget`](/web/20141128030244/http://www2.research.att.com/~astopen/man/man3/optget.html)(3)
    usage strings.

-`s`, --`split-only`
:   Split lines only; do not join short lines to form longer ones.

-`u`, --`uniform-spacing`
:   One space between words, two after sentences.

-`w`, --`width`=`columns`
:   Set the output line width to `columns`. The default value is `72`.

# SEE ALSO

[`mailx`](/web/20141128030244/http://www2.research.att.com/~astopen/man/man1/mailx.html)(1),
[`nroff`](/web/20141128030244/http://www2.research.att.com/~astopen/man/man1/nroff.html)(1),
[`troff`](/web/20141128030244/http://www2.research.att.com/~astopen/man/man1/troff.html)(1),
[`vi`](/web/20141128030244/http://www2.research.att.com/~astopen/man/man1/vi.html)(1),
[`optget`](/web/20141128030244/http://www2.research.att.com/~astopen/man/man3/optget.html)(3)

# IMPLEMENTATION

`version`
:   fmt (AT&T Research) 2007-01-02

`author`
:   Glenn Fowler
    &lt;[glenn.s.fowler@gmail.com](https://web.archive.org/web/20141128030244/mailto:glenn.s.fowler@gmail.com)&gt;

`author`
:   David Korn
    &lt;[dgkorn@gmail.com](https://web.archive.org/web/20141128030244/mailto:dgkorn@gmail.com)&gt;

`copyright`
:   Copyright © 1992-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030244/http://www.eclipse.org/org/documents/epl-v10.html)


