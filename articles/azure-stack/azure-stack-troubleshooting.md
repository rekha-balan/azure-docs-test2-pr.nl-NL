---
title: Microsoft Azure Stack troubleshooting | Microsoft Docs
description: Azure Stack troubleshooting.
services: azure-stack
documentationcenter: ''
author: heathl17
manager: byronr
editor: ''
ms.assetid: a20bea32-3705-45e8-9168-f198cfac51af
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/12/2017
ms.author: helaw
ms.openlocfilehash: 82b0cbed78bde6940b9ac287f87d99143a78274c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553066"
---
# <a name="microsoft-azure-stack-troubleshooting"></a>Microsoft Azure Stack troubleshooting
This document provides common troubleshooting information for Azure Stack.

For the best experience, make sure that your deployment environment meets all [requirements](azure-stack-deploy.md) and [preparations](azure-stack-run-powershell-script.md) before installing. 

The recommendations for troubleshooting issues that are described in this section are derived from several sources and may or may not resolve your particular issue. If you are experiencing an issue not documented, make sure to check the [Azure Stack MSDN Forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=azurestack) for further support and additional information.

Code examples are provided as is and expected results cannot be guaranteed. This section is subject to frequent edits and updates as improvements to the product are implemented.

## <a name="known-issues"></a>Known Issues
* You may notice deployment taking longer than previous releases. 
* Logging out of portal in AD FS deployment will result in an error message.
* You may see incorrect cores/minute usage information for Windows and Linux VMs.
* Opening Storage Explorer from the storage account blade will result in an error.
* Deploying Azure Stack with ADFS and without internet access will result in licensing error messages and the host will expire after 10 days.  We advise having internet connectivity during deployment, and then testing disconnected scenarios once deployment is complete.
* Key Vault services must be created from the tenant portal or tenant API.  If you are logged in as an administrator, make sure to use the tenant portal to create new Key Vault vaults, secrets, and keys.
* There is no marketplace experience for creating VM Scale Sets, though they can be created via template.
* All Infrastructure Roles will display with a known health state, however the health state is not accurate for roles outside of Compute controller and Health controller.
* The restart action on Compute controller infrastructure role (MAS-XRP01 instance) should not be used.  
* You will see an HSM option when creating Key Vault vaults through the portal.  HSM backed vaults are not supported in Azure Stack TP3.
* VM Availability sets can only be configured with a fault domain of one and an update domain of one.  
* You should avoid restarting the one-node environment because Azure Stack infrastructure services do not start in the proper order.
* You cannot associate a load balancer with a backend network via the portal.  This task can be completed with PowerShell or with a template.
* VM Scale Set scale-in operations may fail.
* VM Scale Set resize operations fail to complete. As an example, scaling out a VM Scale Set and resizing from A1 to D2 VMs will fail.
* You will notice in the Total Memory in Region Management>Scale Units is expressed in MB instead of GB.
* You may see a blank dashboard in the portal.  If this happens, recover the dashboard by selecting the gear in the upper right of the portal, and selecting "Restore default settings".
 

## <a name="deployment"></a>Deployment
### <a name="deployment-failure"></a>Deployment failure
If you experience a failure during installation, you can use the -rerun parameter of the Azure Stack install script to try again from the failed step.  Run the following from the PowerShell session where you noticed the failure:

```PowerShell
cd C:\CloudDeployment\Setup
.\InstallAzureStackPOC.ps1 -rerun
```


### <a name="at-the-end-of-the-deployment-the-powershell-session-is-still-open-and-doesnt-show-any-output"></a>At the end of the deployment, the PowerShell session is still open and doesn’t show any output
This behavior is probably just the result of the default behavior of a PowerShell command window, when it has been selected. The POC deployment has actually succeeded but the script was paused when selecting the window. You can verify this is the case by looking for the word "select" in the titlebar of the command window.  Press the ESC key to unselect it, and the completion message should be shown after it.

## <a name="templates"></a>Templates
### <a name="azure-template-wont-deploy-to-azure-stack"></a>Azure template won't deploy to Azure Stack
Make sure that:

