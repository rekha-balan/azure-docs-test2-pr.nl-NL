---
title: Update Management solution in Azure
description: This article is intended to help you understand how to use the Azure Update Management solution to manage updates for your Windows and Linux computers.
services: automation
ms.service: automation
ms.component: update-management
author: georgewallace
ms.author: gwallace
ms.date: 08/29/2018
ms.topic: conceptual
manager: carmonm
ms.openlocfilehash: 62a7bb9bf63e8ebf97f9aeb5b08bf08ef06da43b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857708"
---
# <a name="update-management-solution-in-azure"></a><span data-ttu-id="f8c3d-103">Update Management solution in Azure</span><span class="sxs-lookup"><span data-stu-id="f8c3d-103">Update Management solution in Azure</span></span>

<span data-ttu-id="f8c3d-104">You can use the Update Management solution in Azure Automation to manage operating system updates for your Windows and Linux computers that are deployed in Azure, in on-premises environments, or in other cloud providers.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-104">You can use the Update Management solution in Azure Automation to manage operating system updates for your Windows and Linux computers that are deployed in Azure, in on-premises environments, or in other cloud providers.</span></span> <span data-ttu-id="f8c3d-105">You can quickly assess the status of available updates on all agent computers and manage the process of installing required updates for servers.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-105">You can quickly assess the status of available updates on all agent computers and manage the process of installing required updates for servers.</span></span>

