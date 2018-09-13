---
title: Azure Automation Linux Hybrid Runbook Worker
description: This article provides information on installing an Azure Automation Hybrid Runbook Worker so you can run runbooks on Linux-based computers in your local datacenter or cloud environment.
services: automation
ms.service: automation
ms.component: process-automation
author: georgewallace
ms.author: gwallace
ms.date: 06/28/2018
ms.topic: conceptual
manager: carmonm
ms.openlocfilehash: 0c677b88228097efcaa30399160dfdafa1c01788
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869003"
---
# <a name="deploy-a-linux-hybrid-runbook-worker"></a><span data-ttu-id="7292c-103">Deploy a Linux Hybrid Runbook Worker</span><span class="sxs-lookup"><span data-stu-id="7292c-103">Deploy a Linux Hybrid Runbook Worker</span></span>

<span data-ttu-id="7292c-104">You can use the Hybrid Runbook Worker feature of Azure Automation to run runbooks directly on the computer that's hosting the role and against resources in the environment to manage those local resources.</span><span class="sxs-lookup"><span data-stu-id="7292c-104">You can use the Hybrid Runbook Worker feature of Azure Automation to run runbooks directly on the computer that's hosting the role and against resources in the environment to manage those local resources.</span></span> <span data-ttu-id="7292c-105">The Linux Hybrid Runbook Worker executes runbooks as a special user that can be elevated for running commands that need elevation.</span><span class="sxs-lookup"><span data-stu-id="7292c-105">The Linux Hybrid Runbook Worker executes runbooks as a special user that can be elevated for running commands that need elevation.</span></span> <span data-ttu-id="7292c-106">Runbooks are stored and managed in Azure Automation and then delivered to one or more designated computers.</span><span class="sxs-lookup"><span data-stu-id="7292c-106">Runbooks are stored and managed in Azure Automation and then delivered to one or more designated computers.</span></span>

<span data-ttu-id="7292c-107">This article describes how to install the Hybrid Runbook Worker on a Linux machine.</span><span class="sxs-lookup"><span data-stu-id="7292c-107">This article describes how to install the Hybrid Runbook Worker on a Linux machine.</span></span>

## <a name="supported-linux-operating-systems"></a><span data-ttu-id="7292c-108">Supported Linux operating systems</span><span class="sxs-lookup"><span data-stu-id="7292c-108">Supported Linux operating systems</span></span>

<span data-ttu-id="7292c-109">The Hybrid Runbook Worker feature supports the following distributions:</span><span class="sxs-lookup"><span data-stu-id="7292c-109">The Hybrid Runbook Worker feature supports the following distributions:</span></span>

* <span data-ttu-id="7292c-110">Amazon Linux 2012.09 to 2015.09 (x86/x64)</span><span class="sxs-lookup"><span data-stu-id="7292c-110">Amazon Linux 2012.09 to 2015.09 (x86/x64)</span></span>
* <span data-ttu-id="7292c-111">CentOS Linux 5, 6, and 7 (x86/x64)</span><span class="sxs-lookup"><span data-stu-id="7292c-111">CentOS Linux 5, 6, and 7 (x86/x64)</span></span>
* <span data-ttu-id="7292c-112">Oracle Linux 5, 6, and 7 (x86/x64)</span><span class="sxs-lookup"><span data-stu-id="7292c-112">Oracle Linux 5, 6, and 7 (x86/x64)</span></span>
* <span data-ttu-id="7292c-113">Red Hat Enterprise Linux Server 5, 6, and 7 (x86/x64)</span><span class="sxs-lookup"><span data-stu-id="7292c-113">Red Hat Enterprise Linux Server 5, 6, and 7 (x86/x64)</span></span>
* <span data-ttu-id="7292c-114">Debian GNU/Linux 6, 7, and 8 (x86/x64)</span><span class="sxs-lookup"><span data-stu-id="7292c-114">Debian GNU/Linux 6, 7, and 8 (x86/x64)</span></span>
* <span data-ttu-id="7292c-115">Ubuntu 12.04 LTS, 14.04 LTS, and 16.04 LTS (x86/x64)</span><span class="sxs-lookup"><span data-stu-id="7292c-115">Ubuntu 12.04 LTS, 14.04 LTS, and 16.04 LTS (x86/x64)</span></span>
* <span data-ttu-id="7292c-116">SUSE Linux Enterprise Server 11 and 12 (x86/x64)</span><span class="sxs-lookup"><span data-stu-id="7292c-116">SUSE Linux Enterprise Server 11 and 12 (x86/x64)</span></span>

