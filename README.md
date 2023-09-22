# Mapping-Live-Cyber-Attacks-Using-Azure-Sentinel
Used Microsoft Sentinel, PowerShell Scripts, Log Analytics Workspaces &amp; Virtual Machine in order to obtain geolocation data about brute force attacks and pin them on the map.

# Project Outline
&emsp;&emsp;The project's core focus revolved around harnessing Azure Sentinel to monitor and track instances of failed remote desktop login attempts. This task involved the creation of a PowerShell script, designed to interface with an API, enabling the retrieval of location data linked to the IP addresses associated with these login failures. Subsequently, this location data was graphically represented on a map, offering a visual overview of the attempted security breaches. The overarching goal of this initiative was to elevate the organization's security posture by gaining valuable insights into the origins of these breach attempts. In summation, this project contributes significantly to a more comprehensive understanding of security incidents.

# Index

Creating a Virtual Machine in Azure  
- Configuring the Virtual Machine  
- Administrator Control  
- Networking  

Creating & configuring a Log Analytics Workspace  <br>

Windows Defender for Cloud  
- Defender Plans 
- Data Collection 

Connecting Log Analytics Workspace to Virtual Machine <br>

Microsoft Azure Sentinel  <br>

Login to your Virtual Machine  
- Event Viewer
- Windows Defender Firewall Settings
  
Powershell Script and API  <br>

Creating Custom Log  <br>
- Security Events Query  <br>
- Failed RDP logins Query  <br>

Setting up Maps in Azure  <br>
- Creating a workbook  <br>
- Map Visualization  <br>

Takeaways  <br>

Reference and Gratitude  <br>

# Creating a Virtual Machine in Azure
Login to your azure account and create a new virtual machine.

## Configuring the Virtual Machine
•	Create a name for the resource group.<br>
•	Name your virtual machine.<br>
•	Set the region (You can let it be default).<br>
•	Change availability options to “No infrastructure redundancy required”.<br>
•	Set Security Type to “Standard”.<br>
•	We are using Windows 10 Pro x64 as the image file.<br>
•	Size used for this project is the default.<br>

<p align="center">
  <img width="460" height="460" src="https://github.com/mehakashik/Mapping-Live-Cyber-Attacks-Using-Azure-Sentinel/blob/main/Images/1.png">
</p>

## Administrator Control
•	Set username and password. (Do not make it easy to brute force).<br>
•	Set Public inbound ports to “Allow selected ports”.<br>
•	Set Select Inbound ports to “RDP (3389)”.<br>
•	Confirm your eligibility.<br>
•	Then click next and move on to “Networking” leaving “Disks” page at default selections.<br>

<p align="center">
  <img width="460" height="460" src="https://github.com/mehakashik/Mapping-Live-Cyber-Attacks-Using-Azure-Sentinel/blob/main/Images/2.png">
</p>

## Networking
•	Set NIC network security group to “Advanced” and create a new inbound rule and replace the old one. <br>

<p align="center">
  <img width="460" height="460" src="https://github.com/mehakashik/Mapping-Live-Cyber-Attacks-Using-Azure-Sentinel/blob/main/Images/3.png">
</p>

•	Set destination port range to “ * ” and set priority to a lower number like 100. <br>
•	Name the rule anything you want. <br>

<p align="center">
  <img src="https://github.com/mehakashik/Mapping-Live-Cyber-Attacks-Using-Azure-Sentinel/blob/main/Images/4.png">
</p>

•	Confirm everything and create the virtual machine. <br>

# Creating & configuring a Log Analytics Workspace
Establish a connection between the virtual machine logs and Azure Logs Analytics, while also configuring a custom log to identify its source. <br>
•	Search for log analytics workspace on the search bar.<br>
•	Create a new resource group and name the instance (you can name them as you wish).<br>
•	The region can be set to the default selection.<br>
•	Proceed to review and create the log analytics wokspace.<br>

<p align="center">
  <img width="460" height="460" src="https://github.com/mehakashik/Mapping-Live-Cyber-Attacks-Using-Azure-Sentinel/blob/main/Images/5.png">
