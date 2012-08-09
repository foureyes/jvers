---
layout: no-frills
---
XCode (Developer Tools)
=====
##Overview:
XCode includes Apple's IDE, XCode, and various developer tools, such as gcc.

##Rationale:
Having gcc will allow installation of Python libraries that require compilation (for example, the Python PostgreSQL adapter needs to be compiled).  It will allow customized compilation of libraries and applications, making it possible to install these libraries and applications into specific locations.  As a result, administrative access may not be necessary for some future installations, and these future installations would be isolated to the current user.

##Install Instructions
Install using the Snow Leopard DVD.  Newer versions of XCode for Snow Leopard may no longer be available unless you're registered as an Apple Developer .  However, older versions are not available through the app store unless you're part of the developer program.

##Verification Process:
In older version of XCode, you get gcc... so `which gcc` should give you something like: `/usr/bin/gcc`

git
=====
##Overview:
git is an open source distributed version control system.

##Rationale:
Using a source code management tool is required for version control/back up and collaboration. 

##Install Instructions:
1. Download git here: http://git-scm.com/download/mac
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
As of August, 2012, the most recent stable release of Python 3 is 3.2.

##Install Instructions:
1. Download Python 3: http://www.python.org/ftp/python/3.2.3/python-3.2.3-macosx10.6.dmg.
2. Unpack and run the installer.  The default options should be sufficient.

##Verification Process:
1. If not __user__, log in __as user__.
2. In terminal, `which python3` # should give you something like /usr/local/bin/python3.

Distribute
=====
##Overview:
Distribute allows the installation of packages and modules for Python 3.

##Rationale:
A package manager must be installed for the new version of Python that's been added to the system.  Distribute will bring in a Python 3 compatible version of easy_install.

##Install Instructions:
For reference, the distribute docs have installation instructions here: http://pypi.python.org/pypi/distribute#installation-instructions.
1. If not __user__, log in __as user__.
2. In terminal, `curl -O http://python-distribute.org/distribute_setup.py` # get the install script
3. In terminal, `sudo python3 distribute_setup.py` # run the install script with a user that has administrative rights / sudo... notice that you're using the python3 binary!

##Verification Process:
1. If not __user__, log in __as user__.
2. In terminal, `ls -l /Library/Frameworks/Python.framework/Versions/3.2/bin/easy_install-3.2` to ensure that easy_install for Python 3 is present

Create a Custom .profile
=====
##Overview:
We want to add all of the Python 3 related binaries to our path.

##Rationale:
It's cumbersome to type the whole path to Python 3 and its related binaries.

##Install Instructions:
1. If not __user__, log in __as user__.
2. Create or open a .profile in your user's home directory.
3. Append the directory that includes the 3.2 binaries to your PATH by dropping this in the top of your .profile: `export PATH=$PATH:/Library/Frameworks/Python.framework/Versions/3.2/bin`
4. Make sure that it's added to the end to prevent trampling on the binaries in /usr/bin (like easy_install or python)

##Verification Process:
1. If not __user__, log in __as user__.  Open terminal, and...
2. `which python` # should still return `/usr/bin/python`
3. `which easy_install` # should still return `/usr/bin/easy_install`
4. `which easy_install-3.2` # should now give /Library/Frameworks/Python.framework/Versions/3.2/bin/easy_install-3.2

pip
=====
##Overview:
pip is a modern package management system for Python.

##Rationale:
pip will be used to install Python libraries.

##Install Instructions:
1. If not __user__, log in __as user__
2. Open terminal
3. `sudo easy_install-3.2 pip`

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
###Install packages
1. Open terminal
2. `sudo pip install virtualenv`
3. `sudo pip install virtualenvwrapper`

###Configure virtualenvwrapper and setup .profile
<ol>
<li>Put the following lines ~/.profile
<code>
VIRTUALENVWRAPPER_PYTHON=/Library/Frameworks/Python.framework/Versions/3.2/bin/python3
source /Library/Frameworks/Python.framework/Versions/3.2/bin/virtualenvwrapper.sh
</code>
</li>
<li>
Execute the commands in .profile: 
<code>
source ~/.profile
</code>
<br />
should return
<br />
<code>
virtualenvwrapper.user_scripts creating /Users/test/.virtualenvs/initialize
<br />
.
<br />
.
<br />
virtualenvwrapper.user_scripts creating /Users/test/.virtualenvs/prermproject
virtualenvwrapper.user_scripts creating /Users/test/.virtualenvs/postrmproject
</code>
</li>
<li>
Create a new virtualenv: 
<code>
mkvirtualenv mtec2002
</code>
You should see the following output:
<br />
<code>
New python executable in mtec2002/bin/python
<br />
.
<br />
.
<br />
Installing pip................done.
</code>
</li>
<li>
Add this to ~/.profile
<br />
<code>
workon mtec2002
</code>
</li>
</ol>

## Verification Process:
1. When you open terminal as __user__...
2. You should see mtec2002 as a prefix to your prompt 

Alternate Install Using Homebrew
=====
ruby <(curl -fsSk https://raw.github.com/mxcl/homebrew/go)
brew install git
brew install python3 
brew link python3
python3 --version
brew install mercurial libpng libjpg sdl sdl_image sdl_mixer sdl_ttf smpeg portmidi
in .profile: export PATH=$PATH:/usr/local/share/python3/

Output from history
  1  python
    2  gcc
    3  ifconfig
    4  updated README [foureyes]
    5  vim ~/.profile
    6  pip install bottle
    7  python3
    8  pip install hg+http://bitbucket.org/pygame/pygame
    9  ls
   10  ls
   11  cd ~/Downloads/
   12  ls
   13  ls -lt
   14  vim pygame_image.py 
   15  ls
   16  python pygame_image.py 
   17  pythone pygame_image.py 
   18  python3 pygame_image.py 
   19  vim pygame_image.py 
   20  python3 pygame_image.py 
   21  brew install libjpg
   22  python3 pygame_image.py 
   23  pip install hg+http://bitbucket.org/pygame/pygame
   24  python3 pygame_image.py 
   25  brew install libpng
   26  brew install sdl sdl_image sdl_mixer sdl_ttf smpeg portmidi
   27  brew help
   28  brew uninstall sdl sdl_image sdl_mixer sdl_ttf smpeg portmidi
   29  brew uninstall sdl sdl_image sdl_mixer sdl_ttf smpeg portmidi
   30  brew uninstall sdl sdl_image
   31  brew install sdl sdl_image
   32  python3 pygame_image.py 
   33  pip install hg+http://bitbucket.org/pygame/pygame
   34  python3 pygame_image.py 
   35  ls
   36  cd ~
   37  hg clone https://bitbucket.org/pygame/pygame
   38  ls
   39  cd pygame/
   40  ls
   41  python config.py 
   42  python3 setup.py 
   43  pip -l
   44  pip
   45  pip help
   46  pip uninstall
   47  pip help uninstall
   48  pip uninstall pygame
   49  ls
   50* 
   51  pwd
   52  python config.py 
   53  python setup.py 
   54  whidh python
   55  python3 setup.py 
   56  pip install hg+http://bitbucket.org/pygame/pygame
   57  ls
   58  cd ~/Downloads/
   59  ls
   60  python pygame_image.py 
   61  python3 pygame_image.py 
   62  history