## <a name="installing-a-linux-hybrid-runbook-worker"></a><span data-ttu-id="7292c-117">Installing a Linux Hybrid Runbook Worker</span><span class="sxs-lookup"><span data-stu-id="7292c-117">Installing a Linux Hybrid Runbook Worker</span></span>

<span data-ttu-id="7292c-118">To install and configure a Hybrid Runbook Worker on your Linux computer, you follow a straightforward process to manually install and configure the role.</span><span class="sxs-lookup"><span data-stu-id="7292c-118">To install and configure a Hybrid Runbook Worker on your Linux computer, you follow a straightforward process to manually install and configure the role.</span></span> <span data-ttu-id="7292c-119">It requires enabling the **Automation Hybrid Worker** solution in your Azure Log Analytics workspace and then running a set of commands to register the computer as a worker and add it to a group.</span><span class="sxs-lookup"><span data-stu-id="7292c-119">It requires enabling the **Automation Hybrid Worker** solution in your Azure Log Analytics workspace and then running a set of commands to register the computer as a worker and add it to a group.</span></span>

<span data-ttu-id="7292c-120">The minimum requirements for a Linux Hybrid Runbook Worker are:</span><span class="sxs-lookup"><span data-stu-id="7292c-120">The minimum requirements for a Linux Hybrid Runbook Worker are:</span></span>

* <span data-ttu-id="7292c-121">Two cores</span><span class="sxs-lookup"><span data-stu-id="7292c-121">Two cores</span></span>
* <span data-ttu-id="7292c-122">4 GB of RAM</span><span class="sxs-lookup"><span data-stu-id="7292c-122">4 GB of RAM</span></span>
* <span data-ttu-id="7292c-123">Port 443 (outbound)</span><span class="sxs-lookup"><span data-stu-id="7292c-123">Port 443 (outbound)</span></span>

### <a name="package-requirements"></a><span data-ttu-id="7292c-124">Package requirements</span><span class="sxs-lookup"><span data-stu-id="7292c-124">Package requirements</span></span>

