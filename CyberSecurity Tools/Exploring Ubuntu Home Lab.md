1. **Identify Network Interfaces and IP Addresses**

	**Command:** ip *a* or ifconfig

	Purpose: The ifconfig and ip commands display network interface information, like the name of the interface (in my case ens33) and ip addresses on your server.  Note that older interfaces use eth0. It also shows the MAC address and whether or not the interface is active with keywords like UP or DOWN. 

	Tool Explanation: These commands help provide this information. The ip command has various OPTIONS (flags) as shown below. 
	
		ip Syntax: ip [OPTIONS] OBJECT {COMMAND | help}
			1)  ip a (ip address): Shows all IP addresses associated with all network devices
			
		ifconfig Options:
			2)  ifconfig [interface] : Displays the configuration details of the specified network interface
			3) ifconfig : Displays the configuration details of all network interfaces

	Example: The following shows various options for the ip command
	
	<img width="767" height="398" alt="Image" src="https://github.com/user-attachments/assets/6d2f21ca-4bb7-4431-bce3-c53574c083a5" />
	
	


	Example Output: 
	![[Pasted image 20250922112358.png]]

	

	Example Output: 
	
	![[Pasted image 20250922110756.png]]


3. Check Open Ports

	**Command:** sudo netstat -tuln **or** ss -tuln

	Purpose: This command helps monitor and troubleshoot network connections. It will listen to check if any IPs or ports are connected. The ss command serves the same purpose as the netstat command. It is a newer, faster version of nestat.

	Tool Explanation: The netstat command will output information like the protocol that is being used and the state, whether the port is listening or actively connected. 
	
		netstat Options: 
			1) -t : Displays TCP connections
			2) -u : Displays UDP connections
			3) -l : Listening to ports
			4) -n : Displays numerical addresses 

	Example Output:
	![[Pasted image 20250922114225.png]]
	 

4. Analyze Network Connections

	**Command:** sudo lsof -i -P -n
	
	Purpose: Standing for "list open files", this command identifies open files and network connections on a system. It also provides detailed information about the processes that have open files. 

	Tool Explanation:
	
		lsof Options:
			1) -i : Lists all network connections
			2) -P : Shows the port number
			3) -n: Prevents DNS lookups, only IP addresses
			
		Outputs of lsof: 
			4) COMMAND : Command associated with processes that opened that file
			5) PID : Process Identification Number of the process running the file
			6) USER : User executing the process
			7) FD : File descriptor the process uses to associate with the file
			8) TYPE : The file type and ID
			9) DEVICE : The device numbers related to the file
			10) SIZE/OFF : The value of the file taken during runtime
			11) NODE : Local file's node number
			12) NAME : Path or link to file
	
	Example Output: 
	
	![[Pasted image 20250922115832.png]]

5. Perform Network Scanning with Nmap

	**Command:** sudo nmap -sS -O localHost

	Purpose: The Network Mapper, nmap, is a network scanner that will check what ports are open, the processes running, what type of firewalls are in use, and the type of OS. It can be used for security audits.
	>[!warning] 
	>DO NOT use this on any site without permission

	Tool Explanation: Some of the tools will help run a port scan or show the Operating System being used.
	
		nmap Options:
			1) -sS : TCP SYN scan
			2) -O : Enables OS detection

	Example Output:
	
	![[Pasted image 20250922121238.png]]
	
6. Check for Open Ports on the Server's Network

	**Command:** sudo nmap -sP  Machine_Address

	Purpose: This command checks to see if a host is live through a Ping Scan. A newer version of this OPTION is -sn. 

	Tool Explanation: 
	
		nmap Options:
		1) -sp : Ping Scan without port scanning


	Example Output:
	
	![[Pasted image 20250924181836.png]]
		
	
7. Check for Services and Versions

	**Command:** sudo nmap -sV localhost

	Purpose: This command finds out which services are running on each port and its version, which can be checked for vulnerabilities

	Tool Explanation: The command will show the port number, state, service, and version of open ports. 
	
			nmap Options
			1) -sV : Service Version Detection

	Example Output:

	![[Pasted image 20250924182151.png]]
	
8. Identify Potential Vulnerabilities

	**Command:** sudo nmap --script vuln localhost

	Purpose: The nmap command uses the Nmap Scripting Engine (NSE) to automate systems and vulnerability scans. It can identify outdate software. 

	Tool Explanation: The scan will reveal the port, state, service and any vulnerabilities for found in an open port. 
	
		nmap OPTIONS:
		1) --script : tells nmap to run NSE (Nmap Scripting Engine) scripts
		2) vuln : category of NSE scripts

	Example Output:

	![[Pasted image 20250924182331.png]]
	
	
9. Inspect Network Traffic

	**Command:** sudo tcpdump -i eth0

	Purpose: This command allows you to look at packets in real-time, which can be used for network troubleshooting or simply to understand network behaviors

	Tool Explanation: The command is a packet analyzer used to capture and analyze network traffic. It will show the timestamp, protocol, and type of packets.
	
		tcpdump OPTIONS:
			1)  -i : Specifies the network interface it will listen to

	Example Output:

>[!note]
>Use CTRL + C to stop process

	
![[Pasted image 20250924184018.png]]


9. Monitor Network Connection in Real-Time

	**Command:** sudo watch -n 1 netstat -tulnp

	Purpose: With this command, netstat is used to monitor and troubleshoot network connections. With the watch command, you can monitor the network in real time.

	Tool Explanation: The watch runs at a specified interval (using -n), which helps netstat stay updated. In this case, watch ensures it runs every 1 second. 
	
		netstat OPTIONS:
			1) -t : TCP connections
			2) -u : UDP connections
			3) -l : listening
			4) -n : numeric addresses
			5) -p : program name

	Example Output:

	![[Pasted image 20250924183324.png]]


10. Check Firewall Rules
	
	**Command:** sudo ufw status verbose

	Purpose: This command displays firewall configurations on your server as well as which ports and services are allowed or blocked. 

	Tool Explanation:
	
		1) ufw : Uncomplicated Firewall makes firewall configuration easier
		2) status : Current state of firewall
		3) verbose : Shows detailed output

	Example Output:

	>[!note] 
	>Installation of firewall pending

	![[Pasted image 20250924184538.png]]


>[!info] References
>Linux Commands Cheat Sheet
>https://linux-commands.labex.io/
>Nmap Cheat Sheet
>https://www.almabetter.com/bytes/cheat-sheet/nmap



