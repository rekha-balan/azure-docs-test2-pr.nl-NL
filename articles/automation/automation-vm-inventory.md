---
title: Manage an Azure virtual machine with inventory collection | Microsoft Docs
description: Manage a virtual machine with inventory collection
services: automation
ms.service: automation
ms.component: change-inventory-management
keywords: inventory, automation, change, tracking
author: jennyhunter-msft
ms.author: jehunte
ms.date: 03/30/2018
ms.topic: conceptual
manager: carmonm
ms.openlocfilehash: 30569c3a89de320769d433b5b3a4af9cf4e08e66
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857321"
---
# <a name="manage-an-azure-virtual-machine-with-inventory-collection"></a><span data-ttu-id="1e3bf-104">Manage an Azure virtual machine with inventory collection</span><span class="sxs-lookup"><span data-stu-id="1e3bf-104">Manage an Azure virtual machine with inventory collection</span></span>

<span data-ttu-id="1e3bf-105">You can enable inventory tracking for an Azure virtual machine from the virtual machine's resource page.</span><span class="sxs-lookup"><span data-stu-id="1e3bf-105">You can enable inventory tracking for an Azure virtual machine from the virtual machine's resource page.</span></span> <span data-ttu-id="1e3bf-106">This method provides a browser-based user interface for setting up and configuring inventory collection.</span><span class="sxs-lookup"><span data-stu-id="1e3bf-106">This method provides a browser-based user interface for setting up and configuring inventory collection.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="1e3bf-107">Before you begin</span><span class="sxs-lookup"><span data-stu-id="1e3bf-107">Before you begin</span></span>

<span data-ttu-id="1e3bf-108">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="1e3bf-108">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/).</span></span>

<span data-ttu-id="1e3bf-109">This article assumes you have a VM to configure the solution on.</span><span class="sxs-lookup"><span data-stu-id="1e3bf-109">This article assumes you have a VM to configure the solution on.</span></span> <span data-ttu-id="1e3bf-110">If you don't have an Azure virtual machine, [create a virtual machine](../virtual-machines/windows/quick-create-portal.md).</span><span class="sxs-lookup"><span data-stu-id="1e3bf-110">If you don't have an Azure virtual machine, [create a virtual machine](../virtual-machines/windows/quick-create-portal.md).</span></span>

## <a name="sign-in-to-the-azure-portal"></a><span data-ttu-id="1e3bf-111">Sign in to the Azure portal</span><span class="sxs-lookup"><span data-stu-id="1e3bf-111">Sign in to the Azure portal</span></span>

<span data-ttu-id="1e3bf-112">Sign in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="1e3bf-112">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>

## <a name="enable-inventory-collection-from-the-virtual-machine-resource-page"></a><span data-ttu-id="1e3bf-113">Enable inventory collection from the virtual machine resource page</span><span class="sxs-lookup"><span data-stu-id="1e3bf-113">Enable inventory collection from the virtual machine resource page</span></span>

1. <span data-ttu-id="1e3bf-114">In the left pane of the Azure portal, select **Virtual machines**.</span><span class="sxs-lookup"><span data-stu-id="1e3bf-114">In the left pane of the Azure portal, select **Virtual machines**.</span></span>
2. <span data-ttu-id="1e3bf-115">In the list of virtual machines, select a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="1e3bf-115">In the list of virtual machines, select a virtual machine.</span></span>
3. <span data-ttu-id="1e3bf-116">On the **Resource** menu, under **Operations**, select **Inventory**.</span><span class="sxs-lookup"><span data-stu-id="1e3bf-116">On the **Resource** menu, under **Operations**, select **Inventory**.</span></span>
4. <span data-ttu-id="1e3bf-117">Select a log analytics workspace for storing your data logs.</span><span class="sxs-lookup"><span data-stu-id="1e3bf-117">Select a log analytics workspace for storing your data logs.</span></span>
    <span data-ttu-id="1e3bf-118">If no workspace is available to you for that region, you are prompted to create a default workspace and automation account.</span><span class="sxs-lookup"><span data-stu-id="1e3bf-118">If no workspace is available to you for that region, you are prompted to create a default workspace and automation account.</span></span>
