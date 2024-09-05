<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>osTicket - Prerequisites and Installation</h1>
This tutorial outlines the prerequisites and installation of the open-source help desk ticketing system osTicket.<br />
Please notice that all these programs were given to the students in a folder during the module. You may find all the files at https://drive.google.com/drive/u/1/folders/1APMfNyfNzcxZC6EzdaNfdZsUwxWYChf6



<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Internet Information Services (IIS)

<h2>Operating Systems Used </h2>

- Windows 10</b> (21H2)

<h2>List of Prerequisites</h2>

- In order to do this lab you need to have an Azure active subscription. Go to portal[.azure.com](https://portal.azure.com/) and create one. 
- Create a Resource group in Azure. You may call it RG-osTicket.
- Then create a Virtual Machine in the Resource Group you just made. Remember that your resource group and your virtual machine must be in the same region. Select Windows 10 Pro, version 21H2. In size select Standard_D4s_v3-4vcpus. Select a user name and password and make sure you won't forget. Click next twice, it will create a network for you. Leave the rest of the settings selected by default and click on "Review and Create". After the validation passes, click on "Create".
- Go to the virtual machine you just created and copy the Public IP address. Then in your computer, go to the search bar and type Remote desktop, click on Remote Desktop Connection and in the bar of the window that pops up, paste the IP address of your virtual machine. Log in with the user name and password that you chose when you created your VM
- Install / enable IIS in Windows with CGI, right click the start menu, click "run" type "control". In control panel click on "programs", then turn Windows features on or off, click on Internet Information Services, expand, then World Wide Web Services, Application Development Features and check CGI. Collapse Application Development Features and click on Common HTTP Features, make sure all of the options are checked.
  
![image](https://github.com/user-attachments/assets/279faa96-6680-4fff-b727-e4201aced023)

![image](https://github.com/user-attachments/assets/2017d380-7380-4af5-877b-eb9db12f0fcd)                   

![image](https://github.com/user-attachments/assets/fa4e0b26-9873-45cd-ac7a-c344410854b7)


It is important to install this because IIS webserver is the server where osTicket runs on.
After installing it, to check that it works, open your browser and type 127.0.0.1 and you should see a screen like this:
![image](https://github.com/user-attachments/assets/cd2aed08-b4dc-4e69-bbb5-d11df0f4235b)

- Our next prerequiste is to download and install PHP Manager for IIS.
- Download and instal the Rewrite module (rewrite_amd64_en-US.msi)
- Create a directory for PHP in the local hard drive
- ![image](https://github.com/user-attachments/assets/727ec1d4-8326-4725-bc0c-2f5286e65b78)

- Download (php-7.3.8-nts-Win32-VC15-x86.zip) and unzip the contents into C:\PHP. If the option pops up,choose to "keep" the file.
-  Download and install VC_redist.x86.exe. 
-  Download and install MySQL 5.5.62 (mysql-5.5.62-win32.msi). When installing MySQL pick "Typical install". Be sure to select Lauch the MySQL Configuration Wizard before clicking "Finish" in the dialogue window.
-  In the following window of MySQL pick "Standard configuration" Pick a password, be sure not to forget and click on "Execute".




<h2>Installation Steps</h2>

![image](https://github.com/user-attachments/assets/3ad71286-012b-4428-aff1-84c8103a2879)
  <p>
    
- Click on "start" type iis, do right click and then select "Run as administrator"
- Double click "PHP manager"
- Click on "Register new PHP version"
- Browse to where you put all the PHP files (C:PHP) and then click on php-cgi. Make sure on the right lower bar it says PHP executable. Click "open" then OK.
- Once in the PHP manager window again, click on "Refresh". Be sure to refresh everytime you make a change in the iis.
- Download osTicket from the installation folder
- Go do "Downloads" and double click the file that says osTicket. Right click on the folder "upload", cut and then go to C: , click on inetpub, then wwwroot and paste it there.
- Then rename the "upload" file as "osTicket"
- ![image](https://github.com/user-attachments/assets/72c7c9da-aa44-4bf0-bca5-d0e0ea4b7462)
  
</p>
  
- Go to the PHP manager and click on "Restart"
  
![image](https://github.com/user-attachments/assets/31586172-3d02-46f4-9e15-8d4c1dd0bbdf)

- On the PHP manager, on the left column click on the server, sites, then Default Web Site, then osTicket. On the right column click on “Browse *:80”. You should see the following:

![image](https://github.com/user-attachments/assets/fbcbf704-fcd7-4ecf-af72-0970ca7c04fa)
</p>

Notice than some things are not enable so it is time to change that. We are going to enable **php_imap.dll**, **php_intl.dll** AND  **php_opcache.dll**.

- Go back on the PHP manager to Sites, Default Web Site, osTicket. Double click on PHP manager. Then below PHP extensions click on "Enable or disable an extension" and enable the extensions mentioned above.

- Then refresh the browser and see how the changes are efective.

  ![image](https://github.com/user-attachments/assets/927444d2-5e0c-4d44-a115-15774ebd3f4b)


- Now go to C:\inetpub\wwwroot\osTicket\include\ost-sampleconfig.php , right click on "ost-sampleconfig.php", rename and delete the portion " sample". The file should read "ost-config.php".
- Right click on this new named file, go to properties, security, advance, disable inheritance.

![image](https://github.com/user-attachments/assets/bfddb2e5-bbf7-4c7a-b6cf-debd3dbcbd06)


- Then remove all inheritance permissions from this object. Add, select a principal; type "everyone" in the box.

  ![image](https://github.com/user-attachments/assets/4fb44fa1-892b-42f2-94d5-51242114497c)

  - Click on "check names", then "OK".
  - in Permisiions give everyone "full control". OK
  - In the next window "Advance Security Settings for ost-config.php" click "apply" then "ok", then OK.
  - Then "Continue" setting up osTicket in the browser.
    
    ![image](https://github.com/user-attachments/assets/c315df89-8144-4844-8bef-aa2852a6af4c)

- Fill out the "System Settings", "Admin User" and write them dowm in case you forget.
- From the installation files install HeidiSQL. It will help us connect with the data base we already install.
- Go to downloads and double click HeidiSQL and click next on every window so the file will install. Be sure to select "launch HeidiSQL" before clicking "Finish".
- On HeidiSQL click on "New" to create a new connection to the data base. You will use the user name and password that you previoiusly set for MySQL. Click "open" and you will have your connection open to MySQL.

   ![image](https://github.com/user-attachments/assets/40bb3886-2435-4bf5-a77f-bfe50cb0db5a)

- On MySQL do right click on the left column over the word "unnamed", click on "create new" and then "database". Name it "osTicket". Click "ok". 
- Let's continue to set os Ticket. Fill out the data base settings with the info you have. Then click on "install now"

  ![image](https://github.com/user-attachments/assets/56259b86-a6e8-4281-b0fa-ab94336ec457)

  - You should see a window that says   "Congratulations" like the following:
    
 
    ![image](https://github.com/user-attachments/assets/28f20a9b-c6cf-46fd-b715-2dc8241d1772)


    - It's time to clean up and check that everything is working well. Go to  C: then click on inetpub\wwwroot\osTicket and delete the setup folder doing right click on it and then selecting "delete".
    - Then go to  C:inetpub\wwwroot\osTicket and click on the "include" folder, click on ost-config.php, go to Properties, Security, go to Advanced, go to Everyone, Edit and uncheck Fully, Modify and Write. Only "Read" and "Read and execute" should be selected.
    - Then click ok, apply, ok.
    - Check dthe URL's to see if everything is working well.
    - As an admin copy and paste the following address in your browser http://localhost/osTicket/scp/login.php You should see something like this:
   
    ![image](https://github.com/user-attachments/assets/fa8ee166-e3ee-4a1f-83ed-88ad43278669)

    - Sign up using the admin user name and password you previously created.




    






