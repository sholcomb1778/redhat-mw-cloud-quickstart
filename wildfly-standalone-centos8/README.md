# Red Hat WildFly 18.0.1.Final on CentOS 8 (standalone mode)
<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FSpektraSystems%2Fredhat-mw-cloud-quickstart%2Fmaster%2Fwildfly-standalone-centos8%2Fazuredeploy.json" target="_blank">
    <img src="http://azuredeploy.net/deploybutton.png"/>
</a>
<a href="http://armviz.io/#/?load=https%3A%2F%2Fraw.githubusercontent.com%2FSpektraSystems%2Fredhat-mw-cloud-quickstart%2Fmaster%2Fwildfly-standalone-centos8%2Fazuredeploy.json" target="_blank">
    <img src="http://armviz.io/visualizebutton.png"/>
</a>

`Tags: WildFly 18.0.1.Final, Red Hat, CentOS, Java, Java EE, Jakarta EE, Azure, Azure VM`

<!-- TOC -->

1. [Solution Overview](#solution-overview)
2. [Template Solution Architecture](#template-solution-architecture)
3. [Licenses, Subscriptions and Costs](#licenses-subscriptions-and-costs)
4. [Prerequisites](#prerequisites)
5. [Deployment Steps](#deployment-steps)
6. [Deployment Time](#deployment-time)
7. [Validation Steps](#validation-steps)
8. [Notes](#notes)
8. [Support](#support)

<!-- /TOC -->

## Solution Overview
WildFly 18 is the latest release in a series of JBoss open-source application server offerings. WildFly 18 is an exceptionally fast, lightweight and powerful implementation of the Jakarta Platform specifications. The state-of-the-art architecture built on the Modular Service Container enables services on-demand when your application requires them.

The technology behind WildFly is also available in Red Hat JBoss Enterprise Application Platform (EAP), a hardended enterprise subscription with Red Hat's world-class support, long multi-year maintenance cycles and exclusive content. To obtain a Red Hat Subscription Management (RHSM) account for JBoss EAP, go to: www.redhat.com. Red Hat Subscription Management (RHSM) is a customer-driven, end-to-end solution that provides tools for subscription status and management and integrates with Red Hat's system management tools.

This Azure quickstart template deploys a web application named JBoss-EAP on Azure on a standalone node of WildFly 18.0.1.Final running on CentOS 8 VM.

## Template Solution Architecture 

This template creates all the Azure compute resources to run WildFly 18.0.1.Final on top of CentOS 8.0 VM. The following resources are created by this template:

- CentOS 8 VM 
- Public IP 
- Virtual Network 
- Network Security Group 
- WildFly 18.0.1.Final
- Sample Java application named JBoss-EAP on Azure deployed on WildFly

Following is the Architecture:

![alt text](images/wildfly-arch.png)

To learn more about WildFly 18.0.0.Final, check out:
https://docs.wildfly.org/18/

## Licenses, Subscriptions and Costs 

Click [here](https://azure.microsoft.com/en-us/pricing/details/virtual-machines/linux/#linux) to view the pricing details of CentOS 8 image which is used for this template. WildFly is free to download and use and does not require a Red Hat Subscription or any License, for more details click [here](https://www.wildfly.org/).

## Prerequisites 

1. Azure Subscription (CentOS-Based 8.0 is an [Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/openlogic.centos?tab=Overview) product)

2. To create the VM, you will need to:

    - Choose an admin username and password/ssh key for your VM.  

    - Choose DNS Label Prefix for the public IP which should be unique. Note that this will also be the name of your VM.

    - Choose a WildFly username and password to enable the WildFly Admin Console and deployment method.

## Deployment Steps  

Build your environment with WildFly 18.0.1.Final on top of CentOS 8.0 on Azure in a few simple steps:  
1. Launch the template by clicking the Deploy to Azure button.  
2. Fill in the following parameter values and accept the terms and conditions before clicking on Purchase.

    - **Subscription** - Choose the appropriate subscription where you would like to deploy.

    - **Resource Group** - Create a new Resource Group or you can select an existing one.

    - **Location** - Choose the appropriate location for your deployment.

    - **Admin Username** - User account name for logging into your CentOS VM.

    - **Authentication Type** - Type of authentication to use on the Virtual Machine.

    - **Admin Password or Key** - User account password/ssh key for logging into your CentOS VM.

    - **DNS Label Prefix** - DNS Label for the Public IP and this is also the name of your VM. Must be lowercase. It should match with the following regular expression: ^[a-z][a-z0-9-]{1,61}[a-z0-9]$ or it will raise an error.

    - **WildFly Username** - Username for WildFly Console Manager.

    - **WildFly Password** - User account password for WildFly Console Manager.

    - **VM Size** - Choose the appropriate size of the VM from the dropdown options.

    - Leave the rest of the parameter values as is and proceed.

## Deployment Time 

The deployment takes less than 10 minutes to complete.

## Validation Steps

- Once the deployment is successful, go to the VM and copy the DNS Name of the VM.
- Open a web browser and go to **http://<PUBLIC_HOSTNAME>:8080/dukes/** and you should see the application running:

  ![alt text](images/app.png)

- To access the administration console go to **http://<PUBLIC_HOSTNAME>:8080** and click on the link to Administration Console and enter the Wildfly username and password.

  ![alt text](images/wildfly-console.png)

## Notes

If you're interested in Red Hat JBoss EAP Azure Quickstart templates, you can find it here:

*  <a href="https://github.com/SpektraSystems/redhat-mw-cloud-quickstart/tree/master/jboss-eap-standalone-rhel7" target="_blank"> [Red Hat - JBoss EAP 7.2 on RHEL 7.7 VM (standalone mode)]</a> - Standalone JBoss EAP 7.2 with a sample web app on a RHEL 7.7 Azure VM.

*  <a href="https://github.com/SpektraSystems/redhat-mw-cloud-quickstart/tree/master/jboss-eap-standalone-rhel8" target="_blank"> [Red Hat - JBoss EAP 7.2 on RHEL 8.0 (standalone mode)]</a> - Standalone JBoss EAP 7.2 with a sample web app on a RHEL 8.0 Azure VM.

## Support 

For any support related questions, issues or customization requirements, please contact info@spektrasystems.com