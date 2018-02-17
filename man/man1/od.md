# NAME

od - dump files in octal or other formats

# SYNOPSIS

`od` \[ `options` \] \[ file ... \] \[ \[+\]offset\[.|b|k|m|ll|LL\] \]

# DESCRIPTION

`od` dumps the contents of the input files in various formats on the
standard output. The standard input is read if `-` or no files are
specified. Each output line contains the file offset of the data in the
leftmost column, followed by one or more columns in the specified
format. If more than one format is specified then the subsequent lines
are listed with the offset column blank. Second and subsequent
occurrences of a repeated output line are replaced by a single line with
\`\`' in the first data column.
`--format=c`, `--format=C` and `--format=O` interpret bytes as
characters in the LC\_CTYPE locale category. The three types differ only
in the C style escape sequences recognized; `--format=C` explicitly
allows future extensions. The backslash character is written as \`\\'
and NUL is written as \`\\0'. Other non-printable characters are written
as one three-digit octal number for each byte in the character.
Printable multi-byte characters are written in the area corresponding to
the first byte of the character; the two-character sequence \`\`\`' is
written in the area corresponding to each remaining byte in the
character; the remaining bytes for `-p` are written as \` '. If
`--skip` or `--count` position the file into the middle of a
multibyte character then the entire multibyte character is silently
treated as non-character bytes.

If the output format is specified by one of the obsolete forms (not
`--format`) then the last file argument is interpreted as an offset
expression if it matches the extended regular expression
`+?\[0-9\]+\\.?\[bkm\]?(ll|LL)?` . In this case the first `offset`
bytes of the file are skipped. The optional `b` means bytes, `k`
means Kb, and `m` means Mb. `ll` and `LL` are ignored for
compatibility with some systems.

# OPTIONS

-`A`, --`address-radix`=`radix`
:   The file offset radix.

    [`d`]()
    : decimal

    [`o`]()
    : octal

    [`x`]()
    : hexadecimal

    [`n`]()
    : none - do not print offset

The default value is `o`.\
-`B`, --`swap`=`op`
:   Swap input bytes according to the bit mask `op`, which is the
    inclusive or of:

    [`01`]()
    : swap 8-bit bytes

    [`02`]()
    : swap 16-bit words

    [`04`]()
    : swap 32-bit longs

    [`0`]()
    : swap for big endian testing

-`j`, --`skip-bytes`=`bytes`
:   Skip `bytes` bytes into the data before formatting.

-`N`, --`count|read-bytes`=`bytes`
:   Output only `bytes` bytes of data.

-`m`, --`map`=`codeset`
:   `--printable` and `--format=m` bytes are converted from
    `codeset` to the native codeset. The codesets are:

    [`ascii`]()
    : \
        8 bit ascii

    [`ebcdic`]()
    : \
        X/Open ebcdic

    [`o|ebcdic-o`]()
    : \
        mvs OpenEdition ebcdic

    [`h|ebcdic-h`]()
    : \
        ibm OS/400 AS/400 ebcdic

    [`s|ebcdic-s`]()
    : \
        siemens posix-bc ebcdic

    [`i|ebcdic-i`]()
    : \
        X/Open ibm ebcdic (not idempotent)

    [`m|ebcdic-m`]()
    : \
        mvs ebcdic

    [`u|ebcdic-u`]()
    : \
        microfocus cobol ebcdic

    [`native`]()
    : \
        native code set

-`p`, --`printable`
:   Output the printable bytes (after `--map` if specified), in the
    last data column. Non-printable byte values are printed as \`.'.

-`z`, --`strings`\[=`length`\]
:   Output NUL terminated strings of at least `length` bytes. The option
    value may be omitted. The default value is `3`.

-`t`, --`format|type`=`format\[size\]`
:   The data item output `format` and `size`. A decimal byte count or
    size code may follow all but the `a`, `c`, `C`, `m` and
    `O` formats.

    [`a`]()
    : ISO/IEC 646:1991 named characters

    [`A`]()
    : hexadecimal floating point

    [`b`]()
    : binary character

    [`c`]()
    : locale character or backslash escape (\\a \\b \\f \\n \\r
        \\t \\v)

    [`C`]()
    : locale character or backslash escape (current and
        future escapes)

    [`d`]()
    : signed decimal

    [`f`]()
    : floating point

    [`m`]()
    : `--map` mapped character or hexadecimal value if not printable

    [`o`]()
    : octal

    [`O`]()
    : locale character or backslash escape (\\b \\f \\n \\r \\t)

    [`u`]()
    : unsigned decimal

    [`x`]()
    : hexadecimal

    [`z`]()
    : printable bytes

    [`----- sizes -----`]()\
    [`C`]()
    : sizeof(char)

    [`S`]()
    : sizeof(short)

    [`I`]()
    : sizeof(int)

    [`L|l`]()
    : sizeof(long)

    [`D|ll`]()
    : sizeof(long long)

    [`F`]()
    : sizeof(float)

    [`D`]()
    : sizeof(double)

    [`L`]()
    : sizeof(long double)

The default value is `o2`.\
-`T`, --`test`=`test`
:   Enable internal implementation specific tests.

    [`b``n`]()
    : Allocate a fixed input buffer of size `n`.

    [`m``n`]()
    : Set the mapped input buffer size to `n`.

    [`n`]()
    : Turn off the `SF\_SHARE` input buffer flag.

-`v`, --`all|output-duplicates`
:   Output all data.

-`w`, --`per-line|width`=`per-line`
:   The number of items to format per output line. `per-line` must be a
    multiple of the least common multiple of the sizes of the
    format types.

-`a`
: Equivalent to `-ta`.

-`b`
: Equivalent to `-toC`.

-`c`
: Equivalent to `-tO`.

-`C`
: Equivalent to `-tO`.

-`d`
: Equivalent to `-tuS`.

-`D`
: Equivalent to `-tuL`.

-`f`
: Equivalent to `-tfF`.

-`F`
: Equivalent to `-tfD`.

-`h`
: Equivalent to `-txS`.

-`i`
: Equivalent to `-tdS`.

-`l`
: Equivalent to `-tdL`.

-`o`
: Equivalent to `-toS`.

-`O`
: Equivalent to `-toL`.

-`s`
: Equivalent to `-tdS`.

-`S`
: Equivalent to `-tdL`.

-`u`
: Equivalent to `-tuS`.

-`U`
: Equivalent to `-tuL`.

-`x`
: Equivalent to `-txS`.

-`X`
: Equivalent to `-txL`.

# SEE ALSO

[`sed`](/web/20141128030247/http://www2.research.att.com/~astopen/man/man1/sed.html)(1),
[`strings`](/web/20141128030247/http://www2.research.att.com/~astopen/man/man1/strings.html)(1),
[`swap`](/web/20141128030247/http://www2.research.att.com/~astopen/man/man3/swap.html)(3),
[`ascii`](/web/20141128030247/http://www2.research.att.com/~astopen/man/man5/ascii.html)(5)

# IMPLEMENTATION

`version`
:   od (AT&T Research) 2012-05-31

`author`
:   Glenn Fowler
    &lt;[glenn.s.fowler@gmail.com](https://web.archive.org/web/20141128030247/mailto:glenn.s.fowler@gmail.com)&gt;

`author`
:   David Korn
    &lt;[dgkorn@gmail.com](https://web.archive.org/web/20141128030247/mailto:dgkorn@gmail.com)&gt;

`copyright`
:   Copyright © 1992-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030247/http://www.eclipse.org/org/documents/epl-v10.html)


