# JBoss EAP 7.2 on RHEL 8.0 (clustered, multi-VM)

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FSpektraSystems%2Fredhat-mw-cloud-quickstart%2Fmaster%2Fjboss-eap-clustered-multivm-rhel8%2Fazuredeploy.json" target="_blank">
    <img src="https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/1-CONTRIBUTION-GUIDE/images/deploytoazure.png"/>
</a>
<a href="http://armviz.io/#/?load=https%3A%2F%2Fraw.githubusercontent.com%2FSpektraSystems%2Fredhat-mw-cloud-quickstart%2Fmaster%2Fjboss-eap-clustered-multivm-rhel8%2Fazuredeploy.json" target="_blank">
    <img src="https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/1-CONTRIBUTION-GUIDE/images/visualizebutton.png"/>
</a>

`Tags: JBoss, Red Hat, EAP 7.2, Cluster, Load Balancer, RHEL 8.0, Azure, Azure VM, Java EE`

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

This Azure Resource Manager (ARM) template creates all the Azure compute resources to run JBoss EAP 7.2 cluster on top of n number of RHEL 8.0 VMs where n is decided by the user and all the VMs are added to the backend pool of a Load Balancer. The following resources are created by this template:

- RHEL 8.0 VMs
- 1 Load Balancer
- Public IPs for Load Balancer and VMs
- Virtual Network with single subnet
- JBoss EAP 7.2
- Sample application called eap-session-replication deployed on JBoss EAP 7.2
- Network Security Group
- Storage Account

Following is the Architecture:

![alt text](images/arch.png)

