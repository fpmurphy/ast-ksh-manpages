# NAME

dlls - list dlls and shared libraries on \$PATH

# SYNOPSIS

`dlls` \[ `options` \] \[ plugin \[ name \[ version \[ symbol ... \]
\] \] \]

# DESCRIPTION

`dlls` lists the base name and full path, one per line, of `dlls` and
`shared libraries` found in the directories or sibling directories in
the `PATH` environment variable. The `plugin` operand matches plugin
libraries for the particular `plugin`. If omitted or `-` then no
plugins are matched. The `name` operand is the library base name. All
base names are matched if omitted or `-`. The `version` operand
specifies a specific library version and is an implementation specific
sequence of decimal digits and dots. The latest version is matched if
omitted or `-`. Only the first path for each library base name is
listed. If no options are specified then `--base` `--path` is
assumed.
`symbol` operands, if specified, are searched for in each matched
library. The address or lookup error is listed for each library and
`symbol`.

# OPTIONS

-`b`, --`base`
:   List the `dll` or `shared library` base names.

-`c`, --`containing`
:   Only list libraries containing at least one of the
    `symbol` operands.

-`i`, --`info`
:   List native dll naming and location information.

-`l`, --`long`
:   List the base name, plugin YYYYMMDD version stamp, and full path for
    each shared library. Libraries with no plugin version stamp have
    version stamp 00000000.

-`p`, --`path`
:   List the `dll` or `shared library` path names.

# SEE ALSO

[`find`](/web/20141128030242/http://www2.research.att.com/~astopen/man/man1/find.html)(1),
[`dllscan`](/web/20141128030242/http://www2.research.att.com/~astopen/man/man3/dllscan.html)(3)

# IMPLEMENTATION

`version`
:   dlls (AT&T Research) 2011-04-22

`author`
:   Glenn Fowler

`copyright`
:   Copyright © 2002-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030242/http://www.eclipse.org/org/documents/epl-v10.html)


