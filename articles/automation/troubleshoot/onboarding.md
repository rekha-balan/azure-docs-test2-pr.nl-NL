---
title: Troubleshoot errors onboarding Update Management, Change Tracking, and Inventory
description: Learn how to troubleshoot onboarding errors with the Update Management, Change Tracking, and Inventory solutions
services: automation
author: georgewallace
ms.author: gwallace
ms.date: 06/19/2018
ms.topic: conceptual
ms.service: automation
manager: carmonm
ms.openlocfilehash: 044cb56b8991a1eb2dd6a1d35be621f2ffab3250
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871583"
---
# <a name="troubleshoot-errors-when-onboarding-solutions"></a><span data-ttu-id="18539-103">Troubleshoot errors when onboarding solutions</span><span class="sxs-lookup"><span data-stu-id="18539-103">Troubleshoot errors when onboarding solutions</span></span>

<span data-ttu-id="18539-104">You may encounter errors when onboarding solutions like Update Management or Change Tracking and Inventory.</span><span class="sxs-lookup"><span data-stu-id="18539-104">You may encounter errors when onboarding solutions like Update Management or Change Tracking and Inventory.</span></span> <span data-ttu-id="18539-105">This article describes the various errors that may occur and how to resolve them.</span><span class="sxs-lookup"><span data-stu-id="18539-105">This article describes the various errors that may occur and how to resolve them.</span></span>

## <a name="general-errors"></a><span data-ttu-id="18539-106">General Errors</span><span class="sxs-lookup"><span data-stu-id="18539-106">General Errors</span></span>

### <a name="computer-grou-query-format-error"></a><span data-ttu-id="18539-107">Scenario: ComputerGroupQueryFormatError</span><span class="sxs-lookup"><span data-stu-id="18539-107">Scenario: ComputerGroupQueryFormatError</span></span>

#### <a name="issue"></a><span data-ttu-id="18539-108">Issue</span><span class="sxs-lookup"><span data-stu-id="18539-108">Issue</span></span>

<span data-ttu-id="18539-109">This error code means that the saved search computer group query used to target the solution was not formatted correctly.</span><span class="sxs-lookup"><span data-stu-id="18539-109">This error code means that the saved search computer group query used to target the solution was not formatted correctly.</span></span> 

#### <a name="cause"></a><span data-ttu-id="18539-110">Cause</span><span class="sxs-lookup"><span data-stu-id="18539-110">Cause</span></span>

<span data-ttu-id="18539-111">You may have altered the query, or it may have been altered by the system.</span><span class="sxs-lookup"><span data-stu-id="18539-111">You may have altered the query, or it may have been altered by the system.</span></span>

#### <a name="resolution"></a><span data-ttu-id="18539-112">Resolution</span><span class="sxs-lookup"><span data-stu-id="18539-112">Resolution</span></span>

<span data-ttu-id="18539-113">You can delete the query for this solution, and reonboard the solution, which recreates the query.</span><span class="sxs-lookup"><span data-stu-id="18539-113">You can delete the query for this solution, and reonboard the solution, which recreates the query.</span></span> <span data-ttu-id="18539-114">The query can be found within your workspace, under **Saved searches**.</span><span class="sxs-lookup"><span data-stu-id="18539-114">The query can be found within your workspace, under **Saved searches**.</span></span> <span data-ttu-id="18539-115">The name of the query is **MicrosoftDefaultComputerGroup**, and the category of the query is the name of the solution associated with this query.</span><span class="sxs-lookup"><span data-stu-id="18539-115">The name of the query is **MicrosoftDefaultComputerGroup**, and the category of the query is the name of the solution associated with this query.</span></span> <span data-ttu-id="18539-116">If multiple solutions are enabled, the **MicrosoftDefaultComputerGroup** shows multiple times under **Saved Searches**.</span><span class="sxs-lookup"><span data-stu-id="18539-116">If multiple solutions are enabled, the **MicrosoftDefaultComputerGroup** shows multiple times under **Saved Searches**.</span></span>

