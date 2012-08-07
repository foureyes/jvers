##Overview:
##Rationale:
##Install Instructions:
##Verification Process:

XCode (Developer Tools)
=====
##Overview:
XCode includes Apple's IDE, XCode, and various developer tools, such as gcc.

##Rationale:
Having gcc will allow installation of Python libraries that require compilation (for example, the Python PostgreSQL adapter, needs to be compiled).  Having gcc will allow customized compilation of libraries and applications, making it possible to install these libraries and applications into specific locations.  As a result, administrative access may not be necessary for some future installations, and these future installations would be isolated to the current user.

##Install Instructions
Install using the Snow Leopard DVD.  Newer versions of XCode may not be compatible with Snow Leopard.  However, older versions are not available through the app store unless you're part of the developer program.

##Verification Process:
git
=====
##Overview:
git is an open source distributed version control system.

##Rationale:
Using a source code management tool is required for version control/back up and collaboration. 

##Install Instructions:
1. Follow the links in http://code.google.com/p/git-osx-installer/ to download the installer.
2. Unpack the .dmg and run the .pkg.
3. The default options should be sufficient.
4. You will need admin rights to install.

##Verification Process:
1. If not __user__, log in __as user__.
2. Open terminal.
3. `which git` # should return location of git binary.
4. `git --version` # should print out git version (1.7.x most likely).

Python 3
=====
##Overview:
The most recent stable release of Python 3 (currently 3.2).

##Rationale:
Python 3 has improved upon and cleaned up some inconsistencies in Python 2.x.

##Install Instructions:
1. Download python 3: http://www.python.org/ftp/python/3.2.3/python-3.2.3-macosx10.6.dmg.

##Verification Process:
1. `which python3` # should give you something like /usr/local/bin/python3.

Distribute
=====
##Overview:
Distribute allows the installation of packages and modules for Python 3.

##Rationale:
A package manager must be installed for the new version of Python that's been dropped into the system.  Distribute will bring in a Python 3 compatible version of easy_install.

##Install Instructions:
1.  See the installation instructions for distribute here: http://pypi.python.org/pypi/distribute#installation-instructions
2. `curl -O http://python-distribute.org/distribute_setup.py` # get the install script
3. `sudo python3 distribute_setup.py` # run the install script with a user that has administrative rights / sudo... notice that you're using the python3 binary!

##Verification Process:
1. `ls -l /Library/Frameworks/Python.framework/Versions/3.2/bin/easy_install-3.2` to ensure that easy_install for Python 3 is present

Create a Custom .profile
=====
##Overview:
We want to include all of the Python 3 related binaries into our path.

##Rationale:
It's cumbersome to type the whole path to Python 3 and its related binaries.

##Install Instructions:
1. Create or open a .profile in your user's home directory.
2. Append the directory that includes the 3.2 binaries to your PATH by dropping this in the top of your .profile: `export PATH=$PATH:/Library/Frameworks/Python.framework/Versions/3.2/bin`
3. Make sure that it's added to the end to prevent trampling on the binaries in /usr/bin (like easy_install or python)

##Verification Process:
tests-Mac-Pro:~ test$ which python
/usr/bin/python
tests-Mac-Pro:~ test$ which easy_install
/usr/bin/easy_install
tests-Mac-Pro:~ test$ easy_install
easy_install      easy_install-2.5  easy_install-2.6  easy_install-3.2
tests-Mac-Pro:~ test$ which easy_install-3.2
/Library/Frameworks/Python.framework/Versions/3.2/bin/easy_install-3.2

pip
=====
##Overview:
pip is a modern package management system for Python.

##Rationale:
pip will be used to install Python libraries.

##Install Instructions:
1. Open terminal
2. `sudo easy_install-3.2 pip`

## Verification Process:
1. If not __user__, log in __as user__
2. In terminal...
3. `pip --version` # should return pip version
4. May need to open new terminal for any environment variables to be set appropriately (for example, pip may not be in your path yet)?

virtualenv and virtualenvwrapper
=====
##Overview:
virtualenv and virtualenvwrapper

##Rationale:
These tools will allow users to install Python libraries into "virtual" Python environments.  These will be isolated from the rest of the system and the Python libraries used for these environments will be located in the user's home directory.  Admin rights will not be necessary to manipulate a user's virtualenvs.

