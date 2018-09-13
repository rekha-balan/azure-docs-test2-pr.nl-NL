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
# <a name="troubleshooting-issues-with-update-management"></a>Troubleshooting issues with Update Management

This article discusses solutions to resolve issues that you may encounter when using Update Management.

## <a name="general"></a>General

### <a name="components-enabled-not-working"></a>Scenario: The components for the 'Update Management' solution have been enabled, and now this virtual machine is being configured

#### <a name="issue"></a>Issue

You continue to see the following message on a virtual machine 15 minutes after onboarding:

```
The components for the 'Update Management' solution have been enabled, and now this virtual machine is being configured. Please be patient, as this can sometimes take up to 15 minutes.
```

#### <a name="cause"></a>Cause

This error can be caused by the following reasons:

1. Communication back to the Automation Account is being blocked.
2. The VM being onboarded may have came from a cloned machine that was not sysprepped with the Microsoft Monitoring Agent installed.

#### <a name="resolution"></a>Resolution

1. Visit, [Network planning](../automation-hybrid-runbook-worker.md#network-planning) to learn about which addresses and ports need to be allowed for Update Management to work.
2. If using a cloned image, sysprep the image first and install the MMA agent after the fact.

## <a name="windows"></a>Windows

If you encounter issues while attempting to onboard the solution on a virtual machine, check the **Operations Manager** event log under **Application and Services Logs** on the local machine for events with event ID **4502** and event message containing **Microsoft.EnterpriseManagement.HealthService.AzureAutomation.HybridAgent**.

The following section highlights specific error messages and a possible resolution for each. For other onboarding issues see, [troubleshoot solution onboarding](onboarding.md).

### <a name="machine-already-registered"></a>Scenario: Machine is already registered to a different account

#### <a name="issue"></a>Issue

You receive the following error message:

```
Unable to Register Machine for Patch Management, Registration Failed with Exception System.InvalidOperationException: {"Message":"Machine is already registered to a different account."}
```

#### <a name="cause"></a>Cause

The machine is already onboarded to another workspace for Update Management.

#### <a name="resolution"></a>Resolution

Perform cleanup of old artifacts on the machine by [deleting the hybrid runbook group](../automation-hybrid-runbook-worker.md#remove-a-hybrid-worker-group) and try again.

### <a name="machine-unable-to-communicate"></a>Scenario: Machine is unable to communicate with the service

#### <a name="issue"></a>Issue

You receive one of the following error messages:

```
Unable to Register Machine for Patch Management, Registration Failed with Exception System.Net.Http.HttpRequestException: An error occurred while sending the request. ---> System.Net.WebException: The underlying connection was closed: An unexpected error occurred on a receive. ---> System.ComponentModel.Win32Exception: The client and server can't communicate, because they do not possess a common algorithm
```

```
Unable to Register Machine for Patch Management, Registration Failed with Exception Newtonsoft.Json.JsonReaderException: Error parsing positive infinity value.
```

```
The certificate presented by the service <wsid>.oms.opinsights.azure.com was not issued by a certificate authority used for Microsoft services. Contact your network administrator to see if they are running a proxy that intercepts TLS/SSL communication.
```

#### <a name="cause"></a>Cause

There may be a proxy, gateway or firewall blocking network communication.

#### <a name="resolution"></a>Resolution

Review your networking and ensure appropriate ports and addresses are allowed. See [network requirements](../automation-hybrid-runbook-worker.md#network-planning), for a list of ports and addresses that are required by Update Management and Hybrid Runbook Workers.

### <a name="unable-to-create-selfsigned-cert"></a>Scenario: Unable to create self-signed certificate

#### <a name="issue"></a>Issue

You receive one of the following error messages:

```
Unable to Register Machine for Patch Management, Registration Failed with Exception AgentService.HybridRegistration. PowerShell.Certificates.CertificateCreationException: Failed to create a self-signed certificate. ---> System.UnauthorizedAccessException: Access is denied.
```

#### <a name="cause"></a>Cause

The Hybrid Runbook Worker was not able to generate a self-signed certificate

#### <a name="resolution"></a>Resolution

Verify system account has read access to folder **C:\ProgramData\Microsoft\Crypto\RSA** and try again.

## <a name="linux"></a>Linux

### <a name="scenario-update-run-fails-to-start"></a>Scenario: Update run fails to start

#### <a name="issue"></a>Issue

An update runs fail to start on a Linux machine.

#### <a name="cause"></a>Cause

The Linux Hybrid Worker is unhealthy.

#### <a name="resolution"></a>Resolution

Make a copy of the following log file and preserve it for troubleshooting purposes:

```
/var/opt/microsoft/omsagent/run/automationworker/worker.log
```

### <a name="scenario-update-run-starts-but-encounters-errors"></a>Scenario: Update run starts, but encounters errors

#### <a name="issue"></a>Issue

An update run starts, but encounters errors during the run.

#### <a name="cause"></a>Cause

Possible causes could be:

* Package manager is unhealthy
* Specific packages may interfere with cloud based patching
* Other reasons

#### <a name="resolution"></a>Resolution

If failures occur during an update run after it starts successfully on Linux, check the job output from the affected machine in the run. You may find specific error messages from your machine's package manager that you can research and take action on. Update Management requires the package manager to be healthy for successful update deployments.

In some cases, package updates can interfere with Update Management preventing an update deployment from completing. If you see that, you'll have to either exclude these packages from future update runs or install them manually yourself.

If you can't resolve a patching issue, make a copy of the following log file and preserve it **before** the next update deployment starts for troubleshooting purposes:

```
/var/opt/microsoft/omsagent/run/automationworker/omsupdatemgmt.log
```

## <a name="next-steps"></a>Next steps

If you did not see your problem or are unable to solve your issue, visit one of the following channels for more support:

* Get answers from Azure experts through [Azure Forums](https://azure.microsoft.com/support/forums/)
* Connect with [@AzureSupport](https://twitter.com/azuresupport) – the official Microsoft Azure account for improving customer experience by connecting the Azure community to the right resources: answers, support, and experts.
* If you need more help, you can file an Azure support incident. Go to the [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.