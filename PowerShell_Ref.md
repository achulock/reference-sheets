## Testing ports
- **New-Object net.sockets.tcpclient("<hostname or IP address>", <port #>)** checks if port is open from current machine to another machine
	- **(New-Object net.sockets.tcpclient).connect("<hostname or IP address>", <port #>)** same as before with a more compact output 
- **Test-NetConnection -ComputerName "<FQDN>" -port <PortNo.>** checks if machine can connect using selected port. Only works on Windows Server 2012 R2 and above
- **$listener = [system.net.sockets.tcplistener]5450;** defines a TCP listener on port 5450, requires the following Start command to activate
	- **$listener.start();** opens the TCP listener
	- **$listener.stop();** closes the TCP listener

## AD User Settings
- Get ALL AD User properties (including delegation settings)  
		`Import-Module ServerManager`  
		`Install-WindowsFeature RSAT-AD-Powershell`  
		`Get-ADUser '<ADAccnt>' -properties * | select * | ConvertTo-Json -Depth 1`  
- Get only delegation settings for AD User  
		`Get-ADUser '<ADAccnt>' -Properties TrustedForDelegation | Select SamAccountName, TrustedForDelegation | FT -A`

## Find installed .NET Framework versions  
  `Get-ChildItem 'HKLM:\SOFTWARE\Microsoft\NET Framework Setup\NDP' -Recurse | Get-ItemProperty -Name Version, Release -ErrorAction 0 | where { $_.PSChildName -match '^(?!S)\p{L}'} | select PSChildName, Version, Release`
