<h1>Lab Setup</h1>

<h2>Description</h2>
Building the Malware Analysis Lab
<br />

<h2>Necessary ISOs</h2>
- <a href="https://info.microsoft.com/ww-landing-windows-11-enterprise.html"><b>Windows 11 Enterprise</b></a></br>
- <a href="https://app.box.com/s/am8a5gmibsw8dj6xn2x0thxes6a46bp6"><b>Remnux</b></a>

<h2>Other Items</h2>
- <a href="https://github.com/mandiant/flare-vm"><b>Flare-VM</b></a></br>
- <a href="https://github.com/HuskyHacks/PMAT-labs"><b>PMAT Labs</b></a>

<h2>Building The Lab</h2>
- Download the necessary ISOs and create the associated Virtual Machines (Windows 11 and Remux). </br>
- (Optional) Download and Install the Virtual Box Guest Edition. </br>
- Remnux is setup out of the box for the lab </br>
- Create Flare-VM with Windows 11 VM
  - Download Windows Terminal from Windows Store
  - Disable Proxy Auto Detect (Search Proxy Settings) 
  - Disable Tamper Protection (Search Defender)
  - Disable AV/Defender in GPO (GPEdit)
    - Administrative Templates → Windows Components → Microsoft Defender Antivirus → Enable “Turn off Microsoft Defender Antivirus”</br>
  - Disable Windows Firewall in GPO (GPEdit)</br>
    - Administrative Templates → Network → Network Connections → Windows Defender Firewall → Domain/Standard Profile → Disable “Protect All Network Connections”</br>
  - Run the following commands to setup Flare-VM:</br>
<code>(New-Object net.webclient).DownloadFile('https://raw.githubusercontent.com/mandiant/flare-vm/main/install.ps1',"$([Environment]::GetFolderPath("Desktop"))\install.ps1")
Unblock-File .\install.ps1
Set-ExecutionPolicy Unrestricted
.\install.ps1 -customConfig https://raw.githubusercontent.com/HuskyHacks/PMAT-labs/main/config.xml</code></br>
- Create a Snapshot of the VM post-Flare install.</br>

This may take a while to full install all tools. Also, you will need to pull your Malware for analysis from a trustworthy source (Recommend prior to Flare-VM install. I struggled to pull down malware after install).

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
