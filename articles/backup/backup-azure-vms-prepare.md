---
title: Preparing your environment to back up Azure virtual machines | Microsoft Docs
description: Make sure your environment is prepared for backing up virtual machines in Azure
services: backup
documentationcenter: ''
author: markgalioto
manager: carmonn
editor: ''
keywords: backups; backing up;
ms.assetid: 238ab93b-8acc-4262-81b7-ce930f76a662
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/10/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: 9851f54c31ef54f963492900f8d9699dbeaa8ac5
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556182"
---
# <a name="prepare-your-environment-to-back-up-azure-virtual-machines"></a><span data-ttu-id="cee3b-104">Prepare your environment to back up Azure virtual machines</span><span class="sxs-lookup"><span data-stu-id="cee3b-104">Prepare your environment to back up Azure virtual machines</span></span>
> [!div class="op_single_selector"]
> * [Resource Manager model](backup-azure-arm-vms-prepare.md)
> * [Classic model](backup-azure-vms-prepare.md)
>
>

<span data-ttu-id="cee3b-107">Before you can back up an Azure virtual machine (VM), there are three conditions that must exist.</span><span class="sxs-lookup"><span data-stu-id="cee3b-107">Before you can back up an Azure virtual machine (VM), there are three conditions that must exist.</span></span>

* <span data-ttu-id="cee3b-108">You need to create a backup vault or identify an existing backup vault *in the same region as your VM*.</span><span class="sxs-lookup"><span data-stu-id="cee3b-108">You need to create a backup vault or identify an existing backup vault *in the same region as your VM*.</span></span>
* <span data-ttu-id="cee3b-109">Establish network connectivity between the Azure public Internet addresses and the Azure storage endpoints.</span><span class="sxs-lookup"><span data-stu-id="cee3b-109">Establish network connectivity between the Azure public Internet addresses and the Azure storage endpoints.</span></span>
* <span data-ttu-id="cee3b-110">Install the VM agent on the VM.</span><span class="sxs-lookup"><span data-stu-id="cee3b-110">Install the VM agent on the VM.</span></span>

<span data-ttu-id="cee3b-111">If you know these conditions already exist in your environment then proceed to the [Back up your VMs article](backup-azure-vms.md).</span><span class="sxs-lookup"><span data-stu-id="cee3b-111">If you know these conditions already exist in your environment then proceed to the [Back up your VMs article](backup-azure-vms.md).</span></span> <span data-ttu-id="cee3b-112">Otherwise, read on, this article will lead you through the steps to prepare your environment to back up an Azure VM.</span><span class="sxs-lookup"><span data-stu-id="cee3b-112">Otherwise, read on, this article will lead you through the steps to prepare your environment to back up an Azure VM.</span></span>

##<a name="supported-operating-system-for-backup"></a><span data-ttu-id="cee3b-113">Supported operating system for backup</span><span class="sxs-lookup"><span data-stu-id="cee3b-113">Supported operating system for backup</span></span>
 * <span data-ttu-id="cee3b-114">**Linux**: Azure Backup supports [a list of distributions that are endorsed by Azure](../virtual-machines/linux/endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) except Core OS Linux.</span><span class="sxs-lookup"><span data-stu-id="cee3b-114">**Linux**: Azure Backup supports [a list of distributions that are endorsed by Azure](../virtual-machines/linux/endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) except Core OS Linux.</span></span> <span data-ttu-id="cee3b-115">_Other Bring-Your-Own-Linux distributions also might work as long as the VM agent is available on the virtual machine and support for Python exists. However, we do not endorse those distributions for backup._</span><span class="sxs-lookup"><span data-stu-id="cee3b-115">_Other Bring-Your-Own-Linux distributions also might work as long as the VM agent is available on the virtual machine and support for Python exists. However, we do not endorse those distributions for backup._</span></span>
 * <span data-ttu-id="cee3b-116">**Windows Server**:  Versions older than Windows Server 2008 R2 are not supported.</span><span class="sxs-lookup"><span data-stu-id="cee3b-116">**Windows Server**:  Versions older than Windows Server 2008 R2 are not supported.</span></span>


## <a name="limitations-when-backing-up-and-restoring-a-vm"></a><span data-ttu-id="cee3b-117">Limitations when backing up and restoring a VM</span><span class="sxs-lookup"><span data-stu-id="cee3b-117">Limitations when backing up and restoring a VM</span></span>
> [!NOTE]
> Azure has two deployment models for creating and working with resources: [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md). The following list provides the limitations when deploying in the classic model.
>
>

