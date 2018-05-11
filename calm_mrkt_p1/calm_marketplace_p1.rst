**************************
Calm Marketplace Part 1
**************************


Overview
************

.. note:: Estimated time to complete: **50 MINUTES**

In this exercise you will learn how to manage Calm Blueprints within the Nutanix Marketplace. As part of the exercise you will publish a pre-configured Blueprint to the local Marketplace, clone the Blueprint from the Marketplace for editing, and launch the application.

Publishing Blueprints from Marketplace Manager
**********************************************

By default, Calm comes pre-seeded with validated Blueprints for multiple open source and enterprise applications. Marketplace Manager acts as a staging area for publishing default and user-created Blueprints to your local Marketplace. The Marketplace acts as an application store, providing end users with a catalog of available applications.

From **Prism Central > Apps**, select |image1| **Marketplace Manager** from the sidebar.

Under **Marketplace Blueprints**, select **XClarity**.

Note the Blueprint description contains key information including licensing, hardware requirements, OS, supported platforms, and limitations.

Under normal circumstances you can click the **Publish** to start the publication workflow.  Because we are using a single cluster for the Lenovo Tech Summit, this can only be done once and has already been done for you.

The screenshots below shows the "Mongo" project selected, since these guides were originally written for another global Tech Summit event.  However, the workflow for XClarity is identical.

.. figure:: https://s3.amazonaws.com/s3.nutanixworkshops.com/calm/lab4/image5.png

To configure which projects (and, therefore, users) can use the application, the project's name can be selected from the provided dropdown box.

.. figure:: https://s3.amazonaws.com/s3.nutanixworkshops.com/calm/lab4/image8.png

.. note::

  If the **Projects Shared With** drop down menu is unavailable, refresh your browser.

Cloning Blueprints from Marketplace
***********************************

From **Prism Central > Apps**, select |image5| **Marketplace** from the sidebar. All Blueprints published in Marketplace Manager are visible here.

.. figure:: https://s3.amazonaws.com/s3.nutanixworkshops.com/calm/lab4/image11.png

Select the **XClarity** marketplace application and click **Clone**.

.. note::

  Selecting **Actions Included** for a Blueprint will display the actions that have been implemented for a given Blueprint, such as Create, Start, Stop, Delete, Update, Scale Up, Scale Down, etc.

.. figure:: https://s3.amazonaws.com/s3.nutanixworkshops.com/calm/lab4/image13.png

Fill out the following fields and click **Clone**:

- **Blueprint Name** - XClarity*<INITIALS>*
- **Project** - default

Editing Cloned Blueprint
************************

Select |image8| **Blueprints** from the sidebar and click your **XClarity<INITIALS>** Blueprint to open the Blueprint Editor.

.. figure:: https://s3.amazonaws.com/s3.nutanixworkshops.com/calm/lab4/image15.png

Click :fa:`exclamation-circle` to review the list of errors that would prevent a successful deployment of the Blueprint.

.. figure:: https://s3.amazonaws.com/s3.nutanixworkshops.com/calm/lab4/image16.png

Click **Credentials** and select **admin**.

Fill out the following fields and click **Back**:

- **Username** - root
- **Secret** - Password
- **Password** - nutanix/4u

Select the **Xclarity** Service and confirm the following settings in the **Configuration Pane**:

- **VM Configuration > Image** is set to to **XclarityImage**.  This is a pre-prepared Xclarity image created and published by Lenovo.
- **Connection > Credential** to **admin**.
- **NIC** is connected to **VLAN0**

Launching XClarity
******************

- Click **Launch**
- Specify a unique **Application Name** (e.g. XClarity*<INITIALS>*-1)
- Confirm all variables are correct e.g. Prism Central IP etc
- Use a static IP address for **APPLIANCE_IP** as per the provided list
- Expand the **XCLARITY** VM configuration and confirm NIC is connected to **VLAN0**
- Click **Create**.

.. figure:: https://s3.amazonaws.com/s3.nutanixworkshops.com/calm/lab4/image17.png

Takeaways
***********
- By using pre-seeded Blueprints from the Nutanix Marketplace, users can quickly try out new applications.
- Marketplace Blueprints can be cloned and modified to suit a user's needs. For example, the pre-seeded LAMP Blueprint could be a starting point for a developer looking to swap PHP for a Go application server.
- Marketplace Blueprints can use local disk images or automatically download associated disk images. Users can create their own keys and slipstream them into Blueprints (via cloud-init) to control access.

.. |image1| image:: https://s3.amazonaws.com/s3.nutanixworkshops.com/calm/lab4/image4.png
.. |image5| image:: https://s3.amazonaws.com/s3.nutanixworkshops.com/calm/lab4/image10.png
.. |image8| image:: https://s3.amazonaws.com/s3.nutanixworkshops.com/calm/lab4/image14.png
