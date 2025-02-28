# Active Directory Lab Documentation

This page documents the process of setting up an active directory lab environment with:

- A Windows Server 2022 with Active Directory
- A Windows 10 machine connected to Active Directory
- An Ubuntu Server with Splunk for log collection
- Sysmon for monitoring activities on both Windows machines

---

## Lab Diagram

You can view a diagram of the lab setup here:

[View Server Diagram (PDF)](Server_Diagram.pdf)

---

## 1. Setting up VirtualBox and Configuring NAT Network

In order to host the various operating systems on my local machine, I had to:

- Download VirtualBox from the internet
- Configure a NAT network inside VirtualBox
- Download and load the ISO files for Windows 10, Windows Server, and Ubuntu Server into VirtualBox and configure each machine with the proper amount of storage, memory, and processors needed to run properly
- Configure each machine to be on the same NAT network by clicking `Settings -> Network -> Attached to: NAT Network -> Name: AD Project`

---

## 2. Setting up and Configuring Windows Server and Active Directory

In order to set up and configure Windows Server and Active Directory, I had to:

- Open Windows Server in VirtualBox and complete the initial setup process
- Set up a static IPV4 address with the correct subnet mask and default gateway
- Install Active Directory Domain Services (AD DS) using the Server Manager Dashboard
- Configure AD DS by selecting the "Add New Forest" deployment option, and setting a root domain name to establish a new environment
- Create Organizational Units to simulate a real-world environment including HR, IT, etc.
- Create groups with modified permissions
- Add new users to groups to manage their permissions

---

## 3. Setting up and Configuring Windows 10 and Adding it to Active Directory Domain

In order to set up and configure the Windows 10 machine and add it to the Active Directory, I had to:

- Open Windows 10 in VirtualBox and complete the initial setup process
- Set up a static IPV4 address with the correct subnet mask and default gateway
- Change the domain of the system to the domain of the Active Directory
- Restart the PC
- Log in as any user in the Active Directory server to verify successful setup

---

## 4. Setting up and Configuring Ubuntu Server with Splunk

In order to set up and configure the Ubuntu Server with Splunk, I had to:

- Open Ubuntu Server in VirtualBox and complete the initial setup process
- Set up a static IPv4 by disabling DHCP, entering proper IPv4 information, and setting up DNS to be able to easily ping the server from other devices for testing connection
- Download Splunk Enterprise on my local machine and open it on the Ubuntu Server by using VirtualBox shared folders
- Run the Splunk installer and set the server to run Splunk on startup, and log in as the user "Splunk" to be able to access it

---

## 5. Setting up Splunk Universal Forwarder and Sysmon on Windows Server and Windows 10 Machines

In order to set up both of my machines to forward their logs to Splunk, I had to:

- Open a web browser and go to the IP of the Splunk server on port 8000 to ensure connection between the machine and Splunk server
- Install Splunk Universal Forwarder
- Run the installer and ensure that the machine is sending traffic to the IP of the Splunk server and that it is sending it to the correct port (9997)
- Create an `inputs.conf` file with information about the name of the machine and the logs I want to send to the Splunk server
- Place it in the `/etc/system/local` location in the Splunk forwarder folder
- Complete these steps for both my Windows 10 and Windows Server machines, with different info in the Splunk `inputs.conf` file to specify the name of the machine it is coming from

In order to set up Sysmon on both of my machines, I had to:

- Download Sysmon and install it on the machine
- Download the config file for Sysmon (I used this one: [https://github.com/olafhartong/sysmon-modular](https://github.com/olafhartong/sysmon-modular))
- Run Sysmon using the downloaded config file (I did this using PowerShell)

---

## 6. Setting Up Splunk to Receive the Logs from my Machines

In order to set up Splunk to receive logs from both of my machines, I had to:

- Open a web browser and go to the proper IP and port of the Splunk user interface
- Go to the "Indexes" section and add the index that was specified in the `inputs.conf` file in both of my machines
- Set Splunk to receive traffic from the port that was specified in the installation of Splunk on both of my machines (9997)
- Check to ensure that Splunk is receiving traffic from both of the new indexes that were just created

