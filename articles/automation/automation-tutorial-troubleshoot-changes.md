---
title: Troubleshoot changes on an Azure virtual machine | Microsoft Docs
description: Use Change Tracking to troubleshoot changes on an Azure virtual machine.
services: automation
ms.service: automation
ms.component: change-inventory-management
keywords: change, tracking, automation
author: jennyhunter-msft
ms.author: jehunte
ms.date: 08/27/2018
ms.topic: tutorial
ms.custom: mvc
manager: carmonm
ms.openlocfilehash: fd94fd234067f63eab424c7f757d4adf842e7b46
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866744"
---
# <a name="troubleshoot-changes-in-your-environment"></a><span data-ttu-id="fc9d6-104">Troubleshoot changes in your environment</span><span class="sxs-lookup"><span data-stu-id="fc9d6-104">Troubleshoot changes in your environment</span></span>

<span data-ttu-id="fc9d6-105">In this tutorial, you learn how to troubleshoot changes on an Azure virtual machine.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-105">In this tutorial, you learn how to troubleshoot changes on an Azure virtual machine.</span></span> <span data-ttu-id="fc9d6-106">By enabling Change tracking, you can track changes to software, files, Linux daemons, Windows Services, and Windows Registry keys on your computers.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-106">By enabling Change tracking, you can track changes to software, files, Linux daemons, Windows Services, and Windows Registry keys on your computers.</span></span>
<span data-ttu-id="fc9d6-107">Identifying these configuration changes can help you pinpoint operational issues across your environment.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-107">Identifying these configuration changes can help you pinpoint operational issues across your environment.</span></span>

<span data-ttu-id="fc9d6-108">In this tutorial you learn how to:</span><span class="sxs-lookup"><span data-stu-id="fc9d6-108">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="fc9d6-109">Onboard a VM for Change tracking and Inventory</span><span class="sxs-lookup"><span data-stu-id="fc9d6-109">Onboard a VM for Change tracking and Inventory</span></span>
> * <span data-ttu-id="fc9d6-110">Search change logs for stopped services</span><span class="sxs-lookup"><span data-stu-id="fc9d6-110">Search change logs for stopped services</span></span>
> * <span data-ttu-id="fc9d6-111">Configure change tracking</span><span class="sxs-lookup"><span data-stu-id="fc9d6-111">Configure change tracking</span></span>
> * <span data-ttu-id="fc9d6-112">Enable Activity log connection</span><span class="sxs-lookup"><span data-stu-id="fc9d6-112">Enable Activity log connection</span></span>
> * <span data-ttu-id="fc9d6-113">Trigger an event</span><span class="sxs-lookup"><span data-stu-id="fc9d6-113">Trigger an event</span></span>
> * <span data-ttu-id="fc9d6-114">View changes</span><span class="sxs-lookup"><span data-stu-id="fc9d6-114">View changes</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fc9d6-115">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="fc9d6-115">Prerequisites</span></span>

<span data-ttu-id="fc9d6-116">To complete this tutorial, you need:</span><span class="sxs-lookup"><span data-stu-id="fc9d6-116">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="fc9d6-117">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-117">An Azure subscription.</span></span> <span data-ttu-id="fc9d6-118">If you don't have one yet, you can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="fc9d6-118">If you don't have one yet, you can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).</span></span>
* <span data-ttu-id="fc9d6-119">An [Automation account](automation-offering-get-started.md) to hold the watcher and action runbooks and the Watcher Task.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-119">An [Automation account](automation-offering-get-started.md) to hold the watcher and action runbooks and the Watcher Task.</span></span>
* <span data-ttu-id="fc9d6-120">A [virtual machine](../virtual-machines/windows/quick-create-portal.md) to onboard.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-120">A [virtual machine](../virtual-machines/windows/quick-create-portal.md) to onboard.</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="fc9d6-121">Log in to Azure</span><span class="sxs-lookup"><span data-stu-id="fc9d6-121">Log in to Azure</span></span>

<span data-ttu-id="fc9d6-122">Log in to the Azure portal at http://portal.azure.com.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-122">Log in to the Azure portal at http://portal.azure.com.</span></span>

## <a name="enable-change-tracking-and-inventory"></a><span data-ttu-id="fc9d6-123">Enable Change tracking and Inventory</span><span class="sxs-lookup"><span data-stu-id="fc9d6-123">Enable Change tracking and Inventory</span></span>

