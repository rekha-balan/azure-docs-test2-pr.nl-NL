---
title: Onboard update and change tracking solutions to Azure Automation
description: Learn how to onboard update and change tracking solutions to Azure Automation.
services: automation
ms.service: automation
author: eamonoreilly
ms.author: eamono
manager: carmonm
ms.topic: tutorial
ms.date: 05/10/2018
ms.custom: mvc
ms.openlocfilehash: 5cf09753645d8238232e064af2ba1a301a2a7217
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867450"
---
# <a name="onboard-update-and-change-tracking-solutions-to-azure-automation"></a><span data-ttu-id="98eb0-103">Onboard update and change tracking solutions to Azure Automation</span><span class="sxs-lookup"><span data-stu-id="98eb0-103">Onboard update and change tracking solutions to Azure Automation</span></span>

<span data-ttu-id="98eb0-104">In this tutorial, you learn how to automatically onboard Update, Change Tracking, and Inventory solutions for VMs to Azure Automation:</span><span class="sxs-lookup"><span data-stu-id="98eb0-104">In this tutorial, you learn how to automatically onboard Update, Change Tracking, and Inventory solutions for VMs to Azure Automation:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="98eb0-105">Onboard an Azure VM</span><span class="sxs-lookup"><span data-stu-id="98eb0-105">Onboard an Azure VM</span></span>
> * <span data-ttu-id="98eb0-106">Enable solutions</span><span class="sxs-lookup"><span data-stu-id="98eb0-106">Enable solutions</span></span>
> * <span data-ttu-id="98eb0-107">Install and update modules</span><span class="sxs-lookup"><span data-stu-id="98eb0-107">Install and update modules</span></span>
> * <span data-ttu-id="98eb0-108">Import the onboarding runbook</span><span class="sxs-lookup"><span data-stu-id="98eb0-108">Import the onboarding runbook</span></span>
> * <span data-ttu-id="98eb0-109">Start the runbook</span><span class="sxs-lookup"><span data-stu-id="98eb0-109">Start the runbook</span></span>

## <a name="prerequisites"></a><span data-ttu-id="98eb0-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="98eb0-110">Prerequisites</span></span>

<span data-ttu-id="98eb0-111">To complete this tutorial, the following are required:</span><span class="sxs-lookup"><span data-stu-id="98eb0-111">To complete this tutorial, the following are required:</span></span>

* <span data-ttu-id="98eb0-112">Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="98eb0-112">Azure subscription.</span></span> <span data-ttu-id="98eb0-113">If you don't have one yet, you can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="98eb0-113">If you don't have one yet, you can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).</span></span>
* <span data-ttu-id="98eb0-114">[Automation account](automation-offering-get-started.md) to manage machines.</span><span class="sxs-lookup"><span data-stu-id="98eb0-114">[Automation account](automation-offering-get-started.md) to manage machines.</span></span>
* <span data-ttu-id="98eb0-115">A [virtual machine](../virtual-machines/windows/quick-create-portal.md) to onboard.</span><span class="sxs-lookup"><span data-stu-id="98eb0-115">A [virtual machine](../virtual-machines/windows/quick-create-portal.md) to onboard.</span></span>

## <a name="onboard-an-azure-vm"></a><span data-ttu-id="98eb0-116">Onboard an Azure VM</span><span class="sxs-lookup"><span data-stu-id="98eb0-116">Onboard an Azure VM</span></span>

