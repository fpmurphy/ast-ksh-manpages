# NAME

`mail` - send and receive mail

# SYNOPSIS

\
`mail` `\[-iInv\]` `\[-s` `subject``\]` `\[-c` `cc-addr``\]`
`\[-b` `bcc-addr``\]` `to-addr...`\
`mail` `\[-iInNv\]` `-f` `\[``name``\]`\
`mail` `\[-iInNv\]` `\[-u` `user``\]`

# INTRODUCTION

`Mail` is an intelligent mail processing system, which has a command
syntax reminiscent of
[`ed`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/%3C!--NULL--%3Eed.html)(1)
with lines replaced by messages.

`-v`
: Verbose mode. The details of delivery are displayed on the
    user's terminal.

`-i`
: Ignore tty interrupt signals. This is particularly useful when using
    `mail` on noisy phone lines.

`-I`
: Forces mail to run in interactive mode even when input isn't a
    terminal. In particular, the \```~``' special character when
    sending mail is only active in interactive mode.

`-n`
: Inhibits reading `/etc/mail.rc` upon startup.

`-N`
: Inhibits the initial display of message headers when reading mail or
    editing a mail folder.

`-s`
: Specify subject on command line (only the first argument after the
    `-s` flag is used as a subject; be careful to quote subjects
    containing spaces.)

`-c`
: Send carbon copies to `list` of users.

`-b`
: Send blind carbon copies to `list`. List should be a comma-separated
    list of names.

`-f`
: Read in the contents of your `mbox` (or the specified file) for
    processing; when you `quit`, `mail` writes undeleted messages back
    to this file.

`-u`

: Is equivalent to:

    : `mail -f /var/mail/user`

## Sending mail

To send a message to one or more people, `mail` can be invoked with
arguments which are the names of people to whom the mail will be sent.
You are then expected to type in your message, followed by an
\``control-D`' at the beginning of a line. The section below `Replying
to or originating mail`, describes some features of `mail` available
to help you compose your letter.

## Reading mail

In normal usage `mail` is given no arguments and checks your mail out
of the post office, then prints out a one line header of each message
found. The current message is initially the first message (numbered 1)
and can be printed using the ``print`` command (which can be
abbreviated \``p`).' You can move among the messages much as you move
between lines in
[`ed`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/%3C!--NULL--%3Eed.html)(1),
with the commands \``+`' and \``-`' moving backwards and forwards, and
simple numbers.

## Disposing of mail

After examining a message you can ``delete`` \``d`)' the message or
``reply`` \``r`)' to it. Deletion causes the `mail` program to
forget about the message. This is not irreversible; the message can be
``undeleted`` \``u`)' by giving its number, or the `mail` session
can be aborted by giving the ``exit`` \``x`)' command. Deleted
messages will, however, usually disappear never to be seen again.

## Specifying messages

Commands such as ``print`` and ``delete`` can be given a list of
message numbers as arguments to apply to a number of messages at once.
Thus \`\``delete 1 2`'' deletes messages 1 and 2, while
\`\``delete 1-5`'' deletes messages 1 through 5. The special name \````'
addresses all messages, and \``$`' addresses the last message; thus the
command ``top`` which prints the first few lines of a message could be
used in \`\``top ``'' to print the first few lines of all messages.

## Replying to or originating mail

