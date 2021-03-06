---
# vim: nu et tw=130 ts=8 sts=4 sw=4 ff=unix fo-=l fo+=tcroq2 fdm=marker fmr=@{,@} spell spelllang=en_gb
revision            : none yet
title               :
author              :
language            : en
lang                : en_UK
---

    NAME
      serate - Sudoku Explainer command line rating

    SYNOPSIS
      serate [ --diamond ] [ --format=FORMAT ] [ --input=FILE ] [ --output=FILE ] [ --pearl ] [ puzzle ... ]

    DESCRIPTION
      serate is a Sudoku Explainer command line entry point that rates one or more
      input puzzles. If an --input=FILE option is specified then 81-character puzzle
      strings are read from that file, otherwise if 81-character puzzle operands are
      not specified the puzzles are read from the standard input. If an --output=FILE
      option is specified then the output is written to that file, otherwise output
      is written to the standard output. The output is controlled by the
      --format=FORMAT option.

      Ratings are floating point numbers in the range 0.0 - 20.0, rounded to the
      tenths digit. 0.0 indicates a processing error and 20.0 indicates an valid
      but otherwise unsolvable input puzzle.

    OPTIONS
      -d, --diamond
          Terminate rating if the puzzle is not a diamond.
      -f, --format=FORMAT
          Format the output for each input puzzle according to FORMAT. Format
          conversion are %CHARACTER; all other characters are output unchanged.
          The default format is %r/%p/%d. The format conversions are:
            %d  The diamond rating. This is the highest ER of the methods leading
                to the first candidate elimination.
            %e  The elapsed time to rate the puzzle.
            %g  The puzzle grid in 81-character [0-9] form.
            %n  The input puzzle ordinal, counting from 1.
            %p  The pearl rating. This is the highest ER of the methods leading
                to the first cell placement.
            %r  The puzzle rating. This is the highest ER of the methods leading
                to the puzzle solution.
            %%  The % character.
      -h, --html
          List detailed info in html.
      -i, --input=FILE
          Read 81-character puzzle strings, one per line, from FILE. By default
          operands are treated as 81-character puzzle strings. If no operands are
          specified then the standard input is read.
      -m, --man
          List detailed info in displayed man page form.
      -o, --output=FILE
          Write output to FILE instead of the standard output.
      -p, --pearl
          Terminate rating if the puzzle is not a pearl.
      -V, --version
          Print the Sudoku Explainer (serate) version and exit.

    INVOCATION
      java -Xrs -Xmx500m -cp SudokuExplainer.jar diuf.sudoku.test.serate ...

    SEE ALSO
      SudokuExplainer(1), sudoku(1)

    IMPLEMENTATION
      version     serate 1.2.1.3 (Sudoku Explainer) 2009-01-01
      author      Nicolas Juillerat
      copyright   Copyright (c) 2006-2009 Nicolas Juillerat
      license     Lesser General Public License (LGPL)
