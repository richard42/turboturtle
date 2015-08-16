## Version ##
This document applies to version 1.0 of TurboTurtle.

## Instructions ##
TurboTurtle supports about 100 built-in Logo instructions.  This page is intended to be a reference for the usage of these instructions.

Instructions which have parentheses around their names are parenthesized instructions.  These are special instructions which use a different number of input parameters from their non-parenthesized versions, or contain a variable number of input parameters.  For a parenthesized instruction, like: (SUM 1 2 3 4 5), all of the available parameters within the parentheses are gathered and used as inputs to the instruction.

## Operand Types ##
  * _number_
    * A floating-point numeric value.  Can be either an immediate number (like `42` or `10.3`), or a numeric value returned from another instruction, or a numeric value in a variable, or a combination of any of these in a numeric expression (such as 42 `*` :angle + Heading)
  * _immediate number_
    * A numeric value which is given directly in the Logo program, such as `1` or `3.14159`
  * _boolean_
    * A boolean value.  Can be either an immediate boolean (True or False), or a boolean value returned from another instruction, or a boolean value in a variable, or a comparison expression.  A comparison expression can either compare two numeric values (42 `*` :angle < 180.0) or two booleans (:LastCond <> Xor :a :b).  Boolean comparisons can only compare for equality or non-equality, while numeric comparisons can also compare for greater-than or less-than.
  * _word_
    * A text value.  Can be either an immediate word, or a text value returned from an instruction, or a text value in a variable.
  * _immediate word_
    * A word whose value is given directly in the Logo program, such as `"This_is_a_word`
  * _list_
    * An ordered list of numbers.  Can be either an immediate list, or a list returned from an instruction, or the value of a list variable
  * _immediate list_
    * A group of immediate numbers separated by spaces and surrounded by brackets, such as: `[1 2 3 4.5 67 0.899 -20]`
  * _instructionlist_
    * A sequence of instructions surrounded by brackets, such as `[ Home FD 20 RT 90 ]`
  * _array_
    * A set of numbers in a 1, 2, or 3 dimensional matrix.  The only functions which can return arrays are ARRAY and MDARRAY, and these 2 functions can only be used as inputs to the MAKE instruction.  All other instructions must use arrays stored in variables.

## Variable Definition ##
There are two instructions for defining variables: one for global variables and one for local variables.  These instructions do not return any value.

  * MAKE **name** **value**
    * <u>Operand types</u>: **name** (_immediate word_), **value** (_number_ or _list_ or _word_ or _array_ or _boolean_)
    * <u>Usage</u>: This instruction creates a global variable named **name** and assigns it a value of **value**.

  * LOCALMAKE **name** **value**
    * <u>Operand types</u>: **name** (_immediate word_), **value** (_number_ or _list_ or _word_ or _array_ or _boolean_)
    * <u>Usage</u>: This instruction creates a local variable named **name** and assigns it a value of **value**.  The LOCALMAKE instruction can only be used inside of a procedure.

## Control Structures ##
The control instructions handle normal programming constructs like looping, conditional execution, exiting and returning a value from a procedure, and jumping to a different part of the program.

