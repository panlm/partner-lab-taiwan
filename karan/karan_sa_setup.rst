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
 
Deploying Karan
===============
 
The steps for deploying Karan are as follows.
 
- Download the karan-installer_ . The link referenced is correct as at January 2018.
- Deploy a Windows virtual machine running Windows 2012 R2 using the following parameters:

.. code-block:: bash

  vCPU       : 1x
  Cores      : 2x (2x cores/vCPU)
  Mem        : 2GB
  Storage    : 40GB (default-container)
  Network    : Primary
  Image      : Windows Server 2012 QCOW
  Image Type : Disk
  Bus        : SCSI
  
- Add the Karan VM to the domain, for this lab we will use ntnxlab.local
- Enable PowerShell remote execution on the Karan Windows VM:
 
.. code-block:: bash
 
    > enable-psremoting
   
- Set the PowerShell Execution Policy:
 
.. code-block:: bash
 
    > set-executionpolicy remotesigned
   
- Set all target machines as trusted machines on the Karan host:
 
.. code-block:: bash
 
    > set-item wsman:\localhost\Client\TrustedHosts -Value *
   
- Run the Karan installer and, when prompted, populate the fields as follows.
- Select http or https as required
- Set the port to 8090 (note that this must not be changed and port 8090 must be allowed through the Windows firewall on both host and client VMs)
- Set the number of Karan instances (leave as 1 for demo environments)
- Enter the IP Address of the Karan instance. The IP address must be accessible from the Calm/Prism Central VM!
- Set the gateway UUID to:
 
.. code-block:: bash
 
    2067b70d-bd3f-4b3d-9d82-3add93f30a0a
 
- Enter the Prism Central VM IP Address, as follows:
 
.. code-block:: bash
 
    http://<prism_central_ip_address>:8090
 
.. note:: Don't forget to specify the port, as per the example above!
 
- Click Next
- Specify the account information (for demo environments, the Karan VM’s local administrator account is OK)
- Complete the wizard until Karan is installed
- Once karan has successfully installed, you'll need to insure that the PC VM firewall can communicate through port 8090.  We'll accomplish as follows:

.. code-block::  bash

  > ssh nutanix@10.21.xx.39
  > password nutanix/4u
  > /usr/local/nutanix/cluster/bin/modify_firewall -o open -i eth0 -p 8090 -a -f
  
- After installation, start the Karan service from the Windows Services application:
 
.. code-block:: bash
 
    > services.msc

Configuring Windows target VMs
============================== 
For Karan to have access to the Windows target/client VMs, the following commands must be run. In most cases, these commands would be run as part of preparing a Windows image for use with Sysprep.
 
.. code-block:: bash
 
    > enable-psremoting
    > set-executionpolicy remotesigned
    
For MSSQL to work with Karan you will need to also make the below changes.

1. From the Start menu, point to Administrative Tools, and then click Local Security Policy.

2. In the Local Security Settings dialog box, double-click Local Policies, and then double-click User Rights Assignment.

3. In the details pane, double-click Adjust memory quotas for a process. This is the SE_INCREASE_QUOTA_NAME user right.

4. Click Add User or Group, and, in the Enter the object names to select box, type the user or group name to which you want to assign the user right, and then click OK.

5. Click OK again, and then, in the details pane, double-click Replace a process level token. This is the SE_ASSIGNPRIMARYTOKEN_NAME user right.

6. Click Add User or Group, and, in the Enter the object names to select box, type the user or group name to which you want to assign the user right, and then click OK.
  
 
Using Karan
===========
 
Karan itself isn’t ‘used’ in the traditional sense i.e. there’s no Karan ‘application’. By installing Karan and having it available for Calm itself to use, PowerShell scripts will be automatically ‘proxied’ through the Karan instance, when required.
 
.. note:: When deploying or working with Windows VMs from Calm, the only change that is required is to set the operating system to Windows, as opposed to Linux (the default). 
 
 
Takeaways
*********
 
Congratulations you have successfully configured a guest VM and Karan!

.. _karan-installer: http://10.21.64.50/images/Karan-1.6.0.0.exe

 
