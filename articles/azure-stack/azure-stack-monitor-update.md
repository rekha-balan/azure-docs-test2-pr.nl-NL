---
title: Monitor updates in Azure Stack using the privileged endpoint | Microsoft Docs
description: Learn how to use the privileged endpoint to monitor update status for Azure Stack integrated systems.
services: azure-stack
documentationcenter: ''
author: mattbriggs
manager: femila
editor: ''
ms.assetid: 449ae53e-b951-401a-b2c9-17fee2f491f1
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2018
ms.author: mabrigg
ms.openlocfilehash: 8f384a79811c9a9b104acb98c8f6b6e162946ab8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870182"
---
# <a name="monitor-updates-in-azure-stack-using-the-privileged-endpoint"></a><span data-ttu-id="446cf-103">Monitor updates in Azure Stack using the privileged endpoint</span><span class="sxs-lookup"><span data-stu-id="446cf-103">Monitor updates in Azure Stack using the privileged endpoint</span></span>

<span data-ttu-id="446cf-104">*Applies to: Azure Stack integrated systems*</span><span class="sxs-lookup"><span data-stu-id="446cf-104">*Applies to: Azure Stack integrated systems*</span></span>

<span data-ttu-id="446cf-105">You can use the privileged endpoint to monitor the progress of an Azure Stack update run, and to resume a failed update run from the last successful step should the Azure Stack portal become unavailable.</span><span class="sxs-lookup"><span data-stu-id="446cf-105">You can use the privileged endpoint to monitor the progress of an Azure Stack update run, and to resume a failed update run from the last successful step should the Azure Stack portal become unavailable.</span></span>  <span data-ttu-id="446cf-106">Using the Azure Stack portal is the recommended method to manage updates in Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="446cf-106">Using the Azure Stack portal is the recommended method to manage updates in Azure Stack.</span></span>

<span data-ttu-id="446cf-107">The following new PowerShell cmdlets for update management are included in the 1710 update for Azure Stack integrated systems.</span><span class="sxs-lookup"><span data-stu-id="446cf-107">The following new PowerShell cmdlets for update management are included in the 1710 update for Azure Stack integrated systems.</span></span>

| <span data-ttu-id="446cf-108">Cmdlet</span><span class="sxs-lookup"><span data-stu-id="446cf-108">Cmdlet</span></span>  | <span data-ttu-id="446cf-109">Description</span><span class="sxs-lookup"><span data-stu-id="446cf-109">Description</span></span>  |
|---------|---------|
| `Get-AzureStackUpdateStatus` | <span data-ttu-id="446cf-110">Returns the status of the currently running, completed, or failed update.</span><span class="sxs-lookup"><span data-stu-id="446cf-110">Returns the status of the currently running, completed, or failed update.</span></span> <span data-ttu-id="446cf-111">Provides the high-level status of the update operation, and an XML document that describes both the current step and the corresponding state.</span><span class="sxs-lookup"><span data-stu-id="446cf-111">Provides the high-level status of the update operation, and an XML document that describes both the current step and the corresponding state.</span></span> |
| `Resume-AzureStackUpdate` | <span data-ttu-id="446cf-112">Resumes a failed update at the point where it failed.</span><span class="sxs-lookup"><span data-stu-id="446cf-112">Resumes a failed update at the point where it failed.</span></span> <span data-ttu-id="446cf-113">In certain scenarios, you may have to complete mitigation steps before you resume the update.</span><span class="sxs-lookup"><span data-stu-id="446cf-113">In certain scenarios, you may have to complete mitigation steps before you resume the update.</span></span>         |
| | |

