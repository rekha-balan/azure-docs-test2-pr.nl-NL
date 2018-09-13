---
title: Manage updates for multiple Azure virtual machines
description: This article describes how to manage updates for Azure virtual machines.
services: automation
ms.service: automation
ms.component: update-management
author: georgewallace
ms.author: gwallace
ms.date: 08/29/2018
ms.topic: conceptual
manager: carmonm
ms.openlocfilehash: 231a9876c7a84953a7d9a88b761a1da9475d1f48
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868868"
---
# <a name="manage-updates-for-multiple-machines"></a><span data-ttu-id="dd696-103">Manage updates for multiple machines</span><span class="sxs-lookup"><span data-stu-id="dd696-103">Manage updates for multiple machines</span></span>

<span data-ttu-id="dd696-104">You can use the Update Management solution to manage updates and patches for your Windows and Linux virtual machines.</span><span class="sxs-lookup"><span data-stu-id="dd696-104">You can use the Update Management solution to manage updates and patches for your Windows and Linux virtual machines.</span></span> <span data-ttu-id="dd696-105">From your [Azure Automation](automation-offering-get-started.md) account, you can:</span><span class="sxs-lookup"><span data-stu-id="dd696-105">From your [Azure Automation](automation-offering-get-started.md) account, you can:</span></span>

- <span data-ttu-id="dd696-106">Onboard virtual machines</span><span class="sxs-lookup"><span data-stu-id="dd696-106">Onboard virtual machines</span></span>
- <span data-ttu-id="dd696-107">Assess the status of available updates</span><span class="sxs-lookup"><span data-stu-id="dd696-107">Assess the status of available updates</span></span>
- <span data-ttu-id="dd696-108">Schedule installation of required updates</span><span class="sxs-lookup"><span data-stu-id="dd696-108">Schedule installation of required updates</span></span>
- <span data-ttu-id="dd696-109">Review deployment results to verify that updates were applied successfully to all virtual machines for which Update Management is enabled</span><span class="sxs-lookup"><span data-stu-id="dd696-109">Review deployment results to verify that updates were applied successfully to all virtual machines for which Update Management is enabled</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dd696-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="dd696-110">Prerequisites</span></span>

<span data-ttu-id="dd696-111">To use Update Management, you need:</span><span class="sxs-lookup"><span data-stu-id="dd696-111">To use Update Management, you need:</span></span>

