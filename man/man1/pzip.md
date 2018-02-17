# NAME

pzip - fixed record partition compress/decompress

# SYNOPSIS

`pzip` \[ `options` \] file

# DESCRIPTION

`pzip` compresses and decompresses data files of fixed length rows
(records) and columns (fields). It performs better than
[`gzip`](/web/20141128030249/http://www2.research.att.com/~astopen/man/man1/gzip.html)(1)
in space/time on data that has many (typically &gt; 50%) columns that
change at a low rate (columns with a low rate of change are low
frequency; columns with a high rate of change are high frequency).
The `pzip` compress format is itself `gzipped`; decompressed data is
reorganized according to the user-specified `partition` file (see the
`--partition` option below) before being passed to `gzip`. Low
frequency columns are difference encoded and high frequency column
groups are transposed to column-major order. The `gzip` tables are
flushed between each column partition group. This has a positive
space/time effect on the `gzip` string match and huffman tables.

If a `partition` file is specified then `pzip` compresses the input
`file` to the standard output, otherwise `pzip` decompresses the input
`file` to the standard ouput. If `file` is omitted then the standard
input is used. If the standard input is a tty then `/dev/null` is
silently used.

`file` may be `pzip` compressed, `gzip` compressed, or raw. `pzip` files
self-identify; the row size and partition can be determined from the
`pzip` header. For `gzip` and raw data, the following are done to
determine the row size:

``(1)
: The row size is taken from the `--row` option if specified.

``(2)
: If the `--partition` option is specified then the row size is
    taken from the `partition` file.

``(3)
: If the data is newline-terminated and if it contains at least two
    lines and if the first two data lines have the same length then that
    length is taken to be the row size.

``(4)
: Otherwise the row size cannot be determined and `pzip` exits with
    a diagnostic.

# OPTIONS

-`a`, --`append`
:   Sets the `PZ\_APPEND` flag that may be used by some disciplines.

-`b`, --`bzip`
:   Use
    [`bzip`](/web/20141128030249/http://www2.research.att.com/~astopen/man/man1/bzip.html)(1)
    compression instead of the default
    [`gzip`](/web/20141128030249/http://www2.research.att.com/~astopen/man/man1/gzip.html)(1).
    `bzip` is not fully supported, pending further investigation.

-`c`, --`comment`=`comment`
:   Place `comment` in the output `pzip` file header when compressing.
    The comment is listed by the `--header` option.

-`x`, --`crc`
:   Enable `gzip` crc32 cyclic redundancy checking for decompress. On
    some systems this can double the execution wall time. Most data
    corruption errors are still caught even with `nocrc`.

-`d`, --`dump`
:   Enable detailed tracing.

-`B`, --`bufsize`=`size`
:   Set the output buffer size to `size` -- for debugging.

-`D`, --`debug`=`level`
:   Set the debug trace level to `level`. Higher levels produce
    more output.

-`O`, --`dio`
:   Push the
    [`sfdcdio`](/web/20141128030249/http://www2.research.att.com/~astopen/man/man3/sfdcdio.html)(3)
    direct io discipline on the input streams. Silently ignored on
    systems that do not support direct io.

-`G`, --`gzip`
:   `--nogzip` disables `gzip` compression. Most often used for
    conversion or debugging. On by default; -`G` means --`nogzip`.

-`h`, --`header`
:   List header information on the input `pzip` file and exit. This
    output is compatible with the `--partition` file format.

-`l`, --`library`=`library`
:   Loads the dll `library` via the `pzlib`() call. `library` must
    contain the function `int pz\_init(Pz\_t\` pz, Pzdisc\_t\` disc)`
    which is called during `pzip` stream initialization. `pz\_init`
    allows run time modification to `disc`: most often it supplies
    alternate discipline functions. Runtime libraries may interpret
    options specific to the library; library usage and description will
    be appended to online help output if the help options appear after
    the `--library` option. Runtime libraries may provide additional
    diagnostics and tracing when `--summary`, `--verbose` or
    `--dump` are specified. In general, runtime libraries are not
    needed for decompression. The `--header` option lists the runtime
    libraries used to compress the input file.

-`z`, --`lzw`
:   Use
    [`compress`](/web/20141128030249/http://www2.research.att.com/~astopen/man/man1/compress.html)(1)
    lzw compression instead of the default
    [`gzip`](/web/20141128030249/http://www2.research.att.com/~astopen/man/man1/gzip.html)(1).
    `lzw` is not fully supported, pending further investigation.

-`o`, --`override`=`begin\[-end\]=value`
:   Override the column partition. Currently only fixed value columns
    may be specified. The syntax is `begin`\[-`end`\]='`value`' where
    `begin` is the beginning column offset (starting at 0), `end` is the
    ending column offset for an inclusive range, and `value` is the
    fixed column value. Uncompress time is improved when high frequency
    columns are given fixed values (see the `--partition` option).

-`p`, --`partition`=`file`
:   `file` specifies the data row size and the high frequency column
    partition groups and permutation. `file` may contain URL-like
    components: `path``?name=``part` or `path``\#``part` reads the
    partition file `path` and uses the partition named `part`. Other
    options may be set by separating each with , or space. The partition
    file is a sequence of lines. Comments start with \# and continue to
    the end of the line. The first non-comment line specifies the
    optional name string in "...". The next non-comment line specifies
    the row size. The remaining lines operate on column offset ranges of
    the form: `begin`\[-`end`\] where `begin` is the beginning column
    offset (starting at 0), and `end` is the ending column offset for an
    inclusive range. The file name `//` or `/gzip/` disables
    `pzip` partitioning and applies only `gzip` compression. The
    operators are:

    [`range \[...\]`]()
    : \
        places all columns in the specified `range` list in the same
        high frequency partition group. Each high frequency partition
        group is processed as a separate block by the underlying
        compressor
        ([`gzip`](/web/20141128030249/http://www2.research.att.com/~astopen/man/man1/gzip.html)(1)
        by default).

    [`range='value'`]()
    : \
        specifies that each column in `range` has the fixed character
        value `value` . C-style character escapes are valid for `value`.

-`Z`, --`push`
:   Push the
    [`sfdcpzip`](/web/20141128030249/http://www2.research.att.com/~astopen/man/man3/sfdcpzip.html)(3)
    io discipline rather than direct library calls. Used for debugging
    and performance testing.

-`P`, --`pzip`
:   `--nopzip` disables `pzip` compression. Most often used for
    conversion or debugging. On by default; -`P` means --`nopzip`.

-`Q`, --`regress`
:   Generate output for regression testing, such that identical
    invocations with identical input files will generate the
    same output.

-`r`, --`row`=`row-size`
:   Specifies the input row size (number of byte columns) for data that
    does not self-identify.

-`S`, --`split`\[=`pattern`\]
:   Instead of compressing, the input split discipline, which must be
    specified by a subsequent `--library` option, splits the input
    data into files named `id`. `id` is determined by the split
    discipline `namef` function. The optional `pattern` is a
    [`ksh`](/web/20141128030249/http://www2.research.att.com/~astopen/man/man1/ksh.html)(1)
    file match pattern that limits the split to `id`'s matching
    `pattern` (e.g., `--split='1234|98765'`.) If `--append` is also
    specified then the data is appened to any pre-existing `id` files;
    otherwise each file is truncated when the first record containing
    `id` data is read. If there are no records with `id` data then the
    `id` file is not modified. `--split` should be used in a separate
    directory, and the directory should be cleared when `--append` is
    not specified to avoid mixing inconsistent data. No records will be
    written to a split file with size &gt;= `--window` bytes. The
    option value may be omitted.

-`s`, --`summary`
:   Enable summary tracing to the standard error. Runtime libraries may
    add addtional information to the default
    [`pzip`](/web/20141128030249/http://www2.research.att.com/~astopen/man/man3/pzip.html)(3)
    library summary output. Compression summary includes the compression
    rate, bytes per record, and compression wall time. This option also
    enables split discipline warnings about `id` partitions that should
    be generated by
    [`pin`](/web/20141128030249/http://www2.research.att.com/~astopen/man/man1/pin.html)(1)
    and added to the partition file to improve compression. The
    [`pin`](/web/20141128030249/http://www2.research.att.com/~astopen/man/man1/pin.html)(1)
    output, with an additional "`id`" line manually prepended, can then
    be appended to an existing partition file.

-`T`, --`test`=`mask`
:   Enable
    [`pzip`](/web/20141128030249/http://www2.research.att.com/~astopen/man/man3/pzip.html)(3)
    implementation-specific tests and tracing.

-`v`, --`verbose`
:   Enable intermediate tracing.

-`w`, --`window`=`window-size`
:   Each chunk of `window` bytes is compressed separately. The window
    size may be silently decreased to accomodate an integral number of
    complete rows. The default value is `4M`.

-`W`, --`write-test`=`group`
:   Loop on `sfread`()/
    [`pzwrite`](/web/20141128030249/http://www2.research.att.com/~astopen/man/man3/pzwrite.html)(3)
    in chunks of `group` records rather than a single `pzdeflate` ()
    call for compression. Used for debugging and performance testing.

-`X`, --`prefix`=`count\[\`terminator\]`
:   Uncompressed data contains a prefix that is defined by `count` and
    an optional `terminator`. This data is preserved but is not
    `pzip` compressed. If `count` is `0` on uncompress then the
    header is not copied to the output. `terminator` may be one of:

    [`omitted`]()
    : \
        `count` bytes.

    [`L`]()
    : `count` `newline` terminated records.

    [`'``char`']()
    : \
        `count` `char` terminated records.

# SEE ALSO

[`bzip`](/web/20141128030249/http://www2.research.att.com/~astopen/man/man1/bzip.html)(1),
[`gzip`](/web/20141128030249/http://www2.research.att.com/~astopen/man/man1/gzip.html)(1),
[`pin`](/web/20141128030249/http://www2.research.att.com/~astopen/man/man1/pin.html)(1),
[`pop`](/web/20141128030249/http://www2.research.att.com/~astopen/man/man1/pop.html)(1),
[`pzip`](/web/20141128030249/http://www2.research.att.com/~astopen/man/man3/pzip.html)(3)

# BUGS

`pzip` decompress currently fails if the standard input is a pipe.
This will be addressed in a future release.

# IMPLEMENTATION

`version`
:   pzip (AT&T Research) 2003-07-17

`author`
:   Glenn Fowler
    &lt;[glenn.s.fowler@gmail.com](https://web.archive.org/web/20141128030249/mailto:glenn.s.fowler@gmail.com)&gt;

`copyright`
:   Copyright © 1998-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030249/http://www.eclipse.org/org/documents/epl-v10.html)


