# elasticsearch-setup 
This repository is forked from the original at [elasticsearch-setup](https://github.com/rgl/elasticsearch-setup) with a few updates to make building of the source easier.

## Option 1: Download pre-built binaries

+ Available from [http://ruilopes.com/elasticsearch-setup/](http://ruilopes.com/elasticsearch-setup/)

## Option 2: Build elasticsearch-setup binaries yourself

**Note:** The following assumes a vanilla Windows 7 SP1 install.
 
1. Get elasticsearch-setup source by cloning the github repo

		$ git clone https://github.com/isldevops/elasticsearch-setup.git

1. Install Java JDK

		C:\>cd Path\To\Cloned\Repo
		
		C:\Path\To\Cloned\Repo>cd vendor
		
		C:\Path\To\Cloned\Repo\vendor\>jdk-7u13-windows-x64.exe
		
		*Note:* Install by accepting all defaults		
		
1. Add location (default) of Java JDK to system variables, the full JDK is required as we use JAR.exe during build
		
		C:\>setx PATH "C:\Program Files\Java\jdk1.7.0_13\bin;%PATH%"
		C:\>setx JAVA_HOME "C:\Program Files\Java\jdk1.7.0_13\bin;"
		
1. Install Unicode Inno Setup

		C:\>cd Path\To\Cloned\Repo
		
		C:\Path\To\Cloned\Repo>cd vendor
		
		C:\Path\To\Cloned\Repo\vendor\>isetup-5.4.3-unicode.exe
		
		*Note:* Install by accepting all defaults		
		
1. Install MinGW and MSYS

		C:\>cd Path\To\Cloned\Repo
		
		C:\Path\To\Cloned\Repo>cd vendor
		
		C:\Path\To\Cloned\Repo\vendor\>mingw-get-inst-20120426.exe
		
		*Note:* Select 'Download latest repository catalogues'
		*Note:* Select Components 'C Compiler' and 'MSYS Basic System
		*Note:* Complete install by accepting all other defaults

1. Configure MinGW		

		Launch MinGW by Start>All Programs>MinGW>MinGW Shell
		
		$ mingw-get install msys-unzip
		
		$ mingw-get install msys-wget
		
1. Make (let's build this thing)

		Launch MinGW by Start>All Programs>MinGW>MinGW Shell
		
		$ cd drive:/Path/To/Cloned/Repo
		
		$ make


All going well, the above should download the ElasticSearch	and Common Daemon zip files and compile the installer, outputing something along these lines.

		Successful compile (4.134 sec). Resulting Setup program filename is: c:\development\Github\elasticsearch-setup\elasticsearch-0.20.2-setup-64-bit.exe 
		make[1]: Leaving directory `/c/development/Github/elasticsearch-setup' 	

##Execute build from TeamCity (optional)

1. TBC
		
## Running the installer 

The setup will do the following when installing the application:

1. Install all files into Program Files (the user can change the actual location)

1. Create the elasticsearch local Windows account (with Logon as service privilege)

1. Install a Windows Service to automatically start elasticsearch (run as the elasticsearch account) at boot (but has to be manually started after install...).

1. Grant the elasticsearch account:
1.1 read permissions to the "config" directory.
1.1. full permissions to the "data" and "logs" directories.

1. Create a bunch of Start Menu entries (link to home page, guide, etc).

### A few notes

The setup uses [SetACL.exe](http://helgeklein.com/setacl/) to grant NTFS file permissions to the elasticsearch account.

The setup uses [procrun.exe](http://commons.apache.org/daemon/) to launch elasticsearch as a Windows service.


## Disclaimer
NO warranty, expressed or written