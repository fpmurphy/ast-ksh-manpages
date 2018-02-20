# NAME

regress - run regression tests

# SYNOPSIS

`regress` \[ `options` \] unit \[ command \[ arg ... \] \]

# DESCRIPTION

`regress` runs the tests in `unit`, or `unit``.tst` if `unit` does
not exist. If `command` is omitted then it is assumed to be the base
name of `unit`. All testing is done in the temporary directory
`unit``.tmp`.
Default test output lists the `number` and `description` for each active
`TEST` group and the `number`:`line` for each individual `EXEC`
test. Each test that fails results in a diagnostic that contains the
word `FAILED`; no other diagnostics contain this word.

# OPTIONS

-`b`, --`ignore-space`
:   Ignore space differences when comparing expected output.

-`i`, --`pipe-input`
:   Repeat each test with the standard input redirected through a pipe.

-`k`, --`keep`
:   Enable `core` dumps, exit after the first test that fails, and do
    not remove the temporary directory `unit``.tmp`.

-`l`, --`local-fs`
:   Force `unit``.tmp` to be in a local filesystem.

-`o`, --`pipe-output`
:   Repeat each test with the standard output redirected through a pipe.

-`p`, --`pipe-io`
:   Repeat each test with the standard input and standard output
    redirected through pipes.

-`q`, --`quiet`
:   Output information on `FAILED` tests only.

-`r`, --`regular`
:   Run each test with the standard input and standard output redirected
    through regular files. On by default; -`r` means --`noregular`.

-`t`, --`test`=`pattern`
:   Run only tests matching `pattern`. Tests are numbered and consist of
    at least two digits (0 filled if necessary.) Tests matching `+(0)`
    are always run.

-`x`, --`trace`
:   Enable debug tracing.

-`v`, --`verbose`
:   List differences between actual (&lt;) and expected (&gt;) output,
    errors and exit codes. Also disable long output line truncation.

# INPUT FILES

