# NAME

nocom - strip comments from C source files

# SYNOPSIS

`nocom` \[ `options` \] \[ file ... \]

# DESCRIPTION

`nocom` strips `// ...` and `/\` ... \`/` comments from each C
source `file` and writes the result on the standard output. Comments
that span multiple lines are replaced by `newline` characters to
retain the original source line numbering. If `file` is omitted then the
standard input is read.

# SEE ALSO

[`cc`](/web/20141128030247/http://www2.research.att.com/~astopen/man/man1/cc.html)(1),
[`wc`](/web/20141128030247/http://www2.research.att.com/~astopen/man/man1/wc.html)(1)

# IMPLEMENTATION

`version`
:   nocom (AT&T Research) 1994-01-11

`author`
:   Glenn Fowler
    &lt;[glenn.s.fowler@gmail.com](https://web.archive.org/web/20141128030247/mailto:glenn.s.fowler@gmail.com)&gt;

`copyright`
:   Copyright © 1987-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030247/http://www.eclipse.org/org/documents/epl-v10.html)