</p>

# Windows Defender for Cloud
We will enable the ability to gather logs from the virtual machine into the log analytics workspace by configuring Windows Defender for Cloud. <br>
•	Search for Windows Defender for Cloud in the Search Bar. <br>
•	Navigate to Environment Settings and select the log analytics workspace that your created. <br>

<p align="center">
  <img src="https://github.com/mehakashik/Mapping-Live-Cyber-Attacks-Using-Azure-Sentinel/blob/main/Images/6.png">
</p>

## Defender Plans
•	Turn Foundational CSPM and Servers “On” and let SQL Servers remain “Off”. <br>

<p align="center">
  <img src="https://github.com/mehakashik/Mapping-Live-Cyber-Attacks-Using-Azure-Sentinel/blob/main/Images/7.png">
</p>

## Data Collection
•	Move to Data Collection and select “All Events” which will audit, investigate, and analyze threats from all Windows Security and AppLocker Events. <br>

<p align="center">
  <img src="https://github.com/mehakashik/Mapping-Live-Cyber-Attacks-Using-Azure-Sentinel/blob/main/Images/8.png">
</p>

# Connecting Log Analytics Workspace to Virtual Machine
•	To establish a connection between the workspace and the virtual machine visit the log analytics workspace that was created before (i.e., law-honeypotlab1) in this case and search for virtual machines in it. <br>

<p align="center">
  <img src="https://github.com/mehakashik/Mapping-Live-Cyber-Attacks-Using-Azure-Sentinel/blob/main/Images/9.png">
</p>

•	Select the previously created virtual machine and proceed to connect it to the log analytics workspace.<br>

<p align="center">
  <img src="https://github.com/mehakashik/Mapping-Live-Cyber-Attacks-Using-Azure-Sentinel/blob/main/Images/10.png">
</p>

# Microsoft Azure Sentinel
Search for Microsoft Sentinel in the search bar and proceed to connect the log analytics workspace that we created with Sentinel.

<p align="center">
  <img src="https://github.com/mehakashik/Mapping-Live-Cyber-Attacks-Using-Azure-Sentinel/blob/main/Images/11.png">
</p>

# Login to your Virtual Machine
•	Navigate to your virtual machine and find its public ip address which we will use to remotely login to the machine.

<p align="center">
  <img src="https://github.com/mehakashik/Mapping-Live-Cyber-Attacks-Using-Azure-Sentinel/blob/main/Images/12.png">
</p>

•	Open a remote desktop connection using the public ip address we copied. Proceed to input the username and password that we used to create the VM in the beginning.

<p align="center">
  <img width="460" height="460" src="https://github.com/mehakashik/Mapping-Live-Cyber-Attacks-Using-Azure-Sentinel/blob/main/Images/13.png">
</p>

## Event Viewer
Our primary focus will be on Event ID 4645, which signifies a failed login attempt. You can filter the logs to specifically identify these unsuccessful login endeavors. Since our machine is now exposed to the external world, it's likely that once discovered, people will attempt to log in or use brute force methods. <br>
•	Open the Event Viewer in your VM and navigate to Windows Log>Security. <br>

<p align="center">
  <img src="https://github.com/mehakashik/Mapping-Live-Cyber-Attacks-Using-Azure-Sentinel/blob/main/Images/14.png">
</p>
•	Here you can see the failed login attempts with Event ID 4625.  You can obtain more details about the event by clicking on it.

## Windows Defender Firewall Settings
•	Navigate to your search bar and search for “wf.msc” which will open windows firewall. <br>
•	Open Windows Defender Firewall Properties and turn off firewall on Domain, Private and Public profile.	This will expose the machine to everyone.
<p align="center">
  <img src="https://github.com/mehakashik/Mapping-Live-Cyber-Attacks-Using-Azure-Sentinel/blob/main/Images/15.png">
</p>

