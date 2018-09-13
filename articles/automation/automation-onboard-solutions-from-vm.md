---
title: Onboard Update Management, Change Tracking, and Inventory solutions from an Azure VM
description: Learn how to onboard an Azure virtual machine with Update Management, Change Tracking, and Inventory solutions that are part of Azure Automation.
services: automation
author: georgewallace
ms.author: gwallace
ms.date: 06/06/2018
ms.topic: conceptual
ms.service: automation
ms.custom: mvc
manager: carmonm
ms.openlocfilehash: f270b2ccea51e83bc6475051b8667bf73d7fd717
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869256"
---
# <a name="onboard-update-management-change-tracking-and-inventory-solutions-from-an-azure-virtual-machine"></a><span data-ttu-id="ea488-103">Onboard Update Management, Change Tracking, and Inventory solutions from an Azure virtual machine</span><span class="sxs-lookup"><span data-stu-id="ea488-103">Onboard Update Management, Change Tracking, and Inventory solutions from an Azure virtual machine</span></span>

<span data-ttu-id="ea488-104">Azure Automation provides solutions to help you manage operating system security updates, track changes, and inventory what's installed on your computers.</span><span class="sxs-lookup"><span data-stu-id="ea488-104">Azure Automation provides solutions to help you manage operating system security updates, track changes, and inventory what's installed on your computers.</span></span> <span data-ttu-id="ea488-105">There are multiple ways to onboard machines.</span><span class="sxs-lookup"><span data-stu-id="ea488-105">There are multiple ways to onboard machines.</span></span> <span data-ttu-id="ea488-106">You can onboard the solution from a virtual machine, [from your Automation account](automation-onboard-solutions-from-automation-account.md), [from browsing multiple machines](automation-onboard-solutions-from-browse.md), or by using a [runbook](automation-onboard-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="ea488-106">You can onboard the solution from a virtual machine, [from your Automation account](automation-onboard-solutions-from-automation-account.md), [from browsing multiple machines](automation-onboard-solutions-from-browse.md), or by using a [runbook](automation-onboard-solutions.md).</span></span> <span data-ttu-id="ea488-107">This article covers onboarding these solutions from an Azure virtual machine.</span><span class="sxs-lookup"><span data-stu-id="ea488-107">This article covers onboarding these solutions from an Azure virtual machine.</span></span>

## <a name="sign-in-to-azure"></a><span data-ttu-id="ea488-108">Sign in to Azure</span><span class="sxs-lookup"><span data-stu-id="ea488-108">Sign in to Azure</span></span>

<span data-ttu-id="ea488-109">Sign in to the Azure portal at https://portal.azure.com.</span><span class="sxs-lookup"><span data-stu-id="ea488-109">Sign in to the Azure portal at https://portal.azure.com.</span></span>

## <a name="enable-the-solutions"></a><span data-ttu-id="ea488-110">Enable the solutions</span><span class="sxs-lookup"><span data-stu-id="ea488-110">Enable the solutions</span></span>

<span data-ttu-id="ea488-111">Go to an existing virtual machine.</span><span class="sxs-lookup"><span data-stu-id="ea488-111">Go to an existing virtual machine.</span></span> <span data-ttu-id="ea488-112">Under **OPERATIONS**, select **Update management**, **Inventory**, or **Change tracking**.</span><span class="sxs-lookup"><span data-stu-id="ea488-112">Under **OPERATIONS**, select **Update management**, **Inventory**, or **Change tracking**.</span></span>

<span data-ttu-id="ea488-113">To enable the solution for the VM only, ensure that **Enable for this VM** is selected.</span><span class="sxs-lookup"><span data-stu-id="ea488-113">To enable the solution for the VM only, ensure that **Enable for this VM** is selected.</span></span> <span data-ttu-id="ea488-114">To onboard multiple machines to the solution, select **Enable for VMs in this subscription**, and then select **Click to select machines to enable**.</span><span class="sxs-lookup"><span data-stu-id="ea488-114">To onboard multiple machines to the solution, select **Enable for VMs in this subscription**, and then select **Click to select machines to enable**.</span></span> <span data-ttu-id="ea488-115">To learn how to onboard multiple machines at once, see [Onboard Update Management, Change Tracking, and Inventory solutions](automation-onboard-solutions-from-automation-account.md).</span><span class="sxs-lookup"><span data-stu-id="ea488-115">To learn how to onboard multiple machines at once, see [Onboard Update Management, Change Tracking, and Inventory solutions](automation-onboard-solutions-from-automation-account.md).</span></span>

<span data-ttu-id="ea488-116">Select the Azure Log Analytics workspace and Automation account, and then select **Enable** to enable the solution.</span><span class="sxs-lookup"><span data-stu-id="ea488-116">Select the Azure Log Analytics workspace and Automation account, and then select **Enable** to enable the solution.</span></span> <span data-ttu-id="ea488-117">The solution takes up to 15 minutes to enable.</span><span class="sxs-lookup"><span data-stu-id="ea488-117">The solution takes up to 15 minutes to enable.</span></span>

![Onboard the Update Management solution](media/automation-onboard-solutions-from-vm/onboard-solution.png)

<span data-ttu-id="ea488-119">Go to the other solutions, and then select **Enable**.</span><span class="sxs-lookup"><span data-stu-id="ea488-119">Go to the other solutions, and then select **Enable**.</span></span> <span data-ttu-id="ea488-120">The Log Analytics and Automation account drop-down lists are disabled because these solutions use the same workspace and Automation account as the previously enabled solution.</span><span class="sxs-lookup"><span data-stu-id="ea488-120">The Log Analytics and Automation account drop-down lists are disabled because these solutions use the same workspace and Automation account as the previously enabled solution.</span></span>

> [!NOTE]
> <span data-ttu-id="ea488-121">**Change tracking** and **Inventory** use the same solution.</span><span class="sxs-lookup"><span data-stu-id="ea488-121">**Change tracking** and **Inventory** use the same solution.</span></span> <span data-ttu-id="ea488-122">When one of these solutions is enabled, the other is also enabled.</span><span class="sxs-lookup"><span data-stu-id="ea488-122">When one of these solutions is enabled, the other is also enabled.</span></span>

## <a name="scope-configuration"></a><span data-ttu-id="ea488-123">Scope configuration</span><span class="sxs-lookup"><span data-stu-id="ea488-123">Scope configuration</span></span>

<span data-ttu-id="ea488-124">Each solution uses a scope configuration in the workspace to target the computers that get the solution.</span><span class="sxs-lookup"><span data-stu-id="ea488-124">Each solution uses a scope configuration in the workspace to target the computers that get the solution.</span></span> <span data-ttu-id="ea488-125">The scope configuration is a group of one or more saved searches that are used to limit the scope of the solution to specific computers.</span><span class="sxs-lookup"><span data-stu-id="ea488-125">The scope configuration is a group of one or more saved searches that are used to limit the scope of the solution to specific computers.</span></span> <span data-ttu-id="ea488-126">To access the scope configurations, in your Automation account, under **RELATED RESOURCES**, select **Workspace**.</span><span class="sxs-lookup"><span data-stu-id="ea488-126">To access the scope configurations, in your Automation account, under **RELATED RESOURCES**, select **Workspace**.</span></span> <span data-ttu-id="ea488-127">In the workspace, under **WORKSPACE DATA SOURCES**, select **Scope Configurations**.</span><span class="sxs-lookup"><span data-stu-id="ea488-127">In the workspace, under **WORKSPACE DATA SOURCES**, select **Scope Configurations**.</span></span>

<span data-ttu-id="ea488-128">If the selected workspace doesn't already have the Update Management or Change Tracking solutions, the following scope configurations are created:</span><span class="sxs-lookup"><span data-stu-id="ea488-128">If the selected workspace doesn't already have the Update Management or Change Tracking solutions, the following scope configurations are created:</span></span>

* <span data-ttu-id="ea488-129">**MicrosoftDefaultScopeConfig-ChangeTracking**</span><span class="sxs-lookup"><span data-stu-id="ea488-129">**MicrosoftDefaultScopeConfig-ChangeTracking**</span></span>

* <span data-ttu-id="ea488-130">**MicrosoftDefaultScopeConfig-Updates**</span><span class="sxs-lookup"><span data-stu-id="ea488-130">**MicrosoftDefaultScopeConfig-Updates**</span></span>

<span data-ttu-id="ea488-131">If the selected workspace already has the solution, the solution isn't redeployed and the scope configuration isn't added.</span><span class="sxs-lookup"><span data-stu-id="ea488-131">If the selected workspace already has the solution, the solution isn't redeployed and the scope configuration isn't added.</span></span>

<span data-ttu-id="ea488-132">Select the ellipses (**...**) on any of the configurations, and then select **Edit**.</span><span class="sxs-lookup"><span data-stu-id="ea488-132">Select the ellipses (**...**) on any of the configurations, and then select **Edit**.</span></span> <span data-ttu-id="ea488-133">In the **Edit scope configuration** pane, select **Select Computer Groups**.</span><span class="sxs-lookup"><span data-stu-id="ea488-133">In the **Edit scope configuration** pane, select **Select Computer Groups**.</span></span> <span data-ttu-id="ea488-134">The **Computer Groups** pane shows the saved searches that are used to create the scope configuration.</span><span class="sxs-lookup"><span data-stu-id="ea488-134">The **Computer Groups** pane shows the saved searches that are used to create the scope configuration.</span></span>

## <a name="saved-searches"></a><span data-ttu-id="ea488-135">Saved searches</span><span class="sxs-lookup"><span data-stu-id="ea488-135">Saved searches</span></span>

<span data-ttu-id="ea488-136">When a computer is added to the Update Management, Change Tracking, or Inventory solutions, the computer is added to one of two saved searches in your workspace.</span><span class="sxs-lookup"><span data-stu-id="ea488-136">When a computer is added to the Update Management, Change Tracking, or Inventory solutions, the computer is added to one of two saved searches in your workspace.</span></span> <span data-ttu-id="ea488-137">The saved searches are queries that contain the computers that are targeted for these solutions.</span><span class="sxs-lookup"><span data-stu-id="ea488-137">The saved searches are queries that contain the computers that are targeted for these solutions.</span></span>

<span data-ttu-id="ea488-138">Go to your workspace.</span><span class="sxs-lookup"><span data-stu-id="ea488-138">Go to your workspace.</span></span> <span data-ttu-id="ea488-139">Under **General**, select **Saved searches**.</span><span class="sxs-lookup"><span data-stu-id="ea488-139">Under **General**, select **Saved searches**.</span></span> <span data-ttu-id="ea488-140">The two saved searches that are used by these solutions are shown in the following table:</span><span class="sxs-lookup"><span data-stu-id="ea488-140">The two saved searches that are used by these solutions are shown in the following table:</span></span>

|<span data-ttu-id="ea488-141">Name</span><span class="sxs-lookup"><span data-stu-id="ea488-141">Name</span></span>     |<span data-ttu-id="ea488-142">Category</span><span class="sxs-lookup"><span data-stu-id="ea488-142">Category</span></span>  |<span data-ttu-id="ea488-143">Alias</span><span class="sxs-lookup"><span data-stu-id="ea488-143">Alias</span></span>  |
|---------|---------|---------|
|<span data-ttu-id="ea488-144">MicrosoftDefaultComputerGroup</span><span class="sxs-lookup"><span data-stu-id="ea488-144">MicrosoftDefaultComputerGroup</span></span>     |  <span data-ttu-id="ea488-145">ChangeTracking</span><span class="sxs-lookup"><span data-stu-id="ea488-145">ChangeTracking</span></span>       | <span data-ttu-id="ea488-146">ChangeTracking__MicrosoftDefaultComputerGroup</span><span class="sxs-lookup"><span data-stu-id="ea488-146">ChangeTracking__MicrosoftDefaultComputerGroup</span></span>        |
|<span data-ttu-id="ea488-147">MicrosoftDefaultComputerGroup</span><span class="sxs-lookup"><span data-stu-id="ea488-147">MicrosoftDefaultComputerGroup</span></span>     | <span data-ttu-id="ea488-148">Updates</span><span class="sxs-lookup"><span data-stu-id="ea488-148">Updates</span></span>        | <span data-ttu-id="ea488-149">Updates__MicrosoftDefaultComputerGroup</span><span class="sxs-lookup"><span data-stu-id="ea488-149">Updates__MicrosoftDefaultComputerGroup</span></span>         |

<span data-ttu-id="ea488-150">Select either of the saved searches to view the query that's used to populate the group.</span><span class="sxs-lookup"><span data-stu-id="ea488-150">Select either of the saved searches to view the query that's used to populate the group.</span></span> <span data-ttu-id="ea488-151">The following image shows the query and its results:</span><span class="sxs-lookup"><span data-stu-id="ea488-151">The following image shows the query and its results:</span></span>

![Saved searches](media/automation-onboard-solutions-from-vm/logsearch.png)

## <a name="next-steps"></a><span data-ttu-id="ea488-153">Next steps</span><span class="sxs-lookup"><span data-stu-id="ea488-153">Next steps</span></span>

<span data-ttu-id="ea488-154">Continue to the tutorials for the solutions to learn how to use them:</span><span class="sxs-lookup"><span data-stu-id="ea488-154">Continue to the tutorials for the solutions to learn how to use them:</span></span>

* [<span data-ttu-id="ea488-155">Tutorial - Manage updates for your VM</span><span class="sxs-lookup"><span data-stu-id="ea488-155">Tutorial - Manage updates for your VM</span></span>](automation-tutorial-update-management.md)
* [<span data-ttu-id="ea488-156">Tutorial - Identify software on a VM</span><span class="sxs-lookup"><span data-stu-id="ea488-156">Tutorial - Identify software on a VM</span></span>](automation-tutorial-installed-software.md)
* [<span data-ttu-id="ea488-157">Tutorial - Troubleshoot changes on a VM</span><span class="sxs-lookup"><span data-stu-id="ea488-157">Tutorial - Troubleshoot changes on a VM</span></span>](automation-tutorial-troubleshoot-changes.md)
