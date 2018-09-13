---
title: Automated Patching for SQL Server VMs (Classic) | Microsoft Docs
description: Explains the Automated Patching feature for SQL Server Virtual Machines running in Azure using the classic deployment mode.
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: ''
tags: azure-service-management
ms.assetid: 737b2f65-08b9-4f54-b867-e987730265a8
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/17/2017
ms.author: jroth
ms.openlocfilehash: 69e3172b1eac844863f51997f3061619f50b68da
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551845"
---
# <a name="automated-patching-for-sql-server-in-azure-virtual-machines-classic"></a><span data-ttu-id="6758f-103">Automated Patching for SQL Server in Azure Virtual Machines (Classic)</span><span class="sxs-lookup"><span data-stu-id="6758f-103">Automated Patching for SQL Server in Azure Virtual Machines (Classic)</span></span>
> [!div class="op_single_selector"]
> * [Resource Manager](../sql/virtual-machines-windows-sql-automated-patching.md)
> * [Classic](../classic/sql-automated-patching.md)
> 
> 

<span data-ttu-id="6758f-106">Automated Patching establishes a maintenance window for an Azure Virtual Machine running SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6758f-106">Automated Patching establishes a maintenance window for an Azure Virtual Machine running SQL Server.</span></span> <span data-ttu-id="6758f-107">Automated Updates can only be installed during this maintenance window.</span><span class="sxs-lookup"><span data-stu-id="6758f-107">Automated Updates can only be installed during this maintenance window.</span></span> <span data-ttu-id="6758f-108">For SQL Server, this ensures that system updates and any associated restarts occur at the best possible time for the database.</span><span class="sxs-lookup"><span data-stu-id="6758f-108">For SQL Server, this ensures that system updates and any associated restarts occur at the best possible time for the database.</span></span> <span data-ttu-id="6758f-109">Automated Patching depends on the [SQL Server IaaS Agent Extension](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="6758f-109">Automated Patching depends on the [SQL Server IaaS Agent Extension](../classic/sql-server-agent-extension.md).</span></span>

> [!IMPORTANT] 
> Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md). This article covers using the Classic deployment model. Microsoft recommends that most new deployments use the Resource Manager model. To view the Resource Manager version of this article, see [Automated Patching for SQL Server in Azure Virtual Machines Resource Manager](../sql/virtual-machines-windows-sql-automated-patching.md).

## <a name="prerequisites"></a><span data-ttu-id="6758f-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="6758f-114">Prerequisites</span></span>
<span data-ttu-id="6758f-115">To use Automated Patching, consider the following prerequisites:</span><span class="sxs-lookup"><span data-stu-id="6758f-115">To use Automated Patching, consider the following prerequisites:</span></span>

<span data-ttu-id="6758f-116">**Operating System**:</span><span class="sxs-lookup"><span data-stu-id="6758f-116">**Operating System**:</span></span>

* <span data-ttu-id="6758f-117">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="6758f-117">Windows Server 2012</span></span>
* <span data-ttu-id="6758f-118">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="6758f-118">Windows Server 2012 R2</span></span>

<span data-ttu-id="6758f-119">**SQL Server version**:</span><span class="sxs-lookup"><span data-stu-id="6758f-119">**SQL Server version**:</span></span>

* <span data-ttu-id="6758f-120">SQL Server 2012</span><span class="sxs-lookup"><span data-stu-id="6758f-120">SQL Server 2012</span></span>
* <span data-ttu-id="6758f-121">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="6758f-121">SQL Server 2014</span></span>
* <span data-ttu-id="6758f-122">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="6758f-122">SQL Server 2016</span></span>

<span data-ttu-id="6758f-123">**Azure PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="6758f-123">**Azure PowerShell**:</span></span>

