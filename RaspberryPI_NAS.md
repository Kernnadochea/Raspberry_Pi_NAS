Title: Building a Raspberry Pi NAS with OpenMediaVault

Introduction:

This guide walks you through setting up a Network Attached Storage (NAS) using a Raspberry Pi 4 Model B and OpenMediaVault software. A NAS allows you to centrally store your files and access them from any device on your network.

Prerequisites:

Raspberry Pi 4 Model B
- Micro SD card (minimum 8GB recommended)
- Power adapter for Raspberry Pi
- External USB hard drive
- Ethernet cable
- Windows 11 computer (or any computer with an internet connection)
- Raspberry Pi Imager (download from https://www.raspberrypi.com/software/)
- Password manager (optional, but recommended)

Instructions:

1. Setting Up the SD Card:

- Insert the micro SD card into the SD card reader and connect it to your computer.
- Download and install the Raspberry Pi Imager from the official website
  
 ![image](https://github.com/user-attachments/assets/4ff3aa15-d3d1-40c5-b37d-fd65b563a079)

- Launch the Raspberry Pi Imager and choose your Raspberry Pi model (Raspberry Pi 4 Model B).
- Select "Operating System" and choose "Raspberry Pi OS (other)" followed by "Raspberry Pi OS Lite (64-bit)".
Note: This option provides a command-line interface only. There will be no desktop environment.
- Choose the storage location (your micro SD card) and click "Next."
  
 ![image](https://github.com/user-attachments/assets/0fa742c8-8a38-4dc7-8371-34e2cd675105)

- Click on "Edit configuration settings."
- Enter a username and password for your Raspberry Pi. It's highly recommended to use a strong password and store it securely in a password manager.
- Enter your Wi-Fi network name (SSID) and password. Note: Using a wired ethernet connection is highly recommended for stability.
  
 ![image](https://github.com/user-attachments/assets/61050d4e-7cf0-49b3-a096-ab202663e3ce)
  
- Click "Save" and then "Yes" to confirm applying the settings.
- The writing process will take a few minutes. Once complete, you'll see a confirmation screen.
  
 ![image](https://github.com/user-attachments/assets/714338ea-f5f5-445e-8546-ebb8df94b462)
  
2. Booting Up the Raspberry Pi:

- Remove the micro SD card from the reader and insert it into your Raspberry Pi.
- Connect the power adapter and ethernet cable (if not using Wi-Fi) to the Raspberry Pi.
- Power on the Raspberry Pi.
- Locate the Raspberry Pi's IP address in your router's settings.
  
3. Connecting via SSH:

- Open a command prompt window on your computer.
- Type the following command, replacing username with your chosen username and ip_address with your Raspberry Pi's IP address:
- `ssh username@ip_address`
- You will be prompted to confirm the connection. Type "yes" and press enter.
- Enter your Raspberry Pi password when prompted.
  
![image](https://github.com/user-attachments/assets/d36c3f7e-75f1-40f3-883a-ea0d83110d00)

4. Updating the Raspberry Pi:

- Run the following command to update your Raspberry Pi's software:
- `sudo apt update && sudo apt upgrade -y`
- This process may take a few minutes.

   ![image](https://github.com/user-attachments/assets/3f5fd125-d6d0-4b2a-8631-c67900cfef04)
  
5. Installing OpenMediaVault:

- Use the following command to download and install the OpenMediaVault script from GitHub:
- `sudo wget -O - https://raw.githubusercontent.com/OpenMediaVault-Plugin-Developers/installScript/master/install | sudo bash`
- The installation may take a few minutes.
Note: Your Raspberry Pi's IP address might change after installation. Verify the new IP address in your router settings if needed.

6. Configuring OpenMediaVault:

- Open a web browser and enter your Raspberry Pi's IP address in the address bar.
- You will be directed to the OpenMediaVault web interface.
- Log in using the default credentials:
- `Username: admin`
- `Password: openmediavault`

  ![image](https://github.com/user-attachments/assets/3578e7c0-cde3-4bd0-bb68-aa8176088389)
  
- Important: Change the default password immediately. Click on the user icon in the top right corner and select "Change Password." Enter a strong password and store it securely.

7. Setting Up Storage:

- Connect your external USB hard drive to the Raspberry Pi.
- In the OpenMediaVault web interface, navigate to "Storage" -> "Disks."
- You should see your Raspberry Pi's internal storage and the newly connected external hard drive listed.
  
  ![image](https://github.com/user-attachments/assets/d75bd23d-04d8-4157-996e-580662ab2697)

- Select the external hard drive and click "Format" to wipe any existing data.
- Navigate to "Storage" -> "File Systems" and select "Create and mount a file system."
- Choose "EXT4" from the file system type and click "Next."
- Select the previously formatted external hard drive and click "Finish."
- Click "Apply changes" at the top of the page to configure the storage.
  
  ![image](https://github.com/user-attachments/assets/32d583cb-fbc5-481e-b617-c8eb9ee57b26)

Step 8: Create Shared Folders

Create Shared Folders:
- Go to the "Storage" section.
- Select "Shared Folder" and then click the "Create" icon.
- Create two shared folders: one for SMB and one for NFS.
- Give each folder a name and select the desired drive.
- Apply the pending configuration changes.

Set Permissions:
- For both SMB and NFS shared folders:
- Select the folder and then click "Permissions."
- Give your group "Read/Write" permissions.
- Apply the pending configuration changes.

Step 9: Configure NFS and SMB Sharing
Enable SMB/CIFS:
- Go to the "Services" section.
- Select "SMB/CIFS."
- Under "Settings," enable SMB/CIFS.
- Save the changes.

Create SMB Share:
- Go to the "Shares" tab under "SMB/CIFS."
- Click "Create."
- Select your SMB shared folder and save.

Enable NFS:
- Go to the "Services" section.
- Select "NFS."
- Under "Settings," enable NFS.
- Save the changes.

Create NFS Share:
- Go to the "Shares" tab under "NFS."
- Click "Create."
- Select your NFS shared folder and save.

Step 10: Set Up Network Access
Configure User Access:
- Go to the "Users" section.
- Select your username and edit it.
- Enter and confirm your Raspberry Pi's password.
- Save the changes and apply any pending configurations.

Map Network Drive:
- On your Windows computer, open File Explorer.
- Right-click on "This PC" and select "Add a network location."
- In the Network Location Wizard:
  - Choose "Next."
  - Select "Choose a custom network location."
  - Enter your Raspberry Pi's IP address in the following format: `\\10.10.10.10\Cloud_Storage` (replace the IP with your actual Raspberry Pi's IP).
- When prompted, enter your Raspberry Pi username and password.
- Your Raspberry Pi's storage should now appear in File Explorer.

Step 11: Install Plex Media Server

SSH into Raspberry Pi:
- Connect to your Raspberry Pi using SSH.

Add Plex Repository:
- Update the package lists:
- `sudo apt-get update`

Install the apt-transport-https package:
- `sudo apt-get install apt-transport-https`

Add the Plex signing key:
- `curl https://downloads.plex.tv/plex-keys/PlexSign.key | sudo apt-key add -`

Add the Plex repository:
- `echo "deb https://downloads.plex.tv/repo/deb public main" | sudo tee /etc/apt/sources.list.d/plexmediaserver.list`

Update the package lists1 again:
- `sudo apt-get update`

Install Plex Media Server:
- `sudo apt-get install plexmediaserver`

Step 12: Access Plex

- Open Web Browser:
 - Enter your Raspberry Pi's IP address followed by the port number in your web browser: `http://10.10.10.10:32400/web` (replace the IP with your actual Raspberry Pi's IP).
 
- Sign In or Create Account:
 - Sign in to your existing Plex account or create a free account.

- Server Setup:
 - Name your server and uncheck "Allow me to access my media outside my house."
 - Click "Next" to proceed.

- Access Plex:
  - Download the Plex app on your phone or tablet and sign in.
  - You should now be able to access and manage your media library.

- Additional Tips:

  - IP Address: Ensure you have the correct IP address of your Raspberry Pi. You can find it in your router's settings or use a tool like ifconfig on the Raspberry Pi itself.
  - Firewall: If you have a firewall, make sure it allows access to Plex on port 32400.
  - Security: Consider enabling two-factor authentication for your Plex account.
  - Media Organization: Organize your media files into folders and name them appropriately for easy management.

By following these steps, you should be able to successfully set up network access and install Plex Media Server on your Raspberry Pi.





