# Versions
* v0.5    Set & Divide rule
* v0.6    Component Split (Split rule)
* v0.65   Nested successors

***

* v0.7    Guards/Conditions
* v0.8    Repeat rule
* v0.9    Occlusion Queries
* v1.0    arbitrary footprints/scopes of multiple shapes
* v1.1    Snapping
* v1.2    Generic rules
* v1.3    User defined attributes
* v1.4    more primitve forms (cylinder,sphere,...)

# Introduction
The Procedural Architecture Grammar (PAG) is a grammar based system for generating buildings and other architecture related stuff. The building's general appeareance will be defined via a grammar file (*.pag), containing production rules for the automated generation process.

The principles of operation are scopes and shapes. Scopes restrict shapes along the three axis and contain a shape. The derivation process starts with a rough bounding box for the building as scope. This bounding box is dependent on the parcel the buidling is going to be placed in (namely width x height x depth).

Each production rule describes a modification of the current scope. For further information hava a look at the documentation section below.

# Documentation

PAG is inspired by/based on the paper [Procedural Modeling of Buildings](http://peterwonka.net/Publications/mueller.procedural%20modeling%20of%20buildings.SG2006.final-web.pdf) by Pascal Müller and Peter Wonka. 

For the exact PAG Definition, go to [[PAG Grammar Definition]].

## 1. Production rules

Production rules in general are defined in the following form:

        predecessor : condition ::- successor : probability;

where \<predecessor\> is a symbol identifying a non terminal shape that is to be replaced with \<successor\> (a symbol of the grammar, either a terminal or a non terminal shape symbol). \<condition\> is a guard that has to evaluate to true in order for the rule to be applied. The specific rule is selected with \<probability\>.

Please note that \<condition\> and \<probability\> are optional for each rule. So in case you don't need a condition or a probability (by default the rules' probabilities are calculated as \<probability\>=1/\<number of alternatives\>) you can simply write rules like that:

        predecessor ::- successor;

As already mentioned you can define alternatives for each rule in the following form:

        predecessor : condition ::- alt_1 : prob_1 | alt_2 : prob_1;

Keep in mind that alternatives defined in this way all depend on the same \<condition\>. To use different condition statements for different alternatives you have to specifiy the rule like follows:

        predecessor : cond_1 ::- alt_1;
        predecessor : cond_2 ::- alt_2;

### 1.1 Set rule

The Set rule sets all block in the current scope to the specified block type. A block type is identified by its \<AssetURI\>, which is build up as following:

        "<packageName>:<assetName>"

The set rule is a rule of the following form:

        predecessor : condition ::- Set(<AssetURI>) : probabilities;

Furthermore, the set rule can be used in nested successors (see example for split rule).

### 1.2 Divide rule

The divide rule divides the current scope along one or more axis. The direction is given directly with the divide command, whereas the subshape's sizes are specified within the divide command.

The size of a subshape can either be relative or absolute. Absolute sizes have to be integer values. They specifiy the actual size in total blocks.
Relative sizes are specified in percentage of the remaining size (of the current scope, after subtracting the absolute values from the dimension along the divide direction).

The basic form of a divide rule is as follows:

        divide <direction> {
            [<size1>]   successor1
            [<size2>]   successor2
        }

A typical divide rule may look like the following:

        house : height >= 6 ::- divide y {
                                   [3] ground_floor
                                   [3] roof
                                };

### 1.3 Split rule

The split rule creates new subshapes by the specified split type. Possible split types are "walls", "corner" (might be expanded in the future).
Within the split, shape symbols or other (nested) successors can be applied on the newly created shapes.

The basic form of a split rule is as follows, where multiple split types can be defined in one split rule:

        split {
            [split_type]    successor
        }

The following rule split the scope of floor and sets the walls to cobblestone blocks.

        floor ::- split {
                      [walls]  Set("engine:CobbleStone")
                  };

### 1.4 Repeat rule

The repeat rule repeats the specified pattern along a given direction as often as the specified subshape(s) fit into the current scope.
This rule is useful in cases of filling up space with repeating patterns, such as the building's height with floors, the facade's width with wall elements and so on.

Please note that the repeat arguments need to have a fixed and absolute size. Moreover, if the last repeat element does not fit into the current scope it is left out.

The basic form of a repeat rule is as follows:

        repeat <direction> {
            successor
        }

The repeat rule may get some further functionality in the future, such as
* alternive successor for the "last" element (best relative, to scale it right)
* direction of creation may be specified (last element to the right, left or in the middle)

## 2. Guards and Conditions

With guards and conditions one can define if a rule is applyable to a given symbol. For example, you can give the ground floor another appearance then the other floors, or you can apply different derivations depending on the scopes height/widht/depth.
Furthermore, occlusion checks can be used as guards, so that a rule is only applied if the symbols scope is not occluded by other shapes (for more complex footprints you do not want to have walls inside the building). Another type of guard will be sightlines, with which you can check if a street is "visible" from the current shape. That allows one to place doors on the correct places.

Conditions are normal boolean expressions, such as numerical relations (==, !=, >, >=, <, <=), occlusion and sightline checks.
Several expressions can be combined by logical operators (&& - and, || - or), and single expressions can be negated using "!".

### 2.1 Occlusion Queries

The Occlusion Queries are a special form of a boolean expression. With such a query you can test if the current scope is occluded by other shapes.
Possible occlusion types are "full", "part" and "none". The user may get the best results if the Occlusion Query is applied on small shapes rather then on whole components (it is likely that a sidewall is occluded partly by another shape, but if you test against smaller wall elements you will get a "higher resolution" of where you can place windows/doors and where not).

An important restriction is the "noparent" attribute. If you think about the scope/shape structures build up by the grammar, every child in the derivation process is occluded by its parent shape. The "noparent" attribute excludes all parent shape and tests only against non parent shapes. 
Moreover, only active shapes are included in the testing process. That means, that always the most specific shape is used to determine if the current shape is occluded or not.

A typical Occlusion Queriy may look like this:

        wall_element : occ(noparent) == none  ::- window;
        wall_element : occ(noparent) == part  ::- wall;
        wall_element : occ(noparent) == full  ::- null;

This production rules will test for each wall element if it is occluded by any active non parent shape. If not, a window will be placed at this element. If it is fully occluded (the wall will lay inside the house), no derivation is needed (null equals an epsilon rule). If the wall element is partly occluded, a single wall elemen is placed to fill the gap.

### 2.2 Sightlines

Sightlines are very useful to place doors correctly (there may be other fields of application as well). For example, you want to place a door to a wall if its facing a street. Therefore, you can use the sightline test. It tests if the shortest sightlines to the specified geometry are occluded.

A typical Sightline test may look like the following:

        facade : visible("street")  ::- divide x {
                                           [50%]   wall_elements
                                           [3]        entrance
                                           [50%]   wall_elements
                                        }
        facade ::- wall_elements;

# Related Links
 * [[Grammar System]]
 * [Procedural Modeling of Buildings - Peter Wonka](http://peterwonka.net/Publications/mueller.procedural%20modeling%20of%20buildings
 .SG2006.final-web.pdf)
 * [Procedural World Blog](http://procworld.blogspot.de/)
 * [PAG Incubator (Forum)](http://forum.movingblocks.net/threads/procedural-architecture-grammar.586/)
 * [City Generation and AI (Forum)](http://forum.movingblocks.net/threads/villages-concept-and-stuff.521/)