* <span data-ttu-id="6758f-124">[Install the latest Azure PowerShell commands](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="6758f-124">[Install the latest Azure PowerShell commands](/powershell/azureps-cmdlets-docs).</span></span>

<span data-ttu-id="6758f-125">**SQL Server IaaS Extension**:</span><span class="sxs-lookup"><span data-stu-id="6758f-125">**SQL Server IaaS Extension**:</span></span>

* <span data-ttu-id="6758f-126">[Install the SQL Server IaaS Extension](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="6758f-126">[Install the SQL Server IaaS Extension](../classic/sql-server-agent-extension.md).</span></span>

## <a name="settings"></a><span data-ttu-id="6758f-127">Settings</span><span class="sxs-lookup"><span data-stu-id="6758f-127">Settings</span></span>
<span data-ttu-id="6758f-128">The following table describes the options that can be configured for Automated Patching.</span><span class="sxs-lookup"><span data-stu-id="6758f-128">The following table describes the options that can be configured for Automated Patching.</span></span> <span data-ttu-id="6758f-129">For classic VMs, you must use PowerShell to configure these settings.</span><span class="sxs-lookup"><span data-stu-id="6758f-129">For classic VMs, you must use PowerShell to configure these settings.</span></span>

| <span data-ttu-id="6758f-130">Setting</span><span class="sxs-lookup"><span data-stu-id="6758f-130">Setting</span></span> | <span data-ttu-id="6758f-131">Possible values</span><span class="sxs-lookup"><span data-stu-id="6758f-131">Possible values</span></span> | <span data-ttu-id="6758f-132">Description</span><span class="sxs-lookup"><span data-stu-id="6758f-132">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6758f-133">**Automated Patching**</span><span class="sxs-lookup"><span data-stu-id="6758f-133">**Automated Patching**</span></span> |<span data-ttu-id="6758f-134">Enable/Disable (Disabled)</span><span class="sxs-lookup"><span data-stu-id="6758f-134">Enable/Disable (Disabled)</span></span> |<span data-ttu-id="6758f-135">Enables or disables Automated Patching for an Azure virtual machine.</span><span class="sxs-lookup"><span data-stu-id="6758f-135">Enables or disables Automated Patching for an Azure virtual machine.</span></span> |
| <span data-ttu-id="6758f-136">**Maintenance schedule**</span><span class="sxs-lookup"><span data-stu-id="6758f-136">**Maintenance schedule**</span></span> |<span data-ttu-id="6758f-137">Everyday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday</span><span class="sxs-lookup"><span data-stu-id="6758f-137">Everyday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday</span></span> |<span data-ttu-id="6758f-138">The schedule for downloading and installing Windows, SQL Server, and Microsoft updates for your virtual machine.</span><span class="sxs-lookup"><span data-stu-id="6758f-138">The schedule for downloading and installing Windows, SQL Server, and Microsoft updates for your virtual machine.</span></span> |
| <span data-ttu-id="6758f-139">**Maintenance start hour**</span><span class="sxs-lookup"><span data-stu-id="6758f-139">**Maintenance start hour**</span></span> |<span data-ttu-id="6758f-140">0-24</span><span class="sxs-lookup"><span data-stu-id="6758f-140">0-24</span></span> |<span data-ttu-id="6758f-141">The local start time to update the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="6758f-141">The local start time to update the virtual machine.</span></span> |
| <span data-ttu-id="6758f-142">**Maintenance window duration**</span><span class="sxs-lookup"><span data-stu-id="6758f-142">**Maintenance window duration**</span></span> |<span data-ttu-id="6758f-143">30-180</span><span class="sxs-lookup"><span data-stu-id="6758f-143">30-180</span></span> |<span data-ttu-id="6758f-144">The number of minutes permitted to complete the download and installation of updates.</span><span class="sxs-lookup"><span data-stu-id="6758f-144">The number of minutes permitted to complete the download and installation of updates.</span></span> |
| <span data-ttu-id="6758f-145">**Patch Category**</span><span class="sxs-lookup"><span data-stu-id="6758f-145">**Patch Category**</span></span> |<span data-ttu-id="6758f-146">Important</span><span class="sxs-lookup"><span data-stu-id="6758f-146">Important</span></span> |<span data-ttu-id="6758f-147">The category of updates to download and install.</span><span class="sxs-lookup"><span data-stu-id="6758f-147">The category of updates to download and install.</span></span> |

## <a name="configuration-with-powershell"></a><span data-ttu-id="6758f-148">Configuration with PowerShell</span><span class="sxs-lookup"><span data-stu-id="6758f-148">Configuration with PowerShell</span></span>
<span data-ttu-id="6758f-149">In the following example, PowerShell is used to configure Automated Patching on an existing SQL Server VM.</span><span class="sxs-lookup"><span data-stu-id="6758f-149">In the following example, PowerShell is used to configure Automated Patching on an existing SQL Server VM.</span></span> <span data-ttu-id="6758f-150">The **New-AzureVMSqlServerAutoPatchingConfig** command configures a new maintenance window for automatic updates.</span><span class="sxs-lookup"><span data-stu-id="6758f-150">The **New-AzureVMSqlServerAutoPatchingConfig** command configures a new maintenance window for automatic updates.</span></span>

    $aps = New-AzureVMSqlServerAutoPatchingConfig -Enable -DayOfWeek "Thursday" -MaintenanceWindowStartingHour 11 -MaintenanceWindowDuration 120  -PatchCategory "Important"

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoPatchingSettings $aps | Update-AzureVM

<span data-ttu-id="6758f-151">Based on this example, the following table describes the practical effect on the target Azure VM:</span><span class="sxs-lookup"><span data-stu-id="6758f-151">Based on this example, the following table describes the practical effect on the target Azure VM:</span></span>

| <span data-ttu-id="6758f-152">Parameter</span><span class="sxs-lookup"><span data-stu-id="6758f-152">Parameter</span></span> | <span data-ttu-id="6758f-153">Effect</span><span class="sxs-lookup"><span data-stu-id="6758f-153">Effect</span></span> |
| --- | --- |
| <span data-ttu-id="6758f-154">**DayOfWeek**</span><span class="sxs-lookup"><span data-stu-id="6758f-154">**DayOfWeek**</span></span> |<span data-ttu-id="6758f-155">Patches installed every Thursday.</span><span class="sxs-lookup"><span data-stu-id="6758f-155">Patches installed every Thursday.</span></span> |
| <span data-ttu-id="6758f-156">**MaintenanceWindowStartingHour**</span><span class="sxs-lookup"><span data-stu-id="6758f-156">**MaintenanceWindowStartingHour**</span></span> |<span data-ttu-id="6758f-157">Begin updates at 11:00am.</span><span class="sxs-lookup"><span data-stu-id="6758f-157">Begin updates at 11:00am.</span></span> |
| <span data-ttu-id="6758f-158">**MaintenanceWindowsDuration**</span><span class="sxs-lookup"><span data-stu-id="6758f-158">**MaintenanceWindowsDuration**</span></span> |<span data-ttu-id="6758f-159">Patches must be installed within 120 minutes.</span><span class="sxs-lookup"><span data-stu-id="6758f-159">Patches must be installed within 120 minutes.</span></span> <span data-ttu-id="6758f-160">Based on the start time, they must complete by 1:00pm.</span><span class="sxs-lookup"><span data-stu-id="6758f-160">Based on the start time, they must complete by 1:00pm.</span></span> |
| <span data-ttu-id="6758f-161">**PatchCategory**</span><span class="sxs-lookup"><span data-stu-id="6758f-161">**PatchCategory**</span></span> |<span data-ttu-id="6758f-162">The only possible setting for this parameter is “Important”.</span><span class="sxs-lookup"><span data-stu-id="6758f-162">The only possible setting for this parameter is “Important”.</span></span> |

<span data-ttu-id="6758f-163">It could take several minutes to install and configure the SQL Server IaaS Agent.</span><span class="sxs-lookup"><span data-stu-id="6758f-163">It could take several minutes to install and configure the SQL Server IaaS Agent.</span></span>

<span data-ttu-id="6758f-164">To disable Automated Patching, run the same script without the -Enable parameter to the New-AzureVMSqlServerAutoPatchingConfig.</span><span class="sxs-lookup"><span data-stu-id="6758f-164">To disable Automated Patching, run the same script without the -Enable parameter to the New-AzureVMSqlServerAutoPatchingConfig.</span></span> <span data-ttu-id="6758f-165">As with installation, it can take several minutes to disable Automated Patching.</span><span class="sxs-lookup"><span data-stu-id="6758f-165">As with installation, it can take several minutes to disable Automated Patching.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6758f-166">Next steps</span><span class="sxs-lookup"><span data-stu-id="6758f-166">Next steps</span></span>
<span data-ttu-id="6758f-167">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="6758f-167">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](../classic/sql-server-agent-extension.md).</span></span>

<span data-ttu-id="6758f-168">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6758f-168">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