<span data-ttu-id="98eb0-117">There are multiple ways to onboard machines, you can onboard the solution [from a virtual machine](automation-onboard-solutions-from-vm.md), [from browsing multiple machines](automation-onboard-solutions-from-browse.md) [from your Automation account](automation-onboard-solutions-from-automation-account.md),  or by runbook.</span><span class="sxs-lookup"><span data-stu-id="98eb0-117">There are multiple ways to onboard machines, you can onboard the solution [from a virtual machine](automation-onboard-solutions-from-vm.md), [from browsing multiple machines](automation-onboard-solutions-from-browse.md) [from your Automation account](automation-onboard-solutions-from-automation-account.md),  or by runbook.</span></span> <span data-ttu-id="98eb0-118">This tutorial walks through enabling Update Management through a runbook.</span><span class="sxs-lookup"><span data-stu-id="98eb0-118">This tutorial walks through enabling Update Management through a runbook.</span></span> <span data-ttu-id="98eb0-119">To onboard Azure Virtual Machines at scale, an existing VM must be onboarded with the Change tracking or Update management solution.</span><span class="sxs-lookup"><span data-stu-id="98eb0-119">To onboard Azure Virtual Machines at scale, an existing VM must be onboarded with the Change tracking or Update management solution.</span></span> <span data-ttu-id="98eb0-120">In this step, you onboard a virtual machine with Update management, and Change tracking.</span><span class="sxs-lookup"><span data-stu-id="98eb0-120">In this step, you onboard a virtual machine with Update management, and Change tracking.</span></span>

### <a name="enable-change-tracking-and-inventory"></a><span data-ttu-id="98eb0-121">Enable Change Tracking and Inventory</span><span class="sxs-lookup"><span data-stu-id="98eb0-121">Enable Change Tracking and Inventory</span></span>

<span data-ttu-id="98eb0-122">The Change Tracking and Inventory solution provides the ability to [track changes](automation-vm-change-tracking.md) and [inventory](automation-vm-inventory.md) on your virtual machines.</span><span class="sxs-lookup"><span data-stu-id="98eb0-122">The Change Tracking and Inventory solution provides the ability to [track changes](automation-vm-change-tracking.md) and [inventory](automation-vm-inventory.md) on your virtual machines.</span></span> <span data-ttu-id="98eb0-123">In this step, you enable the solution on a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="98eb0-123">In this step, you enable the solution on a virtual machine.</span></span>

1. <span data-ttu-id="98eb0-124">From the left menu, select **Automation Accounts**, and then select your automation account in the list.</span><span class="sxs-lookup"><span data-stu-id="98eb0-124">From the left menu, select **Automation Accounts**, and then select your automation account in the list.</span></span>
1. <span data-ttu-id="98eb0-125">Select **Inventory** under **CONFIGURATION MANAGEMENT**.</span><span class="sxs-lookup"><span data-stu-id="98eb0-125">Select **Inventory** under **CONFIGURATION MANAGEMENT**.</span></span>
1. <span data-ttu-id="98eb0-126">Select an existing Log Analytics workspace or create new.</span><span class="sxs-lookup"><span data-stu-id="98eb0-126">Select an existing Log Analytics workspace or create new.</span></span> <span data-ttu-id="98eb0-127">Click the **Enable** button.</span><span class="sxs-lookup"><span data-stu-id="98eb0-127">Click the **Enable** button.</span></span>

![Onboard Update solution](media/automation-onboard-solutions/inventory-onboard.png)

<span data-ttu-id="98eb0-129">When the change tracking and inventory solution onboarding notification completes, click on **Update Management** under **CONFIGURATION MANAGEMENT**.</span><span class="sxs-lookup"><span data-stu-id="98eb0-129">When the change tracking and inventory solution onboarding notification completes, click on **Update Management** under **CONFIGURATION MANAGEMENT**.</span></span>

### <a name="enable-update-management"></a><span data-ttu-id="98eb0-130">Enable Update Management</span><span class="sxs-lookup"><span data-stu-id="98eb0-130">Enable Update Management</span></span>

<span data-ttu-id="98eb0-131">The Update Management solution allows you to manage updates and patches for your Azure Windows VMs.</span><span class="sxs-lookup"><span data-stu-id="98eb0-131">The Update Management solution allows you to manage updates and patches for your Azure Windows VMs.</span></span> <span data-ttu-id="98eb0-132">You can assess the status of available updates, schedule installation of required updates, and review deployment results to verify updates were applied successfully to the VM.</span><span class="sxs-lookup"><span data-stu-id="98eb0-132">You can assess the status of available updates, schedule installation of required updates, and review deployment results to verify updates were applied successfully to the VM.</span></span> <span data-ttu-id="98eb0-133">In this step, you enable the solution for your VM.</span><span class="sxs-lookup"><span data-stu-id="98eb0-133">In this step, you enable the solution for your VM.</span></span>

