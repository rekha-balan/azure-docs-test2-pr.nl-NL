---
title: 'Troubleshoot Azure Backup failure: Snapshot VM sub task timed out | Microsoft Docs'
description: 'Symptoms, causes, and resolutions of Azure Backup failures related to error: Could not communicate with the VM agent for snapshot status - Snapshot VM sub task timed out'
services: backup
documentationcenter: ''
author: genlin
manager: cshepard
editor: ''
ms.assetid: 4b02ffa4-c48e-45f6-8363-73d536be4639
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/07/2017
ms.author: genli;markgal;
ms.openlocfilehash: d7924d8aade1ea582faa0f319f8c1d16d5461fbc
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552853"
---
# <a name="troubleshoot-azure-backup-failure-snapshot-vm-sub-task-timed-out"></a><span data-ttu-id="f55e7-103">Troubleshoot Azure Backup failure: Snapshot VM sub task timed out</span><span class="sxs-lookup"><span data-stu-id="f55e7-103">Troubleshoot Azure Backup failure: Snapshot VM sub task timed out</span></span>
## <a name="summary"></a><span data-ttu-id="f55e7-104">Summary</span><span class="sxs-lookup"><span data-stu-id="f55e7-104">Summary</span></span>
<span data-ttu-id="f55e7-105">After you register and schedule a VM for the Azure Backup service, Backup initiates the job by communicating with the VM backup extension to take a point-in-time snapshot.</span><span class="sxs-lookup"><span data-stu-id="f55e7-105">After you register and schedule a VM for the Azure Backup service, Backup initiates the job by communicating with the VM backup extension to take a point-in-time snapshot.</span></span> <span data-ttu-id="f55e7-106">Any of four conditions might prevent the snapshot from being triggered, which in turn can lead to Backup failure.</span><span class="sxs-lookup"><span data-stu-id="f55e7-106">Any of four conditions might prevent the snapshot from being triggered, which in turn can lead to Backup failure.</span></span> <span data-ttu-id="f55e7-107">This article provides troubleshooting steps to help you resolve Backup failures related to snapshot time-out errors.</span><span class="sxs-lookup"><span data-stu-id="f55e7-107">This article provides troubleshooting steps to help you resolve Backup failures related to snapshot time-out errors.</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="symptom"></a><span data-ttu-id="f55e7-108">Symptom</span><span class="sxs-lookup"><span data-stu-id="f55e7-108">Symptom</span></span>
<span data-ttu-id="f55e7-109">Azure Backup for an infrastructure as a service (IaaS) VM fails, returning the following error message in the job error details in the [Azure portal](https://portal.azure.com/): "Could not communicate with the VM agent for snapshot status - Snapshot VM sub task timed out."</span><span class="sxs-lookup"><span data-stu-id="f55e7-109">Azure Backup for an infrastructure as a service (IaaS) VM fails, returning the following error message in the job error details in the [Azure portal](https://portal.azure.com/): "Could not communicate with the VM agent for snapshot status - Snapshot VM sub task timed out."</span></span>

## <a name="cause-1-the-vm-has-no-internet-access"></a><span data-ttu-id="f55e7-110">Cause 1: The VM has no Internet access</span><span class="sxs-lookup"><span data-stu-id="f55e7-110">Cause 1: The VM has no Internet access</span></span>
<span data-ttu-id="f55e7-111">Per the deployment requirement, the VM has no Internet access, or it has restrictions in place that prevent access to the Azure infrastructure.</span><span class="sxs-lookup"><span data-stu-id="f55e7-111">Per the deployment requirement, the VM has no Internet access, or it has restrictions in place that prevent access to the Azure infrastructure.</span></span>

<span data-ttu-id="f55e7-112">To function correctly, the backup extension requires connectivity to the Azure public IP addresses.</span><span class="sxs-lookup"><span data-stu-id="f55e7-112">To function correctly, the backup extension requires connectivity to the Azure public IP addresses.</span></span> <span data-ttu-id="f55e7-113">The extension sends commands to an Azure Storage endpoint (HTTP URL) to manage the snapshots of the VM.</span><span class="sxs-lookup"><span data-stu-id="f55e7-113">The extension sends commands to an Azure Storage endpoint (HTTP URL) to manage the snapshots of the VM.</span></span> <span data-ttu-id="f55e7-114">If the extension has no access to the public Internet, Backup eventually fails.</span><span class="sxs-lookup"><span data-stu-id="f55e7-114">If the extension has no access to the public Internet, Backup eventually fails.</span></span>

### <a name="solution"></a><span data-ttu-id="f55e7-115">Solution</span><span class="sxs-lookup"><span data-stu-id="f55e7-115">Solution</span></span>
<span data-ttu-id="f55e7-116">To resolve the issue, try one of the methods listed here.</span><span class="sxs-lookup"><span data-stu-id="f55e7-116">To resolve the issue, try one of the methods listed here.</span></span>
#### <a name="allow-access-to-the-azure-datacenter-ip-ranges"></a><span data-ttu-id="f55e7-117">Allow access to the Azure datacenter IP ranges</span><span class="sxs-lookup"><span data-stu-id="f55e7-117">Allow access to the Azure datacenter IP ranges</span></span>

1. <span data-ttu-id="f55e7-118">Obtain the [list of Azure datacenter IPs](https://www.microsoft.com/download/details.aspx?id=41653) to allow access to.</span><span class="sxs-lookup"><span data-stu-id="f55e7-118">Obtain the [list of Azure datacenter IPs](https://www.microsoft.com/download/details.aspx?id=41653) to allow access to.</span></span>
2. <span data-ttu-id="f55e7-119">Unblock the IPs by running the **New-NetRoute** cmdlet in the Azure VM in an elevated PowerShell window.</span><span class="sxs-lookup"><span data-stu-id="f55e7-119">Unblock the IPs by running the **New-NetRoute** cmdlet in the Azure VM in an elevated PowerShell window.</span></span> <span data-ttu-id="f55e7-120">Run the cmdlet as an administrator.</span><span class="sxs-lookup"><span data-stu-id="f55e7-120">Run the cmdlet as an administrator.</span></span>
3. <span data-ttu-id="f55e7-121">To allow access to the IPs, add rules to the network security group, if you have one.</span><span class="sxs-lookup"><span data-stu-id="f55e7-121">To allow access to the IPs, add rules to the network security group, if you have one.</span></span>

#### <a name="create-a-path-for-http-traffic-to-flow"></a><span data-ttu-id="f55e7-122">Create a path for HTTP traffic to flow</span><span class="sxs-lookup"><span data-stu-id="f55e7-122">Create a path for HTTP traffic to flow</span></span>

1. <span data-ttu-id="f55e7-123">If you have network restrictions in place (for example, a network security group), deploy an HTTP proxy server to route the traffic.</span><span class="sxs-lookup"><span data-stu-id="f55e7-123">If you have network restrictions in place (for example, a network security group), deploy an HTTP proxy server to route the traffic.</span></span>
2. <span data-ttu-id="f55e7-124">To allow access to the Internet from the HTTP proxy server, add rules to the network security group, if you have one.</span><span class="sxs-lookup"><span data-stu-id="f55e7-124">To allow access to the Internet from the HTTP proxy server, add rules to the network security group, if you have one.</span></span>

<span data-ttu-id="f55e7-125">To learn how to set up an HTTP proxy for VM backups, see [Prepare your environment to back up Azure virtual machines](backup-azure-vms-prepare.md#using-an-http-proxy-for-vm-backups).</span><span class="sxs-lookup"><span data-stu-id="f55e7-125">To learn how to set up an HTTP proxy for VM backups, see [Prepare your environment to back up Azure virtual machines](backup-azure-vms-prepare.md#using-an-http-proxy-for-vm-backups).</span></span>

## <a name="cause-2-the-agent-installed-in-the-vm-is-out-of-date-for-linux-vms"></a><span data-ttu-id="f55e7-126">Cause 2: The agent installed in the VM is out of date (for Linux VMs)</span><span class="sxs-lookup"><span data-stu-id="f55e7-126">Cause 2: The agent installed in the VM is out of date (for Linux VMs)</span></span>

### <a name="solution"></a><span data-ttu-id="f55e7-127">Solution</span><span class="sxs-lookup"><span data-stu-id="f55e7-127">Solution</span></span>
<span data-ttu-id="f55e7-128">Most agent-related or extension-related failures for Linux VMs are caused by issues that affect an outdated VM agent.</span><span class="sxs-lookup"><span data-stu-id="f55e7-128">Most agent-related or extension-related failures for Linux VMs are caused by issues that affect an outdated VM agent.</span></span> <span data-ttu-id="f55e7-129">To troubleshoot this issue, follow these general guidelines:</span><span class="sxs-lookup"><span data-stu-id="f55e7-129">To troubleshoot this issue, follow these general guidelines:</span></span>

1. <span data-ttu-id="f55e7-130">Follow the instructions for [updating the Linux VM agent](../virtual-machines/linux/update-agent.md).</span><span class="sxs-lookup"><span data-stu-id="f55e7-130">Follow the instructions for [updating the Linux VM agent](../virtual-machines/linux/update-agent.md).</span></span>

 >[!NOTE]
 ><span data-ttu-id="f55e7-131">We *strongly recommend* that you update the agent only through a distribution repository.</span><span class="sxs-lookup"><span data-stu-id="f55e7-131">We *strongly recommend* that you update the agent only through a distribution repository.</span></span> <span data-ttu-id="f55e7-132">We do not recommend downloading the agent code directly from GitHub and updating it.</span><span class="sxs-lookup"><span data-stu-id="f55e7-132">We do not recommend downloading the agent code directly from GitHub and updating it.</span></span> <span data-ttu-id="f55e7-133">If the latest agent is unavailable for your distribution, contact distribution support for instructions on how to install it.</span><span class="sxs-lookup"><span data-stu-id="f55e7-133">If the latest agent is unavailable for your distribution, contact distribution support for instructions on how to install it.</span></span> <span data-ttu-id="f55e7-134">To check for the most recent agent, go to the [Windows Azure Linux agent](https://github.com/Azure/WALinuxAgent/releases) page in the GitHub repository.</span><span class="sxs-lookup"><span data-stu-id="f55e7-134">To check for the most recent agent, go to the [Windows Azure Linux agent](https://github.com/Azure/WALinuxAgent/releases) page in the GitHub repository.</span></span>

2. <span data-ttu-id="f55e7-135">Make sure that the Azure agent is running on the VM by running the following command: `ps -e`</span><span class="sxs-lookup"><span data-stu-id="f55e7-135">Make sure that the Azure agent is running on the VM by running the following command: `ps -e`</span></span>

 <span data-ttu-id="f55e7-136">If the process is not running, restart it by using the following commands:</span><span class="sxs-lookup"><span data-stu-id="f55e7-136">If the process is not running, restart it by using the following commands:</span></span>

 * <span data-ttu-id="f55e7-137">For Ubuntu: `service walinuxagent start`</span><span class="sxs-lookup"><span data-stu-id="f55e7-137">For Ubuntu: `service walinuxagent start`</span></span>
 * <span data-ttu-id="f55e7-138">For other distributions: `service waagent start`</span><span class="sxs-lookup"><span data-stu-id="f55e7-138">For other distributions: `service waagent start`</span></span>

3. <span data-ttu-id="f55e7-139">[Configure the auto restart agent](https://github.com/Azure/WALinuxAgent/wiki/Known-Issues#mitigate_agent_crash).</span><span class="sxs-lookup"><span data-stu-id="f55e7-139">[Configure the auto restart agent](https://github.com/Azure/WALinuxAgent/wiki/Known-Issues#mitigate_agent_crash).</span></span>
4. <span data-ttu-id="f55e7-140">Run a new test backup.</span><span class="sxs-lookup"><span data-stu-id="f55e7-140">Run a new test backup.</span></span> <span data-ttu-id="f55e7-141">If the failure persists, please collect the following logs from the customer’s VM:</span><span class="sxs-lookup"><span data-stu-id="f55e7-141">If the failure persists, please collect the following logs from the customer’s VM:</span></span>

   * <span data-ttu-id="f55e7-142">/var/lib/waagent/\*.xml</span><span class="sxs-lookup"><span data-stu-id="f55e7-142">/var/lib/waagent/\*.xml</span></span>
   * <span data-ttu-id="f55e7-143">/var/log/waagent.log</span><span class="sxs-lookup"><span data-stu-id="f55e7-143">/var/log/waagent.log</span></span>
   * <span data-ttu-id="f55e7-144">/var/log/azure/\*</span><span class="sxs-lookup"><span data-stu-id="f55e7-144">/var/log/azure/\*</span></span>

<span data-ttu-id="f55e7-145">If we require verbose logging for waagent, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="f55e7-145">If we require verbose logging for waagent, follow these steps:</span></span>

1. <span data-ttu-id="f55e7-146">In the /etc/waagent.conf file, locate the following line: **Enable verbose logging (y|n)**</span><span class="sxs-lookup"><span data-stu-id="f55e7-146">In the /etc/waagent.conf file, locate the following line: **Enable verbose logging (y|n)**</span></span>
2. <span data-ttu-id="f55e7-147">Change the **Logs.Verbose** value from *n* to *y*.</span><span class="sxs-lookup"><span data-stu-id="f55e7-147">Change the **Logs.Verbose** value from *n* to *y*.</span></span>
3. <span data-ttu-id="f55e7-148">Save the change, and then restart waagent by following the previous steps in this section.</span><span class="sxs-lookup"><span data-stu-id="f55e7-148">Save the change, and then restart waagent by following the previous steps in this section.</span></span>

## <a name="cause-3-the-backup-extension-fails-to-update-or-load"></a><span data-ttu-id="f55e7-149">Cause 3: The backup extension fails to update or load</span><span class="sxs-lookup"><span data-stu-id="f55e7-149">Cause 3: The backup extension fails to update or load</span></span>
<span data-ttu-id="f55e7-150">If extensions cannot be loaded, Backup fails because a snapshot cannot be taken.</span><span class="sxs-lookup"><span data-stu-id="f55e7-150">If extensions cannot be loaded, Backup fails because a snapshot cannot be taken.</span></span>

### <a name="solution"></a><span data-ttu-id="f55e7-151">Solution</span><span class="sxs-lookup"><span data-stu-id="f55e7-151">Solution</span></span>

<span data-ttu-id="f55e7-152">For Windows guests:</span><span class="sxs-lookup"><span data-stu-id="f55e7-152">For Windows guests:</span></span>

<span data-ttu-id="f55e7-153">Verify that the iaasvmprovider service is enabled and has a startup type of *automatic*.</span><span class="sxs-lookup"><span data-stu-id="f55e7-153">Verify that the iaasvmprovider service is enabled and has a startup type of *automatic*.</span></span> <span data-ttu-id="f55e7-154">If the service is not configured in this way, enable it to determine whether the next backup succeeds.</span><span class="sxs-lookup"><span data-stu-id="f55e7-154">If the service is not configured in this way, enable it to determine whether the next backup succeeds.</span></span>

<span data-ttu-id="f55e7-155">For Linux guests:</span><span class="sxs-lookup"><span data-stu-id="f55e7-155">For Linux guests:</span></span>

<span data-ttu-id="f55e7-156">The latest version of VMSnapshot for Linux (the extension used by Backup) is 1.0.91.0.</span><span class="sxs-lookup"><span data-stu-id="f55e7-156">The latest version of VMSnapshot for Linux (the extension used by Backup) is 1.0.91.0.</span></span>

<span data-ttu-id="f55e7-157">If the backup extension still fails to update or load, you can force the VMSnapshot extension to be reloaded by uninstalling the extension.</span><span class="sxs-lookup"><span data-stu-id="f55e7-157">If the backup extension still fails to update or load, you can force the VMSnapshot extension to be reloaded by uninstalling the extension.</span></span> <span data-ttu-id="f55e7-158">The next backup attempt will reload the extension.</span><span class="sxs-lookup"><span data-stu-id="f55e7-158">The next backup attempt will reload the extension.</span></span>

<span data-ttu-id="f55e7-159">To uninstall the extension, do the following:</span><span class="sxs-lookup"><span data-stu-id="f55e7-159">To uninstall the extension, do the following:</span></span>

1. <span data-ttu-id="f55e7-160">Go to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="f55e7-160">Go to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="f55e7-161">Locate the VM that has backup problems.</span><span class="sxs-lookup"><span data-stu-id="f55e7-161">Locate the VM that has backup problems.</span></span>
3. <span data-ttu-id="f55e7-162">Click **Settings**.</span><span class="sxs-lookup"><span data-stu-id="f55e7-162">Click **Settings**.</span></span>
4. <span data-ttu-id="f55e7-163">Click **Extensions**.</span><span class="sxs-lookup"><span data-stu-id="f55e7-163">Click **Extensions**.</span></span>
5. <span data-ttu-id="f55e7-164">Click **Vmsnapshot Extension**.</span><span class="sxs-lookup"><span data-stu-id="f55e7-164">Click **Vmsnapshot Extension**.</span></span>
6. <span data-ttu-id="f55e7-165">Click **Uninstall**.</span><span class="sxs-lookup"><span data-stu-id="f55e7-165">Click **Uninstall**.</span></span>  

<span data-ttu-id="f55e7-166">This procedure causes the extension to be reinstalled during the next backup.</span><span class="sxs-lookup"><span data-stu-id="f55e7-166">This procedure causes the extension to be reinstalled during the next backup.</span></span>

## <a name="cause-4-the-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken"></a><span data-ttu-id="f55e7-167">Cause 4: The snapshot status cannot be retrieved or a snapshot cannot be taken</span><span class="sxs-lookup"><span data-stu-id="f55e7-167">Cause 4: The snapshot status cannot be retrieved or a snapshot cannot be taken</span></span>
<span data-ttu-id="f55e7-168">The VM backup relies on issuing a snapshot command to the underlying storage account.</span><span class="sxs-lookup"><span data-stu-id="f55e7-168">The VM backup relies on issuing a snapshot command to the underlying storage account.</span></span> <span data-ttu-id="f55e7-169">Backup can fail either because it has no access to the storage account or because the execution of the snapshot task is delayed.</span><span class="sxs-lookup"><span data-stu-id="f55e7-169">Backup can fail either because it has no access to the storage account or because the execution of the snapshot task is delayed.</span></span>

### <a name="solution"></a><span data-ttu-id="f55e7-170">Solution</span><span class="sxs-lookup"><span data-stu-id="f55e7-170">Solution</span></span>
<span data-ttu-id="f55e7-171">The following conditions can cause snapshot task failure:</span><span class="sxs-lookup"><span data-stu-id="f55e7-171">The following conditions can cause snapshot task failure:</span></span>

| <span data-ttu-id="f55e7-172">Cause</span><span class="sxs-lookup"><span data-stu-id="f55e7-172">Cause</span></span> | <span data-ttu-id="f55e7-173">Solution</span><span class="sxs-lookup"><span data-stu-id="f55e7-173">Solution</span></span> |
| --- | --- |
| <span data-ttu-id="f55e7-174">The VM has SQL Server backup configured.</span><span class="sxs-lookup"><span data-stu-id="f55e7-174">The VM has SQL Server backup configured.</span></span> | <span data-ttu-id="f55e7-175">By default, the VM backup runs a VSS full backup on Windows VMs.</span><span class="sxs-lookup"><span data-stu-id="f55e7-175">By default, the VM backup runs a VSS full backup on Windows VMs.</span></span> <span data-ttu-id="f55e7-176">On VMs that are running SQL Server-based servers and on which SQL Server backup is configured, snapshot execution delays may occur.</span><span class="sxs-lookup"><span data-stu-id="f55e7-176">On VMs that are running SQL Server-based servers and on which SQL Server backup is configured, snapshot execution delays may occur.</span></span><br><br><span data-ttu-id="f55e7-177">If you are experiencing a Backup failure because of a snapshot issue, set the following registry key:</span><span class="sxs-lookup"><span data-stu-id="f55e7-177">If you are experiencing a Backup failure because of a snapshot issue, set the following registry key:</span></span><br><br><span data-ttu-id="f55e7-178">**[HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\BCDRAGENT] "USEVSSCOPYBACKUP"="TRUE"**</span><span class="sxs-lookup"><span data-stu-id="f55e7-178">**[HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\BCDRAGENT] "USEVSSCOPYBACKUP"="TRUE"**</span></span> |
| <span data-ttu-id="f55e7-179">The VM status is reported incorrectly because the VM is shut down in RDP.</span><span class="sxs-lookup"><span data-stu-id="f55e7-179">The VM status is reported incorrectly because the VM is shut down in RDP.</span></span> | <span data-ttu-id="f55e7-180">If you shut down the VM in Remote Desktop Protocol (RDP), check the portal to determine whether the VM status is correct.</span><span class="sxs-lookup"><span data-stu-id="f55e7-180">If you shut down the VM in Remote Desktop Protocol (RDP), check the portal to determine whether the VM status is correct.</span></span> <span data-ttu-id="f55e7-181">If it’s not correct, shut down the VM in the portal by using the **Shutdown** option on the VM dashboard.</span><span class="sxs-lookup"><span data-stu-id="f55e7-181">If it’s not correct, shut down the VM in the portal by using the **Shutdown** option on the VM dashboard.</span></span> |
| <span data-ttu-id="f55e7-182">Many VMs from the same cloud service are configured to back up at the same time.</span><span class="sxs-lookup"><span data-stu-id="f55e7-182">Many VMs from the same cloud service are configured to back up at the same time.</span></span> | <span data-ttu-id="f55e7-183">It’s a best practice to spread out the backup schedules for VMs from the same cloud service.</span><span class="sxs-lookup"><span data-stu-id="f55e7-183">It’s a best practice to spread out the backup schedules for VMs from the same cloud service.</span></span> |
| <span data-ttu-id="f55e7-184">The VM is running at high CPU or memory usage.</span><span class="sxs-lookup"><span data-stu-id="f55e7-184">The VM is running at high CPU or memory usage.</span></span> | <span data-ttu-id="f55e7-185">If the VM is running at high CPU usage (more than 90 percent) or high memory usage, the snapshot task is queued and delayed, and it eventually times out. In this situation, try an on-demand backup.</span><span class="sxs-lookup"><span data-stu-id="f55e7-185">If the VM is running at high CPU usage (more than 90 percent) or high memory usage, the snapshot task is queued and delayed, and it eventually times out. In this situation, try an on-demand backup.</span></span> |
| <span data-ttu-id="f55e7-186">The VM cannot get the host/fabric address from DHCP.</span><span class="sxs-lookup"><span data-stu-id="f55e7-186">The VM cannot get the host/fabric address from DHCP.</span></span> | <span data-ttu-id="f55e7-187">DHCP must be enabled inside the guest for the IaaS VM backup to work.</span><span class="sxs-lookup"><span data-stu-id="f55e7-187">DHCP must be enabled inside the guest for the IaaS VM backup to work.</span></span>  <span data-ttu-id="f55e7-188">If the VM cannot get the host/fabric address from DHCP response 245, it cannot download or run any extensions.</span><span class="sxs-lookup"><span data-stu-id="f55e7-188">If the VM cannot get the host/fabric address from DHCP response 245, it cannot download or run any extensions.</span></span> <span data-ttu-id="f55e7-189">If you need a static private IP, you should configure it through the platform.</span><span class="sxs-lookup"><span data-stu-id="f55e7-189">If you need a static private IP, you should configure it through the platform.</span></span> <span data-ttu-id="f55e7-190">The DHCP option inside the VM should be left enabled.</span><span class="sxs-lookup"><span data-stu-id="f55e7-190">The DHCP option inside the VM should be left enabled.</span></span> <span data-ttu-id="f55e7-191">For more information, see [Setting a Static Internal Private IP](../virtual-network/virtual-networks-reserved-private-ip.md).</span><span class="sxs-lookup"><span data-stu-id="f55e7-191">For more information, see [Setting a Static Internal Private IP](../virtual-network/virtual-networks-reserved-private-ip.md).</span></span> |