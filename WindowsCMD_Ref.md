# Commands and Applications (alphabetical order)
- **appwiz.cpl** opens Add/Remove Programs to check versions and manage software
- **call** executes a batch file, useful for running subroutine batch files from a main batch file
- **cd/** changes directory to root drive, same as cd\
- **cd..** changes directory up one level
- **cd /d FilePath** navigates to directory location, same as pushd
- **certlm.msc** opens Certificate Manager for local machine, similar to mmc
- **certmgr.msc** opens Certificate Manager for current user, similar to mmc
- **certutil -store My** lists all certificates in the personal store
	- **certutil -verifystore My <#>** verifies the specified certificate in the store
	- **certutil -verify "FilePath"\certificate.cer** verifies the certificate directly from file
- **cls** clears the command window text without losing current folder location
- **cmdkey** implements other usernames and passwords
	- **cmdkey /add:"<ServerName>" /user:"<Domain\UserName>" /pass: "<Password>"** specifies that when any PI client connects to the PI Data Archive, to use these credentials
	- **cmdkey /delete:"<ServerName>"** clears the credentials
- **compmgmt** opens Computer Management
- **control panel** opens Control Panel
	- **control /name microsoft.system** opens system settings, same as right-clicking My Computer > Properties
- **copy z\*.txt CombinedFile.txt** combines all text files starting with "z" into one file named CombinedFile.  Also works for .csv files.
- **copy <File> \\<IPv4address>\C$\<path>** copies file to another location
- **date** displays current machine date in DDD mm/dd/yyyy (Wed 11/01/2017).  See echo command.
- **dcomcnfg** opens Component Services, utilized when configuring OPC communication
- **del <FilePath>** deletes file(s) from directory location.  Wildcard characters applicable.
	- **del /s <FilePath.extension>** deletes file(s) from all subdirectories as well.
- Desktop folder access: **pushd %userprofile%\desktop**
- **dir** provides list of files and folders in a directory
	- **dir \*.<extension> /a /b /s** finds and lists all files with the <extension> in the folder and all subfolders (Ex: **dir .arc /a /b /s > OutputFile.txt**)
- **devmgmt.msc** opens Device Manager to access machine hardware and settings, including NIC card
- **diskmgmt.msc** opens Disk Management to add drives and partition drives
- **doskey /history** displays list of previous commands.  Can be helpful at end of a TS or FS session.
- **@echo** hides/shows commands and outputs from batch files (@echo off or @echo on)
- **echo %variable%** displays output in Command Prompt
	- **echo %date% %time%**
	- **echo %computername%.%userdnsdomain%**
- **eventvwr** opens Windows Event Viewer logs
- **exit** closes the command prompt window, same as **Alt + Space > C**
- **explorer.exe** opens Windows Explorer
- **fc /c FilePath1 FilePath2** compares 2 files (Example: **fc "%pihome%\dat\piclient.ini" "%pihome64%\dat\piclient.ini"**)
- **<FileName.extension>** opens file from directory location
- **find "string" FilePath** searches for a text string in a file.  Wildcard character applicable.
- **findstr /i /s /c:"string" "myDrive:\myFolderPath\\*"** searches for a text string in a file.  Wildcard characters not needed for string, for example /c:"osi" will find the text "myosisoft".  NOTE:  The findstr search does not search file names or folder paths.  Use the dir command instead.
	- **findstr /i /c:"string 1" /c:"string 2" "FilePath"** searches for lines containing either string.  Will not output a line twice if two strings are found in the same line.
	- **findstr /i StringA\*.\*StringB "FilePath"** searches for lines containing both strings.  Does not support spaces within string search terms
	- **findstr /s** searches files in the directory and all sub-directores
- **for** edits lines within a file
	- **for /f "tokens=*" %a in (input.txt) do (echo D:\PI%a) >> output.txt** prepends each line in input.txt with "D:\PI". Useful for prepending lines with a command, for example **D:\PI\arc\piartool - ar Filename.arc**. All characters are required, including the () and >>.
	- **for /f %a in (input.txt) do echo %A.arc >> output.txt** appends each line with ".arc".  All characters required, inluding the () and >>.
- **fsutil file createnew %userprofile%\Desktop\test.udl 0** to create a UDL file on the desktop
- **gpedit.msc** opens Group Policy Editor (to manage prompts, etc.)
- **gpresult /scope computer /v** displays which group policies are applied to the server
	- **gpresult /scope user /v** displays which group policies are applied to the user
- **hostname** displays machine Alias name
- **iisreset** resets the Web Server and recycles all application pools
- **ipconfig** displays IP address of machine and other info
	- **ipconfig /displaydns** displays entries in the Local DNS cache
	- **ipconfig /flushdns** clears entries in the Local DNS cachemsinsetp
- **klist purge** clears the cache of Kerberos tickets for the current logon
- **lusrmgr.msc** opens local users and groups
- **md "FilePath"** creates a folder directory (make directory)
- **mmc** opens Microsoft Management Console for managing certificates (mmc > File > Add/Remove Snap-in > Certificates > Add > Computer account > Next)
- **move "FilePath1" "FilePath2"** moves a file
- **msiexec -i "FolderPath\FileName.msi" -lvx "FilePath.txt"** installs an .MSI file and outputs full logging to a text file.  NOTE:  Should be run from an Administrative command prompt.
	- **msiexec -x "FolderPath\FileName.msi"** from an Administrative command prompt uninstalls a product.  NOTE:  The target .MSI must be the same version and bitness as the currently-installed product.
- **msinfo32** opens System Information, showing the Computer information (similar to My Computer > Properties)
- **ncpa.cpl** opens Network Connections to change IP address and other internet connection settings
- **net** provides access to numerous commands
	- **net use \\<Hostname> /user:<Username> <Password>** tests a username and password, similar to "cmdkey" command
	- **net use \\<Hostname> /delete** removes the connection
	- **net user <username> /domain | find "Group"** finds the groups associated with a username on the current domain
	- **net start <ServiceName>** starts a service, similar to "sc" command
	- **net stop <ServiceName>** stops a service, similar to "sc" command
- **netsh** provides access to network shell
	- **netsh http show sslcert** shows all http SSL certificates associated with each binding, outputs can be compared with certutil
	- **netsh http delete sslcert ipport=0.0.0.0:<port>** deletes certificates bound to a port
	- **netsh firewall shot state** shows if Remote Admin is applied for Group Policy settings
- **netstat** lists ports on which applications are listening
	- **netstat -a** lists all the ports that have established connections or the machine is listening on
	- **netstat -ano** lists IP addresses only
	- **netstat -ano|find "5462"** lists process IDs listening on the specified port
	- **netstat -ano|find "LISTENING"** lists process IDs listening on all ports
	- **netstat -a | find /i "listening" | find /i "5450"** where "/i" enables the command to be case insensitive
	- **netstat -a | find /i "established" | find /i "5450"**
- **notepad.exe** opens Notepad in current dir
	- **notepad.exe FilePath** opens the existing file or creates a new one at the specified location
- **nslookup <MachineName>** displays IPv4 address of a machine, retrieving information from the Local DNS cache and the DNS Server
- **osk** opens the On-Screen Keyboard
- **pathping trace** pinging route, latency, and packet loss
- **perfmon** opens Performance Monitor
- **ping <FQDN, Alias, or IP address>** confirms whether another computer is accessible via ICMP, retrieving information from the Local DNS cache, DNS Server, and the Hosts file that contains DNS entries
	- **ping -t <hostname OR IPaddress OR FQDN>** pings continuously.  Useful after rebooting a remote computer.
	- **ping -l <size> <hostname OR IPaddress OR FQDN>** pings with packets of a specified size (size is in bytes)
- **popd** pops back to the original directory (reverse of "pushd" command)
- **powershell** opens Windows Powershell within command prompt window.  Type **cmd** to return to Command Prompt.
- **prompt OSI$G** changes the prompt directory string to "OSI>".  Can be useful if the directory path becomes very long.  To reset, enter prompt with no parameters.
- **psexec** utility to run programs as SYSTEM user (download from Microsoft)
	- NOTE:  PSEXEC needs to be run from the directory path where the PSEXEC executable resides, for example **C:\SoftwareDownloads\Microsoft\PSTools\psexec.exe -i -s mmc**
	- **psexec -i -d -s C:\Windows\regedit.exe** to open RegEdit as System user
	- **psexec -i -s mmc** to open MMC as System user
- **pushd <"DirectoryLocation">** pushes Command Prompt to a specific directory
- **query user /server:<MachineName>** shows all users connected to the machine (similar to wmic)
- **rd /s /q "Path"** deletes a folder directory and all components (remove directory), same as rmdir
- **reg delete <path> /f** deletes a registry key
- **regedit** opens Windows Registry
- **ren "FilePath.OldName.extension" NewName.extension** renames file in directory location
	- **ren OldFolderName NewFolderName** renames folder in directory location
- **resmon** opens Resource Monitor for troubleshooting processes (see KB00808)
- **rmdir /s /q "Path"** deletes a directory and all components (remove directory), same as rd
- **runas /user:<myMachineName>\<myUserName> notepad.exe** (Note: Must use the machine name and not ".\myUserName")
	- **runas /user:<domain>\<username> "c:\windows\explorer.exe /separate"** opens Windows Explorer as a different user, or another other program (Note: the password prompt will not show the characters that are being entered, but it is working)
- **start <appname> /safe** opens a program in safe mode (start outlook /safe)
- **sc** provides service change capabilities and info
	- **sc query** displays all service names, their display names, and status
	- **sc query <service name>** displays status for one service
	- **sc queryex <service name>** displays extended status including Process ID (PID), helpful for taskkill commands
	- **sc start <service name>**
		- **sc start ServiceA & sc start ServiceB** starts multiple services consecutively
	- **sc stop <service name>**
	- **sc delete <service name>**
	- **sc config ServiceA depend= ServiceB/ServiceC/ServiceD** adds dependencies to a service
	- **sc config ServiceA depend= /** removes dependencies from a service\
	- **sc qc <service name>** lists config and dependencies of service
- **secpol.msc** opens Local Security Policy
- **services.msc** opens Windows Services
- **set** displays all Environmental Variables, including %piserver%, %pihome%, etc.
	- **set pi** displays all Environmental Variables beginning with "pi"
- **set <VariableName>=<StringValue>** creates local variables that can be used in a script, example below:
	- **set IFile=C:\PITemp\MyInput.txt**
	- **set OFile=C:\PITemp\MyOutput.txt**
	- **set DoThis.bat=C:\PITemp\MyFavorite.bat**
	- **call %DoThis.bat% < %IFile% >> %OFile%**
- **setsp**n sets Service Principal Names for Kerberos Authentication
	- NOTE: can use asterisk as wildcard, e.g. **setspn -q */PISRV1**
	- **setspn -d ServiceClass/MachineName Domain\AccountName** deletes an SPN
		- NOTE:  If an SPN cannot be deleted, the Domain\Account may be registered to a different SPN ServiceClass/MachineName.  Utilize **setspn -l** and **setspn -q** to find the original SPN registration, or if needed, see "Method 3" from Microsoft article 321sys044.
	- **setspn -l Domain\AccountName** lists SPNs associated with the account
	- **setspn -q ServiceClass/MachineName** shows all SPNs for the service 
	- **setspn -s ServiceClass/MachineName:Port Domain\AccountName** sets an SPN for a service account, where ":Port" is not needed if using defaults 80 or 443.  Two SPNs should be created for MachineName, one for Hostname and the other for FQDN.
		- **setspn -s HTTP/WebMachineName Domain\PIVisionServiceAccount** (NOTE: Although HTTPS is used, an SPN for HTTP is needed.  A separate SPN for HTTPS is not needed as HTTPS is not a valid service class.)
		- **setspn -s AFServer/AFMachineName Domain\AFApplicationServiceAccount**
		- **setspn -s PIServer/PIMachineName Domain\PIDataArchiveMachineName$**
		- **setspn -s MSSQLSVC/SQLMachineName:SQLExpress Domain\SQLBrowserServiceAccount**
		- **setspn -s MSSQLSVC/SQLMachineName:1433 Domain\SQLBrowserServiceAccount**
	- **setspn -x** shows all duplicate SPNs, i.e. the same SPN assigned to separate accounts