1. <span data-ttu-id="98eb0-134">From your Automation Account, select **Update management** under **UPDATE MANAGEMENT**.</span><span class="sxs-lookup"><span data-stu-id="98eb0-134">From your Automation Account, select **Update management** under **UPDATE MANAGEMENT**.</span></span>
1. <span data-ttu-id="98eb0-135">The Log analytics workspace selected is the same workspace used in the preceding step.</span><span class="sxs-lookup"><span data-stu-id="98eb0-135">The Log analytics workspace selected is the same workspace used in the preceding step.</span></span> <span data-ttu-id="98eb0-136">Click **Enable** to onboard the Update management solution.</span><span class="sxs-lookup"><span data-stu-id="98eb0-136">Click **Enable** to onboard the Update management solution.</span></span>

![Onboard Update solution](media/automation-onboard-solutions/update-onboard.png)

<span data-ttu-id="98eb0-138">While the Update management solution is being installed, a blue banner is shown.</span><span class="sxs-lookup"><span data-stu-id="98eb0-138">While the Update management solution is being installed, a blue banner is shown.</span></span> <span data-ttu-id="98eb0-139">When the solution is enabled select **Change tracking** under **CONFIGURATION MANAGEMENT** to go to the next step.</span><span class="sxs-lookup"><span data-stu-id="98eb0-139">When the solution is enabled select **Change tracking** under **CONFIGURATION MANAGEMENT** to go to the next step.</span></span>

### <a name="select-azure-vm-to-be-managed"></a><span data-ttu-id="98eb0-140">Select Azure VM to be managed</span><span class="sxs-lookup"><span data-stu-id="98eb0-140">Select Azure VM to be managed</span></span>

<span data-ttu-id="98eb0-141">Now that the solutions are enabled, you can add an Azure VM to onboard to those solutions.</span><span class="sxs-lookup"><span data-stu-id="98eb0-141">Now that the solutions are enabled, you can add an Azure VM to onboard to those solutions.</span></span>

1. <span data-ttu-id="98eb0-142">From your Automation Account, on the **Change tracking** page, select **+ Add Azure VM** to add your virtual machine.</span><span class="sxs-lookup"><span data-stu-id="98eb0-142">From your Automation Account, on the **Change tracking** page, select **+ Add Azure VM** to add your virtual machine.</span></span>

1. <span data-ttu-id="98eb0-143">Select your VM from the list and select **Enable**.</span><span class="sxs-lookup"><span data-stu-id="98eb0-143">Select your VM from the list and select **Enable**.</span></span> <span data-ttu-id="98eb0-144">This action enables the Change tacking and Inventory solution for the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="98eb0-144">This action enables the Change tacking and Inventory solution for the virtual machine.</span></span>

   ![Enable update solution for vm](media/automation-onboard-solutions/enable-change-tracking.png)

1. <span data-ttu-id="98eb0-146">When the VM onboarding notification completes, from your Automation Account select **Update management** under **UPDATE MANAGEMENT**.</span><span class="sxs-lookup"><span data-stu-id="98eb0-146">When the VM onboarding notification completes, from your Automation Account select **Update management** under **UPDATE MANAGEMENT**.</span></span>

1. <span data-ttu-id="98eb0-147">Select **+ Add Azure VM** to add your virtual machine.</span><span class="sxs-lookup"><span data-stu-id="98eb0-147">Select **+ Add Azure VM** to add your virtual machine.</span></span>

