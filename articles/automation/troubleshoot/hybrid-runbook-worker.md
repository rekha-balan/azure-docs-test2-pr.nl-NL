---
title: Troubleshooting - Azure Automation Hybrid Runbook Workers
description: This article provides information troubleshooting Azure Automation Hybrid Runbook Workers
services: automation
ms.service: automation
ms.component: ''
author: georgewallace
ms.author: gwallace
ms.date: 06/19/2018
ms.topic: conceptual
manager: carmonm
ms.openlocfilehash: 1cae7253a4bfcb4f83baf003a4d9d3c367d8f014
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866593"
---
# <a name="troubleshoot-hybrid-runbook-workers"></a><span data-ttu-id="16224-103">Troubleshoot Hybrid Runbook Workers</span><span class="sxs-lookup"><span data-stu-id="16224-103">Troubleshoot Hybrid Runbook Workers</span></span>

<span data-ttu-id="16224-104">This article provides information on troubleshooting issues with Hybrid Runbook Workers.</span><span class="sxs-lookup"><span data-stu-id="16224-104">This article provides information on troubleshooting issues with Hybrid Runbook Workers.</span></span>

## <a name="general"></a><span data-ttu-id="16224-105">General</span><span class="sxs-lookup"><span data-stu-id="16224-105">General</span></span>

<span data-ttu-id="16224-106">The Hybrid Runbook Worker depends on an agent to communicate with your Automation account to register the worker, receive runbook jobs, and report status.</span><span class="sxs-lookup"><span data-stu-id="16224-106">The Hybrid Runbook Worker depends on an agent to communicate with your Automation account to register the worker, receive runbook jobs, and report status.</span></span> <span data-ttu-id="16224-107">For Windows, this agent is the Microsoft Monitoring Agent.</span><span class="sxs-lookup"><span data-stu-id="16224-107">For Windows, this agent is the Microsoft Monitoring Agent.</span></span> <span data-ttu-id="16224-108">For Linux, it is the OMS Agent for Linux.</span><span class="sxs-lookup"><span data-stu-id="16224-108">For Linux, it is the OMS Agent for Linux.</span></span>

###<a name="runbook-execution-fails"></a><span data-ttu-id="16224-109">Scenario: Runbook execution fails</span><span class="sxs-lookup"><span data-stu-id="16224-109">Scenario: Runbook execution fails</span></span>

#### <a name="issue"></a><span data-ttu-id="16224-110">Issue</span><span class="sxs-lookup"><span data-stu-id="16224-110">Issue</span></span>

<span data-ttu-id="16224-111">Runbook execution fails and you receive the following error:</span><span class="sxs-lookup"><span data-stu-id="16224-111">Runbook execution fails and you receive the following error:</span></span>

```
"The job action 'Activate' cannot be run, because the process stopped unexpectedly. The job action was attempted three times."
```

<span data-ttu-id="16224-112">Your runbook is suspended shortly after attempting to execute it three times.</span><span class="sxs-lookup"><span data-stu-id="16224-112">Your runbook is suspended shortly after attempting to execute it three times.</span></span> <span data-ttu-id="16224-113">There are conditions, which may interrupt the runbook from completing successfully and the related error message does not include any additional information indicating why.</span><span class="sxs-lookup"><span data-stu-id="16224-113">There are conditions, which may interrupt the runbook from completing successfully and the related error message does not include any additional information indicating why.</span></span>

#### <a name="cause"></a><span data-ttu-id="16224-114">Cause</span><span class="sxs-lookup"><span data-stu-id="16224-114">Cause</span></span>

<span data-ttu-id="16224-115">The following are potential possible causes:</span><span class="sxs-lookup"><span data-stu-id="16224-115">The following are potential possible causes:</span></span>

* <span data-ttu-id="16224-116">The runbooks can't authenticate with local resources</span><span class="sxs-lookup"><span data-stu-id="16224-116">The runbooks can't authenticate with local resources</span></span>

* <span data-ttu-id="16224-117">The hybrid worker is behind a proxy or firewall</span><span class="sxs-lookup"><span data-stu-id="16224-117">The hybrid worker is behind a proxy or firewall</span></span>