5. <span data-ttu-id="1e3bf-119">To start onboarding your computer, select **Enable**.</span><span class="sxs-lookup"><span data-stu-id="1e3bf-119">To start onboarding your computer, select **Enable**.</span></span>

   ![View onboarding options](./media/automation-vm-inventory/inventory-onboarding-options.png)

    <span data-ttu-id="1e3bf-121">A status bar notifies you that the solution is being enabled.</span><span class="sxs-lookup"><span data-stu-id="1e3bf-121">A status bar notifies you that the solution is being enabled.</span></span> <span data-ttu-id="1e3bf-122">This process can take up to 15 minutes.</span><span class="sxs-lookup"><span data-stu-id="1e3bf-122">This process can take up to 15 minutes.</span></span> <span data-ttu-id="1e3bf-123">During this time, you can close the window, or you can keep it open and it notifies you when the solution is enabled.</span><span class="sxs-lookup"><span data-stu-id="1e3bf-123">During this time, you can close the window, or you can keep it open and it notifies you when the solution is enabled.</span></span> <span data-ttu-id="1e3bf-124">You can monitor the deployment status from the notifications pane.</span><span class="sxs-lookup"><span data-stu-id="1e3bf-124">You can monitor the deployment status from the notifications pane.</span></span>

   ![View the inventory solution immediately after onboarding](./media/automation-vm-inventory/inventory-onboarded.png)

<span data-ttu-id="1e3bf-126">When the deployment is complete, the status bar disappears.</span><span class="sxs-lookup"><span data-stu-id="1e3bf-126">When the deployment is complete, the status bar disappears.</span></span> <span data-ttu-id="1e3bf-127">The system is still collecting inventory data, and the data might not be visible yet.</span><span class="sxs-lookup"><span data-stu-id="1e3bf-127">The system is still collecting inventory data, and the data might not be visible yet.</span></span> <span data-ttu-id="1e3bf-128">A full collection of data can take 24 hours.</span><span class="sxs-lookup"><span data-stu-id="1e3bf-128">A full collection of data can take 24 hours.</span></span>

## <a name="configure-your-inventory-settings"></a><span data-ttu-id="1e3bf-129">Configure your inventory settings</span><span class="sxs-lookup"><span data-stu-id="1e3bf-129">Configure your inventory settings</span></span>

<span data-ttu-id="1e3bf-130">By default, software, Windows services, and Linux daemons are configured for collection.</span><span class="sxs-lookup"><span data-stu-id="1e3bf-130">By default, software, Windows services, and Linux daemons are configured for collection.</span></span> <span data-ttu-id="1e3bf-131">To collect Windows registry and file inventory, configure the inventory collection settings.</span><span class="sxs-lookup"><span data-stu-id="1e3bf-131">To collect Windows registry and file inventory, configure the inventory collection settings.</span></span>

1. <span data-ttu-id="1e3bf-132">In the **Inventory** view, select the **Edit Settings** button at the top of the window.</span><span class="sxs-lookup"><span data-stu-id="1e3bf-132">In the **Inventory** view, select the **Edit Settings** button at the top of the window.</span></span>
2. <span data-ttu-id="1e3bf-133">To add a new collection setting, go to the setting category that you want to add by selecting the **Windows Registry**, **Windows Files**, and **Linux Files** tabs.</span><span class="sxs-lookup"><span data-stu-id="1e3bf-133">To add a new collection setting, go to the setting category that you want to add by selecting the **Windows Registry**, **Windows Files**, and **Linux Files** tabs.</span></span>
3. <span data-ttu-id="1e3bf-134">Select the appropriate category and click **Add** at the top of the window.</span><span class="sxs-lookup"><span data-stu-id="1e3bf-134">Select the appropriate category and click **Add** at the top of the window.</span></span>

