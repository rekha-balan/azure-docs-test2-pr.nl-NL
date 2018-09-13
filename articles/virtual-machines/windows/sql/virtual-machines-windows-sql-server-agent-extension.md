---
title: Automate management tasks on SQL VMs (Resource Manager) | Microsoft Docs
description: This topic describes how to manage the SQL Server agent extension, which automates specific SQL Server administration tasks. These include Automated Backup, Automated Patching, and Azure Key Vault Integration. This topic uses the Resource Manager deployment mode.
services: virtual-machines-windows
documentationcenter: ''
author: rothja
manager: jhubbard
editor: ''
tags: azure-resource-manager
ms.assetid: effe4e2f-35b5-490a-b5ef-b06746083da4
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/09/2017
ms.author: jroth
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 306d2979cf3d879b70495cf3b5cc127c2ea4753a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563407"
---
# <a name="automate-management-tasks-on-azure-virtual-machines-with-the-sql-server-agent-extension-resource-manager"></a><span data-ttu-id="72b36-105">Automate management tasks on Azure Virtual Machines with the SQL Server Agent Extension (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="72b36-105">Automate management tasks on Azure Virtual Machines with the SQL Server Agent Extension (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [Resource Manager](virtual-machines-windows-sql-server-agent-extension.md)
> * [Classic](../classic/sql-server-agent-extension.md)
> 
> 

