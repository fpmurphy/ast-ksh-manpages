# NAME

`tksh.ok` - Shell, the standard command language interpreter

# SYNOPSIS

`tksh.ok` \[ `options` \] \[arg ...\]

# DESCRIPTION

`tksh.ok` is a command language interpreter that executes commands
read from a command line string, the standard input, or a specified
file.

If the `-i` option is present, or there are no `arg`s and the standard
input and standard error are attached to a terminal, the shell is
considered to be interactive.

The `-s` and `-c` options are mutually exclusive. If the `-c`
option is specified, the first `arg` is the command-line string and must
be specified. Any remaining `arg`s will be used to initialize `\$0`
and positional parameters.

If the neither `-s` nor `-c` is specified, then the first `arg`
will be the pathname of the file containing commands and `\$0` will be
set to this value. If there is no file with this pathname, and this
pathame does not contain a `/` , then the `PATH` will be searched
for an executable with this name. Any remaining `arg`s will be used to
initialize the positional parmaeters.

Any option can use a `+` instead of a `-` to disable the
corresponding option.

# OPTIONS

-`c`
: Read the commands from the first `arg`.

-`i`
: Specifies that the shell is interactive.

-`l`
: Invoke the shell as a login shell; `/etc/profile` and
    `\$HOME/.profile`, if they exist, are read before the
    first command.

-`r`
: Invoke the shell in a restricted mode. A restricted shell does not
    permit any of the following:

    [`-`]()
    : Changing the working directory.

    [`-`]()
    : Setting values or attributes of the variables `SHELL`,
        `ENV`, `FPATH`, or `PATH`.

    [`-`]()
    : Executing any command whose name as a `/` in it.

    [`-`]()
    : Redirecting output of a command with `&gt;`, `&gt;|`,
        `&lt;&gt;`, or `&gt;&gt;`.

    [`-`]()
    : Adding or deleting built-in commands or libraries with
        `builtin`.

    [`-`]()
    : Executing `command -p` `...` .

-`s`

Read the commands from standard input. The positional parameters will be
initialized from `arg`.

-`D`

Do not execute the script, but output the set of double quoted strings
preceded by a `\$`. These strings are needed for localization of the
script to different locales.

-`E`

Reads the file `\${ENV-\$HOME/.kshrc}`, if it exists, as a profile. On
by default for interactive shells; use `+E` to disable.

-`R` `file`

Do not execute the script, but create a cross reference database in
`file` that can be used a separate shell script browser. The -R option
requires a script to be specified as the first operand.

-`a`

Set the export attribute for each variable whose name does not contain a
`.` that you assign a value in the current shell environment.

-`b`

The shell writes a message to standard error as soon it detects that a
background job completes rather than waiting until the next prompt.

-`e`

A simple command that has an non-zero exit status will cause the shell
to exit unless the simple command is:

`+`
: contained in an `&&` or `||` list.

`+`
: the command immediately following `if`, `while`, or `until`.

`+`
: contained in the pipeline following `!`.

-`f`

Pathname expansion is disabled.

-`h`

Obsolete. Causes each command whose name has the syntax of an alias to
become a tracked aliase when it is first encountered.

-`k`

This is obsolete. All arguments of the form `name``=``value` are
removed and placed in the variable assignment list for the command.
Ordinarily, variable assignments must precede command arguments.

-`m`

When enabled, the shell runs background jobs in a separate process group
and displays a line upon completion. This mode is enabled by default for
interactive shells on systems that support job control.

-`n`

The shell reads commands and checks for syntax errors, but does not
execute the command. Usually specified on command invocation.

-`o`\[`option`\]

If `option` is not specified, the list of options and their current
settings will be written to standard output. When invoked with a `+`
the options will be written in a format that can be reinput to the shell
to restore the settings. This option can be repeated to enable/disable
multiple options. The value of `option` must be one of the following:

`allexport`
: Equivalent to `-a`.

`bgnice`
: Runs background jobs at lower priorities.

`braceexpand`
: Equivalent to `-B`.

`emacs`
: Enables/disables `emacs` editing mode.