<span data-ttu-id="1e3bf-135">The following tables provide information about each property that can be configured for the various categories.</span><span class="sxs-lookup"><span data-stu-id="1e3bf-135">The following tables provide information about each property that can be configured for the various categories.</span></span>

### <a name="windows-registry"></a><span data-ttu-id="1e3bf-136">Windows Registry</span><span class="sxs-lookup"><span data-stu-id="1e3bf-136">Windows Registry</span></span>

|<span data-ttu-id="1e3bf-137">Property</span><span class="sxs-lookup"><span data-stu-id="1e3bf-137">Property</span></span>  |<span data-ttu-id="1e3bf-138">Description</span><span class="sxs-lookup"><span data-stu-id="1e3bf-138">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="1e3bf-139">Enabled</span><span class="sxs-lookup"><span data-stu-id="1e3bf-139">Enabled</span></span>     | <span data-ttu-id="1e3bf-140">Determines if the setting is applied</span><span class="sxs-lookup"><span data-stu-id="1e3bf-140">Determines if the setting is applied</span></span>        |
|<span data-ttu-id="1e3bf-141">Item Name</span><span class="sxs-lookup"><span data-stu-id="1e3bf-141">Item Name</span></span>     | <span data-ttu-id="1e3bf-142">Friendly name of the file to be tracked</span><span class="sxs-lookup"><span data-stu-id="1e3bf-142">Friendly name of the file to be tracked</span></span>        |
|<span data-ttu-id="1e3bf-143">Group</span><span class="sxs-lookup"><span data-stu-id="1e3bf-143">Group</span></span>     | <span data-ttu-id="1e3bf-144">A group name for logically grouping files</span><span class="sxs-lookup"><span data-stu-id="1e3bf-144">A group name for logically grouping files</span></span>        |
|<span data-ttu-id="1e3bf-145">Windows Registry Key</span><span class="sxs-lookup"><span data-stu-id="1e3bf-145">Windows Registry Key</span></span>   | <span data-ttu-id="1e3bf-146">The path to check for the file For example: "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\User Shell Folders\Common Startup"</span><span class="sxs-lookup"><span data-stu-id="1e3bf-146">The path to check for the file For example: "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\User Shell Folders\Common Startup"</span></span>      |

### <a name="windows-files"></a><span data-ttu-id="1e3bf-147">Windows Files</span><span class="sxs-lookup"><span data-stu-id="1e3bf-147">Windows Files</span></span>

|<span data-ttu-id="1e3bf-148">Property</span><span class="sxs-lookup"><span data-stu-id="1e3bf-148">Property</span></span>  |<span data-ttu-id="1e3bf-149">Description</span><span class="sxs-lookup"><span data-stu-id="1e3bf-149">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="1e3bf-150">Enabled</span><span class="sxs-lookup"><span data-stu-id="1e3bf-150">Enabled</span></span>     | <span data-ttu-id="1e3bf-151">Determines if the setting is applied</span><span class="sxs-lookup"><span data-stu-id="1e3bf-151">Determines if the setting is applied</span></span>        |
|<span data-ttu-id="1e3bf-152">Item Name</span><span class="sxs-lookup"><span data-stu-id="1e3bf-152">Item Name</span></span>     | <span data-ttu-id="1e3bf-153">Friendly name of the file to be tracked</span><span class="sxs-lookup"><span data-stu-id="1e3bf-153">Friendly name of the file to be tracked</span></span>        |
|<span data-ttu-id="1e3bf-154">Group</span><span class="sxs-lookup"><span data-stu-id="1e3bf-154">Group</span></span>     | <span data-ttu-id="1e3bf-155">A group name for logically grouping files</span><span class="sxs-lookup"><span data-stu-id="1e3bf-155">A group name for logically grouping files</span></span>        |
|<span data-ttu-id="1e3bf-156">Enter Path</span><span class="sxs-lookup"><span data-stu-id="1e3bf-156">Enter Path</span></span>     | <span data-ttu-id="1e3bf-157">The path to check for the file For example: "c:\temp\myfile.txt"</span><span class="sxs-lookup"><span data-stu-id="1e3bf-157">The path to check for the file For example: "c:\temp\myfile.txt"</span></span>