You can use the ``reply`` command to set up a response to a message,
sending it back to the person who it was from. Text you then type in, up
to an end-of-file, defines the contents of the message. While you are
composing a message, `mail` treats lines beginning with the character
\``~`' specially. For instance, typing \``~m`' (alone on a line) will
place a copy of the current message into the response right shifting it
by a tabstop (see `indentprefix` variable, below). Other escapes will
set up subject fields, add and delete recipients to the message and
allow you to escape to an editor to revise the message or to a shell to
run some commands. (These options are given in the summary below.)

## Ending a mail processing session

You can end a `mail` session with the ``quit`` \``q`)' command.
Messages which have been examined go to your `mbox` file unless they
have been deleted in which case they are discarded. Unexamined messages
go back to the post office. (See the `-f` option above).

## Personal and systemwide distribution lists

It is also possible to create a personal distribution lists so that, for
instance, you can send mail to \`\``cohorts`'' and have it go to a group
of people. Such lists can be defined by placing a line like

: `alias cohorts bill ozalp jkf mark kridle@ucbcory`

in the file `.mailrc` in your home directory. The current list of such
aliases can be displayed with the ``alias`` command in `mail` System
wide distribution lists can be created by editing `/etc/aliases`, see
[`aliases`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man5/aliases.html)(5)
and
[`sendmail`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man8/sendmail.html)(8);
these are kept in a different syntax. In mail you send, personal aliases
will be expanded in mail sent to others so that they will be able to
``reply`` to the recipients. System wide ``aliases`` are not
expanded when the mail is sent, but any reply returned to the machine
will have the system wide alias expanded as all mail goes through
[`sendmail`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man./sendmail.html)(.)

## Network mail (ARPA, UUCP, Berknet)

See
[`mailaddr`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man7/mailaddr.html)(7)
for a description of network addresses.
`Mail` has a number of options which can be set in the `.mailrc` file
to alter its behavior; thus \`\``set askcc`'' enables the `askcc`
feature. (These options are summarized below.)

# SUMMARY

(Adapted from the \`Mail Reference Manual')
Each command is typed on a line by itself, and may take arguments
following the command word. The command need not be typed in its
entirety - the first command which matches the typed prefix is used. For
commands which take message lists as arguments, if no message list is
given, then the next message forward which satisfies the command's
requirements is used. If there are no messages forward of the current
message, the search proceeds backwards, and if there are no good
messages at all, `mail` types \`\``applicable messages`'' and aborts
the command.

``-``
: Print out the preceding message. If given a numeric argument `n`,
    goes to the `n`'th previous message and prints it.

``?``
: Prints a brief summary of commands.

``!``
: Executes the shell (see
    [`sh`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/sh.html)(1)
    and
    [`csh`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/csh.html)(1))
    command which follows.

``Print``
:   (``P``) Like ``print`` but also prints out ignored header
    fields. See also ``print``, ``ignore`` and ``retain``.

``Reply``
:   (``R``) Reply to originator. Does not reply to other recipients of
    the original message.

``Type``
: (``T``) Identical to the ``Print`` command.

``alias``
:   (``a``) With no arguments, prints out all currently-defined
    aliases. With one argument, prints out that alias. With more than
    one argument, creates a new alias or changes an old one.

``alternates``
:   (``alt``) The ``alternates`` command is useful if you have
    accounts on several machines. It can be used to inform `mail` that
    the listed addresses are really you. When you ``reply`` to
    messages, `mail` will not send a copy of the message to any of the
    addresses listed on the ``alternates`` list. If the
    ``alternates`` command is given with no argument, the current set
    of alternate names is displayed.

``chdir``
:   (``c``) Changes the user's working directory to that specified, if
    given. If no directory is given, then changes to the user's
    login directory.

``copy``
: (``co``) The ``copy`` command does the same thing that
    ``save`` does, except that it does not mark the messages it is
    used on for deletion when you quit.

``delete``
:   (``d``) Takes a list of messages as argument and marks them all as
    deleted. Deleted messages will not be saved in `mbox`, nor will they
    be available for most other commands.

``dp``
: (also ``dt``) Deletes the current message and prints the next
    message. If there is no next message, `mail` says \`\``at EOF`.''

``edit``
: (``e``) Takes a list of messages and points the text editor at
    each one in turn. On return from the editor, the message is read
    back in.

``exit``
: ( ``ex`` or ``x``) Effects an immediate return to the Shell
    without modifying the user's system mailbox, his `mbox` file, or his
    edit file in `-f`.

``file``
: (``fi``) The same as ``folder``.

``folders``
:   List the names of the folders in your folder directory.

``folder``
:   (``fo``) The ``folder`` command switches to a new mail file or
    folder. With no arguments, it tells you which file you are currently
    reading. If you give it an argument, it will write out changes (such
    as deletions) you have made in the current file and read in the new
    file. Some special conventions are recognized for the name. \# means
    the previous file, % means your system mailbox, %user means user's
    system mailbox, & means your `mbox` file, and +folder means a file
    in your folder directory.

``from``
: (``f``) Takes a list of messages and prints their message headers.

``headers``
:   (``h``) Lists the current range of headers, which is an 18-message
    group. If a \``+`' argument is given, then the next 18-message group
    is printed, and if a \``-`' argument is given, the previous
    18-message group is printed.

``help``
: A synonym for ``?``

``hold``
: ( ``ho``, also ``preserve``) Takes a message list and marks each
    message therein to be saved in the user's system mailbox instead of
    in `mbox`. Does not override the ``delete`` command.

``ignore``
:   Add the list of header fields named to the `ignored list`. Header
    fields in the ignore list are not printed on your terminal when you
    print a message. This command is very handy for suppression of
    certain machine-generated header fields. The ``Type`` and
    ``Print`` commands can be used to print a message in its entirety,
    including ignored fields. If ``ignore`` is executed with no
    arguments, it lists the current set of ignored fields.

``inc``
: Incorporate any new messages that have arrived while mail is being
    read. The new messages are added to the end of the message list, and
    the current message is reset to be the first new mail message. This
    does not renumber the existing message list, nor does does it cause
    any changes made so far to be saved.

``mail``
: (``m``) Takes as argument login names and distribution group names
    and sends mail to those people.

``mbox``
: Indicate that a list of messages be sent to ``mbox`` in your home
    directory when you quit. This is the default action for messages if
    you do `not` have the ``hold`` option set.

``next``
: (``n``) like ``+`` or CR) Goes to the next message in sequence
    and types it. With an argument list, types the next
    matching message.

``preserve``
:   (``pre``) A synonym for ``hold``.

``print``
:   (``p``) Takes a message list and types out each message on the
    user's terminal.

``quit``
: (``q``) Terminates the session, saving all undeleted, unsaved
    messages in the user's `mbox` file in his login directory,
    preserving all messages marked with ``hold`` or ``preserve`` or
    never referenced in his system mailbox, and removing all other
    messages from his system mailbox. If new mail has arrived during the
    session, the message \`\``You have new mail`'' is given. If given
    while editing a mailbox file with the `-f` flag, then the edit
    file is rewritten. A return to the Shell is effected, unless the
    rewrite of edit file fails, in which case the user can escape with
    the ``exit`` command.

``reply``
:   (``r``) Takes a message list and sends mail to the sender and all
    recipients of the specified message. The default message must not
    be deleted.

``respond``
:   A synonym for ``reply``.

``retain``
:   Add the list of header fields named to the `retained list` Only the
    header fields in the retain list are shown on your terminal when you
    print a message. All other header fields are suppressed. The
    ``Type`` and ``Print`` commands can be used to print a message
    in its entirety. If ``retain`` is executed with no arguments, it
    lists the current set of retained fields.

``save``
: (``s``) Takes a message list and a filename and appends each
    message in turn to the end of the file. The filename in quotes,
    followed by the line count and character count is echoed on the
    user's terminal.

``set``
: (``se``) With no arguments, prints all variable values. Otherwise,
    sets option. Arguments are of the form `option=value` (no space
    before or after =) or `option`. Quotation marks may be placed around
    any part of the assignment statement to quote blanks or tabs, i.e.
    \`\``set indentprefix=->`''

``saveignore``
:   ``Saveignore`` is to ``save`` what ``ignore`` is to
    ``print`` and ``type``. Header fields thus marked are filtered
    out when saving a message by ``save`` or when automatically saving
    to `mbox`.

``saveretain``
:   ``Saveretain`` is to ``save`` what ``retain`` is to
    ``print`` and ``type``. Header fields thus marked are the only
    ones saved with a message when saving by ``save`` or when
    automatically saving to `mbox`. ``Saveretain`` overrides
    ``saveignore``.

``shell``
:   (``sh``) Invokes an interactive version of the shell.

``size``
: Takes a message list and prints out the size in characters of
    each message.

``source``
:   The ``source`` command reads commands from a file.

``top``
: Takes a message list and prints the top few lines of each. The
    number of lines printed is controlled by the variable ``toplines``
    and defaults to five.

``type``
: (``t``) A synonym for ``print``.

``unalias``
:   Takes a list of names defined by ``alias`` commands and discards
    the remembered groups of users. The group names no longer have
    any significance.

``undelete``
:   (``u``) Takes a message list and marks each message as ``not``
    being deleted.

``unread``
:   (``U``) Takes a message list and marks each message as ``not``
    having been read.

``unset``
:   Takes a list of option names and discards their remembered values;
    the inverse of ``set``.

``visual``
:   (``v``) Takes a message list and invokes the display editor on
    each message.

``write``
:   (``w``) Similar to ``save``, except that ``only`` the message
    body (`without`) the header) is saved. Extremely useful for such
    tasks as sending and receiving source program text over the
    message system.

``xit``
: (``x``) A synonym for ``exit``.

``z``
: `Mail` presents message headers in windowfuls as described under
    the ``headers`` command. You can move `mail` attention forward
    to the next window with the ``z`` command. Also, you can move to
    the previous window by using ``z-``.

## Tilde/Escapes

Here is a summary of the tilde escapes, which are used when composing
messages to perform special functions. Tilde escapes are only recognized
at the beginning of lines. The name \`\``tilde escape`'' is somewhat of
a misnomer since the actual escape character can be set by the option
``escape``.

``~!```command`
:   Execute the indicated shell command, then return to the message.

``~a``
: Append the contents of the file `\$HOME/.signature` to the message.

``~b```name...`
:   Add the given names to the list of carbon copy recipients but do not
    make the names visible in the Cc: line ("blind" carbon copy).

``~c```name...`
:   Add the given names to the list of carbon copy recipients.

``~d``
: Read the file \`\``dead.letter`'' from your home directory into
    the message.

``~e``
: Invoke the text editor on the message collected so far. After the
    editing session is finished, you may continue appending text to
    the message.

``~f```messages`
:   Read the named messages into the message being sent. If no messages
    are specified, read in the current message. Message headers
    currently being ignored (by the ``ignore`` or
    ``retain`` command) are not included.

``~F```messages`
:   Identical to ``~f``, except all message headers are included.

``~h``
: Edit the message header fields by typing each one in turn and
    allowing the user to append text to the end or modify the field by
    using the current terminal erase and kill characters.

``~m```messages`
:   Read the named messages into the message being sent, indented by a
    tab or by the value of `indentprefix`. If no messages are specified,
    read the current message. Message headers currently being ignored
    (by the ``ignore`` or ``retain`` command) are not included.

``~M```messages`
:   Identical to ``~m``, except all message headers are included.

``~p``
: Print out the message collected so far, prefaced by the message
    header fields.

``~q``
: Abort the message being sent, copying the message to
    \`\``dead.letter`'' in your home directory if ``save`` is set.

``~r```filename`
:   Read the named file into the message.

``~s```string`
:   Cause the named string to become the current subject field.

``~t```name...`
:   Add the given names to the direct recipient list.

``~v``
: Invoke an alternate editor (defined by the ``VISUAL`` option) on
    the message collected so far. Usually, the alternate editor will be
    a screen editor. After you quit the editor, you may resume appending
    text to the end of your message.

``~w```filename`
:   Write the message onto the named file.

``~|```command`
:   Pipe the message through the command as a filter. If the command
    gives no output or terminates abnormally, retain the original text
    of the message. The command
    [`fmt`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/fmt.html)(1)
    is often used as ``command`` to rejustify the message.

``~:```mail-command`
:   Execute the given mail command. Not all commands, however,
    are allowed.

``~~```string`
:   Insert the string of text in the message prefaced by a single \~. If
    you have changed the escape character, then you should double that
    character in order to send it.

## Mail Options

Options are controlled via ``set`` and ``unset`` commands. Options
may be either binary, in which case it is only significant to see
whether they are set or not; or string, in which case the actual value
is of interest. The binary options include the following:

`append`
:   Causes messages saved in `mbox` to be appended to the end rather
    than prepended. This should always be set (perhaps in
    `/etc/mail.rc`).

`ask`
: Causes `mail` to prompt you for the subject of each message you
    send. If you respond with simply a newline, no subject field will
    be sent.

`askcc`
:   Causes you to be prompted for additional carbon copy recipients at
    the end of each message. Responding with a newline indicates your
    satisfaction with the current list.

`autoinc`
:   Causes new mail to be automatically incorporated when it arrives.
    Setting this is similar to issuing the ``inc`` command at each
    prompt, except that the current message is not reset when new
    mail arrives.

`autoprint`
:   Causes the ``delete`` command to behave like ``dp`` - thus,
    after deleting a message, the next one will be typed automatically.

`debug`
:   Setting the binary option `debug` is the same as specifying `-d`
    on the command line and causes `mail` to output all sorts of
    information useful for debugging `mail`

`dot`
: The binary option `dot` causes `mail` to interpret a period alone
    on a line as the terminator of a message you are sending.

`hold`
: This option is used to hold messages in the system mailbox
    by default.

`ignore`
:   Causes interrupt signals from your terminal to be ignored and echoed
    as @'s.

`ignoreeof`
:   An option related to `dot` is `ignoreeof` which makes `mail`
    refuse to accept a control-d as the end of a message. `Ignoreeof`
    also applies to `mail` command mode.

`metoo`
:   Usually, when a group is expanded that contains the sender, the
    sender is removed from the expansion. Setting this option causes the
    sender to be included in the group.

`noheader`
:   Setting the option `noheader` is the same as giving the `-N` flag
    on the command line.

`nosave`
:   Normally, when you abort a message with two RUBOUT (erase or delete)
    `mail` copies the partial letter to the file \`\``dead.letter`''
    in your home directory. Setting the binary option `nosave`
    prevents this.

`Replyall`
:   Reverses the sense of ``reply`` and ``Reply`` commands.

`quiet`
:   Suppresses the printing of the version when first invoked.

`searchheaders`
:   If this option is set, then a message-list specifier in the form
    \`\`/x:y'' will expand to all messages containing the substring
    \`\`y'' in the header field \`\`x''. The string search is case
    insensitive. If \`\`x'' is ommitted, it will default to the
    \`\`Subject'' header field. The form \`\`/to:y'' is a special case,
    and will expand to all messages containing the substring \`\`y'' in
    the \`\`To'', \`\`Cc'' or \`\`Bcc'' header fields. The check for
    "to" is case sensitive, so that \`\`/To:y'' can be used to limit the
    search for \`\`y'' to just the \`\`To:'' field.

`verbose`
:   Setting the option `verbose` is the same as using the `-v` flag on
    the command line. When mail runs in verbose mode, the actual
    delivery of messages is displayed on the user's terminal.

## Option String Values

``EDITOR``
:   Pathname of the text editor to use in the ``edit`` command and
    ``~e`` escape. If not defined, then a default editor is used.

``LISTER``
:   Pathname of the directory lister to use in the ``folders``
    command. Default is `/bin/ls`.

``PAGER``
:   Pathname of the program to use in the ``more`` command or when
    ``crt`` variable is set. The default paginator
    [`more`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/more.html)(1)
    is used if this option is not defined.

``SHELL``
:   Pathname of the shell to use in the ``!`` command and the ``~!``
    escape. A default shell is used if this option is not defined.

``VISUAL``
:   Pathname of the text editor to use in the ``visual`` command and
    ``~v`` escape.

`crt`
: The valued option `crt` is used as a threshold to determine how long
    a message must be before ``PAGER`` is used to read it. If `crt` is
    set without a value, then the height of the terminal screen stored
    in the system is used to compute the threshold (see
    [`stty`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/stty.html)(1))

`escape`
:   If defined, the first character of this option gives the character
    to use in the place of \~ to denote escapes.

`folder`
:   The name of the directory to use for storing folders of messages. If
    this name begins with a \`/', `mail` considers it to be an
    absolute pathname; otherwise, the folder directory is found relative
    to your home directory.

``MBOX``
: The name of the `mbox` file. It can be the name of a folder. The
    default is \`\``mbox`'' in the user's home directory.

`record`
:   If defined, gives the pathname of the file used to record all
    outgoing mail. If not defined, then outgoing mail is not so saved.

`indentprefix`
:   String used by the \`\`\~m'' tilde escape for indenting messages, in
    place of the normal tab character (\^I). Be sure to quote the value
    if it contains spaces or tabs.

`toplines`
:   If defined, gives the number of lines of a message to be printed out
    with the ``top`` command; normally, the first five lines
    are printed.

# ENVIRONMENT

`Mail` utilizes the ``HOME`` and ``USER`` environment variables.

# FILES

`/var/mail/\`
:   Post office.

\~/mbox
:   User's old mail.

\~/.mailrc
:   File giving initial mail commands. This can be overridden by setting
    the ``MAILRC`` environment variable.

`/tmp/R\`
:   Temporary files.

`/usr/share/misc/Mail.help\`
:   Help files.

`/etc/mail.rc`
:   System initialization file.

# SEE ALSO

[`fmt`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/fmt.html)(1),
[`newaliases`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/newaliases.html)(1),
[`vacation`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/vacation.html)(1),
[`aliases`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man5/aliases.html)(5),
[`mailaddr`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man7/mailaddr.html)(7),
[`sendmail`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man8/sendmail.html)(8)
and
The Mail Reference Manual ..

# HISTORY

A `mail` command appeared in `AT&T UNIX`. This man page is derived
from , The Mail Reference Manualoriginally written by Kurt Shoens.

# BUGS

There are some flags that are not documented here. Most are not useful
to the general user.
Usually, `mail` is just a link to `Mail` which can be confusing.

------------------------------------------------------------------------

  -- -- -------------------
        September 6, 1996
  -- -- -------------------


