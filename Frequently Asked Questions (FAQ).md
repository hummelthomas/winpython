#### Ipython Notebook doesn't work well

When starting the IPython Notebook everything seems OK. I can open notebooks and create new notebooks. However, I can not run them because the cell shows:
```python
In [*]:
```
instead of
```python
In [1]:
```
The issues are of two kinds:
- Incompatible browser: Internet Explorer 8 and 9 are not working well. Chrome, Firefox, or Internet Explorer 10 (or more) are recommended.
- Anti-virus or Firewall settings: Some Antivirus/Firewalls are too restrictive. If you have “ZoneAlarm  Extreme Security”, this post at the mailinglist might be helpfull: [IPython Notebook - In [*]: instead of In [1]:](https://groups.google.com/forum/#!topic/winpython/sOanTThQ-os)

#### no 'IDLE' icon !
If you don't have the IDLE icon, you are probably using an old WinPython version. 
- Solution1: download the missing icon corresponding to your winpython version from [Icons for Winpython](http://sourceforge.net/projects/stonebig.u/files/Icons_for_Winpython), and place it next to the `Spyder.exe` icon.

- Solution2:  click on icon `WinPython Command Prompt.exe` then type in:
````
python lib\idlelib\idle.py
````

- Solution3: click on icon `Spyder.exe`, then type on the bottom right Python console
````
import os; runfile(os.environ["WINPYDIR"]+r"\lib\idlelib\idle.py")
````