| <u>Return Type</u> | <u>Instruction</u> | <u>Abbreviated Name</u> | <u>Operand 1</u> | <u>Operand 2</u> | <u>Usage</u> |
|:-------------------|:-------------------|:------------------------|:-----------------|:-----------------|:-------------|
|                    | REPEAT             |                         | _number_ **count** | _instructionlist_ **instructionlist** | Executes the instructions in **instructionlist** in a loop **count** times.  If **count** is less than 1, **instructionlist** will not be executed. |
|                    | FOREVER            |                         | _instructionlist_ **instructionlist** |                  | Executes the instructions in **instructionlist** continuously. |
| _number_           | REPCOUNT           |  #                      |                  |                  | Returns the value of the loop counter for the innermost REPEAT or FOREVER instruction.  The counter begins at 1 and increments by 1 at the end of each loop iteration. |
|                    | FOR                |                         | _special_ **forcontrol** | _instructionlist_ **instructionlist** | This instruction will create a new local variable and execute the instructions in **instructionlist**, updating the value of the local variable after each iteration, until a condition is met.  The format of **forcontrol** can be either `[`**varname** **start** **stop**`]` or `[`**varname** **start** **stop** **step**`]`.  **varname** is the name of the local variable which will be created.  **varname** is like an _immediate word_, but without the preceding quotation mark.  **start**, **stop**, (and **limit** if present) are _numbers_.  For the 3-parameter variant, first **varname** is initialized to the number **start**, the loop begins and the **instructionlist** is executed, then **varname** changes in the direction of **stop** by 1.0 units.  If the value of **varname** has not crossed over **stop** and is not equal to **stop**, another loop iteration begins and **instructionlist** is executed again.  The 3-parameter variant guarantees that **instructionlist** will be executed at least once and will not be executed more than floor(abs(**stop** - **start**))+1 times.  For the 4-parameter variant, first **varname** is initialized to the number **start**, then the loop begins.  The loop starts by comparing the sign of **varname**-**stop** to the sign of **step**.  If **varname** is equal to **stop** or the sign of **varname**-**stop** is different from the sign of **step**, then the **instructionlist** is executed, **step** is added to **varname**, and the loop begins again.  Otherwise the loop ends.  It is possible to construct a 4-parameter FOR loop which will not execute the **instructionlist** at all, such as FOR `[ i 0 2 -1 ]` |
|                    | DO.WHILE           |                         | _instructionlist_ **instructionlist** | _boolean_ **tf** | This instruction repeatedly executes **instructionlist** and then tests value of the expression **tf**, until the value of **tf** is False.  For example, if **tf** is the _immediate boolean_ False, the **instructionlist** will only execute once.  However, if **tf** is the _immediate boolean_ True, it will execute repeatedly forever. |
|                    | WHILE              |                         | _boolean_ **tf** | _instructionlist_ **instructionlist** | This instruction repeatedly tests the value of the expression **tf**, breaks out of the loop if the value of **tf** is False, otherwise executes **instructionlist** and begins the loop again.  If **tf** is the _immediate boolean_ False, the **instructionlist** will not execute at all.  However, if **tf** is the _immediate boolean_ True, it will execute repeatedly forever. |
|                    | DO.UNTIL           |                         | _instructionlist_ **instructionlist** | _boolean_ **tf** | This instruction repeatedly executes **instructionlist** and then tests value of the expression **tf**, until the value of **tf** is True.  For example, if **tf** is the _immediate boolean_ False, the **instructionlist** will execute repeatedly forever.  However, if **tf** is the _immediate boolean_ True, it will only execute once. |
|                    | UNTIL              |                         | _boolean_ **tf** | _instructionlist_ **instructionlist** | This instruction repeatedly tests the value of the expression **tf**, breaks out of the loop if the value of **tf** is True, otherwise executes **instructionlist** and begins the loop again.  If **tf** is the _immediate boolean_ False, the **instructionlist** will execute repeatedly forever.  However, if **tf** is the _immediate boolean_ True, it will not execute at all. |

| <u>Instruction</u> | <u>Abbreviated Name</u> | <u>Operand 1</u> | <u>Operand 2</u> | <u>Operand 3</u> | <u>Usage</u> |
|:-------------------|:------------------------|:-----------------|:-----------------|:-----------------|:-------------|
| IF                 |                         | _boolean_ **tf** | _instructionlist_ **instructionlist** |                  | If the boolean expression **tf** evaluates to True, then the instructions in **instructionlist** will be executed. |
| IFELSE             |                         | _boolean_ **tf** | _instructionlist_ **instructionlist1** | _instructionlist_  **instructionlist2** | If the boolean expression **tf** evaluates to True, then the instructions in **instructionlist1** will be executed.  Otherwise, the instructions in **instructionlist2** will be executed. |
| TEST               |                         | _boolean_ **tf** |                  |                  | This instruction evaluates the boolean expression **tf** and sets an internal flag with the result.  This internal flag can be subsequently used to conditionally execute instructions with the IFTRUE and IFFALSE instructions. |
| IFTRUE             | IFT                     | _instructionlist_ **instructionlist** |                  |                  | If and only if the value of the internal flag which is set by the TEST instruction is True, then the instructions in **instructionlist** will be executed.  The default value of the internal flag is False. |
| IFFALSE            | IFF                     | _instructionlist_ **instructionlist** |                  |                  | If and only if the value of the internal flag which is set by the TEST instruction is False, then the instructions in **instructionlist** will be executed.  The default value of the internal flag is False. |

