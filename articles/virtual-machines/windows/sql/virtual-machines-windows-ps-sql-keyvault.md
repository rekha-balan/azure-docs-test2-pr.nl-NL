---
title: Integrate Key Vault with SQL Server on Windows VMs in Azure (Resource Manager) | Microsoft Docs
description: Learn how to automate the configuration of SQL Server encryption for use with Azure Key Vault. This topic explains how to use Azure Key Vault Integration with SQL Server virtual machines created with Resource Manager.
services: virtual-machines-windows
documentationcenter: ''
author: rothja
manager: jhubbard
editor: ''
tags: azure-service-management
ms.assetid: cd66dfb1-0e9b-4fb0-a471-9deaf4ab4ab8
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 03/14/2017
ms.author: jroth
ms.openlocfilehash: 0e5b5a41fa55d11c12d738455a4e327c1d42bff7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551573"
---
# <a name="configure-azure-key-vault-integration-for-sql-server-on-azure-virtual-machines-resource-manager"></a><span data-ttu-id="e34f3-104">Configure Azure Key Vault Integration for SQL Server on Azure Virtual Machines (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="e34f3-104">Configure Azure Key Vault Integration for SQL Server on Azure Virtual Machines (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [Resource Manager](virtual-machines-windows-ps-sql-keyvault.md)
> * [Classic](../classic/ps-sql-keyvault.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="e34f3-107">Overview</span><span class="sxs-lookup"><span data-stu-id="e34f3-107">Overview</span></span>
<span data-ttu-id="e34f3-108">There are multiple SQL Server encryption features, such as [transparent data encryption (TDE)](https://msdn.microsoft.com/library/bb934049.aspx), [column level encryption (CLE)](https://msdn.microsoft.com/library/ms173744.aspx), and [backup encryption](https://msdn.microsoft.com/library/dn449489.aspx).</span><span class="sxs-lookup"><span data-stu-id="e34f3-108">There are multiple SQL Server encryption features, such as [transparent data encryption (TDE)](https://msdn.microsoft.com/library/bb934049.aspx), [column level encryption (CLE)](https://msdn.microsoft.com/library/ms173744.aspx), and [backup encryption](https://msdn.microsoft.com/library/dn449489.aspx).</span></span> <span data-ttu-id="e34f3-109">These forms of encryption require you to manage and store the cryptographic keys you use for encryption.</span><span class="sxs-lookup"><span data-stu-id="e34f3-109">These forms of encryption require you to manage and store the cryptographic keys you use for encryption.</span></span> <span data-ttu-id="e34f3-110">The Azure Key Vault (AKV) service is designed to improve the security and management of these keys in a secure and highly available location.</span><span class="sxs-lookup"><span data-stu-id="e34f3-110">The Azure Key Vault (AKV) service is designed to improve the security and management of these keys in a secure and highly available location.</span></span> <span data-ttu-id="e34f3-111">The [SQL Server Connector](http://www.microsoft.com/download/details.aspx?id=45344) enables SQL Server to use these keys from Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="e34f3-111">The [SQL Server Connector](http://www.microsoft.com/download/details.aspx?id=45344) enables SQL Server to use these keys from Azure Key Vault.</span></span>

<span data-ttu-id="e34f3-112">If you running SQL Server with on-premises machines, there are [steps you can follow to access Azure Key Vault from your on-premises SQL Server machine](https://msdn.microsoft.com/library/dn198405.aspx).</span><span class="sxs-lookup"><span data-stu-id="e34f3-112">If you running SQL Server with on-premises machines, there are [steps you can follow to access Azure Key Vault from your on-premises SQL Server machine](https://msdn.microsoft.com/library/dn198405.aspx).</span></span> <span data-ttu-id="e34f3-113">But for SQL Server in Azure VMs, you can save time by using the *Azure Key Vault Integration* feature.</span><span class="sxs-lookup"><span data-stu-id="e34f3-113">But for SQL Server in Azure VMs, you can save time by using the *Azure Key Vault Integration* feature.</span></span>

<span data-ttu-id="e34f3-114">When this feature is enabled, it automatically installs the SQL Server Connector, configures the EKM provider to access Azure Key Vault, and creates the credential to allow you to access your vault.</span><span class="sxs-lookup"><span data-stu-id="e34f3-114">When this feature is enabled, it automatically installs the SQL Server Connector, configures the EKM provider to access Azure Key Vault, and creates the credential to allow you to access your vault.</span></span> <span data-ttu-id="e34f3-115">If you looked at the steps in the previously mentioned on-premises documentation, you can see that this feature automates steps 2 and 3.</span><span class="sxs-lookup"><span data-stu-id="e34f3-115">If you looked at the steps in the previously mentioned on-premises documentation, you can see that this feature automates steps 2 and 3.</span></span> <span data-ttu-id="e34f3-116">The only thing you would still need to do manually is to create the key vault and keys.</span><span class="sxs-lookup"><span data-stu-id="e34f3-116">The only thing you would still need to do manually is to create the key vault and keys.</span></span> <span data-ttu-id="e34f3-117">From there, the entire setup of your SQL VM is automated.</span><span class="sxs-lookup"><span data-stu-id="e34f3-117">From there, the entire setup of your SQL VM is automated.</span></span> <span data-ttu-id="e34f3-118">Once this feature has completed this setup, you can execute T-SQL statements to begin encrypting your databases or backups as you normally would.</span><span class="sxs-lookup"><span data-stu-id="e34f3-118">Once this feature has completed this setup, you can execute T-SQL statements to begin encrypting your databases or backups as you normally would.</span></span>

[!INCLUDE [AKV Integration Prepare](../../../../includes/virtual-machines-sql-server-akv-prepare.md)]

## <a name="enabling-and-configuring-akv-integration"></a><span data-ttu-id="e34f3-119">Enabling and configuring AKV integration</span><span class="sxs-lookup"><span data-stu-id="e34f3-119">Enabling and configuring AKV integration</span></span>
<span data-ttu-id="e34f3-120">You can enable AKV integration during provisioning or configure it for existing VMs.</span><span class="sxs-lookup"><span data-stu-id="e34f3-120">You can enable AKV integration during provisioning or configure it for existing VMs.</span></span>

### <a name="new-vms"></a><span data-ttu-id="e34f3-121">New VMs</span><span class="sxs-lookup"><span data-stu-id="e34f3-121">New VMs</span></span>
<span data-ttu-id="e34f3-122">If you are provisioning a new SQL Server virtual machine with Resource Manager, the Azure portal provides a step to enable Azure Key Vault integration.</span><span class="sxs-lookup"><span data-stu-id="e34f3-122">If you are provisioning a new SQL Server virtual machine with Resource Manager, the Azure portal provides a step to enable Azure Key Vault integration.</span></span> <span data-ttu-id="e34f3-123">The Azure Key Vault feature is available only for the Enterprise, Developer and Evaluation Editions of SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e34f3-123">The Azure Key Vault feature is available only for the Enterprise, Developer and Evaluation Editions of SQL Server.</span></span>

![SQL Azure Key Vault Integration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-ps-sql-keyvault/azure-sql-arm-akv.png)

<span data-ttu-id="e34f3-125">For a detailed walkthrough of provisioning, see [Provision a SQL Server virtual machine in the Azure Portal](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="e34f3-125">For a detailed walkthrough of provisioning, see [Provision a SQL Server virtual machine in the Azure Portal](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

### <a name="existing-vms"></a><span data-ttu-id="e34f3-126">Existing VMs</span><span class="sxs-lookup"><span data-stu-id="e34f3-126">Existing VMs</span></span>
<span data-ttu-id="e34f3-127">For existing SQL Server virtual machines, select your SQL Server virtual machine.</span><span class="sxs-lookup"><span data-stu-id="e34f3-127">For existing SQL Server virtual machines, select your SQL Server virtual machine.</span></span> <span data-ttu-id="e34f3-128">Then select the **SQL Server configuration** section of the **Settings** blade.</span><span class="sxs-lookup"><span data-stu-id="e34f3-128">Then select the **SQL Server configuration** section of the **Settings** blade.</span></span>

![SQL AKV Integration for existing VMs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-ps-sql-keyvault/azure-sql-rm-akv-existing-vms.png)

<span data-ttu-id="e34f3-130">In the **SQL Server configuration** blade, click the **Edit** button in the Automated Key Vault integration section.</span><span class="sxs-lookup"><span data-stu-id="e34f3-130">In the **SQL Server configuration** blade, click the **Edit** button in the Automated Key Vault integration section.</span></span>

![Configure SQL AKV Integration for existing VMs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-ps-sql-keyvault/azure-sql-rm-akv-configuration.png)

<span data-ttu-id="e34f3-132">When finished, click the **OK** button on the bottom of the **SQL Server configuration** blade to save your changes.</span><span class="sxs-lookup"><span data-stu-id="e34f3-132">When finished, click the **OK** button on the bottom of the **SQL Server configuration** blade to save your changes.</span></span>

> [!NOTE]
> You can also configure AKV integration using a template. For more information, see [Azure quickstart template for Azure Key Vault integration](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-keyvault-update).
> 
> 

[!INCLUDE [AKV Integration Next Steps](../../../../includes/virtual-machines-sql-server-akv-next-steps.md)]




