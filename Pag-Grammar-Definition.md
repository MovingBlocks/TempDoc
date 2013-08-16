*This is a work in Progress*

You read that right, this is a grammar for our grammar. That is, this defines the format for the grammars one can use for procedural generation.

PAG specification
=================

	PAG := Header 'grammar' Identifier ':' Section+

Header
------
The _PAG-Header_ will store information for the grammar system, such as which type of structure is created by this grammar, and provide the possibility to assign constants you can later use in the grammar rules. 

	Header := Declaration*

	Declaration := '#'? Identifier ':=' expr ';'

A header declaration that starts with a ``#`` will be interpreted as grammar info field, such as building type, or fitting biomes. You can define module dependencies for the grammar here as well:

        #dependencies := ["myModule", "otherAwesomeModule"];

You may have noticed that different forms of _expressions_ are allowed on the right side, we will come to that later.

Sections
--------
Section make up the actual grammar. Each section can define a priority for a rule.

	Section := Priority Section | '{' Rule+ '}' | Rule+

	Priority := 'Priority' decimalLiteral ':'

	Rule := Predecessor (':' expression)? '->' Successor (':' expression)? ('|' Successor (':' expression)?)+

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

	primary := '(' expression ')' | literal | Identifier | ScopeExpression | ShapeExpression | methodCall

	ScopeExpression := 'Scope' '.' ( Direction | 's' | 'p' | Occlusion)	// what do s and p stand for?

	Occlusion := 'occ' '(' Identifier ')' ('==' | '!=') ('none' | 'part' | 'full')

	ShapeExpression :=  'Shape' '.' 'visible' '(' Identifier ')'

	methodCall := randomSelection

	randomSelection := 'Random' '(' (qualifiedIdentifierList | rangeDefinition) ')'

	qualifiedIdentifierList := qualifiedIdentifier (',' qualifiedIdentifier)*

	rangeDefinition := expression '..' expression	
		 

Base Rules
----------
The following basic rules are supported by the grammar.  

	BaseRule := SetRule | DivideRule | SplitRule | RepeatRule | Invoke | TransformationRule

	SetRule := 'set' '(' '"' qualifiedIdentifier '"' ')'

	DivideRule := 'divide' Direction '{' ('[' Size ']' Successor)+  '}'

	SplitRule := 'split' '{' ('[' SplitType ']' Successor)+ '}'

	RepeatRule := 'repeat' Direction '['expression']' Successor

The invocation of other grammars is just a proposal for allowing the reuse of code. It may be erased from the specification if
it proves not to be practical. 

	Invoke := 'invoke' '(' qualifiedIdentifier ')'

Basic transformation of shapes is supported by the following rules.

	TransformationRule := ScaleRule | TranslateRule | RotateRule

	ScaleRule := 'S' '(' numericLiteral (',' numericLiteral ',' numericLiteral)? ')'

	TranslateRule := 'T' '(' numericLiteral ',' numericLiteral ',' numericLiteral ')'

	RotateRule := ('Rx' | 'Ry' | 'Rz') '(' numericLiteral ')'

Moreover, we need special rules for the roof construction:

	Roof := 'Roof' '(' roofType ',' expression ')' '{' successor '}'

	roofType := 'hipped' | ...

----------
The following attributes are used in the base rules.

	Direction := 'X' | 'x' | 'Y' | 'y' | 'Z' | 'z'

	Size := decimalLiteral ('%')? | floatingPointLiteral

	SplitType := 'faces' | 'sidefaces' | 'edges' | 'vertices' | 'walls' | 'floor'

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


Examples
========

The following code is an example of a PAG-grammar. It is closely related to a example provided by Müller, Wonka et al.

	type := "building"
	kind := "house"
	style := "medieval"

	stone := Random( engine:stone, engine:cobblestone )
	planks := "engine:plank"

	building_height := Random( 3 .. 5)
	door_width := 1
	door_height := 2
	door_depth := 1
	window_spacing := 3
	window_width := 1
	window_height := 1
	window_depth := 1
	wall_depth := 1

	roof_type := hipped
	roof_angle := 40

	grammar House

		priority 1: 
			footprint -> { 
				S(100%, building_height, 100%) facades 
				T(0, height, 0) Roof(roof_type, roof_angle){roof} 
			}		

		priority 2: 
			facades -> split {
				[walls] facade
			}

			facade : Shape.visible(Street) 
				-> divide x {
						[100%] tiles
						[door_width * 1.5] entrance
					} : 0.5
				| divide x {
						[door_width * 1.5] entrance
						[100%] tiles
					}
			facade -> tiles

			tiles -> repeat x [window_spacing] tile

			tile -> divide x {
						[50%] wall
						[window_width] subdiv y {
							[2/3] wall
							[window_height] window
							[1/3] wall
						}
						[50%] wall
					}

			window : Scope.occ(noparent) != none -> wall

			window -> S(100%, 100%, window_depth) set(engine:glass)

			entrance -> divide x {
							[50%] wall
							[door_width] divide y {
								[door_height] door
								[100%] wall
							}
							[50%] wall
						}

			door -> S(100%, 100%, door_depth) set(engine:door)

			wall -> S(100%, 100%, wall_depth) set(stone)

		priority 3:

			roof -> split {
					[sidefaces] set(roofMod:redShingle)
				}
