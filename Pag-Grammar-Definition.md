*This is a work in Progress*

You read that right, this is a grammar for our grammar. That is, this defines the format for the grammars one can use for procedural generation.

**PAG** :=  SECTION<sup>+</sup>

**SECTION** := COMMENT NEWLINE SECTION | PRIORITY NEWLINE SECTION | RULE

**COMMENT** := ##[^NEWLINE]<sup>+</sup>

**PRIORITY** := Priority NUMBER:

**RULE** := (PREDECESSOR : CONDITIONAL -> SUCCESSOR : PROBABILITY)

**PREDECESSOR** := ALPHANUMERIC<sup>+</sup>(LPAREN PARAM(,PARAM)<sup>*</sup> RPAREN)?

**CONDITIONAL** := CONDVAR OP CONDVAR | OCCLUSION | !LPAREN CONDITIONAL RPAREN | CONDITIONAL && CONDITIONAL | CONDITIONAL \|\| CONDITIONAL

**CONDVAR** := PROBVAR | VARARITHMETIC

**SCOPEVAR** := Scope\\.(X | Y | Z | S | P)

**OCCLUSION** := (Shape.occ LPAREN "LETTER<sup>+</sup> " RPAREN (== | !=) ("none" | "part" | "full")) | (Shape.visible LPAREN "LETTER<sup>+</sup> " RPAREN)

**OP** := == | != | > | >= | < | <=


**PROBABILITY** := FLOAT | VARARITHMETIC

**VARARITHMETIC** := PROBVAR ARITHMETIC PROBVAR | LPAREN VARARITHMETIC RPAREN ARITHMETIC LPAREN VARARITHMETIC RPAREN

**PROBVAR** := SCOPEVAR | NUMBER | PARAM | FLOAT

**ARITHMETIC** := \\+ | - | \\* | \\\\

**SUCCESSOR** := PREDECESSOR | BASERULE

**BASERULE** := *TODO*

**PARAM** := LETTER

**ALPHANUMERIC** := LETTER | NUMBER

**NUMBER** := [0-9]

**LETTER** := [A-Za-z]

**LPAREN** := \\ (

**RPAREN** := \\ )

**FLOAT** := NUMBER<sup>*</sup>\\.NUMBER<sup>+</sup>

**NEWLINE** := \\n *(maybe use \\s instead?)*

I use the regular expression notation for + (1 or more), ? (at most 1), brackets for characters, * (for 0 or more), backslash for escaping, and parenthesis for grouping.
