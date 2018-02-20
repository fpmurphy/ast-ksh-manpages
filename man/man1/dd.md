# NAME

dd - convert and copy a file

# SYNOPSIS

`dd` \[ `options` \]

# DESCRIPTION

`dd` copies an input file to an output file with optional conversions.
The standard input and output are used by default. Input and output
block sizes can be specified to take advantage of physical io
limitations. Options are of the form `name=value` and may be specified
with 0, 1, or 2 leading \`-' characters.
A `number` argument may be a scaled number with optional trailing
multipliers of the form \`\` `number`', \`x `number`' or \`X `number`'.
Scale suffixes may be one of:

`b|B`
: 512

`k|K`
: 1000

`ki|Ki`
:   1024

`m|M`
: 1000000

`mi|Mi`
:   1048576

`g|G`
: 1000000000

`gi|Gi`
:   1073741824

`t|T`
: 1000000000000

`ti|Ti`
:   1099511627776

`p|P`
: 1000000000000000

`pi|Pi`
:   1125899906842624

`e|E`
: 1000000000000000000

`ei|Ei`
:   1152921504606846976

# OPTIONS

`bs`=`number`
:   Input and output block size.

`cbs`=`number`
:   Conversion buffer size (logical record length).

`conv`=`conversion`
:   Convert input. `conversion` may be one of:

    [`a2e`]()
    : ascii to ebcdic

    [`a2i`]()
    : ascii to ibm

    [`a2n`]()
    : ascii to native

    [`a2o`]()
    : ascii to open edition ebcdic

    [`ascii`]()
    : \
        ebcdic to ascii

    [`block`]()
    : \
        newline-terminated ascii to fixed record length

    [`e2a`]()
    : ebcdic to ascii

    [`ebcdic`]()
    : \
        equivalent to `a2e`

    [`i2a`]()
    : ibm to ascii

    [`ibm`]()
    : ascii to ibm ebcdic

    [`ignerror`]()
    : \
        continue processing after errors

    [`ispecial`]()
    : \
        currently ignored

    [`lcase`]()
    : \
        to lower case

    [`n2a`]()
    : native to ascii

    [`noerror`]()
    : \
        stop processing only after 5 consecutive errors

    [`notrunc`]()
    : \
        do not truncate pre-existing output files

    [`o2a`]()
    : open edition ibm to ascii

    [`ospecial`]()
    : \
        currently ignored

    [`swab`]()
    : swap byte pairs

    [`sync`]()
    : Pad each input block to `ibs`. Pad with spaces if
        `conv=block` or `conv=unblock`, otherwise pad with nulls.

    [`ucase`]()
    : \
        to upper case

    [`unblock`]()
    : \
        fixed-length records to newline-terminated records

`count`=`number`
:   Copy only `number` input blocks.

`from`=`codeset`
:   Convert from `codeset` to the `to`=`codeset` or the local default.
    `codeset` names are matched by left-anchored case-insensitive
    [`ksh`](/web/20141128030242/http://www2.research.att.com/~astopen/man/man1/ksh.html)(1) patterns.
    `codeset` may be one of:

    [a|ascii|?(iso)?(-)646|?(iso)?(-)8859|latin]()
    : \
        8 bit ascii

    [e|ebcdic?(-)?(\[1e\])]()
    : \
        X/Open ebcdic

    [o|ebcdic?(-)\[3o\]|?(cp|ibm)1047|open?(-)edition]()
    : \
        mvs OpenEdition ebcdic

    [h|ebcdic?(-)h|?(cp|ibm)?(00)37|\[oa\]s?(/-)400]()
    : \
        ibm OS/400 AS/400 ebcdic

    [s|ebcdic?(-)s|siemens|posix-bc]()
    : \
        siemens posix-bc ebcdic

    [i|ebcdic?(-)\[2i\]|ibm]()
    : \
        X/Open ibm ebcdic (not idempotent)

    [m|ebcdic?(-)m|mvs]()
    : \
        mvs ebcdic

    [u|ebcdic?(-)(u|mf)|microfocus]()
    : \
        microfocus cobol ebcdic

    [n|native|local]()
    : \
        native code set

    [un|unicode|utf]()
    : \
        multibyte 8-bit unicode

    [um|ume|utf?(-)7]()
    : \
        multibyte 7-bit unicode

    [(big|euc)\`]()
    : \
        euc family

    [dos?(-)?(855)]()
    : \
        dos code page

    [ucs?(-)?(2)?(be)|utf-16?(be)]()
    : \
        unicode runes

    [ucs?(-)?(2)le|utf-16le]()
    : \
        little endian unicode runes

`ibs`=`number`
:   Input block size.

`if`=`file`
:   The input file name; standard input is the default.

`iseek`=`number`
:   Seek `number` blocks from the beginning of the input file
    before copying.

`obs`=`number`
:   Output block size.

`of`=`file`
:   The output file name; standard output is the default.

`oseek|seek`=`number`
:   Seek `number` blocks from the beginning of the output file
    before copying.

`silent`
:   `silent` does not print the total number of io blocks on exit.

`skip`=`number`
:   Skip `number` blocks before reading. Seek is used if possible,
    otherwise the blocks are read and discarded.

`swap`=`number`
:   Swap bytes acording to the inclusive or of: 1-byte, 2-short, 4-long,
    8-quad, etc.

`to`=`codeset`
:   Convert to `codeset` from the `from`=`codeset` or the
    local default. See `from` for `codeset` names.

# SEE ALSO

[`cp`](/web/20141128030242/http://www2.research.att.com/~astopen/man/man1/cp.html)(1),
[`iconv`](/web/20141128030242/http://www2.research.att.com/~astopen/man/man1/iconv.html)(1),
[`pax`](/web/20141128030242/http://www2.research.att.com/~astopen/man/man1/pax.html)(1),
[`tr`](/web/20141128030242/http://www2.research.att.com/~astopen/man/man1/tr.html)(1),
[`seek`](/web/20141128030242/http://www2.research.att.com/~astopen/man/man2/seek.html)(2)

# IMPLEMENTATION

`version`
:   dd (AT&T Research) 2011-04-21

`author`
:   Glenn Fowler

`copyright`
:   Copyright © 1989-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030242/http://www.eclipse.org/org/documents/epl-v10.html)


