# NAME

stty - set or get terminal modes

# SYNOPSIS

`stty` \[ `options` \] \[mode ...\]

# DESCRIPTION

`stty` sets certain terminal I/O modes for the device that is the
current standard input; without arguments, it writes the settings of
certain modes to standard output.

# OPTIONS

-`a`, --`all`
:   Writes to standard output all of the mode settings.

-`f|F`, --`fd|file`=`fd`
:   Use `fd` as the terminal fd. The default value is `0`.

-`g`, --`save`
:   Writes the current settings to standard output in a form that can be
    used as an argument to another `stty` command. The `rows` and
    `columns` values are not included.

-`t`, --`terminal-group`
:   Print the terminal group id of the device, -1 if unknown.

# EXTENDED DESCRIPTION

Modes are specified either as a single name or as a name followed by a
value. As indicated below, many of the mode names can be preceded by a
`-` to negate its meaning. Modes are listed by group corresponding to
field in the `termios` structure defined in `&lt;termios.h&gt;`.
Modes in the last group are implemented using options in the previous
groups. Note that many combinations of modes make no sense, but no
sanity checking is performed. The modes are selected from the following:
[`Control Modes.`]()

`parenb` (-parenb)
:   Enable (disable) parity generation and detection.

`parodd` (-parodd)
:   Use odd (even) parity.

`cread` (-cread)
:   Enable (disable) input.

`hupcl` (-hupcl)
:   Hangup (do not hangup) connection on last close.

`hup` (-hup)
:   Same as `hupcl`.

`cstopb` (-cstopb)
:   Use two (one) stop bits.

`crtscts` (-crtscts)
:   Enable (disable) RTS/CTS handshaking.

`clocal` (-clocal)
:   Disable (enable) modem control signals.

`0 50 75 110 134 150 200 300 600 1200 1800 2400 4800 9600 19200 38400`
:   Attempt to set input and output baud rate to number given. A value
    of `0` causes immediate hangup.

`ispeed` `n`
:   `n` is the input baud rate.

`ospeed` `n`
:   `n` is the output baud rate.

`line` `n`
:   Line discipline number.

`min` `n`
:   Mininmum number of characters to read in raw mode.

`time` `n`
:   Number of .1 second intervals with raw mode.

`cs5 cs6 cs7 cs8`
:   Number of bits in a character.

[`Input Modes.`]()

`ignbrk` (-ignbrk)
:   Ignore (do not ignore) break characters.

`brkint` (-brkint)
:   Generate (do not generate) INTR signal on break.

`ignpar` (-ignpar)
:   Ignore (do not ignore) characters with parity errors.

`parmrk` (-parmrk)
:   Mark (do not mark) parity errors.

`inpck` (-inpck)
:   Enable (disable) input parity checking.

`istrip` (-istrip)
:   Clear (do not clear) high bit of input characters.

`inlcr` (-inlcr)
:   Translate (do not translate) carriage return to newline.

`igncr` (-igncr)
:   Ignore (do not ignore) carriage return.

`iuclc` (-iuclc)
:   Map (do not map) upper-case to lower case.

`ixon` (-ixon)
:   Enable (disable) XON/XOFF flow control. `stop` character
    stops output.

`ixany` (-ixany)
:   Any character (only start character) can restart output..

`decctlq` (-decctlq)
:   Same as `-ixany`.

`ixoff` (-ixoff)
:   Disable (enable) XON/XOFF flow control.

`imaxbel` (-imaxbel)
:   Beep (do not beep) if a character arrives with full input buffer.

`icrnl` (-icrnl)
:   Translate (do not translate) carriage return to newline.

[`Output Modes.`]()

`olcuc` (-olcuc)
:   Translate (do not translate) lowercase characters to uppercase.

`onlcr` (-onlcr)
:   Translate (do not translate) newline to carriage return-newline.

`onlret` (-onlret)
:   Newline performs (does not perform) a carriage return.

`ocrnl` (-ocrnl)
:   Translate (do not translate) carriage return to newline.

`onocr` (-onocr)
:   Do not (do) print carriage returns in the first column.

`ofill` (-ofill)
:   Use fill characters (use timing) for delays.

