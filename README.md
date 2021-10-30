## Step 1 : Download WSA
To download WSA, use
		Link : https://store.rg-adguard.net/
		
		ProductID : 9P3395VX91NR
		Ring : Slow

## Step 2 : Install WSL 2
First go to Optionalfeatures.exe and then enable Windows Subsystem for Linux
and Virtual Machine Platform, then reboot to see the changes.
Then run the wsl2_update.msi to install WSL 2.
If it is shown alredy installed, proceed to the next step.
Finally run the command in Admin PowerShell to set WSL 2 as Default.
	
	wsl --set-default-version 2

## Step 3 : Install Ubuntu and prerequisites
	
Follow this link and install Ubuntu from the Microsoft Store
Link : https://www.microsoft.com/store/productId/9N9TNGVNDL3Q
	
	sudo apt-get update && sudo apt-get upgrade
	
After the installation, open Ubuntu in Windows Terminal, and then run
the following command to install unzip and lzip.

	sudo apt install unzip lzip

## Step 4 : Downloads GApps
Website : https://opengapps.org/
	If your processor is 64 bit Intel or AMD, then select x86_64.
	If your processor is ARM64 then select platform as ARM64.
	Select Android Version as 11.0
	Variant : Pico.

## Step 5 : Extract WSA bundle :
Rename the previously downloaded .msixbundle to .zip and
then extract the ARM64 release msix for ARM64 architecture as I mentioned above.
For Intel or AMD, extract the x64 release msix.
	Now rename the now extracted .msix to .zip and then extract
the contents in a folder Named "WSA".
	Delete the files appxblockmap, appxsignature and [content_types] 
along with the folder appxmetadata

## Step 6 : Download WSA Scripts
In the Ubuntu Terminal go to the folder where the Android contents
are stored and the run this command to download the required scripts
	
	git clone https://github.com/RahulRST/WSA_Script.git
	
Then move the product.img, system.img, vendor.img and system_ext.img
files to the Image Folder in the Scripts from the WSA folder
Then move the gapps zip file to the GApps folder in the Scripts

## Step 7 : Flash GApps
In the Ubuntu Terminal, go to the WSA_Scripts folder and the execute 
the master.sh using the following command

	cd WSA_Scripts
	sudo ./master.sh
	
This script will flash the GApps onto the Windows Subsystem for Android
After this, move the product.img, system.img, vendor.img and system_ext.img
files to the WSA Folder from the Images folder in the Scripts.

## Step 8 : Install WSA
First, enable developer mode in Windows Privacy and Security Settings.
Uninstall previous versions of WSA.
Open PowerShell as Admin and Run the following command to install WSA
	
	Add-AppxPackage -Register path-to-extracted-msix\AppxManifest.xml
(For example : Add-AppxPackage -Register C:\Users\Rahul\Onedrive\Desktop\Android\AppxManifest.xml)

Finally install Android System Webview from the Google Play Store


## Optional : 
To Get Root Access, copy the kernel file from the tools folder in the scripts
to the Tools folder in the WSA Folder
Then note the ip address of the WSA and connect to it via adb and after connecting,
enter the following commands
	
	adb shell
	su
	setenforce 0