- <span data-ttu-id="dd696-112">An Azure Automation Run As account.</span><span class="sxs-lookup"><span data-stu-id="dd696-112">An Azure Automation Run As account.</span></span> <span data-ttu-id="dd696-113">To learn how to create one, see [Getting started with Azure Automation](automation-offering-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="dd696-113">To learn how to create one, see [Getting started with Azure Automation](automation-offering-get-started.md).</span></span>
- <span data-ttu-id="dd696-114">A virtual machine or computer with one of the supported operating systems installed.</span><span class="sxs-lookup"><span data-stu-id="dd696-114">A virtual machine or computer with one of the supported operating systems installed.</span></span>

## <a name="supported-operating-systems"></a><span data-ttu-id="dd696-115">Supported operating systems</span><span class="sxs-lookup"><span data-stu-id="dd696-115">Supported operating systems</span></span>

<span data-ttu-id="dd696-116">Update Management is supported on the following operating systems:</span><span class="sxs-lookup"><span data-stu-id="dd696-116">Update Management is supported on the following operating systems:</span></span>

|<span data-ttu-id="dd696-117">Operating system</span><span class="sxs-lookup"><span data-stu-id="dd696-117">Operating system</span></span>  |<span data-ttu-id="dd696-118">Notes</span><span class="sxs-lookup"><span data-stu-id="dd696-118">Notes</span></span>  |
|---------|---------|
|<span data-ttu-id="dd696-119">Windows Server 2008, Windows Server 2008 R2 RTM</span><span class="sxs-lookup"><span data-stu-id="dd696-119">Windows Server 2008, Windows Server 2008 R2 RTM</span></span>    | <span data-ttu-id="dd696-120">Supports only update assessments.</span><span class="sxs-lookup"><span data-stu-id="dd696-120">Supports only update assessments.</span></span>         |
|<span data-ttu-id="dd696-121">Windows Server 2008 R2 SP1 and later</span><span class="sxs-lookup"><span data-stu-id="dd696-121">Windows Server 2008 R2 SP1 and later</span></span>     |<span data-ttu-id="dd696-122">Windows PowerShell 4.0 or later is required.</span><span class="sxs-lookup"><span data-stu-id="dd696-122">Windows PowerShell 4.0 or later is required.</span></span> <span data-ttu-id="dd696-123">([Download WMF 4.0](https://www.microsoft.com/download/details.aspx?id=40855))</span><span class="sxs-lookup"><span data-stu-id="dd696-123">([Download WMF 4.0](https://www.microsoft.com/download/details.aspx?id=40855))</span></span></br> <span data-ttu-id="dd696-124">Windows PowerShell 5.1 is recommended for increased reliability.</span><span class="sxs-lookup"><span data-stu-id="dd696-124">Windows PowerShell 5.1 is recommended for increased reliability.</span></span> <span data-ttu-id="dd696-125">([Download WMF 5.1](https://www.microsoft.com/download/details.aspx?id=54616))</span><span class="sxs-lookup"><span data-stu-id="dd696-125">([Download WMF 5.1](https://www.microsoft.com/download/details.aspx?id=54616))</span></span>         |
|<span data-ttu-id="dd696-126">CentOS 6 (x86/x64) and 7 (x64)</span><span class="sxs-lookup"><span data-stu-id="dd696-126">CentOS 6 (x86/x64) and 7 (x64)</span></span>      | <span data-ttu-id="dd696-127">Linux agents must have access to an update repository.</span><span class="sxs-lookup"><span data-stu-id="dd696-127">Linux agents must have access to an update repository.</span></span>        |
|<span data-ttu-id="dd696-128">Red Hat Enterprise 6 (x86/x64) and 7 (x64)</span><span class="sxs-lookup"><span data-stu-id="dd696-128">Red Hat Enterprise 6 (x86/x64) and 7 (x64)</span></span>     | <span data-ttu-id="dd696-129">Linux agents must have access to an update repository.</span><span class="sxs-lookup"><span data-stu-id="dd696-129">Linux agents must have access to an update repository.</span></span>        |
|<span data-ttu-id="dd696-130">SUSE Linux Enterprise Server 11 (x86/x64) and 12 (x64)</span><span class="sxs-lookup"><span data-stu-id="dd696-130">SUSE Linux Enterprise Server 11 (x86/x64) and 12 (x64)</span></span>     | <span data-ttu-id="dd696-131">Linux agents must have access to an update repository.</span><span class="sxs-lookup"><span data-stu-id="dd696-131">Linux agents must have access to an update repository.</span></span>        |
|<span data-ttu-id="dd696-132">Ubuntu 12.04 LTS, 14.04 LTS, and 16.04 LTS (x86/x64)</span><span class="sxs-lookup"><span data-stu-id="dd696-132">Ubuntu 12.04 LTS, 14.04 LTS, and 16.04 LTS (x86/x64)</span></span>      |<span data-ttu-id="dd696-133">Linux agents must have access to an update repository.</span><span class="sxs-lookup"><span data-stu-id="dd696-133">Linux agents must have access to an update repository.</span></span>         |

> [!NOTE]
> <span data-ttu-id="dd696-134">To prevent updates from being applied outside a maintenance window on Ubuntu, reconfigure the Unattended-Upgrade package to disable automatic updates.</span><span class="sxs-lookup"><span data-stu-id="dd696-134">To prevent updates from being applied outside a maintenance window on Ubuntu, reconfigure the Unattended-Upgrade package to disable automatic updates.</span></span> <span data-ttu-id="dd696-135">For more information, see the [Automatic Updates topic in the Ubuntu Server Guide](https://help.ubuntu.com/lts/serverguide/automatic-updates.html).</span><span class="sxs-lookup"><span data-stu-id="dd696-135">For more information, see the [Automatic Updates topic in the Ubuntu Server Guide](https://help.ubuntu.com/lts/serverguide/automatic-updates.html).</span></span>

<span data-ttu-id="dd696-136">Linux agents must have access to an update repository.</span><span class="sxs-lookup"><span data-stu-id="dd696-136">Linux agents must have access to an update repository.</span></span>

<span data-ttu-id="dd696-137">This solution doesn't support an Operations Management Suite (OMS) Agent for Linux that's configured to report to multiple Azure Log Analytics workspaces.</span><span class="sxs-lookup"><span data-stu-id="dd696-137">This solution doesn't support an Operations Management Suite (OMS) Agent for Linux that's configured to report to multiple Azure Log Analytics workspaces.</span></span>

## <a name="enable-update-management-for-azure-virtual-machines"></a><span data-ttu-id="dd696-138">Enable Update Management for Azure virtual machines</span><span class="sxs-lookup"><span data-stu-id="dd696-138">Enable Update Management for Azure virtual machines</span></span>

<span data-ttu-id="dd696-139">In the Azure portal, open your Automation account, and then select **Update management**.</span><span class="sxs-lookup"><span data-stu-id="dd696-139">In the Azure portal, open your Automation account, and then select **Update management**.</span></span>

<span data-ttu-id="dd696-140">Select **Add Azure VMs**.</span><span class="sxs-lookup"><span data-stu-id="dd696-140">Select **Add Azure VMs**.</span></span>

![Add Azure VM tab](./media/manage-update-multi/update-onboard-vm.png)

<span data-ttu-id="dd696-142">Select a virtual machine to onboard.</span><span class="sxs-lookup"><span data-stu-id="dd696-142">Select a virtual machine to onboard.</span></span> 

<span data-ttu-id="dd696-143">Under **Enable Update Management**, select **Enable** to onboard the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="dd696-143">Under **Enable Update Management**, select **Enable** to onboard the virtual machine.</span></span>

![Enable Update Management dialog box](./media/manage-update-multi/update-enable.png)

<span data-ttu-id="dd696-145">When onboarding is finished, Update Management is enabled for your virtual machine.</span><span class="sxs-lookup"><span data-stu-id="dd696-145">When onboarding is finished, Update Management is enabled for your virtual machine.</span></span>

## <a name="enable-update-management-for-non-azure-virtual-machines-and-computers"></a><span data-ttu-id="dd696-146">Enable Update Management for non-Azure virtual machines and computers</span><span class="sxs-lookup"><span data-stu-id="dd696-146">Enable Update Management for non-Azure virtual machines and computers</span></span>

<span data-ttu-id="dd696-147">To learn how to enable Update Management for non-Azure Windows virtual machines and computers, see [Connect Windows computers to the Log Analytics service in Azure](../log-analytics/log-analytics-windows-agent.md).</span><span class="sxs-lookup"><span data-stu-id="dd696-147">To learn how to enable Update Management for non-Azure Windows virtual machines and computers, see [Connect Windows computers to the Log Analytics service in Azure](../log-analytics/log-analytics-windows-agent.md).</span></span>

<span data-ttu-id="dd696-148">To learn how to enable Update Management for non-Azure Linux virtual machines and computers, see [Connect your Linux computers to Log Analytics](../log-analytics/log-analytics-agent-linux.md).</span><span class="sxs-lookup"><span data-stu-id="dd696-148">To learn how to enable Update Management for non-Azure Linux virtual machines and computers, see [Connect your Linux computers to Log Analytics](../log-analytics/log-analytics-agent-linux.md).</span></span>

## <a name="view-computers-attached-to-your-automation-account"></a><span data-ttu-id="dd696-149">View computers attached to your Automation account</span><span class="sxs-lookup"><span data-stu-id="dd696-149">View computers attached to your Automation account</span></span>

<span data-ttu-id="dd696-150">After you enable Update Management for your machines, you can view machine information by selecting **Computers**.</span><span class="sxs-lookup"><span data-stu-id="dd696-150">After you enable Update Management for your machines, you can view machine information by selecting **Computers**.</span></span> <span data-ttu-id="dd696-151">You can see information about *machine name*, *compliance status*, *environment*, *OS type*, *critical and security updates installed*, *other updates installed*, and *update agent readiness* for your computers.</span><span class="sxs-lookup"><span data-stu-id="dd696-151">You can see information about *machine name*, *compliance status*, *environment*, *OS type*, *critical and security updates installed*, *other updates installed*, and *update agent readiness* for your computers.</span></span>

  ![View computers tab](./media/manage-update-multi/update-computers-tab.png)

<span data-ttu-id="dd696-153">Computers that have recently been enabled for Update Management might not have been assessed yet.</span><span class="sxs-lookup"><span data-stu-id="dd696-153">Computers that have recently been enabled for Update Management might not have been assessed yet.</span></span> <span data-ttu-id="dd696-154">The compliance state status for those computers is **Not assessed**.</span><span class="sxs-lookup"><span data-stu-id="dd696-154">The compliance state status for those computers is **Not assessed**.</span></span> <span data-ttu-id="dd696-155">Here's a list of possible values for compliance state:</span><span class="sxs-lookup"><span data-stu-id="dd696-155">Here's a list of possible values for compliance state:</span></span>

- <span data-ttu-id="dd696-156">**Compliant**: Computers that are not missing critical or security updates.</span><span class="sxs-lookup"><span data-stu-id="dd696-156">**Compliant**: Computers that are not missing critical or security updates.</span></span>

- <span data-ttu-id="dd696-157">**Non-compliant**: Computers that are missing at least one critical or security update.</span><span class="sxs-lookup"><span data-stu-id="dd696-157">**Non-compliant**: Computers that are missing at least one critical or security update.</span></span>

- <span data-ttu-id="dd696-158">**Not assessed**: The update assessment data hasn't been received from the computer within the expected timeframe.</span><span class="sxs-lookup"><span data-stu-id="dd696-158">**Not assessed**: The update assessment data hasn't been received from the computer within the expected timeframe.</span></span> <span data-ttu-id="dd696-159">For Linux computers, the expect timeframe is in the last 3 hours.</span><span class="sxs-lookup"><span data-stu-id="dd696-159">For Linux computers, the expect timeframe is in the last 3 hours.</span></span> <span data-ttu-id="dd696-160">For Windows computers, the expected timeframe is in the last 12 hours.</span><span class="sxs-lookup"><span data-stu-id="dd696-160">For Windows computers, the expected timeframe is in the last 12 hours.</span></span>

<span data-ttu-id="dd696-161">To view the status of the agent, select the link in the **UPDATE AGENT READINESS** column.</span><span class="sxs-lookup"><span data-stu-id="dd696-161">To view the status of the agent, select the link in the **UPDATE AGENT READINESS** column.</span></span> <span data-ttu-id="dd696-162">Selecting this option opens the **Hybrid Worker** pane, and shows the status of the Hybrid Worker.</span><span class="sxs-lookup"><span data-stu-id="dd696-162">Selecting this option opens the **Hybrid Worker** pane, and shows the status of the Hybrid Worker.</span></span> <span data-ttu-id="dd696-163">The following image shows an example of an agent that hasn't been connected to Update Management for an extended period of time:</span><span class="sxs-lookup"><span data-stu-id="dd696-163">The following image shows an example of an agent that hasn't been connected to Update Management for an extended period of time:</span></span>

![View computers tab](./media/manage-update-multi/update-agent-broken.png)

## <a name="view-an-update-assessment"></a><span data-ttu-id="dd696-165">View an update assessment</span><span class="sxs-lookup"><span data-stu-id="dd696-165">View an update assessment</span></span>

<span data-ttu-id="dd696-166">After Update Management is enabled, the **Update management** pane opens.</span><span class="sxs-lookup"><span data-stu-id="dd696-166">After Update Management is enabled, the **Update management** pane opens.</span></span> <span data-ttu-id="dd696-167">You can see a list of missing updates on the **Missing updates** tab.</span><span class="sxs-lookup"><span data-stu-id="dd696-167">You can see a list of missing updates on the **Missing updates** tab.</span></span>

## <a name="collect-data"></a><span data-ttu-id="dd696-168">Collect data</span><span class="sxs-lookup"><span data-stu-id="dd696-168">Collect data</span></span>

<span data-ttu-id="dd696-169">Agents that are installed on virtual machines and computers collect data about updates.</span><span class="sxs-lookup"><span data-stu-id="dd696-169">Agents that are installed on virtual machines and computers collect data about updates.</span></span> <span data-ttu-id="dd696-170">The agents send the data to Azure Update Management.</span><span class="sxs-lookup"><span data-stu-id="dd696-170">The agents send the data to Azure Update Management.</span></span>

### <a name="supported-agents"></a><span data-ttu-id="dd696-171">Supported agents</span><span class="sxs-lookup"><span data-stu-id="dd696-171">Supported agents</span></span>

<span data-ttu-id="dd696-172">The following table describes the connected sources that this solution supports:</span><span class="sxs-lookup"><span data-stu-id="dd696-172">The following table describes the connected sources that this solution supports:</span></span>

| <span data-ttu-id="dd696-173">Connected source</span><span class="sxs-lookup"><span data-stu-id="dd696-173">Connected source</span></span> | <span data-ttu-id="dd696-174">Supported</span><span class="sxs-lookup"><span data-stu-id="dd696-174">Supported</span></span> | <span data-ttu-id="dd696-175">Description</span><span class="sxs-lookup"><span data-stu-id="dd696-175">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="dd696-176">Windows agents</span><span class="sxs-lookup"><span data-stu-id="dd696-176">Windows agents</span></span> |<span data-ttu-id="dd696-177">Yes</span><span class="sxs-lookup"><span data-stu-id="dd696-177">Yes</span></span> |<span data-ttu-id="dd696-178">Update Management collects information about system updates from Windows agents and then initiates installation of required updates.</span><span class="sxs-lookup"><span data-stu-id="dd696-178">Update Management collects information about system updates from Windows agents and then initiates installation of required updates.</span></span> |
| <span data-ttu-id="dd696-179">Linux agents</span><span class="sxs-lookup"><span data-stu-id="dd696-179">Linux agents</span></span> |<span data-ttu-id="dd696-180">Yes</span><span class="sxs-lookup"><span data-stu-id="dd696-180">Yes</span></span> |<span data-ttu-id="dd696-181">Update Management collects information about system updates from Linux agents and then initiates installation of required updates on supported distributions.</span><span class="sxs-lookup"><span data-stu-id="dd696-181">Update Management collects information about system updates from Linux agents and then initiates installation of required updates on supported distributions.</span></span> |
| <span data-ttu-id="dd696-182">Operations Manager management group</span><span class="sxs-lookup"><span data-stu-id="dd696-182">Operations Manager management group</span></span> |<span data-ttu-id="dd696-183">Yes</span><span class="sxs-lookup"><span data-stu-id="dd696-183">Yes</span></span> |<span data-ttu-id="dd696-184">Update Management collects information about system updates from agents in a connected management group.</span><span class="sxs-lookup"><span data-stu-id="dd696-184">Update Management collects information about system updates from agents in a connected management group.</span></span> |
| <span data-ttu-id="dd696-185">Azure Storage account</span><span class="sxs-lookup"><span data-stu-id="dd696-185">Azure Storage account</span></span> |<span data-ttu-id="dd696-186">No</span><span class="sxs-lookup"><span data-stu-id="dd696-186">No</span></span> |<span data-ttu-id="dd696-187">Azure Storage doesn't include information about system updates.</span><span class="sxs-lookup"><span data-stu-id="dd696-187">Azure Storage doesn't include information about system updates.</span></span> |

### <a name="collection-frequency"></a><span data-ttu-id="dd696-188">Collection frequency</span><span class="sxs-lookup"><span data-stu-id="dd696-188">Collection frequency</span></span>

<span data-ttu-id="dd696-189">A scan runs twice a day for each managed Windows computer.</span><span class="sxs-lookup"><span data-stu-id="dd696-189">A scan runs twice a day for each managed Windows computer.</span></span> <span data-ttu-id="dd696-190">Every 15 minutes, the Windows API is called to query for the last update time to determine whether the status has changed.</span><span class="sxs-lookup"><span data-stu-id="dd696-190">Every 15 minutes, the Windows API is called to query for the last update time to determine whether the status has changed.</span></span> <span data-ttu-id="dd696-191">If the status changed, a compliance scan starts.</span><span class="sxs-lookup"><span data-stu-id="dd696-191">If the status changed, a compliance scan starts.</span></span> <span data-ttu-id="dd696-192">A scan runs every 3 hours for each managed Linux computer.</span><span class="sxs-lookup"><span data-stu-id="dd696-192">A scan runs every 3 hours for each managed Linux computer.</span></span>

<span data-ttu-id="dd696-193">It can take between 30 minutes and 6 hours for the dashboard to display updated data from managed computers.</span><span class="sxs-lookup"><span data-stu-id="dd696-193">It can take between 30 minutes and 6 hours for the dashboard to display updated data from managed computers.</span></span>

## <a name="schedule-an-update-deployment"></a><span data-ttu-id="dd696-194">Schedule an update deployment</span><span class="sxs-lookup"><span data-stu-id="dd696-194">Schedule an update deployment</span></span>

<span data-ttu-id="dd696-195">To install updates, schedule a deployment that aligns with your release schedule and service window.</span><span class="sxs-lookup"><span data-stu-id="dd696-195">To install updates, schedule a deployment that aligns with your release schedule and service window.</span></span> <span data-ttu-id="dd696-196">You can choose which update types to include in the deployment.</span><span class="sxs-lookup"><span data-stu-id="dd696-196">You can choose which update types to include in the deployment.</span></span> <span data-ttu-id="dd696-197">For example, you can include critical or security updates and exclude update rollups.</span><span class="sxs-lookup"><span data-stu-id="dd696-197">For example, you can include critical or security updates and exclude update rollups.</span></span>

<span data-ttu-id="dd696-198">To schedule a new update deployment for one or more virtual machines, under **Update management**, select **Schedule update deployment**.</span><span class="sxs-lookup"><span data-stu-id="dd696-198">To schedule a new update deployment for one or more virtual machines, under **Update management**, select **Schedule update deployment**.</span></span>

<span data-ttu-id="dd696-199">In the **New update deployment** pane, specify the following information:</span><span class="sxs-lookup"><span data-stu-id="dd696-199">In the **New update deployment** pane, specify the following information:</span></span>

- <span data-ttu-id="dd696-200">**Name**: Enter a unique name to identify the update deployment.</span><span class="sxs-lookup"><span data-stu-id="dd696-200">**Name**: Enter a unique name to identify the update deployment.</span></span>
- <span data-ttu-id="dd696-201">**Operating system**: Select **Windows** or **Linux**.</span><span class="sxs-lookup"><span data-stu-id="dd696-201">**Operating system**: Select **Windows** or **Linux**.</span></span>
- <span data-ttu-id="dd696-202">**Machines to update**: Select a Saved Search, Imported group, or select Machines, to choose the machines that you want to update.</span><span class="sxs-lookup"><span data-stu-id="dd696-202">**Machines to update**: Select a Saved Search, Imported group, or select Machines, to choose the machines that you want to update.</span></span> <span data-ttu-id="dd696-203">If you choose **Machines**, the readiness of the machine is shown in the **UPDATE AGENT READINESS** column.</span><span class="sxs-lookup"><span data-stu-id="dd696-203">If you choose **Machines**, the readiness of the machine is shown in the **UPDATE AGENT READINESS** column.</span></span> <span data-ttu-id="dd696-204">You can see the health state of the machine before you schedule the update deployment.</span><span class="sxs-lookup"><span data-stu-id="dd696-204">You can see the health state of the machine before you schedule the update deployment.</span></span> <span data-ttu-id="dd696-205">To learn about the different methods of creating computer groups in Log Analytics, see [Computer groups in Log Analytics](../log-analytics/log-analytics-computer-groups.md)</span><span class="sxs-lookup"><span data-stu-id="dd696-205">To learn about the different methods of creating computer groups in Log Analytics, see [Computer groups in Log Analytics](../log-analytics/log-analytics-computer-groups.md)</span></span>

  ![New update deployment pane](./media/manage-update-multi/update-select-computers.png)

- <span data-ttu-id="dd696-207">**Update classification**: Select the types of software to include in the update deployment.</span><span class="sxs-lookup"><span data-stu-id="dd696-207">**Update classification**: Select the types of software to include in the update deployment.</span></span> <span data-ttu-id="dd696-208">For a description of the classification types, see [Update classifications](automation-update-management.md#update-classifications).</span><span class="sxs-lookup"><span data-stu-id="dd696-208">For a description of the classification types, see [Update classifications](automation-update-management.md#update-classifications).</span></span> <span data-ttu-id="dd696-209">The classification types are:</span><span class="sxs-lookup"><span data-stu-id="dd696-209">The classification types are:</span></span>
  - <span data-ttu-id="dd696-210">Critical updates</span><span class="sxs-lookup"><span data-stu-id="dd696-210">Critical updates</span></span>
  - <span data-ttu-id="dd696-211">Security updates</span><span class="sxs-lookup"><span data-stu-id="dd696-211">Security updates</span></span>
  - <span data-ttu-id="dd696-212">Update rollups</span><span class="sxs-lookup"><span data-stu-id="dd696-212">Update rollups</span></span>
  - <span data-ttu-id="dd696-213">Feature packs</span><span class="sxs-lookup"><span data-stu-id="dd696-213">Feature packs</span></span>
  - <span data-ttu-id="dd696-214">Service packs</span><span class="sxs-lookup"><span data-stu-id="dd696-214">Service packs</span></span>
  - <span data-ttu-id="dd696-215">Definition updates</span><span class="sxs-lookup"><span data-stu-id="dd696-215">Definition updates</span></span>
  - <span data-ttu-id="dd696-216">Tools</span><span class="sxs-lookup"><span data-stu-id="dd696-216">Tools</span></span>
  - <span data-ttu-id="dd696-217">Updates</span><span class="sxs-lookup"><span data-stu-id="dd696-217">Updates</span></span>

- <span data-ttu-id="dd696-218">**Updates to exclude**: Selecting this option opens the **Exclude** page.</span><span class="sxs-lookup"><span data-stu-id="dd696-218">**Updates to exclude**: Selecting this option opens the **Exclude** page.</span></span> <span data-ttu-id="dd696-219">Enter the KB articles or package names to exclude.</span><span class="sxs-lookup"><span data-stu-id="dd696-219">Enter the KB articles or package names to exclude.</span></span>

- <span data-ttu-id="dd696-220">**Schedule settings**: You can accept the default date and time, which is 30 minutes after the current time.</span><span class="sxs-lookup"><span data-stu-id="dd696-220">**Schedule settings**: You can accept the default date and time, which is 30 minutes after the current time.</span></span> <span data-ttu-id="dd696-221">You can also specify a different time.</span><span class="sxs-lookup"><span data-stu-id="dd696-221">You can also specify a different time.</span></span>

   <span data-ttu-id="dd696-222">You can also specify whether the deployment occurs once or on a recurring schedule.</span><span class="sxs-lookup"><span data-stu-id="dd696-222">You can also specify whether the deployment occurs once or on a recurring schedule.</span></span> <span data-ttu-id="dd696-223">To set up a recurring schedule, under **Recurrence**, select **Recurring**.</span><span class="sxs-lookup"><span data-stu-id="dd696-223">To set up a recurring schedule, under **Recurrence**, select **Recurring**.</span></span>

   ![Schedule Settings dialog box](./media/manage-update-multi/update-set-schedule.png)
- <span data-ttu-id="dd696-225">**Maintenance window (minutes)**: Specify the period of time that you want the update deployment to occur.</span><span class="sxs-lookup"><span data-stu-id="dd696-225">**Maintenance window (minutes)**: Specify the period of time that you want the update deployment to occur.</span></span> <span data-ttu-id="dd696-226">This setting helps ensure that changes are performed within your defined service windows.</span><span class="sxs-lookup"><span data-stu-id="dd696-226">This setting helps ensure that changes are performed within your defined service windows.</span></span>

- <span data-ttu-id="dd696-227">**Reboot control** - This setting determines how reboots are handled for the update deployment.</span><span class="sxs-lookup"><span data-stu-id="dd696-227">**Reboot control** - This setting determines how reboots are handled for the update deployment.</span></span>

   |<span data-ttu-id="dd696-228">Option</span><span class="sxs-lookup"><span data-stu-id="dd696-228">Option</span></span>|<span data-ttu-id="dd696-229">Description</span><span class="sxs-lookup"><span data-stu-id="dd696-229">Description</span></span>|
   |---|---|
   |<span data-ttu-id="dd696-230">Reboot if required</span><span class="sxs-lookup"><span data-stu-id="dd696-230">Reboot if required</span></span>| <span data-ttu-id="dd696-231">**(Default)** If required, a reboot is initiated if the maintenance window allows.</span><span class="sxs-lookup"><span data-stu-id="dd696-231">**(Default)** If required, a reboot is initiated if the maintenance window allows.</span></span>|
   |<span data-ttu-id="dd696-232">Always reboot</span><span class="sxs-lookup"><span data-stu-id="dd696-232">Always reboot</span></span>|<span data-ttu-id="dd696-233">A reboot is initiated regardless of whether one is required.</span><span class="sxs-lookup"><span data-stu-id="dd696-233">A reboot is initiated regardless of whether one is required.</span></span> |
   |<span data-ttu-id="dd696-234">Never reboot</span><span class="sxs-lookup"><span data-stu-id="dd696-234">Never reboot</span></span>|<span data-ttu-id="dd696-235">Regardless of if a reboot is required, reboots are suppressed.</span><span class="sxs-lookup"><span data-stu-id="dd696-235">Regardless of if a reboot is required, reboots are suppressed.</span></span>|
   |<span data-ttu-id="dd696-236">Only reboot - will not install updates</span><span class="sxs-lookup"><span data-stu-id="dd696-236">Only reboot - will not install updates</span></span>|<span data-ttu-id="dd696-237">This option ignores installing updates, and only initiates a reboot.</span><span class="sxs-lookup"><span data-stu-id="dd696-237">This option ignores installing updates, and only initiates a reboot.</span></span>|

<span data-ttu-id="dd696-238">When you're finished configuring the schedule, select the **Create** button to return to the status dashboard.</span><span class="sxs-lookup"><span data-stu-id="dd696-238">When you're finished configuring the schedule, select the **Create** button to return to the status dashboard.</span></span> <span data-ttu-id="dd696-239">The **Scheduled** table shows the deployment schedule that you created.</span><span class="sxs-lookup"><span data-stu-id="dd696-239">The **Scheduled** table shows the deployment schedule that you created.</span></span>

## <a name="view-results-of-an-update-deployment"></a><span data-ttu-id="dd696-240">View results of an update deployment</span><span class="sxs-lookup"><span data-stu-id="dd696-240">View results of an update deployment</span></span>

<span data-ttu-id="dd696-241">After the scheduled deployment starts, you can see the status for that deployment on the **Update deployments** tab under **Update management**.</span><span class="sxs-lookup"><span data-stu-id="dd696-241">After the scheduled deployment starts, you can see the status for that deployment on the **Update deployments** tab under **Update management**.</span></span>

<span data-ttu-id="dd696-242">If the deployment is currently running, its status is **In progress**.</span><span class="sxs-lookup"><span data-stu-id="dd696-242">If the deployment is currently running, its status is **In progress**.</span></span> <span data-ttu-id="dd696-243">After the deployment finishes successfully, the status changes to **Succeeded**.</span><span class="sxs-lookup"><span data-stu-id="dd696-243">After the deployment finishes successfully, the status changes to **Succeeded**.</span></span>

<span data-ttu-id="dd696-244">If one or more updates fail in the deployment, the status is **Partially failed**.</span><span class="sxs-lookup"><span data-stu-id="dd696-244">If one or more updates fail in the deployment, the status is **Partially failed**.</span></span>

![Status of update deployment](./media/manage-update-multi/update-view-results.png)

<span data-ttu-id="dd696-246">To see the dashboard for an update deployment, select the completed deployment.</span><span class="sxs-lookup"><span data-stu-id="dd696-246">To see the dashboard for an update deployment, select the completed deployment.</span></span>

<span data-ttu-id="dd696-247">The **Update results** pane shows the total number of updates and the deployment results for the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="dd696-247">The **Update results** pane shows the total number of updates and the deployment results for the virtual machine.</span></span> <span data-ttu-id="dd696-248">The table on the right gives a detailed breakdown of each update and the installation results.</span><span class="sxs-lookup"><span data-stu-id="dd696-248">The table on the right gives a detailed breakdown of each update and the installation results.</span></span> <span data-ttu-id="dd696-249">Installation results can be one of the following values:</span><span class="sxs-lookup"><span data-stu-id="dd696-249">Installation results can be one of the following values:</span></span>

- <span data-ttu-id="dd696-250">**Not attempted**: The update was not installed because insufficient time was available based on the defined maintenance window.</span><span class="sxs-lookup"><span data-stu-id="dd696-250">**Not attempted**: The update was not installed because insufficient time was available based on the defined maintenance window.</span></span>
- <span data-ttu-id="dd696-251">**Succeeded**: The update succeeded.</span><span class="sxs-lookup"><span data-stu-id="dd696-251">**Succeeded**: The update succeeded.</span></span>
- <span data-ttu-id="dd696-252">**Failed**: The update failed.</span><span class="sxs-lookup"><span data-stu-id="dd696-252">**Failed**: The update failed.</span></span>

<span data-ttu-id="dd696-253">To see all log entries that the deployment created, select **All logs**.</span><span class="sxs-lookup"><span data-stu-id="dd696-253">To see all log entries that the deployment created, select **All logs**.</span></span>

<span data-ttu-id="dd696-254">To see the job stream of the runbook that manages the update deployment on the target virtual machine, select the output tile.</span><span class="sxs-lookup"><span data-stu-id="dd696-254">To see the job stream of the runbook that manages the update deployment on the target virtual machine, select the output tile.</span></span>

<span data-ttu-id="dd696-255">To see detailed information about any errors from the deployment, select **Errors**.</span><span class="sxs-lookup"><span data-stu-id="dd696-255">To see detailed information about any errors from the deployment, select **Errors**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dd696-256">Next steps</span><span class="sxs-lookup"><span data-stu-id="dd696-256">Next steps</span></span>

- <span data-ttu-id="dd696-257">To learn more about Update Management, including logs, output, and errors, see [Update Management solution in Azure](../operations-management-suite/oms-solution-update-management.md).</span><span class="sxs-lookup"><span data-stu-id="dd696-257">To learn more about Update Management, including logs, output, and errors, see [Update Management solution in Azure](../operations-management-suite/oms-solution-update-management.md).</span></span>