`ofdel` (-ofdel)
:   Use DEL (NUL) as fill characters for delays.

`opost` (-opost)
:   Postprocess (do not postprocess) output.

`cr0 cr1 cr2 cr3`
:   Carriage return delay style.

`nl0 nl1`
:   Newline delay style.

`tab0 tab1 tab2 tab3`
:   Horizontal tab delay style.

`bs0 bs1`
:   Backspace delay style.

`ff0 ff1`
:   Form feed delay style.

`vt0 vt1`
:   Vertical tab delay style.

[`Local Modes.`]()

`isig` (-isig)
:   Enable (disable) `intr`, `quit`, and `susp`
    special characters.

`icanon` (-icanon)
:   Enable (disable) `erase`, `kill`, `werase`, and `rprnt`
    special characters.

`iexten` (-iexten)
:   Enable (disable) non-POSIX special characters.

`echo` (-echo)
:   Echo (do not echo) input characters.

`echoe` (-echoe)
:   Echo (do not echo) erase characters as backspace-space-backspace.

`echok` (-echok)
:   Echo (do not echo) a newline after a kill character.

`echoke` (-echoke)
:   Echo (do not echo) a newline after a kill character.

`lfkc` (-lfkc)
:   Same as `echok` (`-echok`); obsolete.

`echonl` (-echonl)
:   Echo (do not echo) newline even if not echoing other character.

`echoctl` (-echoctl)
:   Echo (do not echo) control characters as `\^``c`.

`echoprt` (-echoprt)
:   Echo (do not echo) erased characters backward, between '\\' and '/'.

`xcase` (-xcase)
:   Enable (disable) `icanon` uppercase as lowercase with '\\' prefix.

`flusho` (-flusho)
:   Discard (do not discard) written data. Cleared by subsequent input.

`pendin` (-pendin)
:   Redisplay pending input at next read and then automatically clear
    `pendin` .

`noflsh` (-noflsh)
:   Disable (enable) flushing after `intr` and `quit`
    special characters.

`tostop` (-tostop)
:   Stop (do not stop) background jobs that try to write to
    the terminal.

[`Control Assignments.`]()
If `c` is `undef` or an empty string then the control assignment is
disabled.

`rows` `n`
:   `n` is the number of lines for display.

`cols` `n`
:   `n` is the number of columns for display.

`columns` `n`
:   Same as `cols`.

`intr` `c`
:   Send an interrupt signal.

`quit` `c`
:   Send a quit signal.

`erase` `c`
:   Erase the last character entered.

`kill` `c`
:   Erase the current line.

`eof` `c`
:   Send an end of file.

`eol2` `c`
:   Alternate character to end the line.

`eol` `c`
:   End the line.

`start` `c`
:   Restart the output after stopping it.

`stop` `c`
:   Stop the output.

`susp` `c`
:   Send a terminal stop signal.

`rprnt` `c`
:   Redraw the current line.

`flush` `c`
:   Discard output.

`werase` `c`
:   Erase the last word entered.

`lnext` `c`
:   Enter the next input character literally.

[`Combination Modes.`]()

`ek`
: Reset the `erase` and `kill` special characters to their
    default values.

`evenp`
:   Same as `parenb -parodd cs7`.

`lcase`
:   Set `xcase`, `iuclc`, and `olcuc`.

`oddp`
: Same as `parenb parodd cs7`.

`parity`
:   Same as parenb `-parodd cs7`.

`sane`
: Reset all modes to some reasonable values.

`tabs`
: Preserve (expand to spaces) tabs.

`LCASE`
:   Same as `lcase`.

# IMPLEMENTATION

`version`
:   stty (AT&T Research) 2010-04-01

`author`
:   Glenn Fowler
    &lt;[glenn.s.fowler@gmail.com](https://web.archive.org/web/20150817032527/mailto:glenn.s.fowler@gmail.com)&gt;

`author`
:   David Korn
    &lt;[dgkorn@gmail.com](https://web.archive.org/web/20150817032527/mailto:dgkorn@gmail.com)&gt;

`copyright`
:   Copyright © 1992-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20150817032527/http://www.eclipse.org/org/documents/epl-v10.html)


