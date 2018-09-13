---
title: Automate management tasks on SQL VMs (Classic) | Microsoft Docs
description: This topic describes how to manage the SQL Server agent extension, which automates specific SQL Server administration tasks. These include Automated Backup, Automated Patching, and Azure Key Vault Integration. This topic uses the classic deployment mode.
services: virtual-machines-windows
documentationcenter: ''
author: rothja
manager: jhubbard
editor: ''
tags: azure-service-management
ms.assetid: a9bda2e7-cdba-427c-bc30-77cde4376f3a
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/18/2017
ms.author: jroth
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: aa68816a878959bdb3287c334ff87ab622fc5a05
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556141"
---
# <a name="automate-management-tasks-on-azure-virtual-machines-with-the-sql-server-agent-extension-classic"></a><span data-ttu-id="fe213-105">Automate management tasks on Azure Virtual Machines with the SQL Server Agent Extension (Classic)</span><span class="sxs-lookup"><span data-stu-id="fe213-105">Automate management tasks on Azure Virtual Machines with the SQL Server Agent Extension (Classic)</span></span>
> [!div class="op_single_selector"]
> * [Resource Manager](../sql/virtual-machines-windows-sql-server-agent-extension.md)
> * [Classic](../classic/sql-server-agent-extension.md)
> 
>
 
<span data-ttu-id="fe213-108">The SQL Server IaaS Agent Extension (SQLIaaSAgent) runs on Azure virtual machines to automate administration tasks.</span><span class="sxs-lookup"><span data-stu-id="fe213-108">The SQL Server IaaS Agent Extension (SQLIaaSAgent) runs on Azure virtual machines to automate administration tasks.</span></span> <span data-ttu-id="fe213-109">This topic provides an overview of the services supported by the extension as well as instructions for installation, status, and removal.</span><span class="sxs-lookup"><span data-stu-id="fe213-109">This topic provides an overview of the services supported by the extension as well as instructions for installation, status, and removal.</span></span>

> [!IMPORTANT] 
> Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md). This article covers using the Classic deployment model. Microsoft recommends that most new deployments use the Resource Manager model. To view the Resource Manager version of this article, see [SQL Server Agent Extension for SQL Server VMs Resource Manager](../sql/virtual-machines-windows-sql-server-agent-extension.md).

## <a name="supported-services"></a><span data-ttu-id="fe213-114">Supported services</span><span class="sxs-lookup"><span data-stu-id="fe213-114">Supported services</span></span>
<span data-ttu-id="fe213-115">The SQL Server IaaS Agent Extension supports the following administration tasks:</span><span class="sxs-lookup"><span data-stu-id="fe213-115">The SQL Server IaaS Agent Extension supports the following administration tasks:</span></span>

| <span data-ttu-id="fe213-116">Administration feature</span><span class="sxs-lookup"><span data-stu-id="fe213-116">Administration feature</span></span> | <span data-ttu-id="fe213-117">Description</span><span class="sxs-lookup"><span data-stu-id="fe213-117">Description</span></span> |
| --- | --- |
| <span data-ttu-id="fe213-118">**SQL Automated Backup**</span><span class="sxs-lookup"><span data-stu-id="fe213-118">**SQL Automated Backup**</span></span> |<span data-ttu-id="fe213-119">Automates the scheduling of backups for all databases for the default instance of SQL Server in the VM.</span><span class="sxs-lookup"><span data-stu-id="fe213-119">Automates the scheduling of backups for all databases for the default instance of SQL Server in the VM.</span></span> <span data-ttu-id="fe213-120">For more information, see [Automated backup for SQL Server in Azure Virtual Machines (Classic)](../classic/sql-automated-backup.md).</span><span class="sxs-lookup"><span data-stu-id="fe213-120">For more information, see [Automated backup for SQL Server in Azure Virtual Machines (Classic)](../classic/sql-automated-backup.md).</span></span> |
| <span data-ttu-id="fe213-121">**SQL Automated Patching**</span><span class="sxs-lookup"><span data-stu-id="fe213-121">**SQL Automated Patching**</span></span> |<span data-ttu-id="fe213-122">Configures a maintenance window during which updates to your VM can take place, so  you can avoid updates during peak times for your workload.</span><span class="sxs-lookup"><span data-stu-id="fe213-122">Configures a maintenance window during which updates to your VM can take place, so  you can avoid updates during peak times for your workload.</span></span> <span data-ttu-id="fe213-123">For more information, see [Automated patching for SQL Server in Azure Virtual Machines (Classic)](../classic/sql-automated-patching.md).</span><span class="sxs-lookup"><span data-stu-id="fe213-123">For more information, see [Automated patching for SQL Server in Azure Virtual Machines (Classic)](../classic/sql-automated-patching.md).</span></span> |
| <span data-ttu-id="fe213-124">**Azure Key Vault Integration**</span><span class="sxs-lookup"><span data-stu-id="fe213-124">**Azure Key Vault Integration**</span></span> |<span data-ttu-id="fe213-125">Enables you to automatically install and configure Azure Key Vault on your SQL Server VM.</span><span class="sxs-lookup"><span data-stu-id="fe213-125">Enables you to automatically install and configure Azure Key Vault on your SQL Server VM.</span></span> <span data-ttu-id="fe213-126">For more information, see [Configure Azure Key Vault Integration for SQL Server on Azure VMs (Classic)](../classic/ps-sql-keyvault.md).</span><span class="sxs-lookup"><span data-stu-id="fe213-126">For more information, see [Configure Azure Key Vault Integration for SQL Server on Azure VMs (Classic)](../classic/ps-sql-keyvault.md).</span></span> |