### <a name="linux-files"></a><span data-ttu-id="1e3bf-158">Linux Files</span><span class="sxs-lookup"><span data-stu-id="1e3bf-158">Linux Files</span></span>

|<span data-ttu-id="1e3bf-159">Property</span><span class="sxs-lookup"><span data-stu-id="1e3bf-159">Property</span></span>  |<span data-ttu-id="1e3bf-160">Description</span><span class="sxs-lookup"><span data-stu-id="1e3bf-160">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="1e3bf-161">Enabled</span><span class="sxs-lookup"><span data-stu-id="1e3bf-161">Enabled</span></span>     | <span data-ttu-id="1e3bf-162">Determines if the setting is applied</span><span class="sxs-lookup"><span data-stu-id="1e3bf-162">Determines if the setting is applied</span></span>        |
|<span data-ttu-id="1e3bf-163">Item Name</span><span class="sxs-lookup"><span data-stu-id="1e3bf-163">Item Name</span></span>     | <span data-ttu-id="1e3bf-164">Friendly name of the file to be tracked</span><span class="sxs-lookup"><span data-stu-id="1e3bf-164">Friendly name of the file to be tracked</span></span>        |
|<span data-ttu-id="1e3bf-165">Group</span><span class="sxs-lookup"><span data-stu-id="1e3bf-165">Group</span></span>     | <span data-ttu-id="1e3bf-166">A group name for logically grouping files</span><span class="sxs-lookup"><span data-stu-id="1e3bf-166">A group name for logically grouping files</span></span>        |
|<span data-ttu-id="1e3bf-167">Enter Path</span><span class="sxs-lookup"><span data-stu-id="1e3bf-167">Enter Path</span></span>     | <span data-ttu-id="1e3bf-168">The path to check for the file For example: "/etc/\*.conf"</span><span class="sxs-lookup"><span data-stu-id="1e3bf-168">The path to check for the file For example: "/etc/\*.conf"</span></span>       |
|<span data-ttu-id="1e3bf-169">Path Type</span><span class="sxs-lookup"><span data-stu-id="1e3bf-169">Path Type</span></span>     | <span data-ttu-id="1e3bf-170">Type of item to be tracked, possible values are File and Directory</span><span class="sxs-lookup"><span data-stu-id="1e3bf-170">Type of item to be tracked, possible values are File and Directory</span></span>        |
|<span data-ttu-id="1e3bf-171">Recursion</span><span class="sxs-lookup"><span data-stu-id="1e3bf-171">Recursion</span></span>     | <span data-ttu-id="1e3bf-172">Determines if recursion is used when looking for the item to be tracked.</span><span class="sxs-lookup"><span data-stu-id="1e3bf-172">Determines if recursion is used when looking for the item to be tracked.</span></span>        |
|<span data-ttu-id="1e3bf-173">Use Sudo</span><span class="sxs-lookup"><span data-stu-id="1e3bf-173">Use Sudo</span></span>     | <span data-ttu-id="1e3bf-174">This setting determines if sudo is used when checking for the item.</span><span class="sxs-lookup"><span data-stu-id="1e3bf-174">This setting determines if sudo is used when checking for the item.</span></span>         |
|<span data-ttu-id="1e3bf-175">Links</span><span class="sxs-lookup"><span data-stu-id="1e3bf-175">Links</span></span>     | <span data-ttu-id="1e3bf-176">This setting determines how symbolic links dealt with when traversing directories.</span><span class="sxs-lookup"><span data-stu-id="1e3bf-176">This setting determines how symbolic links dealt with when traversing directories.</span></span><br> <span data-ttu-id="1e3bf-177">**Ignore** - Ignores symbolic links and does not include the files/directories referenced</span><span class="sxs-lookup"><span data-stu-id="1e3bf-177">**Ignore** - Ignores symbolic links and does not include the files/directories referenced</span></span><br><span data-ttu-id="1e3bf-178">**Follow** - Follows the symbolic links during recursion and also includes the files/directories referenced</span><span class="sxs-lookup"><span data-stu-id="1e3bf-178">**Follow** - Follows the symbolic links during recursion and also includes the files/directories referenced</span></span><br><span data-ttu-id="1e3bf-179">**Manage** - Follows the symbolic links and allows alter the treatment of returned content</span><span class="sxs-lookup"><span data-stu-id="1e3bf-179">**Manage** - Follows the symbolic links and allows alter the treatment of returned content</span></span>      |