##Install Instructions:
1. Open terminal
2. `sudo pip install virtualenv`
3. `sudo pip install virtualenvwrapper`
The following commands can be run by the user, so they are not required.  For the sake of completeness (and convenience for the class)....
1. __As user__ follow the instructions in step "4. Configuring .bashrc to enable virtualenvwrapper commands" of this article: http://blog.praveengollakota.com/47430655

## Verification Process:
1. In terminal...
2. `which mkvirtualenv` 
3. May need to open new terminal for any environment variables to be set appropriately (for example, pip may not be in your path yet)?

1. Put the following lines ~/.profile
VIRTUALENVWRAPPER_PYTHON=/Library/Frameworks/Python.framework/Versions/3.2/bin/python3
source /Library/Frameworks/Python.framework/Versions/3.2/bin/virtualenvwrapper.sh
2. source ~/.profile
virtualenvwrapper.user_scripts creating /Users/test/.virtualenvs/initialize
virtualenvwrapper.user_scripts creating /Users/test/.virtualenvs/premkvirtualenv
virtualenvwrapper.user_scripts creating /Users/test/.virtualenvs/postmkvirtualenv
virtualenvwrapper.user_scripts creating /Users/test/.virtualenvs/prermvirtualenv
virtualenvwrapper.user_scripts creating /Users/test/.virtualenvs/postrmvirtualenv
virtualenvwrapper.user_scripts creating /Users/test/.virtualenvs/predeactivate
virtualenvwrapper.user_scripts creating /Users/test/.virtualenvs/postdeactivate
virtualenvwrapper.user_scripts creating /Users/test/.virtualenvs/preactivate
virtualenvwrapper.user_scripts creating /Users/test/.virtualenvs/postactivate
virtualenvwrapper.user_scripts creating /Users/test/.virtualenvs/get_env_details
virtualenvwrapper.user_scripts creating /Users/test/.virtualenvs/premkproject
virtualenvwrapper.user_scripts creating /Users/test/.virtualenvs/postmkproject
virtualenvwrapper.user_scripts creating /Users/test/.virtualenvs/prermproject
virtualenvwrapper.user_scripts creating /Users/test/.virtualenvs/postrmproject

3. mkvirtualenv mtec2002
New python executable in mtec2002/bin/python
Could not call mach_o_change: expected an object with the buffer interface. Trying to call install_name_tool instead.
Installing distribute...................................................................................................................................................................................................................................................................................................................................................................done.
Installing pip................done.

4. Add this to ~/.profile
workon mtec2002

* install yolk to list packages
sudo /Library/Frameworks/Python.framework/Versions/3.2/bin/easy_install-3.2 yolk


   27  sudo 2to3 /Library/Frameworks/Python.framework/Versions/3.2/lib/python3.2/site-packages/yolk-0.4.3-py3.2.egg/yolk/cli.py 
   28  2to3 --help
   29  sudo 2to3 -w /Library/Frameworks/Python.framework/Versions/3.2/lib/python3.2/site-packages/yolk-0.4.3-py3.2.egg/yolk/cli.py 
   30  /Library/Frameworks/Python.framework/Versions/3.2/bin/yolk -l 
   31  sudo 2to3 -w /Library/Frameworks/Python.framework/Versions/3.2/lib/python3.2/site-packages/yolk-0.4.3-py3.2.egg/yolk/pypi.py 
   32  /Library/Frameworks/Python.framework/Versions/3.2/bin/yolk -l 
   33  sudo 2to3 -w /Library/Frameworks/Python.framework/Versions/3.2/lib/python3.2/site-packages/yolk-0.4.3-py3.2.egg/yolk/utils.py 
   34  /Library/Frameworks/Python.framework/Versions/3.2/bin/yolk -l 
   35  sudo 2to3 -w /Library/Frameworks/Python.framework/Versions/3.2/lib/python3.2/site-packages/yolk-0.4.3-py3.2.egg/yolk/setuptools_support.py 
   36  /Library/Frameworks/Python.framework/Versions/3.2/bin/yolk -l 
   37  sudo 2to3 -w /Library/Frameworks/Python.framework/Versions/3.2/lib/python3.2/site-packages/yolk-0.4.3-py3.2.egg/yolk/__init__.py 
   38  /Library/Frameworks/Python.framework/Versions/3.2/bin/yolk -l 
   39  sudo 2to3 -w /Library/Frameworks/Python.framework/Versions/3.2/lib/python3.2/site-packages/yolk-0.4.3-py3.2.egg/yolk/plugins/__init__.py 
   40  /Library/Frameworks/Python.framework/Versions/3.2/bin/yolk -l 

pip install bottle beautifulsoup4
