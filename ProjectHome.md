**TurboTurtle** was built to achieve the maximum possible performance for Turtle Graphics programs, for creating high-speed animations of fractals and geometric designs.

The high-level computer language called Logo was created in the 1960s and used commonly in schools in the 1970s and 1980s.  One of Logo's primary design goals was to be simple and easy to learn but also very powerful and capable of supporting complex operations.  The simplicity of the syntax and the built-in Turtle Graphics capabilities made it a perfect fit for elementary education; I remember using Terrapin Logo on Apple IIe computers in the 3rd grade.

TurboTurtle consists of two parts: a compiler written in Python which compiles the input logo source code into C++, and a set of wrapper files in C++ which are compiled together with the C++ output of the Logo compiler to produce a final executable.

## The Language ##
Turtle Graphics have been implemented in many different computer languages, but the simplicity and the sparse syntax of the Logo language led me to select Logo for this project.  Many different implementations of the Logo language have been published over the years.  I choose the [UCBLogo](http://www.cs.berkeley.edu/~bh/logo.html) implementation as my reference for this project, because it is open source, platform-independent, and well-documented.

The [Language](Language.md) page describes the important similarities and differences between the Logo variants supported by UCBLogo and TurboTurtle.

The [Instructions](Instructions.md) page gives a reference for all of the built-in instructions which are currently supported by TurboTurtle.

## Demo Files ##
There are 35 demonstration Logo programs included with TurboTurtle v1.0.  All but a few of these are adaptations from Logo programs published at http://www.logoarts.co.uk/. Thanks to Guy Walker for permission to include these in TurboTurtle.

## Performance ##
So how fast is TurboTurtle?  Very fast.  I ran a simple benchmark on my development machine (Athlon 64 x2 3800+, 2.0 GHz).  Using the demonstration program Fern.logo, I copied the Fern and Hue procedures (with a small change for compatibility) into UCBLogo and ran "Fern 440 2.0 0.32 0.9".  The interpreter took about 11 seconds to draw the Fern.  I then modified the Fern.logo file to continuously draw the Fern with these parameters, and the resulting executable (which also drew the sliders with labels) ran at 33 frames per second, or 0.03 seconds per frame.  So for this benchmark test, the compiled TurboTurtle program was more than 300 times faster than the UCBLogo interpreter.

## Try It Out ##
To view pre-compiled TurboTurtle demo programs, download one of the binary demo packs on the right.  The Linux versions should run on almost any standard Linux distribution - all that's required are the SDL and OpenGL libraries.  The Windows demo pack should work with Windows XP or newer.  Look at the [command-line options](Readme#Command-line_Options.md) in the [Read-me wiki](Readme.md) for a list of command-line options to tweak the graphical output.

## Build Your Own ##
To compile your own Logo programs with TurboTurtle, download the TurboTurtle compiler source code and read the [compiler directions](Readme#Compiling_Demo_Programs.md) in the [Read-me wiki](Readme.md).  You will also need the software listed in the System Requirements section below.

## System Requirements ##
TurboTurtle was developed and tested on a Linux workstation but uses platform-independent technologies, so porting to Windows should be relatively easy.  To compile your own Logo programs with TurboTurtle, the following software tools are needed:
  1. Python
    * Python v2.5.2 was used for the development of TurboTurtle, but it should work with little modifications for any Python release from 2.4 up to 2.6.
  1. C++ compiler and libraries
    * GNU GCC/G++ is recommended
  1. OpenGL drivers and development headers and libraries
  1. SDL version 1.2.x

## Screenshots ##
Static screenshots such as these don't do justice to the smooth animation in some of these TurboTurtle programs, but they will give you an idea of what kind of graphics are possible.

| [![](http://turboturtle.googlecode.com/svn/wiki/images/Diatoms_thumb.png)](http://code.google.com/p/turboturtle/wiki/Screenshots#Diatoms) | [![](http://turboturtle.googlecode.com/svn/wiki/images/DragonCurve_thumb.png)](http://code.google.com/p/turboturtle/wiki/Screenshots#Dragon_Curve) | [![](http://turboturtle.googlecode.com/svn/wiki/images/Fern_thumb.png)](http://code.google.com/p/turboturtle/wiki/Screenshots#Fern) | [![](http://turboturtle.googlecode.com/svn/wiki/images/FerrisWheels_thumb.png)](http://code.google.com/p/turboturtle/wiki/Screenshots#Ferris_Wheels) | [![](http://turboturtle.googlecode.com/svn/wiki/images/LeaningTree_thumb.png)](http://code.google.com/p/turboturtle/wiki/Screenshots#Leaning_Tree) |
|:------------------------------------------------------------------------------------------------------------------------------------------|:---------------------------------------------------------------------------------------------------------------------------------------------------|:------------------------------------------------------------------------------------------------------------------------------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------|:---------------------------------------------------------------------------------------------------------------------------------------------------|
| [![](http://turboturtle.googlecode.com/svn/wiki/images/Mandelbrot_thumb.png)](http://code.google.com/p/turboturtle/wiki/Screenshots#Mandelbrot) | [![](http://turboturtle.googlecode.com/svn/wiki/images/SpinningSquares_thumb.png)](http://code.google.com/p/turboturtle/wiki/Screenshots#Spinning_Squares) | [![](http://turboturtle.googlecode.com/svn/wiki/images/SpiralSquares_thumb.png)](http://code.google.com/p/turboturtle/wiki/Screenshots#Spiral_Squares) | [![](http://turboturtle.googlecode.com/svn/wiki/images/Spirograph_thumb.png)](http://code.google.com/p/turboturtle/wiki/Screenshots#Spirograph)      | [![](http://turboturtle.googlecode.com/svn/wiki/images/TreeGenerator_thumb.png)](http://code.google.com/p/turboturtle/wiki/Screenshots#Tree_Generator) |

<table align='center' border='0'><tr><td align='center'><a href='http://www.ringsurf.com/ring/logoring/'>Logo Users Ring</a><br><a href='http://www.ringsurf.com'>Powered By Ringsurf</a>
