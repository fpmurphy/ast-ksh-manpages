# NAME

pop - operate on partioned fixed row and column data

# SYNOPSIS

`pop` \[ `options` \] \[ file \]

# DESCRIPTION

`pop` operates on partitioned fixed row and column data files. It can
cut high or low frequency partition columns, list format field names for
partition columns, and list the partition column frequencies. See
[`pzip`](/web/20141128030248/http://www2.research.att.com/~astopen/man/man1/pzip.html)(1)
for a detailed description of file partitions and column frequencies.

# OPTIONS

-`c`, --`cut`
:   Copy selected columns from the input rows to the standard output.

-`e`, --`endiff`
:   Copy the row-by-row difference to the standard output.

-`f`, --`format`=`file`
:   Specifies the data format (schema) file. Two input styles
    are accepted. The first style lists field names and sizes in
    consecutive order: \``name`,`size`\[,`comment`...\]'. The second
    style lists the field offset range and name: \``begin`\[-`end`\]
    `name`'. Column offsets start at 0. Names are used to label
    partition group listings on the standard output, with partition
    groups separated by an empty line.

-`h`, --`high`
:   List information on high frequency columns only. This is
    the default.

-`i`, --`information`
:   List the selected column frequency information on the
    standard output.

-`l`, --`low`
:   List information on low frequency columns only.

-`m`, --`map`
:   List the partition file with the row size equal to the number of
    high frequency columns and the high frequency columns renumbered in
    order from 0. This partition file can then be used on high frequency
    data produced by the `--cut` option.

-`n`, --`newline`
:   Append a newline to each cut output row.

-`o`, --`override`=`name=value`
:   Override the column partition. Currently only fixed value columns
    may be specified. The syntax is `begin`\[-`end`\]='`value`' where
    `begin` is the beginning column offset (starting at 0), `end` is the
    ending column offset for an inclusive range, and `value` is the
    fixed column value. Uncompress time is improved when high frequency
    columns are given fixed values (see the `--partition` option).

-`p`, --`partition`=`file`
:   Specifies the data row size and the high frequency column partition
    groups and permutation. The partition file is a sequence of lines.
    Comments start with \# and continue to the end of the line. The
    first non-comment line specifies the optional name string in "...".
    The next non-comment line specifies the row size. The remaining
    lines operate on column offset ranges of the form: `begin`\[-`end`\]
    where `begin` is the beginning column offset (starting at 0), and
    `end` is the ending column offset for an inclusive range. The
    operators are:

    [`range \[...\]`]()
    : \
        places all columns in the specified `range` list in the same
        high frequency partition group. Each high frequency partition
        group is processed as a separate block by the underlying
        compressor
        ([`gzip`](/web/20141128030248/http://www2.research.att.com/~astopen/man/man1/gzip.html)(1)
        by default).

    [`range='value'`]()
    : \
        specifies that each column in `range` has the fixed character
        value `value` . C-style character escapes are valid for `value`.

-`r`, --`row`=`row-size`
:   Specifies the input row size (number of byte columns). Exactly one
    of `--row` or `--partition` must be specified.

-`u`, --`undiff`
:   The inverse of the `--endiff` difference encoding.

-`v`, --`verbose`
:   List header information on the input `pzip` file or `partition-file`
    and continue processing.

-`x`, --`identify`
:   Identify output information columns with labels from the
    `--format` file.

-`Q`, --`regress`
:   Generate output for regression testing, such that identical
    invocations with identical input files will generate the
    same output.

-`T`, --`test`=`test-mask`
:   Enable implementation-specific tests and tracing.

-`X`, --`prefix`=`count\[\`terminator\]`
:   Uncompressed data contains a prefix that is defined by `count` and
    an optional `terminator`. This data is not `pzip` compressed.
    `terminator` may be one of:

    [`omitted`]()
    : \
        `count` bytes.

    [`L`]()
    : `count` `newline` terminated records.

    [`'``char`']()
    : \
        `count` `char` terminated records.

# SEE ALSO

[`gzip`](/web/20141128030248/http://www2.research.att.com/~astopen/man/man1/gzip.html)(1),
[`pin`](/web/20141128030248/http://www2.research.att.com/~astopen/man/man1/pin.html)(1),
[`pzip`](/web/20141128030248/http://www2.research.att.com/~astopen/man/man1/pzip.html)(1),
[`pzip`](/web/20141128030248/http://www2.research.att.com/~astopen/man/man3/pzip.html)(3)

# IMPLEMENTATION

`version`
:   pop (AT&T Research) 2003-04-05

`author`
:   Glenn Fowler
    &lt;[glenn.s.fowler@gmail.com](https://web.archive.org/web/20141128030248/mailto:glenn.s.fowler@gmail.com)&gt;

`copyright`
:   Copyright © 1998-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030248/http://www.eclipse.org/org/documents/epl-v10.html)


