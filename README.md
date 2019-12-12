# Dell-Boomi
One Step setup Guide for Boomi Atom/Molecule &amp; devOps in Boomi

Installing Atom on a Docker
------------------------------------------------
1.  Go to the Boomi Atomsphere page then 
2.  Go to Manage —> Atom Management —> Click on New —> Select Atom —> Chose Linux/ windows/ Docker/ & click download.
3.  This downloads the installabiles which has all the configurations needed to run an ATOM.
4.  During the download it needes to be decided whether the installation will be done using security token or basic Auth. If the security token is going to be used then copy the token from the download page. It is valid for 24 hour.
5. Post download modify the install file to change the path of ATOM home directory. follwing are the two places where Path needs to be updated .
ATOM_HOME="/var/boomi"
installationDir=/var/boomi #default atom installation dir
6. By default the ATOM conects to Boomi on port 9090 and this can be traced in the installation file. 
     platform=https://atom.boomi.com
        if [ `echo $platform | grep 'localhost' | wc -l` -gt 0 ]
        then
            hostIP=`ifconfig eth0 | grep 'inet addr:'  | cut  -d: -f2 | awk '{print $1}'`
            run_command="docker run -p ${port}:9090 -h ${atomname} --add-host=\"localhost.boomi.com:$hostIP\""
        else
            run_command="docker run -p ${port}:9090 -h ${atomname}"
        fi
7. The home directory or installtion directory should have their parent directory listed as preferred directory for Docker mount.
8. Once everything is ready run the installtion.
  Running the installtion script
  -----------------------------------------------

    Complete Installation Options Command : - 
--------------------------------------------------------
./atomdocker_install64.sh -n <atom name> -u <boomi userid> -p <boomi password> -a <boomi accountid>
	-h <proxy host> -e <proxy username> -d <proxy password> -r <proxy port> -i <installation directory> -o <security update cron>
	-f <docker uid> -y <symlinks directory> -t<port> -b <boomi container name> -k <installation token>

  Install with UID
  ----------------------------------------------

  ./atomdocker_install64.sh -n "<custom Atom container name>" -u "<username@x.com>" -p <PWD> -a "accountid1"

  Install With Token
  -------------------------------------------------
./atomdocker_install64.sh -n "<custom Atoom container name>" -k "<token>"

9.Post running the installtion script in linux/ Unix /Mac go to the install directory and open the install_<atom name>.log. 
  
Following entries will appear
          No suitable Java Virtual Machine could be found on your system.
        Downloading JRE with wget ...
        Unpacking JRE ...
        Preparing JRE ...
        Starting Installer ...
        Warning: Java not found in the system PATH.
        It may cause an issue during Atom install.

        Please update your PATH environment variable.
        Example:
        export PATH=/path/to/jre/bin:$PATH
        The installation directory has been set to /<>/MyLearning/Boomi/atom/Atom_Punit_Training_Dev.
        Retrieving Build Number
        Extracting files...
        Downloading JRE Files

        Downloading Atom Files
        Retrieving Container ID

        Retrieving account keystore.
        Retrieving account trustore.
        Configuring Atom.
        Finishing installation...

10. On installtion Atom will be started and  will appear on the Atomspher. 

