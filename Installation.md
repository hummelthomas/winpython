# Installation

As WinPython is a portable distribution, the installer only copies compressed files to the specified destination directory. To *install* in terms of *register* your distribution in the system, see the section [Registration](#Registration) on this page.

# Settings

All installed Python packages store their settings in `[WINPYTHON_DIR]\settings` instead of a user profile directory (e.g. `C:\Users\username`), hence allowing to move your settings with your favorite distribution, in a portable way. This is the default behavior but it can be changed by simply removing the `[WINPYTHON_DIR]\settings` folder, forcing WinPython to use the user profile directory instead. 

# Registration

The WinPython Control Panel allows to *register* your WinPython distribution to Windows.

![Winpython Control Panel>Advanced>Register distribution](https://winpython.github.io/images/wpcp_register_2741.png)

Registering your WinPython installation will:

- associate file extensions `.py`, `.pyc` and .pyo to Python interpreter
- register Python icons in Windows explorer
- add context menu entries Edit with IDLE and Edit with Spyder for `.py` files
- register WinPython as a standard Python distribution in the registry (the same way as the standard Python Windows installers will do)


# Operating Systems

## Windows Vista, 7, 8 and 10

WinPython works fine in Windows **Vista**, **7**, **8** and **10** just by extracting it to your favorite place.

Older systems like Windows Server 2003 and Windows XP are not no longer supported. You may are able to run your programs, but IPython (and thus Spyder) is defintely broken, unless you apply the workaround described in the next section. As we don't test our releases on these platforms we cannot guarantee incompatibilites and unexpected behavior.

## Windows XP

Windows XP is not supported by Winpython and we don't recommend to run it nevertheless. If you really need to use Winpython on XP, you will get errors like `OSError: [WinError 127]"` and a `Procedure not found` at the end of the backtraces. This comes from the zmq library which depends on a DLL not existing in XP. There's a workaround described in [#17](https://github.com/winpython/winpython/issues/17):

> Transplant the working zmq lib. I took the current WinPython-3.3.5 installation, deleted the contents of "python-3.3.5\Lib\site-packages\zmq" and replaced it with the files of the same directory from WinPython 4.2013. Everthing works a treat now...