* The template must be using a Microsoft Azure service that is already available or in preview in Azure Stack.
* The APIs used for a specific resource are supported by the local Azure Stack instance, and that you are targeting a valid location (“local” in Azure Stack Technical Preview 3, vs the “East US” or “South India” in Azure).
* You review [this article](https://github.com/Azure/AzureStack-QuickStart-Templates/blob/master/README.md) about the Test-AzureRmResourceGroupDeployment cmdlets, which catch small differences in Azure Resource Manager syntax.

You can also use the Azure Stack templates already provided in the [GitHub repository](http://aka.ms/AzureStackGitHub/) to help you get started.

## <a name="virtual-machines"></a>Virtual machines
### <a name="default-image-and-gallery-item"></a>Default image and gallery item
You must first add a Windows Server image and gallery item before deploying VMs in Azure Stack TP3.

### <a name="after-restarting-my-azure-stack-host-some-vms-may-not-automatically-start"></a>After restarting my Azure Stack host, some VMs may not automatically start.
After rebooting your host, you may notice Azure Stack services are not immediately available.  This is because Azure Stack [infrastructure VMs](azure-stack-architecture.md#virtual-machine-roles) and RPs take a little bit to check consistency, but will eventually start automatically.

You may also notice that tenant VMs don't automatically start after a reboot of the POC host.  This is a known issue, and just requires a few manual steps to bring them online:

1.  On the POC host, start **Failover Cluster Manager** from the Start Menu.
2.  Select the cluster **S-Cluster.azurestack.local**.
3.  Select **Roles**.
4.  Tenant VMs will appear in a *saved* state.  Once all Infrastructure VMs are running, right-click the tenant VMs and select **Start** to resume the VM.

### <a name="i-have-deleted-some-virtual-machines-but-still-see-the-vhd-files-on-disk-is-this-behavior-expected"></a>I have deleted some virtual machines, but still see the VHD files on disk. Is this behavior expected?
Yes, this is behavior expected. It was designed this way because:

* When you delete a VM, VHDs are not deleted. Disks are separate resources in the resource group.
* When a storage account gets deleted, the deletion is visible immediately through Azure Resource Manager (portal, PowerShell) but the disks it may contain are still kept in storage until garbage collection runs.

If you see "orphan" VHDs, it is important to know if they are part of the folder for a storage account that was deleted. If the storage account was not deleted, it's normal they are still there.

You can read more about configuring the retention threshold and on-demand reclamation in [manage storage accounts](azure-stack-manage-storage-accounts.md).

## <a name="storage"></a>Storage
### <a name="storage-reclamation"></a>Storage reclamation
It may take up to fourteen hours for reclaimed capacity to show up in the portal. Space reclamation depends on various factors including usage percentage of internal container files in block blob store. Therefore, depending on how much data is deleted, there is no guarantee on the amount of space that could be reclaimed when garbage collector runs.

## <a name="powershell"></a>PowerShell
### <a name="resource-providers-not-registered"></a>Resource Providers not registered
When connecting to tenant subscriptions with PowerShell, you will notice that the resource providers are not automatically registered. Use the [Connect module](https://github.com/Azure/AzureStack-Tools/tree/master/Connect), or run the following command from PowerShell (after you [install and connect](azure-stack-connect-powershell.md) as a tenant): 
  
       Get-AzureRMResourceProvider | Register-AzureRmResourceProvider

## <a name="windows-azure-pack-connector"></a>Windows Azure Pack Connector
* If you change the password of the azurestackadmin account after you deploy Azure Stack TP3, you can no longer configure multi-cloud mode. Therefore, it won't be possible to connect to the target Windows Azure Pack environment.
* After you set up multi-cloud mode:
    * A user can see the dashboard only after they reset the portal settings. (In the user portal, click the portal settings icon (gear icon in the top-right corner). Under **Restore default settings**, click **Apply**.)
    * The dashboard titles may not appear. If this issue occurs, you must manually add them back.
    * Some tiles may not show correctly when you first add them to the dashboard. To fix this issue, refresh the browser.

## <a name="next-steps"></a>Next steps
[Frequently asked questions](azure-stack-faq.md)

