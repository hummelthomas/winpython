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

#### switching between Visual Studio and Mingwpy as C compiler
Two scripts allow you to switch of default compiler:
- winpython-xxbit-x.x.x.x\scripts\make_cython_use_vc.bat = to switch to Visual Studio Compiler 
- winpython-xxbit-x.x.x.x\scripts\make_cython_use_mingw.bat = to switch to mingw Compiler
