# NAME

touch - change file access, modification and status change times

# SYNOPSIS

`touch` \[ `options` \] \[ date \]file ...

# DESCRIPTION

`touch` changes the modification time, access time or both of each
`file`. The modification time is the `st\_mtime` member of the
[`stat`](/web/20150717132046/http://www2.research.att.com/~astopen/man/man2/stat.html)(2)
information and the access time is the `st\_atime` member. On most
systems the file status change time is always set to the current time
when either the access or modification times are changed.
If neither the `--reference` nor the `--time` options are specified
then the time used will be the `date` operand or the current time if
`date` is omitted.

If the `date` operand consists of 4, 6, 8, 10 or 12 digits followed by
an optional `.` and two digits then it is interpreted as: `HHMM.SS`,
`ddHHMM.SS`, `mmddHHMM.SS`, `mmddHHMMyy.SS` or `yymmddHHMM.SS`, or
`mmddHHMMccyy.SS` or `ccyymmddHHMM.SS`. Conflicting standards and
practice allow a leading or trailing 2 or 4 digit year for the 10 and 12
digit forms; the X/Open leading form is used to disambiguate
([`date`](/web/20150717132046/http://www2.research.att.com/~astopen/man/man1/date.html)(1)
uses the trailing form.) Avoid the 10 digit form to avoid confusion. The
digit fields are:

`cc`
: Century - 1, 19-20.

`yy`
: Year in century, 00-99.

`mm`
: Month, 01-12.

`dd`
: Day of month, 01-31.

`HH`
: Hour, 00-23.

`MM`
: Minute, 00-59.

`SS`
: Seconds, 00-60.

# OPTIONS

-`a`, --`access|atime|use`
:   Change the access time. Do not change the modification time unless
    `--modify` is also specified.

-`c`, --`create`
:   Create the `file` if it does not exist, but write no diagnostic. On
    by default; -`c` means --`nocreate`.

-`f`, --`force`
:   Ignored by this implementation.

-`m`, --`modify|mtime|modification`
:   Change the modify time. Do not change the access time unless
    `--access` is also specified.

-`r`, --`reference`=`file`
:   Use the corresponding time of `file` instead of the current time.

-`s|n`, --`change|ctime|neither`
:   Change only the file status change time `st\_ctime`. Most systems
    summarily set `st\_ctime` to the current time.

-`t|d`, --`time|date`=`date-time`
:   Use the specified `date-time` instead of the current date-time. Most
    common formats are accepted. See
    [`tmdate`](/web/20150717132046/http://www2.research.att.com/~astopen/man/man3/tmdate.html)(3)
    for details. If `date-time` consists of 4, 6, 8, 10 or 12 digits
    followed by an optional `.` and 2 digits and another optional
    `.` and 1 or more digits then it is interpreted as the `date`
    operand above, except that the leading 2 or 4 digit year form is
    used to disambiguate. Avoid the 10 digit form to avoid confusion. If
    `--reference` is specified or if `file` already exists then `time`
    may also be one of:

    [`access|atime|use`]()
    : \
        The access time of the reference file.

    [`change|ctime`]()
    : \
        The change time of the reference file.

    [`modify|mtime|modification`]()
    : \
        The modify time of the reference file.

-`v`, --`verbose`
:   Write a diagnostic for each nonexistent `file`.

# CAVEATS

Some systems or file system types may limit the range of times that can
be set. These limitations may not show up until a subsequent
[`stat`](/web/20150717132046/http://www2.research.att.com/~astopen/man/man2/stat.html)(2)
call (yes, the time can be set but not checked!) Upper limits of
&lt;0xffffffff and &lt;0x7fffffff have been observed.

# SEE ALSO

[`date`](/web/20150717132046/http://www2.research.att.com/~astopen/man/man1/date.html)(1),
[`nmake`](/web/20150717132046/http://www2.research.att.com/~astopen/man/man1/nmake.html)(1),
[`utime`](/web/20150717132046/http://www2.research.att.com/~astopen/man/man2/utime.html)(2),
[`tm`](/web/20150717132046/http://www2.research.att.com/~astopen/man/man3/tm.html)(3)

# IMPLEMENTATION

`version`
:   touch (AT&T Research) 2004-12-12

`author`
:   Glenn Fowler
    &lt;[glenn.s.fowler@gmail.com](https://web.archive.org/web/20150717132046/mailto:glenn.s.fowler@gmail.com)&gt;

`copyright`
:   Copyright © 1989-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20150717132046/http://www.eclipse.org/org/documents/epl-v10.html)


