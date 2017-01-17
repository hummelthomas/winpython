## Key features

WinPython is a portable distribution of Python. In other words, even if it provides a working Python environment, WinPython does **not** install Python on your machine.

To install package on Winpython:
- either launch "WinPython Command Prompt" and use the standard PIP Python package manager,
- either download a packages from pypi.io or http://www.lfd.uci.edu/~gohlke/pythonlibs/ , and install them via the graphical WinPython Package Manager "WinPython Control Panel".

The WinPython Package Manager (WPPM) may be removed in the future, when "PIP" will get a standard Graphic User Interface. , a Python program handling package managing tasks (install, uninstall or upgrade packages) for a portable Python distribution.

## WPPM currently supports the following Python package formats:
* [Standard PIP package](https://pypi.org/) -- ** .whl, .zip, .tar.gz**
* (soon deprecated) [Standard executable installers]: -- ** .exe files ** (filename has the form: foo-1.0.win32-py2.7.exe)


## Get Python packages

The main website for finding and downloading Python packages is obviously [PyPI](http://pypi.python.org/pypi) , the Python Package Index.

Please note that Christoph Gohlke's [Unofficial Windows Binaries for Python Extension Packages](http://www.lfd.uci.edu/~gohlke/pythonlibs) provides tons of ready-to-install distutils packages.
WPPM GUI frontend

WPPM has a GUI frontend which is known as the [WinPython Control Panel](https://github.com/winpython/winpython/wiki/Winpython-Control-Panel).


## One (optional) Exception: PIP Package itself
to update PIP package itself and keep WinPython as a movable directory:
- launch Winpython provided "scripts\upgrade_pip.bat"
- or , after PIP upgrade, launch "scripts\make_winpython_movable.bat"

if you do a standard PIP upgrade (or launch "scripts\make_winpython_fix.bat"), all is good as long as you don't move the WinPython directory

***
Old wiki page: http://sourceforge.net/p/winpython/wiki/WPPM/