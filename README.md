# Enumeration
Enumeration creates an active connection with the system and performs directed queries to gain more information about the target. It extracts lists of computers, usernames, user groups, ports, OSes, machine names, network resources, and services using various techniques. Enumeration techniques are conducted in an intranet environment.

Objective
The objective of the lab is to extract information about the target organization that includes, but is not limited to:
- Machine names, their OSes, services, and ports
- Network resources
- Usernames and user groups
- Lists of shares on individual hosts on the network
- Policies and passwords
- Routing tables
- Audit and service settings
- SNMP and FQDN details

Ethical hackers or penetration testers use several tools and techniques to enumerate the target network. Recommended labs that i used in learning various enumeration techniques include:

1. Perform NetBIOS enumeration
 - Perform NetBIOS enumeration using Windows command-line utilities

2. Perform SNMP enumeration
 - Perform SNMP enumeration using SnmpWalk

3. Perform LDAP enumeration
 - Perform LDAP enumeration using Active Directory Explorer (AD Explorer)

4. Perform NFS enumeration
 - Perform NFS enumeration using RPCScan and SuperEnum

5. Perform DNS enumeration
 - Perform DNS enumeration using zone transfer

6. Perform SMTP enumeration
 - Perform SMTP enumeration using Nmap

7. Perform enumeration using various enumeration tools
 - Enumerate information using Global Network Inventory

# Lab 1: Perform NetBIOS Enumeration

Task 1: Perform NetBIOS Enumeration using Windows Command-Line Utilities
Nbtstat helps in troubleshooting NETBIOS name resolution problems. The nbtstat command removes and corrects preloaded entries using several case-sensitive switches. Nbtstat can be used to enumerate information such as NetBIOS over TCP/IP (NetBT) protocol statistics, NetBIOS name tables for both the local and remote computers, and the NetBIOS name cache.
Net use connects a computer to, or disconnects it from, a shared resource. It also displays information about computer connections.
Here, i will use the Nbtstat, and Net use Windows command-line utilities to perform NetBIOS enumeration on the target network.

