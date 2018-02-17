# NAME

ps - report process status

# SYNOPSIS

`ps` \[ `options` \] \[ pid ... \]

# DESCRIPTION

`ps` lists process information subject to the appropriate privilege.
If `pid` arguments are specified then only those processes are listed,
otherwise all processes with the effective user id and controlling
terminal of the caller are listed. The options may alter this default
behavior.
The listings are sorted by &lt;`UID,START,PID`&gt;. Options taking
list arguments accept either space or comma separators.

# OPTIONS

-`a`, --`interactive`
:   List all processes associated with terminals.

-`B`, --`branch`
:   Print tree branch prefixes for `command` and `args`. Implied by
    `--children`, `--parents` , and `--tree`. On by default;
    -`B` means --`nobranch`.

-`c`, --`class`
:   Equivalent to `--fields=pid,class,pri,tty,time,comm`.

-`C`, --`children`
:   Display the process tree hierarchy, including the children of all
    selected processes, in the `CMD` field list.

-`d`, --`no-session`
:   List all processes except session leaders.

-`D`, --`define`=`key\[=value\]`
:   Define `key` with optional `value`. `value` will be expanded when
    `%(``key``)` is specified in `--format`. `key` may override
    internal `--format` identifiers.

-`e|A`, --`all`
:   List all processes.

-`E`, --`escape`
:   Escape non-printing characters in `command` and `args`. On by
    default; -`E` means --`noescape`.

-`f`, --`full`
:   Equivalent to `--fields=user,pid,ppid,start,tty,time,cmd`.

