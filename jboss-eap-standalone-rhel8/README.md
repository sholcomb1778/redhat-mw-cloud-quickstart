# VM-Redhat - JBoss EAP 7 on RHEL 8 standalone mode
<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FSpektraSystems%2Fredhat-mw-cloud-quickstart%2Fmaster%2Fjboss-eap-standalone-rhel8%2Fazuredeploy.json" target="_blank">
    <img src="http://azuredeploy.net/deploybutton.png"/>
</a>
<a href="http://armviz.io/#/?load=https%3A%2F%2Fraw.githubusercontent.com%2FMicrosoft%2Fredhat-mw-cloud-quickstart%2Fmaster%2Fjboss-eap-standalone-rhel7%2Fazuredeploy.json" target="_blank">
    <img src="http://armviz.io/visualizebutton.png"/>
</a>

`Tags: JBoss, EAP, Red Hat, EAP7, RHEL8, Azure, Azure VM, Cluster`

<!-- TOC -->

1. [Solution Overview](#solution-overview)
2. [Template Solution Architecture](#template-solution-architecture)
3. [Licenses, Subscriptions and Costs](#licenses-and-costs)
4. [Prerequisites](#prerequisites)
5. [Deployment Steps](#deployment-steps)
6. [Deployment Time](#deployment-time)
7. [Post Deployment Steps](#post-deployment-steps)

<!-- /TOC -->

## Solution Overview

JBoss EAP is an open source platform for highly transactional, web-scale Java applications. EAP combines the familiar and popular Jakarta EE specifications with the latest technologies, like Microprofile, to modernize your applications from traditional Java EE into the new world of DevOps, cloud, containers, and microservices. EAP includes everything needed to build, run, deploy, and manage enterprise Java applications in a variety of environments, including on-premise, virtual environments, and in private, public, and hybrid clouds.

This template creates all of the compute resource to run JBoss EAP 7 on top of RHEL 8.0.


## Template Solution Architecture
This template creates all of the Azure compute resources to run JBoss EAP 7 on top of RHEL 8.0.  THe followoing are created by this template: 

- RHEL 8.0 VM 
- Public DNS 
- Private Virtual Network 
- Security Configuration 
- JBoss EAP 7
- Sample application deployed to JBoss EAP 7

Following is the Architecture :
<img src="images/RHEL8-Arch.PNG" width="800">

To learn more about JBoss Enterprise Application Platform, visit:
https://access.redhat.com/documentation/en-us/red_hat_jboss_enterprise_application_platform/7.2/

## Licenses, Subscriptions and Costs

This template uses a RHEL 8.0 image which is a Pay-as-you-go (PAYG) image and does not require the user to license it.  The VM will be licensed automatically after the instance is launched for the first time and the user will be charged hourly in addition to Microsoft's Linux VM rates.  Click [here](https://azure.microsoft.com/en-gb/pricing/details/virtual-machines/linux/#red-hat) for pricing details. You will also need to have a RedHat Subscription.  Click [here](https://access.redhat.com/products/red-hat-subscription-management) to learn more about Red Hat Subscription Manager (RHSM), pricing and registeration for RHSM.

## Prerequisites

1. Azure Subscription with specified payment method (RHEL 8 is a marketplace product and requires a payment method to be specified in the Azure Subscription)

2. To deploy the template, you will need to:

   - **Admin Username** and password.
    
   - **VM Name** 

   - **EAP username** and password.
    
   - **RHSM Username** and password
    
   - **SSH Key data** which is an SSH RSA public 

## Deployment Steps

Build your environment with EAP 7.2 on top of RHEL 8.0 on Azure in a few simple steps:

   - **Subscription** - Choose the the appropriate subscription where you would like to deploy.

   - **Resource Group** - Create a new Resource Group or you can select an existing one.

   - **Location** - Choose the appropriate location for your deployment.

   - **Admin Username** - User account name for logging into your RHEL VM.

   - **Admin Password** - User account password for logging into your RHEL VM.

   - **EAP Username** - User name for EAP Console.

   - **EAP Password** - User account password for EAP Console.
    
   - **RHSM Username** - User name for Red Hat account.

   - **RHSM Password** - User account password for RedHat account.
    
   - **SSH Key Data** - Generate an SSH key using Puttygen and provide the data here.

   - Leave the rest of the Parameter Values (artifacts and Location) as it is and proceed to purchase.
    
## Deployment Time 

The deployment takes less than 10 minutes to complete.

## Post Deployment Steps

- Once the deployment is successful, go the VM and copy the Public IP of the VM.
- Open a web browser and go to http://<PUBLIC_HOSTNAME>:8080/dukes/ and you should see the application running
If you want to access the administration console go to http://<PUBLIC_HOSTNAME>:8080 and click on the link Administration Console and enter EAP username and password to see the console.