## <a name="prerequisites"></a><span data-ttu-id="fe213-127">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="fe213-127">Prerequisites</span></span>
<span data-ttu-id="fe213-128">Requirements to use the SQL Server IaaS Agent Extension on your VM:</span><span class="sxs-lookup"><span data-stu-id="fe213-128">Requirements to use the SQL Server IaaS Agent Extension on your VM:</span></span>

### <a name="operating-system"></a><span data-ttu-id="fe213-129">Operating System:</span><span class="sxs-lookup"><span data-stu-id="fe213-129">Operating System:</span></span>
* <span data-ttu-id="fe213-130">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="fe213-130">Windows Server 2012</span></span>
* <span data-ttu-id="fe213-131">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="fe213-131">Windows Server 2012 R2</span></span>

### <a name="sql-server-versions"></a><span data-ttu-id="fe213-132">SQL Server versions:</span><span class="sxs-lookup"><span data-stu-id="fe213-132">SQL Server versions:</span></span>
* <span data-ttu-id="fe213-133">SQL Server 2012</span><span class="sxs-lookup"><span data-stu-id="fe213-133">SQL Server 2012</span></span>
* <span data-ttu-id="fe213-134">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="fe213-134">SQL Server 2014</span></span>
* <span data-ttu-id="fe213-135">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="fe213-135">SQL Server 2016</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="fe213-136">Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="fe213-136">Azure PowerShell:</span></span>
<span data-ttu-id="fe213-137">[Download and configure the latest Azure PowerShell commands](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="fe213-137">[Download and configure the latest Azure PowerShell commands](/powershell/azureps-cmdlets-docs).</span></span>

<span data-ttu-id="fe213-138">Start Windows PowerShell, and connect it to your Azure subscription with the **Add-AzureAccount** command.</span><span class="sxs-lookup"><span data-stu-id="fe213-138">Start Windows PowerShell, and connect it to your Azure subscription with the **Add-AzureAccount** command.</span></span>

    Add-AzureAccount

<span data-ttu-id="fe213-139">If you have multiple subscriptions, use **Select-AzureSubscription** to select the subscription that contains your target classic VM.</span><span class="sxs-lookup"><span data-stu-id="fe213-139">If you have multiple subscriptions, use **Select-AzureSubscription** to select the subscription that contains your target classic VM.</span></span>

    Select-AzureSubscription -SubscriptionName <subscriptionname>

<span data-ttu-id="fe213-140">At this point, you can get a list of the classic virtual machines and their associated service names with the **Get-AzureVM** command.</span><span class="sxs-lookup"><span data-stu-id="fe213-140">At this point, you can get a list of the classic virtual machines and their associated service names with the **Get-AzureVM** command.</span></span>

    Get-AzureVM

## <a name="installation"></a><span data-ttu-id="fe213-141">Installation</span><span class="sxs-lookup"><span data-stu-id="fe213-141">Installation</span></span>
<span data-ttu-id="fe213-142">For classic VMs, you must use PowerShell to install the SQL Server IaaS Agent Extension and configure its associated services.</span><span class="sxs-lookup"><span data-stu-id="fe213-142">For classic VMs, you must use PowerShell to install the SQL Server IaaS Agent Extension and configure its associated services.</span></span> <span data-ttu-id="fe213-143">Use the **Set-AzureVMSqlServerExtension** PowerShell cmdlet to install the extension.</span><span class="sxs-lookup"><span data-stu-id="fe213-143">Use the **Set-AzureVMSqlServerExtension** PowerShell cmdlet to install the extension.</span></span> <span data-ttu-id="fe213-144">For example, the following command installs the extension on a Windows Server VM (classic) and names it "SQLIaaSExtension".</span><span class="sxs-lookup"><span data-stu-id="fe213-144">For example, the following command installs the extension on a Windows Server VM (classic) and names it "SQLIaaSExtension".</span></span>

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -ReferenceName "SQLIaasExtension" -Version "1.2" | Update-AzureVM

<span data-ttu-id="fe213-145">If you update to the latest version of the SQL IaaS Agent Extension, you must restart your virtual machine after updating the extension.</span><span class="sxs-lookup"><span data-stu-id="fe213-145">If you update to the latest version of the SQL IaaS Agent Extension, you must restart your virtual machine after updating the extension.</span></span>

> [!NOTE]
> Classic virtual machines do not have an option to install and configure the SQL IaaS Agent Extension through the portal.
> 
> 

## <a name="status"></a><span data-ttu-id="fe213-147">Status</span><span class="sxs-lookup"><span data-stu-id="fe213-147">Status</span></span>
<span data-ttu-id="fe213-148">One way to verify that the extension is installed is to view the agent status in the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="fe213-148">One way to verify that the extension is installed is to view the agent status in the Azure Portal.</span></span> <span data-ttu-id="fe213-149">Select a virtual machine listed in the virtual machine blade, and then click on **Extensions**.</span><span class="sxs-lookup"><span data-stu-id="fe213-149">Select a virtual machine listed in the virtual machine blade, and then click on **Extensions**.</span></span> <span data-ttu-id="fe213-150">You should see the **SQLIaaSAgent** extension listed.</span><span class="sxs-lookup"><span data-stu-id="fe213-150">You should see the **SQLIaaSAgent** extension listed.</span></span>

![SQL Server IaaS Agent Extension in Azure Portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sqlclassic/media/virtual-machines-windows-classic-sql-server-agent-extension/azure-sql-server-iaas-agent-portal.png)

<span data-ttu-id="fe213-152">You can also use the **Get-AzureVMSqlServerExtension** Azure Powershell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="fe213-152">You can also use the **Get-AzureVMSqlServerExtension** Azure Powershell cmdlet.</span></span>

    Get-AzureVM –ServiceName "service" –Name "vmname" | Get-AzureVMSqlServerExtension

## <a name="removal"></a><span data-ttu-id="fe213-153">Removal</span><span class="sxs-lookup"><span data-stu-id="fe213-153">Removal</span></span>
<span data-ttu-id="fe213-154">In the Azure Portal, you can uninstall the extension by clicking the ellipsis on the **Extensions** blade of your virtual machine properties.</span><span class="sxs-lookup"><span data-stu-id="fe213-154">In the Azure Portal, you can uninstall the extension by clicking the ellipsis on the **Extensions** blade of your virtual machine properties.</span></span> <span data-ttu-id="fe213-155">Then click **Uninstall**.</span><span class="sxs-lookup"><span data-stu-id="fe213-155">Then click **Uninstall**.</span></span>

![Uninstall the SQL Server IaaS Agent Extension in Azure Portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sqlclassic/media/virtual-machines-windows-classic-sql-server-agent-extension/azure-sql-server-iaas-agent-uninstall.png)

<span data-ttu-id="fe213-157">You can also use the **Remove-AzureVMSqlServerExtension** Powershell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="fe213-157">You can also use the **Remove-AzureVMSqlServerExtension** Powershell cmdlet.</span></span>

    Get-AzureVM –ServiceName "service" –Name "vmname" | Remove-AzureVMSqlServerExtension | Update-AzureVM

## <a name="next-steps"></a><span data-ttu-id="fe213-158">Next Steps</span><span class="sxs-lookup"><span data-stu-id="fe213-158">Next Steps</span></span>
<span data-ttu-id="fe213-159">Begin using one of the services supported by the extension.</span><span class="sxs-lookup"><span data-stu-id="fe213-159">Begin using one of the services supported by the extension.</span></span> <span data-ttu-id="fe213-160">For more details, see the topics referenced in the [Supported services](#supported-services) section of this article.</span><span class="sxs-lookup"><span data-stu-id="fe213-160">For more details, see the topics referenced in the [Supported services](#supported-services) section of this article.</span></span>

<span data-ttu-id="fe213-161">For more information about running SQL Server on Azure Virtual Machines, see [SQL Server on Azure Virtual Machines overview](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fe213-161">For more information about running SQL Server on Azure Virtual Machines, see [SQL Server on Azure Virtual Machines overview](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>