To learn more about the JBoss Enterprise Application Platform, visit [Red Hat EAP 7.2 documentation](https://access.redhat.com/documentation/en-us/red_hat_jboss_enterprise_application_platform/7.2/)

## Subscriptions and Costs
READ the instructions in their entirety before deploying!

[Linux virtual machines in Azure](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/) provides additional documentation for deploying VMs in Azure.  

By default, this template uses the On-Demand Red Hat Enterprise Linux image from the Azure Gallery. When using the On-Demand image, there is an additional hourly RHEL subscription charge for using this image on top of the normal compute, network and storage costs. At the same time, the instance will be registered to your Red Hat subscription, so you will also be using one of your entitlements. This will lead to "double billing". To avoid this, you need to build your own RHEL image, which is defined in [this Red Hat KB article](https://access.redhat.com/articles/uploading-rhel-image-to-azure). Check [Red Hat Enterprise Linux pricing](https://azure.microsoft.com/en-us/pricing/details/virtual-machines/red-hat/) for details on the VM price.

If you have a valid Red Hat subscription, register for Cloud Access and [request access](http://aka.ms/rhel-byos) to the BYOS RHEL image in the Private Azure Marketplace to avoid the double billing. To use a 3rd party marketplace offer (such as the BYOS private image), you need to provide the following information for the offer - publisher, offer, sku, and version. You also need to enable the offer for programmatic deployment.

If you are only using one pool ID for all nodes, then enter the same pool ID for both 'rhsmPoolId' and 'rhsmBrokerPoolId'.

In addition you also need to have a Red Hat account to register to Red Hat Subscription Manager (RHSM) and install JBoss EAP. If you have a valid Red Hat subscription, register for Cloud Access, [request access](https://access.redhat.com/public-cloud) to the BYOS RHEL image in the Private Azure Marketplace and follow the below mentioned steps.

You can select the RHEL OS License type as BYOS (Bring-Your-Own-Subscription) for deploying the template to avoid double billing. Your RHSM account must have both Red Hat Enterprise Linux entitlement (for subscribing the RHEL OS for the VM) and EAP entitlement and you will have to enter both the pool IDs as mentioned in the template. To provision the RHEL-BYOS VM in your subscription, you will have to enable it for Cloud Access from the Red Hat Customer Portal and activate Red Hat Gold Images for your subscription. You can enable your subscription for cloud access by following the instructions in this Red Hat KB article: [Enabling and Maintaining Subscriptions for Cloud Access](https://access.redhat.com/documentation/en-us/red_hat_subscription_management/1/html/red_hat_cloud_access_reference_guide/con-enable-subs) and activate the Red Hat Gold Images by following the instructions defined in this Red Hat KB article for [enabling Azure Access](https://access.redhat.com/documentation/en-us/red_hat_subscription_management/1/html/red_hat_cloud_access_reference_guide/using_red_hat_gold_images#con-azure-access). Once your Azure subscription is enabled follow the Microsoft instructions for [Azure Marketplace terms](https://docs.microsoft.com/en-us/azure/virtual-machines/workloads/redhat/byos) to accept the Marketplace terms for RHEL-BYOS image from your Azure subscriptions.

Note that in both cases your RHSM account needs EAP entitlement to use the Enterprise Application Platform. If you don't have EAP entitlement, obtain a [JBoss EAP evaluation subscription](https://access.redhat.com/products/red-hat-jboss-enterprise-application-platform/evaluation) before you get started.

Click this [Red Hat KB article on RHSM](https://access.redhat.com/products/red-hat-subscription-management) to learn more about Red Hat Subscription Manager.

## Prerequisites

1. Azure Subscription with the specified payment method.  RHEL 8 is an [Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/RedHat.RedHatEnterpriseLinux80-ARM?tab=Overview) product and requires a payment method to be specified in the Azure Subscription. If you select the RHEL OS License Type as BYOS (Bring-Your-Own-Subscription), follow the steps mentioned under section 'Subscriptions and Costs'.

2. To deploy the template, you will need:

    - **Admin Username** and password/ssh key data which is an SSH RSA public key for your VM. 

    - **JBoss EAP Username** and password

    - **RHSM Username** and password
    
## Deployment Steps

Build your environment with JBoss EAP 7.2 cluster on top of n number of RHEL 8.0 VMs where n is decided by the user and all the VMs are added to the backend pool of a Load Balancer on Azure in a few simple steps:  

1. Launch the template by clicking the **Deploy to Azure** button.  
2. Complete the following parameter values and accept the Terms and Conditions before clicking on the **Purchase** button.

    - **Subscription** - Choose the appropriate subscription for deployment.

    - **Resource Group** - Create a new Resource Group or select an existing one.

    - **Location** - Choose the appropriate location for deployment.

    - **Admin Username** - User account name for logging into the RHEL VM.
    
    - **Authentication Type** - Type of authentication to use on the Virtual Machine.

    - **Admin Password or SSH Key** - User account password/ssh key data which is an SSH RSA public key for logging into your RHEL VM.

    - **JBoss EAP Username** - Username for JBoss EAP Console.

    - **JBoss EAP Password** - User account password for JBoss EAP Console.

    - **RHEL OS License Type** - Choose the type of RHEL OS License from the dropdown options for deploying your Virtual Machine.  You will have either the option of PAYG by default or BYOS. 

    - **RHSM Username** - Username for the Red Hat account.

    - **RHSM Password** - User account password for the Red Hat account.
   
    - **RHSM Pool ID for EAP** - Red Hat Subscription Manager Pool ID (Should have EAP entitlement)

    - **RHSM Pool ID for RHEL OS** - Red Hat Subscription Manager Pool ID (Should have RHEL entitlement). This is mandatory when selecting BYOS RHEL OS as License Type.  This should be left blank when selecting RHEL OS License Type PAYG.

    - **Storage Replication** - Choose the [Replication Strategy](https://docs.microsoft.com/en-us/azure/storage/common/storage-redundancy) for your Storage account.

    - **VM Size** - Choose the appropriate size of the VM from the dropdown options.

    - **Number of Instances** - Number of VMs to be deployed.

    - Leave the rest of the parameter values (artifacts and location) as is, accept the Terms & Conditions and proceed to purchase.
    
## Deployment Time 

The deployment takes approximately 10 minutes to complete.

## Validation Steps

- Once the deployment is successful, go to the outputs section of the deployment to obtain the App URL.

  ![alt text](images/outputs.png)

- To obtain the Public IP of a VM, go to the VM details page. Under settings section go to Networking and copy the NIC Public IP. Open a web browser and go to **http://<PUBLIC_IP_Address>:8080** and you should see the web page as follows. Use the same Public IP to Login to the VM.

  ![alt text](images/eap.png)

- To access the administration console, click on the **Administration Console** shown in the above image and enter JBoss EAP Username and password to access the console of the respective VM.

  ![alt text](images/eap-admin-console.png)

- To access the LB App UI console, enter the App URL that you copied from the output page and paste it in a browser. The web application displays the *Session ID*, *Session counter* and *Timestamp* (these are variables stored in the session that are replicated) and the container Private IP address that the web page and session is being hosted from. Clicking on the Increment Counter updates the session counter and clicking on Refresh will refresh the page.

  ![alt text](images/eap-session.png)
  
  ![alt text](images/eap-session-rep.png)

- Note that in the EAP Session Replication page of Load Balancer, the private IP displayed is that of one of the VMs. If you click on Increment Counter/Refresh button when you stop VM, restart VM or if the service the VM corresponding to the Private IP displayed is down, the private IP displayed will change to that of another VM but the Session ID remains the same which shows that the Session got replicated.

  ![alt text](images/eap-ses-rep.png)

## Troubleshoot

This section provides information on troubleshooting some of the issues you might face when deploying this template. If the parameter criteria are not fulfilled (ex.- the Admin Password criteria) or if any mandatory parameters are not provided, the deployment will not start. Also the Terms & Conditions mentioned must be accepted before clicking on Purchase. Once the deployment starts the resources being deployed will be visible on the deployment page and in the case of any deployment failure a more detailed failure message is available.  If the deployment fails due to the script extension, you can see the VM is already deployed so login to the VM to check the logs for more troubleshooting detail. The logs are stored in the file jbosseap.install.log in path /var/lib/waagent/custom-script/download/0 or /var/lib/waagent/custon-script/download/1. The script can fail due to various reasons like incorrect RHSM Username/Password. This log file gives you a clear message on why the script failed and exited.  Use these logs to detect and correct errors.  Run the following commands to check the logs once you login to the VM.

- Switch to Root user to avoid permission issues
`sudo su -`

- Enter you VM Admin Password if prompted. It might prompt you for password only if you selected the Authentication Type as Password.

- Move to the directory where the logs are stored
`cd /var/lib/waagent/custom-script/download`

- List the folder inside the download folder using 'ls' command and move into the folder displayed (either 0 or 1) using 'cd' command.

- View the logs in jbosseap.install.log
`vi jbosseap.install.log`

If you select BYOS as RHEL OS License Type make sure to complete the prerequisite steps before starting your deployment.  To provision the RHEL-BYOS VM in your subscription, you must enable it for Cloud Access from the Red Hat Customer Portal and activate Red Hat Gold Images for your subscription. You can enable you subscription for Cloud Access by following the instructions in this Red Hat KB article: [Enabling and Maintaining Subscriptions for Cloud Access](https://access.redhat.com/documentation/en-us/red_hat_subscription_management/1/html/red_hat_cloud_access_reference_guide/con-enable-subs) and activate the Red Hat Gold Images by following the instructions defined in this Red Hat KB article for [enabling Azure Access](https://access.redhat.com/documentation/en-us/red_hat_subscription_management/1/html/red_hat_cloud_access_reference_guide/using_red_hat_gold_images#con-azure-access). If this is not done you will encounter errors with validating the template due to 'marketplace purchase eligibility failed'.

Once your Azure subscription is enabled follow the Microsoft instructions for [Azure Marketplace terms](https://docs.microsoft.com/en-us/azure/virtual-machines/workloads/redhat/byos) to accept the Marketplace terms for RHEL-BYOS image from your Azure subscriptions; otherwise your template will fail.

## Support

For any support related questions, issues or customization requirements, please contact info@spektrasystems.com
