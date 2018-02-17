---
# vim: nu et tw=130 ts=8 sts=4 sw=4 ff=unix fo-=l fo+=tcroq2 fdm=marker fmr=@{,@} spell spelllang=en_gb
revision            : none yet
title               :
author              :
language            : en
lang                : en_UK
---

    NAME
      pseudocoup - (3`3)x(3`3) sudoku solver

    SYNOPSIS
      pseudocoup [ options ] [ puzzle ... | < puzzle.file ... ]

    DESCRIPTION
      pseudocoup solves (3`3)x(3`3) sudoku puzzles defined by the literal puzzle
      operands or puzzles read from the standard input if there are no puzzle
      operands, and solves each puzzle. A solvable puzzle has exactly one solution.
      The solver stops on the first solution for each puzzle.

    OPTIONS
      There are a few compile time options that may degrade performance. Other
      compile time options control puzzle order (4..64) and QWH (quasigroup
      with holes or latin square) vs. sudoku. See the source for details.

    DETAILS
      pseudocoup is coded for solving speed. It uses only two simple constraints:
        F  Forced cell: only one value possible.
        N  Only cell: only one value in row/col/box.
      When the constraints fail to make progress a guess is made and the solver
      backtracks. Guesses are made on solution cells that minimize the maximum
      number of holes for all candidate values for the cell using a 1 level
      forward check. Ties go to the cell with the least number of candidate
      value constraints.

    INPUT FORMAT
      Puzzle input is a sequence of (3`3)x(3`3) characters that fill the grid from left
      to right, top to bottom. Space separated numbers are clue values,
      #...newline, //...newline, "...", [...], and <...> are comments, {...}
      or digit strings separated by space are candidate values (hints), and
      all other characters not matching [[:space:]|`+-] are treated as an
      empty grid space. Invalid puzzles produce a diagnostic. Each puzzle
      description may be followed by 0 or more [R,C]=V or [R,C]={ABC} operations
      that set the cell value at row R column C to V or the candidate values to.
      'ABC' .

    OUTPUT FORMAT
      A comment line containing the puzzle ordinal, and puzzle line if different
      from the ordinal, is printed for each puzzle, followed by the solution
      in grid form.

    PERFORMANCE
      Solution speed on a collection of posted and generated puzzles is
      ~7000 puzzles/second/Ghz. Minimal puzzle generation speed is
      ~10 puzzles/second/Ghz.

    SEE ALSO
      sudoku(1), sudocoo(1)

    IMPLEMENTATION
      version     pseudocoup (3`3)x(3`3) (AT&T; Research) 2007-10-11
      author      Glenn Fowler
      copyright   Copyright (c) 2005-2007 AT&T; Knowledge Ventures
      license     http://www.opensource.org/licenses/cpl1.0.txt
