---
title: Troubleshoot errors with Update Management
description: Learn how to troubleshoot issues with Update Management
services: automation
author: georgewallace
ms.author: gwallace
ms.date: 08/08/2018
ms.topic: conceptual
ms.service: automation
manager: carmonm
ms.openlocfilehash: 2e47320d5ad88edfa8ea6122f3a0abd104230974
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867427"
---
# <a name="troubleshooting-issues-with-update-management"></a><span data-ttu-id="78348-103">Troubleshooting issues with Update Management</span><span class="sxs-lookup"><span data-stu-id="78348-103">Troubleshooting issues with Update Management</span></span>

<span data-ttu-id="78348-104">This article discusses solutions to resolve issues that you may encounter when using Update Management.</span><span class="sxs-lookup"><span data-stu-id="78348-104">This article discusses solutions to resolve issues that you may encounter when using Update Management.</span></span>

## <a name="general"></a><span data-ttu-id="78348-105">General</span><span class="sxs-lookup"><span data-stu-id="78348-105">General</span></span>

### <a name="components-enabled-not-working"></a><span data-ttu-id="78348-106">Scenario: The components for the 'Update Management' solution have been enabled, and now this virtual machine is being configured</span><span class="sxs-lookup"><span data-stu-id="78348-106">Scenario: The components for the 'Update Management' solution have been enabled, and now this virtual machine is being configured</span></span>

#### <a name="issue"></a><span data-ttu-id="78348-107">Issue</span><span class="sxs-lookup"><span data-stu-id="78348-107">Issue</span></span>

<span data-ttu-id="78348-108">You continue to see the following message on a virtual machine 15 minutes after onboarding:</span><span class="sxs-lookup"><span data-stu-id="78348-108">You continue to see the following message on a virtual machine 15 minutes after onboarding:</span></span>

```
The components for the 'Update Management' solution have been enabled, and now this virtual machine is being configured. Please be patient, as this can sometimes take up to 15 minutes.
```

#### <a name="cause"></a><span data-ttu-id="78348-109">Cause</span><span class="sxs-lookup"><span data-stu-id="78348-109">Cause</span></span>

<span data-ttu-id="78348-110">This error can be caused by the following reasons:</span><span class="sxs-lookup"><span data-stu-id="78348-110">This error can be caused by the following reasons:</span></span>

1. <span data-ttu-id="78348-111">Communication back to the Automation Account is being blocked.</span><span class="sxs-lookup"><span data-stu-id="78348-111">Communication back to the Automation Account is being blocked.</span></span>
2. <span data-ttu-id="78348-112">The VM being onboarded may have came from a cloned machine that was not sysprepped with the Microsoft Monitoring Agent installed.</span><span class="sxs-lookup"><span data-stu-id="78348-112">The VM being onboarded may have came from a cloned machine that was not sysprepped with the Microsoft Monitoring Agent installed.</span></span>

#### <a name="resolution"></a><span data-ttu-id="78348-113">Resolution</span><span class="sxs-lookup"><span data-stu-id="78348-113">Resolution</span></span>