## <a name="manage-machine-groups"></a><span data-ttu-id="1e3bf-180">Manage machine groups</span><span class="sxs-lookup"><span data-stu-id="1e3bf-180">Manage machine groups</span></span>

<span data-ttu-id="1e3bf-181">Inventory allows you to create and view machine groups in Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="1e3bf-181">Inventory allows you to create and view machine groups in Log Analytics.</span></span> <span data-ttu-id="1e3bf-182">Machine groups are collections of machines defined by a query in Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="1e3bf-182">Machine groups are collections of machines defined by a query in Log Analytics.</span></span>

<span data-ttu-id="1e3bf-183">To view your machine groups select the **Machine groups** tab on the Inventory page.</span><span class="sxs-lookup"><span data-stu-id="1e3bf-183">To view your machine groups select the **Machine groups** tab on the Inventory page.</span></span>

![View machine groups on the inventory page](./media/automation-vm-inventory/inventory-machine-groups.png)

<span data-ttu-id="1e3bf-185">Selecting a machine group from the list opens the Machine groups page.</span><span class="sxs-lookup"><span data-stu-id="1e3bf-185">Selecting a machine group from the list opens the Machine groups page.</span></span> <span data-ttu-id="1e3bf-186">This page shows details about the machine group.</span><span class="sxs-lookup"><span data-stu-id="1e3bf-186">This page shows details about the machine group.</span></span> <span data-ttu-id="1e3bf-187">These details include the log analytics query that is used to define the group.</span><span class="sxs-lookup"><span data-stu-id="1e3bf-187">These details include the log analytics query that is used to define the group.</span></span> <span data-ttu-id="1e3bf-188">At the bottom of the page, is a paged list of the machines that are part of that group.</span><span class="sxs-lookup"><span data-stu-id="1e3bf-188">At the bottom of the page, is a paged list of the machines that are part of that group.</span></span>

![View machine group page](./media/automation-vm-inventory/machine-group-page.png)

<span data-ttu-id="1e3bf-190">Click the **+ Clone** button to clone the machine group.</span><span class="sxs-lookup"><span data-stu-id="1e3bf-190">Click the **+ Clone** button to clone the machine group.</span></span> <span data-ttu-id="1e3bf-191">Here you must give the group a new name and alias for the group.</span><span class="sxs-lookup"><span data-stu-id="1e3bf-191">Here you must give the group a new name and alias for the group.</span></span> <span data-ttu-id="1e3bf-192">The definition can be altered at this time.</span><span class="sxs-lookup"><span data-stu-id="1e3bf-192">The definition can be altered at this time.</span></span> <span data-ttu-id="1e3bf-193">After changing the query press **Validate query** to preview the machines that would be selected.</span><span class="sxs-lookup"><span data-stu-id="1e3bf-193">After changing the query press **Validate query** to preview the machines that would be selected.</span></span> <span data-ttu-id="1e3bf-194">When you are happy with the group click **Create** to create the machine group</span><span class="sxs-lookup"><span data-stu-id="1e3bf-194">When you are happy with the group click **Create** to create the machine group</span></span>

