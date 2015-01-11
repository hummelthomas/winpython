#### Ipython Notebook issues

For example:
````
When starting the IPython Notebook everything seems OK. I can open notebooks and create new notebooks.
However, I can not run them because the cell shows:
In [*]:
Instead of:
In [1]:
````
Issues are of two kinds:
- incompatible browser: Internet Explorer 8 and 9 are not working well
  => Chrome, Firefox, or Internet Explorer 10 (or more) are suggested.

- Anti-virus or Firewall settings:
  some Free Antivirus/Firewalls are too restrictive. If you have “ZoneAlarm  Extreme Security”, this post my be helpfull https://groups.google.com/forum/#!topic/winpython/sOanTThQ-os

#### IDLE icon issues
If you don't have the IDLE icon, you are probably using an old WinPython version. 
- Solution1: download the missing icon corresponding to your winpython version from here, and place it next to the `Spyder.exe` icon.
http://sourceforge.net/projects/stonebig.u/files/Icons_for_Winpython

- Solution2:  click on icon `WinPython Command Prompt.exe` then type
````
  python lib\idlelib\idle.py
````

- Solution3: click on icon `Spyder.exe`, then type on the bottom right Python console
````
import os;runfile(os.environ["WINPYDIR"]+r"\lib\idlelib\idle.py")
````
