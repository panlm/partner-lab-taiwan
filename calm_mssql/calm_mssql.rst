***************************
Calm Blueprint (MSSQL-2014)
***************************

.. note:: IMPORTANT! This blueprint is for Lab purposes only. Do not put this into production without modifying it to meet your organizations requirements, Nutanix Best Practices, and Microsoft SQL Best Practices.

Overview:
*********

.. note:: Estimated time to complete: **20 MINUTES**

In this lab participants will walk through importing and deploying an MS Windows Server 2012 R2, and an instance of MS SQL Database - 2014.


Getting Engaged with the Product Team
=====================================
- **Slack** - #calm
- **Product Manager** - Jasnoor Gill, jasnoor.gill@nutanix.com
- **Product Marketing Manager** - Gil Haberman, gil.haberman@nutanix.com
- **Technical Marketing Engineer** - Chris Brown, christopher.brown@nutanix.com
- **Field Specialists** - Mark Lavi, mark.lavi@nutanix.com; Andy Schmid, andy.schmid@nutanix.com

Prerequisites:
**************
Certain prerequisites must be met before installation will succeed. The following must be configured:

- Karan Guest VM Configured and Installed: karan-setup_
- MSSQL installation requires CredSSP to be enabled on Karan host
- Account running karan service must have the following privileges

.. code-block:: bash
  
  (SE_ASSIGNPRIMARYTOKEN_NAME, SE_INCREASE_QUOTA_NAME)


Blueprint:
***********
Download the MSSQL Blueprint by clicking the link provided below:

:download:`mssql2014.json <./blueprints/windowsMSSQL2014.json>`

From Apps (Calm) within Prism Central, navigate to the Blueprint Workspace by clicking (|image1|) icon located on the left tool ribbon.  This will open the Blueprint Workspace where self-authored blueprints are staged for editing, publishing, and/or launching as Applications.  When the Blueprint grid appears, click the **Upload Blueprint** button located along the top of the Blueprint grid.

.. figure:: https://s3.amazonaws.com//s3.nutanixworkshops.com/calm/lab3/image2.png

Navigate to the blueprint file (i.e. *mssql2014.json*) recently downloaded and select it by clicking on the file.

A modal dialog will appear prompting for a name and project when saving. Complete the fileds as shown below and click **upload**. This will save the blueprint to the workspace.

- **Name:** mssql2014
- **Project:** Calm

.. figure:: https://s3.us-east-2.amazonaws.com/s3.nutanixtechsummit.com/calm_mssql/image1.png

Assign Credential
=================
Since Blureprints are exported as clear text, they do not retain credential information that could potentially be used maliciously.  You'll be required to set the **Credentials**.  set the creddentials as follows:

.. code-block:: bash

  Credential Name : WINDOWS
  Username        : ntnxlab.local\administrator
  Secrete         : password
  Password        : nutanix/4u
  
Once complete, click the **Back** button located in the upper right, and then click **Save** along the top menu-bar.

Configure Blueprint Variables
=============================
The **mssql2014** blueprint uses service variables to configure pre and post runtime behavior.  The blueprint configuration variables can be accessed by clicking on the **Service** tab of blueprint located to the right of blueprint workspace.

+-----------------------+----------------------------------------------------------------------+
|**Variable**           |**Description**                                                       |
+-----------------------+----------------------------------------------------------------------+
|install_location       |A location directive (internal/external) definng if the image is      |
|                       |accessible internally (fiel share), or externally                     |
|                       |(Microsoft download site).                                            |
+-----------------------+----------------------------------------------------------------------+
|file_share_user        |The username used to authenticate to the internal/external file share.|
+-----------------------+----------------------------------------------------------------------+
|file_share_password    |The username used to authenticate to the internal/external file share.|
+-----------------------+----------------------------------------------------------------------+
|file_server_ip         |IP Address of the server hosting the file share.                      |
+-----------------------+----------------------------------------------------------------------+
|file_share_name        |The name of the share/folder containing the image to be downloaded.   |
+-----------------------+----------------------------------------------------------------------+
|sql_iso_path           |The image name including the full path (if applicable),               |
+-----------------------+----------------------------------------------------------------------+
|mapped_drive           |The logical drive designator if using a mapped location/drive.        |
+-----------------------+----------------------------------------------------------------------+

The following Blueprint variables should be configured as follows: 

.. code-block:: bash

  install_location     : internal
  file_share_user      : administrator
  file_share_password  : nutanix/4u
  file_server_ip       : 10.21.66.59
  file_share_name      : sql
  sql_iso_path         : SQLServer2014SP2-FullSlipstream-x64-ENU.iso
  mapped_drive         : z

