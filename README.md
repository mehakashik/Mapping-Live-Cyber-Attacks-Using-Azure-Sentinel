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
  <img width="460" height="460" src="https://github.com/mehakashik/Mapping-Live-Cyber-Attacks-Using-Azure-Sentinel/blob/main/Images/6.png">
</p>

## Defender Plans
