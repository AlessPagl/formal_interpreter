#INP

A simple Language Interpreter of the IMP Language, written in Haskell, for Didactic purposes. 

This work is part of the *"Formal Methods in Computer Science"* exam at *University of Bari "Aldo Moro".*

## Features
INP is an interpreter (with a parser) of an IMP language composed of the following constructs:
- **skip** performs a jump to the next instruction;
- **assignment** assigns a value to a variable by calculating it if it is written in the form of an expression;
- **If-then-else** conditional control structure;
- **Do-while** iterative control structure of the do-while type;
- **While-do** iterative control structure of the while-do type;
- **For-times** iterative control structure of the for type;

*INP* uses dynamic typization, accepts integer and Boolean data.

## Grammar
```EBNF
program ::= <command> | <command> <program>
 
command ::= <skipcommand> | <assignmentcommand> | <ifcommand> | <whilecommand> | <dowhilecommand> | <forcommand>

skipcommand ::= skip <semicolon> 

assignmentcommand ::= <variable> := (<aexp> | <bexp>) <semicolon> | <letter> := { <array> } <semicolon> 

ifcommand ::= if <space> ( <bexp> ) <space> then { <space> (<program> | <program> else { <space> <program>) } <semicolon>

whilecommand ::= while <space> ( <bexp> ) <space> { <space> do <space> <program> <space> } <semicolon>

dowhilecommand ::= do <space> { <space> do <space> <program> <space> } while <space> ( <bexp> ) <space> <semicolon>

forcommand ::= for <space> <variable> <space> times <space> { <space> <program> <space> }
 
array ::= <afactor> | <afactor> <colon> <array>
 
bexp ::= <bterm> | <bterm> <bexpOp> <bexp>
 
bterm ::= <bfactor> | ( <bexp> ) | ! <bexp>
 
bfactor ::= <aexp> | <aexp> <comparisonOp> <aexp> | <variable>
 
aexpr ::= <aterm> | <aterm> <aexpOp1> <aexp>
 
aterm ::= <afactor> | <afactor> <aexpOp2> <aterm>

afactor ::= <apositivefactor> | <anegativefactor> 

anegativefactor ::= - | <apositivefactor> 

apositivefactor ::= <number> | ( <aexp> ) 

number ::= <positivenumber> | <variable> 

positivenumber ::= <digit> | <digit> <positivenumber> 

variable ::= <letter> | <letter> <variabile> |

semicolon ::= ; | ; <space> 

colon ::= , | , <space> 

digit ::= 0-9 

aexpOp1 ::= + | -

aexpOp2 ::= * | / 

bexpOp ::= & | | 

comparisonOp ::= < | > | = | <= | >= | != 

letter ::= a-z 

space ::= " "

```
## How to compile and start

In a Linux-like system, first install Haskell GHC and then
```sh
$ ghci
GHCi, version 8.8.4: https://www.haskell.org/ghc/  :? for help
Prelude> :load "PATH in which is file INP.hs"
[1 of 1] Compiling Main             ( "PATH in which is file INP.hs", interpreted )
Ok, one module loaded.
*Main> inp

-+-+-+-+-+- INP Language Interpreter -+-+-+-+-+-
         developed by Alessio Pagliarulo

Type ":help" for commands

INP#> TYPE HERE THE CODE TO PARSE AND INTERPRET

```

## Examples of use

**Variable assignment** and **Do-while** with nested **if-then-else**.
```sh
INP#>x:=20;
INP#>do { x:=x+1; if (x<30) { y:=x+1; }; }while (x<40) ;
INP#>:printmem

-+-+ Parsed Code +-+-
x:=20;do { x:=x+1; if (x<30) { y:=x+1; }; }while (x<40) ;

-+-+ Memory +-+-
x=>40 y=>30 
```

**Array assignment**.
```sh
INP#>a:={10,20,30,777};
INP#>:printmem

-+-+ Parsed Code +-+-
a:={10,20,30,777};

-+-+ Memory +-+-
a[0]=>10 a[1]=>20 a[2]=>30 a[3]=>777 
```
More stuff with **arrays**:
```sh
INP#>index:=0;
INP#>value:=100;
INP#>accumulator:=v[0]+v[1]+v[2];
INP#>:printmem

-+-+ Parsed Code +-+-
v:={1,2,3};index:=0;value:=100;accumulator:=v[0]+v[1]+v[2];

-+-+ Memory +-+-
v[0]=>1 v[1]=>2 v[2]=>3 index=>0 value=>100 accumulator=>6 
```

Use of the **While-do loop**.
```sh
INP#>x:=0;
INP#>while (x<10) { do x:=x+1; };
INP#>:printmem

-+-+ Parsed Code +-+-
x:=0;while (x<10) { do x:=x+1; };

-+-+ Memory +-+-
x=>10 
```

Use of the **For-times loop**.
```sh
INP#>x:=5;
INP#>y:=0;
INP#>for x times { y:=y+1; };
INP#>:printmem

-+-+ Parsed Code +-+-
x:=5;y:=0;for x times { y:=y+1; };

-+-+ Memory +-+-
x=>0 y=>5 
```