<span data-ttu-id="1e3bf-195">If you want to create a new mchine group, select **+ Create a machine group**.</span><span class="sxs-lookup"><span data-stu-id="1e3bf-195">If you want to create a new mchine group, select **+ Create a machine group**.</span></span> <span data-ttu-id="1e3bf-196">This button opens the **Create a machine group page** where you can define your new group.</span><span class="sxs-lookup"><span data-stu-id="1e3bf-196">This button opens the **Create a machine group page** where you can define your new group.</span></span> <span data-ttu-id="1e3bf-197">Click **Create** to create the group.</span><span class="sxs-lookup"><span data-stu-id="1e3bf-197">Click **Create** to create the group.</span></span>

![Create new machine group](./media/automation-vm-inventory/create-new-group.png)

## <a name="disconnect-your-virtual-machine-from-management"></a><span data-ttu-id="1e3bf-199">Disconnect your virtual machine from management</span><span class="sxs-lookup"><span data-stu-id="1e3bf-199">Disconnect your virtual machine from management</span></span>

<span data-ttu-id="1e3bf-200">To remove your virtual machine from inventory management:</span><span class="sxs-lookup"><span data-stu-id="1e3bf-200">To remove your virtual machine from inventory management:</span></span>

1. <span data-ttu-id="1e3bf-201">In the left pane of the Azure portal, select **Log Analytics**, and then select the workspace that you used when you onboarded your virtual machine.</span><span class="sxs-lookup"><span data-stu-id="1e3bf-201">In the left pane of the Azure portal, select **Log Analytics**, and then select the workspace that you used when you onboarded your virtual machine.</span></span>
2. <span data-ttu-id="1e3bf-202">In the **Log Analytics** window, on the **Resource** menu, under the **Workspace Data Sources** category, select **Virtual machines**.</span><span class="sxs-lookup"><span data-stu-id="1e3bf-202">In the **Log Analytics** window, on the **Resource** menu, under the **Workspace Data Sources** category, select **Virtual machines**.</span></span>
3. <span data-ttu-id="1e3bf-203">In the list, select the virtual machine that you want to disconnect.</span><span class="sxs-lookup"><span data-stu-id="1e3bf-203">In the list, select the virtual machine that you want to disconnect.</span></span> <span data-ttu-id="1e3bf-204">The virtual machine has a green check mark next to **This workspace** in the **OMS Connection** column.</span><span class="sxs-lookup"><span data-stu-id="1e3bf-204">The virtual machine has a green check mark next to **This workspace** in the **OMS Connection** column.</span></span>
4. <span data-ttu-id="1e3bf-205">At the top of the next page, select **Disconnect**.</span><span class="sxs-lookup"><span data-stu-id="1e3bf-205">At the top of the next page, select **Disconnect**.</span></span>
5. <span data-ttu-id="1e3bf-206">In the confirmation window, select **Yes**.</span><span class="sxs-lookup"><span data-stu-id="1e3bf-206">In the confirmation window, select **Yes**.</span></span>
    <span data-ttu-id="1e3bf-207">This action disconnects the machine from management.</span><span class="sxs-lookup"><span data-stu-id="1e3bf-207">This action disconnects the machine from management.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1e3bf-208">Next steps</span><span class="sxs-lookup"><span data-stu-id="1e3bf-208">Next steps</span></span>

* <span data-ttu-id="1e3bf-209">To learn about managing changes in files and registry settings on your virtual machines, see [Track software changes in your environment with the Change Tracking solution](../log-analytics/log-analytics-change-tracking.md).</span><span class="sxs-lookup"><span data-stu-id="1e3bf-209">To learn about managing changes in files and registry settings on your virtual machines, see [Track software changes in your environment with the Change Tracking solution](../log-analytics/log-analytics-change-tracking.md).</span></span>
* <span data-ttu-id="1e3bf-210">To learn about managing Windows and package updates on your virtual machines, see [The Update Management solution in Azure](../operations-management-suite/oms-solution-update-management.md).</span><span class="sxs-lookup"><span data-stu-id="1e3bf-210">To learn about managing Windows and package updates on your virtual machines, see [The Update Management solution in Azure](../operations-management-suite/oms-solution-update-management.md).</span></span>
