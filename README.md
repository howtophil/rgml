Radio Graphics Markdown Language (RGML)
(Phillip J Rhoades - KE8GGD)
Also on pastebin: https://pastebin.com/j8Y1p5yE

----------------------------------

This is a simple set of narrow-band transmittable instructions that could be
used to transfer a schematic, drawing, etc from one location to another.

It could be used over CW, voice, RTTY, MFSK32, etc...

The receiving end could use a computer program to decode the instructions
or could hand-decode using graph paper, a hand-drawn grid, etc.

Lossless diagram transmission, fun little graphics, complex drawings built
up from simple shapes, etc are all possible.

----------------------------------

Functions

GR X,Y
	Header function
	Define grid space dimensions. Use lines as the unit of measurement. (Line graphics)

GRB X,Y
	Header function
	Define grid space dimensions. Use boxes as the unit of measurement. (Chunky graphics)

PL X,Y,X,Y,X,Y... 
	Plot a line along an indefinite number of points.
	Or a single point with one PL X,Y
	Rhombuses, stars, and generally complex shapes.

SQ X1,Y1,X2,Y2
	Rectangles, squares, horizontal and vertical lines.

TR X1,Y1,X2,Y2,X3,Y3
	Draw a triangle as defined by three points.

CR X,Y,Radius
	Draw a circle of a given radius, centered at X,Y

TT X,Y,"Text to place",Vertical Anchor, Horizontal Anchor
	Place text at X,Y
	Anchor expressed as Top, Bottom, Middle (TBC) and Left, Right, Center (LRC)
		Anchors are optional. Defaults to top left corner as an anchor point.
	TT 1,20,"Hello world.",C,L

CL [Color name or hex code]
	Use this color (if available) for lines until instructed otherwise.
	CL with no color would return to default (black lines).

CF [Color name or hex code]
	Use this color for fills until instructed otherwise.
	CF with no color would return to no-fill (default)

F (modifier) can preface any graphics function.
	This is a call to draw a filled shape.
	FSQ X1,Y1,X2,Y2 is a filled rectangle.
	FTR [...] a filled triangle.
	FCR [...] a filled circle.
	Be sure to have a CF statement to define fill color first.
	F without a predefined fill color is considered an erasure. (overlaps with E modifier)
		Unused parts of a shape could be erased with no-color fills of other shapes.

E (modifier) can preface any graphics function.
	Erases lines, fills, etc in defined shape space.
	ESQ X1,Y1,X2,Y2 is used to erase a rectangle of area
	ETR [...] an eraser triangle.
	ECR [...] an eraser circle.
	This allows you to draw a shape, then remove parts that are not needed.
		Could get an arc out of a circle and an erase-circle/rectangle, triangle, etc

----------------------------------
  
> GR 10,10  
> SQ 2,9,6,5  
> PL 3,8  
> PL 5,8  
> PL 3,7,4,6,5,7  
> SQ 3,5,5,3  
> SQ 1,3,7,1  
> PL 8,7,7,6,8,5  
> TT 8,6,"HELLO",C,L  
  
----------------------------------
