---
title: Troubleshoot Azure Automation Hybrid Runbook Worker | Microsoft Docs
description: Describe the symptoms, causes, and resolution for the most common Hybrid Runbook Worker issues in Azure Automation.
services: automation
documentationcenter: ''
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 02c6606e-8924-4328-a196-45630c2255e9
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/24/2017
ms.author: magoedte
ms.openlocfilehash: 666395edb3d1d579b1c69d1b78840b2a381b5b2b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555509"
---
# <a name="troubleshooting-tips-for-hybrid-runbook-worker"></a>Troubleshooting tips for Hybrid Runbook Worker

This article provides help troubleshooting errors you might experience with Automation Hybrid Runbook Workers and suggests possible solutions to resolve them.

## <a name="hybrid-runbook-worker-a-runbook-job-terminates-with-a-status-of-suspended"></a>Hybrid Runbook Worker: A runbook job terminates with a status of Suspended

Your runbook is suspended shortly after attempting to execute it three times. There are conditions which may interrupt the runbook from completing successfully and the related error message does not include any additional information indicating why. This article provides troubleshooting steps for issues related to the Hybrid Runbook Worker runbook execution failures.

If your Azure issue is not addressed in this article, visit the Azure forums on [MSDN and the Stack Overflow](https://azure.microsoft.com/support/forums/). You can post your issue on these forums or to [@AzureSupport on Twitter](https://twitter.com/AzureSupport). Also, you can file an Azure support request by selecting **Get support** on the [Azure support](https://azure.microsoft.com/support/options/) site.

### <a name="symptom"></a>Symptom
Runbook execution fails and the error returned is, "The job action 'Activate' cannot be run, because the process stopped unexpectedly. The job action was attempted 3 times."

There are several possible causes for the error: 

1. The hybrid worker is behind a proxy or firewall
2. The computer the hybrid worker is running on has less than the minimum hardware [requirements](automation-hybrid-runbook-worker.md#hybrid-runbook-worker-requirements) 
3. The runbooks cannot authenticate with local resources

#### <a name="cause-1-hybrid-runbook-worker-is-behind-proxy-or-firewall"></a>Cause 1: Hybrid Runbook Worker is behind proxy or firewall
The computer the Hybrid Runbook Worker is running on is behind a firewall or proxy server and outbound network access may not be permitted or configured correctly.

#### <a name="solution"></a>Solution
Verify the computer has outbound access to *.cloudapp.net on ports 443, 9354, and 30000-30199. 

#### <a name="cause-2-computer-has-less-than-minimum-hardware-requirements"></a>Cause 2: Computer has less than minimum hardware requirements
Computers running the Hybrid Runbook Worker should meet the minimum hardware requirements before designating it to host this feature. Otherwise, depending on the resource utilization of other background processes and contention caused by runbooks during execution, the computer will become over utilized and cause runbook job delays or timeouts. 

#### <a name="solution"></a>Solution
First confirm the computer designated to run the Hybrid Runbook Worker feature meets the minimum hardware requirements.  If it does, monitor CPU and memory utilization to determine any correlation between the performance of Hybrid Runbook Worker processes and Windows.  If there is memory or CPU pressure, this may indicate the need to upgrade or add additional processors, or increase memory to address the resource bottleneck and resolve the error. Alternatively, select a different compute resource that can support the minimum requirements and scale when workload demands indicate an increase is necessary.         

#### <a name="cause-3-runbooks-cannot-authenticate-with-local-resources"></a>Cause 3: Runbooks cannot authenticate with local resources

#### <a name="solution"></a>Solution
Check the **Microsoft-SMA** event log for a corresponding event with description *Win32 Process Exited with code [4294967295]*.  The cause of this error is you haven't configured authentication in your runbooks or specified the Run As credentials for the Hybrid worker group.  Please review [Runbook permissions](automation-hybrid-runbook-worker.md#runbook-permissions) to confirm you have correctly configured authentication for your runbooks.  

## <a name="next-steps"></a>Next steps

For help troubleshooting other issues in Automation, see [Troubleshooting common Azure Automation issues](automation-troubleshooting-automation-errors.md) 