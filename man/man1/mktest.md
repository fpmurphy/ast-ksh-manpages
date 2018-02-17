# NAME

mktest - generate a regression test scripts

# SYNOPSIS

`mktest` \[ `options` \] unit.rt \[ unit \[ arg ... \] \]

# DESCRIPTION

`mktest` generates regression test scripts from test template commands
in the `unit`.`rt` file. The generated test script writes temporary
output to test`unit`.tmp and compares it to the expected output in
test`unit`.out. Run the test script with the `--accept` option to
(re)generate the test`unit`.out.

# OPTIONS

-`s`, --`style`=`style`
:   The script style:

    [`regress`]()
    : \
        [`regress`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/regress.html)(1)
        command input.

    [`shell`]()
    : \
        Standalone test shell script.

The default value is `regress`.\
-`w`, --`width`=`width`
:   Set the output format width to approximately `width`. The default
    value is `80` .

# INPUT FILES

The regression test command file `unit``.rt` is a
[`ksh`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/ksh.html)(1)
script that makes calls to the following functions:

`DATA` `file` \[ - | \[ options \] data\]
:   Create input data `file` that is empty (-) or contains `data`
    subject to
    [`print`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/print.html)(1)
    `options` or that is a copy of the DATA command standard input. Set
    `file` to `-` to name the standard input.

`DIAGNOSTICS`
:   Diagnostic messages of unspecified format are expected.

`DO` `command` \[ `arg` ... \]
:   Execute `command` if the current test is active.

`EXEC \[` `arg` ... \]
:   Run the command under test with optional arguments. If the standard
    input is not specified then the standard input of the previous EXEC
    is used. The standard input of the first EXEC in a TEST group is an
    empty regular file.

`EXPORT` `name`=`value` ...
:   Export list for subsequent commands in the TEST group or for all
    TEST groups if before the first TEST group.

`IGNORESPACE \[ 0 | 1`
:   Ignore space differences when comparing expected output.

`KEEP` `pattern` ...
:   File match patterns of files to retain between TEST groups.

`NOTE` `comment`
:   `comment` is added to the current test script.

`PROG` `command` \[ `arg` ... \]
:   Run `command` with optional arguments.

`TEST \[` `number` \] \[ `description` ... \]
:   Define a new test group with optional `number` and `descripion`.

`TWD \[` `dir` ... \]
:   Set the temporary test dir to `dir`. The default is `unit` `.tmp`,
    where `unit` is the test input file sans directory and suffix. If
    `dir` matches `/\`` then it is the directory name; if `dir` is
    non-null then the prefix `\${TMPDIR:-/tmp}` is added; otherwise if
    `dir` is omitted then
    `\${TMPDIR:-/tmp}/tst-``unit`-\$\$-\$RANDOM.```unit` is used.

`UMASK \[` `mask` \]
:   Run subsequent tests with
    [`umask`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/umask.html)(1)
    `mask`. If `mask` is omitted then the original `umask` is used.

`UNIT` `command` \[ `arg` ... \]
:   Define the command and optional default arguments to be tested.
    `UNIT` explicitly overrides the default command name derived from
    the test script file name.

`WIDTH` `width`
:   Set the output format width to approximately `width`.

# SEE ALSO

[`regress`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/regress.html)(1),
[`ksh`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/ksh.html)(1)

# IMPLEMENTATION

`version`
:   mktest (AT&T Labs Research) 2010-08-11

`author`
:   Glenn Fowler
    &lt;[glenn.s.fowler@gmail.com](https://web.archive.org/web/20141128030246/mailto:glenn.s.fowler@gmail.com)&gt;

`copyright`
:   Copyright © 2005-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030246/http://www.eclipse.org/org/documents/epl-v10.html)