<span data-ttu-id="f8c3d-106">You can enable Update Management for virtual machines directly from your Azure Automation account.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-106">You can enable Update Management for virtual machines directly from your Azure Automation account.</span></span> <span data-ttu-id="f8c3d-107">To learn how to enable Update Management for virtual machines from your Automation account, see [Manage updates for multiple virtual machines](manage-update-multi.md).</span><span class="sxs-lookup"><span data-stu-id="f8c3d-107">To learn how to enable Update Management for virtual machines from your Automation account, see [Manage updates for multiple virtual machines](manage-update-multi.md).</span></span> <span data-ttu-id="f8c3d-108">You can also enable Update Management for a single virtual machine from the virtual machine pane in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-108">You can also enable Update Management for a single virtual machine from the virtual machine pane in the Azure portal.</span></span> <span data-ttu-id="f8c3d-109">This scenario is available for [Linux](../virtual-machines/linux/tutorial-monitoring.md#enable-update-management) and [Windows](../virtual-machines/windows/tutorial-monitoring.md#enable-update-management) virtual machines.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-109">This scenario is available for [Linux](../virtual-machines/linux/tutorial-monitoring.md#enable-update-management) and [Windows](../virtual-machines/windows/tutorial-monitoring.md#enable-update-management) virtual machines.</span></span>

## <a name="solution-overview"></a><span data-ttu-id="f8c3d-110">Solution overview</span><span class="sxs-lookup"><span data-stu-id="f8c3d-110">Solution overview</span></span>

<span data-ttu-id="f8c3d-111">Computers that are managed by Update Management use the following configurations to perform assessment and update deployments:</span><span class="sxs-lookup"><span data-stu-id="f8c3d-111">Computers that are managed by Update Management use the following configurations to perform assessment and update deployments:</span></span>

* <span data-ttu-id="f8c3d-112">Microsoft Monitoring Agent (MMA) for Windows or Linux</span><span class="sxs-lookup"><span data-stu-id="f8c3d-112">Microsoft Monitoring Agent (MMA) for Windows or Linux</span></span>
* <span data-ttu-id="f8c3d-113">PowerShell Desired State Configuration (DSC) for Linux</span><span class="sxs-lookup"><span data-stu-id="f8c3d-113">PowerShell Desired State Configuration (DSC) for Linux</span></span>
* <span data-ttu-id="f8c3d-114">Automation Hybrid Runbook Worker</span><span class="sxs-lookup"><span data-stu-id="f8c3d-114">Automation Hybrid Runbook Worker</span></span>
* <span data-ttu-id="f8c3d-115">Microsoft Update or Windows Server Update Services (WSUS) for Windows computers</span><span class="sxs-lookup"><span data-stu-id="f8c3d-115">Microsoft Update or Windows Server Update Services (WSUS) for Windows computers</span></span>

<span data-ttu-id="f8c3d-116">The following diagram shows a conceptual view of the behavior and data flow with how the solution assesses and applies security updates to all connected Windows Server and Linux computers in a workspace:</span><span class="sxs-lookup"><span data-stu-id="f8c3d-116">The following diagram shows a conceptual view of the behavior and data flow with how the solution assesses and applies security updates to all connected Windows Server and Linux computers in a workspace:</span></span>

![Update Management process flow](media/automation-update-management/update-mgmt-updateworkflow.png)

<span data-ttu-id="f8c3d-118">Update Management can be used to natively onboard machines in multiple subscriptions in the same tenant.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-118">Update Management can be used to natively onboard machines in multiple subscriptions in the same tenant.</span></span> <span data-ttu-id="f8c3d-119">To manage machines in a different tenant you must onboard them as [Non-Azure machines](automation-onboard-solutions-from-automation-account.md#onboard-a-non-azure-machine).</span><span class="sxs-lookup"><span data-stu-id="f8c3d-119">To manage machines in a different tenant you must onboard them as [Non-Azure machines](automation-onboard-solutions-from-automation-account.md#onboard-a-non-azure-machine).</span></span>

<span data-ttu-id="f8c3d-120">After a computer performs a scan for update compliance, the agent forwards the information in bulk to Azure Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-120">After a computer performs a scan for update compliance, the agent forwards the information in bulk to Azure Log Analytics.</span></span> <span data-ttu-id="f8c3d-121">On a Windows computer, the compliance scan is performed every 12 hours by default.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-121">On a Windows computer, the compliance scan is performed every 12 hours by default.</span></span>

<span data-ttu-id="f8c3d-122">In addition to the scan schedule, the scan for update compliance is initiated within 15 minutes if the MMA is restarted, before update installation, and after update installation.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-122">In addition to the scan schedule, the scan for update compliance is initiated within 15 minutes if the MMA is restarted, before update installation, and after update installation.</span></span>

<span data-ttu-id="f8c3d-123">For a Linux computer, the compliance scan is performed every 3 hours by default.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-123">For a Linux computer, the compliance scan is performed every 3 hours by default.</span></span> <span data-ttu-id="f8c3d-124">If the MMA agent is restarted, a compliance scan is initiated within 15 minutes.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-124">If the MMA agent is restarted, a compliance scan is initiated within 15 minutes.</span></span>

<span data-ttu-id="f8c3d-125">The solution reports how up-to-date the computer is based on what source you're configured to sync with.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-125">The solution reports how up-to-date the computer is based on what source you're configured to sync with.</span></span> <span data-ttu-id="f8c3d-126">If the Windows computer is configured to report to WSUS, depending on when WSUS last synced with Microsoft Update, the results might differ from what Microsoft Updates shows.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-126">If the Windows computer is configured to report to WSUS, depending on when WSUS last synced with Microsoft Update, the results might differ from what Microsoft Updates shows.</span></span> <span data-ttu-id="f8c3d-127">This is the same for Linux computers that are configured to report to a local repo instead of to a public repo.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-127">This is the same for Linux computers that are configured to report to a local repo instead of to a public repo.</span></span>

> [!NOTE]
> <span data-ttu-id="f8c3d-128">To properly report to the service, Update Management requires certain URLs and ports to be enabled.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-128">To properly report to the service, Update Management requires certain URLs and ports to be enabled.</span></span> <span data-ttu-id="f8c3d-129">To learn more about these requirements, see [Network planning for Hybrid Workers](automation-hybrid-runbook-worker.md#network-planning).</span><span class="sxs-lookup"><span data-stu-id="f8c3d-129">To learn more about these requirements, see [Network planning for Hybrid Workers](automation-hybrid-runbook-worker.md#network-planning).</span></span>

<span data-ttu-id="f8c3d-130">You can deploy and install software updates on computers that require the updates by creating a scheduled deployment.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-130">You can deploy and install software updates on computers that require the updates by creating a scheduled deployment.</span></span> <span data-ttu-id="f8c3d-131">Updates classified as *Optional* aren't included in the deployment scope for Windows computers.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-131">Updates classified as *Optional* aren't included in the deployment scope for Windows computers.</span></span> <span data-ttu-id="f8c3d-132">Only required updates are included in the deployment scope.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-132">Only required updates are included in the deployment scope.</span></span> 

<span data-ttu-id="f8c3d-133">The scheduled deployment defines what target computers receive the applicable updates, either by explicitly specifying computers or by selecting a [computer group](../log-analytics/log-analytics-computer-groups.md) that's based on log searches of a specific set of computers.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-133">The scheduled deployment defines what target computers receive the applicable updates, either by explicitly specifying computers or by selecting a [computer group](../log-analytics/log-analytics-computer-groups.md) that's based on log searches of a specific set of computers.</span></span> <span data-ttu-id="f8c3d-134">You also specify a schedule to approve and designate a period of time during which updates can be installed.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-134">You also specify a schedule to approve and designate a period of time during which updates can be installed.</span></span>

<span data-ttu-id="f8c3d-135">Updates are installed by runbooks in Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-135">Updates are installed by runbooks in Azure Automation.</span></span> <span data-ttu-id="f8c3d-136">You can't view these runbooks, and the runbooks don’t require any configuration.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-136">You can't view these runbooks, and the runbooks don’t require any configuration.</span></span> <span data-ttu-id="f8c3d-137">When an update deployment is created, the update deployment creates a schedule that starts a master update runbook at the specified time for the included computers.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-137">When an update deployment is created, the update deployment creates a schedule that starts a master update runbook at the specified time for the included computers.</span></span> <span data-ttu-id="f8c3d-138">The master runbook starts a child runbook on each agent to perform installation of required updates.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-138">The master runbook starts a child runbook on each agent to perform installation of required updates.</span></span>

<span data-ttu-id="f8c3d-139">At the date and time specified in the update deployment, the target computers execute the deployment in parallel.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-139">At the date and time specified in the update deployment, the target computers execute the deployment in parallel.</span></span> <span data-ttu-id="f8c3d-140">Before installation, a scan is performed to verify that the updates are still required.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-140">Before installation, a scan is performed to verify that the updates are still required.</span></span> <span data-ttu-id="f8c3d-141">For WSUS client computers, if the updates aren't approved in WSUS, the update deployment fails.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-141">For WSUS client computers, if the updates aren't approved in WSUS, the update deployment fails.</span></span>

## <a name="clients"></a><span data-ttu-id="f8c3d-142">Clients</span><span class="sxs-lookup"><span data-stu-id="f8c3d-142">Clients</span></span>

### <a name="supported-client-types"></a><span data-ttu-id="f8c3d-143">Supported client types</span><span class="sxs-lookup"><span data-stu-id="f8c3d-143">Supported client types</span></span>

<span data-ttu-id="f8c3d-144">The following table shows a list of supported operating systems:</span><span class="sxs-lookup"><span data-stu-id="f8c3d-144">The following table shows a list of supported operating systems:</span></span>

|<span data-ttu-id="f8c3d-145">Operating system</span><span class="sxs-lookup"><span data-stu-id="f8c3d-145">Operating system</span></span>  |<span data-ttu-id="f8c3d-146">Notes</span><span class="sxs-lookup"><span data-stu-id="f8c3d-146">Notes</span></span>  |
|---------|---------|
|<span data-ttu-id="f8c3d-147">Windows Server 2008, Windows Server 2008 R2 RTM</span><span class="sxs-lookup"><span data-stu-id="f8c3d-147">Windows Server 2008, Windows Server 2008 R2 RTM</span></span>    | <span data-ttu-id="f8c3d-148">Supports only update assessments.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-148">Supports only update assessments.</span></span>         |
|<span data-ttu-id="f8c3d-149">Windows Server 2008 R2 SP1 and later</span><span class="sxs-lookup"><span data-stu-id="f8c3d-149">Windows Server 2008 R2 SP1 and later</span></span>     |<span data-ttu-id="f8c3d-150">.NET Framework 4.5 or later is required.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-150">.NET Framework 4.5 or later is required.</span></span> <span data-ttu-id="f8c3d-151">([Download .NET Framework](/dotnet/framework/install/guide-for-developers))</span><span class="sxs-lookup"><span data-stu-id="f8c3d-151">([Download .NET Framework](/dotnet/framework/install/guide-for-developers))</span></span><br/> <span data-ttu-id="f8c3d-152">Windows PowerShell 4.0 or later is required.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-152">Windows PowerShell 4.0 or later is required.</span></span> <span data-ttu-id="f8c3d-153">([Download WMF 4.0](https://www.microsoft.com/download/details.aspx?id=40855))</span><span class="sxs-lookup"><span data-stu-id="f8c3d-153">([Download WMF 4.0](https://www.microsoft.com/download/details.aspx?id=40855))</span></span><br/> <span data-ttu-id="f8c3d-154">Windows PowerShell 5.1 is recommended for increased reliability.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-154">Windows PowerShell 5.1 is recommended for increased reliability.</span></span>  <span data-ttu-id="f8c3d-155">([Download WMF 5.1](https://www.microsoft.com/download/details.aspx?id=54616))</span><span class="sxs-lookup"><span data-stu-id="f8c3d-155">([Download WMF 5.1](https://www.microsoft.com/download/details.aspx?id=54616))</span></span>        |
|<span data-ttu-id="f8c3d-156">CentOS 6 (x86/x64) and 7 (x64)</span><span class="sxs-lookup"><span data-stu-id="f8c3d-156">CentOS 6 (x86/x64) and 7 (x64)</span></span>      | <span data-ttu-id="f8c3d-157">Linux agents must have access to an update repository.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-157">Linux agents must have access to an update repository.</span></span> <span data-ttu-id="f8c3d-158">Classification-based patching requires 'yum' to return security data which CentOS does not have out of the box.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-158">Classification-based patching requires 'yum' to return security data which CentOS does not have out of the box.</span></span>         |
|<span data-ttu-id="f8c3d-159">Red Hat Enterprise 6 (x86/x64) and 7 (x64)</span><span class="sxs-lookup"><span data-stu-id="f8c3d-159">Red Hat Enterprise 6 (x86/x64) and 7 (x64)</span></span>     | <span data-ttu-id="f8c3d-160">Linux agents must have access to an update repository.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-160">Linux agents must have access to an update repository.</span></span>        |
|<span data-ttu-id="f8c3d-161">SUSE Linux Enterprise Server 11 (x86/x64) and 12 (x64)</span><span class="sxs-lookup"><span data-stu-id="f8c3d-161">SUSE Linux Enterprise Server 11 (x86/x64) and 12 (x64)</span></span>     | <span data-ttu-id="f8c3d-162">Linux agents must have access to an update repository.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-162">Linux agents must have access to an update repository.</span></span>        |
|<span data-ttu-id="f8c3d-163">Ubuntu 14.04 LTS and 16.04 LTS (x86/x64)</span><span class="sxs-lookup"><span data-stu-id="f8c3d-163">Ubuntu 14.04 LTS and 16.04 LTS (x86/x64)</span></span>      |<span data-ttu-id="f8c3d-164">Linux agents must have access to an update repository.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-164">Linux agents must have access to an update repository.</span></span>         |

### <a name="unsupported-client-types"></a><span data-ttu-id="f8c3d-165">Unsupported client types</span><span class="sxs-lookup"><span data-stu-id="f8c3d-165">Unsupported client types</span></span>

<span data-ttu-id="f8c3d-166">The following table lists operating systems that aren't supported:</span><span class="sxs-lookup"><span data-stu-id="f8c3d-166">The following table lists operating systems that aren't supported:</span></span>

|<span data-ttu-id="f8c3d-167">Operating system</span><span class="sxs-lookup"><span data-stu-id="f8c3d-167">Operating system</span></span>  |<span data-ttu-id="f8c3d-168">Notes</span><span class="sxs-lookup"><span data-stu-id="f8c3d-168">Notes</span></span>  |
|---------|---------|
|<span data-ttu-id="f8c3d-169">Windows client</span><span class="sxs-lookup"><span data-stu-id="f8c3d-169">Windows client</span></span>     | <span data-ttu-id="f8c3d-170">Client operating systems (such as Windows 7 and Windows 10) aren't supported.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-170">Client operating systems (such as Windows 7 and Windows 10) aren't supported.</span></span>        |
|<span data-ttu-id="f8c3d-171">Windows Server 2016 Nano Server</span><span class="sxs-lookup"><span data-stu-id="f8c3d-171">Windows Server 2016 Nano Server</span></span>     | <span data-ttu-id="f8c3d-172">Not supported.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-172">Not supported.</span></span>       |

### <a name="client-requirements"></a><span data-ttu-id="f8c3d-173">Client requirements</span><span class="sxs-lookup"><span data-stu-id="f8c3d-173">Client requirements</span></span>

#### <a name="windows"></a><span data-ttu-id="f8c3d-174">Windows</span><span class="sxs-lookup"><span data-stu-id="f8c3d-174">Windows</span></span>

<span data-ttu-id="f8c3d-175">Windows agents must be configured to communicate with a WSUS server or they must have access to Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-175">Windows agents must be configured to communicate with a WSUS server or they must have access to Microsoft Update.</span></span> <span data-ttu-id="f8c3d-176">You can use Update Management with System Center Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-176">You can use Update Management with System Center Configuration Manager.</span></span> <span data-ttu-id="f8c3d-177">To learn more about integration scenarios, see [Integrate System Center Configuration Manager with Update Management](oms-solution-updatemgmt-sccmintegration.md#configuration).</span><span class="sxs-lookup"><span data-stu-id="f8c3d-177">To learn more about integration scenarios, see [Integrate System Center Configuration Manager with Update Management](oms-solution-updatemgmt-sccmintegration.md#configuration).</span></span> <span data-ttu-id="f8c3d-178">The [Windows agent](../log-analytics/log-analytics-agent-windows.md) is required.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-178">The [Windows agent](../log-analytics/log-analytics-agent-windows.md) is required.</span></span> <span data-ttu-id="f8c3d-179">The agent is installed automatically if you're onboarding an Azure virtual machine.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-179">The agent is installed automatically if you're onboarding an Azure virtual machine.</span></span>

#### <a name="linux"></a><span data-ttu-id="f8c3d-180">Linux</span><span class="sxs-lookup"><span data-stu-id="f8c3d-180">Linux</span></span>

<span data-ttu-id="f8c3d-181">For Linux, the machine must have access to an update repository.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-181">For Linux, the machine must have access to an update repository.</span></span> <span data-ttu-id="f8c3d-182">The update repository can be private or public.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-182">The update repository can be private or public.</span></span> <span data-ttu-id="f8c3d-183">TLS 1.1 or TLS 1.2 is required to interact with Update Management.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-183">TLS 1.1 or TLS 1.2 is required to interact with Update Management.</span></span> <span data-ttu-id="f8c3d-184">An Operations Management Suite (OMS) Agent for Linux that's configured to report to multiple Log Analytics workspaces isn't supported with this solution.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-184">An Operations Management Suite (OMS) Agent for Linux that's configured to report to multiple Log Analytics workspaces isn't supported with this solution.</span></span>

<span data-ttu-id="f8c3d-185">For information about how to install the OMS Agent for Linux and to download the latest version, see [Operations Management Suite Agent for Linux](https://github.com/microsoft/oms-agent-for-linux).</span><span class="sxs-lookup"><span data-stu-id="f8c3d-185">For information about how to install the OMS Agent for Linux and to download the latest version, see [Operations Management Suite Agent for Linux](https://github.com/microsoft/oms-agent-for-linux).</span></span> <span data-ttu-id="f8c3d-186">For information about how to install the OMS Agent for Windows, see [Operations Management Suite Agent for Windows](../log-analytics/log-analytics-windows-agent.md).</span><span class="sxs-lookup"><span data-stu-id="f8c3d-186">For information about how to install the OMS Agent for Windows, see [Operations Management Suite Agent for Windows](../log-analytics/log-analytics-windows-agent.md).</span></span>

## <a name="permissions"></a><span data-ttu-id="f8c3d-187">Permissions</span><span class="sxs-lookup"><span data-stu-id="f8c3d-187">Permissions</span></span>

<span data-ttu-id="f8c3d-188">To create and manage update deployments, you need specific permissions.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-188">To create and manage update deployments, you need specific permissions.</span></span> <span data-ttu-id="f8c3d-189">To learn about these permissions, see [Role-based access - Update Management](automation-role-based-access-control.md#update-management).</span><span class="sxs-lookup"><span data-stu-id="f8c3d-189">To learn about these permissions, see [Role-based access - Update Management](automation-role-based-access-control.md#update-management).</span></span>

## <a name="solution-components"></a><span data-ttu-id="f8c3d-190">Solution components</span><span class="sxs-lookup"><span data-stu-id="f8c3d-190">Solution components</span></span>

<span data-ttu-id="f8c3d-191">The solution consists of the following resources.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-191">The solution consists of the following resources.</span></span> <span data-ttu-id="f8c3d-192">The resources are added to your Automation account.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-192">The resources are added to your Automation account.</span></span> <span data-ttu-id="f8c3d-193">They're either directly connected agents or in an Operations Manager-connected management group.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-193">They're either directly connected agents or in an Operations Manager-connected management group.</span></span>

### <a name="hybrid-worker-groups"></a><span data-ttu-id="f8c3d-194">Hybrid Worker groups</span><span class="sxs-lookup"><span data-stu-id="f8c3d-194">Hybrid Worker groups</span></span>

<span data-ttu-id="f8c3d-195">After you enable this solution, any Windows computer that's directly connected to your Log Analytics workspace is automatically configured as a Hybrid Runbook Worker to support the runbooks that are included in this solution.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-195">After you enable this solution, any Windows computer that's directly connected to your Log Analytics workspace is automatically configured as a Hybrid Runbook Worker to support the runbooks that are included in this solution.</span></span>

<span data-ttu-id="f8c3d-196">Each Windows computer that's managed by the solution is listed in the **Hybrid worker groups** pane as a **System hybrid worker group** for the Automation account.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-196">Each Windows computer that's managed by the solution is listed in the **Hybrid worker groups** pane as a **System hybrid worker group** for the Automation account.</span></span> <span data-ttu-id="f8c3d-197">The solutions use the naming convention *Hostname FQDN_GUID*.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-197">The solutions use the naming convention *Hostname FQDN_GUID*.</span></span> <span data-ttu-id="f8c3d-198">You can't target these groups with runbooks in your account.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-198">You can't target these groups with runbooks in your account.</span></span> <span data-ttu-id="f8c3d-199">They fail if you try.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-199">They fail if you try.</span></span> <span data-ttu-id="f8c3d-200">These groups are intended to support only the management solution.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-200">These groups are intended to support only the management solution.</span></span>

<span data-ttu-id="f8c3d-201">You can add the Windows computers to a Hybrid Runbook Worker group in your Automation account to support Automation runbooks if you use the same account for both the solution and the Hybrid Runbook Worker group membership.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-201">You can add the Windows computers to a Hybrid Runbook Worker group in your Automation account to support Automation runbooks if you use the same account for both the solution and the Hybrid Runbook Worker group membership.</span></span> <span data-ttu-id="f8c3d-202">This functionality was added in version 7.2.12024.0 of the Hybrid Runbook Worker.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-202">This functionality was added in version 7.2.12024.0 of the Hybrid Runbook Worker.</span></span>

### <a name="management-packs"></a><span data-ttu-id="f8c3d-203">Management packs</span><span class="sxs-lookup"><span data-stu-id="f8c3d-203">Management packs</span></span>

<span data-ttu-id="f8c3d-204">If your System Center Operations Manager management group is connected to a Log Analytics workspace, the following management packs are installed in Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-204">If your System Center Operations Manager management group is connected to a Log Analytics workspace, the following management packs are installed in Operations Manager.</span></span> <span data-ttu-id="f8c3d-205">These management packs are also installed on directly connected Windows computers after you add the solution.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-205">These management packs are also installed on directly connected Windows computers after you add the solution.</span></span> <span data-ttu-id="f8c3d-206">You don't need to configure or manage these management packs.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-206">You don't need to configure or manage these management packs.</span></span>

* <span data-ttu-id="f8c3d-207">Microsoft System Center Advisor Update Assessment Intelligence Pack (Microsoft.IntelligencePacks.UpdateAssessment)</span><span class="sxs-lookup"><span data-stu-id="f8c3d-207">Microsoft System Center Advisor Update Assessment Intelligence Pack (Microsoft.IntelligencePacks.UpdateAssessment)</span></span>
* <span data-ttu-id="f8c3d-208">Microsoft.IntelligencePack.UpdateAssessment.Configuration (Microsoft.IntelligencePack.UpdateAssessment.Configuration)</span><span class="sxs-lookup"><span data-stu-id="f8c3d-208">Microsoft.IntelligencePack.UpdateAssessment.Configuration (Microsoft.IntelligencePack.UpdateAssessment.Configuration)</span></span>
* <span data-ttu-id="f8c3d-209">Update Deployment MP</span><span class="sxs-lookup"><span data-stu-id="f8c3d-209">Update Deployment MP</span></span>

<span data-ttu-id="f8c3d-210">For more information about how solution management packs are updated, see [Connect Operations Manager to Log Analytics](../log-analytics/log-analytics-om-agents.md).</span><span class="sxs-lookup"><span data-stu-id="f8c3d-210">For more information about how solution management packs are updated, see [Connect Operations Manager to Log Analytics](../log-analytics/log-analytics-om-agents.md).</span></span>

> [!NOTE]
> <span data-ttu-id="f8c3d-211">For systems with the Operations Manger Agent, to be able to be fully managed by Update Management, the agent needs to be updated to the Microsoft Monitoring Agent.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-211">For systems with the Operations Manger Agent, to be able to be fully managed by Update Management, the agent needs to be updated to the Microsoft Monitoring Agent.</span></span> <span data-ttu-id="f8c3d-212">To learn how to update the agent, see [How to upgrade an Operations Manager agent](https://docs.microsoft.com/system-center/scom/deploy-upgrade-agents).</span><span class="sxs-lookup"><span data-stu-id="f8c3d-212">To learn how to update the agent, see [How to upgrade an Operations Manager agent](https://docs.microsoft.com/system-center/scom/deploy-upgrade-agents).</span></span>

### <a name="confirm-that-non-azure-machines-are-onboarded"></a><span data-ttu-id="f8c3d-213">Confirm that non-Azure machines are onboarded</span><span class="sxs-lookup"><span data-stu-id="f8c3d-213">Confirm that non-Azure machines are onboarded</span></span>

<span data-ttu-id="f8c3d-214">To confirm that directly connected machines are communicating with Log Analytics, after a few minutes, you can run one the following log searches.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-214">To confirm that directly connected machines are communicating with Log Analytics, after a few minutes, you can run one the following log searches.</span></span>

#### <a name="linux"></a><span data-ttu-id="f8c3d-215">Linux</span><span class="sxs-lookup"><span data-stu-id="f8c3d-215">Linux</span></span>

```
Heartbeat
| where OSType == "Linux" | summarize arg_max(TimeGenerated, *) by SourceComputerId | top 500000 by Computer asc | render table
```

#### <a name="windows"></a><span data-ttu-id="f8c3d-216">Windows</span><span class="sxs-lookup"><span data-stu-id="f8c3d-216">Windows</span></span>

```
Heartbeat
| where OSType == "Windows" | summarize arg_max(TimeGenerated, *) by SourceComputerId | top 500000 by Computer asc | render table
```

<span data-ttu-id="f8c3d-217">On a Windows computer, you can review the following information to verify agent connectivity with Log Analytics:</span><span class="sxs-lookup"><span data-stu-id="f8c3d-217">On a Windows computer, you can review the following information to verify agent connectivity with Log Analytics:</span></span>

1. <span data-ttu-id="f8c3d-218">In Control Panel, open **Microsoft Monitoring Agent**.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-218">In Control Panel, open **Microsoft Monitoring Agent**.</span></span> <span data-ttu-id="f8c3d-219">On the **Azure Log Analytics** tab, the agent displays the following message: **The Microsoft Monitoring Agent has successfully connected to Log Analytics**.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-219">On the **Azure Log Analytics** tab, the agent displays the following message: **The Microsoft Monitoring Agent has successfully connected to Log Analytics**.</span></span>
2. <span data-ttu-id="f8c3d-220">Open the Windows Event Log.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-220">Open the Windows Event Log.</span></span> <span data-ttu-id="f8c3d-221">Go to **Application and Services Logs\Operations Manager** and search for Event ID 3000 and Event ID 5002 from the source **Service Connector**.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-221">Go to **Application and Services Logs\Operations Manager** and search for Event ID 3000 and Event ID 5002 from the source **Service Connector**.</span></span> <span data-ttu-id="f8c3d-222">These events indicate that the computer has registered with the Log Analytics workspace and is receiving configuration.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-222">These events indicate that the computer has registered with the Log Analytics workspace and is receiving configuration.</span></span>

<span data-ttu-id="f8c3d-223">If the agent can't communicate with Log Analytics and the agent is configured to communicate with the internet through a firewall or proxy server, confirm that the firewall or proxy server is properly configured.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-223">If the agent can't communicate with Log Analytics and the agent is configured to communicate with the internet through a firewall or proxy server, confirm that the firewall or proxy server is properly configured.</span></span> <span data-ttu-id="f8c3d-224">To learn how to verify that the firewall or proxy server is properly configured, see [Network configuration for Windows agent](../log-analytics/log-analytics-agent-windows.md) or [Network configuration for Linux agent](../log-analytics/log-analytics-agent-linux.md).</span><span class="sxs-lookup"><span data-stu-id="f8c3d-224">To learn how to verify that the firewall or proxy server is properly configured, see [Network configuration for Windows agent](../log-analytics/log-analytics-agent-windows.md) or [Network configuration for Linux agent](../log-analytics/log-analytics-agent-linux.md).</span></span>

> [!NOTE]
> <span data-ttu-id="f8c3d-225">If your Linux systems are configured to communicate with a proxy or OMS Gateway and you're onboarding this solution, update the *proxy.conf* permissions to grant the omiuser group read permission on the file by using the following commands:</span><span class="sxs-lookup"><span data-stu-id="f8c3d-225">If your Linux systems are configured to communicate with a proxy or OMS Gateway and you're onboarding this solution, update the *proxy.conf* permissions to grant the omiuser group read permission on the file by using the following commands:</span></span>
>
> `sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/proxy.conf`
> `sudo chmod 644 /etc/opt/microsoft/omsagent/proxy.conf`

<span data-ttu-id="f8c3d-226">Newly added Linux agents show a status of **Updated** after an assessment has been performed.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-226">Newly added Linux agents show a status of **Updated** after an assessment has been performed.</span></span> <span data-ttu-id="f8c3d-227">This process can take up to 6 hours.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-227">This process can take up to 6 hours.</span></span>

<span data-ttu-id="f8c3d-228">To confirm that an Operations Manager management group is communicating with Log Analytics, see [Validate Operations Manager integration with Log Analytics](../log-analytics/log-analytics-om-agents.md#validate-operations-manager-integration-with-log-analytics).</span><span class="sxs-lookup"><span data-stu-id="f8c3d-228">To confirm that an Operations Manager management group is communicating with Log Analytics, see [Validate Operations Manager integration with Log Analytics](../log-analytics/log-analytics-om-agents.md#validate-operations-manager-integration-with-log-analytics).</span></span>

## <a name="data-collection"></a><span data-ttu-id="f8c3d-229">Data collection</span><span class="sxs-lookup"><span data-stu-id="f8c3d-229">Data collection</span></span>

### <a name="supported-agents"></a><span data-ttu-id="f8c3d-230">Supported agents</span><span class="sxs-lookup"><span data-stu-id="f8c3d-230">Supported agents</span></span>

<span data-ttu-id="f8c3d-231">The following table describes the connected sources that are supported by this solution:</span><span class="sxs-lookup"><span data-stu-id="f8c3d-231">The following table describes the connected sources that are supported by this solution:</span></span>

| <span data-ttu-id="f8c3d-232">Connected source</span><span class="sxs-lookup"><span data-stu-id="f8c3d-232">Connected source</span></span> | <span data-ttu-id="f8c3d-233">Supported</span><span class="sxs-lookup"><span data-stu-id="f8c3d-233">Supported</span></span> | <span data-ttu-id="f8c3d-234">Description</span><span class="sxs-lookup"><span data-stu-id="f8c3d-234">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f8c3d-235">Windows agents</span><span class="sxs-lookup"><span data-stu-id="f8c3d-235">Windows agents</span></span> |<span data-ttu-id="f8c3d-236">Yes</span><span class="sxs-lookup"><span data-stu-id="f8c3d-236">Yes</span></span> |<span data-ttu-id="f8c3d-237">The solution collects information about system updates from Windows agents and then initiates installation of required updates.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-237">The solution collects information about system updates from Windows agents and then initiates installation of required updates.</span></span> |
| <span data-ttu-id="f8c3d-238">Linux agents</span><span class="sxs-lookup"><span data-stu-id="f8c3d-238">Linux agents</span></span> |<span data-ttu-id="f8c3d-239">Yes</span><span class="sxs-lookup"><span data-stu-id="f8c3d-239">Yes</span></span> |<span data-ttu-id="f8c3d-240">The solution collects information about system updates from Linux agents and then initiates installation of required updates on supported distributions.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-240">The solution collects information about system updates from Linux agents and then initiates installation of required updates on supported distributions.</span></span> |
| <span data-ttu-id="f8c3d-241">Operations Manager management group</span><span class="sxs-lookup"><span data-stu-id="f8c3d-241">Operations Manager management group</span></span> |<span data-ttu-id="f8c3d-242">Yes</span><span class="sxs-lookup"><span data-stu-id="f8c3d-242">Yes</span></span> |<span data-ttu-id="f8c3d-243">The solution collects information about system updates from agents in a connected management group.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-243">The solution collects information about system updates from agents in a connected management group.</span></span><br/><span data-ttu-id="f8c3d-244">A direct connection from the Operations Manager agent to Log Analytics isn't required.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-244">A direct connection from the Operations Manager agent to Log Analytics isn't required.</span></span> <span data-ttu-id="f8c3d-245">Data is forwarded from the management group to the Log Analytics workspace.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-245">Data is forwarded from the management group to the Log Analytics workspace.</span></span> |

### <a name="collection-frequency"></a><span data-ttu-id="f8c3d-246">Collection frequency</span><span class="sxs-lookup"><span data-stu-id="f8c3d-246">Collection frequency</span></span>

<span data-ttu-id="f8c3d-247">A scan is performed twice per day for each managed Windows computer.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-247">A scan is performed twice per day for each managed Windows computer.</span></span> <span data-ttu-id="f8c3d-248">Every 15 minutes, the Windows API is called to query for the last update time to determine whether the status has changed.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-248">Every 15 minutes, the Windows API is called to query for the last update time to determine whether the status has changed.</span></span> <span data-ttu-id="f8c3d-249">If the status has changed, a compliance scan is initiated.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-249">If the status has changed, a compliance scan is initiated.</span></span> 

<span data-ttu-id="f8c3d-250">A scan is performed every 3 hours for each managed Linux computer.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-250">A scan is performed every 3 hours for each managed Linux computer.</span></span>

<span data-ttu-id="f8c3d-251">It can take between 30 minutes and 6 hours for the dashboard to display updated data from managed computers.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-251">It can take between 30 minutes and 6 hours for the dashboard to display updated data from managed computers.</span></span>

## <a name="viewing-update-assessments"></a><span data-ttu-id="f8c3d-252">View update assessments</span><span class="sxs-lookup"><span data-stu-id="f8c3d-252">View update assessments</span></span>

<span data-ttu-id="f8c3d-253">In your Automation account, select **Update Management** to view the status of your machines.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-253">In your Automation account, select **Update Management** to view the status of your machines.</span></span>

<span data-ttu-id="f8c3d-254">This view provides information about your machines, missing updates, update deployments, and scheduled update deployments.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-254">This view provides information about your machines, missing updates, update deployments, and scheduled update deployments.</span></span> <span data-ttu-id="f8c3d-255">In the **COMPLIANCE COLUMN**, you can see the last time the machine was assessed.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-255">In the **COMPLIANCE COLUMN**, you can see the last time the machine was assessed.</span></span> <span data-ttu-id="f8c3d-256">In the **UPDATE AGENT READINESS** column, you can see if the health of the update agent.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-256">In the **UPDATE AGENT READINESS** column, you can see if the health of the update agent.</span></span> <span data-ttu-id="f8c3d-257">If there's an issue, select the link to go to troubleshooting documentation that can help you learn what steps to take to correct the problem.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-257">If there's an issue, select the link to go to troubleshooting documentation that can help you learn what steps to take to correct the problem.</span></span>

<span data-ttu-id="f8c3d-258">To run a log search that returns information about the machine, update, or deployment, select the item in the list.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-258">To run a log search that returns information about the machine, update, or deployment, select the item in the list.</span></span> <span data-ttu-id="f8c3d-259">The **Log Search** pane opens with a query for the item selected:</span><span class="sxs-lookup"><span data-stu-id="f8c3d-259">The **Log Search** pane opens with a query for the item selected:</span></span>

![Update Management default view](media/automation-update-management/update-management-view.png)

## <a name="install-updates"></a><span data-ttu-id="f8c3d-261">Install updates</span><span class="sxs-lookup"><span data-stu-id="f8c3d-261">Install updates</span></span>

<span data-ttu-id="f8c3d-262">After updates are assessed for all the Linux and Windows computers in your workspace, you can install required updates by creating an *update deployment*.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-262">After updates are assessed for all the Linux and Windows computers in your workspace, you can install required updates by creating an *update deployment*.</span></span> <span data-ttu-id="f8c3d-263">An update deployment is a scheduled installation of required updates for one or more computers.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-263">An update deployment is a scheduled installation of required updates for one or more computers.</span></span> <span data-ttu-id="f8c3d-264">You specify the date and time for the deployment and a computer or group of computers to include in the scope of a deployment.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-264">You specify the date and time for the deployment and a computer or group of computers to include in the scope of a deployment.</span></span> <span data-ttu-id="f8c3d-265">To learn more about computer groups, see [Computer groups in Log Analytics](../log-analytics/log-analytics-computer-groups.md).</span><span class="sxs-lookup"><span data-stu-id="f8c3d-265">To learn more about computer groups, see [Computer groups in Log Analytics](../log-analytics/log-analytics-computer-groups.md).</span></span>

 <span data-ttu-id="f8c3d-266">When you include computer groups in your update deployment, group membership is evaluated only once, at the time of schedule creation.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-266">When you include computer groups in your update deployment, group membership is evaluated only once, at the time of schedule creation.</span></span> <span data-ttu-id="f8c3d-267">Subsequent changes to a group aren't reflected.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-267">Subsequent changes to a group aren't reflected.</span></span> <span data-ttu-id="f8c3d-268">To work around this, delete the scheduled update deployment and re-create it.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-268">To work around this, delete the scheduled update deployment and re-create it.</span></span>

> [!NOTE]
> <span data-ttu-id="f8c3d-269">Windows virtual machines that are deployed from the Azure Marketplace by default are set to receive automatic updates from Windows Update Service.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-269">Windows virtual machines that are deployed from the Azure Marketplace by default are set to receive automatic updates from Windows Update Service.</span></span> <span data-ttu-id="f8c3d-270">This behavior doesn't change when you add this solution or add Windows virtual machines to your workspace.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-270">This behavior doesn't change when you add this solution or add Windows virtual machines to your workspace.</span></span> <span data-ttu-id="f8c3d-271">If you don't actively manage updates by using this solution, the default behavior (to automatically apply updates) applies.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-271">If you don't actively manage updates by using this solution, the default behavior (to automatically apply updates) applies.</span></span>

<span data-ttu-id="f8c3d-272">To avoid updates being applied outside of a maintenance window on Ubuntu, reconfigure the Unattended-Upgrade package to disable automatic updates.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-272">To avoid updates being applied outside of a maintenance window on Ubuntu, reconfigure the Unattended-Upgrade package to disable automatic updates.</span></span> <span data-ttu-id="f8c3d-273">For information about how to configure the package, see [Automatic Updates topic in the Ubuntu Server Guide](https://help.ubuntu.com/lts/serverguide/automatic-updates.html).</span><span class="sxs-lookup"><span data-stu-id="f8c3d-273">For information about how to configure the package, see [Automatic Updates topic in the Ubuntu Server Guide](https://help.ubuntu.com/lts/serverguide/automatic-updates.html).</span></span>

<span data-ttu-id="f8c3d-274">Virtual machines that were created from the on-demand Red Hat Enterprise Linux (RHEL) images that are available in the Azure Marketplace are registered to access the [Red Hat Update Infrastructure (RHUI)](../virtual-machines/virtual-machines-linux-update-infrastructure-redhat.md) that's deployed in Azure.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-274">Virtual machines that were created from the on-demand Red Hat Enterprise Linux (RHEL) images that are available in the Azure Marketplace are registered to access the [Red Hat Update Infrastructure (RHUI)](../virtual-machines/virtual-machines-linux-update-infrastructure-redhat.md) that's deployed in Azure.</span></span> <span data-ttu-id="f8c3d-275">Any other Linux distribution must be updated from the distribution's online file repository by following the distribution's supported methods.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-275">Any other Linux distribution must be updated from the distribution's online file repository by following the distribution's supported methods.</span></span>

## <a name="view-missing-updates"></a><span data-ttu-id="f8c3d-276">View missing updates</span><span class="sxs-lookup"><span data-stu-id="f8c3d-276">View missing updates</span></span>

<span data-ttu-id="f8c3d-277">Select **Missing updates** to view the list of updates that are missing from your machines.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-277">Select **Missing updates** to view the list of updates that are missing from your machines.</span></span> <span data-ttu-id="f8c3d-278">Each update is listed and can be selected.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-278">Each update is listed and can be selected.</span></span> <span data-ttu-id="f8c3d-279">Information about the number of machines that require the update, the operating system, and a link for more information is shown.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-279">Information about the number of machines that require the update, the operating system, and a link for more information is shown.</span></span> <span data-ttu-id="f8c3d-280">The **Log search** pane shows more details about the updates.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-280">The **Log search** pane shows more details about the updates.</span></span>

## <a name="view-update-deployments"></a><span data-ttu-id="f8c3d-281">View update deployments</span><span class="sxs-lookup"><span data-stu-id="f8c3d-281">View update deployments</span></span>

<span data-ttu-id="f8c3d-282">Select the **Update Deployments** tab to view the list of existing update deployments.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-282">Select the **Update Deployments** tab to view the list of existing update deployments.</span></span> <span data-ttu-id="f8c3d-283">Select any of the update deployments in the table to open the **Update Deployment Run** pane for that update deployment.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-283">Select any of the update deployments in the table to open the **Update Deployment Run** pane for that update deployment.</span></span>

![Overview of update deployment results](./media/automation-update-management/update-deployment-run.png)

## <a name="create-or-edit-an-update-deployment"></a><span data-ttu-id="f8c3d-285">Create or edit an update deployment</span><span class="sxs-lookup"><span data-stu-id="f8c3d-285">Create or edit an update deployment</span></span>

<span data-ttu-id="f8c3d-286">To create a new update deployment, select **Schedule update deployment**.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-286">To create a new update deployment, select **Schedule update deployment**.</span></span> <span data-ttu-id="f8c3d-287">The **New Update Deployment** pane opens.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-287">The **New Update Deployment** pane opens.</span></span> <span data-ttu-id="f8c3d-288">Enter values for the properties described in the following table and then click **Create**:</span><span class="sxs-lookup"><span data-stu-id="f8c3d-288">Enter values for the properties described in the following table and then click **Create**:</span></span>

| <span data-ttu-id="f8c3d-289">Property</span><span class="sxs-lookup"><span data-stu-id="f8c3d-289">Property</span></span> | <span data-ttu-id="f8c3d-290">Description</span><span class="sxs-lookup"><span data-stu-id="f8c3d-290">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f8c3d-291">Name</span><span class="sxs-lookup"><span data-stu-id="f8c3d-291">Name</span></span> |<span data-ttu-id="f8c3d-292">Unique name to identify the update deployment.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-292">Unique name to identify the update deployment.</span></span> |
|<span data-ttu-id="f8c3d-293">Operating System</span><span class="sxs-lookup"><span data-stu-id="f8c3d-293">Operating System</span></span>| <span data-ttu-id="f8c3d-294">Linux or Windows</span><span class="sxs-lookup"><span data-stu-id="f8c3d-294">Linux or Windows</span></span>|
| <span data-ttu-id="f8c3d-295">Machines to update</span><span class="sxs-lookup"><span data-stu-id="f8c3d-295">Machines to update</span></span> |<span data-ttu-id="f8c3d-296">Select a Saved search, Imported group, or pick Machine from the drop-down and select individual machines.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-296">Select a Saved search, Imported group, or pick Machine from the drop-down and select individual machines.</span></span> <span data-ttu-id="f8c3d-297">If you choose **Machines**, the readiness of the machine is shown in the **UPDATE AGENT READINESS** column.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-297">If you choose **Machines**, the readiness of the machine is shown in the **UPDATE AGENT READINESS** column.</span></span></br> <span data-ttu-id="f8c3d-298">To learn about the different methods of creating computer groups in Log Analytics, see [Computer groups in Log Analytics](../log-analytics/log-analytics-computer-groups.md)</span><span class="sxs-lookup"><span data-stu-id="f8c3d-298">To learn about the different methods of creating computer groups in Log Analytics, see [Computer groups in Log Analytics](../log-analytics/log-analytics-computer-groups.md)</span></span> |
|<span data-ttu-id="f8c3d-299">Update classifications</span><span class="sxs-lookup"><span data-stu-id="f8c3d-299">Update classifications</span></span>|<span data-ttu-id="f8c3d-300">Select all the update classifications that you need</span><span class="sxs-lookup"><span data-stu-id="f8c3d-300">Select all the update classifications that you need</span></span>|
|<span data-ttu-id="f8c3d-301">Updates to exclude</span><span class="sxs-lookup"><span data-stu-id="f8c3d-301">Updates to exclude</span></span>|<span data-ttu-id="f8c3d-302">Enter the updates to exclude.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-302">Enter the updates to exclude.</span></span> <span data-ttu-id="f8c3d-303">For  Windows, enter the KB without the 'KB' prefix.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-303">For  Windows, enter the KB without the 'KB' prefix.</span></span> <span data-ttu-id="f8c3d-304">For Linux, enter the package name or use a wildcard.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-304">For Linux, enter the package name or use a wildcard.</span></span>  |
|<span data-ttu-id="f8c3d-305">Schedule settings</span><span class="sxs-lookup"><span data-stu-id="f8c3d-305">Schedule settings</span></span>|<span data-ttu-id="f8c3d-306">Select the time to start, and select either Once or recurring for the recurrence</span><span class="sxs-lookup"><span data-stu-id="f8c3d-306">Select the time to start, and select either Once or recurring for the recurrence</span></span>|
| <span data-ttu-id="f8c3d-307">Maintenance window</span><span class="sxs-lookup"><span data-stu-id="f8c3d-307">Maintenance window</span></span> |<span data-ttu-id="f8c3d-308">Number of minutes set for updates.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-308">Number of minutes set for updates.</span></span> <span data-ttu-id="f8c3d-309">The value can be not be less than 30 minutes and no more than 6 hours</span><span class="sxs-lookup"><span data-stu-id="f8c3d-309">The value can be not be less than 30 minutes and no more than 6 hours</span></span> |
| <span data-ttu-id="f8c3d-310">Reboot control</span><span class="sxs-lookup"><span data-stu-id="f8c3d-310">Reboot control</span></span>| <span data-ttu-id="f8c3d-311">Determines how reboots should be handled.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-311">Determines how reboots should be handled.</span></span> <span data-ttu-id="f8c3d-312">Available options are:</span><span class="sxs-lookup"><span data-stu-id="f8c3d-312">Available options are:</span></span></br><span data-ttu-id="f8c3d-313">Reboot if required (Default)</span><span class="sxs-lookup"><span data-stu-id="f8c3d-313">Reboot if required (Default)</span></span></br><span data-ttu-id="f8c3d-314">Always reboot</span><span class="sxs-lookup"><span data-stu-id="f8c3d-314">Always reboot</span></span></br><span data-ttu-id="f8c3d-315">Never reboot</span><span class="sxs-lookup"><span data-stu-id="f8c3d-315">Never reboot</span></span></br><span data-ttu-id="f8c3d-316">Only reboot - will not install updates</span><span class="sxs-lookup"><span data-stu-id="f8c3d-316">Only reboot - will not install updates</span></span>|

## <a name="update-classifications"></a><span data-ttu-id="f8c3d-317">Update classifications</span><span class="sxs-lookup"><span data-stu-id="f8c3d-317">Update classifications</span></span>

<span data-ttu-id="f8c3d-318">The following tables list the update classifications in Update Management, with a definition for each classification.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-318">The following tables list the update classifications in Update Management, with a definition for each classification.</span></span>

### <a name="windows"></a><span data-ttu-id="f8c3d-319">Windows</span><span class="sxs-lookup"><span data-stu-id="f8c3d-319">Windows</span></span>

|<span data-ttu-id="f8c3d-320">Classification</span><span class="sxs-lookup"><span data-stu-id="f8c3d-320">Classification</span></span>  |<span data-ttu-id="f8c3d-321">Description</span><span class="sxs-lookup"><span data-stu-id="f8c3d-321">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="f8c3d-322">Critical updates</span><span class="sxs-lookup"><span data-stu-id="f8c3d-322">Critical updates</span></span>     | <span data-ttu-id="f8c3d-323">An update for a specific problem that addresses a critical, non-security-related bug.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-323">An update for a specific problem that addresses a critical, non-security-related bug.</span></span>        |
|<span data-ttu-id="f8c3d-324">Security updates</span><span class="sxs-lookup"><span data-stu-id="f8c3d-324">Security updates</span></span>     | <span data-ttu-id="f8c3d-325">An update for a product-specific, security-related issue.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-325">An update for a product-specific, security-related issue.</span></span>        |
|<span data-ttu-id="f8c3d-326">Update rollups</span><span class="sxs-lookup"><span data-stu-id="f8c3d-326">Update rollups</span></span>     | <span data-ttu-id="f8c3d-327">A cumulative set of hotfixes that are packaged together for easy deployment.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-327">A cumulative set of hotfixes that are packaged together for easy deployment.</span></span>        |
|<span data-ttu-id="f8c3d-328">Feature packs</span><span class="sxs-lookup"><span data-stu-id="f8c3d-328">Feature packs</span></span>     | <span data-ttu-id="f8c3d-329">New product features that are distributed outside a product release.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-329">New product features that are distributed outside a product release.</span></span>        |
|<span data-ttu-id="f8c3d-330">Service packs</span><span class="sxs-lookup"><span data-stu-id="f8c3d-330">Service packs</span></span>     | <span data-ttu-id="f8c3d-331">A cumulative set of hotfixes that are applied to an application.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-331">A cumulative set of hotfixes that are applied to an application.</span></span>        |
|<span data-ttu-id="f8c3d-332">Definition updates</span><span class="sxs-lookup"><span data-stu-id="f8c3d-332">Definition updates</span></span>     | <span data-ttu-id="f8c3d-333">An update to virus or other definition files.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-333">An update to virus or other definition files.</span></span>        |
|<span data-ttu-id="f8c3d-334">Tools</span><span class="sxs-lookup"><span data-stu-id="f8c3d-334">Tools</span></span>     | <span data-ttu-id="f8c3d-335">A utility or feature that helps complete one or more tasks.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-335">A utility or feature that helps complete one or more tasks.</span></span>        |
|<span data-ttu-id="f8c3d-336">Updates</span><span class="sxs-lookup"><span data-stu-id="f8c3d-336">Updates</span></span>     | <span data-ttu-id="f8c3d-337">An update to an application or file that currently is installed.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-337">An update to an application or file that currently is installed.</span></span>        |

### <a name="linux"></a><span data-ttu-id="f8c3d-338">Linux</span><span class="sxs-lookup"><span data-stu-id="f8c3d-338">Linux</span></span>

|<span data-ttu-id="f8c3d-339">Classification</span><span class="sxs-lookup"><span data-stu-id="f8c3d-339">Classification</span></span>  |<span data-ttu-id="f8c3d-340">Description</span><span class="sxs-lookup"><span data-stu-id="f8c3d-340">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="f8c3d-341">Critical and security updates</span><span class="sxs-lookup"><span data-stu-id="f8c3d-341">Critical and security updates</span></span>     | <span data-ttu-id="f8c3d-342">Updates for a specific problem or a product-specific, security-related issue.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-342">Updates for a specific problem or a product-specific, security-related issue.</span></span>         |
|<span data-ttu-id="f8c3d-343">Other updates</span><span class="sxs-lookup"><span data-stu-id="f8c3d-343">Other updates</span></span>     | <span data-ttu-id="f8c3d-344">All other updates that aren't critical in nature or aren't security updates.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-344">All other updates that aren't critical in nature or aren't security updates.</span></span>        |

<span data-ttu-id="f8c3d-345">For Linux, Update Management can distinguish between critical and security updates in the cloud while displaying assessment data due to data enrichment in the cloud.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-345">For Linux, Update Management can distinguish between critical and security updates in the cloud while displaying assessment data due to data enrichment in the cloud.</span></span> <span data-ttu-id="f8c3d-346">For patching, Update Management relies on classification data available on the machine.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-346">For patching, Update Management relies on classification data available on the machine.</span></span> <span data-ttu-id="f8c3d-347">Unlike other distributions, CentOS does not have this information available out of the box.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-347">Unlike other distributions, CentOS does not have this information available out of the box.</span></span> <span data-ttu-id="f8c3d-348">If you have CentOS machines configured in a way to return security data for the following command, Update Management will be able to patch based on classifications.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-348">If you have CentOS machines configured in a way to return security data for the following command, Update Management will be able to patch based on classifications.</span></span>

```bash
sudo yum -q --security check-update
```

<span data-ttu-id="f8c3d-349">There is currently no method supported method to enable native classification-data availability on CentOS.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-349">There is currently no method supported method to enable native classification-data availability on CentOS.</span></span> <span data-ttu-id="f8c3d-350">At this time, only best-effort support is provided to customers who may have enabled this on their own.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-350">At this time, only best-effort support is provided to customers who may have enabled this on their own.</span></span>

## <a name="ports"></a><span data-ttu-id="f8c3d-351">Ports</span><span class="sxs-lookup"><span data-stu-id="f8c3d-351">Ports</span></span>

<span data-ttu-id="f8c3d-352">The following addresses are required specifically for Update Management.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-352">The following addresses are required specifically for Update Management.</span></span> <span data-ttu-id="f8c3d-353">Communication to these addresses occurs over port 443.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-353">Communication to these addresses occurs over port 443.</span></span>

|<span data-ttu-id="f8c3d-354">Azure Public</span><span class="sxs-lookup"><span data-stu-id="f8c3d-354">Azure Public</span></span>  |<span data-ttu-id="f8c3d-355">Azure Government</span><span class="sxs-lookup"><span data-stu-id="f8c3d-355">Azure Government</span></span>  |
|---------|---------|
|<span data-ttu-id="f8c3d-356">\*.ods.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="f8c3d-356">\*.ods.opinsights.azure.com</span></span>     |<span data-ttu-id="f8c3d-357">\*.ods.opinsights.azure.us</span><span class="sxs-lookup"><span data-stu-id="f8c3d-357">\*.ods.opinsights.azure.us</span></span>         |
|<span data-ttu-id="f8c3d-358">\*.oms.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="f8c3d-358">\*.oms.opinsights.azure.com</span></span>     | <span data-ttu-id="f8c3d-359">\*.oms.opinsights.azure.us</span><span class="sxs-lookup"><span data-stu-id="f8c3d-359">\*.oms.opinsights.azure.us</span></span>        |
|<span data-ttu-id="f8c3d-360">\*.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="f8c3d-360">\*.blob.core.windows.net</span></span>|<span data-ttu-id="f8c3d-361">\*.blob.core.usgovcloudapi.net</span><span class="sxs-lookup"><span data-stu-id="f8c3d-361">\*.blob.core.usgovcloudapi.net</span></span>|

<span data-ttu-id="f8c3d-362">For more information about ports that the Hybrid Runbook Worker requires, see [Hybrid Worker role ports](automation-hybrid-runbook-worker.md#hybrid-worker-role).</span><span class="sxs-lookup"><span data-stu-id="f8c3d-362">For more information about ports that the Hybrid Runbook Worker requires, see [Hybrid Worker role ports](automation-hybrid-runbook-worker.md#hybrid-worker-role).</span></span>

<span data-ttu-id="f8c3d-363">It is recommended to use the addresses listed when defining exceptions.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-363">It is recommended to use the addresses listed when defining exceptions.</span></span> <span data-ttu-id="f8c3d-364">For IP addresses you can download the [Microsoft Azure Datacenter IP Ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="f8c3d-364">For IP addresses you can download the [Microsoft Azure Datacenter IP Ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span></span> <span data-ttu-id="f8c3d-365">This file is updated weekly, and reflects the currently deployed ranges and any upcoming changes to the IP ranges.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-365">This file is updated weekly, and reflects the currently deployed ranges and any upcoming changes to the IP ranges.</span></span>

## <a name="search-logs"></a><span data-ttu-id="f8c3d-366">Search logs</span><span class="sxs-lookup"><span data-stu-id="f8c3d-366">Search logs</span></span>

<span data-ttu-id="f8c3d-367">In addition to the details that are provided in the Azure portal, you can do searches against the logs.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-367">In addition to the details that are provided in the Azure portal, you can do searches against the logs.</span></span> <span data-ttu-id="f8c3d-368">On the solution pages, select **Log Analytics**.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-368">On the solution pages, select **Log Analytics**.</span></span> <span data-ttu-id="f8c3d-369">The **Log Search** pane opens.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-369">The **Log Search** pane opens.</span></span>

<span data-ttu-id="f8c3d-370">You can also learn how to customize the queries or use them from different clients and more by visiting:  [Log Analytics seach API documentation](
https://dev.loganalytics.io/).</span><span class="sxs-lookup"><span data-stu-id="f8c3d-370">You can also learn how to customize the queries or use them from different clients and more by visiting:  [Log Analytics seach API documentation](
https://dev.loganalytics.io/).</span></span>

### <a name="sample-queries"></a><span data-ttu-id="f8c3d-371">Sample queries</span><span class="sxs-lookup"><span data-stu-id="f8c3d-371">Sample queries</span></span>

<span data-ttu-id="f8c3d-372">The following sections provide sample log queries for update records that are collected by this solution:</span><span class="sxs-lookup"><span data-stu-id="f8c3d-372">The following sections provide sample log queries for update records that are collected by this solution:</span></span>

#### <a name="single-azure-vm-assessment-queries-windows"></a><span data-ttu-id="f8c3d-373">Single Azure VM Assessment queries (Windows)</span><span class="sxs-lookup"><span data-stu-id="f8c3d-373">Single Azure VM Assessment queries (Windows)</span></span>

<span data-ttu-id="f8c3d-374">Replace the VMUUID value with the VM GUID of the virtual machine you are querying.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-374">Replace the VMUUID value with the VM GUID of the virtual machine you are querying.</span></span> <span data-ttu-id="f8c3d-375">You can find the VMUUID that should be used by running the following query in Log Analytics: `Update | where Computer == "<machine name>" | summarize by Computer, VMUUID`</span><span class="sxs-lookup"><span data-stu-id="f8c3d-375">You can find the VMUUID that should be used by running the following query in Log Analytics: `Update | where Computer == "<machine name>" | summarize by Computer, VMUUID`</span></span>

##### <a name="missing-updates-summary"></a><span data-ttu-id="f8c3d-376">Missing updates summary</span><span class="sxs-lookup"><span data-stu-id="f8c3d-376">Missing updates summary</span></span>

```
Update
| where TimeGenerated>ago(14h) and OSType!="Linux" and (Optional==false or Classification has "Critical" or Classification has "Security") and VMUUID=~"b08d5afa-1471-4b52-bd95-a44fea6e4ca8"
| summarize hint.strategy=partitioned arg_max(TimeGenerated, UpdateState, Classification, Approved) by Computer, SourceComputerId, UpdateID
| where UpdateState=~"Needed" and Approved!=false
| summarize by UpdateID, Classification
| summarize allUpdatesCount=count(), criticalUpdatesCount=countif(Classification has "Critical"), securityUpdatesCount=countif(Classification has "Security"), otherUpdatesCount=countif(Classification !has "Critical" and Classification !has "Security"
```

##### <a name="missing-updates-list"></a><span data-ttu-id="f8c3d-377">Missing updates list</span><span class="sxs-lookup"><span data-stu-id="f8c3d-377">Missing updates list</span></span>

```
Update
| where TimeGenerated>ago(14h) and OSType!="Linux" and (Optional==false or Classification has "Critical" or Classification has "Security") and VMUUID=~"8bf1ccc6-b6d3-4a0b-a643-23f346dfdf82"
| summarize hint.strategy=partitioned arg_max(TimeGenerated, UpdateState, Classification, Title, KBID, PublishedDate, Approved) by Computer, SourceComputerId, UpdateID
| where UpdateState=~"Needed" and Approved!=false
| project-away UpdateState, Approved, TimeGenerated
| summarize computersCount=dcount(SourceComputerId, 2), displayName=any(Title), publishedDate=min(PublishedDate), ClassificationWeight=max(iff(Classification has "Critical", 4, iff(Classification has "Security", 2, 1))) by id=strcat(UpdateID, "_", KBID), classification=Classification, InformationId=strcat("KB", KBID), InformationUrl=iff(isnotempty(KBID), strcat("https://support.microsoft.com/kb/", KBID), ""), osType=2
| sort by ClassificationWeight desc, computersCount desc, displayName asc
| extend informationLink=(iff(isnotempty(InformationId) and isnotempty(InformationUrl), toobject(strcat('{ "uri": "', InformationUrl, '", "text": "', InformationId, '", "target": "blank" }')), toobject('')))
| project-away ClassificationWeight, InformationId, InformationUrl
```

#### <a name="single-azure-vm-assessment-queries-linux"></a><span data-ttu-id="f8c3d-378">Single Azure VM assessment queries (Linux)</span><span class="sxs-lookup"><span data-stu-id="f8c3d-378">Single Azure VM assessment queries (Linux)</span></span>

<span data-ttu-id="f8c3d-379">For some Linux distros, there is a [endianness](https://en.wikipedia.org/wiki/Endianness) mismatch with the VMUUID value that comes from Azure Resource Manager and what is stored in Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-379">For some Linux distros, there is a [endianness](https://en.wikipedia.org/wiki/Endianness) mismatch with the VMUUID value that comes from Azure Resource Manager and what is stored in Log Analytics.</span></span> <span data-ttu-id="f8c3d-380">The following query checks for a match on either endianness.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-380">The following query checks for a match on either endianness.</span></span> <span data-ttu-id="f8c3d-381">Replace the VMUUID values with the big-endian and little-endian format of the GUID to properly return the results.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-381">Replace the VMUUID values with the big-endian and little-endian format of the GUID to properly return the results.</span></span> <span data-ttu-id="f8c3d-382">You can find the VMUUID that should be used by running the following query in Log Analytics: `Update | where Computer == "<machine name>"
| summarize by Computer, VMUUID`</span><span class="sxs-lookup"><span data-stu-id="f8c3d-382">You can find the VMUUID that should be used by running the following query in Log Analytics: `Update | where Computer == "<machine name>"
| summarize by Computer, VMUUID`</span></span>

##### <a name="missing-updates-summary"></a><span data-ttu-id="f8c3d-383">Missing updates summary</span><span class="sxs-lookup"><span data-stu-id="f8c3d-383">Missing updates summary</span></span>

```
Update
| where TimeGenerated>ago(5h) and OSType=="Linux" and (VMUUID=~"625686a0-6d08-4810-aae9-a089e68d4911" or VMUUID=~"a0865662-086d-1048-aae9-a089e68d4911")
| summarize hint.strategy=partitioned arg_max(TimeGenerated, UpdateState, Classification) by Computer, SourceComputerId, Product, ProductArch
| where UpdateState=~"Needed"
| summarize by Product, ProductArch, Classification
| summarize allUpdatesCount=count(), criticalUpdatesCount=countif(Classification has "Critical"), securityUpdatesCount=countif(Classification has "Security"), otherUpdatesCount=countif(Classification !has "Critical" and Classification !has "Security")
```

##### <a name="missing-updates-list"></a><span data-ttu-id="f8c3d-384">Missing updates list</span><span class="sxs-lookup"><span data-stu-id="f8c3d-384">Missing updates list</span></span>

```
Update
| where TimeGenerated>ago(5h) and OSType=="Linux" and (VMUUID=~"625686a0-6d08-4810-aae9-a089e68d4911" or VMUUID=~"a0865662-086d-1048-aae9-a089e68d4911")
| summarize hint.strategy=partitioned arg_max(TimeGenerated, UpdateState, Classification, BulletinUrl, BulletinID) by Computer, SourceComputerId, Product, ProductArch
| where UpdateState=~"Needed"
| project-away UpdateState, TimeGenerated
| summarize computersCount=dcount(SourceComputerId, 2), ClassificationWeight=max(iff(Classification has "Critical", 4, iff(Classification has "Security", 2, 1))) by id=strcat(Product, "_", ProductArch), displayName=Product, productArch=ProductArch, classification=Classification, InformationId=BulletinID, InformationUrl=tostring(split(BulletinUrl, ";", 0)[0]), osType=1
| sort by ClassificationWeight desc, computersCount desc, displayName asc
| extend informationLink=(iff(isnotempty(InformationId) and isnotempty(InformationUrl), toobject(strcat('{ "uri": "', InformationUrl, '", "text": "', InformationId, '", "target": "blank" }')), toobject('')))
| project-away ClassificationWeight, InformationId, InformationUrl

```

#### <a name="multi-vm-assessment-queries"></a><span data-ttu-id="f8c3d-385">Multi-VM assessment queries</span><span class="sxs-lookup"><span data-stu-id="f8c3d-385">Multi-VM assessment queries</span></span>

##### <a name="computers-summary"></a><span data-ttu-id="f8c3d-386">Computers summary</span><span class="sxs-lookup"><span data-stu-id="f8c3d-386">Computers summary</span></span>

```
Heartbeat
| where TimeGenerated>ago(12h) and OSType=~"Windows" and notempty(Computer)
| summarize arg_max(TimeGenerated, Solutions) by SourceComputerId
| where Solutions has "updates"
| distinct SourceComputerId
| join kind=leftouter
(
    Update
    | where TimeGenerated>ago(14h) and OSType!="Linux"
    | summarize hint.strategy=partitioned arg_max(TimeGenerated, UpdateState, Approved, Optional, Classification) by SourceComputerId, UpdateID
    | distinct SourceComputerId, Classification, UpdateState, Approved, Optional
    | summarize WorstMissingUpdateSeverity=max(iff(UpdateState=~"Needed" and (Optional==false or Classification has "Critical" or Classification has "Security") and Approved!=false, iff(Classification has "Critical", 4, iff(Classification has "Security", 2, 1)), 0)) by SourceComputerId
)
on SourceComputerId
| extend WorstMissingUpdateSeverity=coalesce(WorstMissingUpdateSeverity, -1)
| summarize computersBySeverity=count() by WorstMissingUpdateSeverity
| union (Heartbeat
| where TimeGenerated>ago(12h) and OSType=="Linux" and notempty(Computer)
| summarize arg_max(TimeGenerated, Solutions) by SourceComputerId
| where Solutions has "updates"
| distinct SourceComputerId
| join kind=leftouter
(
    Update
    | where TimeGenerated>ago(5h) and OSType=="Linux"
    | summarize hint.strategy=partitioned arg_max(TimeGenerated, UpdateState, Classification) by SourceComputerId, Product, ProductArch
    | distinct SourceComputerId, Classification, UpdateState
    | summarize WorstMissingUpdateSeverity=max(iff(UpdateState=~"Needed", iff(Classification has "Critical", 4, iff(Classification has "Security", 2, 1)), 0)) by SourceComputerId
)
on SourceComputerId
| extend WorstMissingUpdateSeverity=coalesce(WorstMissingUpdateSeverity, -1)
| summarize computersBySeverity=count() by WorstMissingUpdateSeverity)
| summarize assessedComputersCount=sumif(computersBySeverity, WorstMissingUpdateSeverity>-1), notAssessedComputersCount=sumif(computersBySeverity, WorstMissingUpdateSeverity==-1), computersNeedCriticalUpdatesCount=sumif(computersBySeverity, WorstMissingUpdateSeverity==4), computersNeedSecurityUpdatesCount=sumif(computersBySeverity, WorstMissingUpdateSeverity==2), computersNeeedOtherUpdatesCount=sumif(computersBySeverity, WorstMissingUpdateSeverity==1), upToDateComputersCount=sumif(computersBySeverity, WorstMissingUpdateSeverity==0)
| summarize assessedComputersCount=sum(assessedComputersCount), computersNeedCriticalUpdatesCount=sum(computersNeedCriticalUpdatesCount),  computersNeedSecurityUpdatesCount=sum(computersNeedSecurityUpdatesCount), computersNeeedOtherUpdatesCount=sum(computersNeeedOtherUpdatesCount), upToDateComputersCount=sum(upToDateComputersCount), notAssessedComputersCount=sum(notAssessedComputersCount)
| extend allComputersCount=assessedComputersCount+notAssessedComputersCount


```

##### <a name="missing-updates-summary"></a><span data-ttu-id="f8c3d-387">Missing updates summary</span><span class="sxs-lookup"><span data-stu-id="f8c3d-387">Missing updates summary</span></span>

```
Update
| where TimeGenerated>ago(5h) and OSType=="Linux" and SourceComputerId in ((Heartbeat
| where TimeGenerated>ago(12h) and OSType=="Linux" and notempty(Computer)
| summarize arg_max(TimeGenerated, Solutions) by SourceComputerId
| where Solutions has "updates"
| distinct SourceComputerId))
| summarize hint.strategy=partitioned arg_max(TimeGenerated, UpdateState, Classification) by Computer, SourceComputerId, Product, ProductArch
| where UpdateState=~"Needed"
| summarize by Product, ProductArch, Classification
| union (Update
| where TimeGenerated>ago(14h) and OSType!="Linux" and (Optional==false or Classification has "Critical" or Classification has "Security") and SourceComputerId in ((Heartbeat
| where TimeGenerated>ago(12h) and OSType=~"Windows" and notempty(Computer)
| summarize arg_max(TimeGenerated, Solutions) by SourceComputerId
| where Solutions has "updates"
| distinct SourceComputerId))
| summarize hint.strategy=partitioned arg_max(TimeGenerated, UpdateState, Classification, Approved) by Computer, SourceComputerId, UpdateID
| where UpdateState=~"Needed" and Approved!=false
| summarize by UpdateID, Classification )
| summarize allUpdatesCount=count(), criticalUpdatesCount=countif(Classification has "Critical"), securityUpdatesCount=countif(Classification has "Security"), otherUpdatesCount=countif(Classification !has "Critical" and Classification !has "Security"
```

##### <a name="computers-list"></a><span data-ttu-id="f8c3d-388">Computers list</span><span class="sxs-lookup"><span data-stu-id="f8c3d-388">Computers list</span></span>

```
Heartbeat
| where TimeGenerated>ago(12h) and OSType=="Linux" and notempty(Computer)
| summarize arg_max(TimeGenerated, Solutions, Computer, ResourceId, ComputerEnvironment, VMUUID) by SourceComputerId
| where Solutions has "updates"
| extend vmuuId=VMUUID, azureResourceId=ResourceId, osType=1, environment=iff(ComputerEnvironment=~"Azure", 1, 2), scopedToUpdatesSolution=true, lastUpdateAgentSeenTime=""
| join kind=leftouter
(
    Update
    | where TimeGenerated>ago(5h) and OSType=="Linux" and SourceComputerId in ((Heartbeat
    | where TimeGenerated>ago(12h) and OSType=="Linux" and notempty(Computer)
    | summarize arg_max(TimeGenerated, Solutions) by SourceComputerId
    | where Solutions has "updates"
    | distinct SourceComputerId))
    | summarize hint.strategy=partitioned arg_max(TimeGenerated, UpdateState, Classification, Product, Computer, ComputerEnvironment) by SourceComputerId, Product, ProductArch
    | summarize Computer=any(Computer), ComputerEnvironment=any(ComputerEnvironment), missingCriticalUpdatesCount=countif(Classification has "Critical" and UpdateState=~"Needed"), missingSecurityUpdatesCount=countif(Classification has "Security" and UpdateState=~"Needed"), missingOtherUpdatesCount=countif(Classification !has "Critical" and Classification !has "Security" and UpdateState=~"Needed"), lastAssessedTime=max(TimeGenerated), lastUpdateAgentSeenTime="" by SourceComputerId
    | extend compliance=iff(missingCriticalUpdatesCount > 0 or missingSecurityUpdatesCount > 0, 2, 1)
    | extend ComplianceOrder=iff(missingCriticalUpdatesCount > 0 or missingSecurityUpdatesCount > 0 or missingOtherUpdatesCount > 0, 1, 3)
)
on SourceComputerId
| project id=SourceComputerId, displayName=Computer, sourceComputerId=SourceComputerId, scopedToUpdatesSolution=true, missingCriticalUpdatesCount=coalesce(missingCriticalUpdatesCount, -1), missingSecurityUpdatesCount=coalesce(missingSecurityUpdatesCount, -1), missingOtherUpdatesCount=coalesce(missingOtherUpdatesCount, -1), compliance=coalesce(compliance, 4), lastAssessedTime, lastUpdateAgentSeenTime, osType=1, environment=iff(ComputerEnvironment=~"Azure", 1, 2), ComplianceOrder=coalesce(ComplianceOrder, 2)
| union(Heartbeat
| where TimeGenerated>ago(12h) and OSType=~"Windows" and notempty(Computer)
| summarize arg_max(TimeGenerated, Solutions, Computer, ResourceId, ComputerEnvironment, VMUUID) by SourceComputerId
| where Solutions has "updates"
| extend vmuuId=VMUUID, azureResourceId=ResourceId, osType=2, environment=iff(ComputerEnvironment=~"Azure", 1, 2), scopedToUpdatesSolution=true, lastUpdateAgentSeenTime=""
| join kind=leftouter
(
    Update
    | where TimeGenerated>ago(14h) and OSType!="Linux" and SourceComputerId in ((Heartbeat
    | where TimeGenerated>ago(12h) and OSType=~"Windows" and notempty(Computer)
    | summarize arg_max(TimeGenerated, Solutions) by SourceComputerId
    | where Solutions has "updates"
    | distinct SourceComputerId))
    | summarize hint.strategy=partitioned arg_max(TimeGenerated, UpdateState, Classification, Title, Optional, Approved, Computer, ComputerEnvironment) by Computer, SourceComputerId, UpdateID
    | summarize Computer=any(Computer), ComputerEnvironment=any(ComputerEnvironment), missingCriticalUpdatesCount=countif(Classification has "Critical" and UpdateState=~"Needed" and Approved!=false), missingSecurityUpdatesCount=countif(Classification has "Security" and UpdateState=~"Needed" and Approved!=false), missingOtherUpdatesCount=countif(Classification !has "Critical" and Classification !has "Security" and UpdateState=~"Needed" and Optional==false and Approved!=false), lastAssessedTime=max(TimeGenerated), lastUpdateAgentSeenTime="" by SourceComputerId
    | extend compliance=iff(missingCriticalUpdatesCount > 0 or missingSecurityUpdatesCount > 0, 2, 1)
    | extend ComplianceOrder=iff(missingCriticalUpdatesCount > 0 or missingSecurityUpdatesCount > 0 or missingOtherUpdatesCount > 0, 1, 3)
)
on SourceComputerId
| project id=SourceComputerId, displayName=Computer, sourceComputerId=SourceComputerId, scopedToUpdatesSolution=true, missingCriticalUpdatesCount=coalesce(missingCriticalUpdatesCount, -1), missingSecurityUpdatesCount=coalesce(missingSecurityUpdatesCount, -1), missingOtherUpdatesCount=coalesce(missingOtherUpdatesCount, -1), compliance=coalesce(compliance, 4), lastAssessedTime, lastUpdateAgentSeenTime, osType=2, environment=iff(ComputerEnvironment=~"Azure", 1, 2), ComplianceOrder=coalesce(ComplianceOrder, 2) )
| order by ComplianceOrder asc, missingCriticalUpdatesCount desc, missingSecurityUpdatesCount desc, missingOtherUpdatesCount desc, displayName asc
| project-away ComplianceOrder
```

##### <a name="missing-updates-list"></a><span data-ttu-id="f8c3d-389">Missing updates list</span><span class="sxs-lookup"><span data-stu-id="f8c3d-389">Missing updates list</span></span>

```
Update
| where TimeGenerated>ago(5h) and OSType=="Linux" and SourceComputerId in ((Heartbeat
| where TimeGenerated>ago(12h) and OSType=="Linux" and notempty(Computer)
| summarize arg_max(TimeGenerated, Solutions) by SourceComputerId
| where Solutions has "updates"
| distinct SourceComputerId))
| summarize hint.strategy=partitioned arg_max(TimeGenerated, UpdateState, Classification, BulletinUrl, BulletinID) by SourceComputerId, Product, ProductArch
| where UpdateState=~"Needed"
| project-away UpdateState, TimeGenerated
| summarize computersCount=dcount(SourceComputerId, 2), ClassificationWeight=max(iff(Classification has "Critical", 4, iff(Classification has "Security", 2, 1))) by id=strcat(Product, "_", ProductArch), displayName=Product, productArch=ProductArch, classification=Classification, InformationId=BulletinID, InformationUrl=tostring(split(BulletinUrl, ";", 0)[0]), osType=1
| union(Update
| where TimeGenerated>ago(14h) and OSType!="Linux" and (Optional==false or Classification has "Critical" or Classification has "Security") and SourceComputerId in ((Heartbeat
| where TimeGenerated>ago(12h) and OSType=~"Windows" and notempty(Computer)
| summarize arg_max(TimeGenerated, Solutions) by SourceComputerId
| where Solutions has "updates"
| distinct SourceComputerId))
| summarize hint.strategy=partitioned arg_max(TimeGenerated, UpdateState, Classification, Title, KBID, PublishedDate, Approved) by Computer, SourceComputerId, UpdateID
| where UpdateState=~"Needed" and Approved!=false
| project-away UpdateState, Approved, TimeGenerated
| summarize computersCount=dcount(SourceComputerId, 2), displayName=any(Title), publishedDate=min(PublishedDate), ClassificationWeight=max(iff(Classification has "Critical", 4, iff(Classification has "Security", 2, 1))) by id=strcat(UpdateID, "_", KBID), classification=Classification, InformationId=strcat("KB", KBID), InformationUrl=iff(isnotempty(KBID), strcat("https://support.microsoft.com/kb/", KBID), ""), osType=2)
| sort by ClassificationWeight desc, computersCount desc, displayName asc
| extend informationLink=(iff(isnotempty(InformationId) and isnotempty(InformationUrl), toobject(strcat('{ "uri": "', InformationUrl, '", "text": "', InformationId, '", "target": "blank" }')), toobject('')))
| project-away ClassificationWeight, InformationId, InformationUrl
```

## <a name="integrate-with-system-center-configuration-manager"></a><span data-ttu-id="f8c3d-390">Integrate with System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="f8c3d-390">Integrate with System Center Configuration Manager</span></span>

<span data-ttu-id="f8c3d-391">Customers who have invested in System Center Configuration Manager for managing PCs, servers, and mobile devices also rely on the strength and maturity of Configuration Manager to help them manage software updates.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-391">Customers who have invested in System Center Configuration Manager for managing PCs, servers, and mobile devices also rely on the strength and maturity of Configuration Manager to help them manage software updates.</span></span> <span data-ttu-id="f8c3d-392">Configuration Manager is part of their software update management (SUM) cycle.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-392">Configuration Manager is part of their software update management (SUM) cycle.</span></span>

<span data-ttu-id="f8c3d-393">To learn how to integrate the management solution with System Center Configuration Manager, see [Integrate System Center Configuration Manager with Update Management](oms-solution-updatemgmt-sccmintegration.md).</span><span class="sxs-lookup"><span data-stu-id="f8c3d-393">To learn how to integrate the management solution with System Center Configuration Manager, see [Integrate System Center Configuration Manager with Update Management](oms-solution-updatemgmt-sccmintegration.md).</span></span>

## <a name="patch-linux-machines"></a><span data-ttu-id="f8c3d-394">Patch Linux machines</span><span class="sxs-lookup"><span data-stu-id="f8c3d-394">Patch Linux machines</span></span>

<span data-ttu-id="f8c3d-395">The following sections explain potential issues with Linux patching.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-395">The following sections explain potential issues with Linux patching.</span></span>

### <a name="unexpected-os-level-upgrades"></a><span data-ttu-id="f8c3d-396">Unexpected OS-level upgrades</span><span class="sxs-lookup"><span data-stu-id="f8c3d-396">Unexpected OS-level upgrades</span></span>

<span data-ttu-id="f8c3d-397">On some Linux variants, such as Red Hat Enterprise Linux, OS-level upgrades might occur via packages.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-397">On some Linux variants, such as Red Hat Enterprise Linux, OS-level upgrades might occur via packages.</span></span> <span data-ttu-id="f8c3d-398">This might lead to Update Management runs where the OS version number changes.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-398">This might lead to Update Management runs where the OS version number changes.</span></span> <span data-ttu-id="f8c3d-399">Because Update Management uses the same methods to update packages that an administrator would use locally on the Linux computer, this behavior is intentional.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-399">Because Update Management uses the same methods to update packages that an administrator would use locally on the Linux computer, this behavior is intentional.</span></span>

<span data-ttu-id="f8c3d-400">To avoid updating the OS version via Update Management runs, use the **Exclusion** feature.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-400">To avoid updating the OS version via Update Management runs, use the **Exclusion** feature.</span></span>

<span data-ttu-id="f8c3d-401">In Red Hat Enterprise Linux, the package name to exclude is redhat-release-server.x86_64.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-401">In Red Hat Enterprise Linux, the package name to exclude is redhat-release-server.x86_64.</span></span>

![Packages to exclude for Linux](./media/automation-update-management/linuxpatches.png)

### <a name="critical--security-patches-arent-applied"></a><span data-ttu-id="f8c3d-403">Critical / security patches aren't applied</span><span class="sxs-lookup"><span data-stu-id="f8c3d-403">Critical / security patches aren't applied</span></span>

<span data-ttu-id="f8c3d-404">When you deploy updates to a Linux machine, you can select update classifications.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-404">When you deploy updates to a Linux machine, you can select update classifications.</span></span> <span data-ttu-id="f8c3d-405">This filters the updates that are applied to those that meet the specified criteria.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-405">This filters the updates that are applied to those that meet the specified criteria.</span></span> <span data-ttu-id="f8c3d-406">This filter is applied locally on the machine when the update is deployed.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-406">This filter is applied locally on the machine when the update is deployed.</span></span>

<span data-ttu-id="f8c3d-407">Because Update Management performs update enrichment in the cloud, some updates might be flagged in Update Management as having security impact, even though the local machine doesn't have that information.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-407">Because Update Management performs update enrichment in the cloud, some updates might be flagged in Update Management as having security impact, even though the local machine doesn't have that information.</span></span> <span data-ttu-id="f8c3d-408">As a result, if you apply critical updates to a Linux machine, there might be updates that aren't marked as having security impact on that machine and the updates aren't applied.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-408">As a result, if you apply critical updates to a Linux machine, there might be updates that aren't marked as having security impact on that machine and the updates aren't applied.</span></span>

<span data-ttu-id="f8c3d-409">However, Update Management might still report that machine as being non-compliant because it has additional information about the relevant update.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-409">However, Update Management might still report that machine as being non-compliant because it has additional information about the relevant update.</span></span>

<span data-ttu-id="f8c3d-410">Deploying updates by update classification does not work on CentOS out of the box.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-410">Deploying updates by update classification does not work on CentOS out of the box.</span></span> <span data-ttu-id="f8c3d-411">For SUSE, selecting *only* 'Other updates' as the classification may result in some security updates also being installed if security updates related to zypper (package manager) or its dependencies are required first.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-411">For SUSE, selecting *only* 'Other updates' as the classification may result in some security updates also being installed if security updates related to zypper (package manager) or its dependencies are required first.</span></span> <span data-ttu-id="f8c3d-412">This is a limitation of zypper.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-412">This is a limitation of zypper.</span></span> <span data-ttu-id="f8c3d-413">In some cases, you may be required to rerun the update deployment, to verify check the update log.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-413">In some cases, you may be required to rerun the update deployment, to verify check the update log.</span></span>

## <a name="troubleshoot"></a><span data-ttu-id="f8c3d-414">Troubleshoot</span><span class="sxs-lookup"><span data-stu-id="f8c3d-414">Troubleshoot</span></span>

<span data-ttu-id="f8c3d-415">To learn how to troubleshoot your Update Management, see [Troubleshooting Update Management](troubleshoot/update-management.md)</span><span class="sxs-lookup"><span data-stu-id="f8c3d-415">To learn how to troubleshoot your Update Management, see [Troubleshooting Update Management](troubleshoot/update-management.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="f8c3d-416">Next steps</span><span class="sxs-lookup"><span data-stu-id="f8c3d-416">Next steps</span></span>

<span data-ttu-id="f8c3d-417">Continue to the tutorial to learn how to manage updates for your Windows virtual machines.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-417">Continue to the tutorial to learn how to manage updates for your Windows virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f8c3d-418">Manage updates and patches for your Azure Windows VMs</span><span class="sxs-lookup"><span data-stu-id="f8c3d-418">Manage updates and patches for your Azure Windows VMs</span></span>](automation-tutorial-update-management.md)

* <span data-ttu-id="f8c3d-419">Use log searches in [Log Analytics](../log-analytics/log-analytics-log-searches.md) to view detailed update data.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-419">Use log searches in [Log Analytics](../log-analytics/log-analytics-log-searches.md) to view detailed update data.</span></span>
* <span data-ttu-id="f8c3d-420">[Create alerts](../log-analytics/log-analytics-alerts.md) when critical updates are detected as missing from computers or if a computer has automatic updates disabled.</span><span class="sxs-lookup"><span data-stu-id="f8c3d-420">[Create alerts](../log-analytics/log-analytics-alerts.md) when critical updates are detected as missing from computers or if a computer has automatic updates disabled.</span></span>
