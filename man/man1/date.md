# NAME

date - set/list/convert dates

# SYNOPSIS

`date` \[ `options` \] \[ +format | date ... | file ... \]

# DESCRIPTION

`date` sets the current date and time (with appropriate privilege),
lists the current date or file dates, or converts dates.
Most common `date` forms are recognized, including those for
[`crontab`](/web/20150717123506/http://www2.research.att.com/~astopen/man/man1/crontab.html)(1),
[`ls`](/web/20150717123506/http://www2.research.att.com/~astopen/man/man1/ls.html)(1),
[`touch`](/web/20150717123506/http://www2.research.att.com/~astopen/man/man1/touch.html)(1),
and the default output from `date` itself.

If the `date` operand consists of 4, 6, 8, 10 or 12 digits followed by
an optional `.` and two digits then it is interpreted as: `HHMM.SS`,
`ddHHMM.SS`, `mmddHHMM.SS`, `mmddHHMMyy.SS` or `yymmddHHMM.SS`, or
`mmddHHMMccyy.SS` or `ccyymmddHHMM.SS`. Conflicting standards and
practice allow a leading or trailing 2 or 4 digit year for the 10 and 12
digit forms; the X/Open trailing form is used to disambiguate
([`touch`](/web/20150717123506/http://www2.research.att.com/~astopen/man/man1/touch.html)(1)
uses the leading form.) Avoid the 10 digit form to avoid confusion. The
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

If more than one `date` operand is specified then:

`1.`
: Each operand sets the reference date for the next operand.

`2.`
: The date is listed for each operand.

`3.`
: The system date is not set.

# OPTIONS

-`a`, --`access-time|atime`
:   List file argument access times.

-`c`, --`change-time|ctime`
:   List file argument change times.

-`d`, --`date`=`date`
:   Use `date` as the current date and do not set the system clock.

-`e`, --`epoch`
:   Output the date in seconds since the epoch. Equivalent to
    `--format=%s`.

-`E`, --`elapsed`
:   Interpret pairs of arguments as start and stop dates, sum the
    differences between all pairs, and list the result as a
    [`fmtelapsed`](/web/20150717123506/http://www2.research.att.com/~astopen/man/man3/fmtelapsed.html)(3)
    elapsed time on the standard output. If there are an odd number of
    arguments then the last time argument is differenced with the
    current time.

-`f`, --`format`=`format`
:   Output the date according to the
    [`strftime`](/web/20150717123506/http://www2.research.att.com/~astopen/man/man3/strftime.html)(3)
    `format`. For backwards compatibility, a first argument of the form
    `+``format` is equivalent to `-f` format. `format` is in
    [`printf`](/web/20150717123506/http://www2.research.att.com/~astopen/man/man3/printf.html)(3)
    style, where %`field` names a fixed size field, zero padded if
    necessary, and \\`c` and \\`nnn` sequences are as in C. Invalid
    %`field` specifications and all other characters are copied
    without change. `field` may be preceded by `%-` to turn off
    padding or `%\_` to pad with space, otherwise numeric fields are
    padded with `0` and string fields are padded with space. `field`
    may also be preceded by `E` for alternate era representation or
    `O` for alternate digit representation (if supported by the
    current locale.) Finally, an integral `width` preceding `field`
    truncates the field to `width` characters. The fields are:

    [`%`]()
    : % character

    [`a`]()
    : abbreviated weekday name

    [`A`]()
    : full weekday name

    [`b`]()
    : abbreviated month name

    [`B`]()
    : full month name

    [`c`]()
    : [`ctime`](/web/20150717123506/http://www2.research.att.com/~astopen/man/man3/ctime.html)(3)
        style date without the trailing newline

    [`C`]()
    : 2-digit century

    [`d`]()
    : day of month number

    [`D`]()
    : date as `mm/dd/yy`

    [`e`]()
    : blank padded day of month number

    [`f`]()
    : locale default override date format

    [`F`]()
    : %ISO 8601:2000 standard date format; equivalent to Y-%m-%d

    [`g`]()
    : [`ls`](/web/20150717123506/http://www2.research.att.com/~astopen/man/man1/ls.html)(1)
        `-l` recent date with `hh:mm`

    [`G`]()
    : [`ls`](/web/20150717123506/http://www2.research.att.com/~astopen/man/man1/ls.html)(1)
        `-l` distant date with `yyyy`

    [`h`]()
    : abbreviated month name

    [`H`]()
    : 24-hour clock hour

    [`i`]()
    : international
        [`date`](/web/20150717123506/http://www2.research.att.com/~astopen/man/man1/date.html)(1)
        date with time zone type name

    [`I`]()
    : 12-hour clock hour

    [`j`]()
    : 1-offset Julian date

    [`J`]()
    : 0-offset Julian date

    [`k`]()
    : [`date`](/web/20150717123506/http://www2.research.att.com/~astopen/man/man1/date.html)(1)
        style date

    [`K`]()
    : all numeric date; equivalent to `%Y-%m-%d+%H:%M:%S`;
        `%\_\[EO\]K` for space separator, %OK adds `.%N`, `%EK`
        adds `%.N%z`, `%\_EK` adds `.%N %z`

    [`l`]()
    : [`ls`](/web/20150717123506/http://www2.research.att.com/~astopen/man/man1/ls.html)(1)
        `-l` date; equivalent to `%Q/%g/%G/`

    [`L`]()
    : locale default date format

    [`m`]()
    : month number

    [`M`]()
    : minutes

    [`n`]()
    : newline character

    [`N`]()
    : nanoseconds 000000000-999999999

    [`p`]()
    : meridian (e.g., `AM` or `PM`)

    [`q`]()
    : time zone type name (nation code)

    [`Q`]()
    : `&lt;del&gt;recent&lt;del&gt;distant&lt;del&gt;`: `&lt;del&gt;`
        is a unique delimter character; `recent` format for recent
        dates, `distant` format otherwise

    [`r`]()
    : 12-hour time as `hh:mm:ss meridian`

    [`R`]()
    : 24-hour time as `hh:mm`

    [`s`]()
    : number of seconds since the epoch; `.prec` preceding `s`
        appends `prec` nanosecond digits, `9` if `prec` is omitted

    [`S`]()
    : seconds 00-60

    [`t`]()
    : tab character

    [`T`]()
    : 24-hour time as `hh:mm:ss`

    [`u`]()
    : weekday number 1(Monday)-7

    [`U`]()
    : week number with Sunday as the first day

    [`V`]()
    : ISO week number (i18n is `fun`)

    [`w`]()
    : weekday number 0(Sunday)-6

    [`W`]()
    : week number with Monday as the first day

    [`x`]()
    : locale date style that includes month, day and year

    [`X`]()
    : locale time style that includes hours and minutes

    [`y`]()
    : 2-digit year (you'll be sorry)

    [`Y`]()
    : 4-digit year

    [`z`]()
    : time zone `SHHMM` west of GMT offset where S is `+` or `-`,
        use pad \_ for `SHH:MM`

    [`Z`]()
    : time zone name

    [`=\[=\]\[-+\]flag`]()
    : \
        set (default or +) or clear (-) `flag` for the remainder of
        `format`, or for the remainder of the process if `==`
        is specified. `flag` may be:

        [`l`]()
        : enable leap second adjustments

        [`n`]()
        : convert `%S` as `%S.%N`

        [`u`]()
        : UTC time zone

    [`\#`]()
    : equivalent to %s

    [`?alternate`]()
    : \
        use `alternate` format if a default format override has not been
        specified, e.g.,
        [`ls`](/web/20150717123506/http://www2.research.att.com/~astopen/man/man1/ls.html)(1)
        uses "%?%l"; export TM\_OPTIONS="format='`override`'" to
        override the default

-`i`, --`incremental|adjust`
:   Set the system time in incrementatl adjustments to avoid complete
    time shift shock. Negative adjustments still maintain monotonic
    increasing time. Not available on all systems.

-`L`, --`last`
:   List only the last time for multiple `date` operands.

-`l`, --`leap-seconds`
:   Include leap seconds in time calculations. Leap seconds after the
    ast library release date are not accounted for.

-`m`, --`modify-time|mtime`
:   List file argument modify times.

-`n`, --`network`
:   Set network time. On by default; -`n` means --`nonetwork`.

-`p`, --`parse`=`format`
:   Add `format` to the list of
    [`strptime`](/web/20150717123506/http://www2.research.att.com/~astopen/man/man3/strptime.html)(3)
    parse conversion formats. `format` follows the same conventions as
    the `--format` option, with the addition of these format fields:

    [`|`]()
    : If the format failed before this point then restart the parse
        with the remaining format.

    [`&`]()
    : Call the
        [`tmdate`](/web/20150717123506/http://www2.research.att.com/~astopen/man/man3/tmdate.html)(3)
        heuristic parser. This is is the default when `--parse`
        is omitted.

-`R`, --`rfc-2822`
:   List date and time in RFC 2822 format (%a, %-e %h %Y %H:%M:%S %z).

-`T`, --`rfc-3339`=`type`
:   List date and time in RFC 3339 format according to `type`:

    [`date`]()
    : (%Y-%m-%d)

    [`seconds`]()
    : \
        (%Y-%m-%d %H:%M:%S%\_z)

    [`ns|nanoseconds`]()
    : \
        (%Y-%m-%d %H:%M:%S.%N%\_z)

-`s`, --`show`
:   Show the date without setting the system time.

-`u`, --`utc|gmt|zulu|universal`
:   Output dates in `coordinated universal time` (UTC).

-`U`, --`unelapsed`=`scale`
:   Interpret each argument as
    [`fmtelapsed`](/web/20150717123506/http://www2.research.att.com/~astopen/man/man3/fmtelapsed.html)(3)
    elapsed time and list the
    [`strelapsed`](/web/20150717123506/http://www2.research.att.com/~astopen/man/man3/strelapsed.html)(3)
    1/`scale` seconds.

-`z`, --`list-zones`
:   List the known time zone table and exit. The table columns are:
    country code, standard zone name, savings time zone name, minutes
    west of `UTC`, and savings time minutes offset. Blank or empty
    entries are listed as `-` .

# SEE ALSO

[`crontab`](/web/20150717123506/http://www2.research.att.com/~astopen/man/man1/crontab.html)(1),
[`ls`](/web/20150717123506/http://www2.research.att.com/~astopen/man/man1/ls.html)(1),
[`touch`](/web/20150717123506/http://www2.research.att.com/~astopen/man/man1/touch.html)(1),
[`fmtelapsed`](/web/20150717123506/http://www2.research.att.com/~astopen/man/man3/fmtelapsed.html)(3),
[`strftime`](/web/20150717123506/http://www2.research.att.com/~astopen/man/man3/strftime.html)(3),
[`strptime`](/web/20150717123506/http://www2.research.att.com/~astopen/man/man3/strptime.html)(3),
[`tm`](/web/20150717123506/http://www2.research.att.com/~astopen/man/man3/tm.html)(3)

# IMPLEMENTATION

`version`
:   date (AT&T Research) 2011-01-27

`author`
:   Glenn Fowler
    &lt;[glenn.s.fowler@gmail.com](https://web.archive.org/web/20150717123506/mailto:glenn.s.fowler@gmail.com)&gt;

`author`
:   David Korn
    &lt;[dgkorn@gmail.com](https://web.archive.org/web/20150717123506/mailto:dgkorn@gmail.com)&gt;

`copyright`
:   Copyright © 1992-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20150717123506/http://www.eclipse.org/org/documents/epl-v10.html)