* <span data-ttu-id="cee3b-120">Backing up virtual machines with more than 16 data disks is not supported.</span><span class="sxs-lookup"><span data-stu-id="cee3b-120">Backing up virtual machines with more than 16 data disks is not supported.</span></span>
* <span data-ttu-id="cee3b-121">Backing up virtual machines with a reserved IP address and no defined endpoint is not supported.</span><span class="sxs-lookup"><span data-stu-id="cee3b-121">Backing up virtual machines with a reserved IP address and no defined endpoint is not supported.</span></span>
* <span data-ttu-id="cee3b-122">Backup data doesn't include network mounted drives attached to VM.</span><span class="sxs-lookup"><span data-stu-id="cee3b-122">Backup data doesn't include network mounted drives attached to VM.</span></span>
* <span data-ttu-id="cee3b-123">Replacing an existing virtual machine during restore is not supported.</span><span class="sxs-lookup"><span data-stu-id="cee3b-123">Replacing an existing virtual machine during restore is not supported.</span></span> <span data-ttu-id="cee3b-124">First delete the existing virtual machine and any associated disks, and then restore the data from backup.</span><span class="sxs-lookup"><span data-stu-id="cee3b-124">First delete the existing virtual machine and any associated disks, and then restore the data from backup.</span></span>
* <span data-ttu-id="cee3b-125">Cross-region backup and restore is not supported.</span><span class="sxs-lookup"><span data-stu-id="cee3b-125">Cross-region backup and restore is not supported.</span></span>
* <span data-ttu-id="cee3b-126">Backing up virtual machines by using the Azure Backup service is supported in all public regions of Azure (see the [checklist](https://azure.microsoft.com/regions/#services) of supported regions).</span><span class="sxs-lookup"><span data-stu-id="cee3b-126">Backing up virtual machines by using the Azure Backup service is supported in all public regions of Azure (see the [checklist](https://azure.microsoft.com/regions/#services) of supported regions).</span></span> <span data-ttu-id="cee3b-127">If the region that you are looking for is unsupported today, it will not appear in the dropdown list during vault creation.</span><span class="sxs-lookup"><span data-stu-id="cee3b-127">If the region that you are looking for is unsupported today, it will not appear in the dropdown list during vault creation.</span></span>
* <span data-ttu-id="cee3b-128">Backing up virtual machines by using the Azure Backup service is supported only for select operating system versions:</span><span class="sxs-lookup"><span data-stu-id="cee3b-128">Backing up virtual machines by using the Azure Backup service is supported only for select operating system versions:</span></span>
* <span data-ttu-id="cee3b-129">Restoring a domain controller (DC) VM that is part of a multi-DC configuration is supported only through PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cee3b-129">Restoring a domain controller (DC) VM that is part of a multi-DC configuration is supported only through PowerShell.</span></span> <span data-ttu-id="cee3b-130">Read more about [restoring a multi-DC domain controller](backup-azure-restore-vms.md#restoring-domain-controller-vms).</span><span class="sxs-lookup"><span data-stu-id="cee3b-130">Read more about [restoring a multi-DC domain controller](backup-azure-restore-vms.md#restoring-domain-controller-vms).</span></span>
* <span data-ttu-id="cee3b-131">Restoring virtual machines that have the following special network configurations is supported only through PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cee3b-131">Restoring virtual machines that have the following special network configurations is supported only through PowerShell.</span></span> <span data-ttu-id="cee3b-132">VMs that you create by using the restore workflow in the UI will not have these network configurations after the restore operation is complete.</span><span class="sxs-lookup"><span data-stu-id="cee3b-132">VMs that you create by using the restore workflow in the UI will not have these network configurations after the restore operation is complete.</span></span> <span data-ttu-id="cee3b-133">To learn more, see [Restoring VMs with special network configurations](backup-azure-restore-vms.md#restoring-vms-with-special-network-configurations).</span><span class="sxs-lookup"><span data-stu-id="cee3b-133">To learn more, see [Restoring VMs with special network configurations](backup-azure-restore-vms.md#restoring-vms-with-special-network-configurations).</span></span>
  * <span data-ttu-id="cee3b-134">Virtual machines under load balancer configuration (internal and external)</span><span class="sxs-lookup"><span data-stu-id="cee3b-134">Virtual machines under load balancer configuration (internal and external)</span></span>
  * <span data-ttu-id="cee3b-135">Virtual machines with multiple reserved IP addresses</span><span class="sxs-lookup"><span data-stu-id="cee3b-135">Virtual machines with multiple reserved IP addresses</span></span>
  * <span data-ttu-id="cee3b-136">Virtual machines with multiple network adapters</span><span class="sxs-lookup"><span data-stu-id="cee3b-136">Virtual machines with multiple network adapters</span></span>

## <a name="create-a-backup-vault-for-a-vm"></a><span data-ttu-id="cee3b-137">Create a backup vault for a VM</span><span class="sxs-lookup"><span data-stu-id="cee3b-137">Create a backup vault for a VM</span></span>
<span data-ttu-id="cee3b-138">A backup vault is an entity that stores all the backups and recovery points that have been created over time.</span><span class="sxs-lookup"><span data-stu-id="cee3b-138">A backup vault is an entity that stores all the backups and recovery points that have been created over time.</span></span> <span data-ttu-id="cee3b-139">The backup vault also contains the backup policies that will be applied to the virtual machines being backed up.</span><span class="sxs-lookup"><span data-stu-id="cee3b-139">The backup vault also contains the backup policies that will be applied to the virtual machines being backed up.</span></span>

> [!IMPORTANT]
> Starting March 2017, you can no longer use the classic portal to create Backup vaults. Existing Backup vaults are still supported, and it is possible to [use Azure PowerShell to create Backup vaults](./backup-client-automation-classic.md#create-a-backup-vault). However, Microsoft recommends you create Recovery Services vaults for all deployments because future enhancements apply to Recovery Services vaults, only.


<span data-ttu-id="cee3b-143">This image shows the relationships between the various Azure Backup entities: ![Azure Backup entities and relationships](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms-prepare/vault-policy-vm.png)</span><span class="sxs-lookup"><span data-stu-id="cee3b-143">This image shows the relationships between the various Azure Backup entities: ![Azure Backup entities and relationships](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms-prepare/vault-policy-vm.png)</span></span>



## <a name="network-connectivity"></a><span data-ttu-id="cee3b-144">Network connectivity</span><span class="sxs-lookup"><span data-stu-id="cee3b-144">Network connectivity</span></span>
<span data-ttu-id="cee3b-145">In order to manage the VM snapshots, the backup extension needs connectivity to the Azure public IP addresses.</span><span class="sxs-lookup"><span data-stu-id="cee3b-145">In order to manage the VM snapshots, the backup extension needs connectivity to the Azure public IP addresses.</span></span> <span data-ttu-id="cee3b-146">Without the right Internet connectivity, the virtual machine's HTTP requests time out and the backup operation fails.</span><span class="sxs-lookup"><span data-stu-id="cee3b-146">Without the right Internet connectivity, the virtual machine's HTTP requests time out and the backup operation fails.</span></span> <span data-ttu-id="cee3b-147">If your deployment has access restrictions in place (through a network security group (NSG), for example), then choose one of these options for providing a clear path for backup traffic:</span><span class="sxs-lookup"><span data-stu-id="cee3b-147">If your deployment has access restrictions in place (through a network security group (NSG), for example), then choose one of these options for providing a clear path for backup traffic:</span></span>

* <span data-ttu-id="cee3b-148">[Whitelist the Azure datacenter IP ranges](http://www.microsoft.com/en-us/download/details.aspx?id=41653) - see the article for instructions on how to whitelist the IP addresses.</span><span class="sxs-lookup"><span data-stu-id="cee3b-148">[Whitelist the Azure datacenter IP ranges](http://www.microsoft.com/en-us/download/details.aspx?id=41653) - see the article for instructions on how to whitelist the IP addresses.</span></span>
* <span data-ttu-id="cee3b-149">Deploy an HTTP proxy server for routing traffic.</span><span class="sxs-lookup"><span data-stu-id="cee3b-149">Deploy an HTTP proxy server for routing traffic.</span></span>

<span data-ttu-id="cee3b-150">When deciding which option to use, the trade-offs are between manageability, granular control, and cost.</span><span class="sxs-lookup"><span data-stu-id="cee3b-150">When deciding which option to use, the trade-offs are between manageability, granular control, and cost.</span></span>

| <span data-ttu-id="cee3b-151">Option</span><span class="sxs-lookup"><span data-stu-id="cee3b-151">Option</span></span> | <span data-ttu-id="cee3b-152">Advantages</span><span class="sxs-lookup"><span data-stu-id="cee3b-152">Advantages</span></span> | <span data-ttu-id="cee3b-153">Disadvantages</span><span class="sxs-lookup"><span data-stu-id="cee3b-153">Disadvantages</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cee3b-154">Whitelist IP ranges</span><span class="sxs-lookup"><span data-stu-id="cee3b-154">Whitelist IP ranges</span></span> |<span data-ttu-id="cee3b-155">No additional costs.</span><span class="sxs-lookup"><span data-stu-id="cee3b-155">No additional costs.</span></span><br><br><span data-ttu-id="cee3b-156">For opening access in an NSG, use the <i>Set-AzureNetworkSecurityRule</i> cmdlet.</span><span class="sxs-lookup"><span data-stu-id="cee3b-156">For opening access in an NSG, use the <i>Set-AzureNetworkSecurityRule</i> cmdlet.</span></span> |<span data-ttu-id="cee3b-157">Complex to manage as the impacted IP ranges change over time.</span><span class="sxs-lookup"><span data-stu-id="cee3b-157">Complex to manage as the impacted IP ranges change over time.</span></span><br><br><span data-ttu-id="cee3b-158">Provides access to the whole of Azure, and not just Storage.</span><span class="sxs-lookup"><span data-stu-id="cee3b-158">Provides access to the whole of Azure, and not just Storage.</span></span> |
| <span data-ttu-id="cee3b-159">HTTP proxy</span><span class="sxs-lookup"><span data-stu-id="cee3b-159">HTTP proxy</span></span> |<span data-ttu-id="cee3b-160">Granular control in the proxy over the storage URLs allowed.</span><span class="sxs-lookup"><span data-stu-id="cee3b-160">Granular control in the proxy over the storage URLs allowed.</span></span><br><span data-ttu-id="cee3b-161">Single point of Internet access to VMs.</span><span class="sxs-lookup"><span data-stu-id="cee3b-161">Single point of Internet access to VMs.</span></span><br><span data-ttu-id="cee3b-162">Not subject to Azure IP address changes.</span><span class="sxs-lookup"><span data-stu-id="cee3b-162">Not subject to Azure IP address changes.</span></span> |<span data-ttu-id="cee3b-163">Additional costs for running a VM with the proxy software.</span><span class="sxs-lookup"><span data-stu-id="cee3b-163">Additional costs for running a VM with the proxy software.</span></span> |

### <a name="whitelist-the-azure-datacenter-ip-ranges"></a><span data-ttu-id="cee3b-164">Whitelist the Azure datacenter IP ranges</span><span class="sxs-lookup"><span data-stu-id="cee3b-164">Whitelist the Azure datacenter IP ranges</span></span>
<span data-ttu-id="cee3b-165">To whitelist the Azure datacenter IP ranges, please see the [Azure website](http://www.microsoft.com/en-us/download/details.aspx?id=41653) for details on the IP ranges, and instructions.</span><span class="sxs-lookup"><span data-stu-id="cee3b-165">To whitelist the Azure datacenter IP ranges, please see the [Azure website](http://www.microsoft.com/en-us/download/details.aspx?id=41653) for details on the IP ranges, and instructions.</span></span>

### <a name="using-an-http-proxy-for-vm-backups"></a><span data-ttu-id="cee3b-166">Using an HTTP proxy for VM backups</span><span class="sxs-lookup"><span data-stu-id="cee3b-166">Using an HTTP proxy for VM backups</span></span>
<span data-ttu-id="cee3b-167">When backing up a VM, the backup extension on the VM sends the snapshot management commands to Azure Storage using an HTTPS API.</span><span class="sxs-lookup"><span data-stu-id="cee3b-167">When backing up a VM, the backup extension on the VM sends the snapshot management commands to Azure Storage using an HTTPS API.</span></span> <span data-ttu-id="cee3b-168">Route the backup extension traffic through the HTTP proxy since it is the only component configured for access to the public Internet.</span><span class="sxs-lookup"><span data-stu-id="cee3b-168">Route the backup extension traffic through the HTTP proxy since it is the only component configured for access to the public Internet.</span></span>

> [!NOTE]
> There is no recommendation for the proxy software that should be used. Ensure that you pick a proxy that is compatible with the configuration steps below.
>
>

<span data-ttu-id="cee3b-171">The example image below shows the three configuration steps necessary to use an HTTP proxy:</span><span class="sxs-lookup"><span data-stu-id="cee3b-171">The example image below shows the three configuration steps necessary to use an HTTP proxy:</span></span>

* <span data-ttu-id="cee3b-172">App VM routes all HTTP traffic bound for the public Internet through Proxy VM.</span><span class="sxs-lookup"><span data-stu-id="cee3b-172">App VM routes all HTTP traffic bound for the public Internet through Proxy VM.</span></span>
* <span data-ttu-id="cee3b-173">Proxy VM allows incoming traffic from VMs in the virtual network.</span><span class="sxs-lookup"><span data-stu-id="cee3b-173">Proxy VM allows incoming traffic from VMs in the virtual network.</span></span>
* <span data-ttu-id="cee3b-174">The Network Security Group (NSG) named NSF-lockdown needs a security rule allowing outbound Internet traffic from Proxy VM.</span><span class="sxs-lookup"><span data-stu-id="cee3b-174">The Network Security Group (NSG) named NSF-lockdown needs a security rule allowing outbound Internet traffic from Proxy VM.</span></span>

![NSG with HTTP proxy deployment diagram](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms-prepare/nsg-with-http-proxy.png)

<span data-ttu-id="cee3b-176">To use an HTTP proxy to communicating to the public Internet, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="cee3b-176">To use an HTTP proxy to communicating to the public Internet, follow these steps:</span></span>

#### <a name="step-1-configure-outgoing-network-connections"></a><span data-ttu-id="cee3b-177">Step 1.</span><span class="sxs-lookup"><span data-stu-id="cee3b-177">Step 1.</span></span> <span data-ttu-id="cee3b-178">Configure outgoing network connections</span><span class="sxs-lookup"><span data-stu-id="cee3b-178">Configure outgoing network connections</span></span>
###### <a name="for-windows-machines"></a><span data-ttu-id="cee3b-179">For Windows machines</span><span class="sxs-lookup"><span data-stu-id="cee3b-179">For Windows machines</span></span>
<span data-ttu-id="cee3b-180">This will setup proxy server configuration for Local System Account.</span><span class="sxs-lookup"><span data-stu-id="cee3b-180">This will setup proxy server configuration for Local System Account.</span></span>

1. <span data-ttu-id="cee3b-181">Download [PsExec](https://technet.microsoft.com/sysinternals/bb897553)</span><span class="sxs-lookup"><span data-stu-id="cee3b-181">Download [PsExec](https://technet.microsoft.com/sysinternals/bb897553)</span></span>
2. <span data-ttu-id="cee3b-182">Run following command from elevated prompt,</span><span class="sxs-lookup"><span data-stu-id="cee3b-182">Run following command from elevated prompt,</span></span>

     ```
     psexec -i -s "c:\Program Files\Internet Explorer\iexplore.exe"
     ```
     <span data-ttu-id="cee3b-183">It will open internet explorer window.</span><span class="sxs-lookup"><span data-stu-id="cee3b-183">It will open internet explorer window.</span></span>
3. <span data-ttu-id="cee3b-184">Go to Tools -> Internet Options -> Connections -> LAN settings.</span><span class="sxs-lookup"><span data-stu-id="cee3b-184">Go to Tools -> Internet Options -> Connections -> LAN settings.</span></span>
4. <span data-ttu-id="cee3b-185">Verify proxy settings for System account.</span><span class="sxs-lookup"><span data-stu-id="cee3b-185">Verify proxy settings for System account.</span></span> <span data-ttu-id="cee3b-186">Set Proxy IP and port.</span><span class="sxs-lookup"><span data-stu-id="cee3b-186">Set Proxy IP and port.</span></span>
5. <span data-ttu-id="cee3b-187">Close Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="cee3b-187">Close Internet Explorer.</span></span>

<span data-ttu-id="cee3b-188">This will set up a machine-wide proxy configuration, and will be used for any outgoing HTTP/HTTPS traffic.</span><span class="sxs-lookup"><span data-stu-id="cee3b-188">This will set up a machine-wide proxy configuration, and will be used for any outgoing HTTP/HTTPS traffic.</span></span>

<span data-ttu-id="cee3b-189">If you have setup a proxy server on a current user account(not a Local System Account), use the following script to apply them to SYSTEMACCOUNT:</span><span class="sxs-lookup"><span data-stu-id="cee3b-189">If you have setup a proxy server on a current user account(not a Local System Account), use the following script to apply them to SYSTEMACCOUNT:</span></span>

```
   $obj = Get-ItemProperty -Path Registry::”HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections"
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections" -Name DefaultConnectionSettings -Value $obj.DefaultConnectionSettings
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections" -Name SavedLegacySettings -Value $obj.SavedLegacySettings
   $obj = Get-ItemProperty -Path Registry::”HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Internet Settings"
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings" -Name ProxyEnable -Value $obj.ProxyEnable
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings" -Name Proxyserver -Value $obj.Proxyserver
```

> [!NOTE]
> If you observe "(407)Proxy Authentication Required" in proxy server log, check your authentication is setup correctly.
>
>

###### <a name="for-linux-machines"></a><span data-ttu-id="cee3b-191">For Linux machines</span><span class="sxs-lookup"><span data-stu-id="cee3b-191">For Linux machines</span></span>
<span data-ttu-id="cee3b-192">Add the following line to the ```/etc/environment``` file:</span><span class="sxs-lookup"><span data-stu-id="cee3b-192">Add the following line to the ```/etc/environment``` file:</span></span>

```
http_proxy=http://<proxy IP>:<proxy port>
```

<span data-ttu-id="cee3b-193">Add the following lines to the ```/etc/waagent.conf``` file:</span><span class="sxs-lookup"><span data-stu-id="cee3b-193">Add the following lines to the ```/etc/waagent.conf``` file:</span></span>

```
HttpProxy.Host=<proxy IP>
HttpProxy.Port=<proxy port>
```

#### <a name="step-2-allow-incoming-connections-on-the-proxy-server"></a><span data-ttu-id="cee3b-194">Step 2.</span><span class="sxs-lookup"><span data-stu-id="cee3b-194">Step 2.</span></span> <span data-ttu-id="cee3b-195">Allow incoming connections on the proxy server:</span><span class="sxs-lookup"><span data-stu-id="cee3b-195">Allow incoming connections on the proxy server:</span></span>
1. <span data-ttu-id="cee3b-196">On the proxy server, open Windows Firewall.</span><span class="sxs-lookup"><span data-stu-id="cee3b-196">On the proxy server, open Windows Firewall.</span></span> <span data-ttu-id="cee3b-197">The easiest way to access the firewall is to search for Windows Firewall with Advanced Security.</span><span class="sxs-lookup"><span data-stu-id="cee3b-197">The easiest way to access the firewall is to search for Windows Firewall with Advanced Security.</span></span>

    ![Open the Firewall](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms-prepare/firewall-01.png)
2. <span data-ttu-id="cee3b-199">In the Windows Firewall dialog, right-click  **Inbound Rules** and click **New Rule...**.</span><span class="sxs-lookup"><span data-stu-id="cee3b-199">In the Windows Firewall dialog, right-click  **Inbound Rules** and click **New Rule...**.</span></span>

    ![Create a new rule](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms-prepare/firewall-02.png)
3. <span data-ttu-id="cee3b-201">In the **New Inbound Rule Wizard**, choose the **Custom** option for the **Rule Type** and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="cee3b-201">In the **New Inbound Rule Wizard**, choose the **Custom** option for the **Rule Type** and click **Next**.</span></span>
4. <span data-ttu-id="cee3b-202">On the page to select the **Program**, choose **All Programs** and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="cee3b-202">On the page to select the **Program**, choose **All Programs** and click **Next**.</span></span>
5. <span data-ttu-id="cee3b-203">On the **Protocol and Ports** page, enter the following information and click **Next**:</span><span class="sxs-lookup"><span data-stu-id="cee3b-203">On the **Protocol and Ports** page, enter the following information and click **Next**:</span></span>

    ![Create a new rule](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms-prepare/firewall-03.png)

   * <span data-ttu-id="cee3b-205">for *Protocol type* choose *TCP*</span><span class="sxs-lookup"><span data-stu-id="cee3b-205">for *Protocol type* choose *TCP*</span></span>
   * <span data-ttu-id="cee3b-206">for *Local port* choose *Specific Ports*, in the field below specify the ```<Proxy Port>``` that has been configured.</span><span class="sxs-lookup"><span data-stu-id="cee3b-206">for *Local port* choose *Specific Ports*, in the field below specify the ```<Proxy Port>``` that has been configured.</span></span>
   * <span data-ttu-id="cee3b-207">for *Remote port* select *All Ports*</span><span class="sxs-lookup"><span data-stu-id="cee3b-207">for *Remote port* select *All Ports*</span></span>

     <span data-ttu-id="cee3b-208">For the rest of the wizard, click all the way to the end and give this rule a name.</span><span class="sxs-lookup"><span data-stu-id="cee3b-208">For the rest of the wizard, click all the way to the end and give this rule a name.</span></span>

#### <a name="step-3-add-an-exception-rule-to-the-nsg"></a><span data-ttu-id="cee3b-209">Step 3.</span><span class="sxs-lookup"><span data-stu-id="cee3b-209">Step 3.</span></span> <span data-ttu-id="cee3b-210">Add an exception rule to the NSG:</span><span class="sxs-lookup"><span data-stu-id="cee3b-210">Add an exception rule to the NSG:</span></span>
<span data-ttu-id="cee3b-211">In an Azure PowerShell command prompt, enter the following command:</span><span class="sxs-lookup"><span data-stu-id="cee3b-211">In an Azure PowerShell command prompt, enter the following command:</span></span>

<span data-ttu-id="cee3b-212">The following command adds an exception to the NSG.</span><span class="sxs-lookup"><span data-stu-id="cee3b-212">The following command adds an exception to the NSG.</span></span> <span data-ttu-id="cee3b-213">This exception allows TCP traffic from any port on 10.0.0.5 to any Internet address on port 80 (HTTP) or 443 (HTTPS).</span><span class="sxs-lookup"><span data-stu-id="cee3b-213">This exception allows TCP traffic from any port on 10.0.0.5 to any Internet address on port 80 (HTTP) or 443 (HTTPS).</span></span> <span data-ttu-id="cee3b-214">If you require a specific port in the public Internet, be sure to add that port to the ```-DestinationPortRange``` as well.</span><span class="sxs-lookup"><span data-stu-id="cee3b-214">If you require a specific port in the public Internet, be sure to add that port to the ```-DestinationPortRange``` as well.</span></span>

```
Get-AzureNetworkSecurityGroup -Name "NSG-lockdown" |
Set-AzureNetworkSecurityRule -Name "allow-proxy " -Action Allow -Protocol TCP -Type Outbound -Priority 200 -SourceAddressPrefix "10.0.0.5/32" -SourcePortRange "*" -DestinationAddressPrefix Internet -DestinationPortRange "80-443"
```

<span data-ttu-id="cee3b-215">*Ensure that you replace the names in the example with the details appropriate to your deployment.*</span><span class="sxs-lookup"><span data-stu-id="cee3b-215">*Ensure that you replace the names in the example with the details appropriate to your deployment.*</span></span>

## <a name="vm-agent"></a><span data-ttu-id="cee3b-216">VM agent</span><span class="sxs-lookup"><span data-stu-id="cee3b-216">VM agent</span></span>
<span data-ttu-id="cee3b-217">Before you can back up the Azure virtual machine, you should ensure that the Azure VM agent is correctly installed on the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="cee3b-217">Before you can back up the Azure virtual machine, you should ensure that the Azure VM agent is correctly installed on the virtual machine.</span></span> <span data-ttu-id="cee3b-218">Since the VM agent is an optional component at the time that the virtual machine is created, ensure that the check box for the VM agent is selected before the virtual machine is provisioned.</span><span class="sxs-lookup"><span data-stu-id="cee3b-218">Since the VM agent is an optional component at the time that the virtual machine is created, ensure that the check box for the VM agent is selected before the virtual machine is provisioned.</span></span>

### <a name="manual-installation-and-update"></a><span data-ttu-id="cee3b-219">Manual installation and update</span><span class="sxs-lookup"><span data-stu-id="cee3b-219">Manual installation and update</span></span>
<span data-ttu-id="cee3b-220">The VM agent is already present in VMs that are created from the Azure gallery.</span><span class="sxs-lookup"><span data-stu-id="cee3b-220">The VM agent is already present in VMs that are created from the Azure gallery.</span></span> <span data-ttu-id="cee3b-221">However, virtual machines that are migrated from on-premises datacenters would not have the VM agent installed.</span><span class="sxs-lookup"><span data-stu-id="cee3b-221">However, virtual machines that are migrated from on-premises datacenters would not have the VM agent installed.</span></span> <span data-ttu-id="cee3b-222">For such VMs, the VM agent needs to be installed explicitly.</span><span class="sxs-lookup"><span data-stu-id="cee3b-222">For such VMs, the VM agent needs to be installed explicitly.</span></span> <span data-ttu-id="cee3b-223">Read more about [installing the VM agent on an existing VM](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx).</span><span class="sxs-lookup"><span data-stu-id="cee3b-223">Read more about [installing the VM agent on an existing VM](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx).</span></span>

| <span data-ttu-id="cee3b-224">**Operation**</span><span class="sxs-lookup"><span data-stu-id="cee3b-224">**Operation**</span></span> | <span data-ttu-id="cee3b-225">**Windows**</span><span class="sxs-lookup"><span data-stu-id="cee3b-225">**Windows**</span></span> | <span data-ttu-id="cee3b-226">**Linux**</span><span class="sxs-lookup"><span data-stu-id="cee3b-226">**Linux**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cee3b-227">Installing the VM agent</span><span class="sxs-lookup"><span data-stu-id="cee3b-227">Installing the VM agent</span></span> |<li><span data-ttu-id="cee3b-228">Download and install the [agent MSI](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="cee3b-228">Download and install the [agent MSI](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409).</span></span> <span data-ttu-id="cee3b-229">You will need Administrator privileges to complete the installation.</span><span class="sxs-lookup"><span data-stu-id="cee3b-229">You will need Administrator privileges to complete the installation.</span></span> <li><span data-ttu-id="cee3b-230">[Update the VM property](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) to indicate that the agent is installed.</span><span class="sxs-lookup"><span data-stu-id="cee3b-230">[Update the VM property](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) to indicate that the agent is installed.</span></span> |<li> <span data-ttu-id="cee3b-231">Install the latest [Linux agent](https://github.com/Azure/WALinuxAgent) from GitHub.</span><span class="sxs-lookup"><span data-stu-id="cee3b-231">Install the latest [Linux agent](https://github.com/Azure/WALinuxAgent) from GitHub.</span></span> <span data-ttu-id="cee3b-232">You will need Administrator privileges to complete the installation.</span><span class="sxs-lookup"><span data-stu-id="cee3b-232">You will need Administrator privileges to complete the installation.</span></span> <li> <span data-ttu-id="cee3b-233">[Update the VM property](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) to indicate that the agent is installed.</span><span class="sxs-lookup"><span data-stu-id="cee3b-233">[Update the VM property](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) to indicate that the agent is installed.</span></span> |
| <span data-ttu-id="cee3b-234">Updating the VM agent</span><span class="sxs-lookup"><span data-stu-id="cee3b-234">Updating the VM agent</span></span> |<span data-ttu-id="cee3b-235">Updating the VM agent is as simple as reinstalling the [VM agent binaries](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="cee3b-235">Updating the VM agent is as simple as reinstalling the [VM agent binaries](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409).</span></span> <br><br><span data-ttu-id="cee3b-236">Ensure that no backup operation is running while the VM agent is being updated.</span><span class="sxs-lookup"><span data-stu-id="cee3b-236">Ensure that no backup operation is running while the VM agent is being updated.</span></span> |<span data-ttu-id="cee3b-237">Follow the instructions on [updating the Linux VM agent ](../virtual-machines/linux/update-agent.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cee3b-237">Follow the instructions on [updating the Linux VM agent ](../virtual-machines/linux/update-agent.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <br><br><span data-ttu-id="cee3b-238">Ensure that no backup operation is running while the VM agent is being updated.</span><span class="sxs-lookup"><span data-stu-id="cee3b-238">Ensure that no backup operation is running while the VM agent is being updated.</span></span> |
| <span data-ttu-id="cee3b-239">Validating the VM agent installation</span><span class="sxs-lookup"><span data-stu-id="cee3b-239">Validating the VM agent installation</span></span> |<li><span data-ttu-id="cee3b-240">Navigate to the *C:\WindowsAzure\Packages* folder in the Azure VM.</span><span class="sxs-lookup"><span data-stu-id="cee3b-240">Navigate to the *C:\WindowsAzure\Packages* folder in the Azure VM.</span></span> <li><span data-ttu-id="cee3b-241">You should find the WaAppAgent.exe file present.</span><span class="sxs-lookup"><span data-stu-id="cee3b-241">You should find the WaAppAgent.exe file present.</span></span><li> <span data-ttu-id="cee3b-242">Right-click the file, go to **Properties**, and then select the **Details** tab. The Product Version field should be 2.6.1198.718 or higher.</span><span class="sxs-lookup"><span data-stu-id="cee3b-242">Right-click the file, go to **Properties**, and then select the **Details** tab. The Product Version field should be 2.6.1198.718 or higher.</span></span> |<span data-ttu-id="cee3b-243">N/A</span><span class="sxs-lookup"><span data-stu-id="cee3b-243">N/A</span></span> |

<span data-ttu-id="cee3b-244">Learn about the [VM agent](https://go.microsoft.com/fwLink/?LinkID=390493&clcid=0x409) and [how to install it](https://azure.microsoft.com/blog/2014/04/15/vm-agent-and-extensions-part-2/).</span><span class="sxs-lookup"><span data-stu-id="cee3b-244">Learn about the [VM agent](https://go.microsoft.com/fwLink/?LinkID=390493&clcid=0x409) and [how to install it](https://azure.microsoft.com/blog/2014/04/15/vm-agent-and-extensions-part-2/).</span></span>

### <a name="backup-extension"></a><span data-ttu-id="cee3b-245">Backup extension</span><span class="sxs-lookup"><span data-stu-id="cee3b-245">Backup extension</span></span>
<span data-ttu-id="cee3b-246">To back up the virtual machine, the Azure Backup service installs an extension to the VM agent.</span><span class="sxs-lookup"><span data-stu-id="cee3b-246">To back up the virtual machine, the Azure Backup service installs an extension to the VM agent.</span></span> <span data-ttu-id="cee3b-247">The Azure Backup service seamlessly upgrades and patches the backup extension without additional user intervention.</span><span class="sxs-lookup"><span data-stu-id="cee3b-247">The Azure Backup service seamlessly upgrades and patches the backup extension without additional user intervention.</span></span>

<span data-ttu-id="cee3b-248">The backup extension is installed if the VM is running.</span><span class="sxs-lookup"><span data-stu-id="cee3b-248">The backup extension is installed if the VM is running.</span></span> <span data-ttu-id="cee3b-249">A running VM also provides the greatest chance of getting an application-consistent recovery point.</span><span class="sxs-lookup"><span data-stu-id="cee3b-249">A running VM also provides the greatest chance of getting an application-consistent recovery point.</span></span> <span data-ttu-id="cee3b-250">However, the Azure Backup service will continue to back up the VM--even if it is turned off, and the extension could not be installed (aka Offline VM).</span><span class="sxs-lookup"><span data-stu-id="cee3b-250">However, the Azure Backup service will continue to back up the VM--even if it is turned off, and the extension could not be installed (aka Offline VM).</span></span> <span data-ttu-id="cee3b-251">In this case, the recovery point will be *crash consistent* as discussed above.</span><span class="sxs-lookup"><span data-stu-id="cee3b-251">In this case, the recovery point will be *crash consistent* as discussed above.</span></span>

## <a name="questions"></a><span data-ttu-id="cee3b-252">Questions?</span><span class="sxs-lookup"><span data-stu-id="cee3b-252">Questions?</span></span>
<span data-ttu-id="cee3b-253">If you have questions, or if there is any feature that you would like to see included, [send us feedback](http://aka.ms/azurebackup_feedback).</span><span class="sxs-lookup"><span data-stu-id="cee3b-253">If you have questions, or if there is any feature that you would like to see included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>

## <a name="next-steps"></a><span data-ttu-id="cee3b-254">Next steps</span><span class="sxs-lookup"><span data-stu-id="cee3b-254">Next steps</span></span>
<span data-ttu-id="cee3b-255">Now that you have prepared your environment for backing up your VM, your next logical step is to create a backup.</span><span class="sxs-lookup"><span data-stu-id="cee3b-255">Now that you have prepared your environment for backing up your VM, your next logical step is to create a backup.</span></span> <span data-ttu-id="cee3b-256">The planning article provides more detailed information about backing up VMs.</span><span class="sxs-lookup"><span data-stu-id="cee3b-256">The planning article provides more detailed information about backing up VMs.</span></span>

* [<span data-ttu-id="cee3b-257">Back up virtual machines</span><span class="sxs-lookup"><span data-stu-id="cee3b-257">Back up virtual machines</span></span>](backup-azure-vms.md)
* [<span data-ttu-id="cee3b-258">Plan your VM backup infrastructure</span><span class="sxs-lookup"><span data-stu-id="cee3b-258">Plan your VM backup infrastructure</span></span>](backup-azure-vms-introduction.md)
* [<span data-ttu-id="cee3b-259">Manage virtual machine backups</span><span class="sxs-lookup"><span data-stu-id="cee3b-259">Manage virtual machine backups</span></span>](backup-azure-manage-vms.md)





