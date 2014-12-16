## How to make Winpython of October 2014 (Rewrite in progress)

This procedure may help You doing your own Winpython 'October 2014' distribution in about 2 hours.
(multiply by 4, if you're taking the slow path)

### Changelog 
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

MD5 | SHA-1 | File
----|-------|-----
58dc4df814685a165f58037499c89e76 | 99fb35d97a5ee0df703f0cdd02f2d787d6741f65|windows-kb841290-x86-enu.exe

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

 ==> they are provided at https://sourceforge.net/projects/stonebig.u/files/Do_It_Yourself/mandatory_to_install_tools

 ==> or you can download them from their origin, as described below.


   - download (or use the one provided) and install 7zip :
     7z922.exe is the one I use
     (from http://sourceforge.net/projects/sevenzip/files/7-Zip/9.22/7z922.exe/download)

   - download (or use the one provided) and install Nullsoft Installer (nsis) :
     nsis-2.46-setup.exe is the one I use
     (from http://freefr.dl.sourceforge.net/project/nsis/NSIS%202/2.46/nsis-2.46-setup.exe)

   - download (or use the one provided) and install textReplace plugin for nsis :
     (from http://nsis.sourceforge.net/mediawiki/images/e/eb/Textreplace.zip)
 
2014-10-18 complement
   - download (or use the one provided) and unzip "strlen8192" patch for nsis :
     (http://freefr.dl.sourceforge.net/project/nsis/NSIS%202/2.46/nsis-2.46-strlen_8192.zip
     then, manually replace one by one each patched 7 files in the default nsis 

         C:\Program Files (x86)\NSIS\makensis.exe

         C:\Program Files (x86)\NSIS\Stubs\bzip2 bzip2_solid lzma_solid lzma zlib_solid zlib 

MD5 | SHA-1 | File
----|-------|-----
5e02441c7f3fa4da4f4928a2d42a07c3 | 1a0f9ec81b39da809cdc9495166a2a1c9a79719c | nsis-2.46-setup.exe
2347d68b9579525f6fbcbdb4d93c596f | 8ecc9deb4f233c6622f90ed30afacd890ec56ad0 | textreplace.zip
441274c321383936860e845bd1eb4340 | 03c86e42464c6da82e0340acf807c88e3d1e40e0 | 7z922.exe
604c0c2c7902c5b6a1f89ab0b1f7a87c | 1534fe63749009472c82f6bf960a7da7201dda06 | nsis-2.46-strlen_8192.zip


*******************
**Step 2 (mandatory):** Install a version of winpython (or a standard python) on your PC
*******************
(duration ~ 15')

- downloading for example winpython3.3.5.0 (or using one you have)
- warning : Use a 64 bit winpython if you plan to create a 64 build with it
- download WinPython-64bit-3.3.5.0.exe from sourceforge.net
- check its hash :

MD5 | SHA-1 | File
----|-------|-----
fb6c256442079099e0fec5b37c49ca64 | 224e5f754c3e49c20458b4c560034d9c331ee190 | winpython-64bit-3.3.5.0.exe
ccc8af61ae894a8fa052c49c8ecf2ad1 | df5280fb911ca7d1ad09bcb089a98693b14e566e | winpython-32bit-3.3.5.0.exe


- let suppose you placed it in 
     D:\WinPython-64bit-3.3.5.0 (or 'PC_WinPython_location')

*******************
**Step 3 (mandatory):**  
*******************
(duration ~ 10' if you get what is proposed here and build winpython3.4, 4 hours if your download yourself)

Prepare the 'root' directory hierarchy to build your distribution 

   - a root directory per major release is nice (or copy the old one elsewhere) :
     - D:\winpython , for this example

   - the a sub-directory according to your Python targets :
     - winpython\basedir27 (if you want to build for python 2.7)
     - winpython\basedir33 (if you want to build for python 3.3)
     - winpython\basedir34 (if you want to build for python 3.4)

   - each basedir** subdirectory must contain the following subdirectories, for example
     - basedir34\packages.src
     - basedir34\packages.win32 (if you want to build for python 3.4 - 32bit)
     - basedir34\packages.win-amd64 (if you want to build for python 3.4 - 64bit)
     - build  (initially empty, will contain the Winpython build you're creating before it's made into an installer)
     - tools
     - tools.win32     (if you want to build for python 3.4 - 32bit)
     - tools.win-amd64 (if you want to build for python 3.4 - 64bit)

   ==> the typical contain of these directories is provided as .zip, as it was for winpython (after) ".1"
at https://sourceforge.net/projects/stonebig.u/files/Do_It_Yourself/Winpython_2014-10/

   ==> unzip them "here", so you create the directory at the right level :  basedir34\packages.win32\python-3.4.1.msi , ..

   ==> slow path (or when you will build your own), download them yourself from :
         https://pypi.python.org/pypi
         http://www.lfd.uci.edu/~gohlke/pythonlibs/
         or other places

*******************
**Step 5 (optional):** Feeding tools, tools.win32, tools.win-amd64 yourself
*******************
(duration = 0' if you take them from your usual winpython, ~ 1 hour if you download yourself)

- in basedir34\tools, put tools ok for 32 bit and 64 bit installations :
  copy the "TortoiseHg" from your given Winpython
   (or take the one provided)

- in basedir34\tools.win32, put tools ok for 32 bit installations :
  if you want MinGW32 in our portable distribution :
     - go to https://sourceforge.net/projects/mingw/
     - download mingw-get-setup.exe


MD5 | SHA-1 | File
----|-------|-----
92d905bdfe13c798a2cda2bbacdad932 | 66f1355f16ac1e328243e877880eb6e45e8b30e2 | mingw-get-setup.exe
     - open it,
     - install mingw-developer-tool,
     - mingw32-base
     - mingw32-gcc-fortran,
     - mingw32-gcc-g++,
     - copy the result C:\MinGW\mingw32 in d:\winpython\basedir34\tools.win32\mingw32 

- in basedir34\tools.win-amd64 :
     - go to https://github.com/numpy/numpy/wiki/Mingw-static-toolchain
     - download mingw64static-2014-07.7z and unzip it there

MD5 | SHA-1 | File
----|-------|-----
3879839c7f1e89962fb8ee1da66e5f67 | a15b1b74381423d436b6f95bf25b00601756ddfd | mingw64static-2014-07ter.7z


*******************
**Step 4 (mandatory):** The building moment 
******************
(duration ~ 30')

   - unzip "winpython" source code (taken from github) to (for example) 
      d:\winpython-builder
     (for example from https://github.com/winpython/winpython/releases/tag/1.0.20141018)
     (so that, for example, you have the make file in D:\winpython-builder\make.py)
   - open your standard python (or winpython installation)
   - open with it your  D:\winpython-builder\make.py :
     - uncomment in the final 12 lines the build you want to make, (#) comment the others
     - check and remove previous build-created build\winpython** sub-directories
        (there should be none, until first build attempt)
     - run make.py,
     - wait (about 30')
     - result :
       - Winpython_installer will appear as basedir34\WinPython-32bit-3.4.2.1.exe 
       - a directory basedir34\build\WinPython-32bit-3.4.2.1 is created 
            (to remove before re-launching a build)
     - when it works, start removing, upgrading, adding some packages, and do your own custom Winpython.


*******************
**Step 5 (flavors):** Creating a custom/special Winpython version with additional packages
******************
Let suppose you want to create a MTSW (Minning-the-social-web) edition in python 3.4
   - create a sub-directory 
     - basedir34\Flavor_MTSW
   - add sub-directories to receive your complements :
     - Flavor_MTSW\packages.src
     - Flavor_MTSW\packages.win-amd64
     - Flavor_MTSW\tools
   - change the make.py last line by
````
make_all(1, '', pyver='3.4', rootdir=r'D:\Winpython',
              verbose=False, archis=(64, ), flavor='Flavor_MTSW')
````