- **shutdown /r** restarts the computer
- **start**
	- **start ,** opens a new command prompt
	- **start cmd** also opens a new command prompt, same as start ,
	- **start .** opens the current directory location in Windows Explorer
	- **start "FilePath"** opens the directory folder in Windows Explorer
	- **start notepad++**
	- **start notepad++ "filepath.txt"** opens the target file in Notepad++.  If the file doesn't exist, it prompts to create it.
	- **start powershell | chrome | iexplore | outlook | onenote | excel | word | visio | powershell** opens all programs at once
- **sysdm.cpl** opens System Properties to change computer name, domain, environmental variables, etc.
- **systeminfo** displays OS, machine, and domain information, along with the first 245 Windows Updates that were installed.  Use wmic wfe list to see all Windows Updates instead.
- **taskmgr** opens Program Manager
- **taskschd** opens Task Scheduler
- **taskkill /pid <PID#> /f** kills a service stuck in starting or stopping state.  PID can be found with sc queryex or tasklist commands.
	- **taskkill /im <ProgramName>.exe** kills a process directly without needing Task Manager (Example:  taskkill /im SMTHost.exe)
- **time** displays current machine time in hh:mm:ss.sub-seconds.  See echo command.
- **timeout /t <NumberInSeconds>** pauses batch file before continuing
- **tree** displays map of all sub-directories from current directory
- **wf.msc** opens Windows Firewall
- **whoami** displays current domain\username
	- **whoami /groups**
	- **whoami /user /fo list**
	- **whoami /groups /fo list**
