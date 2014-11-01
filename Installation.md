_Wiki under construction_

Also see the old wiki page at the [outdated project on sourceforge](http://sourceforge.net/p/winpython/wiki/Installation/).

## Windows Vista, 7 and 8

Winpython works fine in Windows **Vista**, **7** and **8** just by extracting it to your favorite place.

Older systems like Windows Server 2003 and Windows XP are not no longer supported. You may are able to run your programs, but Ipython (and thus Spyder) is defintely broken, unless you apply the workaround described in the next section. As we don't test our releases on these platforms we cannot guarantee incompatibilites and unexpected behavior.

## Windows XP

Windows XP is not supported by Winpython and we don't recommend to run it nevertheless. If you really need to use Winpython on XP, you will get errors like `OSError: [WinError 127]"` and a `Procedure not found` at the end of the backtraces. This comes from the zmq library which depends on a DLL not existing in XP. There's a workaround described in [#17](https://github.com/winpython/winpython/issues/17):

> Transplant the working zmq lib. I took the current WinPython-3.3.5 installation, deleted the contents of "python-3.3.5\Lib\site-packages\zmq" and replaced it with the files of the same directory from WinPython 4.2013. Everthing works a treat now...