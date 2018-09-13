---
title: Automate management tasks on SQL VMs (Resource Manager) | Microsoft Docs
description: This article describes how to manage the SQL Server agent extension, which automates specific SQL Server administration tasks. These include Automated Backup, Automated Patching, and Azure Key Vault Integration.
services: virtual-machines-windows
documentationcenter: ''
author: rothja
manager: craigg
editor: ''
tags: azure-resource-manager
ms.assetid: effe4e2f-35b5-490a-b5ef-b06746083da4
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/12/2018
ms.author: jroth
ms.openlocfilehash: c663aec02d4d1808426a9f05a6674d5504563a63
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44804302"
---
# <a name="automate-management-tasks-on-azure-virtual-machines-with-the-sql-server-agent-extension-resource-manager"></a><span data-ttu-id="8a2c6-104">Automate management tasks on Azure Virtual Machines with the SQL Server Agent Extension (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="8a2c6-104">Automate management tasks on Azure Virtual Machines with the SQL Server Agent Extension (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [Resource Manager](virtual-machines-windows-sql-server-agent-extension.md)
> * [Classic](../sqlclassic/virtual-machines-windows-classic-sql-server-agent-extension.md)

<span data-ttu-id="8a2c6-107">The SQL Server IaaS Agent Extension (SQLIaaSExtension) runs on Azure virtual machines to automate administration tasks.</span><span class="sxs-lookup"><span data-stu-id="8a2c6-107">The SQL Server IaaS Agent Extension (SQLIaaSExtension) runs on Azure virtual machines to automate administration tasks.</span></span> <span data-ttu-id="8a2c6-108">This article provides an overview of the services supported by the extension as well as instructions for installation, status, and removal.</span><span class="sxs-lookup"><span data-stu-id="8a2c6-108">This article provides an overview of the services supported by the extension as well as instructions for installation, status, and removal.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="8a2c6-109">To view the classic version of this article, see [SQL Server Agent Extension for SQL Server VMs Classic](../sqlclassic/virtual-machines-windows-classic-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="8a2c6-109">To view the classic version of this article, see [SQL Server Agent Extension for SQL Server VMs Classic](../sqlclassic/virtual-machines-windows-classic-sql-server-agent-extension.md).</span></span>

## <a name="supported-services"></a><span data-ttu-id="8a2c6-110">Supported services</span><span class="sxs-lookup"><span data-stu-id="8a2c6-110">Supported services</span></span>
<span data-ttu-id="8a2c6-111">The SQL Server IaaS Agent Extension supports the following administration tasks:</span><span class="sxs-lookup"><span data-stu-id="8a2c6-111">The SQL Server IaaS Agent Extension supports the following administration tasks:</span></span>

| <span data-ttu-id="8a2c6-112">Administration feature</span><span class="sxs-lookup"><span data-stu-id="8a2c6-112">Administration feature</span></span> | <span data-ttu-id="8a2c6-113">Description</span><span class="sxs-lookup"><span data-stu-id="8a2c6-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8a2c6-114">**SQL Automated Backup**</span><span class="sxs-lookup"><span data-stu-id="8a2c6-114">**SQL Automated Backup**</span></span> |<span data-ttu-id="8a2c6-115">Automates the scheduling of backups for all databases for the default instance of SQL Server in the VM.</span><span class="sxs-lookup"><span data-stu-id="8a2c6-115">Automates the scheduling of backups for all databases for the default instance of SQL Server in the VM.</span></span> <span data-ttu-id="8a2c6-116">For more information, see [Automated backup for SQL Server in Azure Virtual Machines (Resource Manager)](virtual-machines-windows-sql-automated-backup.md).</span><span class="sxs-lookup"><span data-stu-id="8a2c6-116">For more information, see [Automated backup for SQL Server in Azure Virtual Machines (Resource Manager)](virtual-machines-windows-sql-automated-backup.md).</span></span> |
| <span data-ttu-id="8a2c6-117">**SQL Automated Patching**</span><span class="sxs-lookup"><span data-stu-id="8a2c6-117">**SQL Automated Patching**</span></span> |<span data-ttu-id="8a2c6-118">Configures a maintenance window during which important Windows updates to your VM can take place, so  you can avoid updates during peak times for your workload.</span><span class="sxs-lookup"><span data-stu-id="8a2c6-118">Configures a maintenance window during which important Windows updates to your VM can take place, so  you can avoid updates during peak times for your workload.</span></span> <span data-ttu-id="8a2c6-119">For more information, see [Automated patching for SQL Server in Azure Virtual Machines (Resource Manager)](virtual-machines-windows-sql-automated-patching.md).</span><span class="sxs-lookup"><span data-stu-id="8a2c6-119">For more information, see [Automated patching for SQL Server in Azure Virtual Machines (Resource Manager)](virtual-machines-windows-sql-automated-patching.md).</span></span> |
| <span data-ttu-id="8a2c6-120">**Azure Key Vault Integration**</span><span class="sxs-lookup"><span data-stu-id="8a2c6-120">**Azure Key Vault Integration**</span></span> |<span data-ttu-id="8a2c6-121">Enables you to automatically install and configure Azure Key Vault on your SQL Server VM.</span><span class="sxs-lookup"><span data-stu-id="8a2c6-121">Enables you to automatically install and configure Azure Key Vault on your SQL Server VM.</span></span> <span data-ttu-id="8a2c6-122">For more information, see [Configure Azure Key Vault Integration for SQL Server on Azure VMs (Resource Manager)](virtual-machines-windows-ps-sql-keyvault.md).</span><span class="sxs-lookup"><span data-stu-id="8a2c6-122">For more information, see [Configure Azure Key Vault Integration for SQL Server on Azure VMs (Resource Manager)](virtual-machines-windows-ps-sql-keyvault.md).</span></span> |

<span data-ttu-id="8a2c6-123">Once installed and running, the SQL Server IaaS Agent Extension makes these administration features available on the SQL Server panel of the virtual machine in the Azure portal and through Azure PowerShell for SQL Server marketplace images, and through Azure PowerShell for manual installations of the extension.</span><span class="sxs-lookup"><span data-stu-id="8a2c6-123">Once installed and running, the SQL Server IaaS Agent Extension makes these administration features available on the SQL Server panel of the virtual machine in the Azure portal and through Azure PowerShell for SQL Server marketplace images, and through Azure PowerShell for manual installations of the extension.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="8a2c6-124">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="8a2c6-124">Prerequisites</span></span>
<span data-ttu-id="8a2c6-125">Requirements to use the SQL Server IaaS Agent Extension on your VM:</span><span class="sxs-lookup"><span data-stu-id="8a2c6-125">Requirements to use the SQL Server IaaS Agent Extension on your VM:</span></span>

<span data-ttu-id="8a2c6-126">**Operating System**:</span><span class="sxs-lookup"><span data-stu-id="8a2c6-126">**Operating System**:</span></span>

* <span data-ttu-id="8a2c6-127">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="8a2c6-127">Windows Server 2012</span></span>
* <span data-ttu-id="8a2c6-128">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="8a2c6-128">Windows Server 2012 R2</span></span>
* <span data-ttu-id="8a2c6-129">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="8a2c6-129">Windows Server 2016</span></span>

<span data-ttu-id="8a2c6-130">**SQL Server versions**:</span><span class="sxs-lookup"><span data-stu-id="8a2c6-130">**SQL Server versions**:</span></span>

* <span data-ttu-id="8a2c6-131">SQL Server 2012</span><span class="sxs-lookup"><span data-stu-id="8a2c6-131">SQL Server 2012</span></span>
* <span data-ttu-id="8a2c6-132">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="8a2c6-132">SQL Server 2014</span></span>
* <span data-ttu-id="8a2c6-133">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="8a2c6-133">SQL Server 2016</span></span>

<span data-ttu-id="8a2c6-134">**Azure PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="8a2c6-134">**Azure PowerShell**:</span></span>

* [<span data-ttu-id="8a2c6-135">Download and configure the latest Azure PowerShell commands</span><span class="sxs-lookup"><span data-stu-id="8a2c6-135">Download and configure the latest Azure PowerShell commands</span></span>](/powershell/azure/overview)

> [!IMPORTANT]
> At this time, the [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md) is not supported for SQL Server FCI on Azure. We recommend that you uninstall the extension from VMs that participate in an FCI. The features supported by the extension are not available to the SQL VMs after the agent is uninstalled.

## <a name="installation"></a><span data-ttu-id="8a2c6-139">Installation</span><span class="sxs-lookup"><span data-stu-id="8a2c6-139">Installation</span></span>
<span data-ttu-id="8a2c6-140">The SQL Server IaaS Agent Extension is automatically installed when you provision one of the SQL Server virtual machine gallery images.</span><span class="sxs-lookup"><span data-stu-id="8a2c6-140">The SQL Server IaaS Agent Extension is automatically installed when you provision one of the SQL Server virtual machine gallery images.</span></span> <span data-ttu-id="8a2c6-141">If you need to reinstall the extension manually on one of these SQL Server VMs, use the following PowerShell command:</span><span class="sxs-lookup"><span data-stu-id="8a2c6-141">If you need to reinstall the extension manually on one of these SQL Server VMs, use the following PowerShell command:</span></span>

```powershell
Set-AzureRmVMSqlServerExtension -ResourceGroupName "resourcegroupname" -VMName "vmname" -Name "SQLIaasExtension" -Version "1.2" -Location "East US 2"
```

> [!IMPORTANT]
> If the extension is not already installed, installing the extension restarts the SQL Server service.

> [!NOTE]
> The SQL Server IaaS Agent Extension is only supported on [SQL Server VM gallery images](virtual-machines-windows-sql-server-iaas-overview.md#get-started-with-sql-vms) (pay-as-you-go or bring-your-own-license). It is not supported if you manually install SQL Server on an OS-only Windows Server virtual machine or if you deploy a customized SQL Server VM VHD. In these cases, it might be possible to install and manage the extension manually by using PowerShell, but you do not get the SQL Server configuration settings in the Azure portal. However, it is strongly recommended to instead install a SQL Server VM gallery image and then customize it.

## <a name="status"></a><span data-ttu-id="8a2c6-147">Status</span><span class="sxs-lookup"><span data-stu-id="8a2c6-147">Status</span></span>
<span data-ttu-id="8a2c6-148">One way to verify that the extension is installed is to view the agent status in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="8a2c6-148">One way to verify that the extension is installed is to view the agent status in the Azure portal.</span></span> <span data-ttu-id="8a2c6-149">Select **All settings** in the virtual machine window, and then click on **Extensions**.</span><span class="sxs-lookup"><span data-stu-id="8a2c6-149">Select **All settings** in the virtual machine window, and then click on **Extensions**.</span></span> <span data-ttu-id="8a2c6-150">You should see the **SQLIaaSExtension** extension listed.</span><span class="sxs-lookup"><span data-stu-id="8a2c6-150">You should see the **SQLIaaSExtension** extension listed.</span></span>

![SQL Server IaaS Agent Extension in Azure portal](./media/virtual-machines-windows-sql-server-agent-extension/azure-rm-sql-server-iaas-agent-portal.png)

<span data-ttu-id="8a2c6-152">You can also use the **Get-AzureRmVMSqlServerExtension** Azure PowerShell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8a2c6-152">You can also use the **Get-AzureRmVMSqlServerExtension** Azure PowerShell cmdlet.</span></span>

    Get-AzureRmVMSqlServerExtension -VMName "vmname" -ResourceGroupName "resourcegroupname"

<span data-ttu-id="8a2c6-153">The previous command confirms the agent is installed and provides general status information.</span><span class="sxs-lookup"><span data-stu-id="8a2c6-153">The previous command confirms the agent is installed and provides general status information.</span></span> <span data-ttu-id="8a2c6-154">You can also get specific status information about Automated Backup and Patching with the following commands.</span><span class="sxs-lookup"><span data-stu-id="8a2c6-154">You can also get specific status information about Automated Backup and Patching with the following commands.</span></span>

    $sqlext = Get-AzureRmVMSqlServerExtension -VMName "vmname" -ResourceGroupName "resourcegroupname"
    $sqlext.AutoPatchingSettings
    $sqlext.AutoBackupSettings

## <a name="removal"></a><span data-ttu-id="8a2c6-155">Removal</span><span class="sxs-lookup"><span data-stu-id="8a2c6-155">Removal</span></span>
<span data-ttu-id="8a2c6-156">In the Azure Portal, you can uninstall the extension by clicking the ellipsis on the **Extensions** window of your virtual machine properties.</span><span class="sxs-lookup"><span data-stu-id="8a2c6-156">In the Azure Portal, you can uninstall the extension by clicking the ellipsis on the **Extensions** window of your virtual machine properties.</span></span> <span data-ttu-id="8a2c6-157">Then click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="8a2c6-157">Then click **Delete**.</span></span>

![Uninstall the SQL Server IaaS Agent Extension in Azure portal](./media/virtual-machines-windows-sql-server-agent-extension/azure-rm-sql-server-iaas-agent-uninstall.png)

<span data-ttu-id="8a2c6-159">You can also use the **Remove-AzureRmVMSqlServerExtension** PowerShell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8a2c6-159">You can also use the **Remove-AzureRmVMSqlServerExtension** PowerShell cmdlet.</span></span>

    Remove-AzureRmVMSqlServerExtension -ResourceGroupName "resourcegroupname" -VMName "vmname" -Name "SQLIaasExtension"

## <a name="next-steps"></a><span data-ttu-id="8a2c6-160">Next steps</span><span class="sxs-lookup"><span data-stu-id="8a2c6-160">Next steps</span></span>
<span data-ttu-id="8a2c6-161">Begin using one of the services supported by the extension.</span><span class="sxs-lookup"><span data-stu-id="8a2c6-161">Begin using one of the services supported by the extension.</span></span> <span data-ttu-id="8a2c6-162">For more details, see the articles referenced in the [Supported services](#supported-services) section of this article.</span><span class="sxs-lookup"><span data-stu-id="8a2c6-162">For more details, see the articles referenced in the [Supported services](#supported-services) section of this article.</span></span>

<span data-ttu-id="8a2c6-163">For more information about running SQL Server on Azure Virtual Machines, see [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8a2c6-163">For more information about running SQL Server on Azure Virtual Machines, see [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