- **winver** opens a window that displays Windows OS version, similar to msinfo32 command
- **wmic computersystem get model,name,manufacturer,systemtype** displays specific Computer info
- **wmic.exe /node:(computername or ip address) computersystem get username |** shows all users connected to the machine (similar to query)
- **wmic wfe list** displays all installed Windows Updates
- **xcopy** copies files and folders with additional options, superseded by robocopy
	- NOTE: Do not use the /O switch when copying to a root drive, as this can prevent access and require drive restoration
- **@<command>** runs the <command> without echoing the command to keep output files uncluttered.  The @ prepend can be very helpful in batch files.  

## Output of error stream
Command line redirecting usually only redirects the regular output, but not Windows error messages. If you are looking to capture all the messages in an output, then you need to add 2>&1 at the end of the command. Like this:  
    `pidiag -archk > archk_output.txt 2>&1`

## Shortcuts
- Ctrl + C starts a new command line and ends previous command
- /? help switch for any program or executable( pigetmsg /? > helpfile.txt)
- \>> appends file, adding the output to the end of a file.  Will create a new file if one does not currently exist ( pigetmsg -st *-1h -et * >> messages.txt )
- \> output to a file.  Will replace existing file.  ( pigetmsg -st *-1h -et * > messages.txt )
- < input from a file ( piconfig < TestCommands.txt )
- "" is used if there is a space anywhere in the FilePath ( "Drive:\Folder spaces\File spaces.txt" )
- \* wildcard for unlimited characters
- ? wildcard for one character only
- up/down arrow navigates to previous/following commands
- REM comments-out lines in a batch file
- |clip stores output to the clipboard, which can then be pasted into Notepad or other programs ( pigetmsg -st *-1h -et * |clip )
- Drag and drop file or folder into command prompt to get FilePath.  Alternative option is Ctrl + Shift + right-click > select "Copy as path"
- Tab lists directory folders alphabetically, can be pressed repeatedly anywhere within a command (in the %pihome% directory, cd <Tab> yields cd adm and other folders, while cd p<Tab> yields all folders that start with "p")
- Shift + Tab scrolls in opposite direction as Tab
 
