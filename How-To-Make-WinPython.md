# How to make Winpython-2016-02 of April 2016

This procedure may help You doing your own Winpython-201508 of December 2015 distribution in about 2 hours.
(multiply by 4, if you're taking the slow path)

### Changelog 
(v12, 2016-04-20 WinPython 2016-02):
- no more NSIS external module (NSIS usage reduced by half) nor patch
- the NSIS scripts are replaced by open .BAT and .VBS scripts


(v11, 2016-02-09 WinPython 2016-01):
- no choice but to include back pyreadline.exe (until Jupyter5, apparently)
- no changed in procedure, but note 'pip' integration improvement:
   . ".\script\upgrade_pip.bat" propose the exact procedure to upgrade pip and keep WinPython feature,
   . a WinPython-friendly fix will get into standard 'pip' https://github.com/pypa/pip/pull/3448
    

(v10, 2015-11-03):
- nearly all packages are in packages.srcreq
- no more packages in packages.src
- the build pick the packages in packages.srcreq according to provided requirements files.
- specific preparation for Python 3.5 (reading http://stevedower.id.au/blog/the-python-3-5-installer/#comment-241)
  . download from python.org the standard binary installer "python-3.5.1-amd64.exe" in d:\toto
  . D:\toto\python-3.5.1-amd64.exe TargetDir=D:\toto\winpython-3.5.1-amd64\python-3.5.1.amd64 /quiet  InstallAllUsers=0 Include_launcher=0 InstallLauncherAllUsers=0 Include_test=0  AssociateFiles=0 Shortcuts=0
  . zip result 'python-3.5.1.amd64' in basedir35\packages.win-amd64\python-3.5.1.amd64.zip
  . ATTENTION: UNINSTALL Python3.5.1 from your Windows system after !!!!!!!!!!!!


(v09, 2015-11-03):
- now, nearly all packages are in packages.srcreq
- the build pick these packages according to provide requirements files.

(v08, 2015-08-08):
- we now use gcc Compiler provided by mingwpy wheel (same author as mingw64-static: Carl Kleffner, much simpler integration: a wheel)
- we now use a dos batch script instead of runnin make.py interactively

(v07, 2015-03-01):
- due to issue with FlavorJulia on 64bit, it is suggested to remove \tools*\mingw32\bin\libopenblas.dll, unless you really use libopenblas under Python. (see end of thread https://groups.google.com/forum/#!topic/winpython/VkuOpynUT2U ) 
   
(v06, 2015-01-30):
- replace old mingw32 reference per mingw64-static

(v05, 2014-12-20):
- include the two Flavors made with winpython 2014-12 in the Directory https://sourceforge.net/projects/winpython/files/WinPython_Source/Do_It_Yourself/WinPython_2014-12/

(v04b, 2014-10-18b):
- winpython builder is to be used with a python 3.3+
- adding nsis-2.46-strlen_8192.zip patch  (to preserve existing %PATH% bigger than 1024 character)
- use rather an existing Winpython 64 bit version to build a new one
- how to do a flavor


### Procedure
This Procedure is a rewrite or complement of the original method created by Pierre Raybaut ([here](https://sourceforge.net/p/winpython/wiki/How%20To%20Make%20WinPython/))

It provides two optional big shortcuts over the original method :
- not downloading yourself a set of packages, one by one,
- not downloading yourself the additional tools.


*******************
**Step 0 (optional):**  Install a md5/sh1 checker
*******************
(duration ~ 10')

for example the one from microsoft : "fciv.exe":
- go to  http://support.microsoft.com/kb/841290
- drill down to the Installation part and click on 'download the File Checksum Integrity Verifier Utility package now')
- double-click on the  Windows-KB841290-x86-ENU.exe,
- you have now a fciv.exe utility to compute sha1 and md5 of files,
- also remember you have some online sites to check small files :
  - https://www.virustotal.com/fr/
  - http://virusscan.jotti.org/fr

MD5                              | SHA-1                                    | File
---------------------------------|------------------------------------------|------------------------------
58dc4df814685a165f58037499c89e76 | 99fb35d97a5ee0df703f0cdd02f2d787d6741f65 | windows-kb841290-x86-enu.exe

  - see its Readme
  - doing a small fciv_launcher.bat next to it may help: drag & drop the file to check over 'fciv_launcher.bat'

````
rem this is fciv_launcher.bat
"%~dp0fciv.exe" %1 -both>%1.hash.txt
notepad.exe %1.hash.txt
````

******************
**Step 1 (mandatory):** Install the complementary external tools for building Winpython
******************
(duration ~ 20')

optional : 
   - check these with https://www.virustotal.com (and http://virusscan.jotti.org when in doubts)
   - in mandatory_external_tools directory

mandatory : 
   - the python building module "https://github.com/winpython/winpython",
   - 7zip (to install or to re-take from official site)
   - nsis (2.46) + 1 external module  + the "8192 characters in PATH" patch

 ==> they are provided at https://sourceforge.net/projects/winpython/files/WinPython_Source/Do_It_Yourself/mandatory_to_install_tools/

 ==> or you can download them from their origin, as described below.


   - download (or use the one provided) and install 7zip :
     7z922.exe is the one I use
     (from http://sourceforge.net/projects/sevenzip/files/7-Zip/9.22/7z922.exe/download)

   - download (or use the one provided) and install Nullsoft Installer (nsis) :
     nsis-2.46-setup.exe is the one I use
     (from http://freefr.dl.sourceforge.net/project/nsis/NSIS%202/2.46/nsis-2.46-setup.exe)

 

MD5                              | SHA-1                                    | File
---------------------------------|------------------------------------------|------------------------------
5e02441c7f3fa4da4f4928a2d42a07c3 | 1a0f9ec81b39da809cdc9495166a2a1c9a79719c | nsis-2.46-setup.exe
441274c321383936860e845bd1eb4340 | 03c86e42464c6da82e0340acf807c88e3d1e40e0 | 7z922.exe


*******************
**Step 2 (mandatory):** Install a version of winpython (or a standard python) on your PC
*******************
(duration ~ 15')

- downloading for example winpython-3.4.3.4 (or using one you have)
- warning : Use a 64 bit winpython if you plan to create a 64 build with it
- download WinPython-64bit-3.4.3.4.exe from sourceforge.net (or github release tag)
- check its hash :


MD5                              | SHA-1                                    | Binary
---------------------------------|------------------------------------------|------------
e275934df30b0831cad1849efd609e4f | 07c3c29cf34a0f36b804685dd6d769921f95debc | winpython-64bit-3.4.3.4.exe
6a45b8d3e1a36e31d5526adecbf655a4 | fe28d0db8b84001cfc4bc5f45d87b63445942810 | winpython-32bit-3.4.3.4.exe
fb6c256442079099e0fec5b37c49ca64 | 224e5f754c3e49c20458b4c560034d9c331ee190 | winpython-64bit-3.3.5.0.exe
ccc8af61ae894a8fa052c49c8ecf2ad1 | df5280fb911ca7d1ad09bcb089a98693b14e566e | winpython-32bit-3.3.5.0.exe


- let suppose you placed it in 
     D:\WinPython-64bit-3.4.3.4 (or 'PC_WinPython_location')

*******************
**Step 3 (mandatory):**  
*******************
(duration ~ 10' if you get what is proposed here and build winpython3.4, 4 hours if your download yourself)

Prepare the 'root' directory hierarchy to build your distribution 

   - a root directory per major release is nice (or copy the old one elsewhere) :
     - D:\winpython , for this example

   - the a sub-directory according to your Python targets :
     - winpython\basedir27 (if you want to build for python 2.7)
     - winpython\basedir34 (if you want to build for python 3.4)
     - winpythonQt5\basedir34 (if you want to build a variant for python 3.4 with Qt5)
     - winpython\packages.srcreq (all optional packages, picked up by requirement files)

   - each basedir** subdirectory must contain the following subdirectories, for example
     - basedir34\packages.src
     - basedir34\packages.win32 (if you want to build for python 3.4 - 32bit)
     - basedir34\packages.win-amd64 (if you want to build for python 3.4 - 64bit)
     - build  (initially empty, will contain the Winpython build you're creating before it's made into an installer)
     - tools
     - tools.win32     (if you want to build for python 3.4 - 32bit)
     - tools.win-amd64 (if you want to build for python 3.4 - 64bit)

   ==> the typical contain of these directories is provided as .zip, as it was for winpython (after) ".1"
at https://sourceforge.net/projects/winpython/files/WinPython_Source/Do_It_Yourself/Winpython_2015-06/

   ==> unzip them "here", so you create the directory at the right level :  basedir34\packages.win32\python-3.4.4.msi , ..

   ==> slow path (or when you will build your own), download them yourself from :
         https://pypi.python.org/pypi
         http://www.lfd.uci.edu/~gohlke/pythonlibs/
         https://binstar.org/carlkl/mingwpy
         or other places

*******************
**Step 5 (optional):** Feeding tools, tools.win32, tools.win-amd64 yourself
*******************
(duration = 0' if you take them from your usual winpython, ~ 1 hour if you download yourself)

Since Winpython of 2015-08-09, we use mingwpy wheel for the compilation toolchain.
==> Download mingwpy0.1.0b3 (or better) wheels from https://binstar.org/carlkl/mingwpy/files
==> Manage it like any other wheel.

MD5                              | SHA-1                                    | Binary
---------------------------------|------------------------------------------|------------
b25141aaf75b2bc0532bfa6ae1f5664c | a5d3493f2acd7a5e0e7cdf15e84e22aa557cec1b | mingwpy-0.1.0b3-cp27-none-win_amd64.whl
1e06cbf74b9acd6fe2ba3f0815cdf436 | cdbbfa7a9eabbe8c2538b053bf17d315d2cf409c | mingwpy-0.1.0b3-cp27-none-win32.whl
2f85adc0a37fee0af938620b0418db7a | 337ff9ce348cf73dca0ee69b5be0a23e82b4b59c | mingwpy-0.1.0b3-cp34-none-win_amd64.whl
f067f48fcf685d0d6dd4587a0f4280fe | 80553ad13797e160dbcfe240a2e6ac002f366174 | mingwpy-0.1.0b3-cp34-none-win32.whl

*******************
**Step 4 (mandatory):** The building moment 
******************
(duration ~ 30')

   - unzip "winpython" source code (taken from github) to (for example) 
      d:\winpython-builder
     (for example from https://github.com/winpython/winpython/releases/tag/1.2.20150809)
     (so that, for example, you have a dos file in D:\winpython-builder\generate_winpython_distros34.bat)
   - edit 'generate_winpython_distros34.bat' :
     - set my_buildenv to the root directory of your existing Winpython, that will be used to build new ones
````
rem this replace running manually from spyder the make.py 
rem to launch from a winpython module 'make' directory 

set my_original_path=%path%
set my_buildenv=D:\WinPython-64bit-3.4.3.3_b0

set my_root_dir_for_builds=D:\Winpython
set my_python_target=34
set my_pyver=3.4
set my_release=2
set my_flavor=

set my_release_level=
set my_arch=64
set my_preclear_build_directory=Yes

set tmp_reqdir=%my_root_dir_for_builds%\basedir%my_python_target%
set my_requirements=%tmp_reqdir%\requirements.txt %tmp_reqdir%\requirements2.txt %tmp_reqdir%\requirements3.txt

set my_find_links=%tmp_reqdir%\packages.srcreq

set my_install_options=--no-index --pre --trusted-host=None
 
call %~dp0\generate_a_winpython_distro.bat
````

   - save it, double_click on it and wait about 40',
     - result :
       - a directory basedir34\build\WinPython-64bit-3.4.4.2 is created with your new Winpython in it (after 20')
       - a Winpython_installer will be create from it as basedir34\WinPython-64bit-3.4.4.2.exe (after 20' more)
     - when it works, start removing, upgrading, adding some packages, and do your own custom Winpython.


