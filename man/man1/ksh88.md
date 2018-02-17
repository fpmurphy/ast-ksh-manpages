# NAME

ksh88, rksh88 - KornShell 88, a standard/restricted command and
programming language

# SYNOPSIS

`ksh88 ` \[ `±aefhikmnoprstuvx` \] \[ `±o` option \] . . . \[ `-c` string \] \[ arg . . . \]\
`rksh88 ` \[ `±aefhikmnoprstuvx` \] \[ `±o` option \] . . . \[ `-c` string \] \[ arg . . . \]

# DESCRIPTION

`ksh88 ` is a command and programming language that executes commands
read from a terminal or a file. `rksh88 ` is a restricted version of the
command interpreter `ksh88`; it is used to set up login names and
execution environments whose capabilities are more controlled than those
of the standard shell. See `Invocation ` below for the meaning of
arguments to the shell.

## Definitions

A `metacharacter ` is one of the following characters:

: `; & ( ) | &lt; &gt; new-line space tab`

A `blank ` is a `tab` or a `space`. An `identifier ` is a sequence
of letters, digits, or underscores starting with a letter or underscore.
Identifiers are used as names for `functions ` and `variables`. A
`word ` is a sequence of `characters ` separated by one or more
non-quoted `metacharacters`.

A `command ` is a sequence of characters in the syntax of the shell
language. The shell reads each command and carries out the desired
action either directly or by invoking separate utilities. A special
command is a command that is carried out by the shell without creating a
separate process. Except for documented side effects, most special
commands can be implemented as separate utilities.

## Commands

