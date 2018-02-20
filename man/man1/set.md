# NAME

set - set/unset options and positional parameters

# SYNOPSIS

`set` \[ `options` \] \[arg ...\]

# DESCRIPTION

`set` sets or unsets options and positional parameters. Options that
are specified with a `-` cause the options to be set. Options that are
specified with a `+` cause the option to be unset.

`set` without any options or arguments displays the names and values
of all shell variables in the order of the collation sequence in the
current locale. The values are quoted so that they are suitable for
reinput to the shell.

If no `arg`s are specified, not even the end of options argument `--`,
the positional parameters are unchanged. Otherwise, unless the `-A`
options has been specified, the positional parameters are replaced by
the list of `arg`s. A first `arg` of `--` is ignored when setting
positional parameters.

For backward compatibility, a `set` command without any options
specified whose first `arg` is `-` will turn off the `-v` and `-x`
options. If any additional `arg`s are specified, they will replace the
positional parameters.

# OPTIONS

-`s`
: Sort the positional parameters.

-`A` `name`
: Assign the arguments sequentially to the array named by `name`
    starting at subscript 0 rather than to the positional parameters.

-`a`
: Set the export attribute for each variable whose name does not
    contain a `.` that you assign a value in the current
    shell environment.

-`b`
: The shell writes a message to standard error as soon it detects that
    a background job completes rather than waiting until the
    next prompt.

-`e`
: A simple command that has an non-zero exit status will cause the
    shell to exit unless the simple command is:

    [`+`]()
    : contained in an `&&` or `||` list.

    [`+`]()
    : the command immediately following `if`, `while`, or
        `until`.

    [`+`]()
    : contained in the pipeline following `!`.

-`f`

Pathname expansion is disabled.

-`h`

Obsolete. Causes each command whose name has the syntax of an alias to
become a tracked alias when it is first encountered.

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

--`default`

Restore all non-command line options to the default settings.

--`state`

List the current option state in the form of a `set` command that can
be executed to restore the state.

# EXIT STATUS

`0`
: No errors occurred.

`&gt;0`
: An error occurred.

# SEE ALSO

[`typeset`](/web/20141128030250/http://www2.research.att.com/~astopen/man/man1/typeset.html)(1),
[`shift`](/web/20141128030250/http://www2.research.att.com/~astopen/man/man1/shift.html)(1)

# IMPLEMENTATION

`version`
: set (AT&T Research) 1999-09-28

`author`
: David Korn

`copyright`
: Copyright © 1982-2010 AT&T Intellectual Property

`license`
: [http://www.opensource.org/licenses/cpl1.0.txt](https://web.archive.org/web/20141128030250/http://www.opensource.org/licenses/cpl1.0.txt)


