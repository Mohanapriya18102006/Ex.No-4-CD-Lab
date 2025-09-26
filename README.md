# Ex.No:4
# RECOGNITION OF A VALID VARIABLE WHICH STARTS WITH A LETTER FOLLOWED BY ANY NUMBER OF LETTERS OR DIGITS USING YACC
## Register Number:212224220065
## Date:26-09-2025
## Aim:
To write a YACC program to recognize a valid variable which starts with a letter followed by any number of letters or digits.
## ALGORITHM
1.	Start the program.
2.	Write a program in the vi editor and save it with .l extension.
3.	In the lex program, write the translation rules for the keywords int, float and double and for the identifier.
4.	Write a program in the vi editor and save it with .y extension.
5.	Compile the lex program with lex compiler to produce output file as lex.yy.c. eg $ lex filename.l
6.	Compile the yacc program with YACC compiler to produce output file as y.tab.c. eg $ yacc –d arith_id.y
7.	Compile these with the C compiler as gcc lex.yy.c y.tab.c
8.	Enter a statement as input and the valid variables are identified as output.
## PROGRAM
l file
```
%{
#include "expr4.tab.h"
%}

%%

[a-zA-Z][a-zA-Z0-9]*    { return VARIABLE; }
.|\n                    { return INVALID; }

%%
int yywrap() {
    return 1;
}

```
y ifle
```
%{
#include <stdio.h>
#include <stdlib.h>

int count = 0;  // count of 'a's
int yylex(void);
void yyerror(const char *s);
%}

%token A B INVALID

%%

input:
    A_seq B '\n' {
        if (count >= 10) {
            printf("Valid string: a^n b where n >= 10\n");
        } else {
            printf("Invalid: less than 10 'a's before 'b'\n");
        }
        count = 0; // reset for next input
    }
  | INVALID '\n' {
        printf("Invalid character in input.\n");
        count = 0;
    }
  ;

A_seq:
    A           { count = 1; }
  | A_seq A     { count++; }
  ;

%%

int main() {
    printf("Enter strings (e.g., aaa...ab), one per line (Ctrl+D to quit):\n");
    while (yyparse() == 0);
    return 0;
}

void yyerror(const char *s) {
    // Errors handled in grammar
}

```
## Output

<img width="563" height="326" alt="Screenshot 2025-09-26 110608" src="https://github.com/user-attachments/assets/afbeb0d7-e6c8-488c-b2eb-c55aab122b30" />


## Result
A YACC program to recognize a valid variable which starts with a letter followed by any number of letters or digits is executed successfully and the output is verified.
