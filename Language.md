# TurboTurtle Logo Language #

One of the most fundamental differences between TurboTurtle and the usual Logo interpreters is related to the way that the graphics which have been drawn are presented to the user.  Other Logo interpreters typically draw each line instantly on the screen.  Since TurboTurtle is designed for animation and speed, it always uses double buffering.  With this technique, all drawing commands are drawn to an off-screen memory buffer in the video card.  To display the drawn graphics to the user, the Logo program must call the Clean or Clearscreen command.  Only after this command has been called will the lines and dots drawn be displayed on the monitor screen.

The TurboTurtle compiler uses the same general syntax as UCBLogo and most other implementations.  Some particular similarities are:
  * Names of procedures and variables are case-insensitive, as are the special words TO, END, TRUE, and FALSE.
  * Words start with a quotation mark and can contain any character except a space, a square bracket, or a parenthesis.
  * Procedure or variables names can contain any characters except a space, a bracket, a parenthesis, or an infix operator (`+-*/=<>`)
  * An instruction line can be continued onto the following line if its last character is a tilde (~)
  * END must be on a line by itself

However, since TurboTurtle is a compiler instead of an interpreter and is designed for speed, there are a number of limitations which apply.
  * Data values can only be: word, boolean, number, list of numbers, array of numbers
  * Variables cannot change type
  * Variable types must be knowable at compile time
  * Functions must always return the same type (cannot mix OUTPUT and STOP in the same procedure)
  * Default screen mode is WINDOW, not WRAP, though both modes are supported
  * Restrictions on arrays:
    * Arrays can be re-defined to different sizes, but not different numbers of dimensions
    * Only 1-D, 2-D, and 3-D arrays supported
    * ARRAY and MDARRAY instructions can only be used as inputs to MAKE or LOCALMAKE
    * Arrays may be passed in to procedures as arguments, but cannot be returned from them
    * MDARRAY instruction can only take an immediate list (like `[1 2 3]`) or a LIST instruction as its input.  It cannot take a variable (because the number of dimensions must be known at compile time).
    * The default origin for MDARRAY is 0, not 1
    * immediate arrays (with braces) not supported
  * THING command not supported
  * MAKE :VAR not supported
  * Scope of local variables does not cascade to sub-procedures

Finally, since TurboTurtle was designed for graphics and animation, there are some instructions which are not supported or work slightly differently than in UCBLogo, and other instructions which have been added.
  * Added font handling instructions: SETFONT, SETFONTHEIGHT, SETJUSTIFYVERT, SETJUSTIFYHORZ
  * Added .SETSPECIAL instruction and four special variables: FramesPerSec, HighPrecision, WindowSize, and LineSmooth
  * Added ERASESCREEN: clears the drawing screen but doesn't flip pages
  * Added GAUSSIAN: returns a random number of gaussian distribution with mean 0.0 and standard deviation 1.0
  * Added DOT: plots a dot on the screen with the current color and pen size, if the pen is down
  * LABEL instruction works differently
  * PRINT instruction works differently
  * Setter functions not supported
  * Vertical bars (pipes, ||) not supported
  * Optional procedure inputs not supported
  * Macros and Templates not supported
  * File and other I/O operations not supported