1. By default, Windows 11 machine is selected. Click Windows Server 2019 to switch to the Windows Server 2019 machine
2. Open a Command Prompt window and run nbtstat -a [IP address of the remote machine] command (here, the target IP address is 10.10.1.11).
3. The result appears, displaying the NetBIOS name table of a remote computer (here, the WINDOWS11 machine), as shown in the screenshot.
![image alt](https://github.com/asyrafzf95/Enumeration/blob/914283eb5101d2e901b172ddee778536b124e403/images/1.jpg)
4. In the same Command Prompt window, run nbtstat -c command.
5. The result appears, displaying the contents of the NetBIOS name cache, the table of NetBIOS names, and their resolved IP addresses.
![image alt](https://github.com/asyrafzf95/Enumeration/blob/914283eb5101d2e901b172ddee778536b124e403/images/2.jpg)
6. Now, run net use command. The output displays information about the target such as connection status, shared folder/drive and network information, as shown in the screenshot.
![image alt](https://github.com/asyrafzf95/Enumeration/blob/914283eb5101d2e901b172ddee778536b124e403/images/3.jpg)

# Lab 2: Perform SNMP Enumeration

Task 1: Perform SNMP Enumeration using SnmpWalk
SnmpWalk is a command line tool that scans numerous SNMP nodes instantly and identifies a set of variables that are available for accessing the target network. It is issued to the root node so that the information from all the sub nodes such as routers and switches can be fetched.
Here, i will use SnmpWalk to perform SNMP enumeration on a target system.

1. Click Parrot Security to switch to the Parrot Security machine. Login with attacker/toor, open a Terminal window and execute sudo su to run the programs as a root user.
2. Run snmpwalk -v1 -c public [target IP] command (here, the target IP address is 10.10.1.22).
3. The result displays all the OIDs, variables and other associated information.
![image alt](https://github.com/asyrafzf95/Enumeration/blob/914283eb5101d2e901b172ddee778536b124e403/images/4.jpg)
4. Run snmpwalk -v2c -c public [Target IP Address] command to perform SNMPv2 enumeration on the target machine (here, the target IP address is 10.10.1.22).
5. The result displays data transmitted from the SNMP agent to the SNMP server, including information on server, user credentials, and other parameters.
![image alt](https://github.com/asyrafzf95/Enumeration/blob/914283eb5101d2e901b172ddee778536b124e403/images/5.jpg)

# Lab 3: Perform LDAP Enumeration

Task 1: Perform LDAP Enumeration using Active Directory Explorer (AD Explorer)
Active Directory Explorer (AD Explorer) is an advanced Active Directory (AD) viewer and editor. It can be used to navigate an AD database easily, define favorite locations, view object properties and attributes without having to open dialog boxes, edit permissions, view an object's schema, and execute sophisticated searches that can be saved and re-executed.
Here, i will use the AD Explorer to perform LDAP enumeration on an AD domain and modify the domain user accounts.

1. Click Windows Server 2019 to switch to the Windows Server 2019 machine and click Ctrl+Alt+Delete to activate the machine.
2. Navigate to Z:\CEHv13 Module 04 Enumeration\LDAP Enumeration Tools\Active Directory Explorer and double-click ADExplorer.exe.
3. The Connect to Active Directory pop-up appears; type the IP address of the target in the Connect to field (here, we are targeting the Windows Server 2022 machine: 10.10.1.22) and click OK.
![image alt](https://github.com/asyrafzf95/Enumeration/blob/914283eb5101d2e901b172ddee778536b124e403/images/6.jpg)
4. The Active Directory Explorer displays the active directory structure in the left pane, as shown in the screenshot.
![image alt](https://github.com/asyrafzf95/Enumeration/blob/914283eb5101d2e901b172ddee778536b124e403/images/7..jpg)
5. Now, expand DC=CEH, DC=com, and CN=Users by clicking "+" to explore domain user details.
![image alt](https://github.com/asyrafzf95/Enumeration/blob/914283eb5101d2e901b172ddee778536b124e403/images/8.jpg)
6. Click any username (in the left pane) to display its properties in the right pane.
![image alt](https://github.com/asyrafzf95/Enumeration/blob/914283eb5101d2e901b172ddee778536b124e403/images/9.jpg)
7. Right-click any attribute in the right pane (here, displayName) and click Modify… from the context menu to modify the user's profile.
![image alt](https://github.com/asyrafzf95/Enumeration/blob/914283eb5101d2e901b172ddee778536b124e403/images/10.jpg)
8. The Modify Attribute window appears. First, select the username under the Value section, and then click the Modify… button. The Edit Value pop-up appears. Rename the username in the Value data field and click OK to save the changes.

# Lab 4: Perform NFS Enumeration

Task 1: Perform NFS Enumeration using RPCScan and SuperEnum
RPCScan communicates with RPC (remote procedure call) services and checks misconfigurations on NFS shares. It lists RPC services, mountpoints,and directories accessible via NFS. It can also recursively list NFS shares. SuperEnum includes a script that performs a basic enumeration of any open port, including the NFS port (2049).
Here, i will use RPCScan and SuperEnum to enumerate NFS services running on the target machine.

1. Click Windows Server 2019 to switch to the Windows Server 2019 machine. In the Windows Server 2019 machine, click the Start button at the bottom-left corner of Desktop and open Server Manager.
2. The Server Manager main window appears. By default, Dashboard will be selected; click Add roles and features.
![image alt](https://github.com/asyrafzf95/Enumeration/blob/914283eb5101d2e901b172ddee778536b124e403/images/11.jpg)
3. The Add Roles and Features Wizard window appears. Click Next here and in the Installation Type and Server Selection wizards.
4. The Server Roles section appears. Expand File and Storage Services and select the checkbox for Server for NFS under the File and iSCSI Services option, as shown in the screenshot. Click Next.
![image alt](https://github.com/asyrafzf95/Enumeration/blob/914283eb5101d2e901b172ddee778536b124e403/images/12.jpg)
![image alt](https://github.com/asyrafzf95/Enumeration/blob/914283eb5101d2e901b172ddee778536b124e403/images/13.jpg)
5. In the Features section, click Next. The Confirmation section appears; click Install to install the selected features.
6. The features begin installing, with progress shown by the Feature installation status bar. When installation completes, click Close.
7. Having enabled the NFS service, it is necessary to check if it is running on the target system (Windows Server 2019). In order to do this, we will use Parrot Security machine.
8. Click Parrot Security to switch to the Parrot Security machine. Open a Terminal window and execute sudo su to run the programs as a root user
9. Execute nmap -p 2049 [Target IP Address] command (here the target IP address is , 10.10.1.19).
10. The scan result appears indicating that port 2049 is opened, and the NFS service is running on it, as shown in the screenshot.
![image alt](https://github.com/asyrafzf95/Enumeration/blob/914283eb5101d2e901b172ddee778536b124e403/images/14.jpg)
11. Run cd SuperEnum command to navigate to the SuperEnum folder.
12. Run echo "10.10.1.19" >> Target.txt command to create a file having a target machine's IP address (10.10.1.19).
![image alt](https://github.com/asyrafzf95/Enumeration/blob/914283eb5101d2e901b172ddee778536b124e403/images/15.jpg)
13. Execute ./superenum command. Under Enter IP List filename with path, type Target.txt, and press Enter.
![image alt](https://github.com/asyrafzf95/Enumeration/blob/914283eb5101d2e901b172ddee778536b124e403/images/16.jpg)
14. The script starts scanning the target IP address for open NFS and other services.
15. After the scan is finished, scroll down to review the results. Observe that the port 2049 is open and the NFS service is running on it.
![image alt](https://github.com/asyrafzf95/Enumeration/blob/914283eb5101d2e901b172ddee778536b124e403/images/17.jpg)
16. Now, i will perform NFS enumeration using RPCScan. To do so, run cd RPCScan command.
17. Execute python3 rpc-scan.py [Target IP address] --rpc command (here, the target IP address is 10.10.1.19, the Windows Server 2019 machine).
18. The result appears, displaying that port 2049 is open, and the NFS service is running on it.
![image alt](https://github.com/asyrafzf95/Enumeration/blob/914283eb5101d2e901b172ddee778536b124e403/images/18.jpg)

# Lab 5: Perform DNS Enumeration

Task 1: Perform DNS Enumeration using Zone Transfer
DNS zone transfer is the process of transferring a copy of the DNS zone file from the primary DNS server to a secondary DNS server. In most cases, the DNS server maintains a spare or secondary server for redundancy, which holds all information stored in the main server.
If the DNS transfer setting is enabled on the target DNS server, it will give DNS information; if not, it will return an error saying it has failed or refuses the zone transfer.
Here, i will perform DNS enumeration through zone transfer by using the dig (Linux-based systems) and nslookup (Windows-based systems) utilities.

1. I will begin with DNS enumeration of Linux DNS servers. Click Parrot Security to switch to the Parrot Security machine.
2. Open a Terminal window and execute sudo su to run the programs as a root user
3. Now, run cd command to jump to the root directory.
4. Run dig ns [Target Domain] command (here, the target domain is www.certifiedhacker.com).
5. The above command retrieves information about all the DNS name servers of the target domain.
![image alt](https://github.com/asyrafzf95/Enumeration/blob/914283eb5101d2e901b172ddee778536b124e403/images/19.jpg)
6. Run dig @[NameServer] [Target Domain] axfr command (here, the name server is ns1.bluehost.com and the target domain is www.certifiedhacker.com).
7. The result appears, displaying that the server is available, but that the Transfer failed., as shown in the screenshot.
![image alt](https://github.com/asyrafzf95/Enumeration/blob/914283eb5101d2e901b172ddee778536b124e403/images/20.jpg)
8. After retrieving DNS name server information, the attacker can use one of the servers to test whether the target DNS allows zone transfers or not. here, zone transfers are not allowed for the target domain; this is why the command resulted in the message: Transfer failed. A penetration tester should attempt DNS zone transfers on different domains of the target organization.
9. Now, i will perform DNS enumeration on Windows DNS servers. Click Windows 11 to switch to the Windows 11 machine.
10. Click windows Search icon on the Desktop. Search for cmd in the search field, the Command Prompt appears in the results, click Open to launch it.
11. The Command Prompt window appears; execute command nslookup.
12. In the nslookup interactive mode, execute command set querytype=soa.
13. Type the target domain certifiedhacker.com and press Enter. This resolves the target domain information.
14. The result appears, displaying information about the target domain such as the primary name server and responsible mail addr, as shown in the screenshot.
![image alt](https://github.com/asyrafzf95/Enumeration/blob/914283eb5101d2e901b172ddee778536b124e403/images/21.jpg)
15. In the nslookup interactive mode, execute command ls -d [Name Server] (here, the name is ns1.bluehost.com).
16. The result appears, displaying that the DNS server refused the zone transfer, as shown in the screenshot.
![image alt](https://github.com/asyrafzf95/Enumeration/blob/914283eb5101d2e901b172ddee778536b124e403/images/22.jpg)
17. After retrieving DNS name server information, the attacker can use one of the servers to test whether the target DNS allows zone transfers or not. Here, the zone transfer was refused for the target domain. A penetration tester should attempt DNS zone transfers on different domains of the target organization.

# Lab 6: Perform SMTP Enumeration

Task 1: Perform SMTP Enumeration using Nmap
The Nmap scripting engine can be used to enumerate the SMTP service running on the target system, to obtain information about all the user accounts on the SMTP server.
Here, i will use the Nmap to perform SMTP enumeration.

1. In the Parrot Security machine, open a Terminal window and execute sudo su to run the programs as a root user
2. Run nmap -p 25 --script=smtp-enum-users [Target IP Address] command (here, the target IP address is 10.10.1.19).
3. The result appears displaying a list of all the possible mail users on the target machine (10.10.1.19), as shown in the screenshot below.
![image alt](https://github.com/asyrafzf95/Enumeration/blob/914283eb5101d2e901b172ddee778536b124e403/images/23.jpg)
4. Run nmap -p 25 --script=smtp-open-relay [Target IP Address] command (here, the target IP address is 10.10.1.19).
5. The result appears displaying a list of open SMTP relays on the target machine (10.10.1.19), as shown in the screenshot below.
![image alt](https://github.com/asyrafzf95/Enumeration/blob/914283eb5101d2e901b172ddee778536b124e403/images/24.jpg)
6. Run nmap -p 25 --script=smtp-commands [Target IP Address] command (here, the target IP address is 10.10.1.19).
7. A list of all the SMTP commands available in the Nmap directory appears. You can further explore the commands to obtain more information on the target host.
![image alt](https://github.com/asyrafzf95/Enumeration/blob/914283eb5101d2e901b172ddee778536b124e403/images/25.jpg)
8. Using this information, the attackers can perform password spraying attacks to gain unauthorized access to the user accounts.

# Lab 7: Perform Enumeration using Various Enumeration Tools

Task 1: Enumerate Information using Global Network Inventory
Global Network Inventory is used as an audit scanner in zero deployment and agent-free environments. It scans single or multiple computers by IP range or domain, as defined by the Global Network Inventory host file.
Here, i will use the Global Network Inventory to enumerate various types of data from a target IP address range or single IP.

1. Click Windows 11 to switch to the Windows 11 machine, Click Search icon on the Desktop. Type Global in the search field, the Global Network Inventory appears in the results, click Open to launch it.
![image alt](https://github.com/asyrafzf95/Enumeration/blob/914283eb5101d2e901b172ddee778536b124e403/images/26.jpg)
2. The About Global Network Inventory wizard appears; click I Agree.
![image alt](https://github.com/asyrafzf95/Enumeration/blob/914283eb5101d2e901b172ddee778536b124e403/images/27.jpg)
3. The Global Network Inventory GUI appears. Click Close on the Tip of the Day pop-up.
![image alt](https://github.com/asyrafzf95/Enumeration/blob/914283eb5101d2e901b172ddee778536b124e403/images/28.jpg)
4. The New Audit Wizard window appears; click Next.
![image alt](https://github.com/asyrafzf95/Enumeration/blob/914283eb5101d2e901b172ddee778536b124e403/images/29.jpg)
5. Under the Audit Scan Mode section, click the Single address scan radio button, and then click Next.
![image alt](https://github.com/asyrafzf95/Enumeration/blob/914283eb5101d2e901b172ddee778536b124e403/images/30.jpg)
6. Under the Single Address Scan section, specify the target IP address in the Name field of the Single address option (in this example, the target IP address is 10.10.1.22); Click Next.
![image alt](https://github.com/asyrafzf95/Enumeration/blob/914283eb5101d2e901b172ddee778536b124e403/images/31.jpg)
7. The next section is Authentication Settings; select the Connect as radio button and enter the Windows Server 2022 machine credentials.
![image alt](https://github.com/asyrafzf95/Enumeration/blob/914283eb5101d2e901b172ddee778536b124e403/images/32.jpg)
8. In the final step of the wizard, leave the default settings unchanged and click Finish.
![image alt](https://github.com/asyrafzf95/Enumeration/blob/914283eb5101d2e901b172ddee778536b124e403/images/33.jpg)
9. The Scan progress window will appear.
![image alt](https://github.com/asyrafzf95/Enumeration/blob/914283eb5101d2e901b172ddee778536b124e403/images/34.jpg)
10. The results are displayed when the scan finished. The Scan summary of the scanned target IP address (10.10.1.22) appears.
![image alt](https://github.com/asyrafzf95/Enumeration/blob/914283eb5101d2e901b172ddee778536b124e403/images/35.jpg)
11. Hovered my mouse cursor over the Computer details under the Scan summary tab to view the scan summary, as shown in the screenshot.
![image alt](https://github.com/asyrafzf95/Enumeration/blob/914283eb5101d2e901b172ddee778536b124e403/images/36.jpg)
12. Click the Operating System tab and hover the mouse cursor over Windows details to view the complete details of the machine.
![image alt](https://github.com/asyrafzf95/Enumeration/blob/914283eb5101d2e901b172ddee778536b124e403/images/37.jpg)
13. Click the BIOS tab, and hover the mouse cursor over windows details to display detailed BIOS settings information.
![image alt](https://github.com/asyrafzf95/Enumeration/blob/914283eb5101d2e901b172ddee778536b124e403/images/38.jpg)
14. Click the NetBIOS tab, and hover the mouse cursor over any NetBIOS application to display the detailed NetBIOS information about the target.
![image alt](https://github.com/asyrafzf95/Enumeration/blob/914283eb5101d2e901b172ddee778536b124e403/images/39.jpg)
15. Click the User groups tab and hover the mouse cursor over any username to display detailed user groups information.
![image alt](https://github.com/asyrafzf95/Enumeration/blob/914283eb5101d2e901b172ddee778536b124e403/images/40.jpg)
16. Click the Users tab, and hover the mouse cursor over the username to view login details for the target machine.
![image alt](https://github.com/asyrafzf95/Enumeration/blob/914283eb5101d2e901b172ddee778536b124e403/images/41.jpg)
17. Click the Services tab and hover the mouse cursor over any service to view its details.
![image alt](https://github.com/asyrafzf95/Enumeration/blob/914283eb5101d2e901b172ddee778536b124e403/images/42.jpg)
18. Click the Installed software tab, and hover the mouse cursor over any software to view its details.
![image alt](https://github.com/asyrafzf95/Enumeration/blob/914283eb5101d2e901b172ddee778536b124e403/images/43.jpg)
19. Click the Shares tab, and hover the mouse cursor over any shared folder to view its details.
![image alt](https://github.com/asyrafzf95/Enumeration/blob/914283eb5101d2e901b172ddee778536b124e403/images/44.jpg)
20. Similarly, you can click other tabs such as Computer System, Processors, Main board, Memory, SNMP systems and Hot fixes. Hover the mouse cursor over elements under each tab to view their detailed information.
