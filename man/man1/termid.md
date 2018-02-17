# NAME

termid - determine terminal type

# SYNOPSIS

termid \[ `-doV` \] \[ `default` \]

# DESCRIPTION

`termid` automatically determines the current terminal type and writes
the type on the standard output. Typical usage is

TERM=\`termid blit\`

\
from within a shell script. Terminals are identified by sending a
`terminal identification sequence` to the terminal and examining the
response.
If the terminal cannot be identified then `default` is output; if
`default` is omitted then nothing is output and `termid` exits with exit
code 1.

The following terminals are properly identified:

`apollo`
:   local apollo network terminals output as `ap1`

`envision`
:   Envision color graphics terminals output as `envis`

`hp`
: HP 2600 series output as `hp`

`tektronics`
:   Tektronics graphics terminals output as `4105` or `4112`

`teletype`
:   DMD 5620 terminals output as `5620`

The options are:

`-d`
: Enable debugging output.

`-o`
: Print debugging output in octal.

`-V`
: Print the program version.

# SEE ALSO

sh(1)

# DIAGNOSTICS

Returns with exit code 1 if the terminal cannot be identified and
`default` is omitted.

# CAVEATS

It is possible for the `terminal identification sequence` to lock up a
terminal not included in the list above. Typing ahead at the terminal
before `termid` completes may cause identification errors.

# AUTHOR

Glenn Fowler

------------------------------------------------------------------------

  -- -- -------------------
        November 07, 2006
  -- -- -------------------