## <a name="verify-the-cmdlets-are-available"></a><span data-ttu-id="446cf-114">Verify the cmdlets are available</span><span class="sxs-lookup"><span data-stu-id="446cf-114">Verify the cmdlets are available</span></span>
<span data-ttu-id="446cf-115">Because the cmdlets are new in the 1710 update package for Azure Stack, the 1710 update process needs to get to a certain point before the monitoring capability is available.</span><span class="sxs-lookup"><span data-stu-id="446cf-115">Because the cmdlets are new in the 1710 update package for Azure Stack, the 1710 update process needs to get to a certain point before the monitoring capability is available.</span></span> <span data-ttu-id="446cf-116">Typically, the cmdlets are available if the status in the administrator portal indicates that the 1710 update is at the **Restart Storage Hosts** step.</span><span class="sxs-lookup"><span data-stu-id="446cf-116">Typically, the cmdlets are available if the status in the administrator portal indicates that the 1710 update is at the **Restart Storage Hosts** step.</span></span> <span data-ttu-id="446cf-117">Specifically, the cmdlet update occurs during **Step: Running step 2.6 - Update PrivilegedEndpoint whitelist**.</span><span class="sxs-lookup"><span data-stu-id="446cf-117">Specifically, the cmdlet update occurs during **Step: Running step 2.6 - Update PrivilegedEndpoint whitelist**.</span></span>

