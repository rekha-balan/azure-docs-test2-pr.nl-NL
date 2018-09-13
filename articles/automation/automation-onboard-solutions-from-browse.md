---
title: Learn how to onboard Update Management, Change Tracking, and Inventory solutions for multiple VMs in Azure Automation
description: Learn how to onboard an Azure Virtual machine with Update Management, Change Tracking, and Inventory solutions that are part of Azure Automation
services: automation
ms.service: automation
author: georgewallace
ms.author: gwallace
ms.date: 06/06/2018
ms.topic: article
manager: carmonm
ms.custom: mvc
ms.openlocfilehash: 0a624d850b8c3260acb24cb17566090e8ad0043e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966996"
---
# <a name="enable-update-management-change-tracking-and-inventory-solutions-on-multiple-vms"></a><span data-ttu-id="ce633-103">Enable Update Management, Change Tracking, and Inventory solutions on multiple VMs</span><span class="sxs-lookup"><span data-stu-id="ce633-103">Enable Update Management, Change Tracking, and Inventory solutions on multiple VMs</span></span>

<span data-ttu-id="ce633-104">Azure Automation provides solutions to manage operating system security updates, track changes, and inventory what is installed on your computers.</span><span class="sxs-lookup"><span data-stu-id="ce633-104">Azure Automation provides solutions to manage operating system security updates, track changes, and inventory what is installed on your computers.</span></span> <span data-ttu-id="ce633-105">There are multiple ways to onboard machines, you can onboard the solution [from a virtual machine](automation-onboard-solutions-from-vm.md), from your [Automation account](automation-onboard-solutions-from-automation-account.md), when browsing virtual machines, or by [runbook](automation-onboard-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="ce633-105">There are multiple ways to onboard machines, you can onboard the solution [from a virtual machine](automation-onboard-solutions-from-vm.md), from your [Automation account](automation-onboard-solutions-from-automation-account.md), when browsing virtual machines, or by [runbook](automation-onboard-solutions.md).</span></span> <span data-ttu-id="ce633-106">This article covers onboarding these solutions when browsing virtual machines in Azure.</span><span class="sxs-lookup"><span data-stu-id="ce633-106">This article covers onboarding these solutions when browsing virtual machines in Azure.</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="ce633-107">Log in to Azure</span><span class="sxs-lookup"><span data-stu-id="ce633-107">Log in to Azure</span></span>

<span data-ttu-id="ce633-108">Log in to Azure at https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="ce633-108">Log in to Azure at https://portal.azure.com</span></span>

## <a name="enable-solutions"></a><span data-ttu-id="ce633-109">Enable solutions</span><span class="sxs-lookup"><span data-stu-id="ce633-109">Enable solutions</span></span>

<span data-ttu-id="ce633-110">In the Azure portal, navigate to **Virtual machines**.</span><span class="sxs-lookup"><span data-stu-id="ce633-110">In the Azure portal, navigate to **Virtual machines**.</span></span>

<span data-ttu-id="ce633-111">Using the checkboxes, select the virtual machines you wish to onboard with Change Tracking and Inventory or Update Management.</span><span class="sxs-lookup"><span data-stu-id="ce633-111">Using the checkboxes, select the virtual machines you wish to onboard with Change Tracking and Inventory or Update Management.</span></span> <span data-ttu-id="ce633-112">Onboarding is available for up to three different resource groups at a time.</span><span class="sxs-lookup"><span data-stu-id="ce633-112">Onboarding is available for up to three different resource groups at a time.</span></span>

![List of VMs](media/automation-onboard-solutions-from-browse/vmlist.png)
> [!TIP]
> <span data-ttu-id="ce633-114">Use the filter controls to modify the list of virtual machines and then click the top checkbox to select all virtual machines in the list.</span><span class="sxs-lookup"><span data-stu-id="ce633-114">Use the filter controls to modify the list of virtual machines and then click the top checkbox to select all virtual machines in the list.</span></span>

<span data-ttu-id="ce633-115">From the command bar, click **Services** and select either **Change tracking**, **Inventory**, or **Update Management**.</span><span class="sxs-lookup"><span data-stu-id="ce633-115">From the command bar, click **Services** and select either **Change tracking**, **Inventory**, or **Update Management**.</span></span>

> [!NOTE]
> <span data-ttu-id="ce633-116">**Change tracking** and **Inventory** use the same solution, when one is enabled the other is enabled as well.</span><span class="sxs-lookup"><span data-stu-id="ce633-116">**Change tracking** and **Inventory** use the same solution, when one is enabled the other is enabled as well.</span></span>

<span data-ttu-id="ce633-117">The following image is for Update Management.</span><span class="sxs-lookup"><span data-stu-id="ce633-117">The following image is for Update Management.</span></span> <span data-ttu-id="ce633-118">Change tracking and Inventory have the same layout and behavior.</span><span class="sxs-lookup"><span data-stu-id="ce633-118">Change tracking and Inventory have the same layout and behavior.</span></span>

<span data-ttu-id="ce633-119">The list of virtual machines is filtered to show only the virtual machines that are in the same subscription and location.</span><span class="sxs-lookup"><span data-stu-id="ce633-119">The list of virtual machines is filtered to show only the virtual machines that are in the same subscription and location.</span></span> <span data-ttu-id="ce633-120">If your virtual machines are in more than three resource groups, the first three resource groups are selected.</span><span class="sxs-lookup"><span data-stu-id="ce633-120">If your virtual machines are in more than three resource groups, the first three resource groups are selected.</span></span>

<span data-ttu-id="ce633-121">Use the filter controls to select virtual machines from different subscriptions, locations, and resource groups.</span><span class="sxs-lookup"><span data-stu-id="ce633-121">Use the filter controls to select virtual machines from different subscriptions, locations, and resource groups.</span></span>

![Onboard Update management solution](media/automation-onboard-solutions-from-browse/onboardsolutions.png)

<span data-ttu-id="ce633-123">Review the choices for the Log analytics workspace and Automation account.</span><span class="sxs-lookup"><span data-stu-id="ce633-123">Review the choices for the Log analytics workspace and Automation account.</span></span> <span data-ttu-id="ce633-124">A new workspace and Automation Account are selected by default.</span><span class="sxs-lookup"><span data-stu-id="ce633-124">A new workspace and Automation Account are selected by default.</span></span> <span data-ttu-id="ce633-125">If you have an existing Log Analytics workspace and Automation Account you want to use, click **change** to select them from the **Configuration** page.</span><span class="sxs-lookup"><span data-stu-id="ce633-125">If you have an existing Log Analytics workspace and Automation Account you want to use, click **change** to select them from the **Configuration** page.</span></span> <span data-ttu-id="ce633-126">When done, click **Save**.</span><span class="sxs-lookup"><span data-stu-id="ce633-126">When done, click **Save**.</span></span>

![Select workspace and account](media/automation-onboard-solutions-from-browse/selectworkspaceandaccount.png)

<span data-ttu-id="ce633-128">Deselect the checkbox next to any virtual machine that you don't want to enable.</span><span class="sxs-lookup"><span data-stu-id="ce633-128">Deselect the checkbox next to any virtual machine that you don't want to enable.</span></span> <span data-ttu-id="ce633-129">Virtual machines that can't be enabled are already deselected.</span><span class="sxs-lookup"><span data-stu-id="ce633-129">Virtual machines that can't be enabled are already deselected.</span></span>

<span data-ttu-id="ce633-130">Click **Enable** to enable the solution.</span><span class="sxs-lookup"><span data-stu-id="ce633-130">Click **Enable** to enable the solution.</span></span> <span data-ttu-id="ce633-131">The solution takes up to 15 minutes to enable.</span><span class="sxs-lookup"><span data-stu-id="ce633-131">The solution takes up to 15 minutes to enable.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="ce633-132">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="ce633-132">Troubleshooting</span></span>

<span data-ttu-id="ce633-133">When onboarding multiple machines, there may be machines that show as **Cannot enable**.</span><span class="sxs-lookup"><span data-stu-id="ce633-133">When onboarding multiple machines, there may be machines that show as **Cannot enable**.</span></span> <span data-ttu-id="ce633-134">There are different reasons why some machines may not be enabled.</span><span class="sxs-lookup"><span data-stu-id="ce633-134">There are different reasons why some machines may not be enabled.</span></span> <span data-ttu-id="ce633-135">The following sections show possible reasons for the **Cannot enable** state on a VM when attempting to onboard.</span><span class="sxs-lookup"><span data-stu-id="ce633-135">The following sections show possible reasons for the **Cannot enable** state on a VM when attempting to onboard.</span></span>

### <a name="vm-reports-to-a-different-workspace-workspacename--change-configuration-to-use-it-for-enabling"></a><span data-ttu-id="ce633-136">VM reports to a different workspace: '\<workspaceName\>'.</span><span class="sxs-lookup"><span data-stu-id="ce633-136">VM reports to a different workspace: '\<workspaceName\>'.</span></span>  <span data-ttu-id="ce633-137">Change configuration to use it for enabling</span><span class="sxs-lookup"><span data-stu-id="ce633-137">Change configuration to use it for enabling</span></span>

<span data-ttu-id="ce633-138">**Cause**: This error shows that the VM that you are trying to onboard reports to another workspace.</span><span class="sxs-lookup"><span data-stu-id="ce633-138">**Cause**: This error shows that the VM that you are trying to onboard reports to another workspace.</span></span>

<span data-ttu-id="ce633-139">**Solution**: Click **Use as configuration** to change the targeted Automation Account and Log Analytics workspace.</span><span class="sxs-lookup"><span data-stu-id="ce633-139">**Solution**: Click **Use as configuration** to change the targeted Automation Account and Log Analytics workspace.</span></span>

### <a name="vm-reports-to-a-workspace-that-is-not-available-in-this-subscription"></a><span data-ttu-id="ce633-140">VM reports to a workspace that is not available in this subscription</span><span class="sxs-lookup"><span data-stu-id="ce633-140">VM reports to a workspace that is not available in this subscription</span></span>

<span data-ttu-id="ce633-141">**Cause**: The workspace that the virtual machine reports to:</span><span class="sxs-lookup"><span data-stu-id="ce633-141">**Cause**: The workspace that the virtual machine reports to:</span></span>

* <span data-ttu-id="ce633-142">Is in a different subscription, or</span><span class="sxs-lookup"><span data-stu-id="ce633-142">Is in a different subscription, or</span></span>
* <span data-ttu-id="ce633-143">No longer exists, or</span><span class="sxs-lookup"><span data-stu-id="ce633-143">No longer exists, or</span></span>
* <span data-ttu-id="ce633-144">Is in a resource group you don't have access permissions to</span><span class="sxs-lookup"><span data-stu-id="ce633-144">Is in a resource group you don't have access permissions to</span></span>

<span data-ttu-id="ce633-145">**Solution**: Find the automation account associated with the workspace that the VM reports to and onboard the virtual machine by changing the scope configuration.</span><span class="sxs-lookup"><span data-stu-id="ce633-145">**Solution**: Find the automation account associated with the workspace that the VM reports to and onboard the virtual machine by changing the scope configuration.</span></span>

### <a name="vm-operating-system-version-or-distribution-is-not-supported"></a><span data-ttu-id="ce633-146">VM operating system version or distribution is not supported</span><span class="sxs-lookup"><span data-stu-id="ce633-146">VM operating system version or distribution is not supported</span></span>

<span data-ttu-id="ce633-147">**Cause:** The solution is not supported for all Linux distributions or all versions of Windows.</span><span class="sxs-lookup"><span data-stu-id="ce633-147">**Cause:** The solution is not supported for all Linux distributions or all versions of Windows.</span></span>

<span data-ttu-id="ce633-148">**Solution:** Refer to the [list of supported clients](automation-update-management.md#clients) for the solution.</span><span class="sxs-lookup"><span data-stu-id="ce633-148">**Solution:** Refer to the [list of supported clients](automation-update-management.md#clients) for the solution.</span></span>

### <a name="classic-vms-cannot-be-enabled"></a><span data-ttu-id="ce633-149">Classic VMs cannot be enabled</span><span class="sxs-lookup"><span data-stu-id="ce633-149">Classic VMs cannot be enabled</span></span>

<span data-ttu-id="ce633-150">**Cause**: Virtual machines that use the classic deployment model are not supported.</span><span class="sxs-lookup"><span data-stu-id="ce633-150">**Cause**: Virtual machines that use the classic deployment model are not supported.</span></span>

<span data-ttu-id="ce633-151">**Solution**: Migrate the virtual machine to the resource manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="ce633-151">**Solution**: Migrate the virtual machine to the resource manager deployment model.</span></span> <span data-ttu-id="ce633-152">To learn how to do this, see [Migrate classic deployment model resources](../virtual-machines/windows/migration-classic-resource-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ce633-152">To learn how to do this, see [Migrate classic deployment model resources](../virtual-machines/windows/migration-classic-resource-manager-overview.md).</span></span>

### <a name="vm-is-stopped-deallocated"></a><span data-ttu-id="ce633-153">VM is stopped.</span><span class="sxs-lookup"><span data-stu-id="ce633-153">VM is stopped.</span></span> <span data-ttu-id="ce633-154">(deallocated)</span><span class="sxs-lookup"><span data-stu-id="ce633-154">(deallocated)</span></span>

<span data-ttu-id="ce633-155">**Cause**: The virtual machine in not in a **Running** state.</span><span class="sxs-lookup"><span data-stu-id="ce633-155">**Cause**: The virtual machine in not in a **Running** state.</span></span>

<span data-ttu-id="ce633-156">**Solution**: In order to onboard a VM to a solution the VM must be running.</span><span class="sxs-lookup"><span data-stu-id="ce633-156">**Solution**: In order to onboard a VM to a solution the VM must be running.</span></span> <span data-ttu-id="ce633-157">Click the **Start VM** inline link to start the VM without navigating away from the page.</span><span class="sxs-lookup"><span data-stu-id="ce633-157">Click the **Start VM** inline link to start the VM without navigating away from the page.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ce633-158">Next steps</span><span class="sxs-lookup"><span data-stu-id="ce633-158">Next steps</span></span>

<span data-ttu-id="ce633-159">Now that the solution is enabled for your virtual machines, visit the Update Management overview article to learn how to view the update assessment for your machines.</span><span class="sxs-lookup"><span data-stu-id="ce633-159">Now that the solution is enabled for your virtual machines, visit the Update Management overview article to learn how to view the update assessment for your machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ce633-160">Update Management - View update assessment</span><span class="sxs-lookup"><span data-stu-id="ce633-160">Update Management - View update assessment</span></span>](./automation-update-management.md#viewing-update-assessments)

<span data-ttu-id="ce633-161">Addition tutorials on the solutions and how to use them:</span><span class="sxs-lookup"><span data-stu-id="ce633-161">Addition tutorials on the solutions and how to use them:</span></span>

* [<span data-ttu-id="ce633-162">Tutorial - Manage Updates for your VM</span><span class="sxs-lookup"><span data-stu-id="ce633-162">Tutorial - Manage Updates for your VM</span></span>](automation-tutorial-update-management.md)

* [<span data-ttu-id="ce633-163">Tutorial - Identify software on a VM</span><span class="sxs-lookup"><span data-stu-id="ce633-163">Tutorial - Identify software on a VM</span></span>](automation-tutorial-installed-software.md)

* [<span data-ttu-id="ce633-164">Tutorial - Troubleshoot changes on a VM</span><span class="sxs-lookup"><span data-stu-id="ce633-164">Tutorial - Troubleshoot changes on a VM</span></span>](automation-tutorial-troubleshoot-changes.md)