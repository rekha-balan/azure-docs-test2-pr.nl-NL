---
title: Run a validation test in Azure Stack  | Microsoft Docs
description: How to collect log files for diagnostics in Azure Stack.
services: azure-stack
author: mattbriggs
manager: femila
cloud: azure-stack
ms.assetid: D44641CB-BF3C-46FE-BCF1-D7F7E1D01AFA
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: PowerShell
ms.topic: article
ms.date: 07/19/2018
ms.author: mabrigg
ms.reviewer: hectorl
ms.openlocfilehash: a70c736489b25f6e8fd0d838c4c7b4b4db96a4f2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868500"
---
# <a name="run-a-validation-test-for-azure-stack"></a><span data-ttu-id="fa1b7-103">Run a validation test for Azure Stack</span><span class="sxs-lookup"><span data-stu-id="fa1b7-103">Run a validation test for Azure Stack</span></span>

<span data-ttu-id="fa1b7-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="fa1b7-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>
 
<span data-ttu-id="fa1b7-105">You can validate the status of your Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="fa1b7-105">You can validate the status of your Azure Stack.</span></span> <span data-ttu-id="fa1b7-106">When you have an issue, contact Microsoft Customer Services Support.</span><span class="sxs-lookup"><span data-stu-id="fa1b7-106">When you have an issue, contact Microsoft Customer Services Support.</span></span> <span data-ttu-id="fa1b7-107">Support asks you to run **Test-AzureStack** from your management node.</span><span class="sxs-lookup"><span data-stu-id="fa1b7-107">Support asks you to run **Test-AzureStack** from your management node.</span></span> <span data-ttu-id="fa1b7-108">The validation test isolates the failure.</span><span class="sxs-lookup"><span data-stu-id="fa1b7-108">The validation test isolates the failure.</span></span> <span data-ttu-id="fa1b7-109">Support can then analyze the detailed logs, focus on the area where the error occurred, and work with you in resolving the issue.</span><span class="sxs-lookup"><span data-stu-id="fa1b7-109">Support can then analyze the detailed logs, focus on the area where the error occurred, and work with you in resolving the issue.</span></span>

## <a name="run-test-azurestack"></a><span data-ttu-id="fa1b7-110">Run Test-AzureStack</span><span class="sxs-lookup"><span data-stu-id="fa1b7-110">Run Test-AzureStack</span></span>

<span data-ttu-id="fa1b7-111">When you have an issue, contact Microsoft Customer Services Support and then run **Run Test-AzureStack**.</span><span class="sxs-lookup"><span data-stu-id="fa1b7-111">When you have an issue, contact Microsoft Customer Services Support and then run **Run Test-AzureStack**.</span></span>

