# NAME

iconv - codeset conversion

# SYNOPSIS

`iconv` \[ `options` \] \[ pid ... \]

# DESCRIPTION

`iconv` converts the encoding of characters in the `file` operands
from one codeset to another and writes the results to the standard
output. If `file` is `-` or omitted then the standard input is read.
Character encodings in either codeset may include single-byte values
(for example, for the ISO 8859-1:1987 standard characters) or multi-byte
values (for example, for certain characters in the ISO 6937:1983
standard). Invalid characters in the input stream (either those that are
not valid members of the input codeset or those that have no
corresponding value in the output codeset) are output as the underscore
character (`\_`) in the output codeset.

The `native` codeset is determined by the `LANG`, `LC\_ALL` and
`LC\_CTYPE` environment variables. The supported codesets are matched
by these left-anchored case-insensitive
[`ksh`](/web/20141128030244/http://www2.research.att.com/~astopen/man/man1/ksh.html)(1)
patterns:

a|ascii|?(iso)?(-)646|?(iso)?(-)8859|latin
:   8 bit ascii

e|ebcdic?(-)?(\[1e\]
:   X/Open ebcdic

o|ebcdic?(-)\[3o\]|?(cp|ibm)1047|open?(-)edition
:   mvs OpenEdition ebcdic

h|ebcdic?(-)h|?(cp|ibm)?(00)37|\[oa\]s?(/-)400
:   ibm OS/400 AS/400 ebcdic

s|ebcdic?(-)s|siemens|posix-bc
:   siemens posix-bc ebcdic

i|ebcdic?(-)\[2i\]|ibm
:   X/Open ibm ebcdic (not idempotent)

m|ebcdic?(-)m|mvs
:   mvs ebcdic

u|ebcdic?(-)(u|mf)|microfocus
:   microfocus cobol ebcdic

n|native|local
:   native code set

un|unicode|utf
:   multibyte 8-bit unicode

um|ume|utf?(-)7
:   multibyte 7-bit unicode

big|euc)\`
:   euc family

dos?(-)?(855
:   dos code page

ucs?(-)?(2)?(be)|utf-16?(be
:   unicode runes

ucs?(-)?(2)le|utf-16le
:   little endian unicode runes

Conversion between certain codesets may not be supported. Also, since
the standard(s) provide no support for listing the known codesets, the
above list may be incomplete.

# OPTIONS

-`a`, --`all`
:   List all conversion errors. By default (and `--omit` is
    not specified) `iconv` stops after the first error.

-`c`, --`omit`
:   Omit invalid input characters from the output. Invalid input
    characters still affect the exit status.

-`e`, --`errors`
:   Do not ignore conversion errors.

-`f`, --`from`=`codeset`
:   The input codeset is set to `codeset`. The default value is
    `native`.

-`i`, --`ignore`
:   Ignore conversion errors.

-`l`, --`list`
:   List all known codesets on the standard output.

-`s`, --`silent`
:   Suppress invalid character diagnostics. Invalid input characters
    still affect the exit status. If `--all` is also specified then
    non-zero invalid character counts are listed.

-`t`, --`to`=`codeset`
:   The output codeset is set to `codeset`. The default value is
    `native`.

# SEE ALSO

[`dd`](/web/20141128030244/http://www2.research.att.com/~astopen/man/man1/dd.html)(1),
[`iconv`](/web/20141128030244/http://www2.research.att.com/~astopen/man/man3/iconv.html)(3),
[`setlocale`](/web/20141128030244/http://www2.research.att.com/~astopen/man/man3/setlocale.html)(3)

# IMPLEMENTATION

`version`
:   iconv (AT&T Research) 2011-01-11

`author`
:   Glenn Fowler
    &lt;[glenn.s.fowler@gmail.com](https://web.archive.org/web/20141128030244/mailto:glenn.s.fowler@gmail.com)&gt;

`copyright`
:   Copyright © 1989-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030244/http://www.eclipse.org/org/documents/epl-v10.html)


