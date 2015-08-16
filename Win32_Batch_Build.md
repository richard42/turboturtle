Win32Build.bat:
```
cl /O2 /Ox /I ".\SDL-1.2.13\include" /I ".\TurboTurtle-1.2-source" /MD /c TurboTurtle-1.2-source\wrapper_fontdata.cpp
cl /O2 /Ox /I ".\SDL-1.2.13\include" /I ".\TurboTurtle-1.2-source" /MD /c TurboTurtle-1.2-source\wrapper_main.cpp
cl /O2 /Ox /I ".\SDL-1.2.13\include" /I ".\TurboTurtle-1.2-source" /MD /c TurboTurtle-1.2-source\wrapper_opengl.cpp
cl /O2 /Ox /I ".\SDL-1.2.13\include" /I ".\TurboTurtle-1.2-source" /MD /c TurboTurtle-1.2-source\wrapper_pointtext.cpp
for %%F in (.\TurboTurtle-1.2-source\logocode\*.logo) do python .\TurboTurtle-1.2-source\turboturtle.py %%F %%F.cpp
for %%F in (.\TurboTurtle-1.2-source\logocode\*.cpp) do cl /O2 /Ox /I ".\SDL-1.2.13\include" /I ".\TurboTurtle-1.2-source" /MD /c %%F
del .\TurboTurtle-1.2-source\logocode\*.cpp
for %%F in (*.logo.obj) do link /SUBSYSTEM:CONSOLE /MACHINE:X86 /RELEASE .\SDL-1.2.13\lib\SDL.lib .\SDL-1.2.13\lib\SDLmain.lib %%F wrapper_fontdata.obj wrapper_main.obj wrapper_opengl.obj wrapper_pointtext.obj opengl32.lib
del *.obj
```