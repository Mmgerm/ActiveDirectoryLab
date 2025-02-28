# Active Directory Lab Documentation

This page documents the process of setting up an active directoy lab enviornment with:
-A Windows server 2022 with Active Directory
-A Windows 10 machine connected to Active Directory
-An Ubuntu Server with Splunk for log collection
-Sysmon for monitoring of activities on both windows machines

---

#1. Setting up VirtualBox and configuring NAT Network

In order to host the various operating systems on my local machine I had to:
-Download VirtualBox from the internet
-Configure a NAT network inside VirtualBox
-Download and load the ISO files for Windows 10, Windows Server, and Ubuntu Server into VirtualBox and configure each machine with the proper amount of storage, memory, and processors needed to run properly
-Configure each machine to be on the same NAT network by clicking Settings->Network->Attached to: NAT Network->Name: AD Project

---

#2. Setting up and configuring Windows Server and Active Directory

In order to setup and configure Windows Server and Active Directory I had to:
-Open Windows Server in VirtulBox and complete initial setup process
-Setup a static IPV4 address with correct subnet mask and default gateway
-Installed Active Directory Domain Services (AD DS) using the Server Manager Dashboard
-Configured AD DS by selecting the "Add New Forest" deployment option, and setting a root domain name to establish a new environment
-Created Organizational Units to simulate a real world environment including HR, IT, etc.
-Created groups with modified permissions
-Added new users to groups to manage their permissions

#3 Setting up and configuring Windows 10 and Adding it to Active Directory Domain

In order to setup and configure the Windows 10 machine, and add it to the Active Directory I had to:
-Open Windows 10 in VirtualBox and complete initial setup process
-Setup a static IPV4 address with correct subnet mask and default gateway
-Change the domain of the system to the domain of the Active Directory
-Restart PC
-Login as any user in the Active Directory server to verify successful setup

#4 Setting up and configuring Ubuntu Server with Splunk

In order to setup and configure the Ubuntu Server with Splunk I had to:
-Open Ubuntu Server in VirtualBox and complete initial setup process
-Setup a static IPv4 by disabling DHCP, entering proper IPv4 information, and setting up DNS to be able to easily ping the server from other devices for testing connection
-Download Splunk Enterprise on local machine and open it on the Ubuntu Server by using VirtualBox shared folders
-Run the Splunk installer and set server to run Splunk on startup, and login as the user Splunk to be able to access it

#5 Setting up Splunk Universal Forwarder and Sysmon on Windows Server and Windows 10 machines

In order to setup both of my machines to forward their logs to Splunk I had to:
-Open a web browser and go to the IP of the Splunk server on port 8000 to ensure connection between the machine and Splunk server
-Install Splunk Universal forwarder
-Run installer and ensure that the machine is sending traffic to the IP of the Splunk server and that it is sending it to the correct port (9997)
-Created an inputs.conf file with information of the name of the machine and the logs I want to sent to the Splunk server
-Placed it in the /etc/system/local location in the splunk forwarder folder
-Completed these steps for both mt Windows 10 and Windows Servers machines, with different info in the splunk inputs.conf file to specify the name of the machine it is coming from

In order to setup Sysmon on both of my mcahines I had to: 
-Download Sysmon and install it on the machine
-Download config file for Sysmon (I used this one: https://github.com/olafhartong/sysmon-modular)
-Run Sysmon using the downloaded config file (I did this using PowerShell)

#6 Setting Up Splunk to Recieve the Logs from my Machines

In order to setup Splunk to recieve logs from both of my machines I had to:
-Open a web browser and go to the proper IP and port of the Splunk user interface
-Go to the "Indexes" section and add the index that was specified in ine inputs.conf file in both of my machines
-Set Splunk to recieve traffic from the port that was specified in the installation of Splunk on both of my machines (9997)
-Check to ensure that Splunk is recieving traffic from both of the new indexes that were just created
