---
title: Automated Patching for SQL Server VMs (Resource Manager) | Microsoft Docs
description: Explains the Automated Patching feature for SQL Server Virtual Machines running in Azure using Resource Manager.
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: ''
tags: azure-resource-manager
ms.assetid: 58232e92-318f-456b-8f0a-2201a541e08d
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/31/2017
ms.author: jroth
ms.openlocfilehash: a0b914713cd88c202b7467524e039dd7dd913bf5
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540676"
---
# <a name="automated-patching-for-sql-server-in-azure-virtual-machines-resource-manager"></a><span data-ttu-id="30973-103">Automated Patching for SQL Server in Azure Virtual Machines (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="30973-103">Automated Patching for SQL Server in Azure Virtual Machines (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [Resource Manager](virtual-machines-windows-sql-automated-patching.md)
> * [Classic](../classic/sql-automated-patching.md)
> 
> 

<span data-ttu-id="30973-106">Automated Patching establishes a maintenance window for an Azure Virtual Machine running SQL Server.</span><span class="sxs-lookup"><span data-stu-id="30973-106">Automated Patching establishes a maintenance window for an Azure Virtual Machine running SQL Server.</span></span> <span data-ttu-id="30973-107">Automated Updates can only be installed during this maintenance window.</span><span class="sxs-lookup"><span data-stu-id="30973-107">Automated Updates can only be installed during this maintenance window.</span></span> <span data-ttu-id="30973-108">For SQL Server, this rescriction ensures that system updates and any associated restarts occur at the best possible time for the database.</span><span class="sxs-lookup"><span data-stu-id="30973-108">For SQL Server, this rescriction ensures that system updates and any associated restarts occur at the best possible time for the database.</span></span> <span data-ttu-id="30973-109">Automated Patching depends on the [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="30973-109">Automated Patching depends on the [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="30973-110">To view the classic version of this article, see [Automated Patching for SQL Server in Azure Virtual Machines Classic](../classic/sql-automated-patching.md).</span><span class="sxs-lookup"><span data-stu-id="30973-110">To view the classic version of this article, see [Automated Patching for SQL Server in Azure Virtual Machines Classic](../classic/sql-automated-patching.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="30973-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="30973-111">Prerequisites</span></span>
<span data-ttu-id="30973-112">To use Automated Patching, consider the following prerequisites:</span><span class="sxs-lookup"><span data-stu-id="30973-112">To use Automated Patching, consider the following prerequisites:</span></span>

<span data-ttu-id="30973-113">**Operating System**:</span><span class="sxs-lookup"><span data-stu-id="30973-113">**Operating System**:</span></span>

* <span data-ttu-id="30973-114">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="30973-114">Windows Server 2012</span></span>
* <span data-ttu-id="30973-115">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="30973-115">Windows Server 2012 R2</span></span>

<span data-ttu-id="30973-116">**SQL Server version**:</span><span class="sxs-lookup"><span data-stu-id="30973-116">**SQL Server version**:</span></span>

* <span data-ttu-id="30973-117">SQL Server 2012</span><span class="sxs-lookup"><span data-stu-id="30973-117">SQL Server 2012</span></span>
* <span data-ttu-id="30973-118">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="30973-118">SQL Server 2014</span></span>
* <span data-ttu-id="30973-119">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="30973-119">SQL Server 2016</span></span>

<span data-ttu-id="30973-120">**Azure PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="30973-120">**Azure PowerShell**:</span></span>

* <span data-ttu-id="30973-121">[Install the latest Azure PowerShell commands](/powershell/azureps-cmdlets-docs) if you plan to configure Automated Patching with PowerShell.</span><span class="sxs-lookup"><span data-stu-id="30973-121">[Install the latest Azure PowerShell commands](/powershell/azureps-cmdlets-docs) if you plan to configure Automated Patching with PowerShell.</span></span>

> [!NOTE]
> Automated Patching relies on the SQL Server IaaS Agent Extension. Current SQL virtual machine gallery images add this extension by default. For more information, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).
> 
> 

## <a name="settings"></a><span data-ttu-id="30973-125">Settings</span><span class="sxs-lookup"><span data-stu-id="30973-125">Settings</span></span>
<span data-ttu-id="30973-126">The following table describes the options that can be configured for Automated Patching.</span><span class="sxs-lookup"><span data-stu-id="30973-126">The following table describes the options that can be configured for Automated Patching.</span></span> <span data-ttu-id="30973-127">The actual configuration steps vary depending on whether you use the Azure portal or Azure Windows PowerShell commands.</span><span class="sxs-lookup"><span data-stu-id="30973-127">The actual configuration steps vary depending on whether you use the Azure portal or Azure Windows PowerShell commands.</span></span>

| <span data-ttu-id="30973-128">Setting</span><span class="sxs-lookup"><span data-stu-id="30973-128">Setting</span></span> | <span data-ttu-id="30973-129">Possible values</span><span class="sxs-lookup"><span data-stu-id="30973-129">Possible values</span></span> | <span data-ttu-id="30973-130">Description</span><span class="sxs-lookup"><span data-stu-id="30973-130">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="30973-131">**Automated Patching**</span><span class="sxs-lookup"><span data-stu-id="30973-131">**Automated Patching**</span></span> |<span data-ttu-id="30973-132">Enable/Disable (Disabled)</span><span class="sxs-lookup"><span data-stu-id="30973-132">Enable/Disable (Disabled)</span></span> |<span data-ttu-id="30973-133">Enables or disables Automated Patching for an Azure virtual machine.</span><span class="sxs-lookup"><span data-stu-id="30973-133">Enables or disables Automated Patching for an Azure virtual machine.</span></span> |
| <span data-ttu-id="30973-134">**Maintenance schedule**</span><span class="sxs-lookup"><span data-stu-id="30973-134">**Maintenance schedule**</span></span> |<span data-ttu-id="30973-135">Everyday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday</span><span class="sxs-lookup"><span data-stu-id="30973-135">Everyday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday</span></span> |<span data-ttu-id="30973-136">The schedule for downloading and installing Windows, SQL Server, and Microsoft updates for your virtual machine.</span><span class="sxs-lookup"><span data-stu-id="30973-136">The schedule for downloading and installing Windows, SQL Server, and Microsoft updates for your virtual machine.</span></span> |
| <span data-ttu-id="30973-137">**Maintenance start hour**</span><span class="sxs-lookup"><span data-stu-id="30973-137">**Maintenance start hour**</span></span> |<span data-ttu-id="30973-138">0-24</span><span class="sxs-lookup"><span data-stu-id="30973-138">0-24</span></span> |<span data-ttu-id="30973-139">The local start time to update the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="30973-139">The local start time to update the virtual machine.</span></span> |
| <span data-ttu-id="30973-140">**Maintenance window duration**</span><span class="sxs-lookup"><span data-stu-id="30973-140">**Maintenance window duration**</span></span> |<span data-ttu-id="30973-141">30-180</span><span class="sxs-lookup"><span data-stu-id="30973-141">30-180</span></span> |<span data-ttu-id="30973-142">The number of minutes permitted to complete the download and installation of updates.</span><span class="sxs-lookup"><span data-stu-id="30973-142">The number of minutes permitted to complete the download and installation of updates.</span></span> |
| <span data-ttu-id="30973-143">**Patch Category**</span><span class="sxs-lookup"><span data-stu-id="30973-143">**Patch Category**</span></span> |<span data-ttu-id="30973-144">Important</span><span class="sxs-lookup"><span data-stu-id="30973-144">Important</span></span> |<span data-ttu-id="30973-145">The category of updates to download and install.</span><span class="sxs-lookup"><span data-stu-id="30973-145">The category of updates to download and install.</span></span> |

## <a name="configuration-in-the-portal"></a><span data-ttu-id="30973-146">Configuration in the Portal</span><span class="sxs-lookup"><span data-stu-id="30973-146">Configuration in the Portal</span></span>
<span data-ttu-id="30973-147">You can use the Azure portal to configure Automated Patching during provisioning or for existing VMs.</span><span class="sxs-lookup"><span data-stu-id="30973-147">You can use the Azure portal to configure Automated Patching during provisioning or for existing VMs.</span></span>

### <a name="new-vms"></a><span data-ttu-id="30973-148">New VMs</span><span class="sxs-lookup"><span data-stu-id="30973-148">New VMs</span></span>
<span data-ttu-id="30973-149">Use the Azure portal to configure Automated Patching when you create a new SQL Server Virtual Machine in the Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="30973-149">Use the Azure portal to configure Automated Patching when you create a new SQL Server Virtual Machine in the Resource Manager deployment model.</span></span>

<span data-ttu-id="30973-150">In the **SQL Server settings** blade, select **Automated patching**.</span><span class="sxs-lookup"><span data-stu-id="30973-150">In the **SQL Server settings** blade, select **Automated patching**.</span></span> <span data-ttu-id="30973-151">The following Azure portal screenshot shows the **SQL Automated Patching** blade.</span><span class="sxs-lookup"><span data-stu-id="30973-151">The following Azure portal screenshot shows the **SQL Automated Patching** blade.</span></span>

![SQL Automated Patching in Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-sql-automated-patching/azure-sql-arm-patching.png)

<span data-ttu-id="30973-153">For context, see the complete topic on [provisioning a SQL Server virtual machine in Azure](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="30973-153">For context, see the complete topic on [provisioning a SQL Server virtual machine in Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

### <a name="existing-vms"></a><span data-ttu-id="30973-154">Existing VMs</span><span class="sxs-lookup"><span data-stu-id="30973-154">Existing VMs</span></span>
<span data-ttu-id="30973-155">For existing SQL Server virtual machines, select your SQL Server virtual machine.</span><span class="sxs-lookup"><span data-stu-id="30973-155">For existing SQL Server virtual machines, select your SQL Server virtual machine.</span></span> <span data-ttu-id="30973-156">Then select the **SQL Server configuration** section of the **Settings** blade.</span><span class="sxs-lookup"><span data-stu-id="30973-156">Then select the **SQL Server configuration** section of the **Settings** blade.</span></span>

![SQL Automatic Patching for existing VMs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-sql-automated-patching/azure-sql-rm-patching-existing-vms.png)

<span data-ttu-id="30973-158">In the **SQL Server configuration** blade, click the **Edit** button in the Automated patching section.</span><span class="sxs-lookup"><span data-stu-id="30973-158">In the **SQL Server configuration** blade, click the **Edit** button in the Automated patching section.</span></span>

![Configure SQL Automated Patching for existing VMs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-sql-automated-patching/azure-sql-rm-patching-configuration.png)

<span data-ttu-id="30973-160">When finished, click the **OK** button on the bottom of the **SQL Server configuration** blade to save your changes.</span><span class="sxs-lookup"><span data-stu-id="30973-160">When finished, click the **OK** button on the bottom of the **SQL Server configuration** blade to save your changes.</span></span>

<span data-ttu-id="30973-161">If you are enabling Automated Patching for the first time, Azure configures the SQL Server IaaS Agent in the background.</span><span class="sxs-lookup"><span data-stu-id="30973-161">If you are enabling Automated Patching for the first time, Azure configures the SQL Server IaaS Agent in the background.</span></span> <span data-ttu-id="30973-162">During this time, the Azure portal might not show that Automated Patching is configured.</span><span class="sxs-lookup"><span data-stu-id="30973-162">During this time, the Azure portal might not show that Automated Patching is configured.</span></span> <span data-ttu-id="30973-163">Wait several minutes for the agent to be installed, configured.</span><span class="sxs-lookup"><span data-stu-id="30973-163">Wait several minutes for the agent to be installed, configured.</span></span> <span data-ttu-id="30973-164">After that the Azure portal reflects the new settings.</span><span class="sxs-lookup"><span data-stu-id="30973-164">After that the Azure portal reflects the new settings.</span></span>

> [!NOTE]
> You can also configure Automated Patching using a template. For more information, see [Azure quickstart template for Automated Patching](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autopatching-update).
> 
> 

## <a name="configuration-with-powershell"></a><span data-ttu-id="30973-167">Configuration with PowerShell</span><span class="sxs-lookup"><span data-stu-id="30973-167">Configuration with PowerShell</span></span>
<span data-ttu-id="30973-168">After provisioning your SQL VM, use PowerShell to configure Automated Patching.</span><span class="sxs-lookup"><span data-stu-id="30973-168">After provisioning your SQL VM, use PowerShell to configure Automated Patching.</span></span>

<span data-ttu-id="30973-169">In the following example, PowerShell is used to configure Automated Patching on an existing SQL Server VM.</span><span class="sxs-lookup"><span data-stu-id="30973-169">In the following example, PowerShell is used to configure Automated Patching on an existing SQL Server VM.</span></span> <span data-ttu-id="30973-170">The **AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig** command configures a new maintenance window for automatic updates.</span><span class="sxs-lookup"><span data-stu-id="30973-170">The **AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig** command configures a new maintenance window for automatic updates.</span></span>

    $vmname = "vmname"
    $resourcegroupname = "resourcegroupname"
    $aps = AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig -Enable -DayOfWeek "Thursday" -MaintenanceWindowStartingHour 11 -MaintenanceWindowDuration 120  -PatchCategory "Important"

    Set-AzureRmVMSqlServerExtension -AutoPatchingSettings $aps -VMName $vmname -ResourceGroupName $resourcegroupname

<span data-ttu-id="30973-171">Based on this example, the following table describes the practical effect on the target Azure VM:</span><span class="sxs-lookup"><span data-stu-id="30973-171">Based on this example, the following table describes the practical effect on the target Azure VM:</span></span>

| <span data-ttu-id="30973-172">Parameter</span><span class="sxs-lookup"><span data-stu-id="30973-172">Parameter</span></span> | <span data-ttu-id="30973-173">Effect</span><span class="sxs-lookup"><span data-stu-id="30973-173">Effect</span></span> |
| --- | --- |
| <span data-ttu-id="30973-174">**DayOfWeek**</span><span class="sxs-lookup"><span data-stu-id="30973-174">**DayOfWeek**</span></span> |<span data-ttu-id="30973-175">Patches installed every Thursday.</span><span class="sxs-lookup"><span data-stu-id="30973-175">Patches installed every Thursday.</span></span> |
| <span data-ttu-id="30973-176">**MaintenanceWindowStartingHour**</span><span class="sxs-lookup"><span data-stu-id="30973-176">**MaintenanceWindowStartingHour**</span></span> |<span data-ttu-id="30973-177">Begin updates at 11:00am.</span><span class="sxs-lookup"><span data-stu-id="30973-177">Begin updates at 11:00am.</span></span> |
| <span data-ttu-id="30973-178">**MaintenanceWindowsDuration**</span><span class="sxs-lookup"><span data-stu-id="30973-178">**MaintenanceWindowsDuration**</span></span> |<span data-ttu-id="30973-179">Patches must be installed within 120 minutes.</span><span class="sxs-lookup"><span data-stu-id="30973-179">Patches must be installed within 120 minutes.</span></span> <span data-ttu-id="30973-180">Based on the start time, they must complete by 1:00pm.</span><span class="sxs-lookup"><span data-stu-id="30973-180">Based on the start time, they must complete by 1:00pm.</span></span> |
| <span data-ttu-id="30973-181">**PatchCategory**</span><span class="sxs-lookup"><span data-stu-id="30973-181">**PatchCategory**</span></span> |<span data-ttu-id="30973-182">The only possible setting for this parameter is **Important**.</span><span class="sxs-lookup"><span data-stu-id="30973-182">The only possible setting for this parameter is **Important**.</span></span> |

<span data-ttu-id="30973-183">It could take several minutes to install and configure the SQL Server IaaS Agent.</span><span class="sxs-lookup"><span data-stu-id="30973-183">It could take several minutes to install and configure the SQL Server IaaS Agent.</span></span>

<span data-ttu-id="30973-184">To disable Automated Patching, run the same script without the **-Enable** parameter to the **AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig**.</span><span class="sxs-lookup"><span data-stu-id="30973-184">To disable Automated Patching, run the same script without the **-Enable** parameter to the **AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig**.</span></span> <span data-ttu-id="30973-185">The absence of the **-Enable** parameter signals the command to disable the feature.</span><span class="sxs-lookup"><span data-stu-id="30973-185">The absence of the **-Enable** parameter signals the command to disable the feature.</span></span>

## <a name="next-steps"></a><span data-ttu-id="30973-186">Next steps</span><span class="sxs-lookup"><span data-stu-id="30973-186">Next steps</span></span>
<span data-ttu-id="30973-187">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="30973-187">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

<span data-ttu-id="30973-188">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="30973-188">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>