<span data-ttu-id="fc9d6-124">First you need to enable Change tracking and Inventory for your VM for this tutorial.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-124">First you need to enable Change tracking and Inventory for your VM for this tutorial.</span></span> <span data-ttu-id="fc9d6-125">If you have previously enabled another automation solution for a VM, this step is not necessary.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-125">If you have previously enabled another automation solution for a VM, this step is not necessary.</span></span>

1. <span data-ttu-id="fc9d6-126">On the left menu, select **Virtual machines** and select a VM from the list</span><span class="sxs-lookup"><span data-stu-id="fc9d6-126">On the left menu, select **Virtual machines** and select a VM from the list</span></span>
1. <span data-ttu-id="fc9d6-127">On the left menu, under the **OPERATIONS** section, click **Inventory**.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-127">On the left menu, under the **OPERATIONS** section, click **Inventory**.</span></span> <span data-ttu-id="fc9d6-128">The **Change tracking** page opens.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-128">The **Change tracking** page opens.</span></span>

<span data-ttu-id="fc9d6-129">![Enable change](./media/automation-tutorial-troubleshoot-changes/enableinventory.png) The **Change Tracking** screen opens.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-129">![Enable change](./media/automation-tutorial-troubleshoot-changes/enableinventory.png) The **Change Tracking** screen opens.</span></span> <span data-ttu-id="fc9d6-130">Configure the location, Log analytics workspace, and Automation account to use and click **Enable**.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-130">Configure the location, Log analytics workspace, and Automation account to use and click **Enable**.</span></span> <span data-ttu-id="fc9d6-131">If the fields are grayed out, that means another automation solution is enabled for the VM and the same workspace and Automation account must be used.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-131">If the fields are grayed out, that means another automation solution is enabled for the VM and the same workspace and Automation account must be used.</span></span>

<span data-ttu-id="fc9d6-132">A [Log Analytics](../log-analytics/log-analytics-overview.md?toc=%2fazure%2fautomation%2ftoc.json) workspace is used to collect data that is generated by features and services such as Inventory.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-132">A [Log Analytics](../log-analytics/log-analytics-overview.md?toc=%2fazure%2fautomation%2ftoc.json) workspace is used to collect data that is generated by features and services such as Inventory.</span></span>
<span data-ttu-id="fc9d6-133">The workspace provides a single location to review and analyze data from multiple sources.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-133">The workspace provides a single location to review and analyze data from multiple sources.</span></span>

<span data-ttu-id="fc9d6-134">During onboarding the VM is provisioned with the Microsoft Monitoring Agent (MMA) and hybrid worker.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-134">During onboarding the VM is provisioned with the Microsoft Monitoring Agent (MMA) and hybrid worker.</span></span>
<span data-ttu-id="fc9d6-135">This agent is used to communicate with the VM and obtain information about installed software.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-135">This agent is used to communicate with the VM and obtain information about installed software.</span></span>

<span data-ttu-id="fc9d6-136">Enabling the solution can take up to 15 minutes.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-136">Enabling the solution can take up to 15 minutes.</span></span> <span data-ttu-id="fc9d6-137">During this time, you shouldn't close the browser window.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-137">During this time, you shouldn't close the browser window.</span></span>
<span data-ttu-id="fc9d6-138">After the solution is enabled, information about installed software and changes on the VM flows to Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-138">After the solution is enabled, information about installed software and changes on the VM flows to Log Analytics.</span></span>
<span data-ttu-id="fc9d6-139">It can take between 30 minutes and 6 hours for the data to be available for analysis.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-139">It can take between 30 minutes and 6 hours for the data to be available for analysis.</span></span>

## <a name="using-change-tracking-in-log-analytics"></a><span data-ttu-id="fc9d6-140">Using Change tracking in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="fc9d6-140">Using Change tracking in Log Analytics</span></span>

<span data-ttu-id="fc9d6-141">Change tracking generates log data that is sent to Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-141">Change tracking generates log data that is sent to Log Analytics.</span></span> <span data-ttu-id="fc9d6-142">To search the logs by running queries, select **Log Analytics** at the top of the **Change tracking** window.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-142">To search the logs by running queries, select **Log Analytics** at the top of the **Change tracking** window.</span></span>
<span data-ttu-id="fc9d6-143">Change tracking data is stored under the type **ConfigurationChange**.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-143">Change tracking data is stored under the type **ConfigurationChange**.</span></span> <span data-ttu-id="fc9d6-144">The following sample Log Analytics query returns all the Windows Services that have been stopped.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-144">The following sample Log Analytics query returns all the Windows Services that have been stopped.</span></span>