## Opening command prompt
- Start menu > cmd > Ctrl + Shift + Enter runs command prompt as Administrator, same as right-clicking > "Run as administrator"
- Windows key + R > cmd > Enter opens command prompt
- Ctrl + Shift + right-click folder > "Open command window here" opens command prompt at the directory location
- Type cmd in the Windows Explorer navigation bar to open cmd prompt in the current directory 
 
## Copy text from Command Prompt
- Using mouse: Right-click title bar > Properties > Options tab > select QuickEdit Mode > OK > Highlight text anywhere in Command Prompt > press Enter > paste text into another program
- Without using mouse: Alt+Space > E > K > move cursor from top-left to desired location > hold Shift + arrow keys > Enter > paste text into another program
 
## Batch Scripts
- Daily Startup Launcher - Startup.bat  

    `@echo off`  
    `start chrome https://osisoft.lightning.force.com/lightning/page/home`  
    `start outlook`  
    `start onenote`  
    `start chrome`  
    `start chrome "https://tsops/""`  
    `timeout /t 1`  
    `start chrome https://supportadmin.osisoft.int/`  
    `timeout /t 1`  
    `start chrome https://chronos.osisoft.int/`  
     `exit`
 
- Backup a folder while automatically including date and time

    `cd /d "DirectoryLocation"`  
    `for /f "tokens=1* delims=" %%a in ("%date%") do "%%a-%%b-%%c"`  
    `ren "FolderName" "FolderName_%date:/=%_%time::=%"`  
    `md "FolderName"`
  
## References for page content
- FilePath = Drive:\Folder\FileName.extension (Note: enclose in double quotes if there are any spaces)
- DirectoryPath = Drive:\Folder\Folder
- <> = text within the < and > is customizable.  The <> characters are not included in the command.
