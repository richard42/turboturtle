## Version ##
This Readme file reflects TurboTurtle version 1.0.

## Command-line Options ##
The following command-line options may be passed to any TurboTurtle program to control the program operation.

| --resolution **xres** **yres** | Without the --fullscreen option, this sets the window size to **xres** by **yres** (normally 512x512).  With the --fullscreen option, this sets the fullscren resolution |
|:-------------------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| --fullscreen                   | Force the TurboTurtle program to use a fullscreen video mode                                                                                                             |
| --vsync                        | Synchronize the frame updates with the vertical retrace of your display device.  This gives the most smooth animation with no tearing.                                   |

## Compiling Demo Programs ##

### Linux ###
To compile a demo program, use the _runlogo.sh_ script included with the TurboTurtle source code.  Go to a command prompt and change to the directory where you unzipped the TurboTurtle source code.  Build a demo program by running "./runlogo.sh logocode/**program\_name**.logo", where **program\_name** is one of the included demo files such as DragonCurve Fern or Spirograph.  This will create an executable file in the current directory named **program\_name**.  To run it in fullscreen mode, type "./**program\_name** --fullscreen".  Press escape to exit the logo program.

### Windows ###
The Windows demo pack was built with the following tools:
  * [SDL v1.2.13 development libraries](http://www.libsdl.org/release/SDL-devel-1.2.13-VC8.zip) from the [SDL 1.2 download page](http://www.libsdl.org/download-1.2.php)
  * [Python 2.5.4](http://www.python.org/ftp/python/2.5.4/python-2.5.4.msi) from the [Python download page](http://www.python.org/download/)
  * Visual Studio .NET 2005
    * If you use a different version of Visual Studio, make sure that you get the compatible version of the SDL development libraries

To build the demo Logo programs under Windows, install Python and Visual Studio and do the following:
  1. Create a new directory on the desktop (or anywhere you would like) to hold the Logo programs
  1. Unzip the SDL development libraries into the new directory
    * This should create a folder called SDL-1.2.13
  1. Copy the SDL.dll library from the SDL-1.2.13\lib folder into the new directory
  1. Unzip the `TurboTurtle-1.2-source.tar.gz` package into the new directory
    * You may need to install Cygwin or WinRAR to unzip the .tar.gz file
    * This should create a folder called TurboTurtle-1.2-source
  1. Copy this [Windows Batch File](Win32_Batch_Build.md) into the new directory
  1. Start Visual Studio and open a VS command prompt (by clicking the <u>Visual Studio 2005 Command Prompt</u> option under the Tools menu)
  1. CD to the new directory containing the SDL and TurboTurtle folders
  1. Run the batch file to build all the Logo programs

## Compiling Your Own Programs ##
You can modify the demo logo files or create your own Logo programs from scratch and compile them with TurboTurtle.  Simply use the _runlogo.sh_ script in the TurboTurtle directory to build them.  The Logo source code can reside anywhere but the _runlogo.sh_ script must be run from the main TurboTurtle directory which contains the wrapper code.  The executable will be placed in the TurboTurtle directory.  Since the compiled Logo programs are so small (usually around 40-50KB) you can easily email them to friends, but to comply with the GPL license you must also send them the Logo source code.