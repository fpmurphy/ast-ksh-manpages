# NAME

mamake - make abstract machine make

# SYNOPSIS

`mamake` \[ `options` \] \[ target ... \] \[ name=value ... \]

# DESCRIPTION

`mamake` reads `make abstract machine` target and prerequisite file
descriptions from a mamfile (see `-f`) and executes actions to update
targets that are older than their prerequisites. Mamfiles are generated
by the `--mam` option of
[`nmake`](/web/20150717115940/http://www2.research.att.com/~astopen/man/man1/nmake.html)(1)
and
[`gmake`](/web/20150717115940/http://www2.research.att.com/~astopen/man/man1/gmake.html)(1)
and are portable to environments that only have
[`sh`](/web/20150717115940/http://www2.research.att.com/~astopen/man/man1/sh.html)(1)
and
[`cc`](/web/20150717115940/http://www2.research.att.com/~astopen/man/man1/cc.html)(1).
In practice `mamake` is used to bootstrap build
[`nmake`](/web/20150717115940/http://www2.research.att.com/~astopen/man/man1/nmake.html)(1)
and
[`ksh`](/web/20150717115940/http://www2.research.att.com/~astopen/man/man1/ksh.html)(1)
in new environments. Mamfiles are used rather than old-`make`
makefiles because some features are not reliably supported across all
`make` variants:

`action execution`
:   Multi-line actions are executed as a unit by `\$SHELL`. There are
    some shell constructs that cannot be expressed in an
    old-`make` makefile.

`viewpathing`
:   `VPATH` is properly interpreted. This allows source to be separate
    from generated files.

`recursion`
:   Ordered subdirectory recursion over unrelated makefiles.

[`mamprobe`](/web/20150717115940/http://www2.research.att.com/~astopen/man/man1/mamprobe.html)(1)
is called to probe and generate system specific variable definitions.
The probe information is regenerated when it is older than the
`mamprobe` command.
For compatibility with
[`nmake`](/web/20150717115940/http://www2.research.att.com/~astopen/man/man1/nmake.html)(1)
the `-K` option and the `recurse` and `cc-\`` command line targets
are ignored.

# OPTIONS

-`e`
: Explain reason for triggering action. Ignored if -F is on.

-`f` `file`
:   Read `file` instead of the default. The default value is
    `Mamfile`.

-`i`
: Ignore action errors.

-`k`
: Continue after error with sibling prerequisites.

-`n`
: Print actions but do not execute. Recursion actions (see `-r`) are
    still executed. Use `-N` to disable recursion actions too.

-`r` `pattern`
:   Recursively make leaf directories matching `pattern`. Only leaf
    directories containing a makefile named `Nmakefile`,
    `nmakefile`, `Makefile` or `makefile` are considered. The
    first makefile found in each leaf directory is scanned for leaf
    directory prerequisites; the recusion order is determined by a
    topological sort of these prerequisites.

-`C` `directory`
:   Do all work in `directory`. All messages will mention `directory`.

-`D` `level`
:   Set the debug trace level to `level`. Higher levels produce
    more output.

-`F`
: Force all targets to be out of date.

-`K`
: Ignored.

-`N`
: Like `-n` but recursion actions (see `-r`) are also disabled.

-`V`
: Print the program version and exit.

-`G`, --`debug-symbols`
:   Compile and link with debugging symbol options enabled.

-`S`, --`strip-symbols`
:   Strip link-time static symbols from executables.

# SEE ALSO

[`gmake`](/web/20150717115940/http://www2.research.att.com/~astopen/man/man1/gmake.html)(1),
[`make`](/web/20150717115940/http://www2.research.att.com/~astopen/man/man1/make.html)(1),
[`mamprobe`](/web/20150717115940/http://www2.research.att.com/~astopen/man/man1/mamprobe.html)(1),
[`nmake`](/web/20150717115940/http://www2.research.att.com/~astopen/man/man1/nmake.html)(1),
[`sh`](/web/20150717115940/http://www2.research.att.com/~astopen/man/man1/sh.html)(1)

# IMPLEMENTATION

`version`
:   mamake (AT&T Research) 2011-08-31

`author`
:   Glenn Fowler

`copyright`
:   Copyright © 1999-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20150717115940/http://www.eclipse.org/org/documents/epl-v10.html)


