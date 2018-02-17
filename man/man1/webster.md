# NAME

webster - look up words in the dictionary

# SYNOPSIS

`webster` \[-`d`\] \[-`s`\] \[`words`\]

# DESCRIPTION

`Webster` is used to look up words in the online copy of Webster's 7th
Collegiate dictionary. If words are given as arguments to the program,
they will be looked up and their definitions printed. If no arguments
are given, `webster` enters interactive mode, and prompts for words to
be defined.

In interactive mode, you will be prompted with \`\`Word: ''. Just type
the word you want defined, or simply type a blank line to exit. If the
word is found, `webster` will then provide the complete dictionary
entry for the word including definitions, pronunciation, and derivation.
If the specified word was not found, `webster` will try to find close
matches, as if you spelled the word wrong. The possibilities are
numbered and typed out. To select one of them, you can just give its
number.

By preceding a word with \`\`!'', the spelling of the word can be
checked instead of its definition. `webster` will check the spelling
of the word, and will indicate whether it is spelled correctly or not.
If the word is misspelled, `webster` will try to provide a list of
alternate spellings.

Additionally, `webster` can match words using wildcards. The character
\`%' in a word means match exactly one character, so \`\`w%n'' matches
\`\`win'', \`\`won'', \`\`wan'', etc. The character \`\`' matches `zero
or more` characters, so \`\`a\`d''matches \`\`ad'', \`\`and'',
\`\`abound'', \`\`absentminded'', and so on. Any number of wildcards can
be used, and in any arrangement.

The ESC (escape) and \`?' characters also perform special functions.
Typing a partial word, followed by ESC, tries to complete what you have
typed so far. If what you have typed is a unique abbreviation for a
word, the word is typed out. If what you typed is ambiguous, `webster`
will beep at you and do nothing. Typing \`?' at the end of a partial
word will print out all the possible endings for the word you typed. If
there are no possible endings, `webster` will beep at you and do
nothing.

# EXAMPLES

    Word: plur?
    Maybe you mean:
    1. plural   2. pluralism    3. plurality    4. pluralization
    5. pluralize    6. pluri-   7. pluriaxial
    Word: pluri?
    Maybe you mean:
           1. pluri-   2. pluriaxial

Word: `pluria&lt;ESC&gt;`xial
Where the text in italics is typed by the user, and the rest by
`webster`. Note that wildcards may be used in conjunction with ESC and
\`?', for example

    Word: plu`x<ESC>
    Word: pluriaxial

# OPTIONS

The `-d` and `-s` options may be used to put `webster` into
`define` or `spell` mode, respectively. These modes indicate what
`webster` does with words (define them or check their spellings). The
inverse mode is available using the \`\`!'' as described above.

# SEE ALSO

[`look`](/web/20141128030253/http://www2.research.att.com/~astopen/man/man1/look.html)(1),
[`spell`](/web/20141128030253/http://www2.research.att.com/~astopen/man/man1/spell.html)(1),
[`websterd`](/web/20141128030253/http://www2.research.att.com/~astopen/man/man8/websterd.html)(8)

# BUGS

The translation between all the neat special characters in the
dictionary such as upside-down e's, cedillas, accent marks, etc. and a
simple ASCII terminal is marginal at best. Most of the characters are
fairly well faked, but a few of them are impossible. In particular, the
schwa (upside-down e) is represented by an asterisk.

Occasionally, when you type a word to the prompt, another prompt appears
without the word being defined. If this happens, try typing the word
again. If it still doesn't work, exit the program and start again.

# COPYRIGHT

Webster's 7th Collegiate Dictionary, Copyright (C) 1963 by
Merriam-Webster, Inc. No part of this information may be copied or
reprinted without the express written consent of the publisher.

# AUTHOR

David A. Curry\
davy@intrepid.ecn.purdue.edu

------------------------------------------------------------------------

  ----- ------------ ----------------
  ECN   1 May 1986   March 11, 2008
  ----- ------------ ----------------