| <u>Instruction</u> | <u>Abbreviated Name</u> | <u>Operand 1</u> | <u>Usage</u> |
|:-------------------|:------------------------|:-----------------|:-------------|
| STOP               |                         |                  | The STOP instruction returns from a procedure and resumes execution at the next instruction after the procedure call.  The STOP instruction does not return any value.  The STOP instruction can only be used from within a user-defined procedure.  A procedure cannot contain both STOP and OUTPUT instructions. |
| OUTPUT             | OP                      | _number_ or _list_ or _word_ or _boolean_ **value** | The OUTPUT instruction exits from a user-defined procedure and returns **value** in the place where the procedure was called.  The OUTPUT instruction can only be used from within a user-defined procedure.  A procedure cannot contain both STOP and OUTPUT instructions, and all OUTPUT instructions in a user-defined procedure must return the same type. |
| WAIT               |                         | _number_ **time** | This instruction pauses for a specified amount of time.  The amount of time for which the program execution is paused is equal to **time**/60 seconds.  For example, "WAIT 60.0" will pause for exactly 1 second. |
| GOTO               |                         | _immediate word_ **label** | The GOTO instruction causes the execution path of the program to jump to the instruction TAG with the same label as **label**. |
| TAG                |                         | _immediate word_ **label** | The TAG instruction denotes the place in the program to where a GOTO instruction with the same **label** will jump. |

## Graphics ##
These are instructions for drawing lines, plotting points, and writing text on the drawing surface.  These instructions do not return any value.