Once complete, click **Save** located along the top menu-bar.

VM Creation
===========
A Windows Server VM is required to host the MS SQL 2014 Database instance. VM settings and configurations can be accomplished by clicking on the VM tab of the service.  Set the following *Substrate Name*, *Cloud*, and *OS* fields using the following values:

.. code-block:: bash

  Name        : MSSQL2014
  Cloud       : Nutanix
  OS          : Windows

Add a **VDISK** by clicking on the **(+)** to expand the **VDISKS** configuration window. Configure a **VDISK** using the following parameters:

.. code-block:: bash

  Disk Type   : DISK
  Device Bus  : SCSI
  Size        : 100GB

Add an **Image** by clicking on the **(+)** to expand the **IMAGES** configuration window.  Configure the **Guest VM** using the following parameters:

.. code-block:: bash

  VM Name     : @@{calm_application_name}@@
  Image       : Windows2012
  Disk Type   : DISK
  Device Bus  : SCSI
  vCPU        : 2
  Core/vCPU   : 2
  Memory      : 4 GB

Scroll to the bottom and add the NIC **secondary** to the Guest VM.

Assign a *Credential* to the Guest VM using the **WINDOWS** credential created earlier.

Guest Customization
===================
The **mssql2014** blueprint uses **Guest Custiomizations** to configure runtime behavior.  

Guest Customization can be accessed as part of the **VM Configuration**:

- Click the **Guest Customization** Check-Box just below the Guest VM settings to access the script window.
- Select the **Sysprep** radio button.
- Copy the contents from unattend.xml_ and paste it to the **Script** window.

Once complete, click **Save** located along the top menu-bar.


Enable CredSSP
==============
To Enable CredSSP on the Karan host, please follow steps below:

On the Karan Host run the following command to enable CredSSP as a client role and allow Karan host to Delegate credentials to all computers ( Wild card mask "*"):

.. code-block:: bash

  C:>\ Enable-WSManCredSSP -Role Client -DelegateComputer *
  
From command prompt window run:

.. code-block:: bash

  C:>\ gpedit.msc
   
- In the group policy editor window Goto **Computer-configuration -> administrative templates -> system ->credential delegation**.
- Double click on **Allow Delgating Fresh Credentials with NTLM-only server authentication**.
- Select the **Enable** radio button.
- Click on the **show** button.
- In the value field add  **WSMAN/***. This allows delegate fresh credentials to **WSMAN** running in any remote computer


Privileges:
============

.. note:: The instructions in this section are applicable to the karan server and required for SQL Server deployments.

Follow the steps below to assign the correct privileges on the karan server:

- Idenitfy the user account that the Karan service is running as 
- From the Start menu, point to Administrative Tools, and then click Local Security Policy.
- In the Local Security Settings dialog box, double-click Local Policies, and then double-click User Rights Assignment.
- In the details pane, double-click Adjust memory quotas for a process. This is the **SE_INCREASE_QUOTA_NAME** user right.
- Click Add User or Group, and, in the Enter the object names to select box, type the user or group name to which you want to assign the user right, and then click OK.
- Click OK again, and then, in the details pane, double-click Replace a process level token. This is the **SE_ASSIGNPRIMARYTOKEN_NAME** user right.
- Click Add User or Group, and, in then <Enter> the object names to select box, type the user or group name to which you want to assign the user right, and then click OK.
- Restart the Karan service.

Launch Blueprint
================
Once the blueprint has been successfully updated and saved, click the (|image5|) button to lanuch the Blueprint.  Name the application with *mssql2014*.

.. figure:: https://s3.amazonaws.com/s3.nutanixworkshops.com/calm/lab3/image6.png

Click **Create** to launch the application.

Once the application has been launched, the Application Management Dialog will appear showing the state of the Application.  Click the *Audit* button in the tool-bar located along the top of the Application Management Dialog to monitor or audit the provisioning progress of the application.

Takeaways
***********
- Downloaded and Imported an existing Windows MSSQL blueprint ro the *Blueprint Workspace*.
- Learned to set variables that change blueprint behavior to source imnages and define credentials.
- Learned how to setup and configure a Karan proxy server for executing powershell to provision windows servers.

.. _karan-setup: ../karan/karan_sa_setup.html

.. |image1| image:: https://s3.amazonaws.com/s3.nutanixworkshops.com/calm/lab3/image1.png
.. |image5| image:: https://s3.amazonaws.com/s3.nutanixworkshops.com/calm/lab3/image5.png

.. _unattend.xml: ./unattend.html