* <span data-ttu-id="16224-118">The runbooks can't authenticate with local resources</span><span class="sxs-lookup"><span data-stu-id="16224-118">The runbooks can't authenticate with local resources</span></span>

* <span data-ttu-id="16224-119">The computer designated to run the Hybrid Runbook Worker feature meets the minimum hardware requirements.</span><span class="sxs-lookup"><span data-stu-id="16224-119">The computer designated to run the Hybrid Runbook Worker feature meets the minimum hardware requirements.</span></span>

#### <a name="resolution"></a><span data-ttu-id="16224-120">Resolution</span><span class="sxs-lookup"><span data-stu-id="16224-120">Resolution</span></span>

<span data-ttu-id="16224-121">Verify the computer has outbound access to \*.azure-automation.net on port 443.</span><span class="sxs-lookup"><span data-stu-id="16224-121">Verify the computer has outbound access to \*.azure-automation.net on port 443.</span></span>

<span data-ttu-id="16224-122">Computers running the Hybrid Runbook Worker should meet the minimum hardware requirements before designating it to host this feature.</span><span class="sxs-lookup"><span data-stu-id="16224-122">Computers running the Hybrid Runbook Worker should meet the minimum hardware requirements before designating it to host this feature.</span></span> <span data-ttu-id="16224-123">Otherwise, depending on the resource utilization of other background processes and contention caused by runbooks during execution, the computer becomes over utilized and cause runbook job delays or timeouts.</span><span class="sxs-lookup"><span data-stu-id="16224-123">Otherwise, depending on the resource utilization of other background processes and contention caused by runbooks during execution, the computer becomes over utilized and cause runbook job delays or timeouts.</span></span>

<span data-ttu-id="16224-124">Confirm the computer designated to run the Hybrid Runbook Worker feature meets the minimum hardware requirements.</span><span class="sxs-lookup"><span data-stu-id="16224-124">Confirm the computer designated to run the Hybrid Runbook Worker feature meets the minimum hardware requirements.</span></span> <span data-ttu-id="16224-125">If it does, monitor CPU and memory utilization to determine any correlation between the performance of Hybrid Runbook Worker processes and Windows.</span><span class="sxs-lookup"><span data-stu-id="16224-125">If it does, monitor CPU and memory utilization to determine any correlation between the performance of Hybrid Runbook Worker processes and Windows.</span></span> <span data-ttu-id="16224-126">If there is memory or CPU pressure, this may indicate the need to upgrade or add additional processors, or increase memory to address the resource bottleneck and resolve the error.</span><span class="sxs-lookup"><span data-stu-id="16224-126">If there is memory or CPU pressure, this may indicate the need to upgrade or add additional processors, or increase memory to address the resource bottleneck and resolve the error.</span></span> <span data-ttu-id="16224-127">Alternatively, select a different compute resource that can support the minimum requirements and scale when workload demands indicate an increase is necessary.</span><span class="sxs-lookup"><span data-stu-id="16224-127">Alternatively, select a different compute resource that can support the minimum requirements and scale when workload demands indicate an increase is necessary.</span></span>

