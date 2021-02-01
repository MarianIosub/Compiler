# Compiler

Here you have a Lex/Yacc Compiler for a personal programming language made for a project for Faculty.
To run the project you need to run the followings in the terminal:

  yacc -d limbaj.y
  lex limbaj.l
  gcc x.yy.c y.tab.c -o ex
  .ex limbaj.txt

The project contains :

  Parser and semantic analyser for declarations.
  Parser and semantic analyser for structures.
  Parser and semantic analyser for functions.
  Parser and semantic analyser for main block.
  Parser and semantic analyser for a predefined function called "Eval" which calculates and prints the value of a integer expression.

The project can:

  Return values.
  Print variables.
  Calculate numerical expressions.
  
Hope you will enjoy it.

