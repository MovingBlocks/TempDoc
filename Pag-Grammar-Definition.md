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

A header declaration that starts with a ``#`` will be interpreted as _grammar info_ field, such as building type, or fitting biomes. You can define module dependencies for the grammar here as well:

        #dependencies := ["myModule", "otherAwesomeModule"];

You may have noticed that different forms of _expressions_ are allowed on the right side, we will come to that later. Simple constants can be defined in a similar way:
        floor_height := 3;

Sections
--------
Sections make up the grammar and group the grammar rules with the same _priority_. The priority is used to control the order in which derivations are selected. Of course it is possible to have just one section for all rules.

	Section := 'Priority' decimalLiteral ':' ruleStatement+

Each ``ruleStatement`` is of  the form ``predecessor -> successor``. Note that every rule has to be ended by a semicolon. Furthermore, you can specify _guards_ (boolean expressions that guard whether the rule can be applied or not) and _probabilities_. Guards and probabilities are optional for every rule. 

	ruleStatement := Predecessor (':' expression)? '->' Successor (':' expression)? ('|' Successor (':' expression)?)+ ';'

	Predecessor := Identifier

The _successor_ can either be an identifier, which denotes another rule, a _base rule_ or a sequence of the former enclosed in braces.

	Successor := Identifier | Baserule | '{' (Identifier | BaseRule)* '}'

Expressions
-----------
The following set of expressions are supported by the grammar system. You can use standard Boolean and arithmetic operations, numbers (integer and decimal), identifiers and strings and lists of expressions. Furthermore, there are a few special operations/method calls. 

	expression := primary
			| functionCall
			| ('Shape' | 'Scope') '.' ('occ' | 'visible') '(' expression ')'
			| '[' expression ']'
			| ('+' | '-') expression
			| '!' expression
			| expression ('*' | '/' | '%') expression
			| expression ('+' | '-') expression
			| expression ('<=' | '>=' | '<' | '>') expression
			| expression ('==' | '!=') expression
			| expression '&&' expression
			| expression '||' expression

	primary := '(' expression ')'  | literal 'r'? | Identifier

The only _function call_ currently available is the random selection from either a list or a defined range.

        functionCall := randomSelection

        randomSelection := 'Random' '(' (exprList | rangeExpr) ')'

An expression list is simply a sequence of expressions:

        exprList := expression (',' expression)*

You can define a range of integers with the following notation:

        rangeExpr := expression '..' expression

E.g. you can select a random block type from a list or define a scale or measure of length randomly within a range from .. to.

        wall_mat := Random("cobblestone", "stonebricks", "stone");
        number_floors := Random(2..5);

The _occlusion_ and _visibility checks_ are useful as guards. They can be used to determine whether the current scope is occluded by any other shape or scope or if a specific shape is visible from the current scope. This can be used to place doors on walls that face to the street. Note that the occlusion test for scopes is faster but less accurate than the test against shapes.

		wall : Shape.visible("street") -> door_wall;
		wall : Scope.occ("nonparent") == "none" -> win_wall;

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

	#type := house;

	window_spacing  := 4;
	window_width    := 2;
	window_depth    := .5;
	window_height   := 1;
	door_height     := 2;
	door_width      := 2;
	roof_angle      := 45;

	grammar TestHouse:

	Priority 1:
		footprint -> {
			S(1r, building_height, 1r) facades
			T(0, building_height, 0) I("prism") roof
		};

		Priority 2:
			facades -> Split {
				["sidefaces"] facade
			};

			facade : Shape.visible("street") 
				-> Divide "X" {
					[1r] tiles
					[door_width * 1.5] entrance
				} : 0.5
				-> Divide "X" {
					[door_width * 1.5] entrance
					[1r] tiles          
				} : 0.5
				;
			facade -> tiles;

			tiles -> Repeat "X" [window_spacing] tile;

			tile -> Divide "X" {
				[1r] wall
				[window_width] Divide "Y" {
						[window_height] window
						[1r] wall
					}
				[1r] wall
			};

			window : Scope.occ("noparent") != "none" -> wall;
			window -> {
				S(1r, 1r, window_depth) Set("enginge.glass")
			};

			entrance -> Divide "X" {
				[1r] wall
				[door_width] Divide "Y" {
						[door_height] door
						[1r] wall
					}
				[1r] wall
			};

			door -> Set("core.door");

			wall -> Set(Random("cobblestone", "stonebricks"));

		Priority 3:
			roof -> Split {
				["sidefaces"] covering
				["sideedges"] roofedge
				["topedge"] roofedge
			};

			covering -> Set("brick" : "stair");

			roofedge -> Set("stone");
			