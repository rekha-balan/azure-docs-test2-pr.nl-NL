---
title: Azure Government extensions | Microsoft Docs
description: This article lists virtual machine extensions available in Azure Government
services: azure-government
cloud: gov
documentationcenter: ''
author: gsacavdm
manager: pathuff
ms.assetid: 729197f0-c531-493f-a55b-3df950327d67
ms.service: azure-government
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: azure-government
ms.date: 07/13/2018
ms.author: gsacavdm
ms.openlocfilehash: 887766292b32ea93d6764f7fdf64fe8a47ed9f03
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870670"
---
# <a name="azure-government-virtual-machine-extensions"></a><span data-ttu-id="92caf-103">Azure Government virtual machine extensions</span><span class="sxs-lookup"><span data-stu-id="92caf-103">Azure Government virtual machine extensions</span></span>
<span data-ttu-id="92caf-104">This document contains a list of available [virtual machine extensions](../virtual-machines/windows/extensions-features.md) in Azure Government.</span><span class="sxs-lookup"><span data-stu-id="92caf-104">This document contains a list of available [virtual machine extensions](../virtual-machines/windows/extensions-features.md) in Azure Government.</span></span> <span data-ttu-id="92caf-105">If you'd like to see other extensions in Azure Government, please request them via the [Azure Government Feedback Forum](https://feedback.azure.com/forums/558487-azure-government).</span><span class="sxs-lookup"><span data-stu-id="92caf-105">If you'd like to see other extensions in Azure Government, please request them via the [Azure Government Feedback Forum](https://feedback.azure.com/forums/558487-azure-government).</span></span>

## <a name="virtual-machine-extensions"></a><span data-ttu-id="92caf-106">Virtual machine extensions</span><span class="sxs-lookup"><span data-stu-id="92caf-106">Virtual machine extensions</span></span>
<span data-ttu-id="92caf-107">The list of virtual machine extensions available in Azure Government can be obtained by [connecting to Azure Government via PowerShell](documentation-government-get-started-connect-with-ps.md) and running the following commands:</span><span class="sxs-lookup"><span data-stu-id="92caf-107">The list of virtual machine extensions available in Azure Government can be obtained by [connecting to Azure Government via PowerShell](documentation-government-get-started-connect-with-ps.md) and running the following commands:</span></span>

```powershell
Connect-AzureRmAccount -Environment AzureUSGovernment

Get-AzureRmVmImagePublisher -Location USGovVirginia | `
Get-AzureRmVMExtensionImageType | `
Get-AzureRmVMExtensionImage | Select Type, Version
```
<!-- 
Get-AzureRmVmImagePublisher -Location USGovVirginia | `
Get-AzureRmVMExtensionImageType | `
Get-AzureRmVMExtensionImage | `
Select Type, Version | `
Group Type | `
Sort Name | `
Select-Object @{Name="Entry";Expression={"| " + $_.Name + " | " + ($_.Group.Version -join "; ") +  " | " }} | `
Select-Object -ExpandProperty Entry | `
Out-File vm-extensions.md
-->

<span data-ttu-id="92caf-108">The table below contains a snapshot of the list of extensions available in Azure Government as of July 13, 2018.</span><span class="sxs-lookup"><span data-stu-id="92caf-108">The table below contains a snapshot of the list of extensions available in Azure Government as of July 13, 2018.</span></span>

|<span data-ttu-id="92caf-109">Extension</span><span class="sxs-lookup"><span data-stu-id="92caf-109">Extension</span></span>|<span data-ttu-id="92caf-110">Versions</span><span class="sxs-lookup"><span data-stu-id="92caf-110">Versions</span></span>|
| --- | --- |
| <span data-ttu-id="92caf-111">ADETest</span><span class="sxs-lookup"><span data-stu-id="92caf-111">ADETest</span></span> | <span data-ttu-id="92caf-112">1.4.0.2</span><span class="sxs-lookup"><span data-stu-id="92caf-112">1.4.0.2</span></span> | 
| <span data-ttu-id="92caf-113">AzureCATExtensionHandler</span><span class="sxs-lookup"><span data-stu-id="92caf-113">AzureCATExtensionHandler</span></span> | <span data-ttu-id="92caf-114">2.2.0.68</span><span class="sxs-lookup"><span data-stu-id="92caf-114">2.2.0.68</span></span> | 
| <span data-ttu-id="92caf-115">AzureDiskEncryption</span><span class="sxs-lookup"><span data-stu-id="92caf-115">AzureDiskEncryption</span></span> | <span data-ttu-id="92caf-116">1.1.0.1</span><span class="sxs-lookup"><span data-stu-id="92caf-116">1.1.0.1</span></span> | 
| <span data-ttu-id="92caf-117">AzureDiskEncryptionForLinux</span><span class="sxs-lookup"><span data-stu-id="92caf-117">AzureDiskEncryptionForLinux</span></span> | <span data-ttu-id="92caf-118">0.1.0.999195; 0.1.0.999196; 0.1.0.999283; 0.1.0.999297</span><span class="sxs-lookup"><span data-stu-id="92caf-118">0.1.0.999195; 0.1.0.999196; 0.1.0.999283; 0.1.0.999297</span></span> | 
| <span data-ttu-id="92caf-119">AzureDiskEncryptionForLinuxTest</span><span class="sxs-lookup"><span data-stu-id="92caf-119">AzureDiskEncryptionForLinuxTest</span></span> | <span data-ttu-id="92caf-120">0.1.0.999321</span><span class="sxs-lookup"><span data-stu-id="92caf-120">0.1.0.999321</span></span> | 
| <span data-ttu-id="92caf-121">AzureEnhancedMonitorForLinux</span><span class="sxs-lookup"><span data-stu-id="92caf-121">AzureEnhancedMonitorForLinux</span></span> | <span data-ttu-id="92caf-122">2.0.0.2; 3.0.1.0</span><span class="sxs-lookup"><span data-stu-id="92caf-122">2.0.0.2; 3.0.1.0</span></span> | 
| <span data-ttu-id="92caf-123">BGInfo</span><span class="sxs-lookup"><span data-stu-id="92caf-123">BGInfo</span></span> | <span data-ttu-id="92caf-124">2.1</span><span class="sxs-lookup"><span data-stu-id="92caf-124">2.1</span></span> | 
| <span data-ttu-id="92caf-125">ChefClient</span><span class="sxs-lookup"><span data-stu-id="92caf-125">ChefClient</span></span> | <span data-ttu-id="92caf-126">1210.12.110.1000</span><span class="sxs-lookup"><span data-stu-id="92caf-126">1210.12.110.1000</span></span> | 
| <span data-ttu-id="92caf-127">CustomScript</span><span class="sxs-lookup"><span data-stu-id="92caf-127">CustomScript</span></span> | <span data-ttu-id="92caf-128">2.0.2</span><span class="sxs-lookup"><span data-stu-id="92caf-128">2.0.2</span></span> | 
| <span data-ttu-id="92caf-129">CustomScriptExtension</span><span class="sxs-lookup"><span data-stu-id="92caf-129">CustomScriptExtension</span></span> | <span data-ttu-id="92caf-130">1.2; 1.3; 1.4; 1.7; 1.8; 1.9.1</span><span class="sxs-lookup"><span data-stu-id="92caf-130">1.2; 1.3; 1.4; 1.7; 1.8; 1.9.1</span></span> | 
| <span data-ttu-id="92caf-131">CustomScriptForLinux</span><span class="sxs-lookup"><span data-stu-id="92caf-131">CustomScriptForLinux</span></span> | <span data-ttu-id="92caf-132">1.0; 1.1; 1.2.2.0; 1.3.0.2; 1.4.1.0; 1.5.2.0</span><span class="sxs-lookup"><span data-stu-id="92caf-132">1.0; 1.1; 1.2.2.0; 1.3.0.2; 1.4.1.0; 1.5.2.0</span></span> | 
| <span data-ttu-id="92caf-133">DSC</span><span class="sxs-lookup"><span data-stu-id="92caf-133">DSC</span></span> | <span data-ttu-id="92caf-134">2.19.0.0; 2.22.0.0; 2.23.0.0; 2.24.0.0; 2.26.0.0; 2.26.1.0; 2.71.0.0; 2.72.0.0; 2.73.0.0; 2.76.0.0</span><span class="sxs-lookup"><span data-stu-id="92caf-134">2.19.0.0; 2.22.0.0; 2.23.0.0; 2.24.0.0; 2.26.0.0; 2.26.1.0; 2.71.0.0; 2.72.0.0; 2.73.0.0; 2.76.0.0</span></span> | 
| <span data-ttu-id="92caf-135">DSCForLinux</span><span class="sxs-lookup"><span data-stu-id="92caf-135">DSCForLinux</span></span> | <span data-ttu-id="92caf-136">1.0.0.0; 2.0.0.0; 2.70.0.4</span><span class="sxs-lookup"><span data-stu-id="92caf-136">1.0.0.0; 2.0.0.0; 2.70.0.4</span></span> | 
| <span data-ttu-id="92caf-137">IaaSAntimalware</span><span class="sxs-lookup"><span data-stu-id="92caf-137">IaaSAntimalware</span></span> | <span data-ttu-id="92caf-138">1.3.0.0; 1.5.4.4</span><span class="sxs-lookup"><span data-stu-id="92caf-138">1.3.0.0; 1.5.4.4</span></span> | 
| <span data-ttu-id="92caf-139">IaaSAutoPatchingForWindows</span><span class="sxs-lookup"><span data-stu-id="92caf-139">IaaSAutoPatchingForWindows</span></span> | <span data-ttu-id="92caf-140">1.0.1.14</span><span class="sxs-lookup"><span data-stu-id="92caf-140">1.0.1.14</span></span> | 
| <span data-ttu-id="92caf-141">IaaSDiagnostics</span><span class="sxs-lookup"><span data-stu-id="92caf-141">IaaSDiagnostics</span></span> | <span data-ttu-id="92caf-142">1.4.3.0; 1.7.4.0; 1.9.0.0</span><span class="sxs-lookup"><span data-stu-id="92caf-142">1.4.3.0; 1.7.4.0; 1.9.0.0</span></span> | 
| <span data-ttu-id="92caf-143">JsonADDomainExtension</span><span class="sxs-lookup"><span data-stu-id="92caf-143">JsonADDomainExtension</span></span> | <span data-ttu-id="92caf-144">1.3; 1.3.2</span><span class="sxs-lookup"><span data-stu-id="92caf-144">1.3; 1.3.2</span></span> | 
| <span data-ttu-id="92caf-145">Linux</span><span class="sxs-lookup"><span data-stu-id="92caf-145">Linux</span></span> | <span data-ttu-id="92caf-146">1.0.0.9101; 1.0.0.9102</span><span class="sxs-lookup"><span data-stu-id="92caf-146">1.0.0.9101; 1.0.0.9102</span></span> | 
| <span data-ttu-id="92caf-147">LinuxChefClient</span><span class="sxs-lookup"><span data-stu-id="92caf-147">LinuxChefClient</span></span> | <span data-ttu-id="92caf-148">1210.12.109.1005; 1210.12.110.1000</span><span class="sxs-lookup"><span data-stu-id="92caf-148">1210.12.109.1005; 1210.12.110.1000</span></span> | 
| <span data-ttu-id="92caf-149">LinuxDEBIAN7</span><span class="sxs-lookup"><span data-stu-id="92caf-149">LinuxDEBIAN7</span></span> | <span data-ttu-id="92caf-150">1.0.0.9101; 1.0.0.9102</span><span class="sxs-lookup"><span data-stu-id="92caf-150">1.0.0.9101; 1.0.0.9102</span></span> | 
| <span data-ttu-id="92caf-151">LinuxDEBIAN8</span><span class="sxs-lookup"><span data-stu-id="92caf-151">LinuxDEBIAN8</span></span> | <span data-ttu-id="92caf-152">1.0.0.9100; 1.0.0.9101; 1.0.0.9102</span><span class="sxs-lookup"><span data-stu-id="92caf-152">1.0.0.9100; 1.0.0.9101; 1.0.0.9102</span></span> | 
| <span data-ttu-id="92caf-153">LinuxDiagnostic</span><span class="sxs-lookup"><span data-stu-id="92caf-153">LinuxDiagnostic</span></span> | <span data-ttu-id="92caf-154">2.0.9005; 2.1.9005; 2.2.9005; 2.3.9005; 2.3.9007; 2.3.9011; 2.3.9013; 2.3.9015; 2.3.9017; 2.3.9021</span><span class="sxs-lookup"><span data-stu-id="92caf-154">2.0.9005; 2.1.9005; 2.2.9005; 2.3.9005; 2.3.9007; 2.3.9011; 2.3.9013; 2.3.9015; 2.3.9017; 2.3.9021</span></span> | 
| <span data-ttu-id="92caf-155">LinuxOL6</span><span class="sxs-lookup"><span data-stu-id="92caf-155">LinuxOL6</span></span> | <span data-ttu-id="92caf-156">1.0.0.9101; 1.0.0.9102</span><span class="sxs-lookup"><span data-stu-id="92caf-156">1.0.0.9101; 1.0.0.9102</span></span> | 
| <span data-ttu-id="92caf-157">LinuxRHEL6</span><span class="sxs-lookup"><span data-stu-id="92caf-157">LinuxRHEL6</span></span> | <span data-ttu-id="92caf-158">1.0.0.9101; 1.0.0.9102</span><span class="sxs-lookup"><span data-stu-id="92caf-158">1.0.0.9101; 1.0.0.9102</span></span> | 
| <span data-ttu-id="92caf-159">LinuxRHEL7</span><span class="sxs-lookup"><span data-stu-id="92caf-159">LinuxRHEL7</span></span> | <span data-ttu-id="92caf-160">1.0.0.9101; 1.0.0.9102</span><span class="sxs-lookup"><span data-stu-id="92caf-160">1.0.0.9101; 1.0.0.9102</span></span> | 
| <span data-ttu-id="92caf-161">LinuxSLES11SP3</span><span class="sxs-lookup"><span data-stu-id="92caf-161">LinuxSLES11SP3</span></span> | <span data-ttu-id="92caf-162">1.0.0.9101; 1.0.0.9102</span><span class="sxs-lookup"><span data-stu-id="92caf-162">1.0.0.9101; 1.0.0.9102</span></span> | 
| <span data-ttu-id="92caf-163">LinuxSLES11SP4</span><span class="sxs-lookup"><span data-stu-id="92caf-163">LinuxSLES11SP4</span></span> | <span data-ttu-id="92caf-164">1.0.0.9101; 1.0.0.9102</span><span class="sxs-lookup"><span data-stu-id="92caf-164">1.0.0.9101; 1.0.0.9102</span></span> | 
| <span data-ttu-id="92caf-165">LinuxSLES12</span><span class="sxs-lookup"><span data-stu-id="92caf-165">LinuxSLES12</span></span> | <span data-ttu-id="92caf-166">1.0.0.9102</span><span class="sxs-lookup"><span data-stu-id="92caf-166">1.0.0.9102</span></span> | 
| <span data-ttu-id="92caf-167">LinuxUBUNTU1404</span><span class="sxs-lookup"><span data-stu-id="92caf-167">LinuxUBUNTU1404</span></span> | <span data-ttu-id="92caf-168">1.0.0.9100; 1.0.0.9101; 1.0.0.9102</span><span class="sxs-lookup"><span data-stu-id="92caf-168">1.0.0.9100; 1.0.0.9101; 1.0.0.9102</span></span> | 
| <span data-ttu-id="92caf-169">LinuxUBUNTU1604</span><span class="sxs-lookup"><span data-stu-id="92caf-169">LinuxUBUNTU1604</span></span> | <span data-ttu-id="92caf-170">1.0.0.9100; 1.0.0.9101; 1.0.0.9102</span><span class="sxs-lookup"><span data-stu-id="92caf-170">1.0.0.9100; 1.0.0.9101; 1.0.0.9102</span></span> | 
| <span data-ttu-id="92caf-171">MicrosoftMonitoringAgent</span><span class="sxs-lookup"><span data-stu-id="92caf-171">MicrosoftMonitoringAgent</span></span> | <span data-ttu-id="92caf-172">1.0.11030.0; 1.0.11030.1; 1.0.11030.2; 1.0.11049.1</span><span class="sxs-lookup"><span data-stu-id="92caf-172">1.0.11030.0; 1.0.11030.1; 1.0.11030.2; 1.0.11049.1</span></span> | 
| <span data-ttu-id="92caf-173">NetworkWatcherAgentLinux</span><span class="sxs-lookup"><span data-stu-id="92caf-173">NetworkWatcherAgentLinux</span></span> | <span data-ttu-id="92caf-174">1.4.270.0; 1.4.306.5; 1.4.411.1; 1.4.493.1; 1.4.526.2; 1.4.585.2</span><span class="sxs-lookup"><span data-stu-id="92caf-174">1.4.270.0; 1.4.306.5; 1.4.411.1; 1.4.493.1; 1.4.526.2; 1.4.585.2</span></span> | 
| <span data-ttu-id="92caf-175">NetworkWatcherAgentWindows</span><span class="sxs-lookup"><span data-stu-id="92caf-175">NetworkWatcherAgentWindows</span></span> | <span data-ttu-id="92caf-176">1.4.270.0; 1.4.306.5; 1.4.411.1; 1.4.493.1; 1.4.526.2; 1.4.585.2</span><span class="sxs-lookup"><span data-stu-id="92caf-176">1.4.270.0; 1.4.306.5; 1.4.411.1; 1.4.493.1; 1.4.526.2; 1.4.585.2</span></span> | 
| <span data-ttu-id="92caf-177">OmsAgentForLinux</span><span class="sxs-lookup"><span data-stu-id="92caf-177">OmsAgentForLinux</span></span> | <span data-ttu-id="92caf-178">1.2.75.0; 1.4.45.2</span><span class="sxs-lookup"><span data-stu-id="92caf-178">1.2.75.0; 1.4.45.2</span></span> | 
| <span data-ttu-id="92caf-179">OSPatchingForLinux</span><span class="sxs-lookup"><span data-stu-id="92caf-179">OSPatchingForLinux</span></span> | <span data-ttu-id="92caf-180">1.0.1.1; 2.0.0.5; 2.1.0.0; 2.2.0.0; 2.3.0.1</span><span class="sxs-lookup"><span data-stu-id="92caf-180">1.0.1.1; 2.0.0.5; 2.1.0.0; 2.2.0.0; 2.3.0.1</span></span> | 
| <span data-ttu-id="92caf-181">RDMAUpdateForLinux</span><span class="sxs-lookup"><span data-stu-id="92caf-181">RDMAUpdateForLinux</span></span> | <span data-ttu-id="92caf-182">0.1.0.9</span><span class="sxs-lookup"><span data-stu-id="92caf-182">0.1.0.9</span></span> | 
| <span data-ttu-id="92caf-183">SqlIaaSAgent</span><span class="sxs-lookup"><span data-stu-id="92caf-183">SqlIaaSAgent</span></span> | <span data-ttu-id="92caf-184">1.2.11.0; 1.2.15.0; 1.2.16.0; 1.2.17.0; 1.2.18.0</span><span class="sxs-lookup"><span data-stu-id="92caf-184">1.2.11.0; 1.2.15.0; 1.2.16.0; 1.2.17.0; 1.2.18.0</span></span> | 
| <span data-ttu-id="92caf-185">VMAccessAgent</span><span class="sxs-lookup"><span data-stu-id="92caf-185">VMAccessAgent</span></span> | <span data-ttu-id="92caf-186">2.0; 2.0.2; 2.3; 2.4.2; 2.4.4</span><span class="sxs-lookup"><span data-stu-id="92caf-186">2.0; 2.0.2; 2.3; 2.4.2; 2.4.4</span></span> | 
| <span data-ttu-id="92caf-187">VMAccessForLinux</span><span class="sxs-lookup"><span data-stu-id="92caf-187">VMAccessForLinux</span></span> | <span data-ttu-id="92caf-188">1.0; 1.1; 1.2; 1.3.0.1; 1.4.0.0; 1.4.5.0</span><span class="sxs-lookup"><span data-stu-id="92caf-188">1.0; 1.1; 1.2; 1.3.0.1; 1.4.0.0; 1.4.5.0</span></span> | 
| <span data-ttu-id="92caf-189">VMBackupForLinuxExtension</span><span class="sxs-lookup"><span data-stu-id="92caf-189">VMBackupForLinuxExtension</span></span> | <span data-ttu-id="92caf-190">0.1.0.995; 0.1.0.993</span><span class="sxs-lookup"><span data-stu-id="92caf-190">0.1.0.995; 0.1.0.993</span></span> | 
| <span data-ttu-id="92caf-191">VMJITAccessExtension</span><span class="sxs-lookup"><span data-stu-id="92caf-191">VMJITAccessExtension</span></span> | <span data-ttu-id="92caf-192">1.0.0.0; 1.0.1.0</span><span class="sxs-lookup"><span data-stu-id="92caf-192">1.0.0.0; 1.0.1.0</span></span> | 
| <span data-ttu-id="92caf-193">VMSnapshot</span><span class="sxs-lookup"><span data-stu-id="92caf-193">VMSnapshot</span></span> | <span data-ttu-id="92caf-194">1.0.22.0; 1.0.23.0; 1.0.26.0; 1.0.27.0; 1.0.40.0; 1.0.41.0; 1.0.42.0</span><span class="sxs-lookup"><span data-stu-id="92caf-194">1.0.22.0; 1.0.23.0; 1.0.26.0; 1.0.27.0; 1.0.40.0; 1.0.41.0; 1.0.42.0</span></span> | 
| <span data-ttu-id="92caf-195">VMSnapshotLinux</span><span class="sxs-lookup"><span data-stu-id="92caf-195">VMSnapshotLinux</span></span> | <span data-ttu-id="92caf-196">1.0.9111.0; 1.0.9112.0; 1.0.9117.0; 1.0.9118.0; 1.0.9128.0; 1.0.9131.0</span><span class="sxs-lookup"><span data-stu-id="92caf-196">1.0.9111.0; 1.0.9112.0; 1.0.9117.0; 1.0.9118.0; 1.0.9128.0; 1.0.9131.0</span></span> | 
| <span data-ttu-id="92caf-197">VSRemoteDebugger</span><span class="sxs-lookup"><span data-stu-id="92caf-197">VSRemoteDebugger</span></span> | <span data-ttu-id="92caf-198">1.1.3.0</span><span class="sxs-lookup"><span data-stu-id="92caf-198">1.1.3.0</span></span> | 
| <span data-ttu-id="92caf-199">Windows</span><span class="sxs-lookup"><span data-stu-id="92caf-199">Windows</span></span> | <span data-ttu-id="92caf-200">1.0.0.9100; 1.0.0.9101; 1.0.0.9102</span><span class="sxs-lookup"><span data-stu-id="92caf-200">1.0.0.9100; 1.0.0.9101; 1.0.0.9102</span></span> | 

## <a name="next-steps"></a><span data-ttu-id="92caf-201">Next steps</span><span class="sxs-lookup"><span data-stu-id="92caf-201">Next steps</span></span>
* [<span data-ttu-id="92caf-202">Deploy a Windows virtual machine extension</span><span class="sxs-lookup"><span data-stu-id="92caf-202">Deploy a Windows virtual machine extension</span></span>](../virtual-machines/extensions/features-windows.md#run-vm-extensions)
* [<span data-ttu-id="92caf-203">Deploy a Linux virtual machine extension</span><span class="sxs-lookup"><span data-stu-id="92caf-203">Deploy a Linux virtual machine extension</span></span>](../virtual-machines/extensions/features-linux.md#run-vm-extensions)