### <a name="policy-violation"></a><span data-ttu-id="18539-117">Scenario: PolicyViolation</span><span class="sxs-lookup"><span data-stu-id="18539-117">Scenario: PolicyViolation</span></span>

#### <a name="issue"></a><span data-ttu-id="18539-118">Issue</span><span class="sxs-lookup"><span data-stu-id="18539-118">Issue</span></span>

<span data-ttu-id="18539-119">This error code means that the deployment failed due to violation of one or more policies.</span><span class="sxs-lookup"><span data-stu-id="18539-119">This error code means that the deployment failed due to violation of one or more policies.</span></span>

#### <a name="cause"></a><span data-ttu-id="18539-120">Cause</span><span class="sxs-lookup"><span data-stu-id="18539-120">Cause</span></span> 

<span data-ttu-id="18539-121">A policy is in place that is blocking the operation from completing.</span><span class="sxs-lookup"><span data-stu-id="18539-121">A policy is in place that is blocking the operation from completing.</span></span>

#### <a name="resolution"></a><span data-ttu-id="18539-122">Resolution</span><span class="sxs-lookup"><span data-stu-id="18539-122">Resolution</span></span>

<span data-ttu-id="18539-123">In order to successfully deploy the solution, you need to consider altering the indicated policy.</span><span class="sxs-lookup"><span data-stu-id="18539-123">In order to successfully deploy the solution, you need to consider altering the indicated policy.</span></span> <span data-ttu-id="18539-124">As there are many different types of policies that can be defined, the specific changes required depend on the policy that is violated.</span><span class="sxs-lookup"><span data-stu-id="18539-124">As there are many different types of policies that can be defined, the specific changes required depend on the policy that is violated.</span></span> <span data-ttu-id="18539-125">For example, if a policy was defined on a resource group that denied permission to change the contents of certain types of resources within that resource group, you could, for example, do any of the following:</span><span class="sxs-lookup"><span data-stu-id="18539-125">For example, if a policy was defined on a resource group that denied permission to change the contents of certain types of resources within that resource group, you could, for example, do any of the following:</span></span>

* <span data-ttu-id="18539-126">Remove the policy altogether.</span><span class="sxs-lookup"><span data-stu-id="18539-126">Remove the policy altogether.</span></span>
* <span data-ttu-id="18539-127">Try to onboard to a different resource group.</span><span class="sxs-lookup"><span data-stu-id="18539-127">Try to onboard to a different resource group.</span></span>
* <span data-ttu-id="18539-128">Revise the policy, by, for example:</span><span class="sxs-lookup"><span data-stu-id="18539-128">Revise the policy, by, for example:</span></span>
  * <span data-ttu-id="18539-129">Re-targeting the policy to a specific resource (such as to a specific Automation account).</span><span class="sxs-lookup"><span data-stu-id="18539-129">Re-targeting the policy to a specific resource (such as to a specific Automation account).</span></span>
  * <span data-ttu-id="18539-130">Revising the set of resources that policy was configured to deny.</span><span class="sxs-lookup"><span data-stu-id="18539-130">Revising the set of resources that policy was configured to deny.</span></span>

