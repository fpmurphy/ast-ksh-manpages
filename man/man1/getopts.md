# NAME

getopts - parse utility options

# SYNOPSIS

`getopts` \[ `options` \] opstring name \[args...\]

# DESCRIPTION

The `getopts` utility can be used to retrieve options and arguments
from a list of arguments given by `args` or the positional parameters if
`args` is omitted. It can also generate usage messages and a man page
for the command based on the information in `optstring` .

Each time it is invoked, the `getopts` utility places the value of the
next option in the shell variable specified by the `name` operand and
the index of the next argument to be processed in the shell variable
`OPTIND`. When the shell is invoked `OPTIND` is initialized to
`1`. When an option requires or permits an option argument,
`getopts` places the option argument in the shell variable `OPTARG`
. Otherwise `OPTARG` is set to `1` when the option is set and `0`
when the option is unset.

The `optstring` string consists of alpha-numeric characters, the special
characters +, -, ?, :, and &lt;space&gt;, or character groups enclosed
in \[...\]. Character groups may be nested in {...}. Outside of a
\[...\] group, a single new-line followed by zero or more blanks is
ignored. One or more blank lines separate the options from the command
argument synopsis.

Each \[...\] group consists of an optional label, optional attributes
separated by :, and an optional description string following ?. The
characters from the ? to the end of the next \] are ignored for option
parsing and short usage messages. They are used for generating verbose
help or man pages. The : character may not appear in the label. The ?
character must be specified as ?? in the label and the \] character must
be specified as \]\] in the description string. Text between two \\b
(backspace) characters indicates that the text should be emboldened when
displayed. Text between two \\a (bell) characters indicates that the
text should be emphasized or italicized when displayed. Text between two
\\v (vertical tab) characters indicates that the text should displayed
in a fixed width font. Text between two \\f (formfeed) characters will
be replaced by the output from the shell function whose name is that of
the enclosed text.

All output from this interface is written to the standard error.

There are several group types:

`1.`
: A group of the form
    \[-\[`version`\]\[`flag`\[`number`\]\]...\[?`text`\]\] appearing as
    the first group enables the extended interface. `version` specifies
    the interface version, currently `1`. The latest version is
    assumed if `version` is omitted. Future enhancements may increment
    `version`, but all versions will be supported. `text` typically
    specifies an SCCS or CVS identification string. Zero or more `flags`
    with optional `number` values may be specified to control
    option parsing. The flags are:

    [`+`]()
    : Arguments beginning with + are considered options.

    [`c`]()
    : Cache this `optstring` for multiple passes. Used to optimize
        builtins that may be called many times within the same process.

    [`i`]()
    : Ignore this `optstring` when generating help. Used when
        combining `optstring` values from multiple passes.

    [`l`]()
    : Display only `longname` options in help messages.

    [`n`]()
    : Associate -`number` and +`number` options with the first option
        with numeric arguments.

    [`o`]()
    : The `-` option character prefix is optional (supports obsolete
        [`ps`](/web/20141128030244/http://www2.research.att.com/~astopen/man/man1/ps.html)(1)
        option syntax.)

    [`p`]()
    : `number` specifies the number of `-` characters that must
        prefix long option names. The default is `2` ; `0`, `1` or
        `2` are accepted (e.g., `p0` for
        [`dd`](/web/20141128030244/http://www2.research.att.com/~astopen/man/man1/dd.html)(1)
        and `p1` for
        [`find`](/web/20141128030244/http://www2.research.att.com/~astopen/man/man1/find.html)(1).)

    [`s`]()
    : `number` specifies the `--??man` section number, `1`
        by default.

[`2.`]()

An option specification of the form
\[`option`\[!\]\[=`number`\]\[:`longname`\]\[?`text`\]\]. In this case
the first field is the option character; this is the value returned in
the `name` operand when the option is matched. If there is no option
character then a two or more digit number should be specified. This
number will be returned as the value of the `name` operand if the long
option is matched. If `option` is followed by `!` then the option
character sense is the inverse of the longname sense. For options that
do not take values `OPTARG` will be set to `0` for `!` inverted
option characters and `1` otherwise. =`number` optionally specifies a
number to be returned in the `name` operand instead of the option
character. A longname is specified by `--``longname` and is matched by
the shortest non-ambiguous prefix of all long options. \` in the
`longname` field indicates that only characters up to that point need to
match, provided any additional characters match exactly. The enclosing
\[ and \] can be omitted for an option that does not have a longname or
descriptive text.

[`3.`]()

An option argument specification. Options that take arguments can be
followed by : (string value) or \# (numeric value) and an option
argument specification. An option argument specification consists of the
option argument name as field 1. The remaining `:` separated fields
are a type name and zero or more of the special attribute words
`listof`, `oneof`, and `ignorecase`. A default option value may be
specified in the final field as `:=``default`. The option argument
specification may be followed by a list of option value descriptions
enclosed in braces. A long option that takes an argument is specified as
`--``longname`=`value`. If the : or \# is followed by ? then the
option argument is optional. If only the option character form is
specified then the optional argument value is not set if the next
argument starts with - or +.

[`4.`]()

A option value description.

[`5.`]()

A argument specification. A list of valid option argument values can be
specified by enclosing them inside a {...} following the option argument
specification. Each of the permitted values can be specified with a
\[...\] containing the value followed by a description.

[`6.`]()

A group of the form \[+\\n...\] will display the characters representing
... in fixed with font without adding line breaks.

[`7.`]()

A group of the form \[+`name`?`text`\] specifies a section `name` with
descriptive `text`. If `name` is omitted then `text` is placed in a new
paragraph.

[`8.`]()

A group of the form \[-`name`?`text`\] specifies entries for the
`IMPLEMENTATION` section.

A leading : character in `optstring` affects the way errors are handled.
If an option character or longname argument not specified in `optstring`
is encountered when processing options, the shell variable whose name is
`name` will be set to the ? character. The shell variable `OPTARG`
will be set to the character found. If an option argument is missing or
has an invalid value, then `name` will be set to the : character and the
shell variable `OPTARG` will be set to the option character found.
Without the leading :, `name` will be set to the ? character, `OPTARG`
will be unset, and an error message will be written to standard error
when errors are encountered.

A leading + character or a + following a leading : in `optstring`
specifies that arguments beginning with + will also be considered
options.

The end of options occurs when:

`1.`
: The special argument `--` is encountered.

`2.`
: An argument that does not begin with a `-` is encountered.

`3.`
: A help argument is specified.

`4.`
: An error is encountered.

If `OPTIND` is set to the value `1`, a new set of arguments can be
used.

`getopts` can also be used to generate help messages containing
command usage and detailed descriptions. Specify `args` as:

`-?`
: To generate a usage synopsis.

`--??`
: To generate a verbose usage message.

`--??man`
: To generate a formatted man page.

`--??api`
: To generate an easy to parse usage message.

`--??html`
: To generate a man page in `html` format.

`--??nroff`
: To generate a man page in `nroff` format.

`--??usage`
: List the current `optstring`.

`--???``name`
: List `version=``n`, `n`&gt;0, if the option `name` is recognized
    by `getopts` .

When the end of options is encountered, `getopts` exits with a
non-zero return value and the variable `OPTIND` is set to the index of
the first non-option argument.

# OPTIONS

-`a` `name`
: Use `name` instead of the command name in usage messages.

# EXIT STATUS

`0`
: An option specified was found.

`1`
: An end of options was encountered.

`2`
: A usage or information message was generated.

# IMPLEMENTATION

`version`
: getopts (AT&T Research) 2005-01-01

`author`
: Glenn Fowler
    &lt;[glenn.s.fowler@gmail.com](https://web.archive.org/web/20141128030244/mailto:glenn.s.fowler@gmail.com)&gt;

`author`
: David Korn
    &lt;[dgkorn@gmail.com](https://web.archive.org/web/20141128030244/mailto:dgkorn@gmail.com)&gt;

`copyright`
: Copyright © 1982-2010 AT&T Intellectual Property

`license`
: [http://www.opensource.org/licenses/cpl1.0.txt](https://web.archive.org/web/20141128030244/http://www.opensource.org/licenses/cpl1.0.txt)