1. <span data-ttu-id="fa1b7-112">You have an issue.</span><span class="sxs-lookup"><span data-stu-id="fa1b7-112">You have an issue.</span></span>
2. <span data-ttu-id="fa1b7-113">Contact Microsoft Customer Services Support.</span><span class="sxs-lookup"><span data-stu-id="fa1b7-113">Contact Microsoft Customer Services Support.</span></span>
3. <span data-ttu-id="fa1b7-114">Run **Test-AzureStack** from the privileged endpoint.</span><span class="sxs-lookup"><span data-stu-id="fa1b7-114">Run **Test-AzureStack** from the privileged endpoint.</span></span>
    1. <span data-ttu-id="fa1b7-115">Access the privileged endpoint.</span><span class="sxs-lookup"><span data-stu-id="fa1b7-115">Access the privileged endpoint.</span></span> <span data-ttu-id="fa1b7-116">For instructions, see [Using the privileged endpoint in Azure Stack](azure-stack-privileged-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="fa1b7-116">For instructions, see [Using the privileged endpoint in Azure Stack](azure-stack-privileged-endpoint.md).</span></span> 
    2. <span data-ttu-id="fa1b7-117">On the ASDK, sign in to the management host as **AzureStack\CloudAdmin**.</span><span class="sxs-lookup"><span data-stu-id="fa1b7-117">On the ASDK, sign in to the management host as **AzureStack\CloudAdmin**.</span></span>  
    <span data-ttu-id="fa1b7-118">On an integrated system, you will need to use the IP address for the privileged-end-point for the management provided to you by your OEM hardware vendor.</span><span class="sxs-lookup"><span data-stu-id="fa1b7-118">On an integrated system, you will need to use the IP address for the privileged-end-point for the management provided to you by your OEM hardware vendor.</span></span>
    3. <span data-ttu-id="fa1b7-119">Open PowerShell as an administrator.</span><span class="sxs-lookup"><span data-stu-id="fa1b7-119">Open PowerShell as an administrator.</span></span>
    4. <span data-ttu-id="fa1b7-120">Run: `Enter-PSSession -ComputerName <ERCS-VM-name> -ConfigurationName PrivilegedEndpoint`</span><span class="sxs-lookup"><span data-stu-id="fa1b7-120">Run: `Enter-PSSession -ComputerName <ERCS-VM-name> -ConfigurationName PrivilegedEndpoint`</span></span>
    5. <span data-ttu-id="fa1b7-121">Run: `Test-AzureStack`</span><span class="sxs-lookup"><span data-stu-id="fa1b7-121">Run: `Test-AzureStack`</span></span>
4. <span data-ttu-id="fa1b7-122">If any tests report fail, run: `Get-AzureStackLog -FilterByRole SeedRing -OutputPath <Log output path>` The cmdlet gathers the logs from Test-AzureStack.</span><span class="sxs-lookup"><span data-stu-id="fa1b7-122">If any tests report fail, run: `Get-AzureStackLog -FilterByRole SeedRing -OutputPath <Log output path>` The cmdlet gathers the logs from Test-AzureStack.</span></span> <span data-ttu-id="fa1b7-123">For more information about diagnostic logs, see [Azure Stack diagnostics tools](azure-stack-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="fa1b7-123">For more information about diagnostic logs, see [Azure Stack diagnostics tools](azure-stack-diagnostics.md).</span></span>
5. <span data-ttu-id="fa1b7-124">Send the **SeedRing** logs to Microsoft Customer Services Support.</span><span class="sxs-lookup"><span data-stu-id="fa1b7-124">Send the **SeedRing** logs to Microsoft Customer Services Support.</span></span> <span data-ttu-id="fa1b7-125">Microsoft Customer Services Support works with you to resolve the issue.</span><span class="sxs-lookup"><span data-stu-id="fa1b7-125">Microsoft Customer Services Support works with you to resolve the issue.</span></span>

## <a name="reference-for-test-azurestack"></a><span data-ttu-id="fa1b7-126">Reference for Test-AzureStack</span><span class="sxs-lookup"><span data-stu-id="fa1b7-126">Reference for Test-AzureStack</span></span>

<span data-ttu-id="fa1b7-127">This section contains an overview for the Test-AzureStack cmdlet and a summary of the validation report.</span><span class="sxs-lookup"><span data-stu-id="fa1b7-127">This section contains an overview for the Test-AzureStack cmdlet and a summary of the validation report.</span></span>

### <a name="test-azurestack"></a><span data-ttu-id="fa1b7-128">Test-AzureStack</span><span class="sxs-lookup"><span data-stu-id="fa1b7-128">Test-AzureStack</span></span>

<span data-ttu-id="fa1b7-129">Validates the status of Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="fa1b7-129">Validates the status of Azure Stack.</span></span> <span data-ttu-id="fa1b7-130">The cmdlet reports the status of your Azure Stack hardware and software.</span><span class="sxs-lookup"><span data-stu-id="fa1b7-130">The cmdlet reports the status of your Azure Stack hardware and software.</span></span> <span data-ttu-id="fa1b7-131">Support staff can use this  report to reduce the time to resolve Azure Stack support cases.</span><span class="sxs-lookup"><span data-stu-id="fa1b7-131">Support staff can use this  report to reduce the time to resolve Azure Stack support cases.</span></span>

> [!Note]  
> <span data-ttu-id="fa1b7-132">**Test-AzureStack** may detect failures that are not resulting in cloud outages, such as a single failed disk or a single physical host node failure.</span><span class="sxs-lookup"><span data-stu-id="fa1b7-132">**Test-AzureStack** may detect failures that are not resulting in cloud outages, such as a single failed disk or a single physical host node failure.</span></span>

#### <a name="syntax"></a><span data-ttu-id="fa1b7-133">Syntax</span><span class="sxs-lookup"><span data-stu-id="fa1b7-133">Syntax</span></span>

````PowerShell
  Test-AzureStack
````

#### <a name="parameters"></a><span data-ttu-id="fa1b7-134">Parameters</span><span class="sxs-lookup"><span data-stu-id="fa1b7-134">Parameters</span></span>

| <span data-ttu-id="fa1b7-135">Parameter</span><span class="sxs-lookup"><span data-stu-id="fa1b7-135">Parameter</span></span>               | <span data-ttu-id="fa1b7-136">Value</span><span class="sxs-lookup"><span data-stu-id="fa1b7-136">Value</span></span>           | <span data-ttu-id="fa1b7-137">Required</span><span class="sxs-lookup"><span data-stu-id="fa1b7-137">Required</span></span> | <span data-ttu-id="fa1b7-138">Default</span><span class="sxs-lookup"><span data-stu-id="fa1b7-138">Default</span></span> |
| ---                     | ---             | ---      | ---     |
| <span data-ttu-id="fa1b7-139">ServiceAdminCredentials</span><span class="sxs-lookup"><span data-stu-id="fa1b7-139">ServiceAdminCredentials</span></span> | <span data-ttu-id="fa1b7-140">PSCredential</span><span class="sxs-lookup"><span data-stu-id="fa1b7-140">PSCredential</span></span>    | <span data-ttu-id="fa1b7-141">No</span><span class="sxs-lookup"><span data-stu-id="fa1b7-141">No</span></span>       | <span data-ttu-id="fa1b7-142">FALSE</span><span class="sxs-lookup"><span data-stu-id="fa1b7-142">FALSE</span></span>   |
| <span data-ttu-id="fa1b7-143">DoNotDeployTenantVm</span><span class="sxs-lookup"><span data-stu-id="fa1b7-143">DoNotDeployTenantVm</span></span>     | <span data-ttu-id="fa1b7-144">SwitchParameter</span><span class="sxs-lookup"><span data-stu-id="fa1b7-144">SwitchParameter</span></span> | <span data-ttu-id="fa1b7-145">No</span><span class="sxs-lookup"><span data-stu-id="fa1b7-145">No</span></span>       | <span data-ttu-id="fa1b7-146">FALSE</span><span class="sxs-lookup"><span data-stu-id="fa1b7-146">FALSE</span></span>   |
| <span data-ttu-id="fa1b7-147">AdminCredential</span><span class="sxs-lookup"><span data-stu-id="fa1b7-147">AdminCredential</span></span>         | <span data-ttu-id="fa1b7-148">PSCredential</span><span class="sxs-lookup"><span data-stu-id="fa1b7-148">PSCredential</span></span>    | <span data-ttu-id="fa1b7-149">No</span><span class="sxs-lookup"><span data-stu-id="fa1b7-149">No</span></span>       | <span data-ttu-id="fa1b7-150">NA</span><span class="sxs-lookup"><span data-stu-id="fa1b7-150">NA</span></span>      |
| <span data-ttu-id="fa1b7-151">List</span><span class="sxs-lookup"><span data-stu-id="fa1b7-151">List</span></span>                    | <span data-ttu-id="fa1b7-152">SwitchParameter</span><span class="sxs-lookup"><span data-stu-id="fa1b7-152">SwitchParameter</span></span> | <span data-ttu-id="fa1b7-153">No</span><span class="sxs-lookup"><span data-stu-id="fa1b7-153">No</span></span>       | <span data-ttu-id="fa1b7-154">FALSE</span><span class="sxs-lookup"><span data-stu-id="fa1b7-154">FALSE</span></span>   |
| <span data-ttu-id="fa1b7-155">Ignore</span><span class="sxs-lookup"><span data-stu-id="fa1b7-155">Ignore</span></span>                  | <span data-ttu-id="fa1b7-156">String</span><span class="sxs-lookup"><span data-stu-id="fa1b7-156">String</span></span>          | <span data-ttu-id="fa1b7-157">No</span><span class="sxs-lookup"><span data-stu-id="fa1b7-157">No</span></span>       | <span data-ttu-id="fa1b7-158">NA</span><span class="sxs-lookup"><span data-stu-id="fa1b7-158">NA</span></span>      |
| <span data-ttu-id="fa1b7-159">Include</span><span class="sxs-lookup"><span data-stu-id="fa1b7-159">Include</span></span>                 | <span data-ttu-id="fa1b7-160">String</span><span class="sxs-lookup"><span data-stu-id="fa1b7-160">String</span></span>          | <span data-ttu-id="fa1b7-161">No</span><span class="sxs-lookup"><span data-stu-id="fa1b7-161">No</span></span>       | <span data-ttu-id="fa1b7-162">NA</span><span class="sxs-lookup"><span data-stu-id="fa1b7-162">NA</span></span>      |
| <span data-ttu-id="fa1b7-163">BackupSharePath</span><span class="sxs-lookup"><span data-stu-id="fa1b7-163">BackupSharePath</span></span>         | <span data-ttu-id="fa1b7-164">String</span><span class="sxs-lookup"><span data-stu-id="fa1b7-164">String</span></span>          | <span data-ttu-id="fa1b7-165">No</span><span class="sxs-lookup"><span data-stu-id="fa1b7-165">No</span></span>       | <span data-ttu-id="fa1b7-166">NA</span><span class="sxs-lookup"><span data-stu-id="fa1b7-166">NA</span></span>      |
| <span data-ttu-id="fa1b7-167">BackupShareCredential</span><span class="sxs-lookup"><span data-stu-id="fa1b7-167">BackupShareCredential</span></span>   | <span data-ttu-id="fa1b7-168">PSCredential</span><span class="sxs-lookup"><span data-stu-id="fa1b7-168">PSCredential</span></span>    | <span data-ttu-id="fa1b7-169">No</span><span class="sxs-lookup"><span data-stu-id="fa1b7-169">No</span></span>       | <span data-ttu-id="fa1b7-170">NA</span><span class="sxs-lookup"><span data-stu-id="fa1b7-170">NA</span></span>      |


<span data-ttu-id="fa1b7-171">The Test-AzureStack cmdlet supports the common parameters: Verbose, Debug, ErrorAction, ErrorVariable, WarningAction, WarningVariable, OutBuffer, PipelineVariable, and OutVariable.</span><span class="sxs-lookup"><span data-stu-id="fa1b7-171">The Test-AzureStack cmdlet supports the common parameters: Verbose, Debug, ErrorAction, ErrorVariable, WarningAction, WarningVariable, OutBuffer, PipelineVariable, and OutVariable.</span></span> <span data-ttu-id="fa1b7-172">For more information, see [About Common Parameters](http://go.microsoft.com/fwlink/?LinkID=113216).</span><span class="sxs-lookup"><span data-stu-id="fa1b7-172">For more information, see [About Common Parameters](http://go.microsoft.com/fwlink/?LinkID=113216).</span></span> 

### <a name="examples-of-test-azurestack"></a><span data-ttu-id="fa1b7-173">Examples of Test-AzureStack</span><span class="sxs-lookup"><span data-stu-id="fa1b7-173">Examples of Test-AzureStack</span></span>

<span data-ttu-id="fa1b7-174">The following examples assume you're signed in as **CloudAdmin** and accessing the privileged endpoint (PEP).</span><span class="sxs-lookup"><span data-stu-id="fa1b7-174">The following examples assume you're signed in as **CloudAdmin** and accessing the privileged endpoint (PEP).</span></span> <span data-ttu-id="fa1b7-175">For instructions, see [Using the privileged endpoint in Azure Stack](azure-stack-privileged-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="fa1b7-175">For instructions, see [Using the privileged endpoint in Azure Stack](azure-stack-privileged-endpoint.md).</span></span> 

#### <a name="run-test-azurestack-interactively-without-cloud-scenarios"></a><span data-ttu-id="fa1b7-176">Run Test-AzureStack interactively without cloud scenarios</span><span class="sxs-lookup"><span data-stu-id="fa1b7-176">Run Test-AzureStack interactively without cloud scenarios</span></span>

<span data-ttu-id="fa1b7-177">In a PEP session, run:</span><span class="sxs-lookup"><span data-stu-id="fa1b7-177">In a PEP session, run:</span></span>

````PowerShell
    Enter-PSSession -ComputerName <ERCS-VM-name> -ConfigurationName PrivilegedEndpoint -Credential $localcred
    Test-AzureStack
````

#### <a name="run-test-azurestack-with-cloud-scenarios"></a><span data-ttu-id="fa1b7-178">Run Test-AzureStack with cloud scenarios</span><span class="sxs-lookup"><span data-stu-id="fa1b7-178">Run Test-AzureStack with cloud scenarios</span></span>

<span data-ttu-id="fa1b7-179">You can use **Test-AzureStack** to run cloud scenarios against your Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="fa1b7-179">You can use **Test-AzureStack** to run cloud scenarios against your Azure Stack.</span></span> <span data-ttu-id="fa1b7-180">These scenarios include:</span><span class="sxs-lookup"><span data-stu-id="fa1b7-180">These scenarios include:</span></span>

 - <span data-ttu-id="fa1b7-181">Creating resource groups</span><span class="sxs-lookup"><span data-stu-id="fa1b7-181">Creating resource groups</span></span>
 - <span data-ttu-id="fa1b7-182">Creating plans</span><span class="sxs-lookup"><span data-stu-id="fa1b7-182">Creating plans</span></span>
 - <span data-ttu-id="fa1b7-183">Creating offers</span><span class="sxs-lookup"><span data-stu-id="fa1b7-183">Creating offers</span></span>
 - <span data-ttu-id="fa1b7-184">Creating storage accounts</span><span class="sxs-lookup"><span data-stu-id="fa1b7-184">Creating storage accounts</span></span>
 - <span data-ttu-id="fa1b7-185">Creating a virtual machine</span><span class="sxs-lookup"><span data-stu-id="fa1b7-185">Creating a virtual machine</span></span>
 - <span data-ttu-id="fa1b7-186">Perform blob operations using the storage account created in the test scenario</span><span class="sxs-lookup"><span data-stu-id="fa1b7-186">Perform blob operations using the storage account created in the test scenario</span></span>
 - <span data-ttu-id="fa1b7-187">Perform queue operations using the storage account created in the test scenario</span><span class="sxs-lookup"><span data-stu-id="fa1b7-187">Perform queue operations using the storage account created in the test scenario</span></span>
 - <span data-ttu-id="fa1b7-188">Perform table operations using the storage account created in the test scenario</span><span class="sxs-lookup"><span data-stu-id="fa1b7-188">Perform table operations using the storage account created in the test scenario</span></span>

<span data-ttu-id="fa1b7-189">The cloud scenarios require cloud administrator credentials.</span><span class="sxs-lookup"><span data-stu-id="fa1b7-189">The cloud scenarios require cloud administrator credentials.</span></span> 
> [!Note]  
> <span data-ttu-id="fa1b7-190">You cannot run the cloud scenarios using Active Directory Federated Services (AD FS) credentials.</span><span class="sxs-lookup"><span data-stu-id="fa1b7-190">You cannot run the cloud scenarios using Active Directory Federated Services (AD FS) credentials.</span></span> <span data-ttu-id="fa1b7-191">The **Test-AzureStack** cmdlet is only accessible via the PEP.</span><span class="sxs-lookup"><span data-stu-id="fa1b7-191">The **Test-AzureStack** cmdlet is only accessible via the PEP.</span></span> <span data-ttu-id="fa1b7-192">But, the PEP doesn't support AD FS credentials.</span><span class="sxs-lookup"><span data-stu-id="fa1b7-192">But, the PEP doesn't support AD FS credentials.</span></span>

<span data-ttu-id="fa1b7-193">Type the cloud administrator user name in UPN format serviceadmin@contoso.onmicrosoft.com (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fa1b7-193">Type the cloud administrator user name in UPN format serviceadmin@contoso.onmicrosoft.com (Azure AD).</span></span> <span data-ttu-id="fa1b7-194">When prompted, type the password to the cloud administrator account.</span><span class="sxs-lookup"><span data-stu-id="fa1b7-194">When prompted, type the password to the cloud administrator account.</span></span>

<span data-ttu-id="fa1b7-195">In a PEP session, run:</span><span class="sxs-lookup"><span data-stu-id="fa1b7-195">In a PEP session, run:</span></span>

````PowerShell
  Enter-PSSession -ComputerName <ERCS-VM-name> -ConfigurationName PrivilegedEndpoint -Credential $localcred
  Test-AzureStack -ServiceAdminCredentials <Cloud administrator user name>
````

#### <a name="run-test-azurestack-without-cloud-scenarios"></a><span data-ttu-id="fa1b7-196">Run Test-AzureStack without cloud scenarios</span><span class="sxs-lookup"><span data-stu-id="fa1b7-196">Run Test-AzureStack without cloud scenarios</span></span>

<span data-ttu-id="fa1b7-197">In a PEP session, run:</span><span class="sxs-lookup"><span data-stu-id="fa1b7-197">In a PEP session, run:</span></span>

````PowerShell
  $session = New-PSSession -ComputerName <ERCS-VM-name> -ConfigurationName PrivilegedEndpoint -Credential $localcred
  Invoke-Command -Session $session -ScriptBlock {Test-AzureStack}
````

#### <a name="list-available-test-scenarios"></a><span data-ttu-id="fa1b7-198">List available test scenarios:</span><span class="sxs-lookup"><span data-stu-id="fa1b7-198">List available test scenarios:</span></span>

<span data-ttu-id="fa1b7-199">In a PEP session, run:</span><span class="sxs-lookup"><span data-stu-id="fa1b7-199">In a PEP session, run:</span></span>

````PowerShell
  Enter-PSSession -ComputerName <ERCS-VM-name> -ConfigurationName PrivilegedEndpoint -Credential $localcred
  Test-AzureStack -List
````

#### <a name="run-a-specified-test"></a><span data-ttu-id="fa1b7-200">Run a specified test</span><span class="sxs-lookup"><span data-stu-id="fa1b7-200">Run a specified test</span></span>

<span data-ttu-id="fa1b7-201">In a PEP session, run:</span><span class="sxs-lookup"><span data-stu-id="fa1b7-201">In a PEP session, run:</span></span>

````PowerShell
  Enter-PSSession -ComputerName <ERCS-VM-name> -ConfigurationName PrivilegedEndpoint -Credential $localcred
  Test-AzureStack -Include AzsSFRoleSummary, AzsInfraCapacity
````

<span data-ttu-id="fa1b7-202">To exclude specific tests:</span><span class="sxs-lookup"><span data-stu-id="fa1b7-202">To exclude specific tests:</span></span>

````PowerShell
    Enter-PSSession -ComputerName <ERCS-VM-name> -ConfigurationName PrivilegedEndpoint  -Credential $localcred
    Test-AzureStack -Ignore AzsInfraPerformance
````

### <a name="run-test-azurestack-to-test-infrastructure-backup-settings"></a><span data-ttu-id="fa1b7-203">Run Test-AzureStack to test infrastructure backup settings</span><span class="sxs-lookup"><span data-stu-id="fa1b7-203">Run Test-AzureStack to test infrastructure backup settings</span></span>

<span data-ttu-id="fa1b7-204">Before configuring infrastructure backup, you can test the backup share path and credential using the **AzsBackupShareAccessibility** test.</span><span class="sxs-lookup"><span data-stu-id="fa1b7-204">Before configuring infrastructure backup, you can test the backup share path and credential using the **AzsBackupShareAccessibility** test.</span></span>

<span data-ttu-id="fa1b7-205">In a PEP session, run:</span><span class="sxs-lookup"><span data-stu-id="fa1b7-205">In a PEP session, run:</span></span>

````PowerShell
    Enter-PSSession -ComputerName <ERCS-VM-name> -ConfigurationName PrivilegedEndpoint -Credential $localcred
    Test-AzureStack -Include AzsBackupShareAccessibility -BackupSharePath "\\<fileserver>\<fileshare>" -BackupShareCredential <PSCredentials-for-backup-share>
````
<span data-ttu-id="fa1b7-206">After configuring backup, you can run AzsBackupShareAccessibility to validate the share is accessible from the ERCS, from a PEP session run:</span><span class="sxs-lookup"><span data-stu-id="fa1b7-206">After configuring backup, you can run AzsBackupShareAccessibility to validate the share is accessible from the ERCS, from a PEP session run:</span></span>

````PowerShell
    Enter-PSSession -ComputerName <ERCS-VM-name> -ConfigurationName PrivilegedEndpoint  -Credential $localcred
    Test-AzureStack -Include AzsBackupShareAccessibility
````

<span data-ttu-id="fa1b7-207">To test new credentials with the configured backup share, from a PEP session run:</span><span class="sxs-lookup"><span data-stu-id="fa1b7-207">To test new credentials with the configured backup share, from a PEP session run:</span></span>

````PowerShell
    Enter-PSSession -ComputerName <ERCS-VM-name> -ConfigurationName PrivilegedEndpoint -Credential $localcred
    Test-AzureStack -Include AzsBackupShareAccessibility -BackupShareCredential <PSCredential for backup share>
````

### <a name="validation-test"></a><span data-ttu-id="fa1b7-208">Validation test</span><span class="sxs-lookup"><span data-stu-id="fa1b7-208">Validation test</span></span>

<span data-ttu-id="fa1b7-209">The following table summarizes the validation tests run by **Test-AzureStack**.</span><span class="sxs-lookup"><span data-stu-id="fa1b7-209">The following table summarizes the validation tests run by **Test-AzureStack**.</span></span>

| <span data-ttu-id="fa1b7-210">Name</span><span class="sxs-lookup"><span data-stu-id="fa1b7-210">Name</span></span>                                                                                                                              |
|-----------------------------------------------------------------------------------------------------------------------------------|-----------------------|
| <span data-ttu-id="fa1b7-211">Azure Stack Cloud Hosting Infrastructure Summary</span><span class="sxs-lookup"><span data-stu-id="fa1b7-211">Azure Stack Cloud Hosting Infrastructure Summary</span></span>                                                                                  |
| <span data-ttu-id="fa1b7-212">Azure Stack Storage Services Summary</span><span class="sxs-lookup"><span data-stu-id="fa1b7-212">Azure Stack Storage Services Summary</span></span>                                                                                              |
| <span data-ttu-id="fa1b7-213">Azure Stack Infrastructure Role Instance Summary</span><span class="sxs-lookup"><span data-stu-id="fa1b7-213">Azure Stack Infrastructure Role Instance Summary</span></span>                                                                                  |
| <span data-ttu-id="fa1b7-214">Azure Stack Cloud Hosting Infrastructure Utilization</span><span class="sxs-lookup"><span data-stu-id="fa1b7-214">Azure Stack Cloud Hosting Infrastructure Utilization</span></span>                                                                              |
| <span data-ttu-id="fa1b7-215">Azure Stack Infrastructure Capacity</span><span class="sxs-lookup"><span data-stu-id="fa1b7-215">Azure Stack Infrastructure Capacity</span></span>                                                                                               |
| <span data-ttu-id="fa1b7-216">Azure Stack Portal and API Summary</span><span class="sxs-lookup"><span data-stu-id="fa1b7-216">Azure Stack Portal and API Summary</span></span>                                                                                                |
| <span data-ttu-id="fa1b7-217">Azure Stack Azure Resource Manager Certificate Summary</span><span class="sxs-lookup"><span data-stu-id="fa1b7-217">Azure Stack Azure Resource Manager Certificate Summary</span></span>                                                                                               |
| <span data-ttu-id="fa1b7-218">Infrastructure management controller, Network controller, Storage services, and Privileged endpoint Infrastructure Roles</span><span class="sxs-lookup"><span data-stu-id="fa1b7-218">Infrastructure management controller, Network controller, Storage services, and Privileged endpoint Infrastructure Roles</span></span>          |
| <span data-ttu-id="fa1b7-219">Infrastructure management controller, Network controller, Storage services, and Privileged endpoint Infrastructure Role Instances</span><span class="sxs-lookup"><span data-stu-id="fa1b7-219">Infrastructure management controller, Network controller, Storage services, and Privileged endpoint Infrastructure Role Instances</span></span> |
| <span data-ttu-id="fa1b7-220">Azure Stack Infrastructure Role summary</span><span class="sxs-lookup"><span data-stu-id="fa1b7-220">Azure Stack Infrastructure Role summary</span></span>                                                                                           |
| <span data-ttu-id="fa1b7-221">Azure Stack Cloud Service Fabric Services</span><span class="sxs-lookup"><span data-stu-id="fa1b7-221">Azure Stack Cloud Service Fabric Services</span></span>                                                                                         |
| <span data-ttu-id="fa1b7-222">Azure Stack Infrastructure Role Instance Performance</span><span class="sxs-lookup"><span data-stu-id="fa1b7-222">Azure Stack Infrastructure Role Instance Performance</span></span>                                                                              |
| <span data-ttu-id="fa1b7-223">Azure Stack Cloud Host Performance Summary</span><span class="sxs-lookup"><span data-stu-id="fa1b7-223">Azure Stack Cloud Host Performance Summary</span></span>                                                                                        |
| <span data-ttu-id="fa1b7-224">Azure Stack Service Resource Consumption Summary</span><span class="sxs-lookup"><span data-stu-id="fa1b7-224">Azure Stack Service Resource Consumption Summary</span></span>                                                                                  |
| <span data-ttu-id="fa1b7-225">Azure Stack Scale Unit Critical Events (Last 8 hours)</span><span class="sxs-lookup"><span data-stu-id="fa1b7-225">Azure Stack Scale Unit Critical Events (Last 8 hours)</span></span>                                                                             |
| <span data-ttu-id="fa1b7-226">Azure Stack Storage Services Physical Disks Summary</span><span class="sxs-lookup"><span data-stu-id="fa1b7-226">Azure Stack Storage Services Physical Disks Summary</span></span>                                                                               |
|<span data-ttu-id="fa1b7-227">Azure Stack Backup Share Accessibility Summary</span><span class="sxs-lookup"><span data-stu-id="fa1b7-227">Azure Stack Backup Share Accessibility Summary</span></span>                                                                                     |

## <a name="next-steps"></a><span data-ttu-id="fa1b7-228">Next steps</span><span class="sxs-lookup"><span data-stu-id="fa1b7-228">Next steps</span></span>

 - <span data-ttu-id="fa1b7-229">To learn more about Azure Stack diagnostics tools and issue logging, see [ Azure Stack diagnostics tools](azure-stack-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="fa1b7-229">To learn more about Azure Stack diagnostics tools and issue logging, see [ Azure Stack diagnostics tools](azure-stack-diagnostics.md).</span></span>
 - <span data-ttu-id="fa1b7-230">To learn more about troubleshooting, see [Microsoft Azure Stack troubleshooting](azure-stack-troubleshooting.md)</span><span class="sxs-lookup"><span data-stu-id="fa1b7-230">To learn more about troubleshooting, see [Microsoft Azure Stack troubleshooting](azure-stack-troubleshooting.md)</span></span>
