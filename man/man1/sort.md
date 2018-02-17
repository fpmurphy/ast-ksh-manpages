# NAME

sort - sort and/or merge files

# SYNOPSIS

`sort` \[ `options` \] \[ file ... \]

# DESCRIPTION

`sort` sorts lines of all the `files` together and writes the result
on the standard output. The file name `-` means the standard input. If
no files are named, the standard input is sorted.
The default sort key is an entire line. Default ordering is
lexicographic by bytes in machine collating sequence. The ordering is
affected globally by the locale and/or the following options, one or
more of which may appear. See
[`recsort`](/web/20150717163021/http://www2.research.att.com/~astopen/man/man3/recsort.html)(3)
for details.

For backwards compatibility the `-o` option is allowed in any file
operand position when neither the `-c` nor the `--` options are
specified.

# OPTIONS

-`k`, --`key`=`pos1\[,pos2\]|.reclen|.position.length\]\]`
\
Restrict the sort key to a string beginning at `pos1` and ending at
`pos2`. `pos1` and `pos2` each have the form `m.n`, counting from 1,
optionally followed by one or more of the flags `CMbdfginprZ`; `m`
counts fields from the beginning of the line and `n` counts characters
from the beginning of the field. If any flags are present they override
all the global ordering options for this key. If `.n` is missing from
`pos1`, it is taken to be 1; if missing from `pos2`, it is taken to be
the end of the field. If `pos2` is missing, it is taken to be end of
line. The second form specifies a fixed record length `reclen`, and the
last form specifies a fixed field at byte position `position` (counting
from 1) of `length` bytes. The obsolescent `reclen:fieldlen:offset`
(byte offset from 0) is also accepted.
-`K`, --`oldkey`=`pos`
\
Specified in pairs: `-K` `pos1` `-K` `pos2`, where positions count
from 0.
-`R`, --`record|recfmt`=`format`
\
Sets the record format to `format`; newlines will be treated as normal
characters. The formats are:

`d\[``terminator`\]
:   Variable length with record `terminator` character, `\\n`
    by default.

`\[f\]``reclen`
:   Fixed record length `reclen`.

`v\[op...\]`
:   Variable length. `h4o0z2bi` (4 byte IBM V format descriptor) if
    `op` are omitted. `op` may be a combination of:

    [`h``n`]()
    : Header size is `n` bytes (default 4).

    [`o``n`]()
    : Size offset in header is `n` bytes (default 0).

    [`z``n`]()
    : Size length is `n` bytes (default min(`h`-`o`,2)).

    [`b`]()
    : Size is big-endian (default).

    [`l`]()
    : Size is little-endian (default `b`).

    [`i`]()
    : Record length includes header (default).

    [`n`]()
    : Record length does not include header (default `i`).