1. <span data-ttu-id="98eb0-148">Select your VM from the list and select **Enable**.</span><span class="sxs-lookup"><span data-stu-id="98eb0-148">Select your VM from the list and select **Enable**.</span></span> <span data-ttu-id="98eb0-149">This action enables the Update management solution for the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="98eb0-149">This action enables the Update management solution for the virtual machine.</span></span>

   ![Enable update solution for vm](media/automation-onboard-solutions/enable-update.png)

> [!NOTE]
> <span data-ttu-id="98eb0-151">If you do not wait for the other solution to complete, when Enabling the next solution you receive a message stating: *Installation of another solution is in progress on this or a different virtual machine. When that installation completes the Enable button is enabled, and you can request installation of the solution on this virtual machine.*</span><span class="sxs-lookup"><span data-stu-id="98eb0-151">If you do not wait for the other solution to complete, when Enabling the next solution you receive a message stating: *Installation of another solution is in progress on this or a different virtual machine. When that installation completes the Enable button is enabled, and you can request installation of the solution on this virtual machine.*</span></span>

## <a name="install-and-update-modules"></a><span data-ttu-id="98eb0-152">Install and update modules</span><span class="sxs-lookup"><span data-stu-id="98eb0-152">Install and update modules</span></span>

<span data-ttu-id="98eb0-153">It is required to update to the latest Azure modules and import `AzureRM.OperationalInsights` to successfully automate solution onboarding.</span><span class="sxs-lookup"><span data-stu-id="98eb0-153">It is required to update to the latest Azure modules and import `AzureRM.OperationalInsights` to successfully automate solution onboarding.</span></span>

## <a name="update-azure-modules"></a><span data-ttu-id="98eb0-154">Update Azure Modules</span><span class="sxs-lookup"><span data-stu-id="98eb0-154">Update Azure Modules</span></span>

<span data-ttu-id="98eb0-155">From your Automation Account, select **Modules** under **SHARED RESOURCES**.</span><span class="sxs-lookup"><span data-stu-id="98eb0-155">From your Automation Account, select **Modules** under **SHARED RESOURCES**.</span></span> <span data-ttu-id="98eb0-156">Select **Update Azure Modules** to update the Azure modules to the latest version.</span><span class="sxs-lookup"><span data-stu-id="98eb0-156">Select **Update Azure Modules** to update the Azure modules to the latest version.</span></span> <span data-ttu-id="98eb0-157">Select **Yes** on the prompt to update all existing Azure modules to the latest version.</span><span class="sxs-lookup"><span data-stu-id="98eb0-157">Select **Yes** on the prompt to update all existing Azure modules to the latest version.</span></span>

![Update modules](media/automation-onboard-solutions/update-modules.png)

### <a name="install-azurermoperationalinsights-module"></a><span data-ttu-id="98eb0-159">Install AzureRM.OperationalInsights module</span><span class="sxs-lookup"><span data-stu-id="98eb0-159">Install AzureRM.OperationalInsights module</span></span>

<span data-ttu-id="98eb0-160">From the **Modules** page, select **Browse gallery** to open up the module gallery.</span><span class="sxs-lookup"><span data-stu-id="98eb0-160">From the **Modules** page, select **Browse gallery** to open up the module gallery.</span></span> <span data-ttu-id="98eb0-161">Search for AzureRM.OperationalInsights and import this module into the Automation account.</span><span class="sxs-lookup"><span data-stu-id="98eb0-161">Search for AzureRM.OperationalInsights and import this module into the Automation account.</span></span>

![Import OperationalInsights module](media/automation-onboard-solutions/import-operational-insights-module.png)

## <a name="import-the-onboarding-runbook"></a><span data-ttu-id="98eb0-163">Import the onboarding runbook</span><span class="sxs-lookup"><span data-stu-id="98eb0-163">Import the onboarding runbook</span></span>

