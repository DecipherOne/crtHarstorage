# Containment Unit

A collection of front end performance tools.

------------------------------------------------------------------------------------------------------------------------------------------

####Warning :

At this time, there are known security issues with the use of the shell parameter from initializing Popen from the casperjs.py module.
 Use at your own risk. This is currently meant to be used as a standalone web application. This web application is still under development.

 ------------------------------------------------------------------------------------------------------------------------------------------

Includes :
A custom version of HarStorage - https://code.google.com/archive/p/harstorage/
Also allows execution of casperjs scripts through the Python interpreter, through a web interface.
Also makes use of Wraith https://github.com/BBC-News/wraith with a web interface for regression image testing.

Third Party Application Dependencies

Python 2.7, MongoDB, Ruby, Browser-Mob Proxy

Ruby Dependencies

Wraith(Requires own versions of phantomjs and casperjs)

Image Magick

Python Dependencies

Setuptools, pyMongo 2.8, Browser-Mob Proxy 0.7.1 (modified),  pylons 1.0, paste 2.0.2, containmentUnit1.0)

##Windows Installation:

###Install Python 2.7

[https://www.python.org/downloads/release/python-2710/](https://www.python.org/downloads/release/python-2710/)

* Must be this version of python

<b>Make sure that the path(s) to python and python/scripts is set : - Double check to see if the installer set these.</b>

###Install MongoDB

[https://www.mongodb.org/downloads#production](https://www.mongodb.org/downloads#production)

####For Windows 7 or Windows Server 2008 R2

The MongoDB service installation instructions will not work for you until you install Hotfix KB2731284 on your machine. Until you do,
you will receive "Hotfix KB2731284 not installed" error when attempting to run the following command from the docs:

    "C:\mongodb\bin\mongod.exe" --config "C:\mongodb\mongod.cfg" --install

The hotfix must be requested from Microsoft. That request can be made here: [https://support.microsoft.com/en-us/kb/2731284](https://support.microsoft.com/en-us/kb/2731284)

You will be emailed the hotfix. Install it by unzipping the file and running the .exe file. You will have to restart your computer before
continuing with the MongoDB service installation.

------------------------------------------------------------------------------------------------------------------------------------------

Go here for downloads: [https://www.mongodb.org/downloads#production](https://www.mongodb.org/downloads#production)

Download the proper version for your os and run the installer.  The docs all assume you have installed Mongo to C:\mongodb. To do this,
select 'Custom' as the installation type and set installation location to C:\mongodb

Once installed, you need to set mongodb up as a service, so that it will run when windows runs.

Instructions can be found here:

[https://docs.mongodb.org/manual/tutorial/install-mongodb-on-windows/#configure-a-windows-service-for-mongodb-community-edition](https://docs.mongodb.org/manual/tutorial/install-mongodb-on-windows/#configure-a-windows-service-for-mongodb-community-edition)

Create a config file called C:\mongodb\mongodb.cfg  with the following contents. (This is read as a yaml file so indentation is important.)

	systemLog:
		destination:file
    		path: c:\mongodbfiles\log\mongodb.log (Where you want the server log to go.)
    	storage:
        	dbPath: c:\mongodbfiles\data\db (Where you want the documents to be stored.)

Save this file,  If the specified directories do not exist, manually create them,
(You MUST create these directories, otherwise the process will fail.)
Then from an administrative cmd line run the following command (Make sure your paths are set to where you have things installed) :

	"C:\mongodb\bin\mongod.exe" --config "C:\mongodbfiles\mongodb.cfg" --install

If everything went well, the system will spit out a blank line.
Then type:

	net start MongoDB

If everything went well, you'll see the message that the service started successfully.
You now have a configured mongodb service that will start automatically with windows.


###Install Ruby 2.3.X or 2.2.X:

[http://rubyinstaller.org/downloads/](http://rubyinstaller.org/downloads/) - Run the installer

###Install Browser-Mob Proxy:

[https://github.com/lightbody/browsermob-proxy/releases/](https://github.com/lightbody/browsermob-proxy/releases/tag/browsermob-proxy-2.0.0)

Note: This project uses version 2.0

 Download the bin zip file and extract to c:\

 Path should end up being:

	C:\browsermob-proxy-2.0.0

If you install to a different location,make note, YOU NEED TO UPDATE THE PATH IN config/thirdPartyPaths.json .

###Install Phantomjs 1.9.7

[https://bitbucket.org/ariya/phantomjs/downloads](https://bitbucket.org/ariya/phantomjs/downloads)

Extract Zip file and make sure to set your PATH for phantomjs (Make sure to keep this version on the path, the version wraith uses is not compatible with our casperjs functionality.

###Install casperjs 1.1.0

[https://github.com/casperjs/casperjs/releases](https://github.com/casperjs/casperjs/releases)

It may be possible to use other versions, but that has not tested. Make sure to set your path so casperjs will resolve to this version.

If you install to a different location other than C:\casperjs\bin ,make note, YOU NEED TO UPDATE THE PATH IN config/thirdPartyPaths.json .
This has to be set, otherwise the system may resolve casperjs incorrectly to the version wraith uses. If all else fails, check you system PATH variable.

###Install ImageMagick

[http://www.imagemagick.org/script/index.php](http://www.imagemagick.org/script/index.php)

 Make sure to add ImageMagick\bin to your PATH environment variable.

###Install Wraith 3.1.0

[https://github.com/BBC-News/wraith](https://github.com/BBC-News/wraith)

From the cmd line :

    gem install wraith -v 3.1.0

###Install python setuptools



[http://ftp.gnome.org/pub/GNOME/binaries/win32/pygtk/2.22/](http://ftp.gnome.org/pub/GNOME/binaries/win32/pygtk/2.22/)

Grab the .msi and run it to install.

####Install pyrsvg

[http://ftp.gnome.org/pub/GNOME/binaries/win32/gnome-python-desktop/](http://ftp.gnome.org/pub/GNOME/binaries/win32/gnome-python-desktop/)

Grab the .msi and run it to install.

####Install setuptools

[http://pypi.python.org/pypi/setuptools](http://pypi.python.org/pypi/setuptools)

The recommended installation method is to download the ez_setup.py file and run it from the command line.



###Install additional Python dependencies

From an elevated cmd line run the following commands one at a time :

    easy_install pylons==1.0

    easy_install webob==0.9.8

    easy_install pymongo==2.8

    easy_install browsermob-proxy==0.7.1

    easy_install containmentUnit

###Alter modified dependencies

####Modify browser-mob proxy:

The default server version will not terminate correctly on windows.  I altered the server so that it can successfully shut down.

Navigate to your python27 installation directory. My directory is C:\Python27

Then navigate to:

	C:\Python27\Lib\site-packages

You should see the package for browsermob-proxy, if the egg is inaccessible, you will need a program like 7zip to access it.

Once you get the directory open, you will see a list of python files.

In a seperate window/shell navigate to:

	C:\Python27\Lib\site-packages\containmentUnit1.0-py2.7.egg\containmentUnit\dependencyMods\bmpExtract

Copy the contents of this directory to

	C:\Python27\Lib\site-packages\browsermob_proxy-0.7.1-py2.7.egg\browsermobproxy\

The server is now modified to close correctly on windows.

####Modify Wraith Template :

By default the wraith template dumps out the system paths. Since we are hooking our output stream up to the internet, we don't want to expose this data, so we have a modified template.

Navigate to:

	C:\Python27\Lib\site-packages\containmentUnit1.0-py2.7.egg\containmentUnit\dependencyMods\wraith_customFiles

You need to locate wraiths template directory, it will be in your ruby path, mine is:

	C:\tools\ruby22\lib\ruby\gems\2.2.0\gems\wraith-3.1.4\lib\wraith

In the directory replace gallery.rb with the one from the containmentUnit

Then go to:

	C:\tools\ruby22\lib\ruby\gems\2.2.0\gems\wraith-3.1.4\lib\wraith\gallery_template

Replace the slideshow_template.erb with the one from the containmentUnit. Your wraith template is now modified.

###Update thirdPartyPaths.json

    You will need to find where python27 is located and get to the containmentUnit site-package.
    
    Path to thirdPartyPaths.json for me is : c:/python2.7/Lib/site-packages/containmentUnit/config/

    Open this folder up in a text editor.

    ###Update Contents of thirdPartyPaths.json

        When you first Open the file you will see the default windows paths :

        {"casperjs": "c:/casperjs/bin/","browser-mob-proxy":"c:/browsermob-proxy-2.0.0/bin/browsermob-proxy.bat","defaultProxyPort":"8080" }

        This json structure is how the application will resolve the path of our casperjs and browser-mob-proxy installations.
        
        defaultProxyPort - This value is which port the proxy server will attempt to use. Change this here if you 
            the server to use a different port.

####Configure Server for first Run

    Navigate to : C:\Python27\Lib\site-packages\containmentunit-1.0-py2.7.egg\containmentUnit\dependencyMods

    Copy the folder called executableBase and paste it to an easy to remember location like the desktop or c: drive.

    In this directory you will see 3 different batch files. These are examples of files you can use in your systems start folder to kick off the server when windows logs on.

    Or you can simply double click on the batch file to launch the server.

    Before you do that though, you will need to configure the batch files, and the server configuration.

    Server configuration is done here using the production.ini file. The one in the config directory is included for reference.
    In order for the service to be properly registered, you will want to generate a new one.
    You can generate a new ini file by browsing to directory, in an elevated cmd shell, you want your server
    to execute from and issuing the command :

        paster make-config "containmentUnit" production.ini

    You could actually setup multiple server configurations here, dev.ini for example, to run with debug options set to display verbose information.
    This could be helpful in testing altered services.

Which ever file you decide to use, open that file in a text editor and take a look.

        # containmentUnit - Pylons configuration Example
	#
	# The %(here)s variable will be replaced with the parent directory of this file
	#
	[DEFAULT] (if actually in a production environment prob want to set this to false.)
	debug = true

        (This is the main configuration, host says it'll just run on default localhost ip, you can change the port here.)

	[server:main]
	use = egg:Paste#http
	host = 0.0.0.0
	port = 5000

	[app:main]
	use = egg:containmentUnit
	full_stack = true
	static_files = true
	temp_store = %(here)s/data
	bin_store  = %(here)s
	ps_enabled = false
	static_version = 1.0

        (These are the db settings, you can specify a password, set the port, these defaults should work out of the box.But if deploying to a public environment, you will want
        to change these settings for security reasons.)

	mongo_host = localhost
	mongo_port = 27017
	mongo_db   = harstorage
	mongo_auth = false
	mongo_user = admin
	mongo_pswd = admin

	cache_dir = %(here)s/data
	beaker.session.key = harstorage
	beaker.session.secret = txe8uJCVrKOzfYd2ENZrkZ/Xp

	app_instance_uuid = {86dcf52f-197f-4c6b-b852-0116128797d6}

        Logging configuration 

        [loggers] keys = root

        [handlers] keys = console

        [formatters] keys = generic

        [logger_root] level = INFO handlers = console

        [handler_console] class = StreamHandler args = (sys.stderr,) level = NOTSET formatter = generic

        [formatter_generic] format = %(asctime)s %(levelname)-5.5s [%(name)s] [%(threadName)s] %(message)s

Once you have your settings the way you want. Navigate to where the production.ini file is in an admin cmd prompt.

Then type the command :

    paster setup-app production.ini

After running the command you should see :

    Running setup_app() from containmentUnit.websetup

This should have registered your application.

From the same directory, now run :
(log file is optional)

    paster serve production.ini --log-file harStorage.log

If you were doing development and you want the server to restart when a change is made to a python class you'll want to run with the --reload argument

    paster serve --reload production.ini --log-file harStorage.log  

Going to http://127.0.0.1:5000 in your browser for the first time will run the data-migration which essentailly creates the db tables and the like. Make sure to leave your browser open while this runs.

You are now all set!

----------------------------------------------------------------------------------------------------------------------------
##Linux Cent-OS Installation :

###Install Python 2.7 -

* Must be this version of python

From the cmd line : (The software collections repository explanation) - [https://wiki.centos.org/AdditionalResources/Repositories/SCL](https://wiki.centos.org/AdditionalResources/Repositories/SCL)

	yum install -y centos-release-SCL
	yum install -y python27

* Some versions require you to build python2.7 along side of 2.6
Follow these instructions
https://dmngaya.com/2015/10/25/installing-python-2-7-on-centos-6-7/

Side by side install, in order to have python resolve to 2.7, as user navigate to your home directory and open  ~/.bashrc for editing
Find already defined aliases or simply add the line:

alias python=/usr/local/bin/python2.7

This allows the user account to use python2.7 while the root account is still using python2.6 which the system requires.
To verify you are using the right python, from the cmd line type :

    which python

You should see the path to python2.7 dumped out. Now switch to su   then type

    which python

you should see the path to python2.6

###Install MongoDB -

    https://www.mongodb.org/downloads#production
    Follow Installation Instructions here to setup as service :
    https://docs.mongodb.org/v2.4/tutorial/install-mongodb-on-red-hat-centos-or-fedora-linux/

###Install Ruby -

    Try this first
    http://tecadmin.net/install-ruby-2-2-oncentos-rhel/

    Option 2
    https://www.digitalocean.com/community/tutorials/how-to-install-ruby-on-rails-on-centos-6

###Browser-Mob Proxy 2.0 -

    https://github.com/lightbody/browsermob-proxy/releases/tag/browsermob-proxy-2.0.0

    Download the appropriate bin zip package.

    Extract package to desired location : ~/browser-mob-proxy2.0.0
    (You will need to set this path in config/thirdParyPaths.json, so the application can resolve the path.)

    <b>Important</b>
    browser mob proxy requires a jdk version of at least 1.7, on my system, I was using 1.6

    In order to remedy this issue follow this tutorial:
    [http://www.mkyong.com/java/java-unsupported-major-minor-version-51-0](http://www.mkyong.com/java/java-unsupported-major-minor-version-51-0)

    Once this is done, create an alias for java for the user account.
    <b> This step had to be done, no matter what I tried, using alternative, ect..
    adding the alias and changing the bash script had to be done in order to resolve the correct
    java version.</b>

    open ~/.bashrc and add the lines

    alias java='/usr/java/jdk1.7.0_79/bin/java'
    
    make sure to substitute the path to where your jdk is installed

    Modify bash shell script -

    After having set the alias, you can now update the shell script

    Navigate to ~/browsermob-proxy2.0.0/bin/

    open browsermob-proxy.sh in an editor

    Go to line 55 to 67  

    You should see a block that looks like :

    <code>
     If a specific java binary isn't specified search for the standard 'java' binary
    if [ -z "$JAVACMD" ] ; then
      if [ -n "$JAVA_HOME"  ] ; then
        if [ -x "$JAVA_HOME/jre/sh/java" ] ; then
          # IBM's JDK on AIX uses strange locations for the executables
          JAVACMD="$JAVA_HOME/jre/sh/java"
        else
          JAVACMD="$JAVA_HOME/bin/java"
        fi
      else
        JAVACMD=`which java`
      fi
    fi
    </code>

    Line 62 where it is :

        else
          JAVACMD="$JAVA_HOME/bin/java"

   change it to :
        
        JAVACMD="java"

    on line 69 you will see:

    if [ ! -x "$JAVACMD" ] ; then

    change this to :

    if [ ! exec "$JAVACMD" ] ; then

    We change this because we are executing the java cmd directly.

    Save, and finished. This lets the alias settings resolve the java version, as the 
    this script trying to figure it out fails with multiple jdk versions.
    

    

###Install PhantomJS1.9.7 -

    Follow these same instructions , make sure to substitute the version for 1.9.7 
    https://www.bonusbits.com/wiki/HowTo:Install_PhantomJS_on_CentOS

###Install CasperJS 1.1.0 -
    https://github.com/casperjs/casperjs/releases/tag/1.1.0
    I just manually downloaded release 1.1.0 and extracted the folder to the Home/casperjs directory
    (You will need to set this path in config/thirdParyPaths.json, so the application can resolve the path.)

###Install ImageMagick -

    sudo yum install ImageMagick

###Install python setuptools

       sudo yum install pygtk2.x86_64

       sudo yum install pycairo

       sudo yum install gnome-python2-rsvg

       Follow these instructions to get setup tools to register with python2.7 in a side by side install (make sure to install pip)

            https://www.digitalocean.com/community/tutorials/how-to-set-up-python-2-7-6-and-3-3-3-on-centos-6-4

###Install additional Python dependencies

From a cmd line run the following commands one at a time :

    pip install  pylons==1.0

    pip install webob==0.9.8

    pip install pymongo==2.8

    pip install browsermob-proxy==0.7.1

    pip install WebTest==1.3.3

    pip install containmentUnit

   <b> If installation of the containmentUnit fails because of a conflict with WebTests simply installed the required version</b>

    pip install WebTest==1.3.3

###Update thirdPartyPaths.json

    You will need to find where python27 is located and get to the containmentUnit site-package.
    
    Path to thirdPartyPaths.json for me is : /usr/local/lib/python2.7/site-packages/containmentUnit/config/

    Open this folder up in a text editor.

    ###Update Contents of thirdPartyPaths.json

        When you first Open the file you will see the default windows paths :

        {"casperjs": "c:/casperjs/bin/","browser-mob-proxy":"c:/browsermob-proxy-2.0.0/bin/browsermob-proxy.bat","defaultProxyPort":"8080" }

        This json structure is how the application will resolve the path of our casperjs and browser-mob-proxy installations.
        For my linux installation, I had to alter this to : 

        {"casperjs": "/home/me/casperjs/bin/","browser-mob-proxy":"/home/me/browser-mob-proxy2.0/bin/browsermob-proxy","defaultProxyPort":"8080" }
        
        defaultProxyPort - This value is which port the proxy server will attempt to use. Change this here if you 
            the server to use a different port.

	
        
###Make sure that the project has adequate read/write permissions
    
    Depending on how your system is setup, you may need to change ownership of the project directories and
    files so that proper file modification can be performed by the program.

    On installation, ownership for my project directory was set to root.
    You can check ownership by browsing to the directory where containmentUnit is installed and
    typing :

    ls -l

    from the command line. This will give you something like :

    [user@localhost containmentUnit]$ ls -l                                                                                                                     
    total 40                                                                                                                                                   
    drwxr-xr-x 2 root root 4096 Apr 27 15:36 config                                                                                                            
    drwxr-xr-x 2 root root 4096 Apr 27 13:06 controllers                                                                                                       
    drwxr-xr-x 5 root root 4096 Apr 27 13:06 dependencyMods                                                                                                    
    -rw-r--r-- 1 root root    0 Apr 27 13:06 __init__.py                                                                                                       
    -rw-r--r-- 1 root root  152 Apr 27 13:06 __init__.pyc                                                                                                      
    drwxr-xr-x 2 root root 4096 Apr 27 13:06 lib                                                                                                               
    drwxr-xr-x 7 root root 4096 Apr 27 13:06 public                                                                                                            
    drwxr-xr-x 7 root root 4096 Apr 27 13:06 templates                                                                                                         
    drwxr-xr-x 3 root root 4096 Apr 27 13:06 tests                                                                                                             
    -rw-r--r-- 1 root root  367 Apr 27 13:06 websetup.py                                                                                                       
    -rw-r--r-- 1 root root  676 Apr 27 13:06 websetup.pyc

    If ownership is set to root, when trying to run applications commands, we are going
    to have permission issues. To change ownership of all the files and folders in the directory tree,
    issue the following command.

    sudo chown -R user ../containmentUnit

    now if you do ls -l again, you should see

    [user@localhost containmentUnit]$ ls -l                                                                                                                     
    total 40                                                                                                                                                   
    drwxr-xr-x 2 user root 4096 Apr 27 15:36 config                                                                                                            
    drwxr-xr-x 2 user root 4096 Apr 27 13:06 controllers                                                                                                       
    drwxr-xr-x 5 user root 4096 Apr 27 13:06 dependencyMods                                                                                                    
    -rw-r--r-- 1 user root    0 Apr 27 13:06 __init__.py                                                                                                       
    -rw-r--r-- 1 user root  152 Apr 27 13:06 __init__.pyc                                                                                                      
    drwxr-xr-x 2 user root 4096 Apr 27 13:06 lib                                                                                                               
    drwxr-xr-x 7 user root 4096 Apr 27 13:06 public                                                                                                            
    drwxr-xr-x 7 user root 4096 Apr 27 13:06 templates                                                                                                         
    drwxr-xr-x 3 user root 4096 Apr 27 13:06 tests                                                                                                             
    -rw-r--r-- 1 user root  367 Apr 27 13:06 websetup.py                                                                                                       
    -rw-r--r-- 1 user root  676 Apr 27 13:06 websetup.pyc

    The project now has proper rwx permissions.

