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
•	Set the region (You can let it be default).

•	Change availability options to “No infrastructure redundancy required”.<br>
•	Set Security Type to “Standard”.<br>
•	We are using Windows 10 Pro x64 as the image file.<br>
•	Size used for this project is the default.<br>

<p align="center">
  <img src="https://github.com/mehakashik/Mapping-Live-Cyber-Attacks-Using-Azure-Sentinel/blob/main/Images/1.png">
</p>

