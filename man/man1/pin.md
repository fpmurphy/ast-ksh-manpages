# NAME

pin - induce a pzip partition on fixed record data

# SYNOPSIS

`pin` \[ `options` \] file ...

# DESCRIPTION

`pin` induces a
[`pzip`](/web/20141128030248/http://www2.research.att.com/~astopen/man/man1/pzip.html)(1)
column partition on data files of fixed length rows (records) and
columns (fields). If a partition file is specified then that partition
is refined. A partition file, suitable for use by `pin`,
[`pzip`](/web/20141128030248/http://www2.research.att.com/~astopen/man/man1/pzip.html)(1)
or
[`pop`](/web/20141128030248/http://www2.research.att.com/~astopen/man/man1/pop.html)(1)
is listed on the standard output. The input `file` is referred to as
`training data`. `--size` allows more than one `file` argument,
otherwise exactly one file must be specified.
Partitions are induced in a three step process:

``(1)
: If `--partition` is not specified then a subset of columns are
    filtered from the training data for partitioning. This filtering
    usually gathers high frequency columns from the data. A high
    frequency column has data with a high rate of change between rows.
    High frequency cutoff rates, specified by `--high`, typically
    range from 10% to 50%, depending on the data.
    [`pzip`](/web/20141128030248/http://www2.research.att.com/~astopen/man/man1/pzip.html)(1)
    compresses low frequency columns much more efficiently than
    [`gzip`](/web/20141128030248/http://www2.research.att.com/~astopen/man/man1/gzip.html)(1).

``(2)
: A heuristic search determines an initial ordering of high frequency
    columns to present to step (3). An optimal solution for both
    ordering and partitioning is NP-complete.

``(3)
: The optimal partition for the ordering from step (2) is determined
    by a dynamic program that computes the compressed size for all
    partitions that preserve order. Alternative greedy methods are also
    available that work more quickly but do not guarantee optimality.

See
[`pzip`](/web/20141128030248/http://www2.research.att.com/~astopen/man/man1/pzip.html)(1)
for a detailed description of file partitions and column frequencies.
`pin` can run for a long time on some data (e.g., 10 minutes on a
400Mhz Pentium with `--high 80 --window 4M`). Use `--verbose`
possibly with `--test=010` to monitor progress.

# OPTIONS

-`b`, --`bzip`
:   Use
    [`bzip`](/web/20141128030248/http://www2.research.att.com/~astopen/man/man1/bzip.html)(1)
    compression instead of the default
    [`gzip`](/web/20141128030248/http://www2.research.att.com/~astopen/man/man1/gzip.html)(1).
    `bzip` is not fully supported by `pzip`, pending
    further investigation.

-`c`, --`cache`
:   Generate some information on `file` that can be reused on another
    invocation; this information is saved in `pin-``base`, where
    `base` is the base name (no directory) of `file`. Saved information
    includes column frequencies and singleton and pairwise column
    `gzip` rates.

-`g`, --`group`=`columns`
:   Sets the maximum number of columns in any partition group. Lower
    values speed up the the dynamic program but also may produce
    sub-optimal solutions. The default value is `row-size`.

-`h`, --`high`=`columns`
:   Select this number of columns with the highest frequencies for the
    columns in the partition. If `columns` is followed by \`%' then
    columns with frequencies larger than this percentage are selected.
    The default value is `10%`.

-`l`, --`level`=`level`
:   Sets the `gzip` compression level to `level`. Levels range from 1
    (fastest, worst compression) to 9 (slowest, best compression). The
    default value is `6`.

-`m`, --`maxhigh`=`maxhigh`
:   Exit with exit code 3 if the number of high frequency columns
    exceeds `maxhigh` . If `maxhigh` is followed by \`%' then the
    limit is `maxhigh` percent of the total number of columns. The
    default value is `40%`.

-`o`, --`sort`
:   Sort the window data by row before inducing the partition.

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
:   Specifies the input row size (number of byte columns). The row size
    is determined by sampling the input if not specified.

-`v`, --`verbose`
:   List partition search details on the standard error.

-`w`, --`window`=`window-size`
:   Limit the number of training data rows used to induce the partition.
    The window size may be decreased to accomodate an integral number of
    complete rows. The default value is `4M`.

-`O`, --`optimize`=`method`
:   Choose the optimization (partitioning) method for step (3) above.
    The methods are:

    [`dynamic`]()
    : \
        dynamic program optimal partition

    [`greedy`]()
    : \
        greedy approximation partition

    [`none`]()
    : no partition

    [`transitive`]()
    : \
        transitive greedy approximation partition

The default value is `dynamic`.\
-`Q`, --`regress`
:   Generate output for regression testing, such that identical
    invocations with identical input files will generate the
    same output.

-`R`, --`reorder`=`method`
:   Choose the reordering method for step (2) above. The methods are:

    [`heuristic`]()
    : \
        heuristic reorder

    [`none`]()
    : no reordering

    [`tsp`]()
    : tsp reordering

The default value is `heuristic`.\
-`S`, --`size`
:   Ignore `--row`, determine the fixed record size based on a window
    of sampled data, print it on the standard output, and exit. If more
    than one `file` is specified then the record size and name are
    printed for each file. If the sample is insufficient, or if
    `--verify` is specified, then all of the data read to determine
    the row size. A `0` size means the record size could not
    be determined.

-`T`, --`test`=`test-mask`
:   Enable implementation-specific tests and tracing.

    [`0x0010`]()
    : \
        Enable reorder keep trace.

    [`0x0020`]()
    : \
        Enable reorder skip/cost trace.

    [`0x0040`]()
    : \
        Enable reorder permutation trace.

    [`0x0080`]()
    : \
        Enable reorder level 2 merge prune.

    [`0x0100`]()
    : \
        Disable reorder merge prune.

    [`0x0200`]()
    : \
        Partition using initial tsp cycles.

-`V`, --`verify`
:   Verify `--size` by reading all data instead of the window sample.

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

[`bzip`](/web/20141128030248/http://www2.research.att.com/~astopen/man/man1/bzip.html)(1),
[`gzip`](/web/20141128030248/http://www2.research.att.com/~astopen/man/man1/gzip.html)(1),
[`pop`](/web/20141128030248/http://www2.research.att.com/~astopen/man/man1/pop.html)(1),
[`pzip`](/web/20141128030248/http://www2.research.att.com/~astopen/man/man1/pzip.html)(1),
[`pzip`](/web/20141128030248/http://www2.research.att.com/~astopen/man/man3/pzip.html)(3)

# IMPLEMENTATION

`version`
:   pin (AT&T Research) 2003-07-17

`author`
:   Glenn Fowler
    &lt;[glenn.s.fowler@gmail.com](https://web.archive.org/web/20141128030248/mailto:glenn.s.fowler@gmail.com)&gt;

`author`
:   Adam Buchsbaum
    &lt;[alb@adambuchsbaum.com](https://web.archive.org/web/20141128030248/mailto:alb@adambuchsbaum.com)&gt;

`copyright`
:   Copyright © 1998-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030248/http://www.eclipse.org/org/documents/epl-v10.html)


