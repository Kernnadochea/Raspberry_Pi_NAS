Raspberry Pi NAS

Tools:
- Raspberry Pi 4 Model B
  Raspberry Pi Essentials
- Power Adapter
- Micro Center 64Gb SD Card 
- SD Card Reader
- External USB Hard Drive Seagate 1TB Expansion Portable Drive
- Windows 11 Desktop

Software:
- Rasiberry Pi Imager
- 1Password
- xfinity

Step 1: Prep the SD card
- Insert the SD Card into the SD card reader then plug it into the computer
- With the SD card reader plugged in, launch Raspberry Pi imager. Imager can be installed from this URL https://www.raspberrypi.com/software/
  
 ![image](https://github.com/user-attachments/assets/4ff3aa15-d3d1-40c5-b37d-fd65b563a079)

- Choose Device, select your Raspiberry Pi Device from the drop-down, for this case we will be selecting Raspiberry Pi 4
- Choose OS, scroll down to "Raspberry Pi OS (other) then select "Raspiberry Pi OS Lite (64-bits) Note that there will be no Desktop and GUIs, all you will have is a command line. Headless install
- Select the appriporate SD card, then hit next
  
 ![image](https://github.com/user-attachments/assets/0fa742c8-8a38-4dc7-8371-34e2cd675105)

- Now select "Edit Settings"
- Enter the username and password for the account. I have used a random generated password and stored into my 1Password Password Manager.
- Enter your SSID and SSID password (Highly Recommend to use ethernet for this project)
  
 ![image](https://github.com/user-attachments/assets/61050d4e-7cf0-49b3-a096-ab202663e3ce)
  
- Hit save then "Would you like to apply OS customiation settings?" Select Yes "Are you sure you want to continue?" Select Yes
- This will take around 5-10 minutes to complete. Take a coffee break. Once completed you will get a screen like below
  
 ![image](https://github.com/user-attachments/assets/714338ea-f5f5-445e-8546-ebb8df94b462)
  
Step 2: Boot the Pie
- Take your micro SD card out of the SD card reader and insert the micro SD card into your Raspberry Pi micro SD slot
- Plug in the c type power supply cable and ethernet cable into the Raspberry Pi
- Now you will need to go into your home router application and located the Raspberry Pi client and grab its IP address. My ISP is xFinity, I have logged into my xFinity application and capture my Pi's IP from the Wifi Settings.
- Once you have the Raspberry Pi's IP address, open up command prompt and will SSH into the Pi.
- From the command line type in ssh "The username you set"@"IP Address" it should look like the screen below.
- ssh nado@xx.xx.xx.xx
- It will prompt "Are you sure you want to continue connecting (yes/no/[fingerprint])?" Type in yes.
- Run the ssh nado@xx.xx.xx.xx again and then enter your Raspberry Pi's password. Password was stored in 1Password.
- We should now be the command line of the Raspberry Pi
  
![image](https://github.com/user-attachments/assets/d36c3f7e-75f1-40f3-883a-ea0d83110d00)

Step 3: Update the Raspberry Pi
- Run the update command update to make sure your Raspberry Pi is up to date. Run the command below, note that this will take a couple of minutes to complete.N
- sudo apt update && sudo apt upgrade -y
  
 ![image](https://github.com/user-attachments/assets/3f5fd125-d6d0-4b2a-8631-c67900cfef04)

- The update will stop scrolling once the matrix stops scrolling

Step 4: Install the NAS
- Use this command below, this will download a script from GitHub and it will run the script with Bash. Note that this will take a couple minutes to complete. 
- sudo wget -O - https://raw.githubusercontent.com/OpenMediaVault-Plugin-Developers/installScript/master/install | sudo bash
- The update will stop scrolling once the matrix stops scrolling
- Note that there is a possibility that you could have been disconnected from the network when the installation was going on. Your IP address could have been changed, so make sure to verify from your router settings.
- If the IP did get changed, just SSH into the machine again with the new IP Address
- OpenMediaVault is now installed

Step 5: Configuure OpenMediaVault
- Launch your favorite web browser and launch the paste Raspberry Pi's IP address into the URL
- It will direct you to openmediavault GUI, here you will need to enter the default username and password
- Default Username: admin
- Default Password: openmediavault

  ![image](https://github.com/user-attachments/assets/3578e7c0-cde3-4bd0-bb68-aa8176088389)
  
- First thing you would want to do is change the default dmin password immediately
- On the top right hand side, select the user icon and select "Change Password" and enter the new password. Here I will generate a random password from 1Password and save.
- Once completed, now plug in the external USB harddrive into the Raspberry Pi via USB
- On the left hand side, select the "Storage" drop-down and select "Disks". From here we should be able to see the external harddrive we plugged in. You should see one is your Micro SD card and the other is the drive.
  
  ![image](https://github.com/user-attachments/assets/d75bd23d-04d8-4157-996e-580662ab2697)

- Select the external hard drive and perform a quick wipe just to ensure its fresh and clean
- Now under the "Storage" drop-down select File Systems. Select for hard drive for mount. If you do not see your drive then selecxt "create and mount a file system"
- Choose EXT4 and continue. This will take a couple minutes to complete
- You will now see Pending configuration changes above, apply those changes
  
  ![image](https://github.com/user-attachments/assets/32d583cb-fbc5-481e-b617-c8eb9ee57b26)

  Step 6: Create a shared folder
  - Under the "Storage" drop-down select "Shared Folder" and select "Create" icon.
  - Give the folder a name and select the drive. Create one for SMB and one for NFS.
 
  ![image](https://github.com/user-attachments/assets/e7b5f3dd-35fa-42dd-8769-6860879c7cd3)

  - Pending configuration changes message, select apply
  - Still under the "Shared Folder" tab, we want to select the drive and then select permissions
  - Give your group "Read/Write" permissions
  
  ![image](https://github.com/user-attachments/assets/a6100181-b699-4072-b3d4-87cf1e3b8ef0)

   - Pending configuration changes message, select apply
 
  Step 7: Configuring NFS and SMB Shared
  - Note that enableing NFS will allows access from Linux and MAC machines. SMB will allow Windows machine access
  - On the left hand side, select the drop-down "Services" amd select "SMB/CIFS"
  - Select settings and then check on "Enabled" and save.
  - Under SMB/CIFS, select "Shares"
  - Then select "Create" and then select your Shared folder and save
  - Now do the same thing for the NFS settings.
  - Apply the pending configurations
 
  Step 8: Set Up Network
  - On the left hand side select "Users" and select the "Users" drop-down.
  - Select the username and click edit

  ![image](https://github.com/user-attachments/assets/406694e2-9c63-4a64-9787-133a2d57d1bc)

  - Enter the Raspberry Pi's password and confirm the password, then hit save.
  - Apply the pending configurations
  - On your Windows machine, open up file explorer and click "This PC"
  - Under the Devices and drives, right click your mouse and select "Add a network location"
  - On the Network location wizard click "Next", "Choose a custom network location", here you will enter the Raspbery PI's IP address like the following
  - "//10.10.10.10/Cloud_Storage"
    
  ![image](https://github.com/user-attachments/assets/6c364b56-b5a7-4817-9437-8ba70e6dcf21)
    
  - Next, you will get a pop up to enter your Raspberry Pi username and password. Once you enter that it should be mapped in File Explorer
   
    ![image](https://github.com/user-attachments/assets/1ea6ba9c-9122-4a04-ad4f-55bfcccc97f2)

Step 9: Install Plex Media Server
- ssh into the Raspberry Pi via command line
- Enter the command [sudo apt-get install apt-transport-https] and hit enter
- Now we want to add the Plex repositories from our Raspberry Pi and download Plex
- First we are going to verify the keys
- Enter the command [curl https://downloads.plex.tv/plex-keys/PlexSign.key | sudo apt-key add -]
- The next command will add the Plex respository to our lst of respository
- [echo deb https://downloads.plex.tv/repo/deb public main | sudo tee /etc/apt/sources.list.d/plexmediaserver.list]
- With the new respository added we need to update list of available packages
- [sudo apt-get update]
- Run the following command once update is completed
- [sudo apt install plexmediaserver]

  ![image](https://github.com/user-attachments/assets/bbbd8006-4f41-4613-8908-8b839051986d)

  - Installation Successful
 
  Step 10: Access Plex
  - In a web browser enter in the URL, replace this IP address with the IP address of your Raspiberry Pi [http://10.10.10.10:32400/web]
  - You will need to login into Plex, create a free Plex if you don't have one. You don't neeed to sign up for premium
  - In the Server Setup, enter a name for your server use lower case letter and uncheck "Allow me to ccess my media outside my house" then hit next
  - 

![image](https://github.com/user-attachments/assets/ac2367a5-deaa-4bdc-bee5-64b3e1ddb4d9)

- From here you can start adding your libray
- Download the Plex app on your phone and sign in. You should now be able to view those libray you configured
- 





