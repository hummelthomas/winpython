To install python packages that are not included in Winpython, you can install easily.

# Precompiled Packages

For packages that need to be compiled, download the binary from [Gohlke's Unoffical Windows Binaries for Python Extension Packages](http://www.lfd.uci.edu/~gohlke/pythonlibs/), who maintains a huge list of precompiled packages. Otherwise you have to compile them yourself (see the package for details).
Then, select the downloaded package via *Winpython Package Manager* (WPPM) (in your Winpython directory) and install it.

Instead of using the WPPM you can execute the binary directly, if you've registered your installation in your system.

# Other packages

Using the *Winpython Command Prompt* you are able to use [*pip*](https://pip.readthedocs.org/en/latest/) directly to install packages from [PyPI](http://pypi.python.org/) for example:

```bash
pip install flake8
```

![](https://imgur.com/pXATvsc)

It is also possible to open any downloaded packages (usually `.tar.gz` files containing the Python-files) in the WPPM to install them.