```
ConfigurationChange
| where ConfigChangeType == "WindowsServices" and SvcState == "Stopped"
```

<span data-ttu-id="fc9d6-145">To learn more about running and searching log files in Log Analytics, see [Azure Log Analytics](https://docs.loganalytics.io/index).</span><span class="sxs-lookup"><span data-stu-id="fc9d6-145">To learn more about running and searching log files in Log Analytics, see [Azure Log Analytics](https://docs.loganalytics.io/index).</span></span>

## <a name="configure-change-tracking"></a><span data-ttu-id="fc9d6-146">Configure Change tracking</span><span class="sxs-lookup"><span data-stu-id="fc9d6-146">Configure Change tracking</span></span>

<span data-ttu-id="fc9d6-147">Change tracking gives you the ability to track configuration changes on your VM.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-147">Change tracking gives you the ability to track configuration changes on your VM.</span></span> <span data-ttu-id="fc9d6-148">The following steps show you how to configure tracking of registry keys and files.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-148">The following steps show you how to configure tracking of registry keys and files.</span></span>
 
<span data-ttu-id="fc9d6-149">To choose which files and Registry keys to collect and track, select **Edit settings** at the top of the **Change tracking** page.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-149">To choose which files and Registry keys to collect and track, select **Edit settings** at the top of the **Change tracking** page.</span></span>

> [!NOTE]
> <span data-ttu-id="fc9d6-150">Inventory and Change tracking use the same collection settings, and settings are configured on a workspace level.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-150">Inventory and Change tracking use the same collection settings, and settings are configured on a workspace level.</span></span>

<span data-ttu-id="fc9d6-151">In the **Workspace Configuration** window, add the Windows Registry keys, Windows files, or Linux files to be tracked, as outlined in the next three sections.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-151">In the **Workspace Configuration** window, add the Windows Registry keys, Windows files, or Linux files to be tracked, as outlined in the next three sections.</span></span>

### <a name="add-a-windows-registry-key"></a><span data-ttu-id="fc9d6-152">Add a Windows Registry key</span><span class="sxs-lookup"><span data-stu-id="fc9d6-152">Add a Windows Registry key</span></span>

1. <span data-ttu-id="fc9d6-153">On the **Windows Registry** tab, select **Add**.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-153">On the **Windows Registry** tab, select **Add**.</span></span>
    <span data-ttu-id="fc9d6-154">The **Add Windows Registry for Change Tracking** window opens.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-154">The **Add Windows Registry for Change Tracking** window opens.</span></span>

3. <span data-ttu-id="fc9d6-155">On the **Add Windows Registry for Change Tracking**, enter the information for the key to track and click **Save**</span><span class="sxs-lookup"><span data-stu-id="fc9d6-155">On the **Add Windows Registry for Change Tracking**, enter the information for the key to track and click **Save**</span></span>

|<span data-ttu-id="fc9d6-156">Property</span><span class="sxs-lookup"><span data-stu-id="fc9d6-156">Property</span></span>  |<span data-ttu-id="fc9d6-157">Description</span><span class="sxs-lookup"><span data-stu-id="fc9d6-157">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="fc9d6-158">Enabled</span><span class="sxs-lookup"><span data-stu-id="fc9d6-158">Enabled</span></span>     | <span data-ttu-id="fc9d6-159">Determines if the setting is applied</span><span class="sxs-lookup"><span data-stu-id="fc9d6-159">Determines if the setting is applied</span></span>        |
|<span data-ttu-id="fc9d6-160">Item Name</span><span class="sxs-lookup"><span data-stu-id="fc9d6-160">Item Name</span></span>     | <span data-ttu-id="fc9d6-161">Friendly name of the file to be tracked</span><span class="sxs-lookup"><span data-stu-id="fc9d6-161">Friendly name of the file to be tracked</span></span>        |
|<span data-ttu-id="fc9d6-162">Group</span><span class="sxs-lookup"><span data-stu-id="fc9d6-162">Group</span></span>     | <span data-ttu-id="fc9d6-163">A group name for logically grouping files</span><span class="sxs-lookup"><span data-stu-id="fc9d6-163">A group name for logically grouping files</span></span>        |
|<span data-ttu-id="fc9d6-164">Windows Registry Key</span><span class="sxs-lookup"><span data-stu-id="fc9d6-164">Windows Registry Key</span></span>   | <span data-ttu-id="fc9d6-165">The path to check for the file For example: "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\User Shell Folders\Common Startup"</span><span class="sxs-lookup"><span data-stu-id="fc9d6-165">The path to check for the file For example: "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\User Shell Folders\Common Startup"</span></span>      |

### <a name="add-a-windows-file"></a><span data-ttu-id="fc9d6-166">Add a Windows file</span><span class="sxs-lookup"><span data-stu-id="fc9d6-166">Add a Windows file</span></span>

1. <span data-ttu-id="fc9d6-167">On the **Windows Files** tab, select **Add**.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-167">On the **Windows Files** tab, select **Add**.</span></span> <span data-ttu-id="fc9d6-168">The **Add Windows File for Change Tracking** window opens.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-168">The **Add Windows File for Change Tracking** window opens.</span></span>

1. <span data-ttu-id="fc9d6-169">On the **Add Windows File for Change Tracking**, enter the information for the file or directory to track and click **Save**</span><span class="sxs-lookup"><span data-stu-id="fc9d6-169">On the **Add Windows File for Change Tracking**, enter the information for the file or directory to track and click **Save**</span></span>

|<span data-ttu-id="fc9d6-170">Property</span><span class="sxs-lookup"><span data-stu-id="fc9d6-170">Property</span></span>  |<span data-ttu-id="fc9d6-171">Description</span><span class="sxs-lookup"><span data-stu-id="fc9d6-171">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="fc9d6-172">Enabled</span><span class="sxs-lookup"><span data-stu-id="fc9d6-172">Enabled</span></span>     | <span data-ttu-id="fc9d6-173">Determines if the setting is applied</span><span class="sxs-lookup"><span data-stu-id="fc9d6-173">Determines if the setting is applied</span></span>        |
|<span data-ttu-id="fc9d6-174">Item Name</span><span class="sxs-lookup"><span data-stu-id="fc9d6-174">Item Name</span></span>     | <span data-ttu-id="fc9d6-175">Friendly name of the file to be tracked</span><span class="sxs-lookup"><span data-stu-id="fc9d6-175">Friendly name of the file to be tracked</span></span>        |
|<span data-ttu-id="fc9d6-176">Group</span><span class="sxs-lookup"><span data-stu-id="fc9d6-176">Group</span></span>     | <span data-ttu-id="fc9d6-177">A group name for logically grouping files</span><span class="sxs-lookup"><span data-stu-id="fc9d6-177">A group name for logically grouping files</span></span>        |
|<span data-ttu-id="fc9d6-178">Enter Path</span><span class="sxs-lookup"><span data-stu-id="fc9d6-178">Enter Path</span></span>     | <span data-ttu-id="fc9d6-179">The path to check for the file For example: "c:\temp\\\*.txt"</span><span class="sxs-lookup"><span data-stu-id="fc9d6-179">The path to check for the file For example: "c:\temp\\\*.txt"</span></span><br><span data-ttu-id="fc9d6-180">You can also use environment variables such as "%winDir%\System32\\\*.\*"</span><span class="sxs-lookup"><span data-stu-id="fc9d6-180">You can also use environment variables such as "%winDir%\System32\\\*.\*"</span></span>         |
|<span data-ttu-id="fc9d6-181">Recursion</span><span class="sxs-lookup"><span data-stu-id="fc9d6-181">Recursion</span></span>     | <span data-ttu-id="fc9d6-182">Determines if recursion is used when looking for the item to be tracked.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-182">Determines if recursion is used when looking for the item to be tracked.</span></span>        |
|<span data-ttu-id="fc9d6-183">Upload file content for all settings</span><span class="sxs-lookup"><span data-stu-id="fc9d6-183">Upload file content for all settings</span></span>| <span data-ttu-id="fc9d6-184">Turns on or off file content upload on tracked changes.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-184">Turns on or off file content upload on tracked changes.</span></span> <span data-ttu-id="fc9d6-185">Available options: **True** or **False**.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-185">Available options: **True** or **False**.</span></span>|

### <a name="add-a-linux-file"></a><span data-ttu-id="fc9d6-186">Add a Linux file</span><span class="sxs-lookup"><span data-stu-id="fc9d6-186">Add a Linux file</span></span>

1. <span data-ttu-id="fc9d6-187">On the **Linux Files** tab, select **Add**.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-187">On the **Linux Files** tab, select **Add**.</span></span> <span data-ttu-id="fc9d6-188">The **Add Linux File for Change Tracking** window opens.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-188">The **Add Linux File for Change Tracking** window opens.</span></span>

1. <span data-ttu-id="fc9d6-189">On the **Add Linux File for Change Tracking**, enter the information for the file or directory to track and click **Save**</span><span class="sxs-lookup"><span data-stu-id="fc9d6-189">On the **Add Linux File for Change Tracking**, enter the information for the file or directory to track and click **Save**</span></span>

|<span data-ttu-id="fc9d6-190">Property</span><span class="sxs-lookup"><span data-stu-id="fc9d6-190">Property</span></span>  |<span data-ttu-id="fc9d6-191">Description</span><span class="sxs-lookup"><span data-stu-id="fc9d6-191">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="fc9d6-192">Enabled</span><span class="sxs-lookup"><span data-stu-id="fc9d6-192">Enabled</span></span>     | <span data-ttu-id="fc9d6-193">Determines if the setting is applied</span><span class="sxs-lookup"><span data-stu-id="fc9d6-193">Determines if the setting is applied</span></span>        |
|<span data-ttu-id="fc9d6-194">Item Name</span><span class="sxs-lookup"><span data-stu-id="fc9d6-194">Item Name</span></span>     | <span data-ttu-id="fc9d6-195">Friendly name of the file to be tracked</span><span class="sxs-lookup"><span data-stu-id="fc9d6-195">Friendly name of the file to be tracked</span></span>        |
|<span data-ttu-id="fc9d6-196">Group</span><span class="sxs-lookup"><span data-stu-id="fc9d6-196">Group</span></span>     | <span data-ttu-id="fc9d6-197">A group name for logically grouping files</span><span class="sxs-lookup"><span data-stu-id="fc9d6-197">A group name for logically grouping files</span></span>        |
|<span data-ttu-id="fc9d6-198">Enter Path</span><span class="sxs-lookup"><span data-stu-id="fc9d6-198">Enter Path</span></span>     | <span data-ttu-id="fc9d6-199">The path to check for the file For example: "/etc/\*.conf"</span><span class="sxs-lookup"><span data-stu-id="fc9d6-199">The path to check for the file For example: "/etc/\*.conf"</span></span>       |
|<span data-ttu-id="fc9d6-200">Path Type</span><span class="sxs-lookup"><span data-stu-id="fc9d6-200">Path Type</span></span>     | <span data-ttu-id="fc9d6-201">Type of item to be tracked, possible values are File and Directory</span><span class="sxs-lookup"><span data-stu-id="fc9d6-201">Type of item to be tracked, possible values are File and Directory</span></span>        |
|<span data-ttu-id="fc9d6-202">Recursion</span><span class="sxs-lookup"><span data-stu-id="fc9d6-202">Recursion</span></span>     | <span data-ttu-id="fc9d6-203">Determines if recursion is used when looking for the item to be tracked.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-203">Determines if recursion is used when looking for the item to be tracked.</span></span>        |
|<span data-ttu-id="fc9d6-204">Use Sudo</span><span class="sxs-lookup"><span data-stu-id="fc9d6-204">Use Sudo</span></span>     | <span data-ttu-id="fc9d6-205">This setting determines if sudo is used when checking for the item.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-205">This setting determines if sudo is used when checking for the item.</span></span>         |
|<span data-ttu-id="fc9d6-206">Links</span><span class="sxs-lookup"><span data-stu-id="fc9d6-206">Links</span></span>     | <span data-ttu-id="fc9d6-207">This setting determines how symbolic links dealt with when traversing directories.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-207">This setting determines how symbolic links dealt with when traversing directories.</span></span><br> <span data-ttu-id="fc9d6-208">**Ignore** - Ignores symbolic links and does not include the files/directories referenced</span><span class="sxs-lookup"><span data-stu-id="fc9d6-208">**Ignore** - Ignores symbolic links and does not include the files/directories referenced</span></span><br><span data-ttu-id="fc9d6-209">**Follow** - Follows the symbolic links during recursion and also includes the files/directories referenced</span><span class="sxs-lookup"><span data-stu-id="fc9d6-209">**Follow** - Follows the symbolic links during recursion and also includes the files/directories referenced</span></span><br><span data-ttu-id="fc9d6-210">**Manage** - Follows the symbolic links and allows alter the treatment of returned content</span><span class="sxs-lookup"><span data-stu-id="fc9d6-210">**Manage** - Follows the symbolic links and allows alter the treatment of returned content</span></span>      |
|<span data-ttu-id="fc9d6-211">Upload file content for all settings</span><span class="sxs-lookup"><span data-stu-id="fc9d6-211">Upload file content for all settings</span></span>| <span data-ttu-id="fc9d6-212">Turns on or off file content upload on tracked changes.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-212">Turns on or off file content upload on tracked changes.</span></span> <span data-ttu-id="fc9d6-213">Available options: **True** or **False**.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-213">Available options: **True** or **False**.</span></span>|

   > [!NOTE]
   > <span data-ttu-id="fc9d6-214">The "Manage" links option is not recommended.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-214">The "Manage" links option is not recommended.</span></span> <span data-ttu-id="fc9d6-215">File content retrieval is not supported.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-215">File content retrieval is not supported.</span></span>

## <a name="enable-activity-log-connection"></a><span data-ttu-id="fc9d6-216">Enable Activity log connection</span><span class="sxs-lookup"><span data-stu-id="fc9d6-216">Enable Activity log connection</span></span>

<span data-ttu-id="fc9d6-217">From the **Change tracking** page on your VM, select **Manage Activity Log Connection**.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-217">From the **Change tracking** page on your VM, select **Manage Activity Log Connection**.</span></span> <span data-ttu-id="fc9d6-218">This task opens the **Azure Activity log** page.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-218">This task opens the **Azure Activity log** page.</span></span> <span data-ttu-id="fc9d6-219">Select **Connect** to connect Change tracking to the Azure activity log for your VM.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-219">Select **Connect** to connect Change tracking to the Azure activity log for your VM.</span></span>

<span data-ttu-id="fc9d6-220">With this setting enabled, navigate to the **Overview** page for your VM and select **Stop** to stop your VM.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-220">With this setting enabled, navigate to the **Overview** page for your VM and select **Stop** to stop your VM.</span></span> <span data-ttu-id="fc9d6-221">When prompted, select **Yes** to stop the VM.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-221">When prompted, select **Yes** to stop the VM.</span></span> <span data-ttu-id="fc9d6-222">When it is deallocated, select **Start** to restart your VM.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-222">When it is deallocated, select **Start** to restart your VM.</span></span>

<span data-ttu-id="fc9d6-223">Stopping and starting a VM logs an event in its activity log.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-223">Stopping and starting a VM logs an event in its activity log.</span></span> <span data-ttu-id="fc9d6-224">Navigate back to the **Change tracking** page.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-224">Navigate back to the **Change tracking** page.</span></span> <span data-ttu-id="fc9d6-225">Select the **Events** tab at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-225">Select the **Events** tab at the bottom of the page.</span></span> <span data-ttu-id="fc9d6-226">After a while, the events shown in the chart and the table.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-226">After a while, the events shown in the chart and the table.</span></span> <span data-ttu-id="fc9d6-227">Like in the preceding step, each event can be selected to view detailed information on the event.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-227">Like in the preceding step, each event can be selected to view detailed information on the event.</span></span>

![Viewing change details in the portal](./media/automation-tutorial-troubleshoot-changes/viewevents.png)

## <a name="view-changes"></a><span data-ttu-id="fc9d6-229">View changes</span><span class="sxs-lookup"><span data-stu-id="fc9d6-229">View changes</span></span>

<span data-ttu-id="fc9d6-230">Once the Change tracking and Inventory solution is enabled, you can view the results on the **Change tracking** page.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-230">Once the Change tracking and Inventory solution is enabled, you can view the results on the **Change tracking** page.</span></span>

<span data-ttu-id="fc9d6-231">From within your VM, select **Change tracking** under **OPERATIONS**.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-231">From within your VM, select **Change tracking** under **OPERATIONS**.</span></span>

![Screenshot that shows the list of changes to the VM](./media/automation-tutorial-troubleshoot-changes/change-tracking-list.png)

<span data-ttu-id="fc9d6-233">The chart shows changes that have occurred over time.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-233">The chart shows changes that have occurred over time.</span></span>
<span data-ttu-id="fc9d6-234">After you have added an Activity Log connection, the line graph at the top displays Azure Activity Log events.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-234">After you have added an Activity Log connection, the line graph at the top displays Azure Activity Log events.</span></span>
<span data-ttu-id="fc9d6-235">Each row of bar graphs represents a different trackable Change type.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-235">Each row of bar graphs represents a different trackable Change type.</span></span>
<span data-ttu-id="fc9d6-236">These types are Linux daemons, files, Windows Registry keys, software, and Windows services.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-236">These types are Linux daemons, files, Windows Registry keys, software, and Windows services.</span></span>
<span data-ttu-id="fc9d6-237">The change tab shows the details for the changes shown in the visualization in descending order of time that the change occurred (most recent first).</span><span class="sxs-lookup"><span data-stu-id="fc9d6-237">The change tab shows the details for the changes shown in the visualization in descending order of time that the change occurred (most recent first).</span></span>
<span data-ttu-id="fc9d6-238">The **Events** tab, the table displays the connected Activity Log events and their corresponding details with the most recent first.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-238">The **Events** tab, the table displays the connected Activity Log events and their corresponding details with the most recent first.</span></span>

<span data-ttu-id="fc9d6-239">You can see in the results, that there were multiple changes to the system, including changes to services and software.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-239">You can see in the results, that there were multiple changes to the system, including changes to services and software.</span></span> <span data-ttu-id="fc9d6-240">You can use the filters at the top of the page to filter the results by **Change type** or by a time range.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-240">You can use the filters at the top of the page to filter the results by **Change type** or by a time range.</span></span>

<span data-ttu-id="fc9d6-241">Select a **WindowsServices** change, this opens the **Change Details** window.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-241">Select a **WindowsServices** change, this opens the **Change Details** window.</span></span> <span data-ttu-id="fc9d6-242">The change details window shows details about the change and the values before and after the change.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-242">The change details window shows details about the change and the values before and after the change.</span></span> <span data-ttu-id="fc9d6-243">In this instance, the Software Protection service was stopped.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-243">In this instance, the Software Protection service was stopped.</span></span>

![Viewing change details in the portal](./media/automation-tutorial-troubleshoot-changes/change-details.png)

## <a name="next-steps"></a><span data-ttu-id="fc9d6-245">Next Steps</span><span class="sxs-lookup"><span data-stu-id="fc9d6-245">Next Steps</span></span>

<span data-ttu-id="fc9d6-246">In this tutorial you learned how to:</span><span class="sxs-lookup"><span data-stu-id="fc9d6-246">In this tutorial you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="fc9d6-247">Onboard a VM for Change tracking and Inventory</span><span class="sxs-lookup"><span data-stu-id="fc9d6-247">Onboard a VM for Change tracking and Inventory</span></span>
> * <span data-ttu-id="fc9d6-248">Search change logs for stopped services</span><span class="sxs-lookup"><span data-stu-id="fc9d6-248">Search change logs for stopped services</span></span>
> * <span data-ttu-id="fc9d6-249">Configure change tracking</span><span class="sxs-lookup"><span data-stu-id="fc9d6-249">Configure change tracking</span></span>
> * <span data-ttu-id="fc9d6-250">Enable Activity log connection</span><span class="sxs-lookup"><span data-stu-id="fc9d6-250">Enable Activity log connection</span></span>
> * <span data-ttu-id="fc9d6-251">Trigger an event</span><span class="sxs-lookup"><span data-stu-id="fc9d6-251">Trigger an event</span></span>
> * <span data-ttu-id="fc9d6-252">View changes</span><span class="sxs-lookup"><span data-stu-id="fc9d6-252">View changes</span></span>

<span data-ttu-id="fc9d6-253">Continue to the overview for the Change tracking and Inventory solution to learn more about it.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-253">Continue to the overview for the Change tracking and Inventory solution to learn more about it.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="fc9d6-254">Change management and Inventory solution</span><span class="sxs-lookup"><span data-stu-id="fc9d6-254">Change management and Inventory solution</span></span>](automation-change-tracking.md)
