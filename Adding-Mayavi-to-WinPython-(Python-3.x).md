This wiki item can be regarded as a case study: your mileage may vary. Please feel free to formalize this entry to a more prescriptive form.

The goal was to install the Enthought Mayavi 3D graphics and visualization package, with its newly added Python 3.x support, in an installation of WinPython 3.x. The necessary libraries are over 30 Mb in size, so for now it is advisable to have a means to install this package that is independent of the main WinPython distribution.

OS: Windows 8.1 64-bit
Distribution: WinPython 3.5.2.3 64-bit (QT4)

**Procedure**
Downloaded the appropriate wheels from Christophe Gohlke's site (first installing VTK, traits, traitsui and a few other ETS packages, just to be sure, then finally mayavi 4.5.0 itself). I dragged and dropped the wheels into the WinPython Control Panel. Downloaded and ran a test program from the Mayavi website to make interactive dialogs. The program worked perfectly.

**Notes**
There was a small error message to the console: "libpng warning: iCCP: known incorrect sRGB profile", but the interactive program seemed to work OK.