# PowerShell Script and API
A custom PowerShell ISE script is used to obtain geolocation data from an API ( https://ipgeolocation.io/ ) <br>
•	Open PowerShell ISE in the VM and paste the script in a new file. <br>
•	Within the script, there are examples of unsuccessful login attempts. This script collects the geographical location data associated with these failed login attempts and generates custom log entries for these failures. <br>
The custom script is available here: [Log Exporter](https://github.com/mehakashik/Mapping-Live-Cyber-Attacks-Using-Azure-Sentinel/blob/main/Log_Exporter.ps1) <br>

The API key in the script is unique to every user and can be obtained by making an account on https://ipgeolocation.io/ . Change the value in the script once the key is obtained or you will not receive geolocation data.
<p align="center">
  <img src="https://github.com/mehakashik/Mapping-Live-Cyber-Attacks-Using-Azure-Sentinel/blob/main/Images/16.png">
</p>

The data highlighted in pink gives you information about the failed logon attempts. The attempts you see above were test attempts. <br>
The log is then stored in C:\ProgramData\failed_rdp.log. The initial entries will consist of sample data, which serves as a training dataset for the analytics workspace, followed by the inclusion of actual, real-world data. <br>
<p align="center">
  <img src="https://github.com/mehakashik/Mapping-Live-Cyber-Attacks-Using-Azure-Sentinel/blob/main/Images/17.png">
</p>

# Creating Custom Logs
Now we navigate back to “ law-honeypotlab1” the log analytics workspace that we created and proceed to create a new custom log.
<p align="center">
  <img src="https://github.com/mehakashik/Mapping-Live-Cyber-Attacks-Using-Azure-Sentinel/blob/main/Images/18.png">
</p>

•	Select “New custom log (MMA-based)” under Create.<br>
•	Upload the sample log file that was created “failed_rdp.log” and mention the file path as your move forward.<br>
•	Name the custom log file. In this case it is FAILED_RDP_WITH_GEO.<br>
•	Proceed to review the file and create. <br>
<p align="center">
  <img src="https://github.com/mehakashik/Mapping-Live-Cyber-Attacks-Using-Azure-Sentinel/blob/main/Images/19.png">
</p>

## Security Events Query
•	Navigate to Logs and run the query : SecurityEvent | where EventID == 4625.<br>
•	This query will display all attempted failed logon events as shown in the image below.<br>
<p align="center">
  <img src="https://github.com/mehakashik/Mapping-Live-Cyber-Attacks-Using-Azure-Sentinel/blob/main/Images/20.png">
</p>

## Failed RDP logins Query
To obtain more information like the country, ip address, destination, username etc. we run the query: FAILED_RDP_WITH_GEO_CL.
<p align="center">
  <img src="https://github.com/mehakashik/Mapping-Live-Cyber-Attacks-Using-Azure-Sentinel/blob/main/Images/21.png">
</p>
But the information is cluttered so we add a few more lines to bring clarity to the raw data. <br>

<p align="center">
  <img src="https://github.com/mehakashik/Mapping-Live-Cyber-Attacks-Using-Azure-Sentinel/blob/main/Images/22.png">
</p>

The custom log query is available here: [Custom Log](https://github.com/mehakashik/Mapping-Live-Cyber-Attacks-Using-Azure-Sentinel/blob/main/custom%20log%20query.txt )

# Setting up Maps in Microsoft Sentinel
## Creating a workbook
•	Here we navigate to Microsoft Sentinel>Workbooks>Add Workbook
<p align="center">
  <img src="https://github.com/mehakashik/Mapping-Live-Cyber-Attacks-Using-Azure-Sentinel/blob/main/Images/23.png">
</p>
•	Proceed to remove previous workbook widgets and select “Add query”. <br>
•	Now run the custom log query that we created before here.<br>

<p align="center">
  <img src="https://github.com/mehakashik/Mapping-Live-Cyber-Attacks-Using-Azure-Sentinel/blob/main/Images/24.png">
</p>

## Map Visualization
To view the map with the geolocation data of the attempted logon attempts change the visualization drop down to map and size to full.

<p align="center">
  <img src="https://github.com/mehakashik/Mapping-Live-Cyber-Attacks-Using-Azure-Sentinel/blob/main/Images/25.png">
</p>







