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
