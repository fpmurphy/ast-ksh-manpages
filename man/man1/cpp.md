# NAME

cpp - standalone C preprocessor

# SYNOPSIS

`/lib/cpp \[` option ... `\] \[` ifile `\[` ofile `\] \]`

# DESCRIPTION

`cpp` is the standalone preprocessor that is automatically invoked by
the
[`cc`](/web/20141128030241/http://www2.research.att.com/~astopen/man/man1/cc.html)(1)
command. Although primarily intended for the `C` language, there are
several options that support preprocessing of other languages.

`cpp` accepts two optional file name arguments. `ifile` and `ofile` are
respectively the input and output for the preprocessor, defaulting to
standard input and standard output if not specified. `WARNING:` this
is a non-standard file argument syntax that is required by some C
compiler implementations.

## Dialects

`cpp` preprocesses one of two dialects. Each of them has three modes -
`strict` , `transition` , and `C++` :

`ansi`
: The default dialect `ansi` provides a conforming implementation,
    with extensions, of the preprocessing translation stages defined in
    the ANSI C standard. Refer to this document for detailed
    descriptions. The macro `\_\_STDC\_\_` is predefined in
    this dialect.

`compatibility`
:   This dialect provides almost complete compatibility with the old
    (Reiser) `cpp`. Non-supported features of old `cpp` appear in the
    diagnostics when possible. The macro `\_\_STDC\_\_` is not
    predefined in this dialect. Refer to the `Compatibility` section
    below for a description of differences between this and the
    `ansi` dialect.

The dialects may have a strict interpretation, controlled by the
`-D-S` option. When the `strict` mode is in effect, warning
diagnostics are issued when dialect extensions are used in
`non-hosted` files (see the `-I-H` option below).

The macro `\_\_STDPP\_\_` is predefined to be 1 in all dialects.

## Options

The options are processed in order from left to right. Options issuing
directives are executed after `"pp\_default.h"` is read. The options
are:

`-A``arg`
:   SVR4 assertion. `arg` is the name of assertion. This option is
    equivalent to the directive `\#assert` `arg`.

`-C`
: Do not strip comments from the input files.

`-D``arg`
:   Additional `cpp` options accepted by most versions of
    [`cc`](/web/20141128030241/http://www2.research.att.com/~astopen/man/man1/cc.html)(1).
    `arg` may be:

    `-C`
    : Preprocess the `compatibility` dialect.\

    `-D``level`
    : \
        Set the debug trace level to `level`. See the `pp:debug`
        pragma below.

    `-F``filename`
    : \
        Change the name of the input file reported in the line control
        information to `filename`.

    `-H`
    : Mark all files `hosted`. See the `-I-H` option below.\

    `-L`\[`line-directive`\]
    : \
        Change the directive name for line number control output
        directives to `line-directive`. The line number control output
        directives are of the form `\#``line-directive line "file"`.
        The defaults are `line` if `line-directive` is omitted, and
        null if the `-D-L` option is omitted.

    `-M`
    : Mark all files to be included only once. See the `allmultiple`
        and `multiple` pragmas below.\

    `-P`
    : Enable the `passthrough` mode. Specifies the passthrough mode,
        especially useful for preprocessing other languages (e.g.,
        [`nmake`](/web/20141128030241/http://www2.research.att.com/~astopen/man/man1/nmake.html)(1)).
        This option is not suitable for `C` language processing. In
        this mode:

        ·
        : comments are removed\

        ·
        : space characters are preserved on output\

        ·
        : `\#(...)` results are not enclosed in " "\

        ·
        : `\\` escapes the special meaning of " and '\

        ·
        : `\\newline` is removed only in directives\

        ·
        : " and ' constants may contain `newline`s

        \

    `-Q`
    : Produce a checkpoint dump of `ifile` in `ofile`. A checkpoint
        dump file requires no preprocessing; it contains a fully
        preprocessed text section followed by a dump of the macro
        definitions. Checkpoint dump files may be subject to
        `\#include` directives just as normal text files. Performance
        will most likely be improved for source files that reference
        large collections of common, stable header files.

    `-R`
    : Preprocess for `transition` mode.

    `-S`
    : Provide a strict dialect interpretation. See the `pp:strict`
        pragma below.

    `-T``test`
    : \
        Enable the internal debugging test `test`. `test` may be `1`,
        `2` or `3` (both 1 and 2). A diagnostic indicating the
        behavior of selected tests is issued.

    `-W`
    : Produce additional compatibility diagnostics relating to the
        current dialect.

    `-X``probe`
    : \
        Set the default definition probe key to `probe`. In the absence
        of `pp\_default.h` `probe` is used to generate the information
        using
        [`probe`](/web/20141128030241/http://www2.research.att.com/~astopen/man/man1/probe.html)(1).

    `-+`
    : Preprocess for the `C++` language. See the `pp:plusplus`
        pragma below.

    `+``option`
    : \
        Invert the sense of the corresponding `-``option` from above.

    :`option`\[=`value`\]
    : \
        Equivalent to the directive `\#pragma pp:``option value`.

    `%``directive`
    : \
        Enters the preprocessing directive `directive` from the
        command line.

    \#`predicate`(\[`args`\])
    : \
        Equivalent to the directive `\#define`
        \#`predicate`(\[`args`\]).

    `name`\[=`value`\]
    : \
        Equivalent to the directive `\#define` `name value`. `value`
        defaults to `1` if omitted.

    \

`-E`
: No effect. Provides compatibility with some versions of
    [`cc`](/web/20141128030241/http://www2.research.att.com/~astopen/man/man1/cc.html)(1).

`-H`
: Print the included reference files in `stderr`. This is for System
    V compatibility.

`-I``arg`
:   Include file related options. `arg` may be:

    `-`
    : Cause " " include files to be searched for in all `-I`
        directories and &lt; &gt; include files to be searched for only
        in the `-I` directories listed after `-I-`. The standard
        include directory is always searched last for both include file
        forms. This allows the `directory of the including file` (see
        the `-I``dir` option below) to be replaced by a list of
        directories for " " include files. To first search for " "
        include files in the directory of `ifile` specify `-I`
        `directory(ifile)` `-I-` `...,` where `directory(ifile)` is
        the directory portion of the `ifile` file name.
        `(See Makerules(1) for directory prefix of include files in
        Scan Rule)`.\

    `-C`
    : This is for C++. Any `-I``dir` after `-I-C` will be marked
        as C source. This is equivalent to `pp:cdir` pragma below.\

    `-D`\[`file`\]
    : \
        Use the default definitions from `file` rather than
        `pp\_default.h`. If `file` is omitted then no default
        definitions file is read. `file` is read using the `-I-R`
        mechanism described below.

    `-H`\[`directory`\]
    : \
        Include files found in `-I` directories listed after `-I-H`
        are marked `hosted`. If `directory` is specified then all
        `-I` directories, including `directory` itself, listed after
        `-I``directory` are marked hosted. Most warning diagnostics
        are relaxed for `hosted` files. Files found in the standard
        include file directory (`-I-S` below) are marked `hosted` by
        default. If `-D-H` (`-D+H`) is specified then all files are
        marked `hosted` (`non-hosted`) regardless of the
        `-I-H` option.

    `-I``directory`
    : \
        Initialization files, (e.g., `pp\_default.h, -I-R ),` are
        searched for in `directory` before the default standard
        include directory.

    `-I`\[`file` | -`char suffix`\]
    : \
        Ignore `"..."` quoted `\#include` file names listed in file
        `file`, or, if `-``char suffix` is specified, the file named
        by either changing characters following `char` in the input file
        base name to `suffix` or appending `char suffix` to the input
        file name if it does not contain `char`. `\#include` on any of
        the listed files will be ignored. Only the last `-I-I` option
        takes effect. If `file` is omitted then the option is ignored.

    `-R``file`
    : \
        Read the contents of `file` using `\#include` "`file`". `file`
        and all files included by `file` are marked `hosted` even if
        `-D+H` is specified. Line sync output is also disabled for
        these files.

    `-S``dir`
    : \
        Set the standard include file directory to `dir`. This directory
        is the last place searched for all include file forms. The
        default standard include file directory is `/usr/include`.
        Only one standard include directory may be specified.

    `-T``file`
    : \
        Read the contents of `file` before the input file. The output of
        `file` from `cpp` is used in the input file.

    `+``option`
    : \
        Invert the sense of the corresponding -`option` from above

    `dir`
    : " " include files not beginning with `/` are first searched
        for in the directory of the including file, then in the
        directories named in `-I` options and finally the standard
        directory. &lt; &gt; include files use the same search order as
        " " files except that &lt; &gt; files are not searched for in
        the directory of the including file. The `directory of the
        including file` can be replaced by a possibly empty list of
        directories using the `-I-` option described above. (NOTE:
        `dir` cannot start with the `-` character.)

    \

`-M`
: Output the file dependencies in makefile assertion format. This is
    for BSD compatibility.

`-P`
: Preprocess without producing line control information.

`-T`
: Truncate macro names for compatibility with non-flexname
    (8 character) compilation systems. This is equivalent to
    `pp:truncate` pragma below.

`-U``name`
:   Equivalent to the directive `\#undef` `name`.

`-V`
: Prints the `cpp` version in `stderr`.

`-X``dialect`
:   Set the System V standard preprocessing dialect to `dialect`.
    `dialect` may be one of:

    `a`
    : The default `ansi` dialect.\

    `\[Ac\]`
    : The `ansi` strict mode (ANSI conforming). `-D-S` is
        preferred.\

    `F`
    : The C++ mode.\

    `f`
    : The `compatibility` transition and C++ mode.\

    `\[ks\]`
    : The `compatibility` strict mode.\

    `o`
    : The old `cpp`.\

    `t`
    : The `compatibility` transition mode. `-D-C` is preferred.

    \

    The following table summarizes the mode(s) that each `dialect`
    represents:\
    \

    .nf
    .nr
                      \#\~
    .ds
    .fc
    .nr
                      33
    \
    \

    \

`-Y``dir`
:   Set the standard include file directory to `dir`. `-I-S``dir`
    is preferred.

## Directives

`cpp` directives are a single line (after all `\\newline` sequences
have been removed) starting with `\#` as the first non-space character
on the line. A space character is any one of `space`, `tab`,
`vertical-tab` or `formfeed`. `vertical-tab` and `formfeed` are
not valid between the initial `\#` and the terminating `newline`.
Any number of `space` and `tab` characters may appear between the
initial `\#` and the directive name. All tokens in directives are
significant; trailing tokens, sometimes used as commentary in other
implementations, must be enclosed in `/\` ... \`/`. The `\#include`,
`\#if`, `\#ifdef`, `\#ifndef` and `\#macdef` directives can be
nested, although the nesting levels must balance within files. In the
following an `identifier` matches the regular expression
`\[a-zA-Z\_\]\[a-zA-Z\_0-9\]\`` and must not be immediately preceded
by `\[0-9\]`.
The directives are:

`\#define` `name` `` `token-string`
\
Replace subsequent instances of `name` with `token-string`.
`\#define` `name(arg``, ...,` `arg) token-string`
\
Replace subsequent instances of `name` followed by a `(`, a list of
comma-separated set of tokens, and a `)` by `token-string`, where each
occurrence of an `arg` in the `token-string` is replaced by the expanded
value of the corresponding set of tokens in the comma-separated list.
The argument replaced `token-string` is then re-scanned for further
macro replacement. Notice that there can be no space between `name` and
`(` in the definition. Formal arguments appearing in single or double
quoted strings are replaced by the corresponding unexpanded actual
argument text only in the `compatibility` dialect. Macro recursion is
inhibited by not expanding a macro name appearing in its own definition.

If the last formal argument is followed by the `...` token then it is
replaced by the expanded value of all remaining actual arguments and
intervening `,` tokens from the macro call. If there is only one
formal argument then the macro may be called with no actual arguments,
otherwise there must be at least one actual argument for the last formal
argument.

The token `\#` in `token-string` causes the immediately following
formal argument to be replaced by the unexpanded value of the
corresponding actual argument enclosed in double quotes. The token
`\#\#` in `token-string` concatenates the space separated tokens
immediately preceding and following the `\#\#` token. The resulting
token is not checked for further macro expansions. Formal arguments
preceding `\#\#` or following `\#\#` and `\#` are replaced by the
unexpanded value of the corresponding actual argument.

\
`\#define` `\#predicate``(``argument``)`
\
Makes the assertion \#`predicate`(`argument`) that may be tested only in
`\#if` or `\#elif` directive expressions. `predicate` must be an
identifier and `argument` may be any balanced parenthesis sequence of
tokens not containing `newline`. The assertion in no way conflicts
with the `\#define` macro name space. Space character sequences in
`argument` are canonicalized into single `space` characters and macro
expansion is inhibited on both `predicate` and `argument` during
predicate assertion and evaluation. Within `\#if` expressions,
`\#predicate(argument)` evaluates to 1 if `\#define`
`\#predicate``(``argument``)` has been specified; otherwise it
evaluates to 0. Likewise, `\#predicate( )` evaluates to 1 if any
assertion has been made on `predicate`. Multiple assertions on
`predicate` are allowed, with all such assertions evaluating to 1 in
`\#if` expressions.
`\#macdef` `name...`
\
Defines the multi-line macro `name`. A matching `\#endmac` ends the
definition. Nesting is allowed. As with `\#define`, `name` may have
arguments. The definition body may contain directives; these directives
are not executed until the macro is expanded.
`\#elif` `constant-expression`
\
Allows multiple alternate branches for the `\#if` directive.
`constant-expression` evaluation is the same as for `\#if`.
`\#else`
\
Reverses the sense of the test directive matching this directive. If
lines previous to this directive are ignored then the following lines
will appear in the output.
`\#endif`
\
Ends a section of lines begun by a test directive (`\#if`,
`\#ifdef`, or `\#ifndef`). Each test directive must have a matching
`\#endif`.
`\#error` \[`message`\]
\
Emits `message` as a `cpp` error diagnostic and terminates preprocessing
immediately. The default `message` is `user error`.
`\#if` `constant-expression`
\
Subsequent lines will appear in the output if and only if
`constant-expression` evaluates to non-zero. All non-assignment C
operators are valid in `constant-expression`. Operator precedence is the
same as in the C language. Computations are done using `long int` and
`unsigned long int` arithmetic on the host machine; floating point
computations are not supported. Any macros in `constant-expression` are
expanded before the expression is evaluated. The builtin predicate
`defined(``name``)` tests if the macro name `name` has been defined.
The builtin predicate `exists(``file``)` tests if `file` can be
found using `\#include` search rules. `file` must be enclosed in " "
or &lt; &gt;. `exists` accepts additional optional quoted string
arguments that are `:` separated lists of directories to search for
the existence of `file`. The normal `\#include` search rules are
overridden in this case. The builtin predicate
`strcmp(``token1,token2``)` compares the macro expanded string
values of `token1` and `token2` using the
[`strcmp`](/web/20141128030241/http://www2.research.att.com/~astopen/man/man3/strcmp.html)(3)
library function. Only these operators, functions, predicates, integer
constants and names may be used in `constant-expression`. In particular,
the `sizeof` and `,` (comma) operators are not valid in this
context.
`\#ifdef` `name`
\
The lines following will appear in the output if `name` has been the
subject of a previous `\#define` without being the subject of an
intervening `\#undef`.
`\#ifndef` `name`
\
The lines following will not appear in the output if `name` has been the
subject of a previous `\#define` without being the subject of an
intervening `\#undef`.
`\#include` `&lt;filename&gt;`
\
The standard include directories (see the `-I` option above) are
searched for a header identified uniquely by `filename`, and the
directive is replaced by the entire contents of the header. If the
`allmultiple` pragma is off then subsequent `\#include` references
to the header named by `filename` are ignored unless the header contains
a `\#pragma multiple` directive that was processed during the first
inclusion of the header. Any macros on the directive line are first
expanded before the directive is processed.
`\#include` `"filename"`
\
The directory of the including file (see the `-I` option above) is
searched for a source file identified uniquely by `filename`, and the
directive is replaced by the entire contents of the source file. If the
`allmultiple` pragma is off then subsequent `\#include` references
to the source file named by `filename` are ignored unless the source
file contains a `\#pragma multiple` directive that was processed
during the first inclusion of the source file. Any macros on the
directive line are first expanded before the directive is processed. If
the source file search fails then the directive is reprocessed as if it
were `\#include` `&lt;filename&gt;.`
`\#let` `identifier` = `constant-expression`
\
Defines the macro `identifier` to be the value of the evaluated
`constant-expression`, where `constant-expression` is the same as for
the `\#if` directive. Macro redefinition diagnostics are suppressed
for macros defined by `\#let`.
`\#line` `integer-constant` \[`"filename"`\]
\
Outputs line control information for the next pass. `integer-constant`
is the line number of the next line and `filename` is the originating
file. The current file name is set to `filename` if specified. Any
macros on the directive line are first expanded before the directive is
processed.
`\#pragma` \[`pass`:\]\[`no`\]`option` \[`args` ...\]
\
Sets preprocessor and compiler control options. Use of `\#pragma`
should be limited to `hosted` files as the interpretation varies
between compiler implementations. A warning diagnostic is issued when
`\#pragma` directive is encountered in a `non-hosted` file. This
directive is completely ignored for `non-hosted` files in the `strict
ansi` dialect. If `pass` is `pp` then the option is used and verified
and is not passed on, else if `pass` is omitted then the option is used
and passed on, otherwise the option is passed on and not used.
`\#pragma` arguments are not checked for macro expansions. If `no`
is present then `option` is turned off. Pass specific pragmas should not
omit `pass:`. Options specified on the command line override options in
the default include file. The `cpp` specific options are:

`allmultiple`
:   Marks all include files `multiple`. This is the default.

`builtin`
:   Sets a mode that marks all macros defined by `\#define` `builtin`.
    `builtin` macro definitions are not dumped by the `-D-Q` option.

`cdir`
: Marks include files after this pragma as C source. This is for C++.\

`compatibility`
:   Sets the `compatibility` dialect.

`debug` `number`
:   Sets the debug trace level to `number`. Higher levels produce more
    output. Debug tracing is enabled only in debugging versions of
    the preprocessor.

`elseif`
:   Allows `\#else if`, `\#else ifdef`, and `\#else
    ifndef` directives.

`hostdir` "`dir`"
:   Include files found in `dir` or after `dir` in the `-I` directory
    list are marked hosted.

`id` "`string`"
:   Adds the characters in `string` to the set of characters that may
    appear within an identifier name. For example, `\#pragma pp:id
    "\$"` causes `sys\$call` to be tokenized as a single identifier.
    `string` is currently limited to "`\$`". Once added a character
    cannot be deleted from the identifier set.

`include` "`dir`"
:   Equivalent to the `-I``dir` command line option.

`linetype`
:   Specifies that line number control output directives are to contain
    an additional include file type argument. The line number control
    output directives are of the form `\#``line-directive line "file"
    type` where `line-directive` is set by the `-D-L` option (null by
    default), and `type` is `1` for include file push, `2` for
    include file pop and null otherwise.

`load`
: Specifies that lines following this directive were produced by a
    `-D-Q` checkpoint dump. This option should not be used
    explicitly.\

`macref` `name type`
:   Specifies that macro reference pragmas are to be emitted. `name` is
    the macro name and `type` is `-2` for `undef`, `-1` for a
    reference in `\#if`, `\#ifdef` or `\#ifndef`, `0` for macro
    expansion and `&gt;0` (number of lines in the definition) for
    macro definition.

`map` \[`id ...`\] "/`from`/\[,/`to`/\]" \[ "/`old`/`new`/\[`glnu`\]" ... \]
:   `map` allows unknown directives and `pragma` options to be
    mapped to other directives and rescanned. The optional `id`'s
    support the mapping of standard directives and options as well. In
    this case the standard directives and options may be accessed by
    `\_\_id\_\_`.

Each unknown directive line is space canonicalized and placed in a
buffer that is subject to `pp:map` editing. This buffer contains the
initial `\#` and omits the trailing `newline`. `from` is an
[`egrep`](/web/20141128030241/http://www2.research.att.com/~astopen/man/man1/egrep.html)(1)
style regular expression, with the addition of the identifier delimiter
operators `&lt;` and `&gt;`, and the proviso that `\^` and `\$`
match the beginning and end of string (rather than line). The
expressions are delimited by `/` in the example, but any character may
be used, as long as it is escaped within the expressions. The maps are
searched, last in first out, for the longest `from` pattern that matches
the unknown directive buffer. The
[`ed`](/web/20141128030241/http://www2.research.att.com/~astopen/man/man1/ed.html)(1)
style substitute expressions for the longest `from` match are then
applied left to right. The optional `g` substitutes all occurrences of
`old` to `new`. `l` (`u`) converts `new` to lower (upper) case.
`n` specifies that the substitute expression is to be applied only if
all previous substitute expressions failed. The standard C escape
sequences are recognized in all map patterns. In particular, ``\\n
translates to `newline`, allowing a single directive line to be mapped
into many lines. After all substitutions have been applied the resulting
buffer is pushed back onto the input token stream and rescanned. The
original directive line number is preserved during the rescan.

If any of the mapped lines start with `\#\#` then the text between
`\#\#` and the next `newline` is copied verbatim to the output. If
the resulting buffer is empty then the input directive is ignored.

If `to` is also specified then the nested construct `from` to `to` is
matched.

For example,

    #pragma pp:map "/#(pragma )?ident>/"

causes `\#pragma ident ...` and `\#ident ...` directives to be
silently ignored and

    #pragma pp:map "/#pragma lint:/" ",#pragma lint:(.`),##/`\1`/,u"

maps `\#pragma lint:argsused` to `/\`ARGSUSED\`/` on output.

`multiple`
:   If the `allmultiple` option is on then the `\#include` directive
    ensures that each header and source file is included at most one
    time. A `\#pragma multiple` directive, when processed during the
    first inclusion of the header (source file), causes all subsequent
    `\#include` directives on that header (source file) to re-read the
    contents of the header (source file).

`pluscomment`
:   Enable C++ comments.

`plusplus`
:   Preprocess for C++. See `Additional Processing` below.

`predefined`
:   Macroes defined after this pragma are marked as predefined.

`prototyped`
:   Input source files that set the `prototyped` option will be
    filtered using the
    [`proto`](/web/20141128030241/http://www2.research.att.com/~astopen/man/man1/proto.html)(1) transformations.

`readonly`
:   Sets a mode that marks all macros defined by `\#define` or
    undefined by `\#undef` `readonly`. A `readonly` macro cannot be
    redefined by either `\#define` or `\#undef`.

`reserved` `name`\[=`value`\] ...
:   The `name` arguments are marked as reserved keywords. `value`
    optionally specifies the keyword lexical value. This option is used
    when compiler front ends are linked directly with the preprocessor.
    The \`\`classic'' C and C++ keywords have predefined lexical values,
    as do `asm`, `const`, `enum`, `signed`, `void` and
    `volatile`. If `value` is omitted for a keyword that has no
    predefined lexical value then `NOISE` is assumed. `value` may be
    one of:

    `GROUP`
    : \
        A group noise token that may be followed by zero or one balanced
        `( . . . )` groups and zero or one balanced `{ . . . }`
        groups (e.g., `asm`).

    `LINE`
    : A line noise token terminated by the next `newline`.\

    `NOISE`
    : \
        A noise token to be ignored (e.g., `near`).

    `STATEMENT`
    : \
        A statement noise token terminated by the next semicolon.

    \

`spaceout`
:   In the `ansi` dialect for the standalone `cpp` `spaceout` causes
    input spacing to be copied to the output. The default for the
    `ansi` dialect is to place a single space between each output
    token. This mode is required by some `asm` implementations that
    allow the assembly text to be preprocessed.

`splicecat`
:   `\\newline` line splicing may be used to concatenate tokens in
    macros definition.

`standard` "`dir"`
:   Names `dir` as the standard include directory.

`strict`
:   Set the strict interpretation mode.

`stringspan`
:   Allow \\`newline` line in strings.

`text`
: `notext` suppresses output to `ofile` generated by input text.
    This allows files to be scanned for `cpp` directives without
    generating any text output. Note that the `-P` option must still
    be used to suppress line number information output.

`transition`
:   Sets transition mode.

`truncate`
:   Truncate macro names for compatibility with non-flexname (8
    characters) compilation systems.

`version`
:   Outputs both `\#pragma pp:version` `version-string` and `\#pragma
    version`, allowing later passes to emit similar version pragmas.

`warn`
: Produce warnings about extensions used in non-hosted files in the
    strict dialect.

\
`\#rename` `oldname newname`
\
Changes the name of the macro `oldname` to `newname`.
`\#undef` `name`
\
Remove the definition of the macro `name` (if any).
`\#undef` `\#predicate(argument)`
\
`\#undef` `\#predicate( )`
\
The first form removes the assertion of `predicate(argument)`, if any,
while the second form removes all assertions on `predicate`.
`\#warning` \[`message`\]
\
Emits `message` as a `cpp` warning diagnostic and continues normal
processing. The default `message` is `user warning`.

## Builtin Macro

The builtin macro `\#(``\[op\] identifier``...``)` provides access
to preprocess time symbols and definitions. The value of this macro is
enclosed in " " unless otherwise noted. Just as with the `\#` and
`\#\#` operators, any macro formal arguments appearing within
`\#(...)` in a macro definition are copied without expansion on macro
invocation. `arg` may be one of the following:

`FILE`
: The current file name. `\_\_FILE\_\_` is defined to be
    `\#(FILE)` for ANSI conformance.

`LINE`
: The current line number (not quoted). `\_\_LINE\_\_` is defined to
    be `\#(LINE)` for ANSI conformance.

`DATE`
: The current month, day and year `(``MMM DD YYYY``).`
    `\_\_DATE\_\_` is defined to be `\#(DATE)` for ANSI conformance.

`TIME`
: The current time `(``HH:MM:SS``).` `\_\_TIME\_\_` is defined to
    be `\#(TIME)` for ANSI conformance.

`BASE`
: The base name of `FILE`.

`PATH`
: The full path name of the most recent `\#include` directive or
    `exists` predicate evaluation. `\_\_PATH\_\_` is defined to be
    `\#(PATH)` in deference to ANSI conformance.

`VERSION`
:   The `cpp` version stamp. `\_\_VERSION\_\_` is defined to be
    `\#(VERSION)` in deference to ANSI conformance.

`ARGC`
: The number of arguments of a variable arguments macro.
    `\_\_ARGC\_\_` is defined to be `\#(ARGC)` for ANSI conformance.

`getenv``name`
:   The value of `name` as returned by the
    [`getenv`](/web/20141128030241/http://www2.research.att.com/~astopen/man/man3/getenv.html)(3)
    library call.

`getmac``name`
:   The definition of the preprocessor macro `name`. Notice that macro
    formal names appearing in macro definitions are replaced by internal
    format token sequences.

`getopt``option`
:   The setting for the option or pragma `option`.

`getprd``predicate`
:   The argument associated with `predicate` from the most recent
    assertion on `predicate`.

## Default Definitions

`\#include "pp\_default.h"` is automatically executed before the first
line of `ifile` is read using the `-I-R` mechanism described above. A
file other than `pp\_default.h` may be specified using the `-I-D`
option. `pp\_default.h` typically contains `\#define` directives
that describe the current hardware and software environment. By using
the `-I``dir` or `-I-D``file` options different `pp\_default.h`
files may be referenced to support cross-compilation.
Proposed standard assertions for `pp\_default.h` are:

`system(``system-name``)`
:   Defines the operating system name. Example values for `system-name`
    are `unix`, `vms` and `msdos`.

`release(``system-release``)`
:   Defines the operating system release name. Example values for
    `system-release` are `hpux`, `bsd`, `svr4`, `sun`, `uts`,
    and `xinu`.

`version(``release-version``)`
:   Defines the operating system release version. Example values for
    `release-version` are `4.1c` and `4.3` for `release(bsd)`,
    `8` and `9` for `release(research)` and `3.0` etc. for
    `release(V)`.

`model(``model-name``)`
:   Defines the hardware model or workstation name. Example values for
    `model-name` are `apollo`, `sun`, `ibm-pc` and `unix-pc`.

`architecture(``architecture-name``)`
:   Defines the processor architecture name. Example values for
    `architecture-name` are `u3b`, `m68000`, `ibm`, `pdp11`, and
    `vax`.

`machine(``architecture-version``)`
:   Defines the processor architecture version. Example values for
    `architecture-version` are `2`, `20` and `20s` for
    `architecture(3b)`, `70` etc. for `architecture(pdp11)` and
    `750`, `780` and `micro` for `architecture(vax)`.

`addressing(``addressing-mode``)`
:   Defines the addressing mode, useful for PC compiler implementations.
    Example values for `addressing-mode` are: `small`, `medium`,
    `large`, `segmented` and `unsegmented`.

## Additional Processing

Adjacent " " string constants appearing in the text are concatenated.
However, strings are not concatenated in directives.
The new character escapes ``\\a, ``\\v and ``\\x... are converted
to octal notation for compatibility with older passes. This will
disappear as ANSI C support becomes more pervasive.

The ` :: `, ` .\` ` and ` -&gt;\` ` operators and ` //` ...
comments are recognized for the `C++` language.

## Compatibility

The `compatibility` dialect supports pervasive `Reiserisms` that will
be hard to shake out of old code as the ANSI standard arrives.
Compatibility support includes:

·
: `\#assert` and `\#unassert` are supported by maps to `\#define
    \#` and `\#assert \#`.

·
: the `disappearing comments` trick used to concatenate tokens within
    macro definitions (this trick does not work outside of macro
    definitions, but at least a diagnostic is produced). If
    `pp:splicecat` is set then the line splice sequence ``\\newline
    may also be used to concatenate tokens in macro definitions,
    otherwise ``\\newline translates to space.

·
: `vertical-tab` is treated as `space` in directive lines

·
: `formfeed` is treated as a `newline` character (although the
    line count is not incremented by `formfeed`)

·
: macro formal arguments appearing within " " or ' ' quotes in macro
    definitions are replaced by the corresponding actual argument text

·
: macro call arguments are not expanded before being placed in the
    macro body text

·
: trailing characters in directives are silently ignored

# FILES

/usr/include
:   standard directory for `\#include` files

/usr/local/include
:   sometimes searched after the standard directory during
    initialization

pp\_default.h
:   predefined symbols and assertions

# SEE ALSO

cc(1), egrep(1), m4(1), makerules(1), nmake(1), probe(1), proto(1),
getenv(3), pp(3), strcmp(3)\
`American National Standard for Information Systems -- Programming
Language C,` ANSI X3.159-1989.

# DIAGNOSTICS

The error messages produced by `cpp` are intended to be
self-explanatory. The line number and file name are printed along with
the diagnostic.
`predefined`, `readonly` and `active` macro diagnostics may surprise old
`cpp` users.

# AUTHOR

Glenn Fowler\
AT&T Bell Laboratories\

------------------------------------------------------------------------

  -- -- -------------------
        November 07, 2006
  -- -- -------------------