| <u>Instruction</u> | <u>Abbreviated Name</u> | <u>Operand 1</u> | <u>Operand 2</u> | <u>Usage</u> |
|:-------------------|:------------------------|:-----------------|:-----------------|:-------------|
| FORWARD            | FD                      | _number_ **dist** |                  | Moves the turtle from the current position to a new position forward by **dist** steps in the current direction.  If the Pen is down, a line will be drawn.  The color of the line will be the Pen color if the Pen is in Paint mode, or the Background color if in Erase mode. |
| BACK               | BK                      | _number_ **dist** |                  | Moves the turtle from the current position to a new position backward by **dist** steps.  If the Pen is down, a line will be drawn.  The color of the line will be the Pen color if the Pen is in Paint mode, or the Background color if in Erase mode. |
| LEFT               | LT                      | _number_ **angle** |                  | Causes the turtle to turn to the left (counter-clockwise) by **angle** degrees. |
| RIGHT              | RT                      | _number_ **angle** |                  | Causes the turtle to turn to the right (clockwise) by **angle** degrees. |
| DOT                |                         | _number_ **xpos** | _number_ **ypos** | Plots a dot at the position (**xpos**, **ypos**) in the current pen color and size, if the pen is down. |
| (LABEL)            |                         | _number_ or _word_ **thing1** | _number_ or _word_ ... | Prints the values of each of its inputs, separated by spaces.  The output is drawn to the screen using the current pen color, the current font and font height, and is positioned at the current turtle position with the current horizontal and vertical justification.  This instruction must be surrounded by parentheses and can accept one or more operands. |
| SETFONT            |                         | _number_ **fontnum** |                  | Sets the current font.  There are three available fonts, numbered 0 through 2.  All three fonts are fixed-width.  The dimensions of font 0 are 8x12, font 1 is 12x16, and font 2 is 10x18. |
| SETFONTHEIGHT      |                         | _number_ **height** |                  | Sets the current font height to **height** turtle steps.  The width of each character will be set to maintain the correct aspect ratio for the selected font. |
| SETJUSTIFYVERT     |                         | _number_ **index** |                  | Sets the current vertical justification type used by the LABEL instruction.  An **index** value of 0 or less will cause the text to be drawn below the turtle position.  An **index** value of exactly 1 will cause the text to be drawn vertically centered over the turtle position.  And **index** value of 2 or more will cause the text to be drawn above the turtle position. |
| SETJUSTIFYHORZ     |                         | _number_ **index** |                  | Sets the current horizontal justification type used by the LABEL instruction.  An **index** value of 0 or less will cause the text to be drawn to the right of the turtle position.  An **index** value of exactly 1 will cause the text to be drawn horizontally centered over the turtle position.  And **index** value of 2 or more will cause the text to be drawn to the left of the turtle position. |
| SETPOS             |                         | _list_ **pos**   |                  | Sets the current turtle position to the X,Y location given by the first 2 elements of the list **pos**. This draws a line if the pen is down. |
| SETXY              |                         | _number_ **xcor** | _number_ **ycor** | Sets the current turtle position to the X,Y location given by the two input numbers **xcor**,**ycor**. This draws a line if the pen is down |
| SETX               |                         | _number_ **xcor** |                  | Sets the X coordinate of the turtle position to **xcor**.  This draws a line if the pen is down. |
| SETY               |                         | _number_ **ycor** |                  | Sets the Y coordinate of the turtle position to **ycor**.  This draws a line if the pen is down. |
| SETHEADING         | SETH                    | _number_ **degrees** |                  | Sets the current heading of the turtle (the direction that it's facing) to **degrees**.  The heading is measured in degrees clockwise from the +Y axis (straight up). |
| SETSCRUNCH         |                         | _number_ **xratio** | _number_ **yratio** | Sets the scrunch ratios in the X and Y directions.  This is primarily useful to correct for displays with non-square pixel aspect ratios.  Currently the scrunch ratios are only used for the FORWARD and BACK instructions. They are not taken into account for other instructions like SETPOS and SETXY. |

## Turtle Motion Queries ##
These instructions return information about the current status of the turtle.

| <u>Return Type</u> | <u>Instruction</u> | <u>Operand 1</u> | <u>Usage</u> |
|:-------------------|:-------------------|:-----------------|:-------------|
| _list_             | POS                |                  | Returns a 2-item list containing the current X and Y coordinates of the turtle. |
| _number_           | XCOR               |                  | Returns the current X coordinate of the turtle. |
| _number_           | YCOR               |                  | Returns the current Y coordinate of the turtle. |
| _number_           | HEADING            |                  | Returns the current heading of the turtle, measured in degrees clockwise from the +Y axis. |
| _number_           | TOWARD             | _list_ **pos**   | Returns a number which is the heading (in degrees) necessary to make the turtle point from its current position to the position given by **pos**. |

## Turtle and Window Control ##
These are control instructions for the turtle and display window.  These instructions do not take any operands or return any value.

| <u>Instruction</u> | <u>Abbreviated Name</u> | <u>Usage</u> |
|:-------------------|:------------------------|:-------------|
| CLEAN              |                         | Displays everything drawn since the last CLEAN, CLEARSCREEN, or ERASESCREEN instruction and erases the drawing surface.  This instruction does not move the turtle. |
| CLEARSCREEN        | CS                      | Performs exactly the same actions as calling both HOME and CLEAN. |
| ERASESCREEN        |                         | Erases everything on the drawing surface without displaying any previously drawn lines or dots on the screen. |
| HOME               |                         | Moves the turtle to position (0,0) and sets the heading to 0 degrees. |
| WRAP               |                         | Sets the current screen wrapping mode to WRAP. In this mode, when the turtle moves past any of the 4 display boundaries (top, bottom, left, or right), it is transported to the opposite boundary and continues moving.  Using either the WRAP or WINDOW instructions in a TurboTurtle program will cause a performance penalty. |
| WINDOW             |                         | Sets the current screen wrapping mode to WINDOW.  In this mode, when the turtle moves past any of the 4 display boundaries, the lines drawn are no longer visible on the screen until the turtle comes back within the display boundaries.  This is the default mode for TurboTurtle programs.  Using either the WRAP or WINDOW instructions in a TurboTurtle program will cause a performance penalty. |

## Pen and Background Control ##
These are control instructions for the turtle's pen.  These instructions do not return any value.

| <u>Instruction</u> | <u>Abbreviated Name</u> | <u>Operand 1</u> | <u>Usage</u> |
|:-------------------|:------------------------|:-----------------|:-------------|
| PENDOWN            | PD                      |                  | Puts the turtle into the PenDown mode, so that subsequent move commands will cause lines to be drawn. |
| PENUP              | PU                      |                  | Puts the turtle into the PenUp mode, so that subsequent move commands will only change the position of the turtle, without drawing lines or points. |
| PENPAINT           | PPT                     |                  | Sets the turtle into Paint mode, so that subsequent points or lines will be drawn with the PenColor. |
| PENERASE           | PE                      |                  | Sets the turtle into Erase mode, so that subsequent points or lines will be drawn with the Background Color. |
| SETPENCOLOR        | SETPC                   | _number_ or _list_ **color** | Sets the current Pen Color (foreground).  If the input is a _number_, it must be between 0 and 15, and the color will be set according to the color table below.  If the input is a _list_, it must have at least 3 elements, and the color will be set to the RGB value given by the first 3 elements of the list.  Each element should be between 0 and 255. |
| SETPENSIZE         |                         | _number_ **size** | Sets the Pen Size, which affects the width of lines drawn and points plotted.  The default Pen Size is 1.0. |
| SETBACKGROUND      | SETBG                   | _number_ or _list_ **color** | Sets the current Background Color.  If the input is a _number_, it must be between 0 and 15, and the color will be set according to the color table below.  If the input is a _list_, it must have at least 3 elements, and the color will be set to the RGB value given by the first 3 elements of the list.  Each element should be between 0 and 255. |

### Color Table ###
| 0  black   | 1  blue    | 2  green   | 3  cyan |
|:-----------|:-----------|:-----------|:--------|
| 4  red     | 5  magenta | 6  yellow  | 7  white |
| 8  brown   | 9  tan     | 10  forest | 11 aqua |
| 12  salmon | 13  purple | 14  orange | 15 grey |

## Constructors ##

| <u>Return Type</u> | <u>Instruction</u> | <u>Operand 1</u> | <u>Operand 2</u> | <u>Usage</u> |
|:-------------------|:-------------------|:-----------------|:-----------------|:-------------|
| _list_             | LIST               | _number_ **num1** | _number_ **num2** | Returns a _list_ with 2 elements: **num1** and **num2**. |
| _list_             | (LIST)             | _number_ **num1** | _number_ ...     | Returns a _list_ with 1 or more elements, one for each of the numeric values within the parentheses. |
| _list_             | FPUT               | _number_ **num1** | _list_ **list1** | FirstPut - Returns a _list_ which begins with the value of **num1**, and then contains all of the elements of **list1** |
| _list_             | LPUT               | _number_ **num1** | _list_ **list1** | LastPut - Returns a _list_ which begins with all of the elements of **list1**, followed by the value of **num1** |
| _list_             | REVERSE            | _list_ **list1** |                  | Returns a _list_ with the elements in the opposite order of those in **list1** |
| _array_            | ARRAY              | _number_ **size** |                  | Returns a 1 dimensional array of length **size**.  The first index number of the array is 1.  This instruction can only be used as an input to MAKE or LOCALMAKE |
| _array_            | (ARRAY)            | _number_ **size** | _number_ **start** | Returns a 1 dimensional array of length **size**.  The first index number of the array is **start**.  This instruction can only be used as an input to MAKE or LOCALMAKE |
| _array_            | MDARRAY            | _list_ **sizelist** |                  | Returns a multi-dimensional array with the same number of dimensions as there are elements in **sizelist**.  The length of each dimension in the array is given by the corresponding element in **sizelist**.  The first index number of each dimension in the array is 0 (this is different from most Logo interpreters).  This instruction can only be used as an input to MAKE or LOCALMAKE |

## Selectors ##
These are instructions which return numbers or lists generated from lists or arrays.
| <u>Return Type</u> | <u>Instruction</u> | <u>Operand 1</u> | <u>Operand 2</u> | <u>Usage</u> |
|:-------------------|:-------------------|:-----------------|:-----------------|:-------------|
| _number_           | FIRST              | _list_ **list1** |                  | Returns the first element in **list1** |
| _number_           | LAST               | _list_ **list1** |                  | Returns the last element in **list1** |
| _list_             | BUTFIRST           | _list_ **list1** |                  | Returns a list containing all elements but the first in **list1** |
| _list_             | BUTLAST            | _list_ **list1** |                  | Returns a list containing all elements but the last in **list1** |
| _number_           | ITEM               | _number_ **index** | _list_ or _array_ **thing** | Returns the numeric element corresponding to **index** in **thing**. |
| _number_           | MDITEM             | _list_ **indexlist** | _array_ **array1** | Returns the numeric element corresponding to the vector **indexlist** in multi-dimensional **array1**. The first index number of each dimension in the array is 0. |
| _number_           | PICK               | _list_ **list1** |                  | Returns one of the elements in **list1**, randomly selected |

## Queries, Predicates, and Mutators ##
| <u>Return Type</u> | <u>Instruction</u> | <u>Operand 1</u> | <u>Operand 2</u> | <u>Operand 3</u> | <u>Usage</u> |
|:-------------------|:-------------------|:-----------------|:-----------------|:-----------------|:-------------|
| _number_           | COUNT              | _list_ **list1** |                  |                  | Returns the number of elements in **list1** |
| _boolean_          | EMPTYP             | _list_ **list1** |                  |                  | Returns True if there are no elements in **list1**, otherwise False |
| None               | SETITEM            | _number_ **index** | _array_ **array1** | _number_ **value** | Sets the numeric element corresponding to **index** in **array1** to **value**. |
| None               | MDSETITEM          | _list_ **indexlist** | _array_ **array1** | _number_ **value** | Sets the numeric element corresponding to the vector **indexlist** in multi-dimensional **array1** to **value**. |


## Numeric opterations ##
These instructions perform numeric calculations.  They all return a _number_.
| <u>Instruction</u> | <u>Operand 1</u> | <u>Operand 2</u> | <u>Usage</u> |
|:-------------------|:-----------------|:-----------------|:-------------|
| ABS                | _number_ **num1** |                  | Returns the absolute value of **num1** |
| MINUS              | _number_ **num1** |                  | Returns -1 times the value of **num1** |
| SUM                | _number_ **num1** | _number_ **num2** | Returns the sum of **num1** and **num2** |
| (SUM)              | _number_ **num1** | _number_ ...     | Returns the sum of all inputs. There must be at least two. |
| DIFFERENCE         | _number_ **num1** | _number_ **num2** | Returns **num1** - **num2** |
| PRODUCT            | _number_ **num1** | _number_ **num2** | Returns **num1** times **num2** |
| (PRODUCT)          | _number_ **num1** | _number_ ...     | Returns the product of all inputs multiplied together. There must be at least two. |
| QUOTIENT           | _number_ **num1** | _number_ **num2** | Returns **num1** divided by **num2** |
| (QUOTIENT)         | _number_ **num1** |                  | Returns 1.0 divided by **num1** |
| REMAINDER          | _number_ **num1** | _number_ **num2** | Returns the remainder of the integer (whole part of) **num1** divided by the integer of **num2** |
| INT                | _number_ **num1** |                  | Returns the integer of **num1** |
| ROUND              | _number_ **num1** |                  | Returns the value of **num1** rounded to the nearest integer. If the fractional part of **num1** is one half, it's rounded away from  zero  |
| SQRT               | _number_ **num1** |                  | Returns the square root of **num1** |
| POWER              | _number_ **num1** | _number_ **num2** | Returns the value of **num1** raised to the power of **num2** |
| EXP                | _number_ **num1** |                  | Returns the value of e (the base of the natural logarithm) to the power of **num1** |
| LOG10              | _number_ **num1** |                  | Returns the value of the base-10 logarithm of **num1** |
| LN                 | _number_ **num1** |                  | Returns the value of the natural logarithm of **num1** |
| SIN                | _number_ **degrees** |                  | Returns the sine of **degrees** |
| RADSIN             | _number_ **radians** |                  | Returns the sine of **radians** |
| COS                | _number_ **degrees** |                  | Returns the cosine of **degrees** |
| RADCOS             | _number_ **radians** |                  | Returns the cosine of **radians** |
| ARCTAN             | _number_ **ratio** |                  | Returns the arctangent of **ratio**, in degrees |
| (ARCTAN)           | _number_ **x**   | _number_ **y**   | Returns the arctangent of **y**/**x**, in degrees |
| RADARCTAN          | _number_ **ratio** |                  | Returns the arctangent of **ratio**, in radians |
| (RADARCTAN)        | _number_ **x**   | _number_ **y**   | Returns the arctangent of **y**/**x**, in radians |

## Random numbers ##
| <u>Return Type</u> | <u>Instruction</u> | <u>Operand 1</u> | <u>Operand 2</u> | <u>Usage</u> |
|:-------------------|:-------------------|:-----------------|:-----------------|:-------------|
| _number_           | GAUSSIAN           |                  |                  | Returns a random number of gaussian distribution with mean 0.0 and standard deviation 1.0 |
| _number_           | RANDOM             | _number_ **range** |                  | Returns a random integer evenly distributed between 0 and **range**-1 |
| _number_           | (RANDOM)           | _number_ **start** | _number_ **end** | Returns a random integer evenly distributed between **start** and **end** |
|                    | RERANDOM           |                  |                  | Initializes the random number generator to a predictable state. The sequence of random numbers will always be the same (given the same ranges) after a RERANDOM instruction |
|                    | (RERANDOM)         | _number_ **seed** |                  | Initializes the random number generator to a predictable state. Each integer value of **seed** will give a unique, predictable sequence of random numbers after the RERANDOM instruction |

## Logical operations ##
These instructions perform logical calculations.  They all return a _boolean_.
| <u>Instruction</u> | <u>Operand 1</u> | <u>Operand 2</u> | <u>Usage</u> |
|:-------------------|:-----------------|:-----------------|:-------------|
| AND                | _boolean_ **tf1** | _boolean_ **tf2** | Returns True if both **tf1** and **tf2** are True, otherwise returns False. |
| (AND)              | _boolean_ **tf** | _boolean_ ...    | Returns True if <u>all</u> of the inputs are True, otherwise returns False. There must one or more inputs. |
| OR                 | _boolean_ **tf1** | _boolean_ **tf2** | Returns True if either **tf1** or **tf2** are True, otherwise returns False. |
| (OR)               | _boolean_ **tf** | _boolean_ ...    | Returns True if <u>any</u> of the inputs are True, otherwise returns False. There must one or more inputs. |
| NOT                | _boolean_ **tf1** |                  | Returns the logical inverse of **tf1**. |

## Special Instructions ##

| <u>Instruction</u> | <u>Operand 1</u> | <u>Operand 2</u> | <u>Usage</u> |
|:-------------------|:-----------------|:-----------------|:-------------|
| .SETSPECIAL        | _immediate word_ **name** | _number_ **value** | This instruction sets the special TurboTurtle program constant named **name** to a value of **value**.  The supported variable names are given in the table below. |
| (PRINT)            | _word_ or _number_ or _boolean_ **thing1** | _word_ or _number_ or _boolean_ ... | This is a debugging instruction.  It prints the values of each of its inputs, separated by spaces, to the standard output (terminal). There must one or more inputs. |

### Special variables ###
| <u>Name</u> | <u>Meaning</u> |
|:------------|:---------------|
| FramesPerSec | Setting the FramesPerSec special variable to a non-zero value will cause the wrapper code to insert a variable delay after each CLEAN or CLEARSCREEN instruction in order to maintain an average speed of the given number of Frames per Second |
| HighPrecision | Setting the HighPrecision special variable to a non-zero value will cause the Logo program and wrapper to use double-precision floating-point variables instead of single-precision.  This can remove artifacts in some very sensitive programs such as Fern.logo |
| WindowSize  | Setting the WindowSize special variable to any value will cause the display window's height and width to be at least the given number of turtle steps |
| LineSmooth  | Setting the LineSmooth special variable to 0 will disable line anti-aliasing.  Setting LineSmooth to 1 will enable the fastest line anti-aliasing.  Setting LineSmooth to 2 (the default) will enable the highest-quality line anti-aliasing. |