<span data-ttu-id="446cf-118">You can also determine whether the cmdlets are available  programmatically by querying the command list from the privileged endpoint.</span><span class="sxs-lookup"><span data-stu-id="446cf-118">You can also determine whether the cmdlets are available  programmatically by querying the command list from the privileged endpoint.</span></span> <span data-ttu-id="446cf-119">To do this, run the following commands from the hardware lifecycle host or from a Privileged Access Workstation.</span><span class="sxs-lookup"><span data-stu-id="446cf-119">To do this, run the following commands from the hardware lifecycle host or from a Privileged Access Workstation.</span></span> <span data-ttu-id="446cf-120">Also, make sure the privileged endpoint is a trusted host.</span><span class="sxs-lookup"><span data-stu-id="446cf-120">Also, make sure the privileged endpoint is a trusted host.</span></span> <span data-ttu-id="446cf-121">For more information, see step 1 of [Access the privileged endpoint](azure-stack-privileged-endpoint.md#access-the-privileged-endpoint).</span><span class="sxs-lookup"><span data-stu-id="446cf-121">For more information, see step 1 of [Access the privileged endpoint](azure-stack-privileged-endpoint.md#access-the-privileged-endpoint).</span></span> 

1. <span data-ttu-id="446cf-122">Create a PowerShell session on any of the ERCS virtual machines in your Azure Stack environment (*Prefix*-ERCS01, *Prefix*-ERCS02, or *Prefix*-ERCS03).</span><span class="sxs-lookup"><span data-stu-id="446cf-122">Create a PowerShell session on any of the ERCS virtual machines in your Azure Stack environment (*Prefix*-ERCS01, *Prefix*-ERCS02, or *Prefix*-ERCS03).</span></span> <span data-ttu-id="446cf-123">Replace *Prefix* with the virtual machine prefix string that’s specific to your environment.</span><span class="sxs-lookup"><span data-stu-id="446cf-123">Replace *Prefix* with the virtual machine prefix string that’s specific to your environment.</span></span>

   ```powershell
   $cred = Get-Credential

   $pepSession = New-PSSession -ComputerName <Prefix>-ercs01 -Credential $cred -ConfigurationName PrivilegedEndpoint 
   ```
   <span data-ttu-id="446cf-124">When prompted for credentials, use the &lt;*Azure Stack domain*&gt;\cloudadmin account, or an account that's a member of the CloudAdmins group.</span><span class="sxs-lookup"><span data-stu-id="446cf-124">When prompted for credentials, use the &lt;*Azure Stack domain*&gt;\cloudadmin account, or an account that's a member of the CloudAdmins group.</span></span> <span data-ttu-id="446cf-125">For the CloudAdmin account, enter the same password that was provided during installation for the AzureStackAdmin domain administrator account.</span><span class="sxs-lookup"><span data-stu-id="446cf-125">For the CloudAdmin account, enter the same password that was provided during installation for the AzureStackAdmin domain administrator account.</span></span>

2. <span data-ttu-id="446cf-126">Get the full list of commands that are available in the privileged endpoint.</span><span class="sxs-lookup"><span data-stu-id="446cf-126">Get the full list of commands that are available in the privileged endpoint.</span></span> 

   ```powershell
   $commands = Invoke-Command -Session $pepSession -ScriptBlock { Get-Command } 
   ```
3. <span data-ttu-id="446cf-127">Determine if the privileged endpoint was updated.</span><span class="sxs-lookup"><span data-stu-id="446cf-127">Determine if the privileged endpoint was updated.</span></span>

   ```powershell
   $updateManagementModuleName = "Microsoft.Azurestack.UpdateManagement"
    if (($commands | ? Source -eq $updateManagementModuleName)) {
   Write-Host "Privileged endpoint was updated to support update monitoring tools."
    } else {
   Write-Host "Privileged endpoint has not been updated yet. Please try again later."
    } 
   ```

4. <span data-ttu-id="446cf-128">List the commands specific to the Microsoft.AzureStack.UpdateManagement module.</span><span class="sxs-lookup"><span data-stu-id="446cf-128">List the commands specific to the Microsoft.AzureStack.UpdateManagement module.</span></span>

   ```powershell
   $commands | ? Source -eq $updateManagementModuleName 
   ```
   <span data-ttu-id="446cf-129">For example:</span><span class="sxs-lookup"><span data-stu-id="446cf-129">For example:</span></span>
   ```powershell
   $commands | ? Source -eq $updateManagementModuleName
   
   CommandType     Name                                               Version    Source                                                  PSComputerName
    -----------     ----                                               -------    ------                                                  --------------
   Function        Get-AzureStackUpdateStatus                         0.0        Microsoft.Azurestack.UpdateManagement                   Contoso-ercs01
   Function        Resume-AzureStackUpdate                            0.0        Microsoft.Azurestack.UpdateManagement                   Contoso-ercs01
   ``` 

## <a name="use-the-update-management-cmdlets"></a><span data-ttu-id="446cf-130">Use the update management cmdlets</span><span class="sxs-lookup"><span data-stu-id="446cf-130">Use the update management cmdlets</span></span>

> [!NOTE]
> <span data-ttu-id="446cf-131">Run the following commands from the hardware lifecycle host or from a Privileged Access Workstation.</span><span class="sxs-lookup"><span data-stu-id="446cf-131">Run the following commands from the hardware lifecycle host or from a Privileged Access Workstation.</span></span> <span data-ttu-id="446cf-132">Also, make sure the privileged endpoint is a trusted host.</span><span class="sxs-lookup"><span data-stu-id="446cf-132">Also, make sure the privileged endpoint is a trusted host.</span></span> <span data-ttu-id="446cf-133">For more information, see step 1 of [Access the privileged endpoint](azure-stack-privileged-endpoint.md#access-the-privileged-endpoint).</span><span class="sxs-lookup"><span data-stu-id="446cf-133">For more information, see step 1 of [Access the privileged endpoint](azure-stack-privileged-endpoint.md#access-the-privileged-endpoint).</span></span>

### <a name="connect-to-the-privileged-endpoint-and-assign-session-variable"></a><span data-ttu-id="446cf-134">Connect to the privileged endpoint and assign session variable</span><span class="sxs-lookup"><span data-stu-id="446cf-134">Connect to the privileged endpoint and assign session variable</span></span>

<span data-ttu-id="446cf-135">Run the following commands to create a PowerShell session on any of the ERCS virtual machines in your Azure Stack environment (*Prefix*-ERCS01, *Prefix*-ERCS02, or *Prefix*-ERCS03), and to assign a session variable.</span><span class="sxs-lookup"><span data-stu-id="446cf-135">Run the following commands to create a PowerShell session on any of the ERCS virtual machines in your Azure Stack environment (*Prefix*-ERCS01, *Prefix*-ERCS02, or *Prefix*-ERCS03), and to assign a session variable.</span></span>

```powershell
$cred = Get-Credential

$pepSession = New-PSSession -ComputerName <Prefix>-ercs01 -Credential $cred -ConfigurationName PrivilegedEndpoint 
```
 <span data-ttu-id="446cf-136">When prompted for credentials, use the &lt;*Azure Stack domain*&gt;\cloudadmin account, or an account that's a member of the CloudAdmins group.</span><span class="sxs-lookup"><span data-stu-id="446cf-136">When prompted for credentials, use the &lt;*Azure Stack domain*&gt;\cloudadmin account, or an account that's a member of the CloudAdmins group.</span></span> <span data-ttu-id="446cf-137">For the CloudAdmin account, enter the same password that was provided during installation for the AzureStackAdmin domain administrator account.</span><span class="sxs-lookup"><span data-stu-id="446cf-137">For the CloudAdmin account, enter the same password that was provided during installation for the AzureStackAdmin domain administrator account.</span></span>

### <a name="get-high-level-status-of-the-current-update-run"></a><span data-ttu-id="446cf-138">Get high-level status of the current update run</span><span class="sxs-lookup"><span data-stu-id="446cf-138">Get high-level status of the current update run</span></span> 

<span data-ttu-id="446cf-139">To get a high-level status of the current update run, run the following commands:</span><span class="sxs-lookup"><span data-stu-id="446cf-139">To get a high-level status of the current update run, run the following commands:</span></span> 

```powershell
$statusString = Invoke-Command -Session $pepSession -ScriptBlock { Get-AzureStackUpdateStatus -StatusOnly }

$statusString.Value 
```

<span data-ttu-id="446cf-140">Possible values include:</span><span class="sxs-lookup"><span data-stu-id="446cf-140">Possible values include:</span></span>

- <span data-ttu-id="446cf-141">Running</span><span class="sxs-lookup"><span data-stu-id="446cf-141">Running</span></span>
- <span data-ttu-id="446cf-142">Completed</span><span class="sxs-lookup"><span data-stu-id="446cf-142">Completed</span></span>
- <span data-ttu-id="446cf-143">Failed</span><span class="sxs-lookup"><span data-stu-id="446cf-143">Failed</span></span> 
- <span data-ttu-id="446cf-144">Canceled</span><span class="sxs-lookup"><span data-stu-id="446cf-144">Canceled</span></span>

<span data-ttu-id="446cf-145">You can run these commands  repeatedly to see the most up-to-date status.</span><span class="sxs-lookup"><span data-stu-id="446cf-145">You can run these commands  repeatedly to see the most up-to-date status.</span></span> <span data-ttu-id="446cf-146">You don't have to re-establish a connection to check again.</span><span class="sxs-lookup"><span data-stu-id="446cf-146">You don't have to re-establish a connection to check again.</span></span>

### <a name="get-the-full-update-run-status-with-details"></a><span data-ttu-id="446cf-147">Get the full update run status with details</span><span class="sxs-lookup"><span data-stu-id="446cf-147">Get the full update run status with details</span></span> 

<span data-ttu-id="446cf-148">You can get the full update run summary as an XML string.</span><span class="sxs-lookup"><span data-stu-id="446cf-148">You can get the full update run summary as an XML string.</span></span> <span data-ttu-id="446cf-149">You can write the string to a file for examination, or convert it to an XML document and use PowerShell to parse it.</span><span class="sxs-lookup"><span data-stu-id="446cf-149">You can write the string to a file for examination, or convert it to an XML document and use PowerShell to parse it.</span></span> <span data-ttu-id="446cf-150">The following command parses the XML to get a hierarchical list of the currently running steps.</span><span class="sxs-lookup"><span data-stu-id="446cf-150">The following command parses the XML to get a hierarchical list of the currently running steps.</span></span>

```powershell
[xml]$updateStatus = Invoke-Command -Session $pepSession -ScriptBlock { Get-AzureStackUpdateStatus }

$updateStatus.SelectNodes("//Step[@Status='InProgress']")
```

<span data-ttu-id="446cf-151">In the following example, the top-level step (Cloud Update) has a child plan to update and restart the storage hosts.</span><span class="sxs-lookup"><span data-stu-id="446cf-151">In the following example, the top-level step (Cloud Update) has a child plan to update and restart the storage hosts.</span></span> <span data-ttu-id="446cf-152">It shows that the Restart Storage Hosts plan is updating the Blob Storage service on one of the hosts.</span><span class="sxs-lookup"><span data-stu-id="446cf-152">It shows that the Restart Storage Hosts plan is updating the Blob Storage service on one of the hosts.</span></span>

```powershell
[xml]$updateStatus = Invoke-Command -Session $pepSession -ScriptBlock { Get-AzureStackUpdateStatus }

$updateStatus.SelectNodes("//Step[@Status='InProgress']") 

    FullStepIndex : 2
    Index         : 2
    Name          : Cloud Update
    Description   : Perform cloud update.
    StartTimeUtc  : 2017-10-13T12:50:39.9020351Z
    Status        : InProgress
    Task          : Task
    
    FullStepIndex  : 2.9
    Index          : 9
    Name           : Restart Storage Hosts
    Description    : Restart Storage Hosts.
    EceErrorAction : Stop
    StartTimeUtc   : 2017-10-13T15:44:06.7431447Z
    Status         : InProgress
    Task           : Task
    
    FullStepIndex : 2.9.2
    Index         : 2
    Name          : PreUpdate ACS Blob Service
    Description   : Check function level, update deployment artifacts, configure Blob service settings
    StartTimeUtc  : 2017-10-13T15:44:26.0708525Z
    Status        : InProgress
    Task          : Task
```

### <a name="resume-a-failed-update-operation"></a><span data-ttu-id="446cf-153">Resume a failed update operation</span><span class="sxs-lookup"><span data-stu-id="446cf-153">Resume a failed update operation</span></span>

<span data-ttu-id="446cf-154">If the update fails, you can resume the update run where it left off.</span><span class="sxs-lookup"><span data-stu-id="446cf-154">If the update fails, you can resume the update run where it left off.</span></span>

```powershell
Invoke-Command -Session $pepSession -ScriptBlock { Resume-AzureStackUpdate } 
```

## <a name="troubleshoot"></a><span data-ttu-id="446cf-155">Troubleshoot</span><span class="sxs-lookup"><span data-stu-id="446cf-155">Troubleshoot</span></span>

<span data-ttu-id="446cf-156">The privileged endpoint is available on all ERCS virtual machines in the Azure Stack environment.</span><span class="sxs-lookup"><span data-stu-id="446cf-156">The privileged endpoint is available on all ERCS virtual machines in the Azure Stack environment.</span></span> <span data-ttu-id="446cf-157">Because the connection is not made to a highly available endpoint, you may experience occasional interruptions, warning, or error messages.</span><span class="sxs-lookup"><span data-stu-id="446cf-157">Because the connection is not made to a highly available endpoint, you may experience occasional interruptions, warning, or error messages.</span></span> <span data-ttu-id="446cf-158">These messages may indicate that the session was disconnected or that there was an error communicating with the ECE Service.</span><span class="sxs-lookup"><span data-stu-id="446cf-158">These messages may indicate that the session was disconnected or that there was an error communicating with the ECE Service.</span></span> <span data-ttu-id="446cf-159">This behavior is expected.</span><span class="sxs-lookup"><span data-stu-id="446cf-159">This behavior is expected.</span></span> <span data-ttu-id="446cf-160">You can retry the operation in a few minutes or create a new privileged endpoint session on one of the other ERCS virtual machines.</span><span class="sxs-lookup"><span data-stu-id="446cf-160">You can retry the operation in a few minutes or create a new privileged endpoint session on one of the other ERCS virtual machines.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="446cf-161">Next steps</span><span class="sxs-lookup"><span data-stu-id="446cf-161">Next steps</span></span>

- [<span data-ttu-id="446cf-162">Managing updates in Azure Stack</span><span class="sxs-lookup"><span data-stu-id="446cf-162">Managing updates in Azure Stack</span></span>](azure-stack-updates.md) 