A `simple-command ` is a sequence of `blank ` separated words which may
be preceded by a variable assignment list. (See `Environment ` below.)
The first word specifies the name of the command to be executed. Except
as specified below, the remaining words are passed as arguments to the
invoked command. The command name is passed as argument 0 (see
`exec`(2)). The `value ` of a simple-command is its exit status if it
terminates normally, or (octal) 200+`status ` if it terminates
abnormally (see
[`signal`](/web/20141128030245/http://www2.research.att.com/~astopen/man/man2/signal.html)(2)
for a list of status values).

A `pipeline ` is a sequence of one or more `commands ` separated by
`|`. The standard output of each command but the last is connected by
a
[`pipe`](/web/20141128030245/http://www2.research.att.com/~astopen/man/man2/pipe.html)(2)
to the standard input of the next command. Each command is run as a
separate process; the shell waits for the last command to terminate. The
exit status of a pipeline is the exit status of the last command.

A `list ` is a sequence of one or more pipelines separated by `;`,
`&`, `&&`, or `| |`, and optionally terminated by `;`, `&`, or
`|&`. Of these five symbols, `;`, `&`, and `|&` have equal
precedence, which is lower than that of `&&` and `| |`. The symbols
`&&` and `| |` also have equal precedence. A semicolon (`;`)
causes sequential execution of the preceding pipeline; an ampersand
(`&`) causes asynchronous execution of the preceding pipeline (i.e.,
the shell does `not ` wait for that pipeline to finish). The symbol
`|&` causes asynchronous execution of the preceding command or
pipeline with a two-way pipe established to the parent shell. The
standard input and output of the spawned command can be written to and
read from by the parent Shell using the `-p` option of the special
commands `read` and `print ` described later. The symbol `&&`
( `| |` ) causes the `list ` following it to be executed only if the
preceding pipeline returns a zero (non-zero) value. An arbitrary number
of new-lines may appear in a `list, ` instead of a semicolon, to delimit
a command.

A `command ` is either a simple-command or one of the following. Unless
otherwise stated, the value returned by a command is that of the last
simple-command executed in the command.

`for` `identifier ` \[  `in` `word ` . . . \] `;do` `list ` `;done`
: Each time a `for` command is executed, `identifier ` is set to the
    next `word ` taken from the `in` `word ` list. If `in` `word `
    . . . is omitted, then the `for` command executes the `do`
    `list ` once for each positional parameter that is set (see
    `Parameter Substitution ` below). Execution ends when there are no
    more words in the list.

`select` `identifier ` \[  `in` `word ` . . . \] `;do` `list ` `;done`
: A `select` command prints on standard error (file descriptor 2),
    the set of `word`s, each preceded by a number. If `in` `word `
    . . . is omitted, then the positional parameters are used instead
    (see `Parameter Substitution ` below). The `PS3` prompt is printed
    and a line is read from the standard input. If this line consists of
    the number of one of the listed `word`s, then the value of the
    variable `identifier ` is set to the `word ` corresponding to this
    number. If this line is empty the selection list is printed again.
    Otherwise the value of the variable `identifier ` is set to `null`.
    The contents of the line read from standard input is saved in the
    variable `REPLY`. The `list ` is executed for each selection until
    a `break ` or `end-of-file ` is encountered. If the `REPLY`
    variable is set to `null ` by the execution of `list`, then the
    selection list is printed before displaying the `PS3` prompt for
    the next selection.

`case` `word ` `in` \[  \[ `(` \]`pattern ` \[  | `pattern `  \] . . . `)` `list ` `;;`  \] . . . `esac`
: A `case` command executes the `list ` associated with the first
    `pattern ` that matches `word`. The form of the patterns is the same
    as that used for file-name generation (see `File Name
    Generation ` below).

`if` `list ` `;then` `list ` \[  `elif` `list ` `;then` `list `  \] . . . \[  `;else` `list `  \] `;fi`
: The `list ` following `if` is executed and, if it returns a zero
    exit status, the `list ` following the first `then` is executed.
    Otherwise, the `list ` following `elif` is executed and, if its
    value is zero, the `list ` following the next `then` is executed.
    Failing that, the `else` `list ` is executed. If no `else`
    `list ` or `then` `list ` is executed, then the `if` command
    returns a zero exit status.

`while` `list ` `;do` `list ` `;done`

:

`until` `list ` `;do` `list ` `;done`
: A `while` command repeatedly executes the `while` `list ` and,
    if the exit status of the last command in the list is zero, executes
    the `do` `list`; otherwise the loop terminates. If no commands in
    the `do` `list ` are executed, then the `while` command returns
    a zero exit status; `until` may be used in place of `while` to
    negate the loop termination test.

`(``list ``)`
:   Execute `list ` in a separate environment. Note, that if two
    adjacent open parentheses are needed for nesting, a space must be
    inserted to avoid arithmetic evaluation as described below.

`{` `list ``;}`
:   `list ` is simply executed. Note that unlike the metacharacters
    `(` and `)`, `{` and `}` are `reserved word`s and must occur
    at the beginning of a line or after a `;` in order to
    be recognized.

`\[\[``expression ``\]\]`
:   Evaluates `expression ` and returns a zero exit status when
    `expression ` is true. See `Conditional Expressions ` below, for a
    description of `expression`.

`function` `identifier ` `{` `list ` `;}`

:

`identifier ` `() {` `list ` `;}`
: Define a function which is referenced by `identifier`. The body of
    the function is the `list ` of commands between `{` and `}`.
    (See `Functions ` below).

`time` `pipeline `
:   The `pipeline ` is executed and the elapsed time as well as the user
    and system time are printed on standard error.

The following reserved words are only recognized as the first word of a
command and when not quoted:

:

`if then else elif fi case esac for while until do done { } function
select time \[\[ \]\]`

## Comments

A word beginning with `\#` causes that word and all the following
characters up to a new-line to be ignored.

## Aliasing

The first word of each command is replaced by the text of an `alias`
if an `alias` for this word has been defined. An `alias` name
consists of any number of characters excluding metacharacters, quoting
characters, file expansion characters, parameter and command
substitution characters, and `=`. The replacement string can contain
any valid Shell script including the metacharacters listed above. The
first word of each command in the replaced text, other than any that are
in the process of being replaced, will be tested for aliases. If the
last character of the alias value is a `blank ` then the word following
the alias will also be checked for alias substitution. Aliases can be
used to redefine special builtin commands but cannot be used to redefine
the reserved words listed above. Aliases can be created, listed, and
exported with the `alias` command and can be removed with the
`unalias` command. Exported aliases remain in effect for scripts
invoked by name, but must be reinitialized for separate invocations of
the Shell (see `Invocation ` below).

`Aliasing ` is performed when scripts are read, not while they are
executed. Therefore, for an alias to take effect the `alias`
definition command has to be executed before the command which
references the alias is read.

Aliases are frequently used as a short hand for full path names. An
option to the aliasing facility allows the value of the alias to be
automatically set to the full pathname of the corresponding command.
These aliases are called `tracked` aliases. The value of a `tracked`
alias is defined the first time the corresponding command is looked up
and becomes undefined each time the `PATH` variable is reset. These
aliases remain `tracked` so that the next subsequent reference will
redefine the value. Several tracked aliases are compiled into the shell.
The `-h` option of the `set` command makes each referenced command
name into a tracked alias.

The following `exported aliases` are compiled into the shell but can be
unset or redefined:

:

    `autoload='typeset -fu'`

    :

    `false='let 0'`

    :

    `functions='typeset -f'`

    :

    `hash='alias -t'`

    :

    `history='fc -l'`

    :

    `integer='typeset -i'`

    :

    `nohup='nohup '`

    :

    `r='fc -e -'`

    :

    `true=':'`

    :

    `type='whence -v'`

    :

## Tilde Substitution

After alias substitution is performed, each word is checked to see if it
begins with an unquoted `\~`. If it does, then the word up to a `/`
is checked to see if it matches a user name in the `/etc/passwd` file.
If a match is found, the `\~` and the matched login name are replaced
by the login directory of the matched user. This is called a `tilde`
substitution. If no match is found, the original text is left unchanged.
A `\~` by itself, or in front of a `/`, is replaced by `\$HOME`. A
`\~` followed by a `+` or `-` is replaced by `\$PWD` and
`\$OLDPWD` respectively.

In addition, `tilde` substitution is attempted when the value of a
`variable assignment` begins with a `\~`.

## Command Substitution

The standard output from a command enclosed in parenthesis preceded by a
dollar sign ( `\$( )` ) or a pair of grave accents ( `\` \`` ) may
be used as part or all of a word; trailing new-lines are removed. In the
second (archaic) form, the string between the quotes is processed for
special quoting characters before the command is executed. (See
`Quoting ` below.) The command substitution  `\$( cat file )`  can be
replaced by the equivalent but faster  `\$( &lt;file )` . Command
substitution of most special commands that do not perform input/output
redirection are carried out without creating a separate process.

An arithmetic expression enclosed in double parenthesis preceded by a
dollar sign ( `\$(( ))` ) is replaced by the value of the arithmetic
expression within the double parenthesis.

## Process Substitution

This feature is only available on versions of the UNIX operating system
that support the `/dev/fd` directory for naming open files. Each
command argument of the form `&lt;(``list ``)` or
`&gt;(``list ``)` will run process `list` asynchronously connected
to some file in `/dev/fd`. The name of this file will become the
argument to the command. If the form with `&gt;` is selected then
writing on this file will provide input for `list`. If `&lt;` is used,
then the file passed as an argument will contain the output of the
`list` process. For example,

: `paste &lt;(cut -f1` `file1``) &lt;(cut -f3` `file2``) |
    tee &gt;(``process1``) &gt;(``process2``)`

`cuts` fields 1 and 3 from the files `file1` and `file2` respectively,
`pastes` the results together, and sends it to the processes `process1`
and `process2`, as well as putting it onto the standard output. Note
that the file, which is passed as an argument to the command, is a UNIX
[`pipe`](/web/20141128030245/http://www2.research.att.com/~astopen/man/man2/pipe.html)(2)
so programs that expect to
[`lseek`](/web/20141128030245/http://www2.research.att.com/~astopen/man/man2/lseek.html)(2)
on the file will not work.

## Parameter Substitution

A `parameter ` is an `identifier`, one or more digits, or any of the
characters `\``, `@`, `\#`, `?`, `-`, `\$`, and `!\\ `. A
`variable ` (a parameter denoted by an identifier) has a `value ` and
zero or more `attributes`. `Variables ` can be assigned `values ` and
`attributes` by using the `typeset ` special command. The attributes
supported by the Shell are described later with the `typeset ` special
command. Exported variables pass values and attributes to the
environment.

The shell supports a one-dimensional array facility. An element of an
array variable is referenced by a `subscript`. A `subscript ` is denoted
by a `\[`, followed by an `arithmetic expression ` (see `Arithmetic evaluation` below) followed by a `\]`. To assign values to an array,
use `set -A` `name` `value` . . . . The value of all subscripts must
be in the range of 0 through 1023. Arrays need not be declared. Any
reference to a variable with a valid subscript is legal and an array
will be created if necessary. Referencing an array without a subscript
is equivalent to referencing the element zero.

The `value ` of a `variable ` may be assigned by writing:

: `name``=``value  ` \[  `name``=``value `  \] . . .

If the integer attribute, `-i`, is set for `name ` the `value ` is
subject to arithmetic evaluation as described below.

Positional parameters, parameters denoted by a number, may be assigned
values with the `set ` special command. Parameter `\$0` is set from
argument zero when the shell is invoked.

The character `\$` is used to introduce substitutable `parameters`.

`\${``parameter ``}`
: The shell reads all the characters from `\${` to the matching
    `}` as part of the same word even if it contains braces or
    metacharacters. The value, if any, of the parameter is substituted.
    The braces are required when `parameter ` is followed by a letter,
    digit, or underscore that is not to be interpreted as part of its
    name or when a variable is subscripted. If `parameter ` is one or
    more digits then it is a positional parameter. A positional
    parameter of more than one digit must be enclosed in braces. If
    `parameter ` is `\`` or `@`, then all the positional parameters,
    starting with `\$1`, are substituted (separated by a field
    separator character). If an array `identifier ` with subscript
    `\`` or `@` is used, then the value for each of the elements is
    substituted (separated by a field separator character).

`\${\#``parameter ``}`
: If `parameter ` is `\`` or `@`, the number of positional
    parameters is substituted. Otherwise, the length of the value of the
    `parameter ` is substituted.

`\${\#``identifier``\[\`\]}`
: The number of elements in the array `identifier ` is substituted.

`\${``parameter ``:-``word ``}`
: If `parameter ` is set and is non-null then substitute its value;
    otherwise substitute `word`.

`\${``parameter ``:=``word ``}`
: If `parameter ` is not set or is null then set it to `word`; the
    value of the parameter is then substituted. Positional parameters
    may not be assigned to in this way.

`\${``parameter ``:?``word ``}`
: If `parameter ` is set and is non-null then substitute its value;
    otherwise, print `word ` and exit from the shell. If `word ` is
    omitted then a standard message is printed.

`\${``parameter ``:+``word ``}`
: If `parameter ` is set and is non-null then substitute `word`;
    otherwise substitute nothing.

`\${``parameter ``\#``pattern ``}`

:

`\${``parameter ``\#\#``pattern ``}`
: If the Shell `pattern ` matches the beginning of the value of
    `parameter`, then the value of this substitution is the value of the
    `parameter ` with the matched portion deleted; otherwise the value
    of this `parameter ` is substituted. In the first form the smallest
    matching pattern is deleted and in the second form the largest
    matching pattern is deleted. The result is unspecified when
    `parameter ` is `@`, `\``, or an array variable with subscript
    `@`, or `\``.

`\${``parameter ``%``pattern ``}`

:

`\${``parameter ``%%``pattern ``}`
: If the Shell `pattern ` matches the end of the value of `parameter`,
    then the value of this substitution is the value of the `parameter `
    with the matched part deleted; otherwise substitute the value of
    `parameter`. In the first form the smallest matching pattern is
    deleted and in the second form the largest matching pattern is
    deleted. The result is unspecified when `parameter ` is `@`,
    `\``, or an array variable with subscript `@`, or `\``.

In the above, `word ` is not evaluated unless it is to be used as the
substituted string, so that, in the following example, `pwd ` is
executed only if `d ` is not set or is null:

: echo  \${d:- \$( pwd ) }

If the colon ( `: )` is omitted from the above expressions, then the
shell only checks whether `parameter ` is set or not.

The following parameters are automatically set by the shell:

:

    `\#`
    : The number of positional parameters in decimal.

    `-`
    : Flags supplied to the shell on invocation or by the
        `set` command.

    `?`
    : The decimal value returned by the last executed command.

    `\$`
    : The process number of this shell.

    `\_`
    : Initially, the value of `\_` is an absolute pathname of the
        shell or script being executed as passed in the `environment`.
        Subsequently it is assigned the last argument of the previous
        command. This parameter is not set for commands which are
        asynchronous. This parameter is also used to hold the name of
        the matching `MAIL` file when checking for mail.

    `!`
    : The process number of the last background command invoked.

    `ERRNO`
    : The value of `errno` as set by the most recently failed system
        call. This value is system dependent and is intended for
        debugging purposes.

    `LINENO`
    : The line number of the current line within the script or
        function being executed.

    `OLDPWD`
    : The previous working directory set by the `cd` command.

    `OPTARG`
    : The value of the last option argument processed by the
        `getopts` special command.

    `OPTIND`
    : The index of the last option argument processed by the
        `getopts` special command.

    `PPID`
    : The process number of the parent of the shell.

    `PWD`
    : The present working directory set by the `cd` command.

    `RANDOM`
    : Each time this variable is referenced, a random integer,
        uniformly distributed between 0 and 32767, is generated. The
        sequence of random numbers can be initialized by assigning a
        numeric value to `RANDOM`.

    `REPLY`
    : This variable is set by the `select` statement and by the
        `read` special command when no arguments are supplied.

    `SECONDS`
    : Each time this variable is referenced, the number of seconds
        since shell invocation is returned. If this variable is assigned
        a value, then the value returned upon reference will be the
        value that was assigned plus the number of seconds since
        the assignment.

The following variables are used by the shell:

:

    `CDPATH`
    : The search path for the `cd` command.

    `COLUMNS`
    : If this variable is set, the value is used to define the width
        of the edit window for the shell edit modes and for printing
        `select` lists.

    `EDITOR`
    : If the value of this variable ends in `emacs`, `gmacs`, or `vi`
        and the `VISUAL` variable is not set, then the corresponding
        option (see Special Command `set` below) will be turned on.

    `ENV`
    : If this variable is set, then parameter substitution is
        performed on the value to generate the pathname of the script
        that will be executed when the `shell ` is invoked. (See
        `Invocation ` below.) This file is typically used for `alias`
        and `function` definitions.

    `FCEDIT`
    : The default editor name for the `fc` command.

    `FPATH`
    : The search path for function definitions. By default the
        `FPATH` directories are searched after the `PATH` variable.
        If an executable file is found, then it is read and executed in
        the current environment. `FPATH` is searched before `PATH`
        when a function with the `-u` attribute is referenced. The
        preset alias `autoload` preset alias causes a function with
        the `-u` attribute to be created.

    `IFS`
    : Internal field separators, normally `space`, `tab`, and
        `new-line` that are used to separate command words which
        result from command or parameter substitution and for separating
        words with the special command `read`. The first character of
        the `IFS` variable is used to separate arguments for the
        `"\$\`"` substitution (See `Quoting` below).

    `HISTFILE`
    : If this variable is set when the shell is invoked, then the
        value is the pathname of the file that will be used to store the
        command history. (See `Command re-entry ` below.)

    `HISTSIZE`
    : If this variable is set when the shell is invoked, then the
        number of previously entered commands that are accessible by
        this shell will be greater than or equal to this number. The
        default is 128.

    `HOME`
    : The default argument (home directory) for the `cd` command.

    `LINES`
    : If this variable is set, the value is used to determine the
        column length for printing `select` lists. Select lists will
        print vertically until about two-thirds of `LINES` lines
        are filled.

    `MAIL`
    : If this variable is set to the name of a mail file `and ` the
        `MAILPATH` variable is not set, then the shell informs the
        user of arrival of mail in the specified file.

    `MAILCHECK`
    : This variable specifies how often (in seconds) the shell will
        check for changes in the modification time of any of the files
        specified by the `MAILPATH` or `MAIL` variables. The default
        value is 600 seconds. When the time has elapsed the shell will
        check before issuing the next prompt.

    `MAILPATH`
    : A colon ( `:` ) separated list of file names. If this variable
        is set then the shell informs the user of any modifications to
        the specified files that have occurred within the last
        `MAILCHECK` seconds. Each file name can be followed by a `?`
        and a message that will be printed. The message will undergo
        parameter substitution with the variable `\$\_` defined as the
        name of the file that has changed. The default message is `you
        have mail in \$\_ .`

    `PATH`
    : The search path for commands (see `Execution ` below). The user
        may not change `PATH` if executing under `rksh88 ` (except in
        `.profile ).`

    `PS1`
    : The value of this variable is expanded for parameter
        substitution to define the primary prompt string which by
        default is \`\``\$  `''. The character `!` in the primary
        prompt string is replaced by the `command ` number (see `Command
        Re-entry` below). Two successive occurrences of `!` will
        produce a single `!` when the prompt string is printed.

    `PS2`
    : Secondary prompt string, by default \`\``&gt; `''.

    `PS3`
    : Selection prompt string used within a `select` loop, by
        default \`\``\#? `''.

    `PS4`
    : The value of this variable is expanded for parameter
        substitution and precedes each line of an execution trace. If
        omitted, the execution trace prompt is \`\``+  `''.

    `SHELL`
    : The pathname of the `shell ` is kept in the environment. At
        invocation, if the basename of this variable is `rsh`,
        `rksh`, or `krsh`, then the shell becomes restricted.

    `TMOUT`
    : If set to a value greater than zero, the shell will terminate if
        a command is not entered within the prescribed number of seconds
        after issuing the `PS1` prompt. (Note that the shell can be
        compiled with a maximum bound for this value which cannot
        be exceeded.)

    `VISUAL`
    : If the value of this variable ends in `emacs`, `gmacs`, or `vi`
        then the corresponding option (see Special Command `set`
        below) will be turned on.

The shell gives default values to `PATH`, `PS1`, `PS2`, `PS3`,
`PS4`, `MAILCHECK`, `FCEDIT`, `TMOUT` and `IFS`, while
`HOME`, `SHELL` `ENV` and `MAIL` are not set at all by the shell
(although `HOME` `is ` set by `login`(1)). On some systems `MAIL`
and `SHELL` are also set by
[`login`](/web/20141128030245/http://www2.research.att.com/~astopen/man/man1/login.html)(1).

## Blank Interpretation

After parameter and command substitution, the results of substitutions
are scanned for the field separator characters (those found in `IFS `
) and split into distinct arguments where such characters are found.
Explicit null arguments ( `" "` or `' '` ) are retained. Implicit
null arguments (those resulting from `parameters ` that have no values)
are removed.

## File Name Generation

Following substitution, each command `word ` is scanned for the
characters `\``, `?`, and `\[  ` unless the `-f` option has been `set`. If one of these characters appears then the word is regarded as
a `pattern`. The word is replaced with lexicographically sorted file
names that match the pattern. If no file name is found that matches the
pattern, then the word is left unchanged. When a `pattern ` is used for
file name generation, the character `.` at the start of a file name or
immediately following a `/`, as well as the character `/` itself,
must be matched explicitly. In other instances of pattern matching the
`/` and `.` are not treated specially.

:

    `\``
    : Matches any string, including the null string.

    `?`
    : Matches any single character.

    `\[ ` . . . ` \]`
    : Matches any one of the enclosed characters. A pair of characters
        separated by `-` matches any character lexically between the
        pair, inclusive. If the first character following the opening
        "\[  " is a "! " then any character not enclosed is matched. A `-` can be included in the character set by putting it as the
        first or last character.

A `pattern-list` is a list of one or more patterns separated from each
other with a `|`. Composite patterns can be formed with one or more of
the following:

:

    `?(``pattern-list ``)`
    : Optionally matches any one of the given patterns.

    `\`(``pattern-list ``)`
    : Matches zero or more occurrences of the given patterns.

    `+(``pattern-list ``)`
    : Matches one or more occurrences of the given patterns.

    `@(``pattern-list ``)`
    : Matches exactly one of the given patterns.\

    `!(``pattern-list ``)`
    : Matches anything, except one of the given patterns.

## Quoting

Each of the `metacharacters ` listed above (See `Definitions` above) has
a special meaning to the shell and causes termination of a word unless
quoted. A character may be `quoted ` (i.e., made to stand for itself) by
preceding it with a `\\`. The pair `\\new-line` is removed. All
characters enclosed between a pair of single quote marks ( `' '` ),
are quoted. A single quote cannot appear within single quotes. Inside
double quote marks (`" "`), parameter and command substitution occur
and `\\` quotes the characters `\\`, `\``, `"`, and `\$`. The
meaning of `\$\`` and `\$@` is identical when not quoted or when
used as a parameter assignment value or as a file name. However, when
used as a command argument, `"\$\`"` is equivalent to
`"\$1``d`` \$2``d` . . .`"`, where `d` is the first character of
the `IFS` variable, whereas `"\$@"` is equivalent to `"\$1" `
`"\$2" ` . . . . Inside grave quote marks (`\` \``) `\\` quotes
the characters `\\`, `\``, and `\$`. If the grave quotes occur
within double quotes then `\\` also quotes the character `"`.

The special meaning of reserved words or aliases can be removed by
quoting any character of the reserved word. The recognition of function
names or special command names listed below cannot be altered by quoting
them.

## Arithmetic Evaluation

An ability to perform integer arithmetic is provided with the special
command `let`. Evaluations are performed using `long ` arithmetic.
Constants are of the form \[ `base``\# ` \]`n ` where `base ` is a
decimal number between two and thirty-six representing the arithmetic
base and `n ` is a number in that base. If `base ` is omitted then base
10 is used.

An arithmetic expression uses the same syntax, precedence, and
associativity of expression as the C language. All the integral
operators, other than `++`, `- -`, `?:`, and `,` are supported.
Variables can be referenced by name within an arithmetic expression
without using the parameter substitution syntax. When a variable is
referenced, its value is evaluated as an arithmetic expression.

An internal integer representation of a `variable ` can be specified
with the `-i` option of the `typeset` special command. Arithmetic
evaluation is performed on the value of each assignment to a variable
with the `-i` attribute. If you do not specify an arithmetic base, the
first assignment to the variable determines the arithmetic base. This
base is used when parameter substitution occurs.

Since many of the arithmetic operators require quoting, an alternative
form of the `let` command is provided. For any command which begins
with a `((`, all the characters until a matching `))` are treated as
a quoted expression. More precisely, `((`. . .`))` is equivalent to
`let ` `"` . . .`"`.

## Prompting

When used interactively, the shell prompts with the parameter expanded
value of `PS1` before reading a command. If at any time a new-line is
typed and further input is needed to complete a command, then the
secondary prompt (i.e., the value of `PS2`) is issued.

## Conditional Expressions

A `conditional expression` is used with the `\[\[` compound command to test attributes of files and to compare strings. Word splitting and file
name generation are not performed on the words between `\[\[` and `\]\]`. Each expression can be constructed from one or more of the
following unary or binary expressions:

`-a` `file`
: True, if `file` exists.

`-b` `file`
: True, if `file` exists and is a block special file.

`-c` `file`
: True, if `file` exists and is a character special file.

`-d` `file`
: True, if `file` exists and is a directory.

`-f` `file`
: True, if `file` exists and is an ordinary file.

`-g` `file`
: True, if `file` exists and is has its setgid bit set.

`-k` `file`
: True, if `file` exists and is has its sticky bit set.

`-n` `string`
: True, if length of `string` is non-zero.

`-o` `option`
: True, if option named `option` is on.

`-p` `file`
: True, if `file` exists and is a fifo special file or a pipe.

`-r` `file`
: True, if `file` exists and is readable by current process.

`-s` `file`
: True, if `file` exists and has size greater than zero.

`-t` `fildes`
: True, if file descriptor number `fildes` is open and associated with
    a terminal device.

`-u` `file`
: True, if `file` exists and is has its setuid bit set.

`-w` `file`
: True, if `file` exists and is writable by current process.

`-x` `file`
: True, if `file` exists and is executable by current process. If
    `file` exists and is a directory, then the current process has
    permission to search in the directory.

`-z` `string`
: True, if length of `string` is zero.

`-L` `file`
: True, if `file` exists and is a symbolic link.

`-O` `file`
: True, if `file` exists and is owned by the effective user id of
    this process.

`-G` `file`
: True, if `file` exists and its group matches the effective group id
    of this process.

`-S` `file`
: True, if `file` exists and is a socket.

`file1` `-nt` `file2`
: True, if `file1` exists and is newer than `file2`.

`file1` `-ot` `file2`
: True, if `file1` exists and is older than `file2`.

`file1` `-ef` `file2`
: True, if `file1` and `file2` exist and refer to the same file.

`string` `=` `pattern`
: True, if `string` matches `pattern`.

`string` `!=` `pattern`
: True, if `string` does not match `pattern`.

`string1` `&lt;` `string2`
: True, if `string1` comes before `string2` based on ASCII value of
    their characters.

`string1` `&gt;` `string2`
: True, if `string1` comes after `string2` based on ASCII value of
    their characters.

`exp1` `-eq` `exp2`
: True, if `exp1` is equal to `exp2`.

`exp1` `-ne` `exp2`
: True, if `exp1` is not equal to `exp2`.

`exp1` `-lt` `exp2`
: True, if `exp1` is less than `exp2`.

`exp1` `-gt` `exp2`
: True, if `exp1` is greater than `exp2`.

`exp1` `-le` `exp2`
: True, if `exp1` is less than or equal to `exp2`.

`exp1` `-ge` `exp2`
: True, if `exp1` is greater than or equal to `exp2`.

In each of the above expressions, if `file` is of the form
`/dev/fd/``n`, where `n` is an integer, then the test is applied to
the open file whose descriptor number is `n`.

A compound expression can be constructed from these primitives by using
any of the following, listed in decreasing order of precedence.

`(``expression``)`
: True, if `expression` is true. Used to group expressions.

`!` `expression`
: True if `expression` is false.

`expression1` `&&` `expression2`
: True, if `expression1` and `expression2` are both true.

`expression1` `||` `expression2`
: True, if either `expression1` or `expression2` is true.

## Input/Output

Before a command is executed, its input and output may be redirected
using a special notation interpreted by the shell. The following may
appear anywhere in a simple-command or may precede or follow a
`command ` and are `not ` passed on to the invoked command. Command and
parameter substitution occur before `word ` or `digit ` is used except
as noted below. File name generation occurs only if the pattern matches
a single file, and blank interpretation is not performed.

`&lt;``word`
: Use file `word ` as standard input (file descriptor 0).

`&gt;``word`
: Use file `word ` as standard output (file descriptor 1). If the file
    does not exist then it is created. If the file exists, and the
    `noclobber` option is on, this causes an error; otherwise, it is
    truncated to zero length.

`&gt;|``word`
: Sames as `&gt;`, except that it overrides the
    `noclobber` option.

`&gt;&gt;``word`
: Use file `word ` as standard output. If the file exists then output
    is appended to it (by first seeking to the end-of-file); otherwise,
    the file is created.

`&lt;&gt;``word`
: Open file `word ` for reading and writing as standard input.

`&lt;&lt;`\[ `-` \]`word`
: The shell input is read up to a line that is the same as `word`, or
    to an end-of-file. No parameter substitution, command substitution
    or file name generation is performed on `word`. The resulting
    document, called a `here-document`, becomes the standard input. If
    any character of `word ` is quoted, then no interpretation is placed
    upon the characters of the document; otherwise, parameter and
    command substitution occur, `\\new-line` is ignored, and `\\`
    must be used to quote the characters `\\`, `\$`, `\``, and the
    first character of `word`. If `-` is appended to `&lt;&lt;`,
    then all leading tabs are stripped from `word ` and from
    the document.

`&lt;&``digit`
: The standard input is duplicated from file descriptor `digit` (see
    `dup`(2)). Similarly for the standard output using
    `&gt;& ``digit`.

`&lt;&-`
: The standard input is closed. Similarly for the standard output
    using `&gt;&-`.

`&lt;&p`
: The input from the co-process is moved to standard input.

`&gt;&p`
: The output to the co-process is moved to standard output.

If one of the above is preceded by a digit, then the file descriptor
number referred to is that specified by the digit (instead of the
default 0 or 1). For example:

: . . . 2&gt;&1

means file descriptor 2 is to be opened for writing as a duplicate of
file descriptor 1.

The order in which redirections are specified is significant. The shell
evaluates each redirection in terms of the (`file descriptor`, `file`)
association at the time of evaluation. For example:

: . . . 1&gt;`fname ` 2&gt;&1

first associates file descriptor 1 with file `fname `. It then
associates file descriptor 2 with the file associated with file
descriptor 1 (i.e. `fname `). If the order of redirections were
reversed, file descriptor 2 would be associated with the terminal
(assuming file descriptor 1 had been) and then file descriptor 1 would
be associated with file `fname `.

If a command is followed by `&` and job control is not active, then
the default standard input for the command is the empty file
`/dev/null`. Otherwise, the environment for the execution of a command
contains the file descriptors of the invoking shell as modified by
input/output specifications.

## Environment

The `environment ` (see `environ`(7)) is a list of name-value pairs that
is passed to an executed program in the same way as a normal argument
list. The names must be `identifiers ` and the values are character
strings. The shell interacts with the environment in several ways. On
invocation, the shell scans the environment and creates a variable for
each name found, giving it the corresponding value and marking it
`export`. Executed commands inherit the environment. If the user
modifies the values of these variables or creates new ones, using the
`export` or `typeset -x` commands they become part of the
environment. The environment seen by any executed command is thus
composed of any name-value pairs originally inherited by the shell,
whose values may be modified by the current shell, plus any additions
which must be noted in `export` or `typeset -x` commands.

The environment for any `simple-command ` or function may be augmented
by prefixing it with one or more variable assignments. A variable
assignment argument is a word of the form `identifier=value`. Thus:

: TERM=450  cmd  args and\
    (export  TERM; TERM=450; cmd  args)

are equivalent (as far as the above execution of `cmd ` is concerned
except for special commands listed below that are preceded with a
dagger).

If the `-k` flag is set, `all ` variable assignment arguments are
placed in the environment, even if they occur after the command name.
The following first prints `a=b c` and then `c`:

: echo  a=b  c
        set  -k
        echo  a=b  c

This feature is intended for use with scripts written for early versions
of the shell and its use in new scripts is strongly discouraged. It is
likely to disappear someday.

## Functions

The `function ` reserved word, described in the `Commands` section
above, is used to define shell functions. Shell functions are read in
and stored internally. Alias names are resolved when the function is
read. Functions are executed like commands with the arguments passed as
positional parameters. (See `Execution` below.)

Functions execute in the same process as the caller and share all files
and present working directory with the caller. Traps caught by the
caller are reset to their default action inside the function. A trap
condition that is not caught or ignored by the function causes the
function to terminate and the condition to be passed on to the caller. A
trap on `EXIT` set inside a function is executed after the function
completes in the environment of the caller. Ordinarily, variables are
shared between the calling program and the function. However, the
`typeset` special command used within a function defines local
variables whose scope includes the current function and all functions it
calls.

The special command `return` is used to return from function calls.
Errors within functions return control to the caller.

Function identifiers can be listed with the `-f` or `+f` option of
the `typeset` special command. The text of functions will also be
listed with `-f`. Functions can be undefined with the `-f` option of
the `unset` special command.

Ordinarily, functions are unset when the shell executes a shell script.
The `-xf` option of the `typeset` command allows a function to be
exported to scripts that are executed without a separate invocation of
the shell. Functions that need to be defined across separate invocations
of the shell should be specified in the `ENV` file with the `-xf`
option of `typeset`.

## Jobs

If the `monitor` option of the `set` command is turned on, an
interactive shell associates a `job` with each pipeline. It keeps a
table of current jobs, printed by the `jobs` command, and assigns them
small integer numbers. When a job is started asynchronously with `&`,
the shell prints a line which looks like:

``

           [1] 1234

indicating that the job which was started asynchronously was job number
1 and had one (top-level) process, whose process id was 1234.

This paragraph and the next require features that are not in all
versions of UNIX and may not apply. If you are running a job and wish to
do something else you may hit the key `\^Z` (control-Z) which sends a
STOP signal to the current job. The shell will then normally indicate
that the job has been \`Stopped', and print another prompt. You can then
manipulate the state of this job, putting it in the background with the
`bg` command, or run some other commands and then eventually bring the
job back into the foreground with the foreground command `fg`. A
`\^Z` takes effect immediately and is like an interrupt in that
pending output and unread input are discarded when it is typed.

A job being run in the background will stop if it tries to read from the
terminal. Background jobs are normally allowed to produce output, but
this can be disabled by giving the command \`\`stty tostop''. If you set
this tty option, then background jobs will stop when they try to produce
output like they do when they try to read input.

There are several ways to refer to jobs in the shell. A job can be
referred to by the process id of any process of the job or by one of the
following:

`%``number`
: The job with the given number.

`%``string`
: Any job whose command line begins with `string`.

`%?``string`
: Any job whose command line contains `string`.

`%%`
: Current job.

`%+`
: Equivalent to `%%`.

`%-`
: Previous job.

The shell learns immediately whenever a process changes state. It
normally informs you whenever a job becomes blocked so that no further
progress is possible, but only just before it prints a prompt. This is
done so that it does not otherwise disturb your work.

When the monitor mode is on, each background job that completes triggers
any trap set for `CHLD`.

When you try to leave the shell while jobs are running or stopped, you
will be warned that \`You have stopped(running) jobs.' You may use the
`jobs` command to see what they are. If you do this or immediately try
to exit again, the shell will not warn you a second time, and the
stopped jobs will be terminated.

## Signals

The INT and QUIT signals for an invoked command are ignored if the
command is followed by `&` and the `monitor` option is not active.
Otherwise, signals have the values inherited by the shell from its
parent (but see also the `trap` special command below).

## Execution

Each time a command is executed, the above substitutions are carried
out. If the command name matches one of the `Special Commands ` listed
below, it is executed within the current shell process. Next, the
command name is checked to see if it matches one of the user defined
functions. If it does, the positional parameters are saved and then
reset to the arguments of the `function ` call. When the `function `
completes or issues a `return`, the positional parameter list is
restored and any trap set on `EXIT` within the function is executed.
The value of a `function ` is the value of the last command executed. A
function is also executed in the current shell process. If a command
name is not a `special command ` or a user defined `function`, a process
is created and an attempt is made to execute the command via
[`exec`](/web/20141128030245/http://www2.research.att.com/~astopen/man/man2/exec.html)(2).

The shell variable `PATH` defines the search path for the directory
containing the command. Alternative directory names are separated by a
colon (`:`). The default path is `/bin:/usr/bin:` (specifying
`/bin`, `/usr/bin`, and the current directory in that order). The
current directory can be specified by two or more adjacent colons, or by
a colon at the beginning or end of the path list. If the command name
contains a `/` then the search path is not used. Otherwise, each
directory in the path is searched for an executable file. If the file
has execute permission but is not a directory or an `a.out` file, it
is assumed to be a file containing shell commands. A sub-shell is
spawned to read it. All non-exported aliases, functions, and variables
are removed in this case. If the shell command file doesn't have read
permission, or if the `setuid` and/or `setgid` bits are set on the file,
then the shell executes an agent whose job it is to set up the
permissions and execute the shell with the shell command file passed
down as an open file. A parenthesized command is executed in a sub-shell
without removing non-exported quantities.

## Command Re-entry

The text of the last `HISTSIZE` (default 128) commands entered from a
terminal device is saved in a `history` file. The file
`\$HOME/.sh\_history` is used if the `HISTFILE` variable is not set
or if the file it names is not writable. A shell can access the commands
of all `interactive` shells which use the same named `HISTFILE`. The
special command `fc ` is used to list or edit a portion of this file.
The portion of the file to be edited or listed can be selected by number
or by giving the first character or characters of the command. A single
command or range of commands can be specified. If you do not specify an
editor program as an argument to `fc ` then the value of the variable
`FCEDIT` is used. If `FCEDIT` is not defined then `/bin/ed` is
used. The edited command(s) is printed and re-executed upon leaving the
editor. The editor name `-` is used to skip the editing phase and to
re-execute the command. In this case a substitution parameter of the
form `old``=``new` can be used to modify the command before execution.
For example, if `r` is aliased to `'fc -e -'` then typing \``r
bad=good c`' will re-execute the most recent command which starts with
the letter `c`, replacing the first occurrence of the string `bad`
with the string `good`.

## In-line Editing Options

Normally, each command line entered from a terminal device is simply
typed followed by a new-line (\`RETURN' or \`LINE FEED'). If either the
`emacs`, `gmacs`, or `vi` option is active, the user can edit the
command line. To be in either of these edit modes `set` the
corresponding option. An editing option is automatically selected each
time the `VISUAL` or `EDITOR` variable is assigned a value ending in
either of these option names.

The editing features require that the user's terminal accept \`RETURN'
as carriage return without line feed and that a space (\` ') must
overwrite the current character on the screen. ADM terminal users should
set the "space - advance" switch to \`space'. Hewlett-Packard series
2621 terminal users should set the straps to \`bcGHxZ etX'.

The editing modes implement a concept where the user is looking through
a window at the current line. The window width is the value of
`COLUMNS` if it is defined, otherwise 80. If the window width is too
small to display the prompt and leave at least 8 columns to enter input,
the prompt is truncated from the left. If the line is longer than the
window width minus two, a mark is displayed at the end of the window to
notify the user. As the cursor moves and reaches the window boundaries
the window will be centered about the cursor. The mark is a `&gt;`
(&lt;`,` `\``) if the line extends on the right (left, both) side(s)
of the window.

The search commands in each edit mode provide access to the history
file. Only strings are matched, not patterns, although a leading `\^`
in the string restricts the match to begin at the first character in the
line.

## Emacs Editing Mode

This mode is entered by enabling either the `emacs` or `gmacs` option.
The only difference between these two modes is the way they handle
`\^T`. To edit, the user moves the cursor to the point needing
correction and then inserts or deletes characters or words as needed.
All the editing commands are control characters or escape sequences. The
notation for control characters is caret ( `\^` ) followed by the
character. For example, `\^F` is the notation for control `F`. This
is entered by depressing \`f' while holding down the \`CTRL' (control)
key. The \`SHIFT' key is `not` depressed. (The notation `\^?`
indicates the DEL (delete) key.)

The notation for escape sequences is `M-` followed by a character. For
example, `M-f` (pronounced Meta f) is entered by depressing ESC (ascii
`033`) followed by \`f'. (`M-F` would be the notation for ESC
followed by \`SHIFT' (capital) \`F'.)

All edit commands operate from any place on the line (not just at the
beginning). Neither the "RETURN" nor the "LINE FEED" key is entered
after edit commands except when noted.

`\^F`
: Move cursor forward (right) one character.

`M-f`

Move cursor forward one word. (The `emacs` editor's idea of a word is
a string of characters consisting of only letters, digits and
underscores.)

`\^B`

Move cursor backward (left) one character.

`M-b`

Move cursor backward one word.

`\^A`

Move cursor to start of line.

`\^E`

Move cursor to end of line.

`\^\]``char`

Move cursor forward to character `char` on current line.

`M-\^\]``char`

Move cursor backward to character `char` on current line.

`\^X\^X`

Interchange the cursor and mark.

`erase`

(User defined erase character as defined by the
[`stty`](/web/20141128030245/http://www2.research.att.com/~astopen/man/man1/stty.html)(1)
command, usually `\^H` or `\#`.) Delete previous character.

`\^D`

Delete current character.

`M-d`

Delete current word.

`M-\^H`

(Meta-backspace) Delete previous word.

`M-h`

Delete previous word.

`M-\^?`

(Meta-DEL) Delete previous word (if your interrupt character is `\^?`
(DEL, the default) then this command will not work).

`\^T`

Transpose current character with next character in `emacs` mode.
Transpose two previous characters in `gmacs` mode.

`\^C`

Capitalize current character.

`M-c`

Capitalize current word.

`M-l`

Change the current word to lower case.

`\^K`

Delete from the cursor to the end of the line. If preceded by a
numerical parameter whose value is less than the current cursor
position, then delete from given position up to the cursor. If preceded
by a numerical parameter whose value is greater than the current cursor
position, then delete from cursor up to given cursor position.

`\^W`

Kill from the cursor to the mark.

`M-p`

Push the region from the cursor to the mark on the stack.

`kill`

(User defined kill character as defined by the stty command, usually
`\^G` or `@`.) Kill the entire current line. If two `kill`
characters are entered in succession, all kill characters from then on
cause a line feed (useful when using paper terminals).

`\^Y`

Restore last item removed from line. (Yank item back to the line.)

`\^L`

Line feed and print current line.

`\^@`

(Null character) Set mark.

`M-``space`

(Meta space) Set mark.

`\^J`

(New line) Execute the current line.

`\^M`

(Return) Execute the current line.

`eof`

End-of-file character, normally `\^D`, is processed as an End-of-file
only if the current line is null.

`\^P`

Fetch previous command. Each time `\^P` is entered the previous
command back in time is accessed. Moves back one line when not on the
first line of a multi-line command.

`M-&lt;`

Fetch the least recent (oldest) history line.

`M-&gt;`

Fetch the most recent (youngest) history line.

`\^N`

Fetch next command line. Each time `\^N` is entered the next command
line forward in time is accessed.

`\^R``string`

Reverse search history for a previous command line containing `string`.
If a parameter of zero is given, the search is forward. `String` is
terminated by a "RETURN" or "NEW LINE". If string is preceded by a
`\^`, the matched line must begin with `string`. If `string` is
omitted, then the next command line containing the most recent `string`
is accessed. In this case a parameter of zero reverses the direction of
the search.

`\^O`

Operate - Execute the current line and fetch the next line relative to
current line from the history file.

`M-``digits`

(Escape) Define numeric parameter, the digits are taken as a parameter
to the next command. The commands that accept a parameter are `\^F`,
`\^B`, `erase`, `\^C`, `\^D`, `\^K`, `\^R`, `\^P`, `\^N`,
`\^\]`, `M-.`, `M-\^\]`, `M-\_`, `M-b`, `M-c`, `M-d`,
`M-f`, `M-h`, `M-l` and `M-\^H`.

`M-``letter`

Soft-key - Your alias list is searched for an alias by the name
`\_``letter` and if an alias of this name is defined, its value will
be inserted on the input queue. The `letter` must not be one of the
above meta-functions.

`M-\[``letter`
Soft-key - Your alias list is searched for an alias by the name
`\_\_``letter` and if an alias of this name is defined, its value will
be inserted on the input queue. The can be used to program functions
keys on many terminals.

`M-.`

The last word of the previous command is inserted on the line. If
preceded by a numeric parameter, the value of this parameter determines
which word to insert rather than the last word.

`M-\_`

Same as `M-.`.

`M-\``

Attempt file name generation on the current word. An asterisk is
appended if the word doesn't match any file or contain any special
pattern characters.

`M-ESC`

File name completion. Replaces the current word with the longest common
prefix of all filenames matching the current word with an asterisk
appended. If the match is unique, a `/` is appended if the file is a
directory and a space is appended if the file is not a directory.

`M-=`

List files matching current word pattern if an asterisk were appended.

`\^U`

Multiply parameter of next command by 4.

`\\`

Escape next character. Editing characters, the user's erase, kill and
interrupt (normally `\^?`) characters may be entered in a command line
or in a search string if preceded by a `\\`. The `\\` removes the
next character's editing features (if any).

`\^V`

Display version of the shell.

`M-\\\#`

Insert a `\\\#` at the beginning of the line and execute it. This
causes a comment to be inserted in the history file.

## Vi Editing Mode

There are two typing modes. Initially, when you enter a command you are
in the `input ` mode. To edit, the user enters `control ` mode by typing
ESC (`033`) and moves the cursor to the point needing correction and
then inserts or deletes characters or words as needed. Most control
commands accept an optional repeat `count` prior to the command.

When in `vi` mode on most systems, canonical processing is initially
enabled and the command will be echoed again if the speed is 1200 baud
or greater and it contains any control characters or less than one
second has elapsed since the prompt was printed. The ESC character
terminates canonical processing for the remainder of the command and the
user can then modify the command line. This scheme has the advantages of
canonical processing with the type-ahead echoing of raw mode.

If the option `viraw ` is also set, the terminal will always have
canonical processing disabled. This mode is implicit for systems that do
not support two alternate end of line delimiters, and may be helpful for
certain terminals.

## Input Edit Commands

: By default the editor is in input mode.

    `erase`
    : (User defined erase character as defined by the stty command,
        usually `\^H` or `\#`.) Delete previous character.

    `\^W`
    : Delete the previous blank separated word.

    `\^D`
    : Terminate the shell.

    `\^V`
    : Escape next character. Editing characters and the user's erase
        or kill characters may be entered in a command line or in a
        search string if preceded by a `\^V`. The `\^V` removes the
        next character's editing features (if any).

    `\\`
    : Escape the next `erase` or `kill` character.

## Motion Edit Commands

: These commands will move the cursor.

    \[`count`\]`l`
    : Cursor forward (right) one character.

    \[`count`\]`w`
    : Cursor forward one alpha-numeric word.

    \[`count`\]`W`
    : Cursor to the beginning of the next word that follows a blank.

    \[`count`\]`e`
    : Cursor to end of word.

    \[`count`\]`E`
    : Cursor to end of the current blank delimited word.

    \[`count`\]`h`
    : Cursor backward (left) one character.

    \[`count`\]`b`
    : Cursor backward one word.

    \[`count`\]`B`
    : Cursor to preceding blank separated word.

    \[`count`\]`|`
    : Cursor to column `count`.

    \[`count`\]`f``c`
    : Find the next character `c` in the current line.

    \[`count`\]`F``c`
    : Find the previous character `c` in the current line.

    \[`count`\]`t``c`
    : Equivalent to `f` followed by `h`.

    \[`count`\]`T``c`
    : Equivalent to `F` followed by `l`.

    \[`count`\]`;`
    : Repeats `count` times, the last single character find command,
        `f`, `F`, `t`, or `T`.

    \[`count`\]`,`
    : Reverses the last single character find command `count` times.

    `0`
    : Cursor to start of line.

    `\^`
    : Cursor to first non-blank character in line.

    `\$`
    : Cursor to end of line.

    `%`
    : Moves to balancing `(`, `)`, `{`, `}`, `\[`, or `\]`. If cursor is not on one of the above characters, the
        remainder of the line is searched for the first occurrence of
        one of the above characters first.

## Search Edit Commands

: These commands access your command history.

    \[`count`\]`k`
    : Fetch previous command. Each time `k` is entered the previous
        command back in time is accessed.

    \[`count`\]`-`
    : Equivalent to `k`.

    \[`count`\]`j`
    : Fetch next command. Each time `j` is entered the next command
        forward in time is accessed.

    \[`count`\]`+`
    : Equivalent to `j`.

    \[`count`\]`G`
    : The command number `count` is fetched. The default is the least
        recent history command.

    `/``string`
    : Search backward through history for a previous command
        containing `string`. `String` is terminated by a "RETURN" or
        "NEW LINE". If string is preceded by a `\^`, the matched line
        must begin with `string`. If `string` is null the previous
        string will be used.

    `?``string`
    : Same as `/` except that search will be in the
        forward direction.

    `n`
    : Search for next match of the last pattern to `/` or
        `?` commands.

    `N`
    : Search for next match of the last pattern to `/` or `?`, but
        in reverse direction. Search history for the `string` entered by
        the previous `/` command.

## Text Modification Edit Commands

: These commands will modify the line.

    `a`
    : Enter input mode and enter text after the current character.

    `A`
    : Append text to the end of the line. Equivalent to `\$a`.

    \[`count`\]`c``motion`

    :

    `c`\[`count`\]`motion`
    : Delete current character through the character that `motion`
        would move the cursor to and enter input mode. If `motion` is
        `c`, the entire line will be deleted and input mode entered.

    `C`
    : Delete the current character through the end of line and enter
        input mode. Equivalent to `c\$`.

    \[`count`\]`s`
    : Delete `count` characters and enter input mode.

    `S`
    : Equivalent to `cc`.

    `D`
    : Delete the current character through the end of line. Equivalent
        to `d\$`.

    \[`count`\]`d``motion`

    :

    `d`\[`count`\]`motion`
    : Delete current character through the character that `motion`
        would move to. If `motion` is `d ,` the entire line will
        be deleted.

    `i`
    : Enter input mode and insert text before the current character.

    `I`
    : Insert text before the beginning of the line. Equivalent to
        `0i`.

    \[`count`\]`P`
    : Place the previous text modification before the cursor.

    \[`count`\]`p`
    : Place the previous text modification after the cursor.

    `R`
    : Enter input mode and replace characters on the screen with
        characters you type overlay fashion.

    \[`count`\]`r``c`
    : Replace the `count` character(s) starting at the current cursor
        position with `c`, and advance the cursor.

    \[`count`\]`x`
    : Delete current character.

    \[`count`\]`X`
    : Delete preceding character.

    \[`count`\]`.`
    : Repeat the previous text modification command.

    \[`count`\]`\~`
    : Invert the case of the `count` character(s) starting at the
        current cursor position and advance the cursor.

    \[`count`\]`\_`
    : Causes the `count ` word of the previous command to be appended
        and input mode entered. The last word is used if `count `
        is omitted.

    `\``
    : Causes an `\`` to be appended to the current word and file
        name generation attempted. If no match is found, it rings the
        bell. Otherwise, the word is replaced by the matching pattern
        and input mode is entered.

    `\\`
    : Filename completion. Replaces the current word with the longest
        common prefix of all filenames matching the current word with an
        asterisk appended. If the match is unique, a `/` is appended
        if the file is a directory and a space is appended if the file
        is not a directory.

## Other Edit Commands

: Miscellaneous commands.

    \[`count`\]`y``motion`

    :

    `y`\[`count`\]`motion`
    : Yank current character through character that `motion` would
        move the cursor to and puts them into the delete buffer. The
        text and cursor are unchanged.

    `Y`
    : Yanks from current position to end of line. Equivalent to
        `y\$`.

    `u`
    : Undo the last text modifying command.

    `U`
    : Undo all the text modifying commands performed on the line.

    \[`count`\]`v`
    : Returns the command `fc -e \${VISUAL:-\${EDITOR:-vi}}` `count`
        in the input buffer. If `count ` is omitted, then the current
        line is used.

    `\^L`
    : Line feed and print current line. Has effect only in
        control mode.

    `\^J`
    : (New line) Execute the current line, regardless of mode.

    `\^M`
    : (Return) Execute the current line, regardless of mode.

    `\\\#`
    : If the first character of the command is a `\\\#`, then this
        command deletes this `\\\#` and each `\\\#` that follows a
        newline. Otherwise, sends the line after inserting a `\\\#` in
        front of each line in the command. Useful for causing the
        current line to be inserted in the history as a comment and
        removing comments from previous comment commands in the
        history file.

    `=`
    : List the file names that match the current word if an asterisk
        were appended it.

    `@``letter`
    : Your alias list is searched for an alias by the name
        `\_``letter` and if an alias of this name is defined, its
        value will be inserted on the input queue for processing.

## Special Commands

The following simple-commands are executed in the shell process.
Input/Output redirection is permitted. Unless otherwise indicated, the
output is written on file descriptor 1 and the exit status, when there
is no syntax error, is zero. Commands that are preceded by one or two §
are treated specially in the following ways:

1.
: Variable assignment lists preceding the command remain in effect
    when the command completes.

2.
: I/O redirections are processed after variable assignments.

3.
: Errors cause a script that contains them to abort.

4.
: Words, following a command preceded by §§ that are in the format of
    a variable assignment, are expanded with the same rules as a
    variable assignment. This means that tilde substitution is performed
    after the `=` sign and word splitting and file name generation are
    not performed.

§ `:` \[  `arg ` . . . \]
: The command only expands parameters.\

§ ` .` `file ` \[  `arg ` . . . \]
: Read the complete `file ` then execute the commands. The commands
    are executed in the current Shell environment. The search path
    specified by `PATH` is used to find the directory containing
    `file`. If any arguments `arg ` are given, they become the
    positional parameters. Otherwise the positional parameters are
    unchanged. The exit status is the exit status of the last
    command executed.

§§ `alias` \[  `-tx`  \] \[  `name`\[  `=``value `  \]  \] . . .
: `alias ` with no arguments prints the list of aliases in the form
    `name=value ` on standard output. An `alias ` is defined for each
    name whose `value ` is given. A trailing space in `value ` causes
    the next word to be checked for alias substitution. The `-t` flag
    is used to set and list tracked aliases. The value of a tracked
    alias is the full pathname corresponding to the given `name`. The
    value becomes undefined when the value of `PATH` is reset but the
    aliases remained tracked. Without the `-t` flag, for each `name `
    in the argument list for which no `value ` is given, the name and
    value of the alias is printed. The `-x` flag is used to set or
    print exported aliases. An exported alias is defined for scripts
    invoked by name. The exit status is non-zero if a `name ` is given,
    but no value, and no alias has been defined for the `name `.

`bg` \[  `job `. . . \]
: This command is only on systems that support job control. Puts each
    specified `job ` into the background. The current job is put in the
    background if `job ` is not specified. See `Jobs` for a description
    of the format of `job`.

§ `break` \[  `n `  \]
: Exit from the enclosing `for `, `while `, `until `, or
    `select ` loop, if any. If `n ` is specified then break
    `n ` levels.

§ `continue` \[  `n `  \]
: Resume the next iteration of the enclosing `for `, `while `,
    `until `, or `select ` loop. If `n ` is specified then resume at
    the `n`-th enclosing loop.

`cd` \[  `arg `  \]

:

`cd` `old ` `new `
: This command can be in either of two forms. In the first form it
    changes the current directory to `arg`. If `arg ` is `-` the
    directory is changed to the previous directory. The shell variable
    `HOME` is the default `arg`. The variable `PWD` is set to the
    current directory. The shell variable `CDPATH` defines the search
    path for the directory containing `arg`. Alternative directory names
    are separated by a colon (`:`). The default path is
    `&lt;null&gt;` (specifying the current directory). Note that the
    current directory is specified by a null path name, which can appear
    immediately after the equal sign or between the colon delimiters
    anywhere else in the path list. If `arg` begins with a `/` then
    the search path is not used. Otherwise, each directory in the path
    is searched for `arg`.

The second form of `cd` substitutes the string `new` for the string
`old` in the current directory name, `PWD` and tries to change to this
new directory.

The `cd ` command may not be executed by `rksh88 .`

`echo` \[  `arg ` . . . \]
: See
    [`echo`](/web/20141128030245/http://www2.research.att.com/~astopen/man/man1/echo.html)(1)
    for usage and description.

§ `eval` \[  `arg ` . . . \]
: The arguments are read as input to the shell and the
    resulting command(s) executed.

§ `exec` \[  `arg ` . . . \]
: If `arg ` is given, the command specified by the arguments is
    executed in place of this shell without creating a new process.
    Input/output arguments may appear and affect the current process. If
    no arguments are given the effect of this command is to modify file
    descriptors as prescribed by the input/output redirection list. In
    this case, any file descriptor numbers greater than 2 that are
    opened with this mechanism are closed when invoking another program.

§ `exit` \[  `n `  \]
: Causes the shell to exit with the exit status specified by `n`. The
    value will be the least significant 8 bits of the specified status.
    If `n ` is omitted then the exit status is that of the last command
    executed. When `exit` occurs when executing a trap, the last
    command refers to the command that executed before the trap was
    invoked. An end-of-file will also cause the shell to exit except for
    a shell which has the `ignoreeof` option (See `set` below)
    turned on.

§§ `export` \[  `name`\[ `=``value ` \]  \] . . .
: The given `name`s are marked for automatic export to the
    `environment ` of subsequently-executed commands.

`fc` \[  `-e` `ename `   \] \[  `-nlr `  \] \[  `first ` \[  `last `  \]  \]

:

`fc -e -` \[  `old```\\=`new `  \] \[  `command `  \]
: In the first form, a range of commands from `first ` to `last ` is
    selected from the last `HISTSIZE` commands that were typed at the
    terminal. The arguments `first ` and `last ` may be specified as a
    number or as a string. A string is used to locate the most recent
    command starting with the given string. A negative number is used as
    an offset to the current command number. If the `-l` flag is
    selected, the commands are listed on standard output. Otherwise, the
    editor program `ename ` is invoked on a file containing these
    keyboard commands. If `ename ` is not supplied, then the value of
    the variable `FCEDIT` (default `/bin/ed `) is used as the
    editor. When editing is complete, the edited command(s) is executed.
    If `last ` is not specified then it will be set to `first`. If
    `first ` is not specified the default is the previous command for
    editing and -16 for listing. The flag `-r` reverses the order of
    the commands and the flag `-n` suppresses command numbers when
    listing. In the second form the `command ` is re-executed after the
    substitution `old ``=``new ` is performed.

`fg` \[  `job `. . . \]
: This command is only on systems that support job control. Each
    `job ` specified is brought to the foreground. Otherwise, the
    current job is brought into the foreground. See `Jobs` for a
    description of the format of `job`.

`getopts` `optstring name ` \[  `arg ` . . . \]
: Checks `arg` for legal options. If `arg` is omitted, the positional
    parameters are used. An option argument begins with a `+` or a
    `-`. An option not beginning with `+` or `-` or the argument
    `- -` ends the options. `optstring` contains the letters that
    `getopts` recognizes. If a letter is followed by a `:`, that
    option is expected to have an argument. The options can be separated
    from the argument by blanks.

`getopts` places the next option letter it finds inside variable
`name ` each time it is invoked with a `+` prepended when `arg` begins
with a `+`. The index of the next `arg` is stored in `OPTIND`. The
option argument, if any, gets stored in `OPTARG`.

A leading `:` in `optstring` causes `getopts` to store the letter of
an invalid option in `OPTARG`, and to set `name` to `?` for an
unknown option and to `:` when a required option is missing.
Otherwise, `getopts` prints an error message. The exit status is
non-zero when there are no more options.

`jobs` \[  `-lnp `  \] \[  `job ` \\. . . \]
: Lists information about each given job; or all active jobs if `job`
    is omitted. The `-l` flag lists process ids in addition to the
    normal information. The `-n` flag only displays jobs that have
    stopped or exited since last notified. The `-p` flag causes only
    the process group to be listed. See `Jobs` for a description of the
    format of `job`.

`kill` \[  `-``sig `  \] `job ` . . .

:

`kill` `-l`
: Sends either the TERM (terminate) signal or the specified signal to
    the specified jobs or processes. Signals are either given by number
    or by names (as given in `&lt;signal.h&gt;`, stripped of the
    prefix \`\`SIG'' with the exception that SIGCHD is named CHLD). If
    the signal being sent is TERM (terminate) or HUP (hangup), then the
    job or process will be sent a CONT (continue) signal if it is
    stopped. The argument `job ` can be the process id of a process that
    is not a member of one of the active jobs. See `Jobs` for a
    description of the format of `job`. In the second form, `kill -l`,
    the signal numbers and names are listed.

`let` `arg ` . . .
: Each `arg` is a separate `arithmetic expression` to be evaluated.
    See `Arithmetic Evaluation` above, for a description of arithmetic
    expression evaluation.

The exit status is 0 if the value of the last expression is non-zero,
and 1 otherwise.

§ `newgrp` \[  `arg ` . . . \]
: Equivalent to `exec /bin/newgrp` `arg ` . . . .

`print` \[  `-Rnprsu `\[ `n`  \]  \] \[  `arg ` . . . \]
: The shell output mechanism. With no flags or with flag `-` or
    `- -`, the arguments are printed on standard output as described
    by
    [`echo`](/web/20141128030245/http://www2.research.att.com/~astopen/man/man1/echo.html)(1).
    In raw mode, `-R` or `-r`, the escape conventions of `echo` are
    ignored. The `-R` option will print all subsequent arguments and
    options other than `-n`. The `-p` option causes the arguments to
    be written onto the pipe of the process spawned with `|&` instead
    of standard output. The `-s` option causes the arguments to be
    written onto the history file instead of standard output. The `-u`
    flag can be used to specify a one digit file descriptor unit number
    `n ` on which the output will be placed. The default is 1. If the
    flag `-n` is used, no `new-line ` is added to the output. The
    exit status is 0 unless the output file is not open for writing.

`pwd`
: Equivalent to `print -r - \$PWD`

`read` \[  `-prsu `\[  `n `  \]  \] \[  `name``?``prompt `  \] \[  `name ` . . . \]
: The shell input mechanism. One line is read and is broken up into
    fields using the characters in `IFS` as separators. The escape
    character, `\\`, is used to remove any special meaning for the
    next character and for line continuation. In raw mode, `-r,` the
    `\\` character is not treated specially. The first field is
    assigned to the first `name`, the second field to the second `name`,
    etc., with leftover fields assigned to the last `name`. The `-p`
    option causes the input line to be taken from the input pipe of a
    process spawned by the shell using `|&`. If the `-s` flag is
    present, the input will be saved as a command in the history file.
    The flag `-u` can be used to specify a one digit file descriptor
    unit `n ` to read from. The file descriptor can be opened with the
    `exec ` special command. The default value of `n ` is 0. If
    `name ` is omitted then `REPLY` is used as the default `name`. The
    exit status is 0 unless the input file is not open for reading or an
    end-of-file is encountered. An end-of-file with the `-p` option
    causes cleanup for this process so that another can be spawned. If
    the first argument contains a `?`, the remainder of this word is
    used as a `prompt ` on standard error when the shell is interactive.
    The exit status is 0 unless an end-of-file is encountered.

§§ `readonly` \[  `name`\[ `=``value ` \]  \] . . .
: The given `name`s are marked readonly and these names cannot be
    changed by subsequent assignment.

§ `return` \[  `n `  \]
: Causes a shell `function` or ` .` script to return to the invoking
    script with the return status specified by `n`. The value will be
    the least significant 8 bits of the specified status. If `n ` is
    omitted then the return status is that of the last command executed.
    If `return` is invoked while not in a `function` or a ` .`
    script, then it is the same as an `exit`.

`set` \[  `±aefhkmnopstuvx`  \] \[  `±o` `option `  \]. . . \[  `±A` `name `  \] \[  `arg ` . . . \]
: The flags for this command have meaning as follows:

    :

        `-A`
        : Array assignment. Unset the variable `name` and assign
            values sequentially from the list `arg`. If `+A` is used,
            the variable `name` is not unset first.

        `-a`
        : All subsequent variables that are defined are
            automatically exported.

        `-e`
        : If a command has a non-zero exit status, execute the `ERR`
            trap, if set, and exit. This mode is disabled while
            reading profiles.

        `-f`
        : Disables file name generation.

        `-h`
        : Each command becomes a tracked alias when first encountered.

        `-k`
        : All variable assignment arguments are placed in the
            environment for a command, not just those that precede the
            command name.

        `-m`
        : Background jobs will run in a separate process group and a
            line will print upon completion. The exit status of
            background jobs is reported in a completion message. On
            systems with job control, this flag is turned on
            automatically for interactive shells.

        `-n`
        : Read commands and check them for syntax errors, but do not
            execute them. Ignored for interactive shells.

        `-o`
        : The following argument can be one of the following option
            names:

            :

                `allexport`
                : Same as `-a`.

                `errexit`
                : Same as `-e`.

                `bgnice`
                : All background jobs are run at a lower priority.
                    This is the default mode.

                `emacs`
                : Puts you in an `emacs` style in-line editor for
                    command entry.

                `gmacs`
                : Puts you in a `gmacs` style in-line editor for
                    command entry.

                `ignoreeof`
                : The shell will not exit on end-of-file. The command
                    `exit` must be used.

                `keyword`
                : Same as `-k`.

                `markdirs`
                : All directory names resulting from file name
                    generation have a trailing `/` appended.

                `monitor`
                : Same as `-m`.

                `noclobber`
                : Prevents redirection `&gt;` from truncating
                    existing files. Require `&gt;|` to truncate a file
                    when turned on.

                `noexec`
                : Same as `-n`.

                `noglob`
                : Same as `-f`.

                `nolog`
                : Do not save function definitions in history file.

                `nounset`
                : Same as `-u`.

                `privileged`
                : Same as `-p`.

                `verbose`
                : Same as `-v`.

                `trackall`
                : Same as `-h`.

                `vi`
                : Puts you in insert mode of a `vi ` style in-line
                    editor until you hit escape character `033`. This
                    puts you in control mode. A return sends the line.

                `viraw`
                : Each character is processed as it is typed in
                    `vi ` mode.

                `xtrace`
                : Same as `-x`.

                If no option name is supplied then the current option settings are printed.

                :

    `-p`
    : Disables processing of the `\$HOME/.profile` file and uses the
        file `/etc/suid\_profile` instead of the `ENV` file. This
        mode is on whenever the effective uid (gid) is not equal to the
        real uid (gid). Turning this off causes the effective uid and
        gid to be set to the real uid and gid.

    `-s`
    : Sort the positional parameters lexicographically.

    `-t`
    : Exit after reading and executing one command.

    `-u`
    : Treat unset parameters as an error when substituting.

    `-v`
    : Print shell input lines as they are read.

    `-x`
    : Print commands and their arguments as they are executed.

    `-`
    : Turns off `-x` and `-v` flags and stops examining arguments
        for flags.

    `- -`
    : Do not change any of the flags; useful in setting `\$1` to a
        value beginning with `-`. If no arguments follow this flag
        then the positional parameters are unset.

    Using `+` rather than `-` causes these flags to be turned off.
    These flags can also be used upon invocation of the shell. The
    current set of flags may be found in `\$-`. Unless `-A` is
    specified, the remaining arguments are positional parameters and are
    assigned, in order, to `\$1` `\$2` . . . . If no arguments are
    given then the names and values of all variables are printed on the
    standard output.

§ `shift` \[  `n `  \]

\
The positional parameters from `\$``n``+1` . . . are renamed `\$1`
. . . , default `n ` is 1. The parameter `n ` can be any arithmetic
expression that evaluates to a non-negative number less than or equal to
`\$\#`.

§ `times`

\
Print the accumulated user and system times for the shell and for
processes run from the shell.

§ `trap` \[  `arg `  \] \[  `sig `  \] . . .

`arg ` is a command to be read and executed when the shell receives
signal(s) `sig`. (Note that `arg ` is scanned once when the trap is set
and once when the trap is taken.) Each `sig ` can be given as a number
or as the name of the signal. Trap commands are executed in order of
signal number. Any attempt to set a trap on a signal that was ignored on
entry to the current shell is ineffective. If `arg ` is omitted or is
`-`, then the trap(s) for each `sig ` are reset to their original
values. If `arg ` is the null string then this signal is ignored by the
shell and by the commands it invokes. If `sig ` is `ERR` then `arg `
will be executed whenever a command has a non-zero exit status. If
`sig ` is `DEBUG` then `arg ` will be executed after each command. If
`sig ` is `0` or `EXIT` and the `trap` statement is executed
inside the body of a function, then the command `arg ` is executed after
the function completes. If `sig ` is `0` or `EXIT` for a `trap`
set outside any function then the command `arg ` is executed on exit
from the shell. The `trap` command with no arguments prints a list of
commands associated with each signal number.

§§ `typeset` \[  `±HLRZfilrtux `\[ `n` \]  \] \[  `name`\[  `=``value `  \]    \] . . .

Sets attributes and values for shell variables and functions. When
invoked inside a function, a new instance of the variables `name ` is
created. The variables value and type are restored when the function
completes. The following list of attributes may be specified:

:

    `-H`
    : This flag provides UNIX to host-name file mapping on
        non-UNIX machines.

    `-L`
    : Left justify and remove leading blanks from `value`. If `n` is
        non-zero it defines the width of the field, otherwise it is
        determined by the width of the value of first assignment. When
        the variable is assigned to, it is filled on the right with
        blanks or truncated, if necessary, to fit into the field.
        Leading zeros are removed if the `-Z` flag is also set. The
        `-R` flag is turned off.

    `-R`
    : Right justify and fill with leading blanks. If `n` is non-zero
        it defines the width of the field, otherwise it is determined by
        the width of the value of first assignment. The field is left
        filled with blanks or truncated from the end if the variable is
        reassigned. The `-L` flag is turned off.

    `-Z`
    : Right justify and fill with leading zeros if the first non-blank
        character is a digit and the `-L` flag has not been set. If
        `n` is non-zero it defines the width of the field, otherwise it
        is determined by the width of the value of first assignment.

    `-f`
    : The names refer to function names rather than variable names. No
        assignments can be made and the only other valid flags are
        `-t`, `-u` and `-x`. The flag `-t` turns on execution
        tracing for this function. The flag `-u` causes this function
        to be marked undefined. The `FPATH` variable will be searched
        to find the function definition when the function is referenced.
        The flag `-x` allows the function definition to remain in
        effect across shell procedures invoked by name.

    `-i`
    : Parameter is an integer. This makes arithmetic faster. If `n` is
        non-zero it defines the output arithmetic base, otherwise the
        first assignment determines the output base.

    `-l`
    : All upper-case characters are converted to lower-case. The
        upper-case flag, `-u` is turned off.

    `-r`
    : The given `name`s are marked readonly and these names cannot be
        changed by subsequent assignment.

    `-t`
    : Tags the variables. Tags are user definable and have no special
        meaning to the shell.

    `-u`
    : All lower-case characters are converted to upper-case
        characters. The lower-case flag, `-l` is turned off.

    `-x`

    : The given `name`s are marked for automatic export to the
        `environment ` of subsequently-executed commands.

        The `-i` attribute can not be specified along with `-R`,
        `-L`, `-Z`, or `-f`.

        Using `+` rather than `-` causes these flags to be turned
        off. If no `name ` arguments are given but flags are specified,
        a list of `names ` (and optionally the `values `) of the
        `variables ` which have these flags set is printed. (Using `+`
        rather than `-` keeps the values from being printed.) If no
        `name`s and flags are given, the `names ` and `attributes ` of
        all `variables ` are printed.

`ulimit` \[  `-HSacdfmnpstv`  \] \[  `limit `  \]

Set or display a resource limit. The available resources limits are
listed below. Many systems do not contain one or more of these limits.
The limit for a specified resource is set when `limit ` is specified.
The value of `limit ` can be a number in the unit specified below with
each resource, or the value `unlimited`. The `H` and `S` flags
specify whether the hard limit or the soft limit for the given resource
is set. A hard limit cannot be increased once it is set. A soft limit
can be increased up to the value of the hard limit. If neither the `H`
or `S` options is specified, the limit applies to both. The current
resource limit is printed when `limit ` is omitted. In this case the
soft limit is printed unless `H` is specified. When more that one
resource is specified, then the limit name and unit is printed before
the value.

:

    `-a`
    : Lists all of the current resource limits.

    `-c`
    : The number of 512-byte blocks on the size of core dumps.

    `-d`
    : The number of K-bytes on the size of the data area.

    `-f`
    : The number of 512-byte blocks on files written by child
        processes (files of any size may be read).

    `-m`
    : The number of K-bytes on the size of physical memory.

    `-n`
    : The number of file descriptors plus 1.

    `-p`
    : The number of 512-byte blocks for pipe buffering.

    `-s`
    : The number of K-bytes on the size of the stack area.

    `-t`
    : The number of seconds to be used by each process.

    `-v`
    : The number of K-bytes for virtual memory.
        If no option is given, `-f` is assumed.

`umask` \[  `mask `  \]

The user file-creation mask is set to `mask ` (see `umask`(2)). `mask`
can either be an octal number or a symbolic value as described in
[`chmod`](/web/20141128030245/http://www2.research.att.com/~astopen/man/man1/chmod.html)(1).
If a symbolic value is given, the new umask value is the complement of
the result of applying `mask ` to the complement of the previous umask
value. If `mask ` is omitted, the current value of the mask is printed.

`unalias` `name ` . . .

The `aliases ` given by the list of `name`s are removed from the
`alias ` list.

`unset` \[  `-f`  \] `name ` . . .

The variables given by the list of `name`s are unassigned, i.e., their
values and attributes are erased. Readonly variables cannot be unset. If
the `-f`, flag is set, then the names refer to `function ` names.
Unsetting `ERRNO`, `LINENO`, `MAILCHECK`, `OPTARG`, `OPTIND`,
`RANDOM`, `SECONDS`, `TMOUT`, and `\_` removes their special
meaning even if they are subsequently assigned to.

§ `wait` \[  `job `  \]

Wait for the specified `job` and report its termination status. If
`job ` is not given then all currently active child processes are waited
for. The exit status from this command is that of the process waited
for. See `Jobs` for a description of the format of `job`.

`whence` \[  `-pv`  \] `name ` . . .

For each `name`, indicate how it would be interpreted if used as a
command name.

The `-v` flag produces a more verbose report.

The `-p` flag does a path search for `name ` even if name is an alias,
a function, or a reserved word.

## Invocation

If the shell is invoked by
[`exec`](/web/20141128030245/http://www2.research.att.com/~astopen/man/man2/exec.html)(2),
and the first character of argument zero (`\$0`) is `-`, then the
shell is assumed to be a `login` shell and commands are read from
`/etc/profile` and then from either `.profile` in the current
directory or `\$HOME/.profile`, if either file exists. Next, commands
are read from the file named by performing parameter substitution on the
value of the environment variable `ENV` if the file exists. If the
`-s` flag is not present and `arg ` is, then a path search is
performed on the first `arg ` to determine the name of the script to
execute. The script `arg ` must have read permission and any `setuid`
and `getgid` settings will be ignored. If the script is not found on the
path, `arg ` is processed as if it named a builtin command or function.
Commands are then read as described below; the following flags are
interpreted by the shell when it is invoked:

`-c``  string `
: If the `-c` flag is present then commands are read from `string`.

`-s`
: If the `-s` flag is present or if no arguments remain then
    commands are read from the standard input. Shell output, except for
    the output of the `Special Commands ` listed above, is written to
    file descriptor 2.

`-i`
: If the `-i` flag is present or if the shell input and output are
    attached to a terminal (as told by `ioctl`(2)) then this shell is
    `interactive`. In this case TERM is ignored (so that `kill 0` does
    not kill an interactive shell) and INTR is caught and ignored (so
    that `wait` is interruptible). In all cases, QUIT is ignored by
    the shell.

`-r`
: If the `-r` flag is present the shell is a restricted shell.

The remaining flags and arguments are described under the `set`
command above.

## rksh88 Only

`rksh88` is used to set up login names and execution environments whose
capabilities are more controlled than those of the standard shell. The
actions of `rksh88 ` are identical to those of `ksh88 `, except that the
following are disallowed:

: changing directory (see `cd`(1)),\
    setting the value of `SHELL`, `ENV`, or `PATH,`\
    specifying path or command names containing `/`,\
    redirecting output (`&gt;`, `&gt;|`, `&lt;&gt;`, and
    `&gt;&gt;`),\
    changing group (see `newgrp`(1)).

The restrictions above are enforced after `.profile` and the `ENV`
files are interpreted.

When a command to be executed is found to be a shell procedure,
`rksh88 ` invokes `ksh88 ` to execute it. Thus, it is possible to
provide to the end-user shell procedures that have access to the full
power of the standard shell, while imposing a limited menu of commands;
this scheme assumes that the end-user does not have write and execute
permissions in the same directory.

The net effect of these rules is that the writer of the `.profile` has
complete control over user actions, by performing guaranteed setup
actions and leaving the user in an appropriate directory (probably
`not ` the login directory).

The system administrator often sets up a directory of commands (i.e.,
`/usr/rbin`) that can be safely invoked by `rksh88`.

# EXIT STATUS

Errors detected by the shell, such as syntax errors, cause the shell to
return a non-zero exit status. Otherwise, the shell returns the exit
status of the last command executed (see also the `exit` command
above). If the shell is being used non-interactively then execution of
the shell file is abandoned. Run time errors detected by the shell are
reported by printing the command or function name and the error
condition. If the line number that the error occurred on is greater than
one, then the line number is also printed in square brackets (`\[\]`)
after the command or function name.

# FILES

/etc/passwd\
/etc/profile\
/etc/suid\_profile\
\$HOME/`.`profile\
/tmp/sh\`\
/dev/null

# SEE ALSO

cat(1), cd(1), chmod(1), cut(1), echo(1), emacs(1), env(1), gmacs(1),
newgrp(1), stty(1), test(1), umask(1), vi(1), dup(2), exec(2), fork(2),
ioctl(2), lseek(2), paste(1), pipe(2), signal(2), umask(2), ulimit(2),
wait(2), rand(3), a.out(5), profile(5), environ(7).

Morris I. Bolsky and David G. Korn, `The KornShell Command and
Programming Language`, Prentice Hall, 1989.

# CAVEATS

If a command which is a `tracked alias` is executed, and then a command
with the same name is installed in a directory in the search path before
the directory where the original command was found, the shell will
continue to `exec ` the original command. Use the `-t` option of the
`alias ` command to correct this situation.

Some very old shell scripts contain a `\^` as a synonym for the pipe
character `|`.

Using the `fc ` built-in command within a compound command will cause
the whole command to disappear from the history file.

The built-in command ` .` `file ` reads the whole file before any
commands are executed. Therefore, `alias` and `unalias` commands in
the file will not apply to any functions defined in the file.

Traps are not processed while a job is waiting for a foreground process.
Thus, a trap on `CHLD` won't be executed until the foreground job
terminates.

------------------------------------------------------------------------

  -------------- ---------------------------- ---------------
  RDS Standard   User Environment Utilities   July 02, 2009
  -------------- ---------------------------- ---------------


