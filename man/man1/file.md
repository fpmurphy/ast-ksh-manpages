# NAME

file - determine file type

# SYNOPSIS

`file` \[ `options` \] \[ file ... \]

# DESCRIPTION

`file` tests and attempts to classify each `file` argument.
Non-regular files are classified by their
[`stat`](/web/20150302161016/http://www2.research.att.com:80/~astopen/man/man2/stat.html)(2)
types. Empty and non-readable regular files are classified as such.
Otherwise a data block is read from `file` and this is used to match
against the `magic` file(s) (see `MAGIC FILE` below). Files with less
than 1024 bytes of data are labelled `small` to note that the sample
may be too small for an accurate classification. Failing a content
match, the file name extension may be used to classify. As a last resort
statistical sampling is done for a small range of languages and
applications. Failed matches usually result in the less informative
`ascii text` or `binary data`.

# OPTIONS

-`a`, --`all`
:   List all magic table matches.

-`b`, --`brief|no-filename`
:   Suppress the output line file name prefix.

-`c`, --`mime`
:   List the
    [`mime`](/web/20150302161016/http://www2.research.att.com:80/~astopen/man/man1/mime.html)(1)
    classification for each `file` . Although the default descriptions
    are fairly consistent, use `--mime` for precise
    classification matching.

-`d`, --`default-magic`
:   Equivalent to `--magic=-`.

-`f`, --`files|file-list`=`file`
:   `file` contains list of file names, one per line, that
    are classified.

-`i`, --`ignore-magic`
:   Equivalent to `--magic=/dev/null`.

-`l`, --`list`
:   The loaded `magic` files are listed and then `file` exits.

-`M`, --`magic`=`file`
:   `file` is loaded as a `magic` file. More than one `--magic` option
    may be specified; the precedence is from left to right. The first
    `--magic` option causes the default system `magic` file to be
    ignored; the file `-` may then be specified to explicitly load the
    default system `magic` file. To ignore all magic files specify the
    file `/dev/null` and no others.

-`m`, --`append-magic`=`file`
:   `file` is loaded as a `magic` file. Equivalent to the `--magic`
    option, except that the default system `magic` file is still
    loaded last. If `--magic` is also specified then the default
    system `magic` is only loaded if explicity specified.

-`p`, --`pattern|match`=`pattern`
:   Only files with descriptions matching the
    [`sh`](/web/20150302161016/http://www2.research.att.com:80/~astopen/man/man1/sh.html)(1)
    match `pattern` are listed. `file` exits with status 0 if any
    files match, 0 otherwise.

-`q`, --`quiet|silent`
:   Do not list matching `--pattern` files.

-`L`, --`logical|dereference`
:   Follow symbolic links.

-`P|h`, --`physical`
:   Don't follow symbolic links.

-`w`, --`warn`
:   Enable magic file parse warning messages.

# MAGIC FILE

A `magic` file specifies file content and name match expressions,
descriptions, and
[`mime`](/web/20150302161016/http://www2.research.att.com:80/~astopen/man/man1/mime.html)(1)
classifications. Each line in the file consists of five `tab`
separated fields:

`\[op\]offset`
:   `offset` determines tha data location for the content test.
    `(@``expression` `)` specifies an indirect offset, i.e., the
    offset is the numeric contents of the data location at `expression`.
    The default indirect numeric size is 4 bytes; a `B` suffix denotes
    1 byte, `H` denotes 2 bytes, and `Q` denotes 8 bytes. `offset`
    may also be one of { `atime` `blocks` `ctime` `fstype`
    `gid` `mode` `mtime` `name` `nlink` `size` `uid` } to
    access
    [`stat`](/web/20150302161016/http://www2.research.att.com:80/~astopen/man/man2/stat.html)(2)
    information for the current file. The optional `op` specifies
    relationships with surrounding `magic` lines:

    [`+`]()
    : previous fields in block match, current optional

    [`&`]()
    : previous and current fields in block match

    [`|`]()
    : previous fields in block do not match, subsequent skipped

    [`{`]()
    : start nesting block

    [`}`]()
    : end nesting block

    [`c{`]()
    : function declaration and call (1 char names)

    [`}`]()
    : function return

    [`c`()]()
    : function call

`type`
: The content data type:

    [`byte`]()
    : 1 byte integer

    [`short`]()
    : \
        2 byte integer

    [`long`]()
    : 4 byte integer

    [`quad`]()
    : 8 byte integer

    [`date`]()
    : 4 byte time\_t

    [`version`]()
    : \
        4 byte unsigned integer of the form `YYYYMMDD` for `YYYY-MM-DD`,
        0x`YYZZ` for `YY.ZZ`, or 0x`WWXXYYZZ` for `WW.XX.YY.ZZ`

    [`edit`]()
    : substitute operator for string data: %`old`%`new`%\[glu\], where
        `%` is any delimiter

    [`match`]()
    : \
        case insensitive
        [`sh`](/web/20150302161016/http://www2.research.att.com:80/~astopen/man/man1/sh.html)(1)
        match pattern operator for string data

`\[mask\]operator`
:   `mask` is an optional `&``number` that is masked (bit `and`)
    with the content data before comparison. `operator` is one of {
    `&lt; &lt;= &gt; &gt;= != ==` }. Numeric values may be decimal,
    octal or hex.

`description`
:   The description text. Care was taken to maintain consistency between
    all descriptions, i.e., character case, grammatical parts placement,
    and punctuation, making description pattern matches feasible.
    `description` may contain one
    [`printf`](/web/20150302161016/http://www2.research.att.com:80/~astopen/man/man3/printf.html)(3)
    format specification for the current data value at `offset`.

`mime`
: The
    [`mime`](/web/20150302161016/http://www2.research.att.com:80/~astopen/man/man1/mime.html)(1) type/subtype.
    This provides a standard and consistent matching key space.

# FILES

`lib/file/magic`
:   Default magic file on `\$PATH`.

# SEE ALSO

[`find`](/web/20150302161016/http://www2.research.att.com:80/~astopen/man/man1/find.html)(1),
[`ls`](/web/20150302161016/http://www2.research.att.com:80/~astopen/man/man1/ls.html)(1),
[`mime`](/web/20150302161016/http://www2.research.att.com:80/~astopen/man/man1/mime.html)(1),
[`tw`](/web/20150302161016/http://www2.research.att.com:80/~astopen/man/man1/tw.html)(1)

# IMPLEMENTATION

`version`
:   file (AT&T Research) 2011-08-01

`author`
:   Glenn Fowler

`copyright`
:   Copyright © 1989-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20150302161016/http://www.eclipse.org/org/documents/epl-v10.html)


