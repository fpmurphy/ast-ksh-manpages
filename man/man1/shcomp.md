# NAME

shcomp - compile a shell script

# SYNOPSIS

`shcomp` \[ `options` \] \[infile \[outfile\]\]

# DESCRIPTION

Unless `-D` is specified, `shcomp` takes a shell script, `infile`,
and creates a binary format file, `outfile`, that `ksh` can read and
execute with the same effect as the original script.
Since aliases are processed as the script is read, alias definitions
whose value requires variable expansion will not work correctly.

If `-D` is specified, all double quoted strings that are preceded by
`\$` are output. These are the messages that need to be translated to
locale specific versions for internationalization.

If `outfile` is omitted, then the results will be written to standard
output. If `infile` is also omitted, the shell script will be read from
standard input.

# OPTIONS

-`D`, --`dictionary`
:   Generate a list of strings that need to be placed in a message
    catalog for internationalization.

-`n`, --`noexec`
:   Displays warning messages for obsolete or non-conforming constructs.

-`v`, --`verbose`
:   Displays input from `infile` onto standard error as it reads it.

# EXIT STATUS

`0`
: Successful completion.

`&gt;0`
:   An error occurred.

# SEE ALSO

[`ksh`](/web/20141128030250/http://www2.research.att.com/~astopen/man/man1/ksh.html)(1)

# IMPLEMENTATION

`version`
:   shcomp (AT&T Research) 2003-03-02

`author`
:   David Korn

`copyright`
:   Copyright © 1982-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030250/http://www.eclipse.org/org/documents/epl-v10.html)


