# NAME

release - list recent changes

# SYNOPSIS

`release` \[ `options` \] \[ file ... \]

# DESCRIPTION

`release` lists the changes within the date range specified by the
`--from` and `--to` options. The input files are assumed to contain
date tag lines of the form \[`cc`\]`yy-mm-dd` \[ `text` \] (or
[`date`](/web/20141128030249/http://www2.research.att.com/~astopen/man/man1/date.html)(1)
default format), where `cc` is determined by a Y2K window year of 69 (we
can produce an example coding dated 1991 - this can be patented?, how
about 1+1=2?.) The date tag lines are followed by `readme` text in
reverse chronological order (newer entries at the top of the file.) If
no selection options are spcified then all changes are listed. If no
`file` operands are specified then the standard input is read.
The entries for each `file` are annotated with the file directory name.

# OPTIONS

-`f`, --`from`=`date`
:   Entries older than `date` are omitted.

-`r`, --`release`=`count`
:   List all changes that include the first `count` release marks. A
    release mark has a date tag followed by optional space and at least
    three `-` characters. Changes from release mark `count`+1 are
    not listed. If there are no release marks then the date range is
    used; if there is at least one release mark then the date range is
    ignored and at most `count` release marks will be listed.

-`t`, --`to`=`date`
:   Entries newer than `date` are omitted.

-`V`
: Print the program version and exit.

# SEE ALSO

[`package`](/web/20141128030249/http://www2.research.att.com/~astopen/man/man1/package.html)(1)

# IMPLEMENTATION

`version`
:   release (AT&T Research) 2000-01-28

`author`
:   Glenn Fowler

`copyright`
:   Copyright © 1999-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030249/http://www.eclipse.org/org/documents/epl-v10.html)


