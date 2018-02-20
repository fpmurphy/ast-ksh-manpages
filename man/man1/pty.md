# NAME

pty - create pseudo terminal and run command

# SYNOPSIS

`pty` \[ `options` \] command \[arg ...\]

# DESCRIPTION

`pty` creates a pseudo pty and then runs `command` with arguments
given by `arg` and the standard input, standard output, and standard
error connected to the pseudo terminal. By default, the `pty` creates
a new session.
If `command` does not contain a `/`, the `PATH` variable will be
used to locate the `command`.

Input to `pty` will be written to the standard input of this command.
The standard output and standard error from the command will be written
to the standard output of `pty`.

The `pty` commmand terminates when the command completes.

# OPTIONS

-`d`, --`dialogue`
:   Execute the dialogue on the standard input. A dialogue is a sequence
    of commands, one command per line. All `re` patterns are extended
    regular expressions. The `re` `?1` will print the subject string
    on the standard error and match the string; the `re` `?0` will
    print the subject string on the standard error and not match
    the string. The `re` `?.` matches EOF. The commands are:

    [`\#` `comment`]()
    : \
        comment line

    [`c` `text`]()
    : \
        write `text` to the master; C style escapes in text are
        converted, including \\E for ESC and \\cX for control-X

    [`d` `milliseconds`]()
    : \
        set the delay before each master write to `milliseconds`; the
        default is no delay

    [`i` `re`]()
    : read a line from the master; if it matches `re` then execute
        lines until matching `e` or `f`

    [`e \[re\]`]()
    : \
        else \[if match re\] then execute lines until matching `e` or
        `f`

    [`f`]()
    : end of `i`/`e` block

    [`m` `text`]()
    : \
        write `text` to the standard error

    [`p` `text`]()
    : \
        peek input until `text` is found at the beginning of a line;
        input is not consumed

    [`r \[``re`\]]()
    : \
        read a line from the master \[and it should match re\]

    [`s` `milliseconds`]()
    : \
        sleep for `milliseconds`

    [`t` `milliseconds`]()
    : \
        set the master read timout to `milliseconds`; the default is
        `1000`

    [`u` `re`]()
    : read lines from the master until one matches `re`

    [`v` `level`]()
    : \
        set the verbose trace `level`, more output for higher levels,
        disabled for level 0

    [`w` `text`]()
    : \
        write `text`\\r\\n to the master; C style escapes in text are
        converted, including \\E for ESC and \\cX for control-X

    [`x \[``code`\]]()
    : \
        exit `pty` with exit code `0` \[`code`\]

    [`I` `re`]()
    : ignore master lines matching `re`

    [`L` `label`]()
    : \
        prefix all diagnostics with `label`:

    [`P` `text`]()
    : \
        delay each master write until the beginning of an unread input
        line exactly matches `text`

-`D`, --`debug`=`level`
:   Set the debug trace `level`, higher levels produce more output,
    disabled for level 0.

-`l`, --`log`=`file`
:   Log the master stdout and stderr to `file`.

-`m`, --`messages`=`file`
:   Redirect diagnostic message output to `file`.

-`s`, --`session`
:   Create a separate session for the process started by `pty`. On by
    default; -`s` means --`nosession`.

-`t`, --`timeout`=`milliseconds`
:   Set the master read timeout to `milliseconds`. The default value is
    `1000` .

-`T`, --`tty`=`stty`
:   Pass `stty` to the
    [`stty`](/web/20141128030248/http://www2.research.att.com/~astopen/man/man1/stty.html)(1)
    command to initialize the pty.

-`w`, --`delay`=`milliseconds`
:   Set the delay before each master write to `milliseconds`. The
    default value is `0`.

# EXIT STATUS

If the command determined by `command` is run the exit status of
`pty` is that of this command. Otherwise, the exit status is one of
the following:

`127`
: The command is found but cannot be executed.

`128`
: The command could not be found.

# SEE ALSO

[`command`](/web/20141128030248/http://www2.research.att.com/~astopen/man/man1/command.html)(1),
[`exec`](/web/20141128030248/http://www2.research.att.com/~astopen/man/man1/exec.html)(1)

# IMPLEMENTATION

`version`
:   pty (AT&T Research) 2012-06-11

`author`
:   Glenn Fowler

`author`
:   David Korn

`copyright`
:   Copyright © 2001-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030248/http://www.eclipse.org/org/documents/epl-v10.html)