`errexit`
: Equivalent to `-e`.

`globstar`
: Equivalent to `-G`.

`gmacs`
: Enables/disables `gmacs` editing mode. `gmacs` editing mode is
    the same as `emacs` editing mode except for the handling of
    `\^T`.

`histexpand`
: Equivalent to `-H`.

`ignoreeof`
: Prevents an interactive shell from exiting on reading
    an end-of-file.

`keyword`
: Equivalent to `-k`.

`markdirs`
: A trailing `/` is appended to directories resulting from
    pathname expansion.

`monitor`
: Equivalent to `-m`.

`multiline`
: Use multiple lines when editing lines that are longer than the
    window width.

`noclobber`
: Equivalent to `-C`.

`noexec`
: Equivalent to `-n`.

`noglob`
: Equivalent to `-f`.

`nolog`
: This has no effect. It is provided for backward compatibility.

`notify`
: Equivalent to `-b`.

`nounset`
: Equivalent to `-u`.

`pipefail`
: A pipeline will not complete until all components of the pipeline
    have completed, and the exit status of the pipeline will be the
    value of the last command to exit with non-zero exit status, or will
    be zero if all commands return zero exit status.

`privileged`
: Equivalent to `-p`.

`showme`
: Simple commands preceded by a `;` will be traced as if `-x` were
    enabled but not executed.

`trackall`
: Equivalent to `-h`.

`verbose`
: Equivalent to `-v`.

`vi`
: Enables/disables `vi` editing mode.

`viraw`
: Does not use canonical input mode when using `vi` edit mode.

`xtrace`
: Equivalent to `-x`.

The option value may be omitted.

-`p`

Privileged mode. Disabling `-p` sets the effective user id to the real
user id, and the effective group id to the real group id. Enabling
`-p` restores the effective user and group ids to their values when
the shell was invoked. The `-p` option is on whenever the real and
effective user id is not equal or the real and effective group id is not
equal. User profiles are not processed when `-p` is enabled.

-`r`

restricted. Enables restricted shell. This option cannot be unset once
enabled.

-`t`

Obsolete. The shell reads one command and then exits.

-`u`

If enabled, the shell displays an error message when it tries to expand
a variable that is unset.

-`v`

Verbose. The shell displays its input onto standard error as it reads
it.

-`x`

Execution trace. The shell will display each command after all expansion
and before execution preceded by the expanded value of the `PS4`
parameter.

-`B`

Enable {...} group expansion. On by default.

-`C`

Prevents existing regular files from being overwritten using the
`&gt;` redirection operator. The `&gt;|` redirection overrides this
`noclobber` option.

-`G`

Causes `\`\`` by itself to also match all sub-directories during
pathname expansion.

-`H`

Enable `!`-style history expansion similar to `csh`.

# EXIT STATUS

If `tksh.ok` executes command, the exit status will be that of the
last command executed. Otherwise, it will be one of the following:

`0`
: The script or command line to be executed consists entirely of zero
    or more blank lines or comments.

`&gt;1-125`
: A noninteractive shell detected a syntax error, a variable
    assignment error, or an error in a special built-in.

`126`
: `-c` and `-s` were not specified and the command script was
    found on `PATH` but was not executable.

`127`
: `-c` and `-s` were not specified and the command script
    corresponding to `arg` could not be found.

# SEE ALSO

[`set`](/web/20141128030251/http://www2.research.att.com/~astopen/man/man1/set.html)(1),
[`builtin`](/web/20141128030251/http://www2.research.att.com/~astopen/man/man1/builtin.html)(1)

# IMPLEMENTATION

`version`
: sh (AT&T Research) 93t 2008-07-17

`author`
: David Korn
    &lt;[dgkorn@gmail.com](https://web.archive.org/web/20141128030251/mailto:dgkorn@gmail.com)&gt;

`copyright`
: Copyright © 1982-2008 AT&T Intellectual Property

`license`
: [http://www.opensource.org/licenses/cpl1.0.txt](https://web.archive.org/web/20141128030251/http://www.opensource.org/licenses/cpl1.0.txt)