The regression test file `unit``.tst` is a
[`ksh`](/web/20141128030249/http://www2.research.att.com/~astopen/man/man1/ksh.html)(1)
script that is executed in an environment with the following functions
defined:

`BODY` { ... }
:   Defines the test body; used for complex tests.

`CD` `directory`
:   Create and change to working directory for one test.

`CLEANUP` `status`
:   Called at exit time to remove the temporary directory `unit`
    `.tmp`, list the tests totals via `TALLY`, and exit with status
    `status`.

`COMMAND` `arg` ...
:   Runs the current command under test with `arg` ... appended to the
    default args.

`CONTINUE`
:   The background job must be running.

`COPY` `from to`
:   Copy file `from` to `to`. `from` may be a regular file or `INPUT`,
    `OUTPUT` or `ERROR`. Post test comparisons are still done for
    `from`.

`DIAGNOSTICS` \[ `1` | `0` | `pattern` \]
:   No argument or an argument of `1` declares that diagnostics are to
    expected for the remainder of the current `TEST`; `0` reverts to
    the default state that diagnostics are not expected; otherwise the
    argument is a
    [`ksh`](/web/20141128030249/http://www2.research.att.com/~astopen/man/man1/ksh.html)(1)
    pattern that must match the non-empty contents of the
    standard error.

`DO` `statement`
:   Defines additional statements to be executed for the current test.
    `statement` may be a { ... } group.

`EMPTY` INPUT|OUTPUT|ERROR|SAME
:   The corresponding file is expected to be empty.

`ERROR` \[ `-e` `filter` \] \[ `-n` \] `file` | - `data` ...
:   The standard error is expected to match either the contents of
    `file` or the line `data`. `ERROR -n` does not append a newline to
    `data`. `filter` is a shell command or pipeline that reads standard
    input and writes standard output that is applied to ERROR before
    comparison with the expected contents.

`EXEC` \[ `arg` ... \]
:   Runs the command under test with optional arguments. `INPUT` ,
    `OUTPUT`, `ERROR`, `EXIT` and `SAME` calls following this
    `EXEC` up until the next `EXEC` or the end of the script provide
    details for the expected results. If no arguments are specified then
    the arguments from the previious `EXEC` in the current `TEST`
    group are used, or no arguments if this is the first `EXEC` in
    the group.

`EXIT` `status`
:   The command exit status is expected to match the pattern `status`.

`EXITED`
:   The background job must have exited.

`EXPORT` \[-\] `name`=`value` ...
:   Export environment variables for one test.

`FATAL` `message` ...
:   `message` is printed on the standard error and `regress` exits
    with status `1`.

`FIFO` INPUT|OUTPUT|ERROR `\[` -n `\]` `file` | - `data` ...
:   The `IOB file is a fifo.`

`IF` `command` \[`note`\]
:   If the
    [`sh`](/web/20141128030249/http://www2.research.att.com/~astopen/man/man1/sh.html)(1)
    `command` exits 0 then tests until the next `ELIF`, `ELSE` or
    `FI` are enabled. Otherwise those tests are skipped. `IF` ...
    `FI` may be nested, but must not cross `TEST` boundaries. `note`
    is listed on the standard error if the correspoding test block is
    enabled; `IF`, `ELIF`, `ELSE` may nave a `note` operand.

`IGNORE` `file` ...
:   `file` is ignored for subsequent result comparisons. `file` may be
    `OUTPUT` or `ERROR`.

`IGNORESPACE`
:   Ignore space differences when comparing expected output.

`INCLUDE` `file` ...
:   One or more `file` operands are read via the
    [`ksh`](/web/20141128030249/http://www2.research.att.com/~astopen/man/man1/ksh.html)(1)
    [`.`](/web/20141128030249/http://www2.research.att.com/~astopen/man/man1/..html)(1) command.
    `VIEW` is used to locate the files.

`INFO` `description`
:   `description` is printed on the standard error.

`INITIALIZE`
:   Called by `regress` to initialize a each `TEST` group.

`INPUT` \[ `-e` `filter` \] \[ `-n` \] `file` | - `data` ...
:   The standard input is set to either the contents of `file` or the
    line `data`. `INPUT -n` does not append a newline to `data`.
    `filter` is a shell command or pipeline that reads standard input
    and writes standard output that is applied to OUTPUT before
    comparison with the expected contents.

`INTRO`
:   Called by `regress` to introduce all `TEST` groups.

`IO` \[ `FIFO` | `PIPE` \] `INPUT|OUTPUT|ERROR` \[ `-e` `filter` \] \[ `-n` \] `file` | - `data` ...
:   Internal support for the `INPUT`, `OUTPUT` and
    `ERROR` functions.

`JOB` `op` \[ ... \]
:   Like `EXEC` except the command is run as a background job for the
    duration of the group or until it is killed via `KILL`.

`KEEP` `pattern` ...
:   The temporary directory is cleared for each test. Files matching
    `pattern` are retained between tests.

`KILL` \[ `signal` \]
:   Kill the background job with `signal` \[ `SIGKILL` \].

`MOVE` `from to`
:   Rename file `from` to `to`. `from` may be a regular file or
    `INPUT`, `OUTPUT` or `ERROR`. Post test comparisons are
    ignored for `from`.

`NOTE` `comment`
:   `comment` is added to the current test trace output.

`OUTPUT` \[ `-e` `filter` \] \[ `-n` \] `file` | - `data` ...
:   The standard output is expected to match either the contents of
    `file` or the line `data`. `OUTPUT -n` does not append a newline
    to `data`. `filter` is a shell command or pipeline that reads
    standard input and writes standard output that is applied to ERROR
    before comparison with the expected contents.

`PIPE` INPUT|OUTPUT|ERROR `\[` -n `\]` `file` | - `data` ...
:   The `IOB file is a pipe.`

`PROG` `command` \[ `arg` ... \]
:   `command` is run with optional arguments.

`REMOVE` `file` ...
:   `file` ... are removed after the current test is done.

`RUN`
: Called by `regress` to run the current test.

`SAME` `new old`
:   `new` is expected to be the same as `old` after the current
    test completes.

`SET` \[`no`\]`name`\[=`value`\]
:   Set the command line option --`name`. The setting is in effect for
    all tests until the next explicit `SET`.

`TALLY`
:   Called by `regress` display the `TEST` results.

`TEST` `number` \[ `description` ... \]
:   Define a new test group labelled `number` with optional
    `descripion`.

`TITLE` \[+\] `text`
:   Set the `TEST` output title to `text`. If `+` is specified then
    `text` is appended to the default title. The default title is the
    test file base name, and, if different from the test file base name,
    the test unit base name.

`TWD` \[ `dir` ... \]
:   Set the temporary test dir to `dir`. The default is `unit` `.tmp`,
    where `unit` is the test input file sans directory and suffix. If
    `dir` matches `/\`` then it is the directory name; if `dir` is
    non-null then the prefix `\${TMPDIR:-/tmp}` is added; otherwise if
    `dir` is omitted then
    `\${TMPDIR:-/tmp}/tst-``unit`-\$\$-\$RANDOM.```unit` is used.

`UMASK` \[ `mask` \]
:   Run subsequent tests with
    [`umask`](/web/20141128030249/http://www2.research.att.com/~astopen/man/man1/umask.html)(1)
    `mask`. If `mask` is omitted then the original `umask` is used.

`UNIT` `command` \[ `arg` ... \]
:   Define the command and optional default arguments to be tested.
    `UNIT` explicitly overrides the default command name derived from
    the test script file name. A `command` operand with optional
    arguments overrides the `UNIT` `command` and arguments, with the
    exception that if the `UNIT` `command` is `-` or `+` the
    `UNIT` arguments are appended to the operand or default unit
    command and arguments.

`VIEW` `var` \[ `file` \]
:   `var` is set to the full pathname of `var` \[ `file` \] in the
    current `\$VPATH` view if defined.

# SEE ALSO

[`nmake`](/web/20141128030249/http://www2.research.att.com/~astopen/man/man1/nmake.html)(1),
[`ksh`](/web/20141128030249/http://www2.research.att.com/~astopen/man/man1/ksh.html)(1)

# IMPLEMENTATION

`version`
:   regress (AT&T Research) 2012-02-02

`author`
:   Glenn Fowler

`copyright`
:   Copyright © 1995-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030249/http://www.eclipse.org/org/documents/epl-v10.html)


