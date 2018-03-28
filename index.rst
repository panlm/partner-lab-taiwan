.. title:: Tech Summit 2018

.. _intro-docs:

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
  github/github
  afs/index
  xtract-vm/xtract-vm
  xtract-db/xtract-db
  xray/index

.. toctree::
  :maxdepth: 2
  :caption:     Optional Labs
  :name: _opt-labs
  :hidden:

  karan/karan_sa_setup
  calm_mssql/calm_mssql
  citrix/index
  git/gitlab
  hycu/index
  docker/calm_workshop_lab7_docker
  .. k8s/index
  ansible/calm_workshop_lab6
  rest/calm/calm_workshop_lab5_api
  .. terraform/index

.. toctree::
  :maxdepth: 2
  :caption:     Other Resources
  :name: _resources
  :hidden:

  .. jenkins/index
  .. chef/index
  .. puppet/index

.. raw:: html

    <div class="row">
        <div class="col-md-6">
            <h2>Need Support?</h2>
            <p>Join us in #techsummit2018 on Slack for questions, comments, and important announcements.</p>
            <p><a class="btn btn-secondary" href="slack://channel?id=C7ELNM1KL&amp;team=T0252CLM8" role="button">Join Channel &raquo;</a></p>
        </div>
        <div class="col-md-6">
            <h2>Awards and Prizes</h2>
            <p>In addition to bragging rights and special recognition at SKO, the winning team will receive a Nutanix Tech Summit branded fleece vest from The North Face.</p>
        </div>
    </div>
    <hr>

Getting Started
===============

.. note::

  Due to resource limitations, many labs are designed to be completed as a group. The Overview section of each lab will indicate whether the lab should be completed once per group/cluster or if it can be performed individually. **Do Not Start Labs Before Electing a Team Lead and Consulting Your Team Coach**.

Following presentations on Tuesday, you will have approximately 4 hours to complete the **Required Labs**.

Beginning on Wednesday you will be provided with a customer challenge. Your goal is to build and propose a solution using Nutanix and optional 3rd party technologies. The **Optional Labs** provide step by step guides for additional technologies you may find useful for your proposed solution. Bonus points can be earned by incorporating additional technologies (Chef, Puppet, Jenkins, Nagios, etc.) not covered in **Optional Labs**.

Each team has been provided a four node cluster running AHV and AOS 5.5.1. It is **HIGHLY RECOMMENDED** that you access the environment via a `Citrix XenDesktop <https://citrixready.nutanix.com>`_ session.

**Do Not Start Labs Before Electing a Team Lead and Consulting Your Team Coach**

Each cluster has been pre-staged with the following:

.. **Challenge**


.. `Uptick Capital English <https://s3.us-east-2.amazonaws.com/s3.nutanixtechsummit.com/challenge/challenge-uptick-capital-english.pdf>`_

.. `Uptick Capital Chinese <https://s3.us-east-2.amazonaws.com/s3.nutanixtechsummit.com/challenge/challenge-uptick-capital-chinese.pdf>`_

.. `Uptick Capital Korean <https://s3.us-east-2.amazonaws.com/s3.nutanixtechsummit.com/challenge/challenge-uptick-capital-korean.pdf>`_

.. `Uptick Capital Japanese <https://s3.us-east-2.amazonaws.com/s3.nutanixtechsummit.com/challenge/challenge-uptick-capital-japanese.pdf>`_

**Images**

- All required images have been pre-staged in your cluster's AHV Image Service

**Virtual Machines**

- **PC** VM - 10.21.XX.39 - Nutanix Prism Central 5.5.0.6
- **DC** VM - 10.21.XX.40 - ntnxlab.local Domain Controller
- **XD** VM - 10.21.XX.41 - Citrix XenDesktop 7.15 Delivery Controller/StoreFront/License Server
- **HYCU** VM - 10.21.XX.44 - Comtrade HYCU 2.0.0
- **X-Ray** VM - 10.21.XX.45 - Nutanix X-Ray 2.3

**Credentials**

- **Prism Username:** admin **Password:** techX2018!
- **Prism Central Username:** admin **Password:** techX2018!
- **CVM Username:** nutanix **Password:** techX2018!
- **PC VM Username:** nutanix **Password:** nutanix/4u
- **Domain Username** NTNXLAB\\Administrator **Password:** nutanix/4u

**Networks**

- **Primary** Network - 10.21.XX.1/25 - IPAM DHCP Pool 10.21.XX.50-10.21.XX.124
- **Secondary** Network - 10.21.XX.129/25 - IPAM DHCP Pool 10.21.XX.132-10.21.XX.253
- **Link-Local** Network - **DO NOT ENABLE IPAM**

`Click here to view details of your team cluster assignment. <https://docs.google.com/spreadsheets/d/16enUOq3RAOvEz3RmL1zywxDvvIjAlvkqa3StauCeCEk>`_

`Click here to view the Team Leader Playbook. <https://drive.google.com/open?id=1oYaZgawgZP-pjZl8Jj_Po1byAitVnRzv>`_

`Click here to view the Tech Summit EMEA Challenge. <https://drive.google.com/open?id=1BXlnPI9Uvx-JuzNNskOq4VtDplSR3reL>`_
