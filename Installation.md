# Requirements

As some packages were built using Microsoft Visual Studio, you may have to install one of the following redistribution packages for WinPython 2.7 only:

- WinPython 2.7 32bit: [Microsoft Visual C++ 2008 Redistributable Package (x86)](http://www.microsoft.com/en-us/download/details.aspx?id=29)
- WinPython 2.7 64bit: [Microsoft Visual C++ 2008 Redistributable Package (x64)](http://www.microsoft.com/en-us/download/details.aspx?id=15336)
- WinPython 3.5 (on non-Windows 10 platforms): [Microsoft Visual C++ Redistributable for Visual Studio 2015](https://www.microsoft.com/en-us/download/details.aspx?id=49984)

# Installation

As WinPython is a portable distribution, the installer only copies compressed files to the specified destination directory. To *install* in terms of *register* your distribution in the system, see the section [Registration](#Registration) on this page.

# Settings

All installed Python packages store their settings in `[WINPYTHON_DIR]\settings` instead of a user profile directory (e.g. `C:\Users\username`), hence allowing to move your settings with your favorite distribution, in a portable way. This is the default behavior but it can be changed by simply removing the `[WINPYTHON_DIR]\settings` folder, forcing WinPython to use the user profile directory instead. 

# Registration

The WinPython Control Panel allows to *register* your WinPython distribution to Windows.

![Winpython Control Panel>Advanced>Register distribution](https://winpython.github.io/images/wpcp_register_2741.png)

## Unregistration
> Registering your WinPython installation will:

> - associate file extensions `.py`, `.pyc` and .pyo to Python interpreter
> - register Python icons in Windows explorer
> - add context menu entries Edit with IDLE and Edit with Spyder for `.py` files
> - register WinPython as a standard Python distribution in the registry (the same way as the standard Python Windows installers will do)

> ---------------------------
> Register distribution
> ---------------------------
> This will associate file extensions, icons and Windows explorer's context menu entries ('Edit with IDLE', ...) with selected Python distribution in Windows registry. <br>Shortcuts for all WinPython launchers will be installed in <i>WinPython</i> Start menu group (replacing existing shortcuts).<br>If <i>pywin32</i> is installed (it should be on any WinPython distribution), the Python ActiveX Scripting client will also be registered.<br><br><u>Warning</u>: the only way to undo this change is to register another Python distribution to Windows registry.<br><br><u>Note</u>: these actions are exactly the same as those performed when installing Python with the official installer for Windows.<br><br>Do you want to continue?
> ---------------------------
> &Yes   &No   
> ---------------------------


# Operating Systems

## Windows Vista, 7, 8 and 10

WinPython works fine in Windows **7**, **8** and **10** just by extracting it to your favorite place.

Older systems like Windows Server 2003, Windows XP and Windows Vista are not no longer supported. You may are able to run your programs, but IPython (and thus Spyder) is defintely broken, unless you apply the workaround described in the next section. As we don't test our releases on these platforms we cannot guarantee incompatibilites and unexpected behavior.

## Windows XP

Windows XP is not supported by Winpython and we don't recommend to run it nevertheless. If you really need to use Winpython on XP, you will get errors like `OSError: [WinError 127]"` and a `Procedure not found` at the end of the backtraces. This comes from the zmq library which depends on a DLL not existing in XP. There's a workaround described in [#17](https://github.com/winpython/winpython/issues/17):

> Transplant the working zmq lib. I took the current WinPython-3.3.5 installation, deleted the contents of "python-3.3.5\Lib\site-packages\zmq" and replaced it with the files of the same directory from WinPython 4.2013. Everything works a treat now...