1. <span data-ttu-id="78348-114">Visit, [Network planning](../automation-hybrid-runbook-worker.md#network-planning) to learn about which addresses and ports need to be allowed for Update Management to work.</span><span class="sxs-lookup"><span data-stu-id="78348-114">Visit, [Network planning](../automation-hybrid-runbook-worker.md#network-planning) to learn about which addresses and ports need to be allowed for Update Management to work.</span></span>
2. <span data-ttu-id="78348-115">If using a cloned image, sysprep the image first and install the MMA agent after the fact.</span><span class="sxs-lookup"><span data-stu-id="78348-115">If using a cloned image, sysprep the image first and install the MMA agent after the fact.</span></span>

## <a name="windows"></a><span data-ttu-id="78348-116">Windows</span><span class="sxs-lookup"><span data-stu-id="78348-116">Windows</span></span>

<span data-ttu-id="78348-117">If you encounter issues while attempting to onboard the solution on a virtual machine, check the **Operations Manager** event log under **Application and Services Logs** on the local machine for events with event ID **4502** and event message containing **Microsoft.EnterpriseManagement.HealthService.AzureAutomation.HybridAgent**.</span><span class="sxs-lookup"><span data-stu-id="78348-117">If you encounter issues while attempting to onboard the solution on a virtual machine, check the **Operations Manager** event log under **Application and Services Logs** on the local machine for events with event ID **4502** and event message containing **Microsoft.EnterpriseManagement.HealthService.AzureAutomation.HybridAgent**.</span></span>

<span data-ttu-id="78348-118">The following section highlights specific error messages and a possible resolution for each.</span><span class="sxs-lookup"><span data-stu-id="78348-118">The following section highlights specific error messages and a possible resolution for each.</span></span> <span data-ttu-id="78348-119">For other onboarding issues see, [troubleshoot solution onboarding](onboarding.md).</span><span class="sxs-lookup"><span data-stu-id="78348-119">For other onboarding issues see, [troubleshoot solution onboarding](onboarding.md).</span></span>

### <a name="machine-already-registered"></a><span data-ttu-id="78348-120">Scenario: Machine is already registered to a different account</span><span class="sxs-lookup"><span data-stu-id="78348-120">Scenario: Machine is already registered to a different account</span></span>

#### <a name="issue"></a><span data-ttu-id="78348-121">Issue</span><span class="sxs-lookup"><span data-stu-id="78348-121">Issue</span></span>

<span data-ttu-id="78348-122">You receive the following error message:</span><span class="sxs-lookup"><span data-stu-id="78348-122">You receive the following error message:</span></span>

```
Unable to Register Machine for Patch Management, Registration Failed with Exception System.InvalidOperationException: {"Message":"Machine is already registered to a different account."}
```

#### <a name="cause"></a><span data-ttu-id="78348-123">Cause</span><span class="sxs-lookup"><span data-stu-id="78348-123">Cause</span></span>

<span data-ttu-id="78348-124">The machine is already onboarded to another workspace for Update Management.</span><span class="sxs-lookup"><span data-stu-id="78348-124">The machine is already onboarded to another workspace for Update Management.</span></span>

#### <a name="resolution"></a><span data-ttu-id="78348-125">Resolution</span><span class="sxs-lookup"><span data-stu-id="78348-125">Resolution</span></span>

<span data-ttu-id="78348-126">Perform cleanup of old artifacts on the machine by [deleting the hybrid runbook group](../automation-hybrid-runbook-worker.md#remove-a-hybrid-worker-group) and try again.</span><span class="sxs-lookup"><span data-stu-id="78348-126">Perform cleanup of old artifacts on the machine by [deleting the hybrid runbook group](../automation-hybrid-runbook-worker.md#remove-a-hybrid-worker-group) and try again.</span></span>

### <a name="machine-unable-to-communicate"></a><span data-ttu-id="78348-127">Scenario: Machine is unable to communicate with the service</span><span class="sxs-lookup"><span data-stu-id="78348-127">Scenario: Machine is unable to communicate with the service</span></span>

#### <a name="issue"></a><span data-ttu-id="78348-128">Issue</span><span class="sxs-lookup"><span data-stu-id="78348-128">Issue</span></span>

<span data-ttu-id="78348-129">You receive one of the following error messages:</span><span class="sxs-lookup"><span data-stu-id="78348-129">You receive one of the following error messages:</span></span>

```
Unable to Register Machine for Patch Management, Registration Failed with Exception System.Net.Http.HttpRequestException: An error occurred while sending the request. ---> System.Net.WebException: The underlying connection was closed: An unexpected error occurred on a receive. ---> System.ComponentModel.Win32Exception: The client and server can't communicate, because they do not possess a common algorithm
```

```
Unable to Register Machine for Patch Management, Registration Failed with Exception Newtonsoft.Json.JsonReaderException: Error parsing positive infinity value.
```

```
The certificate presented by the service <wsid>.oms.opinsights.azure.com was not issued by a certificate authority used for Microsoft services. Contact your network administrator to see if they are running a proxy that intercepts TLS/SSL communication.
```

#### <a name="cause"></a><span data-ttu-id="78348-130">Cause</span><span class="sxs-lookup"><span data-stu-id="78348-130">Cause</span></span>

<span data-ttu-id="78348-131">There may be a proxy, gateway or firewall blocking network communication.</span><span class="sxs-lookup"><span data-stu-id="78348-131">There may be a proxy, gateway or firewall blocking network communication.</span></span>

#### <a name="resolution"></a><span data-ttu-id="78348-132">Resolution</span><span class="sxs-lookup"><span data-stu-id="78348-132">Resolution</span></span>

<span data-ttu-id="78348-133">Review your networking and ensure appropriate ports and addresses are allowed.</span><span class="sxs-lookup"><span data-stu-id="78348-133">Review your networking and ensure appropriate ports and addresses are allowed.</span></span> <span data-ttu-id="78348-134">See [network requirements](../automation-hybrid-runbook-worker.md#network-planning), for a list of ports and addresses that are required by Update Management and Hybrid Runbook Workers.</span><span class="sxs-lookup"><span data-stu-id="78348-134">See [network requirements](../automation-hybrid-runbook-worker.md#network-planning), for a list of ports and addresses that are required by Update Management and Hybrid Runbook Workers.</span></span>

### <a name="unable-to-create-selfsigned-cert"></a><span data-ttu-id="78348-135">Scenario: Unable to create self-signed certificate</span><span class="sxs-lookup"><span data-stu-id="78348-135">Scenario: Unable to create self-signed certificate</span></span>

#### <a name="issue"></a><span data-ttu-id="78348-136">Issue</span><span class="sxs-lookup"><span data-stu-id="78348-136">Issue</span></span>

<span data-ttu-id="78348-137">You receive one of the following error messages:</span><span class="sxs-lookup"><span data-stu-id="78348-137">You receive one of the following error messages:</span></span>

```
Unable to Register Machine for Patch Management, Registration Failed with Exception AgentService.HybridRegistration. PowerShell.Certificates.CertificateCreationException: Failed to create a self-signed certificate. ---> System.UnauthorizedAccessException: Access is denied.
```

#### <a name="cause"></a><span data-ttu-id="78348-138">Cause</span><span class="sxs-lookup"><span data-stu-id="78348-138">Cause</span></span>

<span data-ttu-id="78348-139">The Hybrid Runbook Worker was not able to generate a self-signed certificate</span><span class="sxs-lookup"><span data-stu-id="78348-139">The Hybrid Runbook Worker was not able to generate a self-signed certificate</span></span>

#### <a name="resolution"></a><span data-ttu-id="78348-140">Resolution</span><span class="sxs-lookup"><span data-stu-id="78348-140">Resolution</span></span>

<span data-ttu-id="78348-141">Verify system account has read access to folder **C:\ProgramData\Microsoft\Crypto\RSA** and try again.</span><span class="sxs-lookup"><span data-stu-id="78348-141">Verify system account has read access to folder **C:\ProgramData\Microsoft\Crypto\RSA** and try again.</span></span>

## <a name="linux"></a><span data-ttu-id="78348-142">Linux</span><span class="sxs-lookup"><span data-stu-id="78348-142">Linux</span></span>

### <a name="scenario-update-run-fails-to-start"></a><span data-ttu-id="78348-143">Scenario: Update run fails to start</span><span class="sxs-lookup"><span data-stu-id="78348-143">Scenario: Update run fails to start</span></span>

#### <a name="issue"></a><span data-ttu-id="78348-144">Issue</span><span class="sxs-lookup"><span data-stu-id="78348-144">Issue</span></span>

<span data-ttu-id="78348-145">An update runs fail to start on a Linux machine.</span><span class="sxs-lookup"><span data-stu-id="78348-145">An update runs fail to start on a Linux machine.</span></span>

#### <a name="cause"></a><span data-ttu-id="78348-146">Cause</span><span class="sxs-lookup"><span data-stu-id="78348-146">Cause</span></span>

<span data-ttu-id="78348-147">The Linux Hybrid Worker is unhealthy.</span><span class="sxs-lookup"><span data-stu-id="78348-147">The Linux Hybrid Worker is unhealthy.</span></span>

#### <a name="resolution"></a><span data-ttu-id="78348-148">Resolution</span><span class="sxs-lookup"><span data-stu-id="78348-148">Resolution</span></span>

<span data-ttu-id="78348-149">Make a copy of the following log file and preserve it for troubleshooting purposes:</span><span class="sxs-lookup"><span data-stu-id="78348-149">Make a copy of the following log file and preserve it for troubleshooting purposes:</span></span>

```
/var/opt/microsoft/omsagent/run/automationworker/worker.log
```

### <a name="scenario-update-run-starts-but-encounters-errors"></a><span data-ttu-id="78348-150">Scenario: Update run starts, but encounters errors</span><span class="sxs-lookup"><span data-stu-id="78348-150">Scenario: Update run starts, but encounters errors</span></span>

#### <a name="issue"></a><span data-ttu-id="78348-151">Issue</span><span class="sxs-lookup"><span data-stu-id="78348-151">Issue</span></span>

<span data-ttu-id="78348-152">An update run starts, but encounters errors during the run.</span><span class="sxs-lookup"><span data-stu-id="78348-152">An update run starts, but encounters errors during the run.</span></span>

#### <a name="cause"></a><span data-ttu-id="78348-153">Cause</span><span class="sxs-lookup"><span data-stu-id="78348-153">Cause</span></span>

<span data-ttu-id="78348-154">Possible causes could be:</span><span class="sxs-lookup"><span data-stu-id="78348-154">Possible causes could be:</span></span>

* <span data-ttu-id="78348-155">Package manager is unhealthy</span><span class="sxs-lookup"><span data-stu-id="78348-155">Package manager is unhealthy</span></span>
* <span data-ttu-id="78348-156">Specific packages may interfere with cloud based patching</span><span class="sxs-lookup"><span data-stu-id="78348-156">Specific packages may interfere with cloud based patching</span></span>
* <span data-ttu-id="78348-157">Other reasons</span><span class="sxs-lookup"><span data-stu-id="78348-157">Other reasons</span></span>

#### <a name="resolution"></a><span data-ttu-id="78348-158">Resolution</span><span class="sxs-lookup"><span data-stu-id="78348-158">Resolution</span></span>

<span data-ttu-id="78348-159">If failures occur during an update run after it starts successfully on Linux, check the job output from the affected machine in the run.</span><span class="sxs-lookup"><span data-stu-id="78348-159">If failures occur during an update run after it starts successfully on Linux, check the job output from the affected machine in the run.</span></span> <span data-ttu-id="78348-160">You may find specific error messages from your machine's package manager that you can research and take action on.</span><span class="sxs-lookup"><span data-stu-id="78348-160">You may find specific error messages from your machine's package manager that you can research and take action on.</span></span> <span data-ttu-id="78348-161">Update Management requires the package manager to be healthy for successful update deployments.</span><span class="sxs-lookup"><span data-stu-id="78348-161">Update Management requires the package manager to be healthy for successful update deployments.</span></span>

<span data-ttu-id="78348-162">In some cases, package updates can interfere with Update Management preventing an update deployment from completing.</span><span class="sxs-lookup"><span data-stu-id="78348-162">In some cases, package updates can interfere with Update Management preventing an update deployment from completing.</span></span> <span data-ttu-id="78348-163">If you see that, you'll have to either exclude these packages from future update runs or install them manually yourself.</span><span class="sxs-lookup"><span data-stu-id="78348-163">If you see that, you'll have to either exclude these packages from future update runs or install them manually yourself.</span></span>

<span data-ttu-id="78348-164">If you can't resolve a patching issue, make a copy of the following log file and preserve it **before** the next update deployment starts for troubleshooting purposes:</span><span class="sxs-lookup"><span data-stu-id="78348-164">If you can't resolve a patching issue, make a copy of the following log file and preserve it **before** the next update deployment starts for troubleshooting purposes:</span></span>

```
/var/opt/microsoft/omsagent/run/automationworker/omsupdatemgmt.log
```

## <a name="next-steps"></a><span data-ttu-id="78348-165">Next steps</span><span class="sxs-lookup"><span data-stu-id="78348-165">Next steps</span></span>

<span data-ttu-id="78348-166">If you did not see your problem or are unable to solve your issue, visit one of the following channels for more support:</span><span class="sxs-lookup"><span data-stu-id="78348-166">If you did not see your problem or are unable to solve your issue, visit one of the following channels for more support:</span></span>

* <span data-ttu-id="78348-167">Get answers from Azure experts through [Azure Forums](https://azure.microsoft.com/support/forums/)</span><span class="sxs-lookup"><span data-stu-id="78348-167">Get answers from Azure experts through [Azure Forums](https://azure.microsoft.com/support/forums/)</span></span>
* <span data-ttu-id="78348-168">Connect with [@AzureSupport](https://twitter.com/azuresupport) – the official Microsoft Azure account for improving customer experience by connecting the Azure community to the right resources: answers, support, and experts.</span><span class="sxs-lookup"><span data-stu-id="78348-168">Connect with [@AzureSupport](https://twitter.com/azuresupport) – the official Microsoft Azure account for improving customer experience by connecting the Azure community to the right resources: answers, support, and experts.</span></span>
* <span data-ttu-id="78348-169">If you need more help, you can file an Azure support incident.</span><span class="sxs-lookup"><span data-stu-id="78348-169">If you need more help, you can file an Azure support incident.</span></span> <span data-ttu-id="78348-170">Go to the [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span><span class="sxs-lookup"><span data-stu-id="78348-170">Go to the [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span></span>