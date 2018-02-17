# NAME

rectify - induce fixed length record groups from data

# SYNOPSIS

`rectify` \[ `options` \] \[ file ... \]

# DESCRIPTION

`rectify` induces fixed length record groups from input data by
sampling and comparing character frequencies. The standard input is read
if `-` or no files are specified.

# OPTIONS

-`c`, --`context`=`context`
:   List `context` records at the beginning and end of record groups
    larger that 3\`context`.

-`d`, --`description`=`file`
:   Specify a structured dump description file. Each line of this file
    describes the size and content of a contiguous portion of the
    input file. The description is applied separately to each
    input file. Comments and optional labels in the following
    descriptions are listed with the `--verbose` option. Supported
    descriptions are:

    [`c comment`]()
    : \
        comment

    [`d size \[label\]`]()
    : \
        `size` bytes of data with optional label

    [`i size \[label\]`]()
    : \
        ignore `size` bytes of data

    [`r size count \[label\]`]()
    : \
        `count` records of length `size`

    [`t count`]()
    : \
        Match `count` records against the `T` record table. `count`=0
        continues until no record type match is found.

    [`z size \[label\]`]()
    : \
        a string with length determined by a `size` byte binary integer

    [`T idlen id size unit \[offset\]`]()
    : \
        Defines a sized record table entry.

        [`idlen`]()
        : \
            type identifier length, must be &lt;= 4 bytes

        [`id`]()
        : type identifier, starting at record offset 0

        [`size`]()
        : default record size

        [`unit`]()
        : if &gt; 0 then the record is variable length and the size is
            the byte at `offset`

        [`offset`]()
        : \
            if `unit` &gt; 0 then this byte multiplied by `unit` is the
            size of variable length data appended to the record

-`f`, --`format`=`format`
:   Byte output
    [`printf`](/web/20141128030249/http://www2.research.att.com/~astopen/man/man3/printf.html)(3)
    format. The default value is `02x`.

-`g`, --`group`
:   Group output in 4's. On by default; -`g` means --`nogroup`.

-`m`, --`min`=`min`
:   Minimum record length to consider. The default value is `8`.

-`n`, --`count`=`count`
:   List the top `count` candidate record lengths. The default value is
    `16`.

-`o`, --`offset`=`offset`
:   Start description listing at `offset`. The default value is `0`.

-`r`, --`run`=`run`
:   List runs at least as long as `run`.

-`v`, --`verbose`
:   Dump description labels with data.

# SEE ALSO

[`pin`](/web/20141128030249/http://www2.research.att.com/~astopen/man/man1/pin.html)(1),
[`pop`](/web/20141128030249/http://www2.research.att.com/~astopen/man/man1/pop.html)(1)

# IMPLEMENTATION

`version`
:   rectify (AT&T Research) 1999-03-22

`author`
:   Glenn Fowler
    &lt;[glenn.s.fowler@gmail.com](https://web.archive.org/web/20141128030249/mailto:glenn.s.fowler@gmail.com)&gt;

`copyright`
:   Copyright © 1998-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030249/http://www.eclipse.org/org/documents/epl-v10.html)


