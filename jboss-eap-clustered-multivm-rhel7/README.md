# JBoss EAP 7.2 on RHEL 7.7 (clustered, multi-VM)

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FSpektraSystems%2Fredhat-mw-cloud-quickstart%2Fmaster%2Fjboss-eap-clustered-multivm-rhel7%2Fazuredeploy.json" target="_blank">
    <img src="https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/1-CONTRIBUTION-GUIDE/images/deploytoazure.png"/>
</a>
<a href="http://armviz.io/#/?load=https%3A%2F%2Fraw.githubusercontent.com%2FSpektraSystems%2Fredhat-mw-cloud-quickstart%2Fmaster%2Fjboss-eap-clustered-multivm-rhel7%2Fazuredeploy.json" target="_blank">
    <img src="https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/1-CONTRIBUTION-GUIDE/images/visualizebutton.png"/>
</a>

`Tags: JBoss, Red Hat, EAP 7.2, Cluster, Load Balancer, RHEL 7.7, Azure, Azure VM, Java EE`

<!-- TOC -->

1. [Solution Overview](#solution-overview)
2. [Template Solution Architecture](#template-solution-architecture)
3. [Subscriptions and Costs](#subscriptions-and-costs)
4. [Prerequisites](#prerequisites)
5. [Deployment Steps](#deployment-steps)
6. [Deployment Time](#deployment-time)
7. [Validation Steps](#validation-steps)
8. [Troubleshoot](#troubleshoot)
9. [Support](#support)

<!-- /TOC -->

## Solution Overview

JBoss EAP (Enterprise Application Platform) is an open source platform for highly transactional, web-scale Java applications. EAP combines the familiar and popular Jakarta EE specifications with the latest technologies, like Microprofile, to modernize your applications from traditional Java EE into the new world of DevOps, cloud, containers, and microservices. EAP includes everything needed to build, run, deploy, and manage enterprise Java applications in a variety of environments, including on-premises, virtual environments, and in private, public, and hybrid clouds.

Red Hat Subscription Management (RHSM) is a customer-driven, end-to-end solution that provides tools for subscription status and management and integrates with Red Hat's system management tools. To obtain an RHSM account for JBoss EAP, go to: www.redhat.com.

## Template Solution Architecture

This template creates all the Azure compute resources to run JBoss EAP 7.2 cluster on top of n number of RHEL 7.7 VMs where n is decided by the user and all the VMs are added to the backend pool of a Load Balancer. The following resources are created by this template:

- RHEL 7.7 VMs
- 1 Load balancer
- Public IPs for Load Balancer and VMs
- Virtual Network with single subnet
- JBoss EAP 7.2
- Sample application called eap-session-replication deployed on JBoss EAP 7.2
- Network Security Group
- Storage Account

Following is the Architecture:

![alt text](images/arch.png)

To learn more about the JBoss Enterprise Application Platform, visit:
https://access.redhat.com/documentation/en-us/red_hat_jboss_enterprise_application_platform/7.2/

## Licenses, Subscriptions and Costs

If you select the RHEL OS License type as PAYG (Pay-As-You-Go), this template uses the On-Demand Red Hat Enterprise Linux 8.0 Pay-As-You-Go image from the Azure Gallery.

> When using the On-Demand image, there is an additional hourly RHEL subscription charge for using this image on top of the normal compute, network and storage costs. At the same time, the instance will be registered to your Red Hat subscription, so you will also be using one of your entitlements. This will lead to "double billing". To avoid this, you would need to build your own RHEL image, which is defined in this [Red Hat KB article](https://access.redhat.com/articles/uploading-rhel-image-to-azure).

If you have a valid Red Hat subscription, register for Cloud Access, [request access](https://access.redhat.com/public-cloud) to the BYOS RHEL image in the Private Azure Marketplace and follow the below mentioned steps to avoid the double billing.

Check [Red Hat Enterprise Linux pricing](https://azure.microsoft.com/en-us/pricing/details/virtual-machines/red-hat/) for details on the VM price.

You can select the RHEL OS License type as BYOS (Bring-Your-Own-Subscription) for deploying the template to avoid double billing. Your RHSM account must have both Red Hat Enterprise Linux entitlement (for subscribing the RHEL OS for the VM) and EAP entitlement and you will have to enter both the pool IDs as mentioned in the template. To provision the RHEL-BYOS VM in your subscription, you will have to enable it in the Cloud Access from Red Hat portal and activate Red Hat Gold Images for your subscription. You can enable subscription for cloud access by following the instructions mentioned [here](https://access.redhat.com/documentation/en-us/red_hat_subscription_management/1/html/red_hat_cloud_access_reference_guide/con-enable-subs) and activate the Red Hat Gold Images by following the instructions mentioned [here](https://access.redhat.com/documentation/en-us/red_hat_subscription_management/1/html/red_hat_cloud_access_reference_guide/using_red_hat_gold_images#con-azure-access). Once your Azure subscription is enabled, please follow this [link](https://docs.microsoft.com/en-us/azure/virtual-machines/workloads/redhat/byos) to accept the Marketplace terms for RHEL-BYOS image from your Azure subscription.

Note that in both the cases your RHSM account needs EAP entitlement to use the Enterprise Application Platform. You can get an evaluation account for EAP from [here](https://access.redhat.com/products/red-hat-jboss-enterprise-application-platform/evaluation).

Click [here](https://access.redhat.com/products/red-hat-subscription-management) to know more about RHSM.

## Prerequisites

1. Azure Subscription with the specified payment method (RHEL 7.7 is an [Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/RedHat.RedHatEnterpriseLinux77-ARM?tab=Overview) product and requires a payment method to be specified in the Azure Subscription). If you select the RHEL OS License type as BYOS (Bring-Your-Own-Subscription), please follow steps mentioned under section 'Licenses, Subscriptions and Costs'.

2. To deploy the template, you will need:

    - **Admin Username** and password/ssh key data which is an SSH RSA public key for your VM. 

    - **JBoss EAP Username** and password

    - **RHSM Username** and password
    
## Deployment Steps

Build your environment with JBoss EAP 7.2 cluster on top of n number of RHEL 7.7 VMs where n is decided by the user and all the VMs are added to the backend pool of a Load Balancer on Azure in a few simple steps:
1. Launch the template by clicking the **Deploy to Azure** button.  
2. Complete the following parameter values and accept the terms and conditions before clicking on the **Purchase** button.

    - **Subscription** - Choose the appropriate subscription where you would like to deploy.

    - **Resource Group** - Create a new Resource Group or you can select an existing one.

    - **Location** - Choose the appropriate location for your deployment.

    - **Admin Username** - User account name for logging into your RHEL VM.
    
    - **Authentication Type** - Type of authentication to use on the Virtual Machine.

    - **Admin Password or SSH Key** - User account password/ssh key data which is an SSH RSA public key for logging into your RHEL VM.

    - **JBoss EAP Username** - Username for JBoss EAP Console.

    - **JBoss EAP Password** - User account password for JBoss EAP Console.

    - **RHEL OS License Type** - Choose the type of RHEL OS License from the dropdown options for deploying your Virtual Machine.

    - **RHSM Username** - Username for the Red Hat account.

    - **RHSM Password** - User account password for the Red Hat account.
   
    - **RHSM Pool ID for EAP** - Red Hat Subscription Manager Pool ID (Should have EAP entitlement)

    - **RHSM Pool ID for RHEL OS** - Red Hat Subscription Manager Pool ID (Should have RHEL entitlement). Mandartory if you select the BYOS RHEL OS License type. You can leave it blank if you select RHEL OS License type PAYG.

    - **Storage Replication** - Choose the Replication Strategy for your Storage account.

    - **VM Size** - Choose the appropriate size of the VM from the dropdown options.

    - **Number of Instances** - Number of VMs to be deployed.

    - Leave the rest of the parameter values (artifacts and location) as is and proceed to purchase.
    
## Deployment Time 

The deployment takes approximately 10 minutes to complete.

## Validation Steps

- Once the deployment is successful, go to the outputs section of the deployment to obtain the App URL.

  ![alt text](images/outputs.png)

- To obtain the Public IP of a VM, go to the VM details page. Under settings section go to Networking and copy the NIC Public IP. Open a web browser and go to **http://<PUBLIC_IP_Address>:8080** and you should see the web page as follows. Use the same Public IP to Login to the VM.

  ![alt text](images/eap.png)

- To access the administration console, click on the **Administration Console** shown in the above image and enter JBoss EAP Username and password to access the console of the respective VM.

  ![alt text](images/eap-admin-console.png)

- To access the LB App UI console, enter the App URL that you copied from the output page and paste it in a browser. The web application displays the *Session ID*, *Session Counter* and *Timestamp* (these are variables stored in the session that are replicated) and the container Private IP address that the web page and session is being hosted from. Clicking on the Increment Counter updates the session counter and clicking on Refresh will refresh the page.

  ![alt text](images/eap-session.png)
  
  ![alt text](images/eap-session-rep.png)

- Note that in the EAP Session Replication page of Load Balancer, the private IP displayed is that of one of the VMs. If you click on Increment Counter/Refresh button when you stop VM,restart VM or if the service the VM corresponding to the Private IP displayed is down, the private IP displayed will change to that of another VM but the Session ID remains the same which shows that the Session got replicated.

  ![alt text](images/eap-ses-rep.png)

## Troubleshoot

This section is to give you an idea on troubleshooting the issues that you might face when you deploy this template. If the parameter criteria are not fulfilled(like the Admin Password criteria) or if any parameter that are mandatory are not filled in the parameters section then the deployment will not start. Also make sure that you accept the terms and conditions mentioned before you click on Purchase. Once the deployment starts you can clearly see the resources getting deployed on the deployment page and if any deployment fails you can see which of the resources failed and check the deployment failure message for more details. If your deployment fails due to the script extension, you can see that the VM is already deployed so please login to the VM to check the logs for more troubleshooting. The logs are stored in the file jbosseap.install.log in path /var/lib/waagent/custom-script/download/0. The script can fail due to various reasons like incorrect RHSM Username/Password. This log file give you a clear message on why the script failed and exited. So you can use this log file to detect errors and troubleshoot them. Please run the following commands to check the logs once you login to the VM.

- Switch to Root user to avoid permission issues

    `sudo su -`

- Enter your VM admin Password if prompted. It might prompt you for password only if you selected the Authentication Type as Password.

- Move to the directory where the logs are stored

    `cd /var/lib/waagent/custom-script/download/0`

- View the logs in jbosseap.install.log

    `more jbosseap.install.log`

If you select BYOS as RHEL OS License type, then please make sure that you complete some pre-requisite steps before you start the deployment. To provision the RHEL-BYOS VM in your subscription, you will have to enable it in the Cloud Access from Red Hat portal and activate Red Hat Gold Images for your subscription. You can enable subscription for cloud access by following the instructions mentioned [here](https://access.redhat.com/documentation/en-us/red_hat_subscription_management/1/html/red_hat_cloud_access_reference_guide/con-enable-subs) and activate the Red Hat Gold Images by following the instructions mentioned [here](https://access.redhat.com/documentation/en-us/red_hat_subscription_management/1/html/red_hat_cloud_access_reference_guide/using_red_hat_gold_images#con-azure-access). If this is not done you will face issue with validating the template due to marketplace purchase eligibility failed.

Once your Azure subscription is enabled, please follow this [link](https://docs.microsoft.com/en-us/azure/virtual-machines/workloads/redhat/byos) to accept the Marketplace terms for RHEL-BYOS image from your Azure subscription otherwise your template will fail.

## Support

For any support related questions, issues or customization requirements, please contact info@spektrasystems.com
