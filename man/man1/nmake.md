# NAME

nmake - configure, manage and update file hierarchies

# SYNOPSIS

`nmake` \[ `options` \] \[ script ... \] \[ target ... \]

# DESCRIPTION

`nmake` reads input `makefiles` and triggers shell actions to build
target files that are out of date with prerequisite files. Most
information used to build targets is contained in the global `base
rules` that are augmented by user `makefiles`. Each operand may be an
option, script, or target. An option operand is preceded by `-` or
`+`. A script operand contains at least one of `space`, `tab`,
`newline`, `:`, `=`, `"`, or ``\\ and is parsed as a separate,
complete makefile. Otherwise the operand is a `target` that is generated
according to the `makefile` and `global` rules. `target` operands are
made in order from left to right and override the default targets.
Command line options, scripts and targets may appear in any order, with
the exception that no option operand may appear after a `--` operand.

Options are qualified by the base name of the makefile that defined
them. Unqualified options are defined by `nmake` itself.

## Makefiles

`makefiles` are the main source of input to `nmake`. A makefile contains
a sequence of assertions and variable assignments that describe target
files and their prerequisites. All parsing is ordered from left to
right, top to bottom.
At least one makefile must be specified. If no `file` options are
present then `nmake` attempts to read, in order, one of `Makefile` or
`makefile`. The first line of the first makefile determines the base
rules context. If it is of the form

    rules [ "base-rules" ]