<span data-ttu-id="16224-128">Check the **Microsoft-SMA** event log for a corresponding event with description *Win32 Process Exited with code [4294967295]*.</span><span class="sxs-lookup"><span data-stu-id="16224-128">Check the **Microsoft-SMA** event log for a corresponding event with description *Win32 Process Exited with code [4294967295]*.</span></span> <span data-ttu-id="16224-129">The cause of this error is you haven't configured authentication in your runbooks or specified the Run As credentials for the Hybrid worker group.</span><span class="sxs-lookup"><span data-stu-id="16224-129">The cause of this error is you haven't configured authentication in your runbooks or specified the Run As credentials for the Hybrid worker group.</span></span> <span data-ttu-id="16224-130">Review [Runbook permissions](../automation-hrw-run-runbooks.md#runbook-permissions) to confirm you have correctly configured authentication for your runbooks.</span><span class="sxs-lookup"><span data-stu-id="16224-130">Review [Runbook permissions](../automation-hrw-run-runbooks.md#runbook-permissions) to confirm you have correctly configured authentication for your runbooks.</span></span>

## <a name="linux"></a><span data-ttu-id="16224-131">Linux</span><span class="sxs-lookup"><span data-stu-id="16224-131">Linux</span></span>

<span data-ttu-id="16224-132">The Linux Hybrid Runbook Worker depends on the OMS Agent for Linux to communicate with your Automation account to register the worker, receive runbook jobs, and report status.</span><span class="sxs-lookup"><span data-stu-id="16224-132">The Linux Hybrid Runbook Worker depends on the OMS Agent for Linux to communicate with your Automation account to register the worker, receive runbook jobs, and report status.</span></span> <span data-ttu-id="16224-133">If registration of the worker fails, here are some possible causes for the error:</span><span class="sxs-lookup"><span data-stu-id="16224-133">If registration of the worker fails, here are some possible causes for the error:</span></span>

###<a name="oms-agent-not-running"></a><span data-ttu-id="16224-134">Scenario: The OMS Agent for Linux is not running</span><span class="sxs-lookup"><span data-stu-id="16224-134">Scenario: The OMS Agent for Linux is not running</span></span>

<span data-ttu-id="16224-135">If the OMS Agent for Linux is not running, this prevents the Linux Hybrid Runbook Worker from communicating with Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="16224-135">If the OMS Agent for Linux is not running, this prevents the Linux Hybrid Runbook Worker from communicating with Azure Automation.</span></span> <span data-ttu-id="16224-136">Verify the agent is running by entering the following command: `ps -ef | grep python`.</span><span class="sxs-lookup"><span data-stu-id="16224-136">Verify the agent is running by entering the following command: `ps -ef | grep python`.</span></span> <span data-ttu-id="16224-137">You should see output similar to the following, the python processes with **nxautomation** user account.</span><span class="sxs-lookup"><span data-stu-id="16224-137">You should see output similar to the following, the python processes with **nxautomation** user account.</span></span> <span data-ttu-id="16224-138">If the Update Management or Azure Automation solutions are not enabled, none of the following processes are running.</span><span class="sxs-lookup"><span data-stu-id="16224-138">If the Update Management or Azure Automation solutions are not enabled, none of the following processes are running.</span></span>

```bash
nxautom+   8567      1  0 14:45 ?        00:00:00 python /opt/microsoft/omsconfig/modules/nxOMSAutomationWorker/DSCResources/MSFT_nxOMSAutomationWorkerResource/automationworker/worker/main.py /var/opt/microsoft/omsagent/state/automationworker/oms.conf rworkspace:<workspaceId> <Linux hybrid worker version>
nxautom+   8593      1  0 14:45 ?        00:00:02 python /opt/microsoft/omsconfig/modules/nxOMSAutomationWorker/DSCResources/MSFT_nxOMSAutomationWorkerResource/automationworker/worker/hybridworker.py /var/opt/microsoft/omsagent/state/automationworker/worker.conf managed rworkspace:<workspaceId> rversion:<Linux hybrid worker version>
nxautom+   8595      1  0 14:45 ?        00:00:02 python /opt/microsoft/omsconfig/modules/nxOMSAutomationWorker/DSCResources/MSFT_nxOMSAutomationWorkerResource/automationworker/worker/hybridworker.py /var/opt/microsoft/omsagent/<workspaceId>/state/automationworker/diy/worker.conf managed rworkspace:<workspaceId> rversion:<Linux hybrid worker version>
```

<span data-ttu-id="16224-139">The following list shows the processes that are started for a Linux Hybrid Runbook Worker.</span><span class="sxs-lookup"><span data-stu-id="16224-139">The following list shows the processes that are started for a Linux Hybrid Runbook Worker.</span></span> <span data-ttu-id="16224-140">They are all located in the `/var/opt/microsoft/omsagent/state/automationworker/` directory.</span><span class="sxs-lookup"><span data-stu-id="16224-140">They are all located in the `/var/opt/microsoft/omsagent/state/automationworker/` directory.</span></span>

* <span data-ttu-id="16224-141">**oms.conf** - This is the worker manager process, this is started directly from DSC.</span><span class="sxs-lookup"><span data-stu-id="16224-141">**oms.conf** - This is the worker manager process, this is started directly from DSC.</span></span>

* <span data-ttu-id="16224-142">**worker.conf** - This process is the Auto Registered Hybrid worker process, it is started by the worker manager.</span><span class="sxs-lookup"><span data-stu-id="16224-142">**worker.conf** - This process is the Auto Registered Hybrid worker process, it is started by the worker manager.</span></span> <span data-ttu-id="16224-143">This process is used by Update Management and is transparent to the user.</span><span class="sxs-lookup"><span data-stu-id="16224-143">This process is used by Update Management and is transparent to the user.</span></span> <span data-ttu-id="16224-144">This process is not present if the Update Management solution is not enabled on the machine.</span><span class="sxs-lookup"><span data-stu-id="16224-144">This process is not present if the Update Management solution is not enabled on the machine.</span></span>

* <span data-ttu-id="16224-145">**diy/worker.conf** - This process is the DIY hybrid worker process.</span><span class="sxs-lookup"><span data-stu-id="16224-145">**diy/worker.conf** - This process is the DIY hybrid worker process.</span></span> <span data-ttu-id="16224-146">The DIY hybrid worker process is used to execute user runbooks on the Hybrid Runbook Worker.</span><span class="sxs-lookup"><span data-stu-id="16224-146">The DIY hybrid worker process is used to execute user runbooks on the Hybrid Runbook Worker.</span></span> <span data-ttu-id="16224-147">It only differs from the Auto registered Hybrid worker process in the key detail that is uses a different configuration.</span><span class="sxs-lookup"><span data-stu-id="16224-147">It only differs from the Auto registered Hybrid worker process in the key detail that is uses a different configuration.</span></span> <span data-ttu-id="16224-148">This process is not present if the Azure Automation solution is not enabled, and the DIY Linux Hybrid Worker is not registered.</span><span class="sxs-lookup"><span data-stu-id="16224-148">This process is not present if the Azure Automation solution is not enabled, and the DIY Linux Hybrid Worker is not registered.</span></span>

<span data-ttu-id="16224-149">If the OMS Agent for Linux is not running, run the following command to start the service: `sudo /opt/microsoft/omsagent/bin/service_control restart`.</span><span class="sxs-lookup"><span data-stu-id="16224-149">If the OMS Agent for Linux is not running, run the following command to start the service: `sudo /opt/microsoft/omsagent/bin/service_control restart`.</span></span>

###<a name="class-does-not-exist"></a><span data-ttu-id="16224-150">Scenario: The specified class does not exist</span><span class="sxs-lookup"><span data-stu-id="16224-150">Scenario: The specified class does not exist</span></span>

<span data-ttu-id="16224-151">If you see the error: **The specified class does not exist..**</span><span class="sxs-lookup"><span data-stu-id="16224-151">If you see the error: **The specified class does not exist..**</span></span> <span data-ttu-id="16224-152">in the  `/var/opt/microsoft/omsconfig/omsconfig.log` then the OMS Agent for Linux needs to be updated.</span><span class="sxs-lookup"><span data-stu-id="16224-152">in the  `/var/opt/microsoft/omsconfig/omsconfig.log` then the OMS Agent for Linux needs to be updated.</span></span> <span data-ttu-id="16224-153">Run the following command to reinstall the OMS Agent:</span><span class="sxs-lookup"><span data-stu-id="16224-153">Run the following command to reinstall the OMS Agent:</span></span>

```bash
wget https://raw.githubusercontent.com/Microsoft/OMS-Agent-for-Linux/master/installer/scripts/onboard_agent.sh && sh onboard_agent.sh -w <WorkspaceID> -s <WorkspaceKey>
```

## <a name="windows"></a><span data-ttu-id="16224-154">Windows</span><span class="sxs-lookup"><span data-stu-id="16224-154">Windows</span></span>

<span data-ttu-id="16224-155">The Windows Hybrid Runbook Worker depends on the Microsoft Monitoring Agent to communicate with your Automation account to register the worker, receive runbook jobs, and report status.</span><span class="sxs-lookup"><span data-stu-id="16224-155">The Windows Hybrid Runbook Worker depends on the Microsoft Monitoring Agent to communicate with your Automation account to register the worker, receive runbook jobs, and report status.</span></span> <span data-ttu-id="16224-156">If registration of the worker fails, here are some possible causes for the error:</span><span class="sxs-lookup"><span data-stu-id="16224-156">If registration of the worker fails, here are some possible causes for the error:</span></span>

###<a name="mma-not-running"></a><span data-ttu-id="16224-157">Scenario: The Microsoft Monitoring Agent is not running</span><span class="sxs-lookup"><span data-stu-id="16224-157">Scenario: The Microsoft Monitoring Agent is not running</span></span>

#### <a name="issue"></a><span data-ttu-id="16224-158">Issue</span><span class="sxs-lookup"><span data-stu-id="16224-158">Issue</span></span>

<span data-ttu-id="16224-159">The `healthservice` service is not running on the Hybrid Runbook Worker machine.</span><span class="sxs-lookup"><span data-stu-id="16224-159">The `healthservice` service is not running on the Hybrid Runbook Worker machine.</span></span>

#### <a name="cause"></a><span data-ttu-id="16224-160">Cause</span><span class="sxs-lookup"><span data-stu-id="16224-160">Cause</span></span>

<span data-ttu-id="16224-161">If the Microsoft Monitoring Agent Windows service is not running, this prevents the Hybrid Runbook Worker from communicating with Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="16224-161">If the Microsoft Monitoring Agent Windows service is not running, this prevents the Hybrid Runbook Worker from communicating with Azure Automation.</span></span>

#### <a name="resolution"></a><span data-ttu-id="16224-162">Resolution</span><span class="sxs-lookup"><span data-stu-id="16224-162">Resolution</span></span>

<span data-ttu-id="16224-163">Verify the agent is running by entering the following command in PowerShell: `Get-Service healthservice`.</span><span class="sxs-lookup"><span data-stu-id="16224-163">Verify the agent is running by entering the following command in PowerShell: `Get-Service healthservice`.</span></span> <span data-ttu-id="16224-164">If the service is stopped, enter the following command in PowerShell to start the service: `Start-Service healthservice`.</span><span class="sxs-lookup"><span data-stu-id="16224-164">If the service is stopped, enter the following command in PowerShell to start the service: `Start-Service healthservice`.</span></span>

###<a name="event-4502"></a> <span data-ttu-id="16224-165">Event 4502 in Operations Manager log</span><span class="sxs-lookup"><span data-stu-id="16224-165">Event 4502 in Operations Manager log</span></span>

#### <a name="issue"></a><span data-ttu-id="16224-166">Issue</span><span class="sxs-lookup"><span data-stu-id="16224-166">Issue</span></span>

<span data-ttu-id="16224-167">In the **Application and Services Logs\Operations Manager** event log, you see event 4502  and EventMessage containing **Microsoft.EnterpriseManagement.HealthService.AzureAutomation.HybridAgent** with the following description: *The certificate presented by the service \<wsid\>.oms.opinsights.azure.com was not issued by a certificate authority used for Microsoft services. Please contact your network administrator to see if they are running a proxy that intercepts TLS/SSL communication. The article KB3126513 has additional troubleshooting information for connectivity issues.*</span><span class="sxs-lookup"><span data-stu-id="16224-167">In the **Application and Services Logs\Operations Manager** event log, you see event 4502  and EventMessage containing **Microsoft.EnterpriseManagement.HealthService.AzureAutomation.HybridAgent** with the following description: *The certificate presented by the service \<wsid\>.oms.opinsights.azure.com was not issued by a certificate authority used for Microsoft services. Please contact your network administrator to see if they are running a proxy that intercepts TLS/SSL communication. The article KB3126513 has additional troubleshooting information for connectivity issues.*</span></span>

#### <a name="cause"></a><span data-ttu-id="16224-168">Cause</span><span class="sxs-lookup"><span data-stu-id="16224-168">Cause</span></span>

<span data-ttu-id="16224-169">This can be caused by your proxy or network firewall blocking communication to Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="16224-169">This can be caused by your proxy or network firewall blocking communication to Microsoft Azure.</span></span> <span data-ttu-id="16224-170">Verify the computer has outbound access to \*.azure-automation.net on ports 443.</span><span class="sxs-lookup"><span data-stu-id="16224-170">Verify the computer has outbound access to \*.azure-automation.net on ports 443.</span></span>

#### <a name="resolution"></a><span data-ttu-id="16224-171">Resolution</span><span class="sxs-lookup"><span data-stu-id="16224-171">Resolution</span></span>

<span data-ttu-id="16224-172">Logs are stored locally on each hybrid worker at C:\ProgramData\Microsoft\System Center\Orchestrator\7.2\SMA\Sandboxes.</span><span class="sxs-lookup"><span data-stu-id="16224-172">Logs are stored locally on each hybrid worker at C:\ProgramData\Microsoft\System Center\Orchestrator\7.2\SMA\Sandboxes.</span></span> <span data-ttu-id="16224-173">You can check if there are any warning or error events written to the **Application and Services Logs\Microsoft-SMA\Operations** and **Application and Services Logs\Operations Manager** event log that would indicate a connectivity or other issue affecting onboarding of the role to Azure Automation or issue while performing normal operations.</span><span class="sxs-lookup"><span data-stu-id="16224-173">You can check if there are any warning or error events written to the **Application and Services Logs\Microsoft-SMA\Operations** and **Application and Services Logs\Operations Manager** event log that would indicate a connectivity or other issue affecting onboarding of the role to Azure Automation or issue while performing normal operations.</span></span>

<span data-ttu-id="16224-174">[Runbook output and messages](../automation-runbook-output-and-messages.md) are sent to Azure Automation from hybrid workers just like runbook jobs run in the cloud.</span><span class="sxs-lookup"><span data-stu-id="16224-174">[Runbook output and messages](../automation-runbook-output-and-messages.md) are sent to Azure Automation from hybrid workers just like runbook jobs run in the cloud.</span></span> <span data-ttu-id="16224-175">You can also enable the Verbose and Progress streams the same way you would for other runbooks.</span><span class="sxs-lookup"><span data-stu-id="16224-175">You can also enable the Verbose and Progress streams the same way you would for other runbooks.</span></span>

## <a name="next-steps"></a><span data-ttu-id="16224-176">Next steps</span><span class="sxs-lookup"><span data-stu-id="16224-176">Next steps</span></span>

<span data-ttu-id="16224-177">If you did not see your problem or are unable to solve your issue, visit one of the following channels for more support:</span><span class="sxs-lookup"><span data-stu-id="16224-177">If you did not see your problem or are unable to solve your issue, visit one of the following channels for more support:</span></span>

* <span data-ttu-id="16224-178">Get answers from Azure experts through [Azure Forums](https://azure.microsoft.com/support/forums/)</span><span class="sxs-lookup"><span data-stu-id="16224-178">Get answers from Azure experts through [Azure Forums](https://azure.microsoft.com/support/forums/)</span></span>
* <span data-ttu-id="16224-179">Connect with [@AzureSupport](https://twitter.com/azuresupport) – the official Microsoft Azure account for improving customer experience by connecting the Azure community to the right resources: answers, support, and experts.</span><span class="sxs-lookup"><span data-stu-id="16224-179">Connect with [@AzureSupport](https://twitter.com/azuresupport) – the official Microsoft Azure account for improving customer experience by connecting the Azure community to the right resources: answers, support, and experts.</span></span>
* <span data-ttu-id="16224-180">If you need more help, you can file an Azure support incident.</span><span class="sxs-lookup"><span data-stu-id="16224-180">If you need more help, you can file an Azure support incident.</span></span> <span data-ttu-id="16224-181">Go to the [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span><span class="sxs-lookup"><span data-stu-id="16224-181">Go to the [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span></span>
