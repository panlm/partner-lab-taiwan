***********************
Karan Configuration SA
***********************
 
 
Overview
*********

.. note:: Estimated time to complete: **30 MINUTES**
 
In this lab, participants will deploy a Windows 2012 Server Guest VM and provision it with Karan.  Karan is used as a proxy for Calm automation.
 
Karan is a component that allows the Calm services to run PowerShell scripts on Windows virtual machines. Think of Karan as a “translation” layer between Calm and the Windows VMs.
 
 
Configure Karan
******************
Using Windows with Calm
 
In order for Calm to work with Windows virtual machines, an additional step is required. After deploying Prism Central and completing the configuration of Calm itself, an additional virtual machine must be deployed that runs the ‘Karan’ service.
 
.. note:: Check to make sure that Prism Central has already been configured and Calm has been setup before proceeding.
 
Before you begin
================
- The Karan service will be installed on Windows Server 2012 R2.
- Your Windows Server should always be up and running to support Calm automation for windows.
- Powershell 3.0 or onwards should be installed on the Karan server.
- .Net framework 4.0 or 4.5 should be installed on the Karan server.
 
Deploying Karan Guest VM
=========================
Create a Windows Virtual Machine running Windows 2012 R2 using the following parameters:

.. code-block:: bash

  vCPU       : 2x
  Cores      : 2x (2x cores/vCPU)
  Mem        : 2GB
  Storage    : 40GB (default-container)
  Network    : Secondary
  Image      : Windows2012 (This is a Server 2012 QCOW image)
  Image Type : Disk
  Bus        : SCSI
  
Power the Karan Guest VM on.

Login to the Karan Guest VM via *Launch Console* or *Remote Desktop*.  Upon successful log-in:

- **Change** the Computer Name to **KARAN**
- **Add** the Karan Guest VM to the **ntnxlab.local** domain.  
- Reboot the server.

.. figure:: https://s3.us-east-2.amazonaws.com/s3.nutanixtechsummit.com/karan/image15.png

- Disabke the Karan Guest VM firewall.

After the Karan Guest VM has completed reboot, login via *Launch Console* or *Remote Desktop*.  Upon successful log-in open a *Command-Prompt* window.

Within the Command-Prompt, Enable PowerShell remote execution:
 
.. code-block:: bash
 
    c:\> enable-psremoting
   
Within the Command-Prompt set the PowerShell Execution Policy:
 
.. code-block:: bash
 
    c:\> set-executionpolicy remotesigned
   
Within the Command-Prompt set all target machines as trusted machines on the Karan host:
 
.. code-block:: bash
 
    c:\> set-item wsman:\localhost\Client\TrustedHosts -Value *

Installing Karan
=================

.. note:: The karan installer is very large and might be best to use a VDI connection to download the file from http://10.21.64.50/images/Karan-1.6.0.0.exe and then map the download to you Guest VM.

If you download the karan-installer_ locally to your Mac, you'll need to establish a cifs connection

.. code-block:: bash

  % cifs://<karan-guest-vm-ipaddress>/c$ 
  
.. note:: The karan.exe link referenced was sourced as of January 2018.

Upload the karan installer to the Karan Guest VM and launch the Karan installer...  When prompted, populate the fields as follows:

- Select HTTP.  DO NOT SELECT HTTPS (Default)!!
- Set the port to 8090 (note that this must not be changed and port 8090 must be allowed through the Windows firewall on both host and client VMs)
- Set the number of Karan instances to 1 (typical for demo/lab environments)
- Enter the IP Address of the Karan instance. The IP address must be accessible from the Calm/Prism Central VM!
- Set the gateway UUID to:
 
.. code-block:: bash
 
    2067b70d-bd3f-4b3d-9d82-3add93f30a0a
 
- Enter the Prism Central VM IP Address and the port of the Epsilon Service as follows:
 
.. code-block:: bash
 
    http://<prism_central_ip_address>:8090
 
.. note:: Be sure to specify the port 8090, as per the example above for the Epsilon Servi!
 
- Click Next
- Specify the account information:

.. code-block:: bash
  
  logon account: administrator
  password: nutanix/4u
  
- Complete the wizard until Karan has successfully completed the installation.
- Once karan has successfully installed, perform the following steps to insure the PC VM firewall can communicate through port 8090.  

.. code-block::  bash

  c:\> ssh nutanix@10.21.xx.39
  c:\> password nutanix/4u
  c:\> /usr/local/nutanix/cluster/bin/modify_firewall -o open -i eth0 -p 8090 -a -f
  
- Using a command-prompt start the Windows Services as follows:
 
.. code-block:: bash
 
  c:\> services.msc

- From the Windows Services start the Karan service.

.. figure:: https://s3.us-east-2.amazonaws.com/s3.nutanixtechsummit.com/karan/image16.png


Configuring Windows Target VMs
============================== 
For Karan to have access to the Windows target/client VMs, the following commands must be run. In most cases, these commands would be run as part of preparing a Windows image for use with Sysprep.
 
.. code-block:: bash
 
    c:\> enable-psremoting
    c:\> set-executionpolicy remotesigned
    
In order for MSSQL to work with Karan you'll be required to make the following changes:

1. From the Start menu, point to Administrative Tools, and then click Local Security Policy.
2. In the Local Security Settings dialog box, double-click Local Policies, and then double-click User Rights Assignment.
3. In the details pane, double-click Adjust memory quotas for a process (Note: this is **SE_INCREASE_QUOTA_NAME** user right).
4. Click **Add User or Group**, and, in the *Enter the object names to select* box, type the user or group name to which you want to assign the user right, and then click OK.  
5. Click OK again, and then, in the details pane, double-click Replace a process level token. This is the **SE_ASSIGNPRIMARYTOKEN_NAME** user right.
6. Click Add User or Group, and, in the Enter the object names to select box, type the user or group name to which you want to assign the user right, and then click OK.
 
.. note:: When deploying or working with Windows VMs deployed by Calm, the only change required is to set the operating system to Windows, as opposed to Linux (default) within the blueprint. 

Takeaways
*********
Congratulations you have successfully configured a guest VM and Karan!

.. _karan-installer: http://10.21.64.50/images/Karan-1.6.0.0.exe

 
