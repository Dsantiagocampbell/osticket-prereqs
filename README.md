<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>osTicket - Prerequisites and Installation</h1>
This tutorial outlines the prerequisites and installation of the open-source help desk ticketing system osTicket.<br />



<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Internet Information Services (IIS)

<h2>Operating Systems Used </h2>

- Windows 10</b> (21H2)

<h2>List of Prerequisites</h2>

- Azure Virtual Machine
- osTicket Installation files
- Heidi SQL

<h2>Installation Steps</h2>

<p>
</P>
Welcome to my first tutorial. We'll start off by logging into Microsoft Azure Portal and creating a Virtual Machine (VM). VMs are great learning tools to help you better learn programs, languaging writing, or just experimenting. Okay, after we write the name for our resource group (I named it osTicket) then we can click on "Review+ create" on the bottom left hand corner. 

<img src="https://i.imgur.com/SWXchOC.png" height="80%" width="80%" alt="Creating osTicket"/>
<img src="https://i.imgur.com/0zbRge0.png" height="80%" width="80%" alt="Finished Creating"/>
</p>
<p>
Next, we're going to go ahead and create the VM. Click on home to go back to main page for Azure or simply use the search bar on the top and type "Virtual machines". Click on create and select Azure virtual machine.
<img src="https://i.imgur.com/Ar93vAF.png" height="80%" width="80%" alt="Creating VM"/>

On the next screen we're going to see our resource group that we created earlier and we'll go ahead and use that. Fill the rest out (I'm going to name our virtual manchine VM1). Scroll down and you'll be able to select your OS (Operating System) and the specs of the VM you want to have. Create your username and password. Click on on "Review + Create" when you're done.

<img src="https://i.imgur.com/yviBbEU.png" height="80%" width="80%" alt="VM Stats"/>

The VM may take a minute to create.
<img src="https://i.imgur.com/o3GOmHO.png" height="80%" width="80%" alt="VM deployment"/>
<img src="https://i.imgur.com/ZatFxEE.png" height="80%" width="80%" alt="VM deployment"/>
</p>

</p>
</p>
<br />

<p>
Go back to virtual machine and now you should see "VM1" click on it to reveal the details. Here you can see the specs of the VM, but what we really want right now is the IP address of the VM. As shown on the screen, I'm going to copy "20.231.74.112" 
<img src="https://i.imgur.com/viSNHJl.png" height="80%" width="80%" alt="VM Details"/>


Next, we're going to login into the VM via RDP (Remote Desktop Protocol). Go to start, then search, type in "rdp" like I did and you should it pop up. Click on it and enter in the VM IP address.
<img src="https://i.imgur.com/gFEJSiJ.png" height="80%" width="80%" alt=" RDP Search"/>
<img src="https://i.imgur.com/qI0vBKv.png" height="80%" width="80%" alt="RDP"/>

Once the login screen pops up, you're going to use whatever login credentials you put in place when your created the VM (I used labuser as my username).
<img src="https://i.imgur.com/Z1EnYFY.png" height="80%" width="80%" alt=" Logging RDP"/>
<img src="https://i.imgur.com/ALMXFzc.png" height="80%" width="80%" alt=" Logged in VM"/>
</p>
</p>
<p>
Now that we're in our VM, lets enable on IIS (Internet Information Services). Click on search on the bottom and type in "control panel". Click on Programs and then Programs and Features. On the left you'll see a link "Turn Windows features on or off". Click on that and select "Internet Information Services". Click ok let it finish. 
<img src="https://i.imgur.com/viRIGRp.png" height="80%" width="80%" alt=" Control Panel"/>
<img src="https://i.imgur.com/bpBzD0F.png" height="80%" width="80%" alt=" Enabling IIS"/>


</p>
<br />

<p>

</p>
<p>
Now let's install IIS Web Platform Installer. Here's a link:
https://drive.google.com/drive/u/0/folders/1APMfNyfNzcxZC6EzdaNfdZsUwxWYChf6
Everything we need is in that link.
<img src="https://i.imgur.com/sWfHlDY.png" height="80%" width="80%" alt="Web Platform Install"/>

Once installed, open Web Platformer. Search for "MySQL 5.5" and x86 verison of PHP 7.0.33.
<img src="https://i.imgur.com/3G9I4aD.png" height="80%" width="80%" alt="Searching SQL"/>
<img src="https://i.imgur.com/wCkTK6N.png" height="80%" width="80%" alt="Searching PHP"/>

There are going to be some files that don't successfully install. Go back to the google drive link provided above to get C++ redistributable package as well as PHP 7.3.8 and PHP Manager for IIS.

Extract and copy the "upload" folder into c:\inetpub\wwwroot. Afterwards rename the folder to osTicket.

Open IIS Manager and restart the server. Once inside IIS manager go to Sites->Default->osTicket on the right, click "Browse*.80" from there your default browser should open osTicket webserver.

<img src="https://i.imgur.com/voTZ99e.png" height="80%" width="80%" alt="IIS Manager"/>

Now we need to enable some extensions in IIS Manager. Go to Sites> Default> osTicket and double click PHP manager in the middle of the app. Enable "php_intl.dll" & "php_opcache.dll" then refresh the osTicket webserver and obsereve the changes "Intl Extension" should now be enabled.

<img src="https://i.imgur.com/dHb8H8c.png" height="80%" width="80%" alt="IIS Manager"/>

Go back into c:\inetpub\wwwroot\osTicket\include\ost-sampleconfig.php rename the file to c:\inetpub\wwwroot\osTicket\include\ost-config.php Assign permissions to ost-config.php Disable inheritance->Removeall New Permissions->Everyone->all

<img src="https://camo.githubusercontent.com/0a89dc3d5a476c0a5d2a90e808776c26c1c24397702e3064076650c9e6fcd040/68747470733a2f2f692e696d6775722e636f6d2f316e59615947652e706e67" height="80%" width="80%" alt="Disable Inheritance"/>

Almost done, go back into IIS Manager, click on osTicket and click on "Browse +80" to go into osTicket. Once in,(click continue) then you will name the Helpdesk to your liking. Select a default email that will receive emails from customers who submit tickets.


Continue filling out the rest of everything else and Viola! We're done. All we have left to do is clean up.  Clean up Delete: C:\inetpub\wwwroot\osTicket\setup Set Permissions to “Read” only: C:\inetpub\wwwroot\osTicket\include\ost-config.php Login to the osTicket Admin Panel (http://localhost/osTicket/scp/login.php)

<br />
