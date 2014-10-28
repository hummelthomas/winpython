_Wiki under construction_

Winpython works fine in Windows Vista, 7 and XP just by extracting it to your favorite place.

## Windows XP

Windows XP is not supported by Winpython and we don't recommend to run it nevertheless. If you really need to use Winpython on XP, you will get errors like `OSError: [WinError 127]"` and a `Procedure not found` at the end of the backtraces. This comes from the zmq library which depends on a DLL not existing in XP. There's a workaround described in [#17](https://github.com/winpython/winpython/issues/17):

> Transplant the working zmq lib. I took the current WinPython-3.3.5 installation, deleted the contents of "python-3.3.5\Lib\site-packages\zmq" and replaced it with the files of the same directory from WinPython 4.2013. Everthing works a treat now...