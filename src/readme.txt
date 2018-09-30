#
#  General notes
#

Facepager originally is developed for Python 2.7 with PySide 1
Facepager recently migrated to Python 3.4 with PySide 1.

Facepager depends on the following packages:

PySide: Download from https://qt-project.org/wiki/Category:LanguageBindings::PySide::Downloads (Licence: LGPL)
SQLAlchemy: pip install SQLAlchemy (Licence: MIT)
dateutil: pip install python-dateutil (PSF License)
requests: pip install requests (Apache2 License)
requests_oauthlib: pip install requests_oauthlib (ISC License, equivalent to the BSD 2-Clause and MIT licenses)
requests[security]: pip install -U requests[security]==2.7.0
rauth: pip install rauth (MIT licence)
numpy and pandas: pip install numpy pandas

Facepager needs some secret keys to connect to Facebook and Twitter.
See credentials.py.readme for further details.

########
#
# Steps to run under Windows with Python3
#
########

1. Install Python3.4
	
		
	Stick to Python3.4 because: 
	- newer versions not compatible with pyside v1, 
	- pyside2 not compatible with QtWebEngineWidgets on 32bit windows
	
	Download from https://www.python.org/downloads/windows/ and install
	Open command line in installation folder. 
	Check you use the pip from the new installation:
	
	$ pip -V
	
	Install libraries:
	
	$ pip install pyside
	$ pip install sqlalchemy
	$ pip install python-dateutil
	$ pip install rauth
	$ pip install requests_oauthlib
	
	For pandas you need Microsoft Visual C++ 10.0. 
	I used the chip installer, be aware of adware!: https://www.chip.de/downloads/Visual-C-2010-Express_24081894.html 

	
	Install numpy and pandas:
	
	$ pip install numpy pandas


2. Eclipse Setup
Install Liclipse with PyDev, set interpreter to the just installed python.exe
( Window -> Preferences -> PyDev -> Interpreters -> Python Interpreter -> New)


3. Facepager Setup
clone Facepager
setup credentials.py (see credentials.py.readme)
run Facepager

(in run and debug configuration of liclipse set correct interpreter)



########
#
#  Steps to run under linux
#  (tested under ubuntu vivid x64, thx to crsqq / Christoph Martin) 
#
########

#### Notice: the instructions work for Python 2.7. Meanwhile Facepager migrated to Python 3.x.

git clone https://github.com/strohne/Facepager
cd Facepager

sudo apt-get install build-essential git cmake libqt4-dev libphonon-dev python2.7-dev libxml2-dev libxslt1-dev qtmobility-dev python-virtualenv

virtualenv facepager_env
. facepager_env/bin/activate

pip install SQLAlchemy python-dateutil requests rauth wheel
cd src/

#you may want to change the download link to the most recent version
wget https://pypi.python.org/packages/source/P/PySide/PySide-1.2.2.tar.gz
extract PySide-1.2.2.tar.gz 
cd PySide-1.2.2/


python2.7 setup.py bdist_wheel --qmake=/usr/bin/qmake-qt4

../pacepager_env/bin/pip2.7 install dist/PySide-1.2.2-cp27-none-linux_x86_64.whl 

#add your credentials
cp credentials.py.readme credentials.py
python Facepager.py 


#######
#
#  Steps to run under Windows Subsystem for Linux (Windows 10)
#
#  Commands to run in bash are marked with $ sign 
#
########

#### Notice: the instructions work for Python 2.7. Meanwhile Facepager migrated to Python 3.x.

#
# 1. Prepare bash
#

	# Install WSL, see https://msdn.microsoft.com/de-de/commandline/wsl/install_guide
	# Install Xming X Server to run graphical apps, see https://askubuntu.com/questions/823352/windows-10-bash-cannot-connect-to-display and  http://www.pcworld.com/article/3055403/windows/windows-10s-bash-shell-can-run-graphical-linux-applications-with-this-trick.html
	# Start bash: windows key, type "bash"
	# Enable QuickEdit-Mode, this way you can copy&paste commands from this file to the terminal by mouse right click: click on Ubunutu icon in topleft corner of terminal window, click "Properties", "Options", "QuickEdit-Mode"; for further information see http://stackoverflow.com/questions/38832230/copy-paste-in-bash-on-ubuntu-on-windows
	# Create a directory to work in, directories under /mnt/ will be shared between windows and linux, e.g.

	$ mkdir /mnt/c/FacepagerLinux
	$ cd /mnt/c/FacepagerLinux

#
# 2. Install dependencies and setup Python environment
#

	$ sudo apt-get install build-essential git cmake libqt4-dev libphonon-dev python2.7-dev libxml2-dev libxslt1-dev qtmobility-dev python-virtualenv

	$ virtualenv facepager_env
	$ . facepager_env/bin/activate
	$ pip install SQLAlchemy python-dateutil requests rauth wheel

	# The following commands take a long time, press return if terminal seems to hang
	$ pip install pyside
	$ pip install numpy pandas

