# NAME

cpp - C language preprocessor

# SYNOPSIS

`cpp` \[ `options` \] \[ input \[ output \] \]

# DESCRIPTION

`cpp` is the preprocessor for all C language dialects. It is a
standalone version of the
[`libpp`](/web/20141128030238/http://www2.research.att.com/~astopen/man/man3/libpp.html)(3)
preprocessor library. The C dialect implemented by `cpp` is determined
by probing
[`cc`](/web/20141128030238/http://www2.research.att.com/~astopen/man/man1/cc.html)(1)
using
[`probe`](/web/20141128030238/http://www2.research.att.com/~astopen/man/man1/probe.html)(1).
The path of the emulated compiler can be changed by the `-D-X` command
line option.
If `output` is omitted then the standard output is written; if `input`
is also omitted then the standard input is read. NOTE: this is an
ancient, non-standard, non-intuitiive file operand syntax that is
required by
[`cc`](/web/20141128030238/http://www2.research.att.com/~astopen/man/man1/cc.html)(1);
use shell file name expansion at your peril.

`cpp` specific options are set by the `-D-` and `-I-` options.

# OPTIONS

-`C`, --`comments`
:   Pass comments to the output. By default comments are omitted.

-`D`, --`define`=`name\[=value\]`
:   Define the macro `name` to have `value`; `1` is assumed if `=`
    `value` is omitted. If `name` begins with `:` then it is
    interpreted as a
    [`libpp`](/web/20141128030238/http://www2.research.att.com/~astopen/man/man3/libpp.html)(3)
    `\#pragma pp:` statement; if `name` begins with `%` then it is
    interpreted as a
    [`libpp`](/web/20141128030238/http://www2.research.att.com/~astopen/man/man3/libpp.html)(3)
    `\#` directive statement; if `name` begins with `-` or `+`
    then it is interpreted as a
    [`libpp`](/web/20141128030238/http://www2.research.att.com/~astopen/man/man3/libpp.html)(3)
    option; `-` turns the option on, `+` turns it off. Most options
    have a `\#pragma` counterpart that is listed with the
    option definition. Right, this is ugly, but its the only portable
    way to pass options through
    [`cc`](/web/20141128030238/http://www2.research.att.com/~astopen/man/man1/cc.html)(1)
    to `cpp`:

    [`-D-C, pp:compatibility`]()
    : \
        Preprocess for K&R compatibility.

    [`-D-D``level`, `pp:debug` `level`]()
    : \
        Set the debug trace level. Higher levels produce more output.
        Levels higher than 3 enabled only in `-g` compiled versions.

    [`-D-F``name`]()
    : \
        Set the main input file name to `name`. This only affects error
        message and line sync output.

    [`-D-H, pp:hosted`]()
    : \
        All directories are hosted; compatibility warning messages from
        hosted directory headers are suppressed.

    [`-D-I, pp:cdir`]()
    : \
        All directories contain C headers; used only with `-D-+`.

    [`-D-K, pp:keyargs`]()
    : \
        Enable the non-standard `name=value` macro argument mode.

    [`-D-L`\[`id`\], `pp:lineid` \[`id`\]]()
    : \
        Set the line sync directive id to `id` or null if omitted.

    [`-D-M, pp:nomultiple`]()
    : \
        Disable multiple include detection.

    [`-D-P, pp:passthrough`]()
    : \
        Enable the non-standard passthrough mode; may be useful for
        processing non-C input.

    [`-D-Q, pp:dump`]()
    : \
        Dump macro definitions to the output so that the output may be
        passed through `cpp` again. Used for generating
        precompiled headers.

    [`-D-R, pp:transition`]()
    : \
        Enable the transition preprocessing mode. Used for compilers
        that can't make up their semantics between K&R and ISO.

    [`-D-S, pp:strict`]()
    : \
        Enable strict preprocessing semantics and warnings. Works with
        any mode (compatibiliy, transition, or the default ISO).

    [`-D-T``test`, `pp:test` `test`]()
    : \
        Enable implementation specific test code according to `test`.

    [`-D-W, pp:warn`]()
    : \
        Enable warnings in non-hosted files.

    [`-D-X`\[`cc`\]]()
    : \
        Preprocess for the compiler `cc` which must be an executable
        path or an executable on `\$PATH`.

    [`-D-Y, pp:pedantic`]()
    : \
        Enable pedantic `pp::warn` warnings in non-hosted files.

    [`-D-Z, pp:pool`]()
    : \
        Enable pool mode. See
        [`libpp`](/web/20141128030238/http://www2.research.att.com/~astopen/man/man3/libpp.html)(3).

    [`-D-d`]()
    : List canonicalized `\#define` statements for non-predefined
        macros in the output.

    [`-D-m`]()
    : List canonicalized `\#define` statements for all macros. All
        other output is disabled.

    [`-D-+, pp:plusplus`]()
    : \
        Preprocess for the C++ dialect.

-`I`, --`include`\[=`directory`\]
:   Append `directory` to the list of directories searched for
    `\#include` files. If `directory` is `-` then: (1) `-I`
    directories before `-I-` are searched only for "..." include
    files; (2) `-I` directories after `-I-` are searched for "..."
    and &lt;...&gt; include files; (3) the directory `.` is searched
    only if it is explicitly specified by a `-I` option.

    [`-I-C``directory`, `pp:cdir` `directory`]()
    : \
        Mark `directory` as a C header directory. Used with
        `pp:plusplus`.

    [`-I-D\[``file`\]]()
    : \
        Read the default
        [`probe`](/web/20141128030238/http://www2.research.att.com/~astopen/man/man1/probe.html)(1)
        definitions from `file`, or ignore the default definitions if
        `file` is omitted.

    [`-I-H``directory`, `pp:hostdir` `directory`]()
    : \
        Mark `directory` as a hosted directory. Headers from hosted
        directories have compatibility warnings disabled.

    [`-I-I``header`, `pp:ignore` `header`]()
    : \
        Add `header` to the list of ignored headers.

    [`-I-M``file`]()
    : \
        `file` contains a sequence of `header` \[= "`map`" \] lines,
        where `header` is either &lt;`name`&gt; or "`name`", and "`map`"
        is an explicit binding for `header`. `header` is ignored if =
        "`map`" is omitted.

    [`-I-R``file`]()
    : \
        Include `file` but do not emit text or line syncs.

    [`-I-S``directory`]()
    : \
        Add `directory` to the default standard include directory list.

    [`-I-T``file`]()
    : \
        Include `file` and emit text to the output file.

The option value may be omitted.\
-`M`, --`dependencies`
:   Generate
    [`make`](/web/20141128030238/http://www2.research.att.com/~astopen/man/man1/make.html)(1) dependencies.
    Not needed with
    [`nmake`](/web/20141128030238/http://www2.research.att.com/~astopen/man/man1/nmake.html)(1).
    `-M` may be followed by optional `flags` to change dependency
    output styles:

    [`D`]()
    : Generate dependencies in a separate `.d` file. Preprocessed
        output is still written to `output` , or the standard output if
        `output` is omitted.

    [`G`]()
    : Generate missing dependencies too.

    [`M`]()
    : Only generate local header dependencies; `hosted` headers
        are omitted. Note that `hosted` headers are determined by
        `-I-H` and the `pp:hosted` and `pp:hostdir` pragmas; no
        special distiction is made between "" and &lt;&gt;
        `include` styles.

-`P`, --`sync`
:   Emit line syncs. On by default; -`P` means --`nosync`.

-`U`, --`undefine`=`name`
:   Remove the definition for the macro `name`.

-`A`, --`assert`=`assertion`
:   Enter the assertion via `\#assert` for system V compatibility.

-`E`, --`preprocess`
:   Ignored for compatibility with ancient compilers.

-`H`, --`include-reference`\[=`size`\]
:   Emit `\#include` file paths on the standard error, one per line,
    indented to show nesting. If the optional `size` argument is
    specified then the entire `-H` option is ignored. The option value
    may be omitted.

-`T`\[`length`\]
:   If not
    [`gcc`](/web/20141128030238/http://www2.research.att.com/~astopen/man/man1/gcc.html)(1)
    then truncate identifiers to `length` characters for compatibility
    with old AT&T (I guess only Lucent needs them now) compilers. The
    option value may be omitted.

-`V`, --`version`
:   Emit the
    [`libpp`](/web/20141128030238/http://www2.research.att.com/~astopen/man/man3/libpp.html)(3) version.

-`X`, --`argmode`
:   Enable `name`=`value` macro arguments for
    [`easel`](/web/20141128030238/http://www2.research.att.com/~astopen/man/man1/easel.html)(1) compatibility.

-`Y`, --`standard`=`directory`
:   Add `directory` to the list searched for `\#include`
    `&lt;...&gt;` files.

# SEE ALSO

[`cc`](/web/20141128030238/http://www2.research.att.com/~astopen/man/man1/cc.html)(1),
[`gcc`](/web/20141128030238/http://www2.research.att.com/~astopen/man/man1/gcc.html)(1),
[`libpp`](/web/20141128030238/http://www2.research.att.com/~astopen/man/man3/libpp.html)(3)

# IMPLEMENTATION

`version`
:   cpp (AT&T Research) 2009-02-02

`author`
:   Glenn Fowler
    &lt;[glenn.s.fowler@gmail.com](https://web.archive.org/web/20141128030238/mailto:glenn.s.fowler@gmail.com)&gt;

`copyright`
:   Copyright © 1986-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030238/http://www.eclipse.org/org/documents/epl-v10.html)