| <span data-ttu-id="7292c-125">**Required package**</span><span class="sxs-lookup"><span data-stu-id="7292c-125">**Required package**</span></span> | <span data-ttu-id="7292c-126">**Description**</span><span class="sxs-lookup"><span data-stu-id="7292c-126">**Description**</span></span> | <span data-ttu-id="7292c-127">**Minimum version**</span><span class="sxs-lookup"><span data-stu-id="7292c-127">**Minimum version**</span></span>|
|--------------------- | --------------------- | -------------------|
|<span data-ttu-id="7292c-128">Glibc</span><span class="sxs-lookup"><span data-stu-id="7292c-128">Glibc</span></span> |<span data-ttu-id="7292c-129">GNU C Library</span><span class="sxs-lookup"><span data-stu-id="7292c-129">GNU C Library</span></span>| <span data-ttu-id="7292c-130">2.5-12</span><span class="sxs-lookup"><span data-stu-id="7292c-130">2.5-12</span></span> |
|<span data-ttu-id="7292c-131">Openssl</span><span class="sxs-lookup"><span data-stu-id="7292c-131">Openssl</span></span>| <span data-ttu-id="7292c-132">OpenSSL Libraries</span><span class="sxs-lookup"><span data-stu-id="7292c-132">OpenSSL Libraries</span></span> | <span data-ttu-id="7292c-133">1.0 (TLS 1.1 and TLS 1.2 are supported</span><span class="sxs-lookup"><span data-stu-id="7292c-133">1.0 (TLS 1.1 and TLS 1.2 are supported</span></span>|
|<span data-ttu-id="7292c-134">Curl</span><span class="sxs-lookup"><span data-stu-id="7292c-134">Curl</span></span> | <span data-ttu-id="7292c-135">cURL web client</span><span class="sxs-lookup"><span data-stu-id="7292c-135">cURL web client</span></span> | <span data-ttu-id="7292c-136">7.15.5</span><span class="sxs-lookup"><span data-stu-id="7292c-136">7.15.5</span></span>|
|<span data-ttu-id="7292c-137">Python-ctypes</span><span class="sxs-lookup"><span data-stu-id="7292c-137">Python-ctypes</span></span> | |
|<span data-ttu-id="7292c-138">PAM</span><span class="sxs-lookup"><span data-stu-id="7292c-138">PAM</span></span> | <span data-ttu-id="7292c-139">Pluggable Authentication Modules</span><span class="sxs-lookup"><span data-stu-id="7292c-139">Pluggable Authentication Modules</span></span>|
| <span data-ttu-id="7292c-140">**Optional package**</span><span class="sxs-lookup"><span data-stu-id="7292c-140">**Optional package**</span></span> | <span data-ttu-id="7292c-141">**Description**</span><span class="sxs-lookup"><span data-stu-id="7292c-141">**Description**</span></span> | <span data-ttu-id="7292c-142">**Minimum version**</span><span class="sxs-lookup"><span data-stu-id="7292c-142">**Minimum version**</span></span>|
| <span data-ttu-id="7292c-143">PowerShell Core</span><span class="sxs-lookup"><span data-stu-id="7292c-143">PowerShell Core</span></span> | <span data-ttu-id="7292c-144">To run PowerShell runbooks, PowerShell needs to be installed, see [Installing PowerShell Core on Linux](/powershell/scripting/setup/installing-powershell-core-on-linux) to learn how to install it.</span><span class="sxs-lookup"><span data-stu-id="7292c-144">To run PowerShell runbooks, PowerShell needs to be installed, see [Installing PowerShell Core on Linux](/powershell/scripting/setup/installing-powershell-core-on-linux) to learn how to install it.</span></span>  | <span data-ttu-id="7292c-145">6.0.0</span><span class="sxs-lookup"><span data-stu-id="7292c-145">6.0.0</span></span> |

### <a name="installation"></a><span data-ttu-id="7292c-146">Installation</span><span class="sxs-lookup"><span data-stu-id="7292c-146">Installation</span></span>

<span data-ttu-id="7292c-147">Before you proceed, note the Log Analytics workspace that your Automation account is linked to.</span><span class="sxs-lookup"><span data-stu-id="7292c-147">Before you proceed, note the Log Analytics workspace that your Automation account is linked to.</span></span> <span data-ttu-id="7292c-148">Also note the primary key for your Automation account.</span><span class="sxs-lookup"><span data-stu-id="7292c-148">Also note the primary key for your Automation account.</span></span> <span data-ttu-id="7292c-149">You can find both from the Azure portal by selecting your Automation account, selecting **Workspace** for the workspace ID, and selecting **Keys** for the primary key.</span><span class="sxs-lookup"><span data-stu-id="7292c-149">You can find both from the Azure portal by selecting your Automation account, selecting **Workspace** for the workspace ID, and selecting **Keys** for the primary key.</span></span> <span data-ttu-id="7292c-150">For information on ports and addresses that you need for the Hybrid Runbook Worker, see [Configuring your network](automation-hybrid-runbook-worker.md#network-planning).</span><span class="sxs-lookup"><span data-stu-id="7292c-150">For information on ports and addresses that you need for the Hybrid Runbook Worker, see [Configuring your network](automation-hybrid-runbook-worker.md#network-planning).</span></span>

1. <span data-ttu-id="7292c-151">Enable the **Automation Hybrid Worker** solution in Azure by using one of the following methods:</span><span class="sxs-lookup"><span data-stu-id="7292c-151">Enable the **Automation Hybrid Worker** solution in Azure by using one of the following methods:</span></span>

   * <span data-ttu-id="7292c-152">Add the **Automation Hybrid Worker** solution to your subscription by using the procedure at [Add Log Analytics management solutions to your workspace](../log-analytics/log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="7292c-152">Add the **Automation Hybrid Worker** solution to your subscription by using the procedure at [Add Log Analytics management solutions to your workspace](../log-analytics/log-analytics-add-solutions.md).</span></span>
   * <span data-ttu-id="7292c-153">Run the following cmdlet:</span><span class="sxs-lookup"><span data-stu-id="7292c-153">Run the following cmdlet:</span></span>

        ```azurepowershell-interactive
         Set-AzureRmOperationalInsightsIntelligencePack -ResourceGroupName  <ResourceGroupName> -WorkspaceName <WorkspaceName> -IntelligencePackName  "AzureAutomation" -Enabled $true
        ```

1. <span data-ttu-id="7292c-154">Install the OMS Agent for Linux by running the following command.</span><span class="sxs-lookup"><span data-stu-id="7292c-154">Install the OMS Agent for Linux by running the following command.</span></span> <span data-ttu-id="7292c-155">Replace \<WorkspaceID\> and \<WorkspaceKey\> with the appropriate values from your workspace.</span><span class="sxs-lookup"><span data-stu-id="7292c-155">Replace \<WorkspaceID\> and \<WorkspaceKey\> with the appropriate values from your workspace.</span></span>

   ```bash
   wget https://raw.githubusercontent.com/Microsoft/OMS-Agent-for-Linux/master/installer/scripts/onboard_agent.sh && sh onboard_agent.sh -w <WorkspaceID> -s <WorkspaceKey>
   ```

1. <span data-ttu-id="7292c-156">Run the following command, changing the values for the parameters *-w*, *-k*, *-g*, and *-e*.</span><span class="sxs-lookup"><span data-stu-id="7292c-156">Run the following command, changing the values for the parameters *-w*, *-k*, *-g*, and *-e*.</span></span> <span data-ttu-id="7292c-157">For the *-g* parameter, replace the value with the name of the Hybrid Runbook Worker group that the new Linux Hybrid Runbook Worker should join.</span><span class="sxs-lookup"><span data-stu-id="7292c-157">For the *-g* parameter, replace the value with the name of the Hybrid Runbook Worker group that the new Linux Hybrid Runbook Worker should join.</span></span> <span data-ttu-id="7292c-158">If the name doesn't exist in your Automation account, a new Hybrid Runbook Worker group is made with that name.</span><span class="sxs-lookup"><span data-stu-id="7292c-158">If the name doesn't exist in your Automation account, a new Hybrid Runbook Worker group is made with that name.</span></span>

   ```bash
   sudo python /opt/microsoft/omsconfig/modules/nxOMSAutomationWorker/DSCResources/MSFT_nxOMSAutomationWorkerResource/automationworker/scripts/onboarding.py --register -w <LogAnalyticsworkspaceId> -k <AutomationSharedKey> -g <hybridgroupname> -e <automationendpoint>
   ```

1. <span data-ttu-id="7292c-159">After the command is completed, the **Hybrid Worker Groups** page in the Azure portal shows the new group and the number of members.</span><span class="sxs-lookup"><span data-stu-id="7292c-159">After the command is completed, the **Hybrid Worker Groups** page in the Azure portal shows the new group and the number of members.</span></span> <span data-ttu-id="7292c-160">If this is an existing group, the number of members is incremented.</span><span class="sxs-lookup"><span data-stu-id="7292c-160">If this is an existing group, the number of members is incremented.</span></span> <span data-ttu-id="7292c-161">You can select the group from the list on the **Hybrid Worker Groups** page and select the **Hybrid Workers** tile.</span><span class="sxs-lookup"><span data-stu-id="7292c-161">You can select the group from the list on the **Hybrid Worker Groups** page and select the **Hybrid Workers** tile.</span></span> <span data-ttu-id="7292c-162">On the **Hybrid Workers** page, you see each member of the group listed.</span><span class="sxs-lookup"><span data-stu-id="7292c-162">On the **Hybrid Workers** page, you see each member of the group listed.</span></span>

## <a name="turning-off-signature-validation"></a><span data-ttu-id="7292c-163">Turning off signature validation</span><span class="sxs-lookup"><span data-stu-id="7292c-163">Turning off signature validation</span></span>

<span data-ttu-id="7292c-164">By default, Linux Hybrid Runbook Workers require signature validation.</span><span class="sxs-lookup"><span data-stu-id="7292c-164">By default, Linux Hybrid Runbook Workers require signature validation.</span></span> <span data-ttu-id="7292c-165">If you run an unsigned runbook against a worker, you see an error that says "Signature validation failed."</span><span class="sxs-lookup"><span data-stu-id="7292c-165">If you run an unsigned runbook against a worker, you see an error that says "Signature validation failed."</span></span> <span data-ttu-id="7292c-166">To turn off signature validation, run the following command.</span><span class="sxs-lookup"><span data-stu-id="7292c-166">To turn off signature validation, run the following command.</span></span> <span data-ttu-id="7292c-167">Replace the second parameter with your Log Analytics workspace ID.</span><span class="sxs-lookup"><span data-stu-id="7292c-167">Replace the second parameter with your Log Analytics workspace ID.</span></span>

 ```bash
 sudo python /opt/microsoft/omsconfig/modules/nxOMSAutomationWorker/DSCResources/MSFT_nxOMSAutomationWorkerResource/automationworker/scripts/require_runbook_signature.py --false <LogAnalyticsworkspaceId>
 ```

## <a name="supported-runbook-types"></a><span data-ttu-id="7292c-168">Supported runbook types</span><span class="sxs-lookup"><span data-stu-id="7292c-168">Supported runbook types</span></span>

<span data-ttu-id="7292c-169">Linux Hybrid Runbook Workers don't support the full set of runbook types in Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="7292c-169">Linux Hybrid Runbook Workers don't support the full set of runbook types in Azure Automation.</span></span>

<span data-ttu-id="7292c-170">The following runbook types work on a Linux Hybrid Worker:</span><span class="sxs-lookup"><span data-stu-id="7292c-170">The following runbook types work on a Linux Hybrid Worker:</span></span>

* <span data-ttu-id="7292c-171">Python 2</span><span class="sxs-lookup"><span data-stu-id="7292c-171">Python 2</span></span>
* <span data-ttu-id="7292c-172">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7292c-172">PowerShell</span></span>

  > [!NOTE]
  > <span data-ttu-id="7292c-173">PowerShell runbooks require PowerShell Core to be installed on the Linux machine.</span><span class="sxs-lookup"><span data-stu-id="7292c-173">PowerShell runbooks require PowerShell Core to be installed on the Linux machine.</span></span> <span data-ttu-id="7292c-174">See [Installing PowerShell Core on Linux](/powershell/scripting/setup/installing-powershell-core-on-linux) to learn how to install it.</span><span class="sxs-lookup"><span data-stu-id="7292c-174">See [Installing PowerShell Core on Linux](/powershell/scripting/setup/installing-powershell-core-on-linux) to learn how to install it.</span></span>

<span data-ttu-id="7292c-175">The following runbook types don't work on a Linux Hybrid Worker:</span><span class="sxs-lookup"><span data-stu-id="7292c-175">The following runbook types don't work on a Linux Hybrid Worker:</span></span>

* <span data-ttu-id="7292c-176">PowerShell Workflow</span><span class="sxs-lookup"><span data-stu-id="7292c-176">PowerShell Workflow</span></span>
* <span data-ttu-id="7292c-177">Graphical</span><span class="sxs-lookup"><span data-stu-id="7292c-177">Graphical</span></span>
* <span data-ttu-id="7292c-178">Graphical PowerShell Workflow</span><span class="sxs-lookup"><span data-stu-id="7292c-178">Graphical PowerShell Workflow</span></span>

## <a name="troubleshoot"></a><span data-ttu-id="7292c-179">Troubleshoot</span><span class="sxs-lookup"><span data-stu-id="7292c-179">Troubleshoot</span></span>

<span data-ttu-id="7292c-180">To learn how to troubleshoot your Hybrid Runbook Workers, see [Troubleshooting Linux Hybrid Runbook Workers](troubleshoot/hybrid-runbook-worker.md#linux)</span><span class="sxs-lookup"><span data-stu-id="7292c-180">To learn how to troubleshoot your Hybrid Runbook Workers, see [Troubleshooting Linux Hybrid Runbook Workers](troubleshoot/hybrid-runbook-worker.md#linux)</span></span>

## <a name="next-steps"></a><span data-ttu-id="7292c-181">Next steps</span><span class="sxs-lookup"><span data-stu-id="7292c-181">Next steps</span></span>

* <span data-ttu-id="7292c-182">To learn how to configure your runbooks to automate processes in your on-premises datacenter or other cloud environment, see [Run runbooks on a Hybrid Runbook Worker](automation-hrw-run-runbooks.md).</span><span class="sxs-lookup"><span data-stu-id="7292c-182">To learn how to configure your runbooks to automate processes in your on-premises datacenter or other cloud environment, see [Run runbooks on a Hybrid Runbook Worker](automation-hrw-run-runbooks.md).</span></span>
* <span data-ttu-id="7292c-183">For instructions on how to remove Hybrid Runbook Workers, see [Remove Azure Automation Hybrid Runbook Workers](automation-hybrid-runbook-worker.md#remove-a-hybrid-runbook-worker).</span><span class="sxs-lookup"><span data-stu-id="7292c-183">For instructions on how to remove Hybrid Runbook Workers, see [Remove Azure Automation Hybrid Runbook Workers](automation-hybrid-runbook-worker.md#remove-a-hybrid-runbook-worker).</span></span>
