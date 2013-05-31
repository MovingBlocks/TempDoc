*This is a work in Progress*

You read that right, this is a grammar for our grammar. That is, this defines the format for the grammars one can use for procedural generation.

PAG specification
=================

	PAG := Header? 'grammar' Identifier Section+

Header
------
The _PAG-Header_ will store information for the grammar system, such as which type of structure is created by this grammar, and provide
the possibility to assign variables for later use in the grammar.

	Header := Statement*

	Statement := Identifier ':=' expression

Sections
--------
Section make up the actual grammar. Each section can define a priority for a rule.

	Section := Priority Section | '{' Section '}' | Rule

	Priority := 'Priority' decimalLiteral ':'

	Rule := Predecessor (':' expression)? '->' Successor (':' expression)?

	Predecessor := Identifier ('(' Parameter ')')?

	Parameter := literal | Identifier

	Successor := Predecessor | BaseRule | '{' (Predecessor | BaseRule)+ '}'

Expressions
-----------
Basic logic and arithmetic expressions supported by the grammar.

	expression
		:= primary
		 | '!' expression
		 | expression ('*' | '/' | '%') expression
		 | expression ('+' | '-') expression
		 | expression ('<' '=' | '>' '=' | '<' | '>') expression
		 | expression ('==' | '!=') expression
		 | expression '&&' expression
		 | expression '||' expression

	primary := '(' expression ')' | literal | Identifier | ScopeExpression

	ScopeExpression := 'Scope' '.' ( Direction | 's' | 'p' | Occlusion)	// what do s and p stand for?

	Occlusion 
		:= 'occ' '(' Identifier ')' ('==' | '!=') ('none' | 'part' | 'full')
		 | 'visible' '(' Identifier ')'

Base Rules
----------
The following basic rules are supported by the grammar.  

	BaseRule := SetRule | DivideRule | SplitRule | RepeatRule | Invoke | TransformationRule

	SetRule := 'set' '(' qualifiedIdentifier ')'

	DivideRule := 'divide' Direction '{' ('[' Size ']' Successor)+  '}'

	SplitRule := 'split' '{' ('[' SplitType ']' Successor)+ '}'

	RepeatRule := 'repeat' Direction Successor

The invocation of other grammars is just a proposal for allowing the reuse of code. It may be erased from the specification if
it proves not to be practical. 

	Invoke := 'invoke' '(' qualifiedIdentifier ')'

Basic transformation of shapes is supported by the following rules.

	TransformationRule := ScaleRule | TranslateRule | RotateRule

	ScaleRule := 'S' '(' numericLiteral (',' numericLiteral ',' numericLiteral)? ')'

	TranslateRule := 'T' '(' numericLiteral ',' numericLiteral ',' numericLiteral ')'

	RotateRule := ('Rx' | 'Ry' | 'Rz') '(' numericLiteral ')'

----------
The following attributes are used in the base rules.

	Direction := 'X' | 'x' | 'Y' | 'y' | 'Z' | 'z'

	Size := decimalLiteral ('%')? | floatingPointLiteral

	SplitType := 'faces' | 'edges' | 'vertices' | 'walls' | 'floor'

Literals
--------

	literal := numericLiteral | booleanLiteral

	booleanLiteral := 'true' | 'false'

	numericLiteral := decimalLiteral | floatingPointLiteral

	decimalLiteral := '0' | '1'..'9' Digit*

	floatingPointLiteral := Digits '.' Digits? | '.' Digits | Digits 'f'

	Digits := Digit*

	Digit := '0'..'9'


Identifiers
-----------
Identifiers (such as predecessor and variable names) have to start with a letter, followed by any sequence of alphnumerical characters.
Qualified Identifiers will be used to specify assets (such as blocks or other grammar files).
	
	Identifier := Letter (Letter | Digit)*

	Letter := 'a'..'z' | 'A'..'Z' | '_'

	qualifiedIdentifier := Identifier (':' Identifier)*	

Comments, Whitespaces, ...
--------------------------
Comments, whitespaces and such are skipped during parsing and have no influence on the actual grammar functionality.
The rules are denoted using a syntax similar to ANTLR.

	COMMENT := '/*' (.*)? '*/' -> channel(HIDDEN)

	LINE_COMMENT := '//' ~[\r\n]* -> channel(HIDDEN)

	WS := ( '\r' | '\t' | ' ' | '\n' )+ -> channel(HIDDEN)


I use the regular expression notation for _+_ (1 or more), _?_ (at most 1), brackets for characters ranges, _*_ (for 0 or
more), _\\_ for escaping, _' '_ for literals and parenthesis for grouping. Furthermore, _._ is a wildcard character and
_~_ denotes "everything until ...".