then `base-rules` will be used rather than the default `makerules`. If
"`base-rules`" is not specified then no base rules are used. Omitting
`rules` is equivalent to specifying `rules "makerules"`. The actual
base rules file, which must be a compiled global makefile, is found by
changing the `base-rules` suffix to `.mo` and binding the resulting
name using the directories of `.SOURCE.mk` (see `Binding`). The
following makefile descriptions rely on `nmake` engine constructs and
are independent of the base rules context.
If a makefile contains
[`cpp`](/web/20150717143740/http://www2.research.att.com/~astopen/man/man1/cpp.html)(1)
directives then it is first passed through a modified ANSI `cpp`.
Directives and C-style comments are treated as usual, but `cpp` macros
are only expanded on directive lines. `#` preceded by zero or more space
characters (`space` or `tab`) starting in column 1 is interpreted by
`cpp`, otherwise text between `#` (preceded by at least one space
character) and `newline` is treated as a comment by `nmake`. Blank
lines are uniformly ignored.

After all the makefiles have been read in, and before any command line
targets are made, the collective makefile information is automatically
`compiled` into a single `nmake` object file. The next time `nmake`
executes this object file is read in place of the makefiles. The object
file is automatically regenerated whenever the makefiles or their
prerequisites (.e.g., `include` dependencies) have changed. The
`nmake` object file name is `base``.mo` where `base` is the base name
of the first non-global makefile. For better performance makefiles
specified by the `global` option should be precompiled `nmake` object
files. Refer to the `compile` option below for more information.

## Variables

Variables are assigned by

    variable = value

where `variable` may be any sequence of letters, digits, underscores and
`dot`s. Depending on the context (e.g., `:` dependency, operator
dependency, assignment, action), subsequent appearances of `$(variable)`
expand to `value` and `$$(variable)` expands to `$(variable)`, otherwise
`$` is passed untouched. `value` is not expanded until `$(variable)` is
encountered (see `Variable Editing`). `variable := value` causes
`value` to be expanded before assigning it to `variable` and
`variable += value` appends the expanded `value` to the current value of
`variable`. `variable == value` assigns `value` to `variable` and also
marks `variable` as a candidate implicit state variable prerequisite.
`variable &= value` defines the hidden (auxiliary) value of `variable`.
The auxiliary value is not saved in the statefile. The expansion of
`variable` will include the primary and auxiliary values (see the :V
edit operator of `Variable Editing`).
Variable assignments come from many sources. The precedence order
(highest to lowest) is:

`automatic`
:   Variables maintained by `nmake` (see `Automatic Variables`).

`dynamic`
:   Assignments done while building targets.

`command line`
:   Assignments in command line `scripts`.

`import variables`
:   Colon separated environment variable names listed in the value of
    the `MAKEIMPORT` variable (see `ENVIRONMENT`).

`makefile`
:   Normal makefile assignments.

`environment`
:   Variables defined in the environment (see
    [`env`](/web/20150717143740/http://www2.research.att.com/~astopen/man/man1/env.html)(1)).

`global makefile`
:   Includes base rule assignments.

\
Variable names containing `dot` cannot conflict with environment
variables set by the shell; such variables are typically used by the
base rules. To avoid base rule conflicts users should not define upper
case variable names with `dot` as both the first and last character.

## Assertions

`assertions` specify dependency relationships between targets and
prerequisites and provide actions that may be executed to build targets
that are out of date with their prerequisites. An individual assertion
is a list of target atoms, a `dependency operator` (see `Assertion
Operators`), and an ordered list of prerequisite atoms for the targets.
Subsequent lines with an indentation level greater than the first target
comprise the action. The target list, the prerequisite list and the
action may be empty. Variables in the target and prerequisite lists are
expanded when the assertion is read, whereas variables in the action are
not expanded until the action is executed. For portability only `tab`
characters should be used for action indentation.
A single assertion with multiple targets associates the prerequisite
list and action with the targets as if each target were in a separate
assertion. Single assertions are more efficient in that the storage used
by the action is shared among the targets.

An atom may appear as a target in more than one assertion. Prerequisites
from successive assertions are simply appended to the prerequisite list
of the target, with the exception that duplicate prerequisites are
deleted (from the right) at assertion time. Only one action may be
specified per target. The collection of all assertions for a given
target is called the `rule` for that target. Atom names containing the
special characters `:,` `#,` `=` and `+` must be enclosed in double
quotes. For example:

    target : ":file1" file2
           action

## Binding

In the process of making a target atom `nmake` `binds` the atom to
either a `file`, a `virtual atom` or a `state variable`. This binding
remains in effect for the entire `nmake` execution.
A `state variable` is an atom associated with an `nmake` variable that
holds the variable value and the time the variable last changed. This
information is retained in the `statefile` `base`.ms where `base` is the
base name of the first makefile. Statefiles are automatically generated
and loaded using the `nmake` object file algorithms. The state variable
atom for the `nmake` variable `variable` is `(``variable``)``.` For
example:

    x.o : (DEBUG)

specifies that `x.o` depends on the definition of the variable `DEBUG`.
The contents of the statefile can be listed by executing

    nmake -f base.ms -blr

Atoms are bound to files using the prerequisites of the special
`.SOURCE` and `.SOURCE``.pattern` atoms (see `Special Atoms`). The
prerequisites of these atoms are ordered lists of directories to be
scanned when searching for files.

A `virtual` atom binds neither to a file nor to a state variable.
Virtual atoms are declared using the `.VIRTUAL` attribute. Virtual
atom times are retained in the statefile.

## Make Algorithm

The steps taken to make a target atom are:

bind the atom
:   An atom retains its binding until `nmake` exits unless it is
    explicitly unbound.

check if atom already made
:   No work required for atoms that have already been made. If atom is
    active (action executing) then block until its action completes
    before returning.

check statefile consistency
:   The current time, prerequisites and action are compared with those
    recorded in the statefile. Any differences force the target to be
    rebuilt. Notice that this type of rebuild may result in empty
    `\$(&gt;)` expansions in non-metarule actions.

check `.INSERT` and `.APPEND`
:   Target prerequisites are modified according to these special atoms.

make explicit prerequisites
:   The explicit prerequisites are (recursively) made from left to
    right. The most recent prerequisite time is saved.

make implicit prerequisites
:   If the target has no explicit action and no explicit prerequisites
    and a metarule can be applied to generate the target then the
    metarule prerequisites are (recursively) made from left to right.
    Again the most recent prerequisite time is saved.

check if out of date
:   If the most recent prerequisite is newer than the target or if the
    target information is not consistent with the statefile then the
    target action is triggered to build the target.

make scan prerequisites
:   If the target atom is a file with a `.SCAN``.x` attribute (see
    `Special Atoms`) then the scan prerequisites are (recursively)
    made from left to right. The scan prerequisites are determined
    either from the statefile information (if consistent) or by reading
    the contents of the file using scan strategy `.x`. The time noted
    for the target atom is the most recent of its own and
    all (recursively) of its scan prerequisite times. The scan
    prerequisites are saved in the statefile to avoid scanning during
    the next `nmake` execution.

sync statefile information
:   When the target is built (action, if any, completed) its time,
    action and prerequisites are saved in the statefile in preparation
    for the next `nmake` execution.

## Engine Control

The global flow of control in the `nmake` engine is, in order:

read the args file
:   The first file in `\$(MAKEARGS)` (see `ENVIRONMENT`) that exists
    in the current directory is read and the contents are inserted into
    the command line argument list.

read the command line arguments
:   The `options` and command line `script` arguments are parsed.

read the initialization script
:   In addition to the variables listed in `ENVIRONMENT` section, the
    special atoms `.VIEW` and `.SOURCE.mk` are initialized.

read the base rules
:   Determine which base rules are to be used (either user-defined or
    default) by checking the first line of the first explicit makefile
    for the `rules` statement. The first explicit makefile is
    determined by first ckecking the command line for the `-f`
    file option. If the `-f` option is not found, then the first file
    listed in `\$(MAKEFILES)` (see `ENVIRONMENT`) that exists
    is checked. If the `rules` statement is not found in that file,
    then the default base fules, `\$(MAKERULES),` (see
    `ENVIRONMENT`) are used.

read the global makefiles
: \

read the explicit makefiles
:   If no `file` options are given then the files listed in
    `\$(MAKEFILES)` (see `ENVIRONMENT`) are used.

compile makefiles to form the `nmake` object file
:   If the `nmake` object file is out of date with the input makefiles
    then the makefiles are recompiled.

read the statefile
:   The statefile is loaded as an `nmake` object file.

initialize `.ARGS`
:   The prerequisites of `.ARGS` are set to the list of command line
    `targets`.

make `.MAKEINIT` if defined
: \

make `.INIT` if defined
: \

check `.ARGS`
:   If `.ARGS` has no prerequisites then append the prerequisites of
    `.MAIN` onto `.ARGS`.

make the prerequisites of `.ARGS`
:   This constitutes the actions requested either on the command line or
    in the makefile, subject to the actions of `.MAKEINIT` and
    `.INIT`.

make `.DONE` if defined
: \

## Programming Constructs

Stuctured programming constructs may appear inside `.MAKE` actions or
outside assertions. The construct keywords must be the first word on a
line. Atom names matching any of the keywords must be quoted (when the
first word on a line) to avoid conflicts.
Each `expression` may be a combination of arithmetic and string
expressions where the string expression components must be quoted. "..."
strings use shell pattern matching (.e.g., "`string`" == "`pattern`")
whereas '...' strings use string equality. Empty strings evaluate to 0
in arithmetic expressions and non-empty strings evaluate to non-zero.
Expression components may also contain optional variable assignments.
All computations are done using signed long integers.

`error` `level message`
:   `message` is output as an `nmake` error message with severity level
    `level`. `level` may be one of:

    `&lt; 0`
    : debug trace -- output only if `level` &lt;= `debug`.

    `0`
    : information

    `1`
    : warning

    `2`
    : error -- no exit

    `&gt;= 3`
    : error -- exit with code (`level`-2)

    \

`eval`
: \

`...`
: \

`end`
: The statements between `eval` and `end` are expanded an
    additional time. `eval ... end` pairs may nest to cause more than
    one additional expansion.

`break`
:   Breaks out of the `for` and `while` loops and resumes execution
    after the `end` statement.

`for` `variable` `patterns` ...
: \

`...`
: \

`end`
: The statements between `for` and `end` are executed with
    `variable` assigned to the name of each atom matching one of the
    shell `patterns`. A `break` statement breaks out of the loop and
    resumes execution after the `end` statement.

`if` `expression`
: \

`...`
: \

`elif` `expression`
: \

`...`
: \

`else`
: \

`...`
: \

`end`
: Nested `if` conditional construct.

`include` \[ - \] `path`
:   Include the file specified by `path`. If `-` is present, then the
    file is optionally included (no warning is generated if the file is
    not found).

`let` `variable = expression`
:   Sets the value of `variable` to the numeric value of `expression`.

`local` `var1 var2 ...`
:   Declares variables local to the current action.

`return` \[ `expression` \]
:   Return from the action with results specified by `expression`:

    `omitted`
    : \
        If `expression` is omitted then return as if the action
        completed normally.

    `-1`
    : The action failed.

    `0`
    : The target exists but has not been updated.

    `&gt;0`
    : Set the target time to the value specified by expression.

    \

`set` \[`no`\]`name`=\[`value`\]
:   Sets options using option-by-name format (see `OPTIONS`).

`while` `expression`
: \

`...`
: \

`end`
: `while` loop construct. A `break` statement breaks out of the
    loop and resumes execution after the `end` statement.

`print` `message`
:   Prints `message` to the standard output. (This is the same as
    `error` `0 message`.)

`rules` \["`base-rules`"\]
:   Determines the base rules context. If the `rules` statement is
    specified, it must be the first line of the first makefile. It will
    overwrite the context of the default base rules. Omitting the
    `rules` statement is equivalent to specifying `rules
    "makerules"`. The `rules` statement with no file name specified
    is a request that no base rules file is to be used.

## Metarules

Based on metarule patterns, `nmake` can infer prerequisites for files
that have no explicit actions or prerequisites. The prototype metarule
pattern is `prefix`%`suffix` and is matched by any string containing the
non-overlapping strings `prefix` at the beginning and `suffix` at the
end. `%` matches the remaining characters and is called the `stem`.
The following makefile specifies that `program` depends on two files
`a.o` and `b.o`, and that they in turn depend on `.c` files and a common
file `header.h`.

    program : a.o b.o
           cc a.o b.o libx.a -lm -o program

a.o : header.h a.c ``
           cc -c a.c

b.o : header.h b.c ``
           cc -c b.c

The `metarule` to create a file with suffix `.s2` that depends on a file
(with the same `base` name) with suffix `.s1` is `%.s2 : %.s1`. Any
prerequisites following `%.s1` are transferred to each target when the
metarule is applied. For example, a metarule for making optimized `.o`
files from `.c` files is

    %.o : %.c (CC) (CCFLAGS)
           $(CC) $(CCFLAGS) -c -o $(<) $(>)

Notice that the `.o` targets also depend on the values of the `CC` and
`CCFLAGS` `nmake` variables. If the current target is `a.o` then `nmake`
infers the following from the `%.o : %.c` metarule:

    a.o : a.c (CC) (CCFLAGS)
           cc -O -c -o a.o a.c

In this case the `stem` is `a`, `$(CC)` and `$(CCFLAGS)` expand to `cc`
and `-O`, respectively.
Assuming the `%.o : %.c` metarule has been asserted, the example can be
stated more briefly:

    program : a.o b.o
           $(CC) $(`) libx.a -lm -o $(<)

a.o b.o : header.h

Metarules are applied according to the order of the patterns listed as
the prerequisites of the `.METARULE` atom. Pattern order is
significant; the first possible name for which both a file and a
metarule exist is inferred.

Metarules are chained as necessary. Given the metarules `%.z : %.m` and
`%.m : %.a` and the source file `x.a`, the target file `x.z` will be
generated by first applying `%.m : %.a` to `x.a` to build `x.m`, and
then applying `%.z : %.m` to `x.m` to build `x.z`.

Metarules with the `%` target pattern are called `unconstrained`
metarules and are subject to additional constraints that control
metarule chaining. `unconstrained` metarules with the `.TERMINAL`
attribute are applied only when the prerequisite pattern matches an
existing file. Otherwise an `unconstrained` metarule is applied only if
there exists no other metarule (other than a `unconstrained` metarule)
for which the target pattern matches the current target. For example

    % : .TERMINAL RCS/%,v
           $(CO) $(COFLAGS) $(>)

is a metarule that generates source files from RCS version files in the
`RCS` subdirectory.

## Variable Editing

Edit operators allow variable values to be tested and modified during
expansion. The expansion syntax is:

    $(variable[:[@]op[sep arg]]...)

The operator groups, each preceded by `:`, are applied in order from
left to right to each space separated token in the expanded variable
`value`. The operator groups form a token pipeline where the output
(`returned` or `selected` tokens) of any operator group becomes the
input for the next operator group. `newline` is treated as a separate
token. `"`, `'` and \\ quote space characters, but they are
considered part of the token and are not removed. If `@` immediately
precedes an `op`, then the entire `value` is treated as a single token
for that operator. `sep` is usually `=`, but, where appropriate, some
operators support `!=` and the arithmetic comparisons `&lt;`,
`&lt;=`, `&gt;=` and `&gt;`.
The expansion algorithm first expands the variable name `variable` to
determine the value to be edited. This value and the operator
expressions (\[:\[@\]`op`\[`sep arg`\]\]...) are then expanded before
the edit operators are applied. The ultimate expansion is formed by
applying each operator to each token, separating adjacent results by a
single `space` character.

\$(`var1` | `var2`...) expands the value of the first (left to right)
non-`null` valued variable. If the last variable name is enclosed in
`" "` then this string is used as the value if all preceding variables
have `null` values. The standard `\\` character constants are
interpreted within the string.

Some operators `select` tokens by simply returning the token value as
the result; non-selected tokens produce `null` (the empty string). The
operators are:

`A`\[`sep` `expression`\]
\
Selects tokens having one or more attributes or prerequisites listed in
`expression`. The tokens are treated as atoms. In case of `expression`
being a space or vertical bar separated list of `attributes`, if `sep`
is \[ ! \]=, then atoms that \[` do not `\] have any of the listed
`attributes` are \[` not `\] selected (see `Special Atoms`).
`Attributes` defined through `.ATTRIBUTE` special atom may also be
used. If `sep` is &lt;, then the pattern association rule for the rule
inferred from the input token and the pattern association rule base name
specified in `attribute1` of `expression` is returned (ex.
\$("stdio.h":A&lt;.SOURCE.) would give .SOURCE.%.LCL.INCLUDE). `A`
alone expands to the list of applicable user-defined attributes.
`B`\[=`base`\]
\
`D`\[=`directory`\]
\
`S`\[=`suffix`\]
\
As stated previously, the edit operators form token pipelines. The file
component edit operators (`:D:B:S`) are the exception to the rule;
they do not form token pipelines because `nmake` treats the file
component edit operators as a group (although separated by `:`). Each
is applied as a single edit operation. Pathnames are partitioned into
three (possibly `null`) components. `directory` includes all
characters up to but not including the last `/`. `base` includes all
characters after the last `/` up to but not including the last `.`.
`suffix` includes all characters from the last `.` on. Multiple
`.`'s are treated as a single `.` and if `.` is the first
character after the last `/` and is the only `.` then it is included
in `base` rather than `suffix`. If the pipeline result is desired, extra
`:` must be specified (e.g., `:D::B` will apply `:B` edit
operation to the result of `:D` edit operation).
`C``&lt;del&gt;old&lt;del&gt;new&lt;del&gt;``\[G\]`
\
Similar to the
[`ed`](/web/20150717143740/http://www2.research.att.com/~astopen/man/man1/ed.html)(1)
substitute command. Substitutes the first occurrence of the string `old`
with the string `new` in each token. A trailing `G` causes all
occurrences of `old` to be substituted. `&lt;del&gt;` may be any
delimiter character. `C/` may be abbreviated as `/`.
`E`
Evaluates the complete input string as a logical, string, or integer
expression.
`F``=format`
\
Converts tokens according to `format`. `format` may be a concatenation
of the following:

`L`
: The token is converted to lower case.

`U`
: The token is converted to upper case.

`V`
: The token is converted to the valid `nmake` variable name.

`%`\[-\]\[`n`\]\[.`m`\]`c`
:   [`printf`](/web/20150717143740/http://www2.research.att.com/~astopen/man/man3/printf.html)(3)
    style formatting. Only the `s`, `d`, `o`, `x` and `u` conversions
    are supported.

\
`G``=pattern`
\
Selects token files that can build (generate) files that match the
metarule pattern `pattern` using the metarules. For example, a token
`x``.y` is selected if a metarule `%``.s` `: %.y` has been
asserted.
`H` \[`sep`\]\[`U`\]
\
Heap sorts the tokens in ascending (if `sep` is &lt; or default) or
descending (if `sep` is &gt;) order. &lt;= `sep` will give low to high
numeric sort, and &gt;= `sep` will give high to low numeric sort. If
`U` is specified, the sort is unique (the duplicates are removed).
`I``=list`
\
`list` is expanded and directory tokens in `variable` that also appear
in the expanded value of `list` are selected. Each selected directory
will appear at most once in the return value. The directory path names
are canonicalized before comparison.
`K`=`pfx`
\
Splits long lines like `xargs(1)` into a number of tokens, applying
optional `pfx` to each token.
`L` \[`sep` \[`&lt;pattern`&gt;\]\]
\
Each token is treated as a directory name. For each token, the list of
all files in the specified directories which match the optional
`pattern` are returned. `sep` may be &lt;= or &gt;= and is used to
specify that the list should be sorted in ascending or descending order
respectively. The default order is unsorted.
`M`\[ ! \]=`pattern`
\
Selects tokens \[` not `\] matching the
[`egrep`](/web/20150717143740/http://www2.research.att.com/~astopen/man/man1/egrep.html)(1)
style regular expression `pattern`.
`N`\[ ! \]=`pattern`
\
Selects tokens \[` not `\] matching the
[`sh`](/web/20150717143740/http://www2.research.att.com/~astopen/man/man1/sh.html)(1)
file match expression `pattern`. Multiple patterns separated by `|`
denotes the inclusive or of the individual patterns.
`O`\[ ! \]|\[`&lt;relop&gt;&lt;n&gt;`\]
\
Each token is numbered by its left to right position, starting with 1.
Tokens with positions satisfying the integer expression `position relop
n` are selected. `relop` may be one of `&lt;`, `&lt;=`, `=`,
`!=`, `&gt;=` or `&gt;`. If `O` is specified alone, the output
is the number count of tokens, `O!` gives the string length of each
token.
`P`\[ ! \]=`op`
\
Treats the tokens as file path names and applies the path name operator
`op`. `op` may be:

`A`
: Returns the absolute path name for specified files.

`C`
: Returns the canonicalized path name. `.`'s and redundant `/`'s
    are removed (unless `.` is the only remaining character). Each
    `..` cancels the path name component to its left (unless that
    component is also `..`); `.. 's` are moved to the front of the
    name. `/..` forms are preserved in deference to some remote file
    system implementations.

`D`
: For each token that is a bound atom, the directory where the atom
    was bound is returned.

`H`\[=`suffix`\]
:   Generates 9 character hash file name (or up to 14 character hash
    file name if `suffix` is used - takes first 5 characters in `suffix`
    if it is greater than 5 characters) for the given token.

`I`=`file`
:   Selects tokens which are existing files and which have the same
    device and inode numbers as `file`. If `P!=I=`file`` is used, then
    those tokens which are existing files and are not the same file as
    `file` are returned.

`L`\[`&lt;relop&gt;level`\]
:   Selects tokens that are atoms bound in the level 0
    \[`&lt;relop&gt;level`\] view. Views are defined using the `.VIEW`
    special atom. `relop` may be one of `&lt;`, `&lt;=`, `=`,
    `!=`, `&gt;=` or `&gt;`.

`L\``
: Returns all the views of a bound file.

`L!`
: Returns the first occurrence of a bound file from all the views.

`P`=`lang`
:   Returns the pathname for the probe information file for the language
    specified by `lang` and the language processor specified in the
    input token.

`R`
: For each token, treated as a directory path name, a path name that
    leads to the (possibly relative) root of the token is returned. The
    return value is either `.` or a path name consisting of
    `..` components.

`S`
: The bound name for each token that is bound to a file within a
    subdirectory of its view is returned.

`U`
: The unbound name for each token is returned.

`V`
: Returns the view directory path name of the makefile for each token
    that is an atom bound to a file (see `.VIEW` special atom).

`X`
: Returns each token that is the path name of an existing file. The
    tokens are not bound.

\
`Q`
Each token is quoted for literal interpretation by
[`sh`](/web/20150717143740/http://www2.research.att.com/~astopen/man/man1/sh.html)(1).
`R`
Each token is parsed as a makefile, each in a separate context. `null`
is returned.\
`T``=type`
\
`T``=type``?``return`
\
The tokens are bound to atoms (unless stated otherwise) and are operated
on according to `type`. `?``return` replaces the default non-`null`
return value with the expanded value of `return` for selected atoms and
`null` otherwise. `return` is only expanded (a `second` expansion: the
operators have already been expanded once) if the test succeeds. If
`type` is preceded by `X`, then no binding is done. `type` may be one
of:

`A`
Returns the archive update action for each atom with the `.ARCHIVE`
attribute. If the returned action is `non-`null then it must be
executed for any archive that has been modified or copied before the
archive is used by the compilers or loaders (e.g.,
[`ranlib`](/web/20150717143740/http://www2.research.att.com/~astopen/man/man1/ranlib.html)(1)
on BSD-based systems).
`D`
The
[`cc`](/web/20150717143740/http://www2.research.att.com/~astopen/man/man1/cc.html)(1)
style definition of each token that binds to a state variable is
returned. Given:

    DEBUG =
    TEST = 1
    SIZE = 13
    STATEVARS = (DEBUG) (TEST) (SIZE)

`$(STATEVARS:T=D)` expands to `-DTEST -DSIZE=13`.
`E`
Similar to `T=D` except that the expanded definitions are
`name`=`value` pairs. Given the above example, `$(STATEVARS:T=E)`
expands to `DEBUG= TEST=1 SIZE=13`.
`F`
Each atom that binds to a file is selected. The bound atom name is
returned.
`G`
Each atom bound to a file that has been built (generated) is selected.
The bound atom name is returned.
`I\[-\]`
Each input token is the name of an input file to be read. The contents
of all the files are returned (including any newlines). A - following
the `I` inhibits the expansion of variable names in the file.
`M`
Generates the parentage chain of each active token.
`N`
If the unbound value of `variable` is `null` then `1` is returned,
otherwise `null` is returned.
`O`\[`mode`\]\[=`text`\]
\
Each input token is the name of the file to be written according to the
specified `mode .` If no `mode` is specified, `text` overrides the
contents of each file. By default, the new line separator is attached to
the end of the `text.` This edit operator is the complement to
`:T=I\[-\].` `mode` may be:

`+`
: Appends `text.`

`-`
: Does not put the new line separator at the end of `text.`

\
`P`
Each atom that binds to a file and is also not a symbolic link is
selected. The bound atom name is returned. If symbolic links (`link`(2))
are not implemented then `:T=P:` is equivalent to `:T=F:`.
`Q`
Each atom that exists is selected.
`R`
Each token is treated as an atom and the relative time (number of
seconds since the Epoch) of each atom is returned.
`S`\[`conv`\[`data`\]\]
\
Converts each atom to a new atom type specified by `conv` and `data`
(`null` is returned when the conversion specifies an undefined atom).
`conv` may be:

`A`
: Given the internal name for a state rule, convert it to the
    original name.

`F`
: Forces creation of a new atom. Used in conjunction with the other
    conversion operators.

`M`
: Returns the metarule name that generates files matching the metarule
    pattern `data` from files matching the metarule pattern named by
    each token.

`P`
: Returns the alternate prerequisite state atom.

`R`
: Returns the primary state atom. This is the default when `conv`
    is omitted.

`V`
: Returns the state variable atom for each token that names
    a variable.

\
`T`
The format for this operator is `T``relop``T``atom`. A comparison is
done between the time associated with `atom` and the times associated
with the atoms in the token list. The tokens whose times are `relop
atom` are returned. `relop` can be &lt;, &gt;, =, &lt;=, &gt;=, or !=.
If `atom` is not specified, it defaults to the current target. For
example,

    $(`:T>T)

lists the prerequisites whose times are newer than the time for the
current target.
`U`
Returns the atom or variable name for each state atom token.
`V`
If the unbound value of `variable` is non-`null` then `1` is
returned, otherwise `null` is returned.
`W`
If a type operator is forcing a file to be bound, and the `W` operator
is applied, do not wait for the bind to complete.
`X`
Binding should not be done. Used in conjunction with other type edit
operators.

\
`V`\[`type`\]
\
The `value` of `variable` is used without expansion. `type` may be:

`A`
: Expands to the auxiliary (assigned to `variable` with `&=`
    assignment operator) `value` of `variable` (see `Variables`).

`P`
: Expands to the primary `value` of `variable.`

\
`X``=list`
\
The directory cross product of the tokens in `variable` and the tokens
in the expanded value of `list` is returned. The first `.` `lhs`
operand produces a `.` in the cross product. All `rhs` absolute path
(rooted at `/`) operands are collected, in order, after all other
products have been computed, regardless of the `lhs` operands.
`Y``&lt;del&gt;non-null&lt;del&gt;null&lt;del&gt;`
\
If `value` is `null` then `null` is expanded and returned, otherwise
`non-null` is expanded and returned. `&lt;del&gt;` may be any delimiter
character. `Y?` may be abbreviated as `?`.
To illustrate some of the above operators:

    FILES = a.h b.h c.h x.c y.c z.c
    HEADERS = $(FILES:N=`.h)

    $(HEADERS:/^/-I/)       =>   -Ia.h -Ib.h -Ic.h
    $(FILES:N=`.c:/ /:/G)   =>   x.c:y.c:z.c

## Automatic Variables

The following variables are automatically defined and updated by
`nmake`:

`\$(-)`
: The current option settings suitable for use on `nmake` command
    lines. The options are listed using the `-o` option-by-name style
    and only those option settings different from the default
    are listed.

`\$(-``option``)`
:   `1` if the named `option` is set and non-zero, otherwise `null`.

`\$(+)`
: The current option settings suitable for use by `set`. Only those
    option settings different from the default are listed.

`\$(+``option``)`
:   The current setting for the named `option`, suitable for use by
    `set`.

`\$(=)`
: The list of command line `script` arguments and assignments for
    variables that are prerequisites of the atom `.EXPORT`.

`\$(&lt;)`
: The current target name.

`\$(&gt;)`
: The list of all explicit file prerequisites of the current target
    that are out of date with the target. `\$(&gt;)` is always
    non-`null` for triggered metarule actions but otherwise may be
    `null` (even if the current target action has triggered).

`\$(%)`
: The `stem` of the current metarule match, or the arguments of a
    function (see `.FUNCTION` in `Special Atoms`).

`\$(\`)`
: The list of all explicit file prerequisites of the current target.

`\$(\~)`
: The list of all explicit prerequisites of the current target.

`\$(&)`
: The list of all implicit and explicit state variable prerequisites
    of the current target. Implicit state variable prerequisites are
    generated by the language dependent scan.

`\$(!)`
: The list of all implicit and explicit file prerequisites of the
    current target. Implicit file prerequisites are generated by the
    language dependent scan.

`\$(?)`
: The list of all prerequisites of the current target. This includes
    all implicit and explicit state variable and file prerequisites.

`\$(\#)`
: If the current target is a state variable then `\$(\#)` is the
    state variable value, otherwise it is the unbound atom name.

`\$(@)`
: The action for the current target.

`\$(\^)`
: If the current target has been bound to a file in other than the top
    view then `\$(\^)` is set to the original (lower view) binding and
    `\$(&lt;)` is set to new (top view) binding, otherwise `\$(\^)`
    is `null`.

`\$(. . .)`
:   Represents all the atoms, rules and state variables used when
    making .MAKEINIT.

Each repeated occurrence of the automatic variable name character in the
variable expansion causes the `parent` of the current target to be used
as a reference. For example, `\$(&lt;&lt;)` is the name of the parent
of the current target and `\$(\`\`)` is the list of all its
prerequisites. `\$(c``atom``)` references information for `atom`
instead of the current target. Notice that `.IGNORE`, `.STATE`,
`.USE` and `.VIRTUAL` atoms are not included in `\$(&lt;)`,
`\$(&gt;)`, `\$(\`)`, or `\$(!)` automatic variable expansions.

## Assertion Operators

Assertion operators provide fine control over makefile assertions. Each
operator is an atom whose action is executed whenever the atom appears
as an operator in an assertion. Assertion operators are defined by
assertions:

    ":operator:" : .OPERATOR
           action

where the operator name syntax is `::` and `:``identifier``:``.`
and the operator name must be quoted in its defining assertion. An
operator is activated by an assertion of the form:

    lhs  :operator: rhs
           commands

The operator action is executed with `\$(&lt;)` set to `lhs`,
`\$(&gt;)` set to `rhs`, and `\$(@)` set to `commands`. No variable
expansion is done on `lhs`, `rhs`, or `commands`.

## Special Atoms

The Special Atoms defined by `nmake` all have the form .ID, where "ID"
is any string of capital letters, dots, or numbers. Users can define
their own Special Atoms, which do not have to begin with dot (.).
`nmake's` Special Atoms. The following atoms are special to `nmake` and
fall into one or more of these types, depending on the context:

`action rule`
:   Action used for `nmake` control.

`assertion attribute`
:   Provides fine control over `:` dependency operator assertions.

`dynamic attribute`
:   Assigned to target atoms by listing attribute names as prerequisites
    in assertions. Dynamic atom attributes may be tested using the
    `:A=``attribute``:` edit operator.

`dynamic list`
:   Prerequisites are used to control `nmake` actions.

`immediate rule`
:   Invokes an `nmake` action when appearing as a target in assertions
    `at assertion time.` The prerequisites and actions are cleared after
    the assertion.

`pattern association rule`
:   The meaning of the attribute is applied to the atoms matching the
    specified `pattern`. `pattern` is given in one of the following
    formats: string match (SOURCE.%.c, .BIND.-l%), suffix match
    (.SOURCE.c), or attribute match (.INSERT.%.ARCHIVE).

`readonly attribute`
:   Maintained by `nmake` and may not be explicitly assigned.

`readonly list`
:   Prerequisites maintained by `nmake`.

`sequence atom`
:   Sequence atoms are made at specific times during `nmake` execution
    and are ignored if not specified. Sequence atom shell actions are
    always executed in the foreground. Assert intermediate rules (with
    actions) and append these to the sequence atom prerequisite list to
    avoid attribute or base and global rule clashes.

\
The special atoms are:
`.ACCEPT   \[dynamic attribute\]`
\
Only file prerequisites can make `.ACCEPT` atoms out of date.
`.ACCEPT   \[immediate rule\]`
\
The prerequisite atoms are accepted as being up to date. However,
subsequent file prerequisites may make the atoms out of date.
`.AFTER   \[dynamic attribute\]`
\
`.AFTER` prerequisites are made after the action for the target atom
has completed.
`.ALWAYS   \[dynamic attribute\]`
\
The `noexec` option inhibits the execution of shell actions. However,
shell actions for `.ALWAYS` targets are executed even with `noexec`
on.
`.APPEND .pattern  \[pattern association rule\]`
\
The prerequisites of `.APPEND``.pattern` are appended to the
prerequisite list of each target atom which matches `pattern`
immediately before the target prerequisites are made. Notice that
`pattern` must be `%.ARCHIVE` for `.ARCHIVE` targets and
`%.COMMAND` for `.COMMAND` targets.
`.ARCHIVE   \[dynamic attribute\]`
\
Target atoms with the `.ARCHIVE` attribute are treated as archives
(see
[`ar`](/web/20150717143740/http://www2.research.att.com/~astopen/man/man1/ar.html)(1)).
Binding a `.ARCHIVE` target atom also binds the archive members to the
target. `.ARCHIVE` may be used as a pseudo-suffix for `.APPEND` and
`.INSERT`.
`.ARGS   \[dynamic list\]`
\
The prerequisites of `.ARGS` are the command line target arguments.
If, after making the `.INIT` sequence atom `.ARGS` has no
prerequisites then the prerequisites of `.MAIN` are copied to
`.ARGS`. As each prerequisite of `.ARGS` is made it is removed from
the `.ARGS` prerequisite list.
`.ATTRIBUTE   \[dynamic attribute\]`
\
Marks the target as a named attribute. Named attributes may be tested
using the `:A=``attribute``:` edit operator. A maximum of 32 named
attributes may be defined. The prerequisites of `.ATTRIBUTE`
constitute the list of all named attributes.
`.ATTRIBUTE .pattern  \[pattern association rule\]`
\
When an atom which matches `.pattern` is bound, it inherits the
attributes of `.ATTRIBUTE``.pattern`.
`.BEFORE   \[dynamic attribute\]`
\
`.BEFORE` prerequisites are made just before the action for the target
atom is executed.
`.BIND   \[immediate rule\]`
\
The prerequisite atoms are bound.
`.BIND .pattern  \[pattern association rule\]`
\
Specifies binding rules to be used when an atom cannot be bound using
the normal rules. The return value is new binding.
`.BOUND   \[readonly attribute\]`
\
Marks bound atoms.
`.BUILT   \[readonly attribute\]`
\
Marks state rule atoms corresponding to atoms that have been built.
`.CLEAR   \[assertion attribute\]`
\
Clears the attributes, prerequisites and action for the targets in the
assertion.
`.COMMAND   \[dynamic attribute\]`
\
Marks target atoms that bind to executable command files. `.COMMAND`
may be used as a pseudo-suffix for `.APPEND` and `.INSERT`.
`.COMPINIT   \[sequence atom\]`
\
This atom is made when the input makefiles are (re)compiled, just before
the make object file is written.
`.DEBUG   \[immediate rule / action rule\]`
\
`.DEBUG` is an alias for `.QUERY` (see `.QUERY`).
`.DONE   \[sequence atom\]`
\
This is the last atom made before `nmake` terminates execution.
`.DONTCARE   \[dynamic attribute\]`
\
If a `.DONTCARE` target cannot be made `nmake` continues as if it
existed, otherwise an error is issued and `nmake` either discontinues
work on the target parent and siblings if `keepgoing` is on or it
terminates processing and exits.
`.ENTRIES   \[readonly attribute\]`
\
Marks scanned directory or archive atoms that have entries (members).
`.ERROR   \[sequence atom\]`
\
This atom is executed when an error is encountered and the compile
option is off. If the `.ERROR` make action block returns 0 (default),
control returns to the point after the error. If the action block
returns -1, then the error processing continues.
`.EXISTS   \[readonly attribute\]`
\
Marks atoms that have been successfully made.
`.EXPORT   \[dynamic list\]`
\
The prerequisites are treated as `variable` names to be included in
`\$(=)` automatic variable expansions.
`.FAILED   \[readonly attribute\]`
\
Marks atoms that have been unsuccessfully made.
`.FILE   \[readonly attribute\]`
\
Marks atoms bound to existing files.
`.FORCE   \[dynamic attribute\]`
\
An atom with this attribute is always out of date the first time it is
made during a single `nmake` execution.
`.FOREGROUND   \[dynamic attribute\]`
\
The target action blocks until all other actions have completed.
Normally `nmake` makes future prerequisites while concurrent actions are
being executed, however, a `.FOREGROUND` target causes `nmake` to
block until the corresponding action completes.
`.FUNCTION   \[dynamic attribute\]`
\
A compound .USE attribute used in the default base rules composed from
.USE .ATTRIBUTE .MAKE .FUNCTIONAL .VIRTUAL .FORCE .REPEAT dynamic
attributes.
`.FUNCTIONAL   \[dynamic attribute\]`
\
A functional atom is associated with a variable by the same name. Each
time the variable is expanded the corresponding atom is made before the
variable value is determined. For example,

    src : .MAKE .FUNCTIONAL
    return $(`.SOURCE:L<=`.c)

In this example, `$(src)` evaluates to all the .c files in the
directories specified as prerequisites of `.SOURCE` (listed in the
ascending order). Also, `.FUNCTIONAL` special atom provides argument
support. For example,

    V : .MAKE .FUNCTIONAL
    return $(%:T=F)

one can call it by \$(V a1 ... an), where a1 ... an is the list of
arguments that can be referenced by `$(%)`.
`.GLOBALFILES   \[readonly list\]`
\
The prerequisites are the list of global makefiles specified by the
`global` option.
`.IGNORE   \[dynamic attribute\]`
\
Prevents any parent targets from becoming out of date with the target,
even if the target has just been built. This allows initialization
sequences to be specified for individual atoms:

    main : init header
           echo "executed if header is newer than main"

init : .IGNORE ``
           echo "always executed for main"

`.IMMEDIATE   \[dynamic attribute\]`
\
An atom with this attribute is made immediately after each assertion of
the atom.
`.IMMEDIATE   \[immediate rule\]`
\
The prerequisites and action are made each time this atom is asserted.
`.IMPLICIT   \[dynamic attribute\]`
\
This target attribute causes the implicit metarules to be applied even
if there is no action but prerequisites have been specified for the
target. Otherwise the implicit metarules are only applied to targets
with no explicit actions and prerequisites. This attribute turns the
`.TERMINAL` attribute off at assertion time.
`.INIT   \[sequence atom\]`
\
Made after the `.MAKEINIT` sequence atom.
`.INSERT   \[assertion attribute\]`
\
Causes the prerequisites to be inserted before rather than appended to
the target prerequisite list.
`.INSERT .pattern  \[pattern association rule\]`
\
The prerequisites of `.INSERT``.pattern` are inserted onto the
prerequisite list of each target atom which matches `.pattern`
immediately before the target prerequisites are made. Notice that
`.pattern` must be `.ARCHIVE` for `.ARCHIVE` targets and
`.COMMAND` for `.COMMAND` targets.
`.INTERNAL   \[readonly list\]`
\
This atom is used internally and appears here for completeness.
`.INTERRUPT   \[sequence atom\]`
\
This atom is made when an interrupt signal is caught. The engine state
may become corrupted by actions triggered while `.INTERRUPT` is
active. If the interrupt occurs while `.QUERY` is being made and `set
nointerrupt` is executed by `.INTERRUPT` then after `.INTERRUPT` is
made `nmake` continues from the point where the interrupt occurred,
otherwise `nmake` exits with non-zero status.
`.JOINT   \[dynamic attribute\]`
\
The action causes all targets on the left hand side to be jointly built
with respect to the prerequisites on the right.
`.LOCAL   \[dynamic attribute\]`
\
An atom with this attribute is made on the local machine after each
assertion of the atom when the coshell is active, no-op otherwise (see
[`coshell`](/web/20150717143740/http://www2.research.att.com/~astopen/man/man1/coshell.html)(1)).
`.LOCAL   \[immediate rule\]`
\
The prerequisites and action are made on the local machine each time
this atom is asserted when the coshell is active, no-op otherwise (see
[`coshell`](/web/20150717143740/http://www2.research.att.com/~astopen/man/man1/coshell.html)(1)).
`.MAIN   \[dynamic list\]`
\
If, after the `.INIT` target has been made, `.ARGS` has no
prerequisites then the prerequisites of `.MAIN` are appended onto
`.ARGS`. If not explicitly asserted in the input makefiles then the
first prerequisite of `.MAIN` is set to be the first target in the
input makefile that is neither a special atom nor a metarule.
`.MAKE   \[dynamic attribute\]`
\
Causes the target action to be read by `nmake` rather than executed by
the shell. Such actions are always read, even with `noexec` on.
`.MAKE   \[immediate rule\]`
\
The prerequisites and action are made each time this atom is asserted.
`.MAKEDONE   \[sequence atom\]`
\
Made after the `.DONE` sequence atom.
`.MAKEFILES   \[readonly list\]`
\
The prerequisites are the list of makefiles specified by the `file`
option.
`.MAKEINIT   \[sequence atom\]`
\
This target is made just after the statefile has been loaded. The base
rules typically use this atom to initialize the `nmake` engine. For this
reason the user should not redefine the `.MAKEINIT` action or
attributes. However, it is safe to insert or append prerequisites onto
`.MAKEINIT`.
`.MAKING   \[readonly attribute\]`
\
Marks each atom whose action is executing.
`.MEMBER   \[readonly attribute\]`
\
Marks an atom that is a member of a bound archive.
`.METARULE   \[readonly list\]`
\
The ordered list of LHS metarule patterns for all asserted metarules
excluding the `%` match-all metarules. This list determines the
metarule application order.
`.MULTIPLE   \[dynamic attribute\]`
\
Normally each assertion removes duplicate prerequisites from the end of
the target atom prerequisites list. `.MULTIPLE` atoms are allowed to
appear more than one in a prerequisite list.
`.NOTYET   \[readonly attribute\]`
\
Marks atoms that have not been made.
`.NULL   \[assertion attribute\]`
\
Assigns the null action to the target atoms. Used when an action must be
present, usually to force source files with prerequisites to be
accepted.
`.OPERATOR   \[dynamic attribute\]`
\
This attribute marks the target as an `operator` to be applied when
reading makefiles. Assertion operator names must match either `::` or
`:``identifier``:``.`
`.PARAMETER   \[dynamic attribute\]`
\
State variables with the `.PARAMETER` attribute are not expanded by
the `:T=D:` and `:T=E:` edit operators.
`.QUERY   \[immediate rule\]`
\
Full atom and state information is listed for each prerequisite.
`.QUERY   \[action rule\]`
\
Making `.QUERY` places `nmake` in an interactive loop. Input entered
at the `make&gt;` prompt may be any valid makefile input. However,
parsing readahead requires that a blank line follow an interactive
assertion before it takes effect. If a list of atoms is entered without
an assertion or assignment operator then the atoms are listed as if they
were prerequisites of the `.QUERY` `immediate rule`. The interactive
loop is exited by entering `control-D` (or `quit`) from the
keyboard. The assertion `.INTERRUPT : .QUERY` causes the interactive
loop to be entered on interrupts. The interactive loop can also be
invoked by specifying the `.QUERY` Special Atom on the command line.
The following command line will invoke the interactive loop:
`$ nmake -f nmake_filename .QUERY`

or, more commonly,

`$ nmake -f nmake_filename query`
`.READ   \[dynamic attribute\]`
\
The standard output of the action is read and interpreted as nmake
statements.
`.REBIND   \[immediate rule\]`
\
Each prerequisite is unbound and bound again as if it had already been
made.
`.REGULAR   \[readonly attribute\]`
\
Marks atoms that are bound to regular files.
`.REPEAT   \[dynamic attribute\]`
\
By default an atom is made at most once per `nmake` invocation.
`.REPEAT` marks atoms that are to be made repeatedly. `.FORCE` is
required to force the action to be triggered each time the atom is made.
`.REQUIRE .pattern  \[pattern association rule\]`
\
Modifies the binding algorithm to allow a bound atom to map to a list of
bound atoms. For example:

    .REQUIRE.-lcs : .FUNCTION
    return -lcs -lnsl -lsocket

will return the entire list specified above every time `-lcs` is called:

    -lcs => -lcs -lnsl -lsocket

`.RETAIN   \[immediate rule\]`
\
The prerequisites are variable names whose values are to be retained in
the statefile.
`.SCAN   \[dynamic attribute\]`
\
Used for defining scanning rules for a project specific language that
are not defined in the default base rules (see
[`makerules`](/web/20150717143740/http://www2.research.att.com/~astopen/man/man1/makerules.html)(1)
for the complete list of defined scan strategies).
`.SCAN .x  \[dynamic attribute\]`
\
Marks an atom (when bound to a file) to be scanned for implicit
prerequisites using the `.x` scan strategy. `.ATTRIBUTE``.pattern` `:
.SCAN``.x` is asserted for each of the scan strategies listed in
[`makerules`](/web/20150717143740/http://www2.research.att.com/~astopen/man/man1/makerules.html)(1).
`.SCAN.NULL   \[dynamic attribute\]`
\
Inhibits scanning. Used to override `.ATTRIBUTE``.pattern` scan
strategies.
`.SCAN.STATE   \[dynamic attribute\]`
\
Marks candidate state variables for scanning.
`.SCAN.IGNORE   \[dynamic attribute\]`
\
No-op scan strategies.
`.SCANNED   \[readonly attribute\]`
\
Marks archive and directory atoms that have been scanned for members
(implicit prerequisites) and records this information in the
`statefile`. The `.SCANNED` attribute may be removed from the
`statefile` with `-SCANNED` assertion, thus causing `nmake` to rescan
the file being scanned at a later time. For example,

    t :: t.c
    t.c : -SCANNED

`t.c` file is being scanned by `nmake` using `.SCAN.c` scan strategy
and it is marked with `.SCANNED` attribute. `t.c : -SCANNED` nullifies
this action.
`.SEMAPHORE   \[dynamic attribute\]`
\
Limits the number of executing shell actions for target atoms having the
same `.SEMAPHORE` prerequisite. Each `.SEMAPHORE` within an
assertion increments the semaphore count by 1. The maximum semaphore
count is 7. The following example makes the shell actions for a and b
mutually exclusive.

    set jobs=10
    all : a b
    .sema : .SEMAPHORE
    a b : .sema
           action

`.SOURCE   \[dynamic list\]`
\
The prerequisites of `.SOURCE` are directories to be scanned when
searching for files. The (left to right) directory order is important;
the first directory containing the file is used. The directory `.` is
always searched first.
`.SOURCE .pattern  \[pattern association rule\]`
\
The prerequisites of `.SOURCE``.pattern` are directories to be scanned
when searching for files which match suffix `.pattern`. If the file is
not found then the directories specified by the prerequisites of
`.SOURCE` are checked. The (left to right) directory order is
important; the first directory containing the file is used. The
directory `.` is always searched first. The implicit dependency scan
strategy (see `.SCAN`) may augment or override the default `.SOURCE`
search for individual atoms.
`.SPECIAL   \[assertion attribute\]`
\
Target atoms in the assertion are not appended to the prerequisites of
`.MAIN` and multiple action diagnostics are inhibited.
`.STATE   \[dynamic attribute\]`
\
Non-`.STATEVAR` atoms with this attribute are treated as state
variables with no implied connection to an `nmake` variable.
`.STATE   \[immediate rule\]`
\
The prerequisites are variable names that are marked as candidate
implicit state variable prerequisites (see `Variables`).
`.STATERULE   \[readonly attribute\]`
\
Marks internal state rule atoms that are used to store state
information.
`.STATEVAR   \[readonly attribute\]`
\
Marks state variable atoms.
`.TARGET   \[readonly attribute\]`
\
Marks atoms that appeared as the target of an assertion.
`.TERMINAL   \[dynamic attribute\]`
\
This attribute allows only `.TERMINAL` metarules to be applied to the
target. Otherwise metarules are applied to targets with no explicit
actions and prerequisites. This attribute turns the `.IMPLICIT`
attribute off at assertion time. For metarule assertions, `.TERMINAL`
marks `unconstrained` metarules that may be applied only to
`.TERMINAL` targets or non-generated source files. `.TERMINAL`
attribute may also be applied to directories that do not have
subdirectories. If a `.SOURCE` directory has `.TERMINAL` attribute,
`nmake` will not search that directory for subdirectories. This can be
used as an optimization technique when there are many `.SOURCE`
directories that do not have subdirectories and there are many files
with the directory prefixes (saves on unnecessary filename look-ups).
`.TMPLIST   \[readonly list\]`
\
This atom is used internally and appears here for completeness.
`.TRIGGERED   \[readonly attribute\]`
\
Marks atoms whose actions have triggered during the current `nmake`
execution.
`.UNBIND   \[immediate rule\]`
\
Each prerequisite is unbound as if it had not been bound.
`.USE   \[dynamic attribute\]`
\
Marks the target as a `.USE` atom. Any target having a `.USE` atom
as a prerequisite will be built using the `.USE` atom action and
attributes. The leftmost `.USE` prerequisite takes precedence.
`.VIEW   \[readonly list\]`
\
The prerequisites are view directory path names. `.` is by default the
first view directory. A view directory is a directory from which `nmake`
could be executed. `.VIEW` is initialized from the `MAKEPATH` and
`VPATH` environment variables.
`.VIRTUAL   \[dynamic attribute\]`
\
A `.VIRTUAL` atom never binds to a file. `.VIRTUAL` atom times are
saved in the statefile.
`-   \[dynamic list\]`
\
Used to control synchronization when making a list of prerequisites. A
`-` in a prerequisite list causes nmake to wait until the preceding
prerequisite's actions are complete before continuing.

## Command Execution

Each shell action is sent as a unit to `sh` via
[`coshell`](/web/20150717143740/http://www2.research.att.com/~astopen/man/man3/coshell.html)(3).
`sh` echos commands within actions as they are executed unless the
`silent` option is on. Since actions are sent as a unit, special shell
constructs (`case`, `if`, `for`, `while`) may cross `newline`
boundaries without `newline` escapes.
Commands within actions returning nonzero status (see
[`intro`](/web/20150717143740/http://www2.research.att.com/~astopen/man/man1/intro.html)(1))
cause `nmake` to stop unless the `ignore` or `keepgoing` option is
on.

`nmake` works only with `Bourne`-based shells such as
[`sh`](/web/20150717143740/http://www2.research.att.com/~astopen/man/man1/sh.html)(1)
and
[`ksh`](/web/20150717143740/http://www2.research.att.com/~astopen/man/man1/ksh.html)(1).
`nmake` is optimized to work with
[`ksh`](/web/20150717143740/http://www2.research.att.com/~astopen/man/man1/ksh.html)(1).
`COSHELL` environment variable must point to either `ksh`, `sh`, or
the network shell server
[`coshell`](/web/20150717143740/http://www2.research.att.com/~astopen/man/man1/coshell.html)(1).

## Special Commands

`ignore` `shell-command`
:   Causes the exit status of `shell-command` to be ignored.

`silent` `shell-command`
:   Prevents `shell-command` from being printed by the shell, if
    possible. `silent` must precede `ignore` if both are to be used.
    `set +x` prevents subsequent commands from being printed by the
    shell up to and including the next `set -x`.

## Jobs

The `jobs` option allows `nmake` to build many targets concurrently.
The builds are synchronized using the target dependency graph. Actions
for targets with the `.FOREGROUND` attribute block until all other
jobs have completed. Prerequisites with the `.SEMAPHORE` attribute are
used for mutual exclusion.
All actions should be written with concurrency in mind. Most problems
occur when commands generate files with fixed names, such as
[`yacc`](/web/20150717143740/http://www2.research.att.com/~astopen/man/man1/yacc.html)(1)
and
[`lex`](/web/20150717143740/http://www2.research.att.com/~astopen/man/man1/lex.html)(1).

## Conventions

`nmake` attributes match the regular expression
`.\[.A-Z\]\[.A-Z0-9\]\``. User attributes match the regular expression
`.\[.A-Z\]\[.a-z0-9\]\``. Intermediate targets match the regular
expression `.\[.a-z\]\[.a-z0-9\]\``. Use \$COTEMP (see
`ENVIRONMENT`) to generate temporary file names. To avoid conflicts
with the base rules the user should not define upper case atom or
variable names with `.` as the first character.

# ENVIRONMENT

The file names and directories used by the `nmake` engine are
parameterized using variables.

## Engine Variables

These variables are assigned default values by the `nmake` engine
itself. Some of the values are determined at installation time while
others are determined by each invocation environment.
`COTEMP`
\
The `COTEMP` environment variable is generated and set to a different
value for each shell command. It is 10 characters long and can be used
for temporary file names, so names of the form

    <pfx>$COTEMP<sfx>

will be upto 14 characters to satisfy the system V file name length
restriction.
`MAKE`
The path name of the current `nmake` program suitable for use as a shell
command or in an
[`execvp`](/web/20150717143740/http://www2.research.att.com/~astopen/man/man3/execvp.html)(3)
system call.
`MAKEARGS=``Makeargs``:``makeargs`
\
A colon separated list of the candidate argument file names.
`MAKEFILE`
\
The name of the first makefile.
`MAKEFILES=``Makefile``:``makefile`
\
A colon separated list of candidate implicit makefile names.
`MAKELIB`
\
The directory for `nmake` related files, e.g., base rules.
`MAKEPP=``\$(MAKELIB)/../cpp`
\
The name of the (deprecated) makefile preprocessor.
`MAKERULES=``makerules`
\
The name of the default base rules. The base rules file must be a
compiled make object file and is named by changing the suffix in
`\$(MAKERULES)` to `.mo` and binding the result using the
directories in `.SOURCE.mk`. `makerules` may be an absolute path name.
`MAKERULESPATH=``\$(LOCALRULESPATH):\$(MAKELIB):/usr/local/lib/make:/usr/lib/make`
\
Used to initialize `.SOURCE.mk`. All makefiles, including compiled
make object files and files included by makefiles, are bound using the
directories in `.SOURCE.mk`.
`MAKEVERSION`
\
The `nmake` engine version stamp.
`OLDMAKE`
\
Executed via
[`execvp`](/web/20150717143740/http://www2.research.att.com/~astopen/man/man3/execvp.html)(3)
when the first input makefile is not a valid `nmake` makefile.
`PWD`
The absolute pathname of the current directory.

## Uninitialized Variables

These variables have `null` default values and are used only when
defined.
`COSHELL`
\
The name of the shell used to execute shell actions.
[`execvp`](/web/20150717143740/http://www2.research.att.com/~astopen/man/man3/execvp.html)(3)
is used to execute the shell. If `COSHELL` is not defined, then
`ksh`, `sh`, and `/bin/sh` are tried in order.
`MAKECONVERT`
\
A space separated pair of the build tool script (other than `nmake`) and
the conversion tool. Used for compile time makefile conversion. For
example:

    export MAKECONVERT='Make.src "nmakegen $(>)"'

`MAKEIMPORT`
\
A colon separated list of environment variable names, the values of
which override any makefile variable assignments.
`MAKEPATH`
\
A colon separated list of directory names from which `nmake` could be
run on the current makefile. These directories are used by the
initialization script to initialize the `.VIEW` special atom. `.` is
always the first view by default.
`NPROC`
\
The maximum number of coshell processes that are to be executed
simultaneously (the environment variable equivalent of -j).
`VOFFSET`
\
`VOFFSET` is set to the path that goes from the viewpath node root to
the current working directory.
`VPATH`
\
A colon separated list of viewpath node names. The node names are
converted to `MAKEPATH` directories that are used by the
initialization script to initialize the `.VIEW` special atom.
`VPATH` is ignored if `nmake` is not executing within the first
viewpath node.
`VROOT`
\
`VROOT` is set to the relative path that gets from the current working
directory to the viewpath node root.

# OPTIONS

-`A`, --`accept`
:   Accept filesystem timestamps of existing targets.

-`a`, --`alias`
:   Enable directory aliasing.

-`b`, --`base`
:   Compile base or global rules.

-`B`, --`believe`=`level`
:   Believe the state file time of files lower than view level
    `level-1`. The file system time will be checked for files with no
    state or files in views equal to or higher than `level`. `level=0`
    causes the file system time to be checked for files on all
    view levels. The top view is level 0. The default value is `0`.

-`C`, --`compatibility`
:   Disable compatibility messages.

-`c`, --`compile`
:   Compile the input makefile and exit.

-`X`, --`corrupt`\[=`action`\]
:   `action` determines the action to take for corrupt or invalid top
    view state files. The top view default is `error` and the lower
    view default is `accept`. `action` may be one of:

    `accept`
    : \
        print a warning and set `--accept`

    `error`
    : \
        print a diagnostic and exit

    `ignore`
    : \
        print a warning and set `--noreadstate`

    If the option value is omitted then `accept` is assumed.

-`J`, --`cross`
:   Don't run generated executables.

-`d`, --`debug`=`level`
:   Set the debug trace level to `level`. Higher levels produce
    more output.

-`E`, --`errorid`=`id`
:   Add `id` to the error message command identifier. The default value
    is `make`.

-`n`, --`exec`
:   Enable shell action execution. `--noexec` disables all but
    `.ALWAYS` shell actions and also disables make object and state
    file generation/updates. On by default; -`n` means --`noexec`.

-`x`, --`expandview`
:   Expand `3d` filesystem paths.

-`e`, --`explain`
:   Explain each action.

-`f`, --`file`=`file`
:   Read the makefile `file`. If `--file` is not specified then the
    makefile names specified by `\$(MAKEFILES)` are attempted in order
    from left to right. The file `-` is equivalent to `/dev/null`.

-`F`, --`force`
:   Force all targets to be out of date.

-`g`, --`global`\[=`file`\]
:   Read the global makefile `file`. The `--file` search is not
    affected. The option value may be omitted.

-`i`, --`ignore`
:   Ignore shell action errors.

-`K`, --`ignorelock`
:   Ignore state file locks.

-`I`, --`include`=`directory`
:   Add `directory` to the makefile search list.

-`G`, --`intermediate`
:   Force intermediate target generation.

-`j`, --`jobs`=`level`
:   Set the shell action concurrency level to `level`. Level `1`
    allows dependency checking while an action is executing; level `0`
    stops all activity while an action is executing. The default value
    is `\${NPROC:-1}`.

-`k`, --`keepgoing`
:   Continue after error with sibling prerequisites.

-`l`, --`list`
:   List the current rules and variables on the standard output in
    makefile form.

-`M`, --`mam`=`type\[,subtype\]\[:file\[:parent\[:directory\]\]\]`
:   Write `make abstract machine` output to `file` if specified or to
    the standard output otherwise. See
    [`mam`](/web/20150717143740/http://www2.research.att.com/~astopen/man/man5/mam.html)(5)
    for details on the `make abstract machine` language. If `parent` !=0
    then it is the process id of a parent `mam` process. `directory` is
    the working directory of the current `mam` process relative to the
    root `mam` process, `.` if not specified. `type` must be one of:

    `dynamic`
    : \
        `mam` trace of an actual build

    `regress`
    : \
        `mam` for regression testing; labels, path names and time stamps
        are canonicalized for easy comparison

    `static`
    : \
        `mam` representation of the makefile assertions; used for
        makefile conversion

    `----`
    : 0 or more comma separated subtypes ----

    `port`
    : used by the base rules to generate portable makefiles; some
        paths are parameterized; on by default

    `----`
    : mam options ----

    `\[no\]hold`
    : \
        `hold` `mam` output until nested `nohold`

-`N`, --`never`
:   Don't execute any shell actions. `--noexec` executes `.ALWAYS`
    shell actions.

--`option`=`'char;name;flags;set;description;values'`
:   Define a new option. The definition is a delimiter separated
    field list. Any non-alpha-numeric delimiter other than `-` may
    be used. `;` is used in this description. Makefile `set option`
    definitions must be '...' quoted. Two adjacent delimiters specifies
    the literal delimiter character and a `-` field value specifies an
    empty field. `char` is the single character option name, `name` is
    the long option name, `set` is an optional `.FUNCTION` that is
    called when the option value is changed by `set`, `values` is an
    [`optget`](/web/20150717143740/http://www2.research.att.com/~astopen/man/man3/optget.html)(3)
    value list, and `flags` are a combination of:

    `a`
    : multiple values appended

    `b`
    : boolean value

    `i`
    : internal value inverted

    `n`
    : numeric value

    `o`
    : `-char` means `--no``name`

    `p`
    : .mo probe prerequisite

    `s`
    : string value

    `v`
    : optional option argument

    `x`
    : not expanded in `\$(-)`

--`override`
:   Implicit rules or metarules override explicit rules.

-`Q`, --`questionable`=`mask`
:   Enable questionable features defined by `mask`. Questionable
    features are artifacts of previous implementations (`nmake` has
    been around since 1984-11-01) that will eventually be dropped. The
    questionable `mask` registry is in the `main.c` `nmake`
    source file.

-`R`, --`readonly`
:   Current assignments and assertions will be marked `readonly`.

-`S`, --`readstate`\[=`level`\]
:   Ignore state files lower than view level `level`. `level=0` ignores
    state files on all view levels. The top view is level 0. The option
    value may be omitted. The default value is `0`.

-`q`, --`regress`\[=`action`\]
:   Massage output for regression testing. `action` may be one of:

    `message`
    : \
        alter messages only

    `sync`
    : sync 1-second clocks if necessary and alter messages

    If the option value is omitted then `message` is assumed.

--`reread`
:   Ignore any previously generated `.mo` files and re-read all
    input makefiles.

-`r`, --`ruledump`
:   Dump rule information in tabular form on the standard error when
    `nmake` exits.

--`scan`
:   Scan for and/or check implicit file prerequisites. On by default.

-`O`, --`serialize`
:   Serialize concurrent output by caching job stdout and stderr output
    until job completion.

-`s`, --`silent`
:   Do not trace shell actions as they are executed.

-`V`, --`strictview`
:   Set `VPATH` `.SOURCE` rule interpretation to follow strict `3d`
    filesystem semantics, where directories in the top views
    take precedence. On by default when running in `2d` with `VPATH`
    defined, off by default otherwise.

--`target-context`
:   Expand and execute shell actions in the target directory context.
    This allows a single makefile to control a directory tree while
    generating target files at the source file directory level. By
    default target files are generated in the current directory.

--`target-prefix`=`separator`
:   Allow metarules to match `separator` in the target to `/` in
    the source. Used to disambiguate source file base name clashes when
    target files are generated in the current directory. `separator`
    must not contain metarule or shell pattern characters.

-`T`, --`test`=`mask`
:   Enable test code defined by `mask`. Test code is
    implementation specific. The test `mask` registry is in the
    `main.c` `nmake` source file.

-`z`, --`tolerance`=`seconds`
:   Set the time comparison tolerance to `seconds`. Times within the
    tolerance range compare equal. Useful on systems that can't quite
    get the file system and local clocks in sync. A tolerance of more
    that 5 seconds soon becomes intolerable.

-`t`, --`touch`
:   Touch the time stamps of out of date targets rather than execute the
    shell action.

-`v`, --`vardump`
:   Dump variable information in tabular form on the standard error when
    `nmake` exits.

-`w`, --`warn`
:   Enable verbose warning messages.

--`writeobject`\[=`file`\]
:   Generate a `.mo` make object file in `file` that can be read
    instead of the input makefiles on the next `nmake` invocation. On
    by default. `--nowriteobject` prevents the generation. The default
    name is used if `file` is omitted or `-`. If `file` is a directory
    then the default is placed in that directory. The option value may
    be omitted. The default value is `\$(MAKEFILE:B:S=.mo)`.

--`writestate`\[=`file`\]
:   Generate a `.ms` make state file in `file` when `nmake`
    exits.The state contains the time stamps of all prerequisites and
    targets that have been accessed since the state file was
    first generated. On by default. `--nowritestate` prevents
    the generation. The default name is used if `file` is omitted or
    `-`. If `file` is a directory then the default is placed in that
    directory. The option value may be omitted. The default value is
    `\$(MAKEFILE:B:S=.ms)`.

-`o`, --`byname`=`name\[=value\]`
:   (obsolete) Set options by name.

-`D`, --`define`=`name\[=value\]`
:   (obsolete) Pass macro definition to the makefile preprocessor.

-`P`, --`preprocess`
:   (obsolete) Preprocess all makefiles.

-`U`, --`undef`=`name`
:   (obsolete) Pass macro deletion to the makefile preprocessor.

--`all-static`
:   (Makerules) Force the prerequisite libraries of static `+l``name`
    library references to be static.

--`ancestor`=`depth`
:   (Makerules) Set the ancestor search directory depth to `depth`.
    `MAKEPATH` and variant recursive invocations may increase the
    depth. The default value is `3`.

--`ancestor-source`=`.SOURCE.suffix directory...`
:   (Makerules) A list of `.SOURCE``.suffix` `directory` pairs added
    to the ancestor directory search. The default value is `.SOURCE.a
    lib .SOURCE.h include`.

--`archive-clean`=`edit-ops`
:   (Makerules) A catenation of edit operators that selects archive
    member files to be removed after being added to the archive.

--`archive-output`=`file`
:   (Makerules) The output file name for archiving actions (`pax`,
    `save`, `tgz`, etc.) The default is based on the current
    directory and the VERSION variable.

--`cctype`=`type`
:   (Makerules) Set the
    [`probe`](/web/20150717143740/http://www2.research.att.com/~astopen/man/man1/probe.html)(1)
    C compiler type identifier. The default value is based on the
    `CC` variable. To disable the C probe use `--cctype=-` or set
    `CC=""`.

--`clean-ignore`=`pattern`
:   (Makerules) Ignore `clean` action generated target files matching
    `pattern`.

--`clobber`\[=`pattern`\]
:   (Makerules) Replace existing `install` action targets matching
    `pattern` instead of renaming to `target``.old`. If the option
    value is omitted then `\`` is assumed.

--`compare`
:   (Makerules) Ignore `install` action targets whose contents have
    not changed. On by default.

--`debug-symbols`
:   (Makerules) Compile and link with debugging symbol options enabled.

--`force-shared`
:   (Makerules) Do not ignore `-l``name` shared library reference
    modification times.

--`instrument`=`command`
:   (Makerules) Enable compile-time, link-time and/or run-time
    code instrumentation. Instrumentation interfaces that replace the
    compiler command, and the `app`, `insight`, `purecov`,
    `purify`, `quantify` and `sentinel` special-need interfaces,
    are supported.

--`ld-script`=`suffix`
:   (Makerules) A space-separated list of suffixes of script files to be
    passed to the linker.

--`lib-type`
:   (Makerules) Bind library references to `--debug-symbols` or
    `--profile` specific variants.

--`link`=`pattern`
:   (Makerules) Hard link `install` action targets matching `pattern`
    instead of copying.

--`local-static`
:   (Makerules) Compile and link against static library targets. The
    default links against shared library targets, but care must be taken
    to point runtime shared library binding to the current directory
    when executing command targets in the current directory.

--`native-pp`=`level`
:   (Makerules) Force the use of the native C preprocessor and print a
    `level` diagnostic message noting the override.

--`official-output`=`file`
:   (Makerules) The
    [`diff`](/web/20150717143740/http://www2.research.att.com/~astopen/man/man1/diff.html)(1)
    log file name for the `official` action. If `file` is a relative
    path name then it is written in the next view level. The default
    value is `OFFICIAL`.

--`prefix-include`
:   (Makerules) Override the C preprocessor prefix include option.
    `--noprefix-include` may be needed for some compilers that
    misbehave when `\$(CC.INCLUDE.LOCAL)` is set and `\#include
    "..."` assumes the subdirectory of the including file. The default
    value is based on the
    [`probe`](/web/20150717143740/http://www2.research.att.com/~astopen/man/man1/probe.html)(1) information.

--`preserve`\[=`pattern`\]
:   (Makerules) Move existing `install` action targets matching
    `pattern` to the `ETXTBSY` subdirectory of the install target. If
    the option value is omitted then `\`` is assumed.

--`profile`
:   (Makerules) Compile and link with
    [`prof`](/web/20150717143740/http://www2.research.att.com/~astopen/man/man1/prof.html)(1)
    instrumentation options enabled.

--`recurse`=`action`
:   (Makerules) Set the recursive `:MAKE:` `action`:

    `combine`
    : \
        Combine all recursive makefiles into one rooted at the
        current directory. `::`, `:PACKAGE:`, `.SOURCE`\`, and
        `LDLIBRARIES` are intercepted to adjust relative directory and
        library references. Complex makefile hierarchies may not be
        amenable to combination.

    `implicit`
    : \
        All makefiles in all subdirectories are treated as if they
        contained `:MAKE:`.

    `list`
    : List the recursion directories, one per line, on the standard
        output and exit. A `-` prerequisite separates groups that may
        be made concurrently and a `+` prerequisite separates leaf
        directories from intermediate directories.

    `only`
    : Disable component closure and operate on explicit
        prerequisites only.

    `prereqs`
    : \
        List the recursion directory dependencies as a makefile on the
        standard output and exit.

    `number`
    : \
        Set the directory recursion concurrency level to `number`.

    The default value is `1`.

--`recurse-enter`=`text`
:   (Makerules) `text` prependeded to the `directory``:` message
    printed on the standard error upon entering a recursive
    `:MAKE:` directory.

--`recurse-leave`=`text`
:   (Makerules) `text` prependeded to the `directory``:` message
    printed on the standard error upon leaving a recursive
    `:MAKE:` directory. If `--recurse-leave` is not specified then
    no message is printed upon leaving `:MAKE:` directories.

--`select`=`edit-ops`
:   (Makerules) A catenation of edit operators that selects terminal
    source files.

--`separate-include`
:   (Makerules) Allow `\$(CC.INCLUDE.LOCAL)` to be used with compilers
    that support it. On by default. If `--noseparate-include` is set
    then `\$(CC.INCLUDE.LOCAL)` will not be used, even if the current
    compiler supports it.

--`shared`
:   (Makerules) Set `:LIBRARY:` to generate shared libraries (dlls).

--`static-link`
:   (Makerules) Compile and link with a preference for static libraries.

--`strip-symbols`
:   (Makerules) Strip link-time static symbols from executables.

--`threads`
:   (Makerules) Compile and link with thread options enabled. Not
    implemented yet.

--`variants`\[=`pattern`\]
:   (Makerules) Select only `cc-``variant` directories matching
    `pattern`. If the option value is omitted then `\`` is assumed.

--`view-verify`=`level`
:   (Makerules) Verify that all view root directories exist. If there
    are any missing directories then a `level` diagnostic is printed.

--`virtual`
:   (Makerules) Allow `:MAKE:` to
    [`mkdir`](/web/20150717143740/http://www2.research.att.com/~astopen/man/man1/mkdir.html)(1)
    recursive directories that do not exist in the top view. On
    by default. If `--novirtual` is set then `:MAKE:` warns about
    but ignores virtual recursive directories.

# DIAGNOSTICS

Diagnostic messages are printed on the standard error and are classified
by levels. The level determines if the diagnostic is printed, if it
causes `nmake` to exit, and if it affects the `nmake` exit status.
The levels are:

`&lt;0`
: Debug message, enabled when the absolute value of `level` is greater
    than or equal to the `--debug` level. Debug diagnostics are
    prefixed by `debug`-`level``:`.

`1`
: Warning message, disabled by `--silent`. Warning diagnostics are
    prefixed by `warning```:`

`2`
: Non-fatal error message. Processing continues after the diagnostic,
    but the eventual `nmake` exit status will be non-zero.

`&gt;2`
: Fatal error message. `nmake` exits after the diagnostic (and
    internal cleanup) with exit status `level`-2.

# SEE ALSO

[`3d`](/web/20150717143740/http://www2.research.att.com/~astopen/man/man1/3d.html)(1),
[`ar`](/web/20150717143740/http://www2.research.att.com/~astopen/man/man1/ar.html)(1),
[`cc`](/web/20150717143740/http://www2.research.att.com/~astopen/man/man1/cc.html)(1),
[`coshell`](/web/20150717143740/http://www2.research.att.com/~astopen/man/man1/coshell.html)(1),
[`cpp`](/web/20150717143740/http://www2.research.att.com/~astopen/man/man1/cpp.html)(1),
[`probe`](/web/20150717143740/http://www2.research.att.com/~astopen/man/man1/probe.html)(1),
[`sh`](/web/20150717143740/http://www2.research.att.com/~astopen/man/man1/sh.html)(1)

# FILES

Makefile, makefile
:   default makefiles, tried in order

Makeargs, makeargs
:   default argument files, tried in order

\$MAKELIB/Makeinit.mk
:   engine initialization script

\$MAKELIB/makerules.mo
:   default compiled base rules

`base`.ml
:   make lock file

`base`.mo
:   make object file

`base`.ms
:   make statefile

# CAVEATS

Any variables that are expanded while reading makefiles are `frozen`
into the corresponding `nmake` object file. If the value of a `frozen`
variable changes from one invocation of `nmake` to the next, either in a
command line definition or in the environment, then a warning is issued
and the makefile is automatically recompiled. Most frozen variable
expansions can be deferred by entering `\$(``var``)` as
`\$\$(``var``)``.`
Some commands return nonzero status inappropriately. Use `ignore`
`command` to overcome any difficulties.

`nmake` only detects source files that it builds or those that exist
before `nmake` is executed.

# IMPLEMENTATION

`version`
:   make (AT&T Research) 5.7 2012-06-20

`author`
:   Glenn Fowler &lt;gsf@research.att.com&gt;

`copyright`
:   Copyright (c) 1984-2012 AT&T Intellectual Property

`license`
:   http://www.eclipse.org/org/documents/epl-v10.html

------------------------------------------------------------------------

  -- -- ---------------
        June 21, 2012
  -- -- ---------------