<span data-ttu-id="72b36-108">The SQL Server IaaS Agent Extension (SQLIaaSExtension) runs on Azure virtual machines to automate administration tasks.</span><span class="sxs-lookup"><span data-stu-id="72b36-108">The SQL Server IaaS Agent Extension (SQLIaaSExtension) runs on Azure virtual machines to automate administration tasks.</span></span> <span data-ttu-id="72b36-109">This topic provides an overview of the services supported by the extension as well as instructions for installation, status, and removal.</span><span class="sxs-lookup"><span data-stu-id="72b36-109">This topic provides an overview of the services supported by the extension as well as instructions for installation, status, and removal.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="72b36-110">To view the classic version of this article, see [SQL Server Agent Extension for SQL Server VMs Classic](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="72b36-110">To view the classic version of this article, see [SQL Server Agent Extension for SQL Server VMs Classic](../classic/sql-server-agent-extension.md).</span></span>

## <a name="supported-services"></a><span data-ttu-id="72b36-111">Supported services</span><span class="sxs-lookup"><span data-stu-id="72b36-111">Supported services</span></span>
<span data-ttu-id="72b36-112">The SQL Server IaaS Agent Extension supports the following administration tasks:</span><span class="sxs-lookup"><span data-stu-id="72b36-112">The SQL Server IaaS Agent Extension supports the following administration tasks:</span></span>

| <span data-ttu-id="72b36-113">Administration feature</span><span class="sxs-lookup"><span data-stu-id="72b36-113">Administration feature</span></span> | <span data-ttu-id="72b36-114">Description</span><span class="sxs-lookup"><span data-stu-id="72b36-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="72b36-115">**SQL Automated Backup**</span><span class="sxs-lookup"><span data-stu-id="72b36-115">**SQL Automated Backup**</span></span> |<span data-ttu-id="72b36-116">Automates the scheduling of backups for all databases for the default instance of SQL Server in the VM.</span><span class="sxs-lookup"><span data-stu-id="72b36-116">Automates the scheduling of backups for all databases for the default instance of SQL Server in the VM.</span></span> <span data-ttu-id="72b36-117">For more information, see [Automated backup for SQL Server in Azure Virtual Machines (Resource Manager)](virtual-machines-windows-sql-automated-backup.md).</span><span class="sxs-lookup"><span data-stu-id="72b36-117">For more information, see [Automated backup for SQL Server in Azure Virtual Machines (Resource Manager)](virtual-machines-windows-sql-automated-backup.md).</span></span> |
| <span data-ttu-id="72b36-118">**SQL Automated Patching**</span><span class="sxs-lookup"><span data-stu-id="72b36-118">**SQL Automated Patching**</span></span> |<span data-ttu-id="72b36-119">Configures a maintenance window during which updates to your VM can take place, so  you can avoid updates during peak times for your workload.</span><span class="sxs-lookup"><span data-stu-id="72b36-119">Configures a maintenance window during which updates to your VM can take place, so  you can avoid updates during peak times for your workload.</span></span> <span data-ttu-id="72b36-120">For more information, see [Automated patching for SQL Server in Azure Virtual Machines (Resource Manager)](virtual-machines-windows-sql-automated-patching.md).</span><span class="sxs-lookup"><span data-stu-id="72b36-120">For more information, see [Automated patching for SQL Server in Azure Virtual Machines (Resource Manager)](virtual-machines-windows-sql-automated-patching.md).</span></span> |
| <span data-ttu-id="72b36-121">**Azure Key Vault Integration**</span><span class="sxs-lookup"><span data-stu-id="72b36-121">**Azure Key Vault Integration**</span></span> |<span data-ttu-id="72b36-122">Enables you to automatically install and configure Azure Key Vault on your SQL Server VM.</span><span class="sxs-lookup"><span data-stu-id="72b36-122">Enables you to automatically install and configure Azure Key Vault on your SQL Server VM.</span></span> <span data-ttu-id="72b36-123">For more information, see [Configure Azure Key Vault Integration for SQL Server on Azure VMs (Resource Manager)](virtual-machines-windows-ps-sql-keyvault.md).</span><span class="sxs-lookup"><span data-stu-id="72b36-123">For more information, see [Configure Azure Key Vault Integration for SQL Server on Azure VMs (Resource Manager)](virtual-machines-windows-ps-sql-keyvault.md).</span></span> |

## <a name="prerequisites"></a><span data-ttu-id="72b36-124">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="72b36-124">Prerequisites</span></span>
<span data-ttu-id="72b36-125">Requirements to use the SQL Server IaaS Agent Extension on your VM:</span><span class="sxs-lookup"><span data-stu-id="72b36-125">Requirements to use the SQL Server IaaS Agent Extension on your VM:</span></span>

<span data-ttu-id="72b36-126">**Operating System**:</span><span class="sxs-lookup"><span data-stu-id="72b36-126">**Operating System**:</span></span>

* <span data-ttu-id="72b36-127">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="72b36-127">Windows Server 2012</span></span>
* <span data-ttu-id="72b36-128">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="72b36-128">Windows Server 2012 R2</span></span>
* <span data-ttu-id="72b36-129">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="72b36-129">Windows Server 2016</span></span>

<span data-ttu-id="72b36-130">**SQL Server versions**:</span><span class="sxs-lookup"><span data-stu-id="72b36-130">**SQL Server versions**:</span></span>

* <span data-ttu-id="72b36-131">SQL Server 2012</span><span class="sxs-lookup"><span data-stu-id="72b36-131">SQL Server 2012</span></span>
* <span data-ttu-id="72b36-132">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="72b36-132">SQL Server 2014</span></span>
* <span data-ttu-id="72b36-133">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="72b36-133">SQL Server 2016</span></span>

<span data-ttu-id="72b36-134">**Azure PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="72b36-134">**Azure PowerShell**:</span></span>

* [<span data-ttu-id="72b36-135">Download and configure the latest Azure PowerShell commands</span><span class="sxs-lookup"><span data-stu-id="72b36-135">Download and configure the latest Azure PowerShell commands</span></span>](/powershell/azureps-cmdlets-docs)

## <a name="installation"></a><span data-ttu-id="72b36-136">Installation</span><span class="sxs-lookup"><span data-stu-id="72b36-136">Installation</span></span>
<span data-ttu-id="72b36-137">The SQL Server IaaS Agent Extension is automatically installed when you provision one of the SQL Server virtual machine gallery images.</span><span class="sxs-lookup"><span data-stu-id="72b36-137">The SQL Server IaaS Agent Extension is automatically installed when you provision one of the SQL Server virtual machine gallery images.</span></span>

<span data-ttu-id="72b36-138">If you create an OS-only Windows Server virtual machine, you can install the extension manually by using the **Set-AzureVMSqlServerExtension** PowerShell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="72b36-138">If you create an OS-only Windows Server virtual machine, you can install the extension manually by using the **Set-AzureVMSqlServerExtension** PowerShell cmdlet.</span></span> <span data-ttu-id="72b36-139">For example, the following command installs the extension on an OS-only Windows Server VM and names it "SQLIaaSExtension".</span><span class="sxs-lookup"><span data-stu-id="72b36-139">For example, the following command installs the extension on an OS-only Windows Server VM and names it "SQLIaaSExtension".</span></span>

    Set-AzureRmVMSqlServerExtension -ResourceGroupName "resourcegroupname" -VMName "vmname" -Name "SQLIaasExtension" -Version "1.2" -Location "East US 2"

<span data-ttu-id="72b36-140">If you update to the latest version of the SQL IaaS Agent Extension, you must restart your virtual machine after updating the extension.</span><span class="sxs-lookup"><span data-stu-id="72b36-140">If you update to the latest version of the SQL IaaS Agent Extension, you must restart your virtual machine after updating the extension.</span></span>

> [!NOTE]
> If you install the SQL Server IaaS Agent Extension manually on a Windows Server VM, you must use and manage its features using PowerShell commands. The portal interface is available only for SQL Server gallery images.
> 
> 

## <a name="status"></a><span data-ttu-id="72b36-143">Status</span><span class="sxs-lookup"><span data-stu-id="72b36-143">Status</span></span>
<span data-ttu-id="72b36-144">One way to verify that the extension is installed is to view the agent status in the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="72b36-144">One way to verify that the extension is installed is to view the agent status in the Azure Portal.</span></span> <span data-ttu-id="72b36-145">Select **All settings** in the virtual machine blade, and then click on **Extensions**.</span><span class="sxs-lookup"><span data-stu-id="72b36-145">Select **All settings** in the virtual machine blade, and then click on **Extensions**.</span></span> <span data-ttu-id="72b36-146">You should see the **SQLIaaSExtension** extension listed.</span><span class="sxs-lookup"><span data-stu-id="72b36-146">You should see the **SQLIaaSExtension** extension listed.</span></span>

![SQL Server IaaS Agent Extension in Azure Portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-sql-server-agent-extension/azure-rm-sql-server-iaas-agent-portal.png)

<span data-ttu-id="72b36-148">You can also use the **Get-AzureVMSqlServerExtension** Azure Powershell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="72b36-148">You can also use the **Get-AzureVMSqlServerExtension** Azure Powershell cmdlet.</span></span>

    Get-AzureRmVMSqlServerExtension -VMName "vmname" -ResourceGroupName "resourcegroupname"

<span data-ttu-id="72b36-149">The previous command confirms the agent is installed and provides general status information.</span><span class="sxs-lookup"><span data-stu-id="72b36-149">The previous command confirms the agent is installed and provides general status information.</span></span> <span data-ttu-id="72b36-150">You can also get specific status information about Automated Backup and Patching with the following commands.</span><span class="sxs-lookup"><span data-stu-id="72b36-150">You can also get specific status information about Automated Backup and Patching with the following commands.</span></span>

    $sqlext = Get-AzureRmVMSqlServerExtension -VMName "vmname" -ResourceGroupName "resourcegroupname"
    $sqlext.AutoPatchingSettings
    $sqlext.AutoBackupSettings

## <a name="removal"></a><span data-ttu-id="72b36-151">Removal</span><span class="sxs-lookup"><span data-stu-id="72b36-151">Removal</span></span>
<span data-ttu-id="72b36-152">In the Azure Portal, you can uninstall the extension by clicking the ellipsis on the **Extensions** blade of your virtual machine properties.</span><span class="sxs-lookup"><span data-stu-id="72b36-152">In the Azure Portal, you can uninstall the extension by clicking the ellipsis on the **Extensions** blade of your virtual machine properties.</span></span> <span data-ttu-id="72b36-153">Then click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="72b36-153">Then click **Delete**.</span></span>

![Uninstall the SQL Server IaaS Agent Extension in Azure Portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-sql-server-agent-extension/azure-rm-sql-server-iaas-agent-uninstall.png)

<span data-ttu-id="72b36-155">You can also use the **Remove-AzureRmVMSqlServerExtension** Powershell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="72b36-155">You can also use the **Remove-AzureRmVMSqlServerExtension** Powershell cmdlet.</span></span>

    Remove-AzureRmVMSqlServerExtension -ResourceGroupName "resourcegroupname" -VMName "vmname" -Name "SQLIaasExtension"

## <a name="next-steps"></a><span data-ttu-id="72b36-156">Next Steps</span><span class="sxs-lookup"><span data-stu-id="72b36-156">Next Steps</span></span>
<span data-ttu-id="72b36-157">Begin using one of the services supported by the extension.</span><span class="sxs-lookup"><span data-stu-id="72b36-157">Begin using one of the services supported by the extension.</span></span> <span data-ttu-id="72b36-158">For more details, see the topics referenced in the [Supported services](#supported-services) section of this article.</span><span class="sxs-lookup"><span data-stu-id="72b36-158">For more details, see the topics referenced in the [Supported services](#supported-services) section of this article.</span></span>

<span data-ttu-id="72b36-159">For more information about running SQL Server on Azure Virtual Machines, see [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="72b36-159">For more information about running SQL Server on Azure Virtual Machines, see [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>



