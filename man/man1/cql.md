# NAME

cql - C query language

# SYNOPSIS

`cql` \[ `options` \] \[ data \]

# DESCRIPTION

`cql` applies C style expressions to flat database files. It fills the
gap between
[`awk`](/web/20141128030241/http://www2.research.att.com/~astopen/man/man1/awk.html)(1)
and full blown relational database management programs. A flat database
is a sequence of `newline` terminated records of `delimiter`
separated fields.
Files are processed as follows. `cql` first evaluates the `begin`
expression if defined, then sequentially applies the `select`
expression to all records. The `action` expression is evaluated for
each record that `select` evaluates to non-0. After all records have
been checked the `done` expression is evaluated if defined, and
`cql` exits. The default `select` expression is `1` (all records
are selected) and the default `action` expression prints the record on
the standard output.

Depending on the input file declarations, `cql` may generate index
files for quick record access. Indexes are used to filter out records
for which `select` would evaluate to `0`. Index files are placed in
the current directory and each is named by changing the suffix to
`.hix` or by adding a `.hix` suffix.

# OPTIONS

-`a`, --`active`
:   Run in active mode by reading declarations and expressions from the
    standard input. The special sequence `%%` separates the
    declarations from the expressions. `%%` after an expression
    applies that expression to the input files. `EOF` terminates the
    active session. Active mode error message lines are prefixed with
    `%% cql:`.

-`c`, --`compile`=`file`
:   If `file` matches `\`.c` then the `cql` expression are converted
    to C and placed in `file`, and `cql` exits. `file` may then be
    compiled with
    [`cc`](/web/20141128030241/http://www2.research.att.com/~astopen/man/man1/cc.html)(1).
    Otherwise `file` is assumed to be a `dll` (compiled and linked from
    a `.c` file previously generated by `clq`) and is loaded into
    the current process.

-`e|d`, --`expression`=`expr`
:   `expression` defines the database schemas and the labelled
    expressions that control database traversal. Multiple
    `--expression` expressions are parsed in order from left to right.

-`f`, --`file`=`file`
:   Equivalent to `-e "\#include '``file``'"`.

-`l`, --`local`
:   By default index files are only generated in the directory
    containing the data files; `--local` causes index files to be
    generated in the current directory.

-`n`, --`index`
:   Enable index file generation. If index files must be (re)generated
    and `--noindex` is on then `cql` exits with a diagnostic. On by
    default; -`n` means --`noindex`.

-`r`, --`replace`
:   Replace the top level database view with an updated view if there
    were updates.

-`R`, --`regenerate`
:   If index files are required then `--regenerate` forces them to be
    regenerated even if the otherwise seem up-to-date.

-`u`, --`update`
:   Only output updated records. By default all selected records
    are output.

-`w`, --`warn`
:   Disable malformed data warning messages. With `--nowarn` malformed
    records are silently repaired or discarded. On by default; -`w`
    means --`nowarn`.

-`I`, --`include`=`dir`
:   Add `dir` to the list of directories searched for include and
    library files. The default `../lib/cql` directories on `\$PATH`
    are added to this list.

-`D`, --`debug`=`level`
:   Set the debug trace level to `level`. Higher levels produce
    more output.

-`T`, --`test`=`mask`
:   Inclusive-or `mask` into the implementation defined test mask.
    Occasionally a particular mask may be used as a temporary
    bug workaround. Otherwise use at your own risk.

-`g`, --`g2`
:   (obsolete) Enable `g2` output mode.

# SCHEMAS

A schema is similar to a C `struct` declaration with the `struct`
keyword omitted. A schema specifies names and types for the fields in a
database record. The types are:

`char\``
:   A null-terminated C string.

`date\_t`
:   A C `unsigned long` variable whose string representation is
    a date.

`elapsed\_t`
:   A C `long` variable whose string representation is elapsed time in
    1/100 seconds.

`float`
:   A C `double` variable.

`hex`
: A C `unsigned long` variable whose string representation
    is hexadecimal.

`int`
: A C `long` variable.

`string`
:   Equivalent to a null-terminated C `char\``.

`unsigned`
:   A C `unsigned long` variable.

Schemas are themselves types. `schema field;` declares a subfield within
a record and `schema\` field;` declares a field that indexes another
schema. In this case the `field` value is a string key that is used to
match the first field in the referenced schema. The `register` prefix
denotes fields that should be indexed; references to other schemas are
always indexed.
The first declared schema becomes the main schema (the schema of the
data to be scanned.) The main schema may also be set by `schema=`
`schema``;`. `schema``.delimiter="``delimiter``";` sets the
delimiter for `schema` and `schema` `.input="``file``";` sets the
input to `file`. The default delimiter is "`;`". The main schema input
is the `data` command line argument if specified. Otherwise schema input
file names are determined by the schema name with an optional `.db`
suffix. Multiple schemas may be placed in a single file using the
[`pax`](/web/20141128030241/http://www2.research.att.com/~astopen/man/man1/pax.html)(1)
`vdb` archive format.

# EXPRESSIONS

A labelled expression is defined by one of: [`label : statement-list`]()
[`type label`() { statement-list }`]()
Supported expression labels are:

`action`
:   Evaluated for each record in which `select` returns non-zero. The
    default `action` lists each selected record as it appears in
    the databse.

`begin`
:   Evaluated once before the traversal begins. The return value
    is ignored.

`end`
: Evaluated once after the traversal ends. The return value
    is ignored.

`select`
:   Evaluated once for each record. If the return value is non-zero then
    `action` is evaluated. The default `select` return value is
    always non-zero.

`closure`
:   TBD

`loop`
: TBD

`select` is assumed when `label`: or `type label`() is omitted.
`statement-list` is composed of
[`expr`](/web/20141128030241/http://www2.research.att.com/~astopen/man/man3/expr.html)(3)
C style expressions, including `int` `variable`, ... and `float`
`variable`, ... declarations, `(int)` and `(float)` casts, `if` -
`else` conditionals, `for` and `while` loops, and { ... } blocks.
The trailing `;` in any expression is optional. In the absense of a
`return` statement the expression value is the value of the last
evaluated expression in `statement-list`. Numbers and comments follow C
syntax. String operands must be quoted with either "..." or '...'.
String comparisons (`==` and `!=`) treat the right hand operand as a
[`ksh`](/web/20141128030241/http://www2.research.att.com/~astopen/man/man1/ksh.html)(1)
file match pattern.
The expressions operate on the fields in the current input record. The
`begin` and `end` expressions operate on a null valued current
record. If a `date\_t` type field is an operand to a binary operator
then the other operand may be a string that is interpreted as a
[`date`](/web/20141128030241/http://www2.research.att.com/~astopen/man/man1/date.html)(1)
date expression; there is similar treatment for other types with
alternate string representations.

There is also a predefined readonly schema with the following elements:

`elapsed\_t clock`
:   The elapsed time in 1/100 seconds since this `cql` started.

`date\_t date`
:   The date when this `cql` started.

`int errors`
:   The current soft error count. `cql` continues after a soft error
    but exits with a non-zero exit status when complete.

`int line`
:   The current input file line number.

`int offset`
:   The current input file byte offset.

`int record`
:   The current input file record number.

`int select`
:   The current number of selected records.

`int size`
:   The size in bytes of the current input record.

`date\_t time`
:   The current date and time.

The following
[`expr`](/web/20141128030241/http://www2.research.att.com/~astopen/man/man3/expr.html)(3)
functions are also supported:

`cql.getenv`(`name`)
:   Returns the value of the environment variable `name`. The empty
    string is returned for undefined environment variables.

`cql.path`(`name,len`)
:   Truncates the file pathname `name` to `len` bytes.
    cql.sub(`string,old,new,flags`)?Returns the substituted value of
    `string` the first match of the
    [`egrep`](/web/20141128030241/http://www2.research.att.com/~astopen/man/man1/egrep.html)(1)
    style regular expression `old` replaced by `new`. `flags` may be any
    combination of:

    [`g`]()
    : Substitute all matches of `old`.

    [`l`]()
    : Convert matches to lower case.

    [`u`]()
    : Convert matches to upper case.

`exit`(`expr`)
:   Causes `cql` to exit with the exit code `expr`. `expr` defaults to
    0 if omitted.

`printf`(`format\[,arg...\]`)
:   Print the arguments on `stdout` using the
    [`printf`](/web/20141128030241/http://www2.research.att.com/~astopen/man/man3/printf.html)(3)
    specification `format`.

`eprintf`(`format\[,arg...\]`)
:   Like `printf` but output goes to `stderr` .

`query`(`format\[,arg...\]``)`
:   Prompt with the
    [`printf`](/web/20141128030241/http://www2.research.att.com/~astopen/man/man3/printf.html)(3)
    message on `stderr` for an interactive response. A line beginning
    with `y` returns 1, `q` or `EOF` causes `cql` to exit
    immediately, and any other input returns 0.

# SEE ALSO

[`awk`](/web/20141128030241/http://www2.research.att.com/~astopen/man/man1/awk.html)(1),
[`grep`](/web/20141128030241/http://www2.research.att.com/~astopen/man/man1/grep.html)(1),
[`ksh`](/web/20141128030241/http://www2.research.att.com/~astopen/man/man1/ksh.html)(1),
[`pax`](/web/20141128030241/http://www2.research.att.com/~astopen/man/man1/pax.html)(1),
[`perl`](/web/20141128030241/http://www2.research.att.com/~astopen/man/man1/perl.html)(1),
[`tw`](/web/20141128030241/http://www2.research.att.com/~astopen/man/man1/tw.html)(1),
[`expr`](/web/20141128030241/http://www2.research.att.com/~astopen/man/man3/expr.html)(3),
[`printf`](/web/20141128030241/http://www2.research.att.com/~astopen/man/man3/printf.html)(3),
[`tm`](/web/20141128030241/http://www2.research.att.com/~astopen/man/man3/tm.html)(3)

# IMPLEMENTATION

`version`
:   cql (AT&T Research) 2002-09-06

`author`
:   Glenn Fowler

`copyright`
:   Copyright © 1991-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030241/http://www.eclipse.org/org/documents/epl-v10.html)


