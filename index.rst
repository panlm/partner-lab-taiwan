.. title:: Taiwan Partner Lab May 2018

.. toctree::
  :maxdepth: 2
  :caption:     Required Labs
  :name: _req-labs
  :hidden:

  .. example/index
  ssp/ssp
  calm_mysql/calm_mysql
  calm_lamp/calm_lamp
  calm_mrkt_p1/calm_marketplace_p1
  calm_mrkt_p2/calm_marketplace_p2
  karan/karan_sa_setup

.. _getting_started:

Getting Started
===============

.. raw:: html

  <strong><font color="red">Do not start any labs before being told to do so by your Presenter.</font></strong>
  
The Taiwan Partner Lab 2018 session is intended to provide hands-on time with Nutanix Prism Central and Nutanix Calm.

Takeaways from the labs, at a high-level, are as follows:

- Familiarity with the architecture of a Nutanix Self-Service Portal (SSP) and Nutanix Calm configuration
- Familiarity with the prerequisites for enabling SSP and Calm
- Experience with creating Nutanix Calm blueprints
- Experience with taking an existing Nutanix Marketplace application and publishing it to a new, custom (optional) blueprint
- Using the Nutanix Calm Marketplace to launch pre-seeded application
- Using the Nutanix Calm Marketplace to launch a cloned application

.. raw:: html

  <strong><font color="red">There are a small number of labs that are not required for this session but that have been left on this site later reference.  Please don't do them, during this session.  :)</font></strong> 

.. _cluster_details:

Cluster Details
+++++++++++++++

The lab cluster has been pre-staged with the following:

**Pre-staged Images**

- **Windows2016** - Windows Server 2016 Standard ISO Image
- **CentOS7-For-Calm** - CentOS 7 Disk Image
- **NTNXVirtIO** - Nutanix VirtIO, used when creating Windows VMs (not a required part of this lab)
- **CENTOS-7.4 x2** - Used for other marketplace applications, e.g. LAMP

**Pre-staged Virtual Machines**

- **PC** VM - Provided during lab - Nutanix Prism Central 5.6

**Networks**

- **VLAN0** Network (name may be different in the live lab) - 10.134.20.0/24 - IPAM DHCP Pool 10.134.20.55-10.134.20.95

**Credentials**

- **Prism Username:** Provided during lab **Password:** Provided during lab
- **Prism Central Username:** Provided during lab **Password:** Provided during lab!
- **CVM Username:** Provided during lab **Password:** Provided during lab
- **PC VM Username:** Provided during lab **Password:** Provided during lab