<span data-ttu-id="18539-131">Check the notifications in the top right corner of the Azure portal or navigate to the resource group that contains your automation account and select **Deployments** under **Settings** to view the failed deployment.</span><span class="sxs-lookup"><span data-stu-id="18539-131">Check the notifications in the top right corner of the Azure portal or navigate to the resource group that contains your automation account and select **Deployments** under **Settings** to view the failed deployment.</span></span> <span data-ttu-id="18539-132">To learn more about Azure Policy visit: [Overview of Azure Policy](../../azure-policy/azure-policy-introduction.md?toc=%2fazure%2fautomation%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="18539-132">To learn more about Azure Policy visit: [Overview of Azure Policy](../../azure-policy/azure-policy-introduction.md?toc=%2fazure%2fautomation%2ftoc.json).</span></span>

## <a name="mma-extension-failures"></a><span data-ttu-id="18539-133">MMA Extension failures</span><span class="sxs-lookup"><span data-stu-id="18539-133">MMA Extension failures</span></span>

<span data-ttu-id="18539-134">When deploying a solution, a variety of related resources are deployed.</span><span class="sxs-lookup"><span data-stu-id="18539-134">When deploying a solution, a variety of related resources are deployed.</span></span> <span data-ttu-id="18539-135">One of those resources is the Microsoft Monitoring Agent Extension or OMS Agent for Linux.</span><span class="sxs-lookup"><span data-stu-id="18539-135">One of those resources is the Microsoft Monitoring Agent Extension or OMS Agent for Linux.</span></span> <span data-ttu-id="18539-136">These are Virtual Machine Extensions installed by the virtual machine’s Guest Agent that is responsible for communicating with the configured Operations Management Suite (OMS) Workspace, for the purpose of later coordination of the downloading of binaries and other files that the solution you are onboarding depend on once it begins execution.</span><span class="sxs-lookup"><span data-stu-id="18539-136">These are Virtual Machine Extensions installed by the virtual machine’s Guest Agent that is responsible for communicating with the configured Operations Management Suite (OMS) Workspace, for the purpose of later coordination of the downloading of binaries and other files that the solution you are onboarding depend on once it begins execution.</span></span>
<span data-ttu-id="18539-137">You typically first become aware of MMA or OMS Agent for Linux installation failures from a notification appearing in the Notifications Hub.</span><span class="sxs-lookup"><span data-stu-id="18539-137">You typically first become aware of MMA or OMS Agent for Linux installation failures from a notification appearing in the Notifications Hub.</span></span> <span data-ttu-id="18539-138">Clicking on that notification gives further information about the specific failure.</span><span class="sxs-lookup"><span data-stu-id="18539-138">Clicking on that notification gives further information about the specific failure.</span></span> <span data-ttu-id="18539-139">Navigation to the Resource Groups resource, and then to the Deployments element within it also provides details on the deployment failures that occurred.</span><span class="sxs-lookup"><span data-stu-id="18539-139">Navigation to the Resource Groups resource, and then to the Deployments element within it also provides details on the deployment failures that occurred.</span></span>
<span data-ttu-id="18539-140">Installation of the MMA or OMS Agent for Linux can fail for a variety of reasons, and the steps to take to address these failures vary, depending on the issue.</span><span class="sxs-lookup"><span data-stu-id="18539-140">Installation of the MMA or OMS Agent for Linux can fail for a variety of reasons, and the steps to take to address these failures vary, depending on the issue.</span></span> <span data-ttu-id="18539-141">Specific troubleshooting steps follow.</span><span class="sxs-lookup"><span data-stu-id="18539-141">Specific troubleshooting steps follow.</span></span>

<span data-ttu-id="18539-142">The following section describes various issues that you can encounter when onboarding that cause a failure in the deployment of the MMA extension.</span><span class="sxs-lookup"><span data-stu-id="18539-142">The following section describes various issues that you can encounter when onboarding that cause a failure in the deployment of the MMA extension.</span></span>

### <a name="webclient-exception"></a><span data-ttu-id="18539-143">Scenario: An exception occurred during a WebClient request</span><span class="sxs-lookup"><span data-stu-id="18539-143">Scenario: An exception occurred during a WebClient request</span></span>

<span data-ttu-id="18539-144">The MMA extension on the virtual machine is unable to communicate with external resources and deployment fails.</span><span class="sxs-lookup"><span data-stu-id="18539-144">The MMA extension on the virtual machine is unable to communicate with external resources and deployment fails.</span></span>

#### <a name="issue"></a><span data-ttu-id="18539-145">Issue</span><span class="sxs-lookup"><span data-stu-id="18539-145">Issue</span></span>

<span data-ttu-id="18539-146">The following are examples of error messages that are returned:</span><span class="sxs-lookup"><span data-stu-id="18539-146">The following are examples of error messages that are returned:</span></span>

```
Please verify the VM has a running VM agent, and can establish outbound connections to Azure storage.
```

```
'Manifest download error from https://<endpoint>/<endpointId>/Microsoft.EnterpriseCloud.Monitoring_MicrosoftMonitoringAgent_australiaeast_manifest.xml. Error: UnknownError. An exception occurred during a WebClient request.
```

#### <a name="cause"></a><span data-ttu-id="18539-147">Cause</span><span class="sxs-lookup"><span data-stu-id="18539-147">Cause</span></span>

<span data-ttu-id="18539-148">Some potential causes to this error are:</span><span class="sxs-lookup"><span data-stu-id="18539-148">Some potential causes to this error are:</span></span>

* <span data-ttu-id="18539-149">There is a proxy configured in the VM, that only allows specific ports.</span><span class="sxs-lookup"><span data-stu-id="18539-149">There is a proxy configured in the VM, that only allows specific ports.</span></span>

* <span data-ttu-id="18539-150">A firewall setting has blocked access to the required ports and addresses.</span><span class="sxs-lookup"><span data-stu-id="18539-150">A firewall setting has blocked access to the required ports and addresses.</span></span>

#### <a name="resolution"></a><span data-ttu-id="18539-151">Resolution</span><span class="sxs-lookup"><span data-stu-id="18539-151">Resolution</span></span>

<span data-ttu-id="18539-152">Ensure that you have the proper ports and addresses open for communication.</span><span class="sxs-lookup"><span data-stu-id="18539-152">Ensure that you have the proper ports and addresses open for communication.</span></span> <span data-ttu-id="18539-153">For a list of ports and addresses, see [planning your network](../automation-hybrid-runbook-worker.md#network-planning).</span><span class="sxs-lookup"><span data-stu-id="18539-153">For a list of ports and addresses, see [planning your network](../automation-hybrid-runbook-worker.md#network-planning).</span></span>

### <a name="transient-environment-issue"></a><span data-ttu-id="18539-154">Scenario: Install failed due to transient environment issues</span><span class="sxs-lookup"><span data-stu-id="18539-154">Scenario: Install failed due to transient environment issues</span></span>

<span data-ttu-id="18539-155">The installation of the Microsoft Monitoring Agent extension failed during deployment due to another installation or action blocking the installation</span><span class="sxs-lookup"><span data-stu-id="18539-155">The installation of the Microsoft Monitoring Agent extension failed during deployment due to another installation or action blocking the installation</span></span>

#### <a name="issue"></a><span data-ttu-id="18539-156">Issue</span><span class="sxs-lookup"><span data-stu-id="18539-156">Issue</span></span>

<span data-ttu-id="18539-157">The following are examples of error messages may be returned:</span><span class="sxs-lookup"><span data-stu-id="18539-157">The following are examples of error messages may be returned:</span></span>

```
The Microsoft Monitoring Agent failed to install on this machine. Please try to uninstall and reinstall the extension. If the issue persists, please contact support.
```

```
'Install failed for plugin (name: Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent, version 1.0.11081.4) with exception Command C:\Packages\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\1.0.11081.4\MMAExtensionInstall.exe of Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent has exited with Exit code: 1618'
```

```
'Install failed for plugin (name: Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent, version 1.0.11081.2) with exception Command C:\Packages\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\1.0.11081.2\MMAExtensionInstall.exe of Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent has exited with Exit code: 1601'
```

#### <a name="cause"></a><span data-ttu-id="18539-158">Cause</span><span class="sxs-lookup"><span data-stu-id="18539-158">Cause</span></span>

<span data-ttu-id="18539-159">Some potential causes to this error are:</span><span class="sxs-lookup"><span data-stu-id="18539-159">Some potential causes to this error are:</span></span>

* <span data-ttu-id="18539-160">Another installation is in progress</span><span class="sxs-lookup"><span data-stu-id="18539-160">Another installation is in progress</span></span>
* <span data-ttu-id="18539-161">The system is was triggered to reboot during template deployment</span><span class="sxs-lookup"><span data-stu-id="18539-161">The system is was triggered to reboot during template deployment</span></span>

#### <a name="resolution"></a><span data-ttu-id="18539-162">Resolution</span><span class="sxs-lookup"><span data-stu-id="18539-162">Resolution</span></span>

<span data-ttu-id="18539-163">This error is a transient error in nature.</span><span class="sxs-lookup"><span data-stu-id="18539-163">This error is a transient error in nature.</span></span> <span data-ttu-id="18539-164">Retry the deployment to install the extension.</span><span class="sxs-lookup"><span data-stu-id="18539-164">Retry the deployment to install the extension.</span></span>

### <a name="installation-timeout"></a><span data-ttu-id="18539-165">Scenario: Installation timeout</span><span class="sxs-lookup"><span data-stu-id="18539-165">Scenario: Installation timeout</span></span>

<span data-ttu-id="18539-166">The installation of the MMA extension did not complete due to a timeout.</span><span class="sxs-lookup"><span data-stu-id="18539-166">The installation of the MMA extension did not complete due to a timeout.</span></span>

#### <a name="issue"></a><span data-ttu-id="18539-167">Issue</span><span class="sxs-lookup"><span data-stu-id="18539-167">Issue</span></span>

<span data-ttu-id="18539-168">The following is an example of an error message that may be returned:</span><span class="sxs-lookup"><span data-stu-id="18539-168">The following is an example of an error message that may be returned:</span></span>

```
Install failed for plugin (name: Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent, version 1.0.11081.4) with exception Command C:\Packages\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\1.0.11081.4\MMAExtensionInstall.exe of Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent has exited with Exit code: 15614
```

#### <a name="cause"></a><span data-ttu-id="18539-169">Cause</span><span class="sxs-lookup"><span data-stu-id="18539-169">Cause</span></span>

<span data-ttu-id="18539-170">This error is due to the virtual machine being under a heavy load during installation.</span><span class="sxs-lookup"><span data-stu-id="18539-170">This error is due to the virtual machine being under a heavy load during installation.</span></span>

### <a name="resolution"></a><span data-ttu-id="18539-171">Resolution</span><span class="sxs-lookup"><span data-stu-id="18539-171">Resolution</span></span>

<span data-ttu-id="18539-172">Attempt to install the MMA extension when the VM is under a lower load.</span><span class="sxs-lookup"><span data-stu-id="18539-172">Attempt to install the MMA extension when the VM is under a lower load.</span></span>

## <a name="next-steps"></a><span data-ttu-id="18539-173">Next steps</span><span class="sxs-lookup"><span data-stu-id="18539-173">Next steps</span></span>

<span data-ttu-id="18539-174">If you did not see your problem or are unable to solve your issue, visit one of the following channels for more support:</span><span class="sxs-lookup"><span data-stu-id="18539-174">If you did not see your problem or are unable to solve your issue, visit one of the following channels for more support:</span></span>

* <span data-ttu-id="18539-175">Get answers from Azure experts through [Azure Forums](https://azure.microsoft.com/support/forums/)</span><span class="sxs-lookup"><span data-stu-id="18539-175">Get answers from Azure experts through [Azure Forums](https://azure.microsoft.com/support/forums/)</span></span>
* <span data-ttu-id="18539-176">Connect with [@AzureSupport](https://twitter.com/azuresupport) – the official Microsoft Azure account for improving customer experience by connecting the Azure community to the right resources: answers, support, and experts.</span><span class="sxs-lookup"><span data-stu-id="18539-176">Connect with [@AzureSupport](https://twitter.com/azuresupport) – the official Microsoft Azure account for improving customer experience by connecting the Azure community to the right resources: answers, support, and experts.</span></span>
* <span data-ttu-id="18539-177">If you need more help, you can file an Azure support incident.</span><span class="sxs-lookup"><span data-stu-id="18539-177">If you need more help, you can file an Azure support incident.</span></span> <span data-ttu-id="18539-178">Go to the [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span><span class="sxs-lookup"><span data-stu-id="18539-178">Go to the [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span></span>