-`F`, --`format`=`format`
:   Append to the listing format string (if `--format` is specified
    then `--fields` and all options that modify `--fields`
    are ignored.) The
    [`df`](/web/20141128030248/http://www2.research.att.com/~astopen/man/man1/df.html)(1),
    [`ls`](/web/20141128030248/http://www2.research.att.com/~astopen/man/man1/ls.html)(1)
    and
    [`pax`](/web/20141128030248/http://www2.research.att.com/~astopen/man/man1/pax.html)(1)
    commands also have `--format` options in this same style. `format`
    follows
    [`printf`](/web/20141128030248/http://www2.research.att.com/~astopen/man/man3/printf.html)(3)
    conventions, except that
    [`sfio`](/web/20141128030248/http://www2.research.att.com/~astopen/man/man3/sfio.html)(3)
    inline ids are used instead of arguments:
    %\[\#-+\]\[`width`\[.`precis` \[.`base`\]\]\](`id`\[:`heading`\])`char`. If `\#` is specified
    then the internal width and precision are used. If `char` is `s`
    then the string form of the item is listed, otherwise the
    corresponding numeric form is listed. If `char` is `q` then the
    string form of the item is \$'...' quoted if it contains space or
    non-printing characters. If `width` is omitted then the default
    width is assumed. `heading` overrides the default heading for `id`.
    Supported `id`s are:

    [`addr`]()
    : Physical address. The title string is `ADDR` and the default
        width is 8.

    [`class`]()
    : \
        Scheduling class. The title string is `CLS` and the default
        width is 3. Not available on this system.

    [`cmd`]()
    : Command path with arguments. The title string is `CMD` and the
        default width is -32.

    [`comm`]()
    : Command file base name. The title string is `COMMAND` and the
        default width is -24.

    [`cpu`]()
    : Cpu percent usage. The title string is `%CPU` and the default
        width is 4.

    [`etime`]()
    : \
        Elapsed time since start. The title string is `ELAPSED` and
        the default width is 7.

    [`flags`]()
    : \
        State flags (octal and additive). The title string is `F` and
        the default width is 3.

    [`gid`]()
    : Numeric group id. The title string is `GROUP` and the default
        width is 8. Not available on this system.

    [`group`]()
    : \
        Group id name. The title string is `GROUP` and the default
        width is 8. Not available on this system.

    [`job`]()
    : Job id. The title string is `JOB` and the default width is 5.

    [`nice`]()
    : Adjusted scheduling priority. The title string is `NI` and the
        default width is 4.

    [`npid`]()
    : Native process id. The title string is `NPID` and the default
        width is 5. Not available on this system.

    [`pgrp`]()
    : Process group id. The title string is `PGRP` and the default
        width is 5.

    [`pid`]()
    : Process id. The title string is `PID` and the default width
        is 5.

    [`ppid`]()
    : Parent process id. The title string is `PPID` and the default
        width is 5.

    [`pri`]()
    : Scheduling priority. The title string is `PRI` and the default
        width is 3.

    [`processor`]()
    : \
        Assigned processor. The title string is `PROC` and the default
        width is 3. Not available on this system.

    [`refcount`]()
    : \
        Reference count. The title string is `REFS` and the default
        width is 4. Not available on this system.

    [`rss`]()
    : Resident page set size in kilobytes. The title string is `RSS`
        and the default width is 5.

    [`sid`]()
    : Session id. The title string is `SID` and the default width
        is 5.

    [`size`]()
    : Virtual memory size in kilobytes. The title string is `SIZE`
        and the default width is 6.

    [`start`]()
    : \
        Start time. The title string is `START` and the default width
        is 8.

    [`state`]()
    : \
        Basic state. The title string is `S` and the default width
        is 1.

    [`tgrp`]()
    : Terminal group id. The title string is `TGRP` and the default
        width is 5.

    [`time`]()
    : usr+sys time. The title string is `TIME` and the default width
        is 6.

    [`tty`]()
    : Controlling terminal base name. The title string is `TT` and
        the default width is -7.

    [`uid`]()
    : Numeric user id. The title string is `USER` and the default
        width is 8.

    [`user`]()
    : User id name. The title string is `USER` and the default width
        is 8.

    [`wchan`]()
    : \
        Wait address. The title string is `WCHAN` and the default
        width is 8.

    [`args`]()
    : Equivalent to `cmd`.

    [`command`]()
    : \
        Equivalent to `cmd`.

    [`f`]()
    : Equivalent to `flags`.

    [`jid`]()
    : Equivalent to `job`.

    [`ntpid`]()
    : \
        Equivalent to `npid`.

    [`pcpu`]()
    : Equivalent to `cpu`.

    [`pgid`]()
    : Equivalent to `pgrp`.

    [`proc`]()
    : Equivalent to `processor`.

    [`psr`]()
    : Equivalent to `processor`.

    [`rgroup`]()
    : \
        Equivalent to `group`.

    [`ruser`]()
    : \
        Equivalent to `user`.

    [`s`]()
    : Equivalent to `state`.

    [`sess`]()
    : Equivalent to `sid`.

    [`stime`]()
    : \
        Equivalent to `start`.

    [`tid`]()
    : Equivalent to `tgrp`.

    [`vsz`]()
    : Equivalent to `size`.

-`g`, --`pgrps|process-groups`=`pgrp...`
:   List processes with group leaders in the `pgrp` list.

-`G`, --`groups`=`group...`
:   List processes with real group id names or numbers in the
    `group` list.

-`h`, --`heading`
:   Output a heading line. On by default; -`h` means --`noheading`.

-`j`, --`jobs`
:   Equivalent to `--fields=pid,pgrp,sid,tty,time,comm`.

-`l`, --`long`
:   Equivalent to
    `--fields=flags,state,user,pid,ppid,pri,nice,size,rss,wchan,tty,time,cmd`.

-`L`, --`leaders`
:   List session leaders.

-`n`, --`namelist`
:   Specifies an alternate system namelist `file`. Ignored by
    this implementation.

-`N`, --`default`
:   Equivalent to `--fields=pid,tty,time,comm`. This is the format
    when `--fields` is not specified.

-`o`, --`fields`=`key\[+width\]\[=label\]...`
:   (`--format` is more general.) List information according to
    `key` . Multiple `--fields` options may be specified; the
    resulting format is a left-right ordered list with duplicate entries
    deleted from the right. The default width can be overriden by
    appending `+width` to `key`, and the default `label` can be
    overridden by appending `=label` to `key`. The keys, labels and
    widths are listed under `--format`.

-`p`, --`pids`=`pid...`
:   List processes in the `pid` list.

-`P`, --`parents`
:   Display the process tree hierarchy, including the parents of all
    selected processes, in the `CMD` field list.

-`r|R`, --`recursive`
:   Recursively list the children of all selected processes.

-`s`, --`sessions`=`sid...`
:   List processes with session leaders in the `sid` list.

-`t`, --`terminals|ttys`=`tty...`
:   List processes with controlling terminals in the `tty` list.

-`T`, --`tree|forest`
:   Display the process tree hierarchy, including the parents and
    children of all selected processes, in the `CMD` field list.

-`u|U`, --`users`=`user...`
:   List processes with real user id names or numbers in the
    `user` list.

-`v`, --`verbose`
:   List verbose error messages for inaccessible processes.

-`w`, --`wide`
:   Ignored by this implementation.

-`x`, --`detached`
:   List all processes not associated with terminals.

-`X`, --`hex`
:   List numeric entries in hexadecimal notation.

# SEE ALSO

[`df`](/web/20141128030248/http://www2.research.att.com/~astopen/man/man1/df.html)(1),
[`kill`](/web/20141128030248/http://www2.research.att.com/~astopen/man/man1/kill.html)(1),
[`ls`](/web/20141128030248/http://www2.research.att.com/~astopen/man/man1/ls.html)(1),
[`nice`](/web/20141128030248/http://www2.research.att.com/~astopen/man/man1/nice.html)(1),
[`pax`](/web/20141128030248/http://www2.research.att.com/~astopen/man/man1/pax.html)(1),
[`ps`](/web/20141128030248/http://www2.research.att.com/~astopen/man/man1/ps.html)(1),
[`sh`](/web/20141128030248/http://www2.research.att.com/~astopen/man/man1/sh.html)(1),
[`top`](/web/20141128030248/http://www2.research.att.com/~astopen/man/man1/top.html)(1)

# IMPLEMENTATION

`version`
:   ps (AT&T Research) 2011-12-13

`author`
:   Glenn Fowler
    &lt;[glenn.s.fowler@gmail.com](https://web.archive.org/web/20141128030248/mailto:glenn.s.fowler@gmail.com)&gt;

`copyright`
:   Copyright © 1998-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030248/http://www.eclipse.org/org/documents/epl-v10.html)