#
# 3. Install and run Facepager
#

	$ cd /mnt/c/FacepagerLinux
	$ git clone https://github.com/strohne/Facepager
	$ cd Facepager/src
	$ cp credentials.py.readme credentials.py

	# Don't forget to manually add your credentials in credentials.py

	#Activate x server
	$ export DISPLAY=:0

	#Run Facepager
	$ python Facepager.py 



#######
#
#   Steps to run under OSX El Capitan in VMWare
#
#	tested in virtual machine with VMware Workstation 12 Player under windows 10
#   see http://techsviewer.com/how-to-install-mac-os-x-el-capitan-on-vmware-on-pc/
#
#######


0. Install OSX in virtual machine
Follow the steps in http://techsviewer.com/how-to-install-mac-os-x-el-capitan-on-vmware-on-pc/
Edit virtual machine, in Network Adapter section set network connection to "Bridged" instead of "NAT"


1.Prepare system
1.1 Install python 2.7 from python.org. This gives you a Python folder under Applications, containing the Python Launcher
[1.2 Maybe optional: update PIP by running get-pip.py (see http://pyside.readthedocs.io/en/latest/installing/macosx.html)]
1.3 Install homebrew, type in terminal:
	
	/usr/bin/ruby/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

	
2.Install packages

2.1 Install PySide, type in terminal:		

	brew install qt
	brew install PySide	
	
	[Check the output, replace USERNAME by your username in the following command]
	
	mkdir -p /Users/USERNAME/Library/Python/2.7/lib/python/site-packages
	echo 'import site; site.addsitedir("/usr/local/lib/python2.7/site-packages")' >> /Users/USERNAME/Library/Python/2.7/lib/python/site-packages/homebrew.pth
	
2.2. Install other packages, type in terminal:

	pip install SQLAlchemy
	pip install python-dateutil
	pip install requests
	pip install requests_oauthlib
	pip install -U requests[security]==2.7.0
	pip install rauth
	pip install pandas
	

3. Install Facepager

    - Download from github or clone (https://github.com/strohne/Facepager.git)
    
	- To clone via https open terminal and run the following commands:
	  (could fail in virtual machine, workaround is to install GitHub Desktop? better way: bridge network in vwware player instead of nat)
	  (adjust folder name if neccessary)
	  
	    $ cd Documents
	    $ git clone https://github.com/strohne/Facepager.git
  	  
	  
    - Create credentials.py (see above)

4. Launch Facepager.py (with python launcher, not in terminal)


#######
#
#   Steps to run under macOS High Sierra in VirtualBox under Windows
#
#######

0. Install maxOS in virtual machine
Follow the steps in https://saintlad.com/install-macos-high-sierra-in-virtualbox-on-windows-10/

If network connection is not available: Edit virtual machine, in Network Adapter section set network connection to "Bridged" instead of "NAT"

To exchange files between host and guest set network connection to bridged, open macos system preferences, search sharing -> files. click options and allow sharing. Note the address of the machine and open this address with windows explorer.

Special keys in macOS
square brackets: Alt+5 / 6.
@ character: Alt+L
~ character: Alt+N

Open terminal by typing "terminal" in the spotlight search (top right corner on the screen)

1.Install Python

	High Sierra comes with Python 2.7. We need Python 3.4. 
	
	See https://docs.python-guide.org/starting/install3/osx/#install3-osx
	
	Install homebrew, type in terminal:	
	$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

	Install Python3.4. This is the last version supporting PySide v1.
	Install older version with pyenv (brew install python would install the newest version)
	
	$ brew install pyenv
	$ pyenv install 3.4.3
	$ PATH="~/.pyenv/versions/3.4.3/bin:${PATH}"
	$ pyenv global 3.4.3
		
	Alternatively install from package:
	$ brew install https://raw.githubusercontent.com/Homebrew/homebrew-core/bd43f59bd50bb49242259f327cb6ac7a8dd59478/Formula/python3.rb

2. Install PySide, type in terminal:		

	$ pip install PySide	

	
3. Install other packages, type in terminal:

	pip install SQLAlchemy
	pip install python-dateutil	
	pip install requests_oauthlib	
	pip install rauth
	pip install numpy pandas
	

4. Install Facepager

    - Download from github or clone (https://github.com/strohne/Facepager.git)
      
	    $ cd Documents
	    $ git clone https://github.com/strohne/Facepager.git
	  
    - Create credentials.py (see credentials.py.readme)

	- Launch Facepager
	
		In Facepager/src folder:		
		$ python3 Facepager.py
