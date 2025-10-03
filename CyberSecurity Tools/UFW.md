I. Enable UFW (Uncomplicated Firewall)

1)	Check the status of UFW
	Command: sudo UFW status 
	
	![Image](https://github.com/user-attachments/assets/7c1ee0e3-4563-4b89-a752-41caeb898208)
	
2) Check to make sure your connection to SSH is allowed
	
	![Image](https://github.com/user-attachments/assets/f797cd57-7d34-49a0-b70f-8bc912cdb8ca)


>[!note] 	
>	The default policy of UFW denies any incoming traffic and only allows outgoing traffic. Before enabling UFW, you should allow traffic through port 22 or else the connection will drop and you will be unable to connect to the server via SSH. 
	
3) Socket Statistics checks network statistics.
   
	Command: sudo ss -tuln  Socket Statistics checks network statistics
			1) t : TCP
			2) u: UPD
			3) l : Listening
			4) n: displays address in numeric form

![Image](https://github.com/user-attachments/assets/5a2816a4-6ef6-4d2e-813a-55bf9eb7b93c)

	Check specific service of that port			
	Command: sudo lsof -i :*portNumber*  
	
![[Pasted image 20251002124919.png]]

4) Enable UFW

	Command: sudo ufw enable
	
![Image](https://github.com/user-attachments/assets/2b0c9280-2ad7-49c5-8af6-044f0c64fede)

5) Check the status 

	Command: sudo ufw status
	
	![[Pasted image 20251002142746.png]]


>[!note] 	
>	If your server is a web server, you should allow port 80 for HTTP and port 443 for HTTPS.

6) Check the status using the verbose command
	Command: sudo ufw status verbose


>[!note] 	
>	The command shows the default policies for UFW. In this case, it denies all incoming traffic and allows outgoing traffic. 

7)  Blocking an IP Address
	Command: sudo ufw deny from <*ip address*>
		Example: sudo ufw deny from 10.0.0.0
	
8) Allow Access by specific port and IP Address
	Command: sudo ufw allow from <*target*> to <*destination*> port <*port number*>
		Example: sudo ufw allow from 192.168.1.50 to any port 587

>[!note] 	
>	Port 587 is used for secure email submission

![Image](https://github.com/user-attachments/assets/cb073f5b-a2b9-430f-86b8-e9a9a06443c0)


II. Enable UFW Logging

1) Ensure that UFW logging is enabled
![Image](https://github.com/user-attachments/assets/b2acafd7-ba34-420c-8550-bc92b8eaba17)

2) If you need more detailed or less verbose logs, change the logging levels.

	Command: sudo ufw logging *level*
	1) low : minimal logging, mainly for blocked incoming packets
	2) medium : includes blocked incoming packets with additional packet header details
	3) high : includes all blocked packets and connection information
	4) full : extensive logging of all UFW events
	
	![Image](https://github.com/user-attachments/assets/9b96e245-8d8d-43ca-b8ea-6e52a3a39e85)


3) Logging Details

	1) MAC: Source MAC address of the traffic - MAC=aa:bb:cc:dd:ee:ff
	2) SRC: Source IP address of the traffic - SRC=192.168.1.100
	3) DST: Destination IP address - DST=192.168.1.50
	4) SPT: Source port - SPT=12345
	5) DPT: Destination port - DPT=80
	6) PROTO: Protocol used (e.g., TCP, UDP) - PROTO=TCP
	7) UFW BLOCK: Indicates that the packet was blocked by UFW
	
![Image](https://github.com/user-attachments/assets/ec0b5b9c-5c3c-43b4-a2ef-a4bc78c5e64e)

>[!note] 	
>	This information can provide insight into system activities, analyzing system errors, and detect security incidents. 

4)  Viewing logs in the VM
	Command: sudo tail -f /var/log/ufw.log
	1) tail : views the end of files
	2) -f : monitors log files in real time

	![Image](https://github.com/user-attachments/assets/de8fc9a0-554b-4165-9958-c84818756618)


>[!note] 	
>	Use Ctrl + C to terminate command

5) Filter Specific Entries Using the GREP command
	Command for denied traffic: sudo grep 'DENY' /var/log/ufw.log
	
![Image](https://github.com/user-attachments/assets/d6e0fe33-d5db-4e3a-989e-d3fddcfe8cef)
	Command for allowed traffic: sudo grep 'ALLOW' /var/log/ufw.log

![Image](https://github.com/user-attachments/assets/fcf362ad-33f3-4cf2-8d35-19c1c9385249)

>[!note] 	
>	There is no output for DENY. Recall that the default policy for UFW is to deny incoming traffic unless a rule indicates otherwise. In this example, there was no indication of any incoming traffic. 



>[!info] References
>UFW
>https://help.ubuntu.com/community/UFW#Allow_and_Deny_.28specific_rules.29 