`%`
: If the record format is not otherwise specified, and the any input
    file name, from left to right, ends with `%``format` or
    `%``format``.`\` then the record format is set to `format`. In
    addition, the `-o` path, if specified and if it does not contain
    `%` and if it names a regular file, is renamed to contain the
    input `%` `format`.

`-`
: The first block of the first input file is sampled to check for
    `v` variable length and `f` fixed length format records. Not all
    formats are detected. `sort` exits with an error diagnostic if the
    record format cannot be determined from the sample.

-`b`, --`ignorespace|ignore-leading-blanks`
\
Ignore leading white space (spaces and tabs) in field comparisons.
-`d`, --`dictionary`
\
\`Phone directory' order: only letters, digits and white space are
significant in string comparisons.
-`E`, --`codeset|convert`=`codeset|from:to`
\
The field data codeset is `codeset` or the field data must be converted
from the `from` codeset to the `to` codeset. The codesets are:

`ascii`
:   8 bit ascii

`ebcdic`
:   X/Open ebcdic

`o|ebcdic-o`
:   mvs OpenEdition ebcdic

`h|ebcdic-h`
:   ibm OS/400 AS/400 ebcdic

`s|ebcdic-s`
:   siemens posix-bc ebcdic

`i|ebcdic-i`
:   X/Open ibm ebcdic (not idempotent)

`m|ebcdic-m`
:   mvs ebcdic

`u|ebcdic-u`
:   microfocus cobol ebcdic

`native`
:   native code set

-`f`, --`fold|ignorecase`
\
Fold lower case letters onto upper case.
-`h`, --`scaled|human-readable`
\
Compare numbers scaled with IEEE 1541-2002 suffixes.
-`i`, --`ignorecontrol`
\
Ignore characters outside the ASCII range 040-0176 in string
comparisons.
-`J`, --`shuffle|jumble`=`seed`
\
Do a random shuffle of the sort keys. `seed` specifies a pseudo random
number generator seed. A `seed` of 0 generates a seed based on time and
pid.
-`n`, --`numeric`
\
An initial numeric string, consisting of optional white space, optional
sign, and a nonempty string of digits with optional decimal point, is
sorted by value.
-`g`, --`floating`
\
Numeric, like `-n`, with `e`-style exponents allowed.
-`p`, --`bcd|packed-decimal`
\
Compare packed decimal (bcd) numbers with trailing sign.
-`M`, --`months`
\
Compare as month names. The first three characters after optional white
space are folded to lower case and compared. Invalid fields compare low
to `jan`.
-`r`, --`reverse|invert`
\
Reverse the sense of comparisons.
-`t`, --`tabs`=`tab-char`
\
\`Tab character' separating fields is `char`.
-`c`, --`check`
\
Check that the single input file is sorted according to the ordering
rules; give no output on the standard output. If the input is out of
sort then write one diagnostic line on the standard error and exit with
code `1`.
-`C`, --`silent-check`
\
Like `--check` except no diagnostic is written.
-`j`, --`processes|nproc|jobs`=`processes`
\
Use up to `jobs` separate processes to sort the input. The current
implementation still uses one process for the final merge phase;
improvements are planned.
-`m`, --`merge`
\
Merge; the input files are already sorted.
-`u`, --`unique`
\
Unique. Keep only the first of multiple records that compare equal on
all keys. Implies `-s`.
-`s`, --`stable`
\
Stable sort. When all keys compare equal, preserve input order. The
default is `--nostable` (`unstable` sort): when all keys compare
equal, break the tie by using the entire record, ignoring all but the
`-r` option.
-`o`, --`output`=`output`
\
Place output in the designated `file` instead of on the standard output.
This file may be the same as one of the inputs. The `file` `-` names
the standard output. The option may appear among the file arguments,
except after `--`.
-`l`, --`library`=`library\[,name=value...\]`
\
Load the external sort discipline `library` with optional comma
separated `name=value` arguments. Libraries are loaded, in left to right
order, after the sort method has been initialized.
-`T`, --`tempdir`=`tempdir`
\
Put temporary files in `tempdir`. The default value is `/usr/tmp`.
-`L`, --`list`
\
List the available sort methods. See the `-x` option.
-`x`, --`method`=`method`
\
Specify the sort method to apply:

`rasp`
: Initial radix split into a forest of splay trees.

`radix`
:   Radix sort.

`splay`
:   Splay tree sort.

`verify`
:   Verify that the input is sorted.

`copy`
: Copy (no sort).

The default value is `rasp`.
-`v`, --`verbose`
\
Trace the sort progress on the standard error.
-`P`, --`plugins`=`style`
\
List plugin information for each `file` operand in --`style` on the
standard error. If no `file` operands are specified then the first
instance of each `sort` plugin installed on `\$PATH` or a sibling
dir on `\$PATH` is listed. The special `style` `list` lists a line
on the standard output for each plugin with the name, a tab character,
and plugin specific command line options parameterized by `\${style}`
(suitable for `eval` 'ing in
[`sh`](/web/20150717163021/http://www2.research.att.com/~astopen/man/man1/sh.html)(1).)
The default value is `list|man|html|nroff|usage`.
-`Z`, --`zd|zoned-decimal`
\
Compare zoned decimal (ZD) numbers with embedded trailing sign.
-`z`, --`size|zip`=`type\[size\]`
\
Suggest using the specified number of bytes of internal store to tune
performance. Power of 2 and power of 10 size suffixes are accepted. Type
is a single character and may be one of:

`a`
: Buffer alignment.

`b`
: Input reserve buffer size.

`c`
: Input chunk size; sort chunks of this size and disable merge.

`i`
: Input buffer size.

`m`
: Maximum number of intermediate merge files.

`p`
: Input sort size; sort chunks of this size before merge.

`o`
: Output buffer size.

`r`
: Maximum record size.

`I`
: Decompress the input if it is compressed.

`O`
: [`gzip`](/web/20150717163021/http://www2.research.att.com/~astopen/man/man1/gzip.html)(1)
    compress the output.

-`X`, --`test`=`test`
\
Enables implementation defined test code. Some or all of these may be
disabled.

`dump`
: List detailed information on the option settings.

`io`
: List io file paths.

`keys`
: List the canonical key for each record.

`read`
: Force input file read by disabling memory mapping.

`show`
: Show setup information and exit before sorting.

`test`
: Immediatly exit with status 0; used to verify this implementation

-`D`, --`debug`=`level`
\
Sets the debug trace level. Higher levels produce more output.
-`S|y` `size`
\
Equivalent to `-zp``size`; if `size` has no suffix then `ki` is
assumed.
+`pos1` -`pos2` is the classical alternative to `-k`, with counting
from 0 instead of 1, and pos2 designating next-after-last instead of
last character of the key. A missing character count in `pos2` means 0,
which in turn excludes any `-t` tab character from the end of the key.
Thus +1 -1.3 is the same as `-k` 2,2.3 and +1r -3 is the same as
`-k` 2r,3.
Under option `-t``x` fields are strings separated by `x`; otherwise
fields are non-empty strings separated by white space. White space
before a field is part of the field, except under option `-b`. A `b`
flag may be attached independently to `pos1` and `pos2`.
When there are multiple sort keys, later keys are compared only after
all earlier keys compare equal. Except under option `-s`, lines with
all keys equal are ordered with all bytes significant. `-S` turns off
`-s`, the last occurrence, left-to-right, takes affect.
Sorting is done by a method determined by the `-x` option. `-L`
lists the available methods. rasp (radix+splay-tree) is the default and
current all-around best.
Single-letter options may be combined into a single string, such as
`-cnrt:`. The option combination `-di` and the combination of `-n`
with any of `-diM` are improper. Posix argument conventions are
supported.
Options `-b`, `-c`, `-d`, `-f`, `-i`, `-k`, `-m`, `-n`,
`-o`, `-r`, `-t`, and `-u` are in the Posix and/or X/Open
standards.

# DIAGNOSTICS

`sort` comments and exits with non-zero status for various trouble
conditions and for disorder discovered under option `-c` .

# SEE ALSO

[`comm`](/web/20150717163021/http://www2.research.att.com/~astopen/man/man1/comm.html)(1),
[`join`](/web/20150717163021/http://www2.research.att.com/~astopen/man/man1/join.html)(1),
[`uniq`](/web/20150717163021/http://www2.research.att.com/~astopen/man/man1/uniq.html)(1),
[`recsort`](/web/20150717163021/http://www2.research.att.com/~astopen/man/man3/recsort.html)(3)

# CAVEATS

The never-documented default `pos1`=0 for cases such as `sort -1` has
been abolished. An input file overwritten by `-o` is not replaced
until the entire output file is generated in the same directory as the
input, at which point the input is renamed.

# IMPLEMENTATION

`version`
:   sort (AT&T Research) 2010-08-11

`author`
:   Glenn Fowler
    &lt;[glenn.s.fowler@gmail.com](https://web.archive.org/web/20150717163021/mailto:glenn.s.fowler@gmail.com)&gt;

`author`
:   Phong Vo
    &lt;[kpv@research.att.com](https://web.archive.org/web/20150717163021/mailto:kpv@research.att.com)&gt;

`author`
:   Doug McIlroy
    &lt;[doug@research.bell-labs.com](https://web.archive.org/web/20150717163021/mailto:doug@research.bell-labs.com)&gt;

`copyright`
:   Copyright © 1996-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20150717163021/http://www.eclipse.org/org/documents/epl-v10.html)


