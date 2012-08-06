tests-Mac-Pro:mtec2002 test$ cat install.txt 
* install python python 3
** download python 3: http://www.python.org/ftp/python/3.2.3/python-3.2.3-macosx10.6.dmg
** check in the install by typing which python3
** should give you something like /usr/local/bin/python3

* distribute http://pypi.python.org/pypi/distribute#installation-instructions
** grab the install script
*** curl -O http://python-distribute.org/distribute_setup.py
** run the install script
*** sudo python3 distribute_setup.py
*** make sure you use python 3

easy install should be here
/Library/Frameworks/Python.framework/Versions/3.2/bin/easy_install-3.2

* install yolk to list packages
sudo /Library/Frameworks/Python.framework/Versions/3.2/bin/easy_install-3.2 yolk

* install pip for package installation
sudo /Library/Frameworks/Python.framework/Versions/3.2/bin/easy_install-3.2 pip

/Library/Frameworks/Python.framework/Versions/3.2/lib/python3.2/site-package


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




42  sudo find / -iname *Idle*
   43  usr/local/bin/idle3
   44  /usr/local/bin/idle3
   45  sudo find . -iname pip
   46  sudo find / -iname pip
   47  which pip
   48  source ~/.bashrc 
   49  which python3
   50  which pip
   51  pip install requests pyglet beatifulsoup4
   52  pip install bottle beatifulsoup4
   53  pip install bottle BeatifulSoup4
   54  pip install bottle beautifulsoup4
   55  history


(mtec2002)tests-Mac-Pro:~ test$ cat ~/.profile 
export PATH=/Library/Frameworks/Python.framework/Versions/3.2/bin:$PATH
VIRTUALENVWRAPPER_PYTHON=/Library/Frameworks/Python.framework/Versions/3.2/bin/python3
source /Library/Frameworks/Python.framework/Versions/3.2/bin/virtualenvwrapper.sh
workon mtec2002

