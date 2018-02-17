# NAME

mamprobe - generate MAM cc probe info

# SYNOPSIS

`mamprobe` \[ `options` \] info-file cc-path

# DESCRIPTION

`mamprobe` generates MAM (make abstract machine)
[`cc`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/cc.html)(1)
probe information for use by
[`mamake`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/mamake.html)(1).
`cc-path` is the absolute path of the probed compiler and `info-file` is
where the information is placed. `info-file` is usually
`\$INSTALLROOT/lib/probe/C/mam/``hash`, where `hash` is a hash of
`cc-path`. Any `info-file` directories are created if needed. If
`info-file` is `-` then the probe information is written to the
standard output.
`mamprobe` and `mamake` are used in the bootstrap phase of
[`package`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/package.html)(1)
installation before
[`nmake`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/nmake.html)(1)
is built. The probed variable names are the
[`nmake`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/nmake.html)(1)
names with a `mam\_` prefix, `CC` converted to `cc`, and `.`
converted to `\_`. Additional variables are:

`\_hosttype\_`
:   the
    [`package`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/package.html)(1)
    host type

`mam\_cc\_L`
:   `-L``dir` supported

`STDCAT`
:   command to execute for
    [`cat`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/cat.html)(1);
    prefixed by
    [`execrate`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/execrate.html)(1)
    on `.exe` challenged systems

`STDCHMOD`
:   command to execute for
    [`chmod`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/chmod.html)(1);
    prefixed by
    [`execrate`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/execrate.html)(1)
    on `.exe` challenged systems

`STDCMP`
:   command to execute for
    [`cmp`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/cmp.html)(1);
    prefixed by
    [`execrate`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/execrate.html)(1)
    on `.exe` challenged systems

`STDCP`
:   command to execute for
    [`cp`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/cp.html)(1);
    prefixed by
    [`execrate`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/execrate.html)(1)
    on `.exe` challenged systems

`STDED`
:   command to execute for
    [`ed`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/ed.html)(1)
    or
    [`ex`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/ex.html)(1)

`STDEDFLAGS`
:   flags for `STDED`

`STDLN`
:   command to execute for
    [`ln`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/ln.html)(1);
    prefixed by
    [`execrate`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/execrate.html)(1)
    on `.exe` challenged systems

`STDMV`
:   command to execute for
    [`mv`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/mv.html)(1);
    prefixed by
    [`execrate`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/execrate.html)(1)
    on `.exe` challenged systems

`STDRM`
:   command to execute for
    [`rm`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/rm.html)(1);
    prefixed by
    [`execrate`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/execrate.html)(1)
    on `.exe` challenged systems

# OPTIONS

-`d`, --`debug`
:   Enable probe script debug trace.

# SEE ALSO

[`execrate`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/execrate.html)(1),
[`package`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/package.html)(1),
[`mamake`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/mamake.html)(1),
[`nmake`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/nmake.html)(1),
[`probe`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/probe.html)(1)

# IMPLEMENTATION

`version`
:   mamprobe (AT&T Labs Research) 2011-02-11