1. <span data-ttu-id="98eb0-164">From your Automation Account, select on **Runbooks** under the **PROCESS AUTOMATION**.</span><span class="sxs-lookup"><span data-stu-id="98eb0-164">From your Automation Account, select on **Runbooks** under the **PROCESS AUTOMATION**.</span></span>
1. <span data-ttu-id="98eb0-165">Select **Browse gallery**.</span><span class="sxs-lookup"><span data-stu-id="98eb0-165">Select **Browse gallery**.</span></span>
1. <span data-ttu-id="98eb0-166">Search for **update and change tracking**, click the runbook and select **Import** on the **View Source** page.</span><span class="sxs-lookup"><span data-stu-id="98eb0-166">Search for **update and change tracking**, click the runbook and select **Import** on the **View Source** page.</span></span> <span data-ttu-id="98eb0-167">Select **OK** to import the runbook into the Automation account.</span><span class="sxs-lookup"><span data-stu-id="98eb0-167">Select **OK** to import the runbook into the Automation account.</span></span>

  ![Import onboarding runbook](media/automation-onboard-solutions/import-from-gallery.png)

1. <span data-ttu-id="98eb0-169">On the **Runbook** page, select **Edit**, then select **Publish**.</span><span class="sxs-lookup"><span data-stu-id="98eb0-169">On the **Runbook** page, select **Edit**, then select **Publish**.</span></span> <span data-ttu-id="98eb0-170">On the **Publish Runbook** dialog, select **Yes** to publish the runbook.</span><span class="sxs-lookup"><span data-stu-id="98eb0-170">On the **Publish Runbook** dialog, select **Yes** to publish the runbook.</span></span>

## <a name="start-the-runbook"></a><span data-ttu-id="98eb0-171">Start the runbook</span><span class="sxs-lookup"><span data-stu-id="98eb0-171">Start the runbook</span></span>

<span data-ttu-id="98eb0-172">You must have onboarded either change tracking or update solutions to an Azure VM in order to start this runbook.</span><span class="sxs-lookup"><span data-stu-id="98eb0-172">You must have onboarded either change tracking or update solutions to an Azure VM in order to start this runbook.</span></span> <span data-ttu-id="98eb0-173">It requires an existing virtual machine and resource group with the solution onboarded for parameters.</span><span class="sxs-lookup"><span data-stu-id="98eb0-173">It requires an existing virtual machine and resource group with the solution onboarded for parameters.</span></span>

1. <span data-ttu-id="98eb0-174">Open the Enable-MultipleSolution runbook.</span><span class="sxs-lookup"><span data-stu-id="98eb0-174">Open the Enable-MultipleSolution runbook.</span></span>

   ![Multiple solution runbooks](media/automation-onboard-solutions/runbook-overview.png)

