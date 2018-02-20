<!--
# Because Github doesn't properly support YAML headers
# vim:nu et tw=130 ts=8 sts=4 sw=4 ff=unix fo-=l fo+=tcroq2 fdm=marker fmr=@{,@} spell spelllang=en_gb
revision : Wed Nov 08, 2017 17:00:54
-->

# NAME

iffe - C compilation environment feature probe

# SYNOPSIS

```
iffe [ options ] [ - ] [ file.iffe | statement [ : statement ... ] ]
```

# DESCRIPTION

`iffe(1)` is a command interpreter that probes the C compilation environment for features. A feature is any file, option or
symbol that controls or is controlled by the C compiler. `iffe(1)` tests features by generating and compiling C programs and
observing the behaviour of the C compiler and generated programs.

`iffe(1)` interprets `iffe(5)` statements. These line-oriented statements may appear in the operand list with the `:` operand or
`newline` as the line delimiter. The standard input is read if there are no command line statements or if `file.iffe` is omitted.

Though similar in concept to `autoconf(1)` and `confi(1)` there are fundamental differences. The latter tend to generate global
headers accessed by all components in a package, whereas `iffe` is aimed at localized, self contained feature testing.

Output is generated in `FEATURE/test` by default, where `test` is the base name of `file.iffe` or the `iffe run` file operand.
Output is first generated in a temporary file; the output file is updated if it does not exist or if the temporary file is
different. If the first operand is `-` then the output is written to the standard output and no update checks are done.

Files with suffixes `.iffe` and `.iff` are assumed to contain `iffe(5)` statements.

# OPTIONS

-   `-a, --all`

    Define failed test macros `0`. By default only successful test macros are defined `1`.

-   `-c, --cc=C-compiler-name \[C-compiler-flags ...\]`

    Sets the C compiler name and flags to be used in the feature tests.

-   `-C, --config`

    Generate `config(1)` style `HAVE_` macro names. This implies `--undef`. Since `config(1)` has inconsistent naming conventions,
    the `exp` op may be needed to translate from the (consistent) `iffe` names. Unless otherwise noted a `config` macro name is
    the `iffe` macro name prefixed with `HAVE` and converted to upper case. `--config` is set by default if the command arguments
    contain a `run` op on an input file with the base name `config`.

-   `-d, --debug=level`

    Sets the debug level. Level 0 inhibits most error messages, level 1 shows compiler messages, and level 2 traces internal
    `iffe` `ksh(1)` actions and does not remove core dumps on exit.

-   `-D, --define`

    Successful test macro definitions are emitted. This is the default.

-   `-E, --explicit`

    Disable implicit test output.

-   `-F, --features=hdr`

    Sets the feature test header to `hdr`. This header typically defines `_SOURCE` feature test macros.
    The default value is `NONE`.

-   `-i, --input=file`

    Sets the input file name to `file`, which must contain `iffe` statements.

-   `-I, --include=dir`

    Adds `-Idir` to the C compiler flags.

-   `-L, --library=dir`

    Adds `-Ldir` to the C compiler flags.

-   `-n, --name-value`

    Output `name`=`value` assignments only.

-   `-N, --optimize`

    `--nooptimize` disables compiler optimization options. On by default; `-N` means `--nooptimize`.

-   `-o, --output=file`

    Sets the output file name to `file`.

-   `-O, --stdio=hdr`

    Sets the standard io header to `hdr`. The default value is `stdio.h`.

-   `-e, --package=name`

    Sets the `proto(1)` package name to `name`.

-   `-p, --prototyped`

    Emits `#pragma prototyped` at the top of the output file. See `proto(1)`.

-   `-P, --pragma=text`

    Emits `#pragma` `text` at the top of the output file.

-   `-r, --regress`

    Massage output for regression testing.

-   `-s, --shell=name`

    Sets the internal shell name to `name`.

    Used for debugging Bourne shell compatibility (otherwise `iffe` uses `ksh` constructs if available). The supported names are
    `ksh`, `bsh`, `bash` , and `osh`. `osh` forces the `read -r` compatibility read command to be compiled and used instead of
    `read -r`. The default is determined by probing the shell at startup.

-   `-S, --static=flags`

    Sets the C compiler flags that force static linking. If not set then `iffe` probes the compiler to determine the flags. `iffe`
    must use static linking (no dlls) because on some systems missing library symbols are only detected when referenced at runtime
    from dynamically linked executables.

-   `-u, --undef`

    `#undef` failed test macros. By default only successful test macros are defined `1`.

-   `-v, --verbose`

    Produce a message line on the standard error for each test as it is performed.

-   `-x, --cross=crosstype`

    Some tests compile an executable (`a.out`) and then run it. If the C compiler is a cross compiler and the executable format is
    incompatible with the execution environment then the generated executables must be run in a different environment, possibly on
    another host. `crosstype` is the HOSTTYPE for generated executables (the `package(1)` command generates a consistent HOSTTYPE
    namespace). Generated executables are run via `crossexec(1)` with `crosstype` as the first argument. `crossexec` supports
    remote execution for cross-compiled executables. See `crossexec(1)` for details.

-   `-X, --exclude=dir`

    Removes `-Idir` `-I/dir` C compiler flags.

-   `-?`

    Generate a usage synopsis.

-   `--man`

    Generate a formatted `man(1)` page for `iffe(1)`.

-   `--api`

    Generate an easy to parse usage message.

-   `--html`

    Generate a man page in HTML format.

-   `--nroff`

    Generate a man page in `nroff(1)` format.

-   `--syntax`

    Generate a formatted manpage for `iffe(5)` statements.

# SEE ALSO

`autoconf(1)`,
`config(1)`,
`crossexec(1)`,
`getconf(1)`,
`iffe(5)`,
`ksh(1)`,
`nmake(1)`,
`nroff(1)`,
`package(1)`,
`proto(1)`.

# IMPLEMENTATION

version
:   iffe (AT&T Research) 2012-06-08

author

copyright
:   Copyright © 1994-2012 AT&T Intellectual Property

license
:   <http://www.eclipse.org/org/documents/epl-v10.html>