1. <span data-ttu-id="98eb0-176">Click the start button and enter the following values for parameters.</span><span class="sxs-lookup"><span data-stu-id="98eb0-176">Click the start button and enter the following values for parameters.</span></span>

   * <span data-ttu-id="98eb0-177">**VMNAME** - Leave blank.</span><span class="sxs-lookup"><span data-stu-id="98eb0-177">**VMNAME** - Leave blank.</span></span> <span data-ttu-id="98eb0-178">The name of an existing VM to onboard to update or change tracking solution.</span><span class="sxs-lookup"><span data-stu-id="98eb0-178">The name of an existing VM to onboard to update or change tracking solution.</span></span> <span data-ttu-id="98eb0-179">By leaving this value blank, all VMs in the resource group are onboarded.</span><span class="sxs-lookup"><span data-stu-id="98eb0-179">By leaving this value blank, all VMs in the resource group are onboarded.</span></span>
   * <span data-ttu-id="98eb0-180">**VMRESOURCEGROUP** - The name of the resource group for the VMs to be onboarded.</span><span class="sxs-lookup"><span data-stu-id="98eb0-180">**VMRESOURCEGROUP** - The name of the resource group for the VMs to be onboarded.</span></span>
   * <span data-ttu-id="98eb0-181">**SUBSCRIPTIONID** - Leave blank.</span><span class="sxs-lookup"><span data-stu-id="98eb0-181">**SUBSCRIPTIONID** - Leave blank.</span></span> <span data-ttu-id="98eb0-182">The subscription ID of the new VM to be onboarded.</span><span class="sxs-lookup"><span data-stu-id="98eb0-182">The subscription ID of the new VM to be onboarded.</span></span> <span data-ttu-id="98eb0-183">If left blank, the subscription of the workspace is used.</span><span class="sxs-lookup"><span data-stu-id="98eb0-183">If left blank, the subscription of the workspace is used.</span></span> <span data-ttu-id="98eb0-184">When a different subscription ID is given, the RunAs account for this automation account should be added as a contributor for this subscription also.</span><span class="sxs-lookup"><span data-stu-id="98eb0-184">When a different subscription ID is given, the RunAs account for this automation account should be added as a contributor for this subscription also.</span></span>
   * <span data-ttu-id="98eb0-185">**ALREADYONBOARDEDVM** - The name of the VM that was manually onboarded to either the Updates or ChangeTracking solution.</span><span class="sxs-lookup"><span data-stu-id="98eb0-185">**ALREADYONBOARDEDVM** - The name of the VM that was manually onboarded to either the Updates or ChangeTracking solution.</span></span>
   * <span data-ttu-id="98eb0-186">**ALREADYONBOARDEDVMRESOURCEGROUP** - The name of the resource group that the VM is a member of.</span><span class="sxs-lookup"><span data-stu-id="98eb0-186">**ALREADYONBOARDEDVMRESOURCEGROUP** - The name of the resource group that the VM is a member of.</span></span>
   * <span data-ttu-id="98eb0-187">**SOLUTIONTYPE** - Enter **Updates** or **ChangeTracking**</span><span class="sxs-lookup"><span data-stu-id="98eb0-187">**SOLUTIONTYPE** - Enter **Updates** or **ChangeTracking**</span></span>

   ![Enable-MultipleSolution runbook parameters](media/automation-onboard-solutions/runbook-parameters.png)

1. <span data-ttu-id="98eb0-189">Select **OK** to start the runbook job.</span><span class="sxs-lookup"><span data-stu-id="98eb0-189">Select **OK** to start the runbook job.</span></span>
1. <span data-ttu-id="98eb0-190">Monitor progress and any errors on the runbook job page.</span><span class="sxs-lookup"><span data-stu-id="98eb0-190">Monitor progress and any errors on the runbook job page.</span></span>

## <a name="next-steps"></a><span data-ttu-id="98eb0-191">Next steps</span><span class="sxs-lookup"><span data-stu-id="98eb0-191">Next steps</span></span>

<span data-ttu-id="98eb0-192">In this tutorial, you learned how to:</span><span class="sxs-lookup"><span data-stu-id="98eb0-192">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="98eb0-193">Onboard an Azure virtual machine manually.</span><span class="sxs-lookup"><span data-stu-id="98eb0-193">Onboard an Azure virtual machine manually.</span></span>
> * <span data-ttu-id="98eb0-194">Install and update required Azure modules.</span><span class="sxs-lookup"><span data-stu-id="98eb0-194">Install and update required Azure modules.</span></span>
> * <span data-ttu-id="98eb0-195">Import a runbook that onboards Azure VMs.</span><span class="sxs-lookup"><span data-stu-id="98eb0-195">Import a runbook that onboards Azure VMs.</span></span>
> * <span data-ttu-id="98eb0-196">Start the runbook that onboards Azure VMs automatically.</span><span class="sxs-lookup"><span data-stu-id="98eb0-196">Start the runbook that onboards Azure VMs automatically.</span></span>

<span data-ttu-id="98eb0-197">Follow this link to learn more about scheduling runbooks.</span><span class="sxs-lookup"><span data-stu-id="98eb0-197">Follow this link to learn more about scheduling runbooks.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="98eb0-198">[Scheduling runbooks](automation-schedules.md).</span><span class="sxs-lookup"><span data-stu-id="98eb0-198">[Scheduling runbooks](automation-schedules.md).</span></span>
