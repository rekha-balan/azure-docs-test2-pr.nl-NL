---
title: Azure Government Backup | Microsoft Docs
description: This article provides an overview of the Azure Backup features available in Azure Government.
services: azure-government
documentationcenter: ''
author: markgalioto
manager: carmonm
ms.assetid: a7622135-8790-4be4-a02a-7b9ac8a4996f
ms.service: azure-government
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: azure-government
ms.date: 1/5/2017
ms.author: markgal;
ms.openlocfilehash: ff0ed96889256cdde42c3648fef5abda964feadf
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556177"
---
# <a name="azure-government-backup"></a><span data-ttu-id="54f02-103">Azure Government Backup</span><span class="sxs-lookup"><span data-stu-id="54f02-103">Azure Government Backup</span></span>

<span data-ttu-id="54f02-104">This article provides an overview of the Azure Backup service and lists the Backup features available in Azure Government.</span><span class="sxs-lookup"><span data-stu-id="54f02-104">This article provides an overview of the Azure Backup service and lists the Backup features available in Azure Government.</span></span> <span data-ttu-id="54f02-105">Azure Backup is the Azure-based service you can use to back up (or protect) your data to the Microsoft cloud.</span><span class="sxs-lookup"><span data-stu-id="54f02-105">Azure Backup is the Azure-based service you can use to back up (or protect) your data to the Microsoft cloud.</span></span> <span data-ttu-id="54f02-106">Protecting your data in Azure not only means backing it up to the cloud, but restoring the data either to the cloud, or to an on-premises installation.</span><span class="sxs-lookup"><span data-stu-id="54f02-106">Protecting your data in Azure not only means backing it up to the cloud, but restoring the data either to the cloud, or to an on-premises installation.</span></span> <span data-ttu-id="54f02-107">Azure Backup provides these key benefits:</span><span class="sxs-lookup"><span data-stu-id="54f02-107">Azure Backup provides these key benefits:</span></span>

- <span data-ttu-id="54f02-108">Automatic storage management</span><span class="sxs-lookup"><span data-stu-id="54f02-108">Automatic storage management</span></span>
- <span data-ttu-id="54f02-109">Unlimited scaling</span><span class="sxs-lookup"><span data-stu-id="54f02-109">Unlimited scaling</span></span>
- <span data-ttu-id="54f02-110">Multiple storage options</span><span class="sxs-lookup"><span data-stu-id="54f02-110">Multiple storage options</span></span>
- <span data-ttu-id="54f02-111">Unlimited data transfer</span><span class="sxs-lookup"><span data-stu-id="54f02-111">Unlimited data transfer</span></span>
- <span data-ttu-id="54f02-112">Data encryption</span><span class="sxs-lookup"><span data-stu-id="54f02-112">Data encryption</span></span>
- <span data-ttu-id="54f02-113">Application-consistent backup</span><span class="sxs-lookup"><span data-stu-id="54f02-113">Application-consistent backup</span></span>
- <span data-ttu-id="54f02-114">Long-term retention</span><span class="sxs-lookup"><span data-stu-id="54f02-114">Long-term retention</span></span>

<span data-ttu-id="54f02-115">If you're new to Azure Backup and would like an overview of the available features, read the article, [What is Azure Backup](../backup/backup-introduction-to-azure-backup.md).</span><span class="sxs-lookup"><span data-stu-id="54f02-115">If you're new to Azure Backup and would like an overview of the available features, read the article, [What is Azure Backup](../backup/backup-introduction-to-azure-backup.md).</span></span>

[!INCLUDE [learn-about-backup-deployment models](../../includes/backup-deployment-models.md)]

## <a name="azure-backup-components-available-in-azure-government-backup"></a><span data-ttu-id="54f02-116">Azure Backup components available in Azure Government Backup</span><span class="sxs-lookup"><span data-stu-id="54f02-116">Azure Backup components available in Azure Government Backup</span></span>

<span data-ttu-id="54f02-117">You can use Azure Backup to protect: files, folders, volumes, virtual machines, applications, and workloads.</span><span class="sxs-lookup"><span data-stu-id="54f02-117">You can use Azure Backup to protect: files, folders, volumes, virtual machines, applications, and workloads.</span></span> <span data-ttu-id="54f02-118">Depending on what you want to protect, and where that data exists, you use a different Azure Backup component.</span><span class="sxs-lookup"><span data-stu-id="54f02-118">Depending on what you want to protect, and where that data exists, you use a different Azure Backup component.</span></span> <span data-ttu-id="54f02-119">The following sections have links to articles in the Azure Backup public documentation for each component.</span><span class="sxs-lookup"><span data-stu-id="54f02-119">The following sections have links to articles in the Azure Backup public documentation for each component.</span></span> <span data-ttu-id="54f02-120">The sections are broken out by classic portal or Azure portal.</span><span class="sxs-lookup"><span data-stu-id="54f02-120">The sections are broken out by classic portal or Azure portal.</span></span> <span data-ttu-id="54f02-121">Use the Azure portal version if you are planning to use Resource Manager deployments.</span><span class="sxs-lookup"><span data-stu-id="54f02-121">Use the Azure portal version if you are planning to use Resource Manager deployments.</span></span>

### <a name="using-windows-server-and-windows-computers-in-azure-portal"></a><span data-ttu-id="54f02-122">Using Windows Server and Windows computers in Azure portal</span><span class="sxs-lookup"><span data-stu-id="54f02-122">Using Windows Server and Windows computers in Azure portal</span></span>

- [<span data-ttu-id="54f02-123">Back up Windows Server and Windows client computers</span><span class="sxs-lookup"><span data-stu-id="54f02-123">Back up Windows Server and Windows client computers</span></span>](../backup/backup-configure-vault.md)
- [<span data-ttu-id="54f02-124">Restore Windows Server and Windows client computers</span><span class="sxs-lookup"><span data-stu-id="54f02-124">Restore Windows Server and Windows client computers</span></span>](../backup/backup-azure-restore-windows-server.md)
- [<span data-ttu-id="54f02-125">Manage Windows Server and Windows client computer backups</span><span class="sxs-lookup"><span data-stu-id="54f02-125">Manage Windows Server and Windows client computer backups</span></span>](../backup/backup-azure-manage-windows-server.md)
- [<span data-ttu-id="54f02-126">Using PowerShell to back up Windows Server</span><span class="sxs-lookup"><span data-stu-id="54f02-126">Using PowerShell to back up Windows Server</span></span>](../backup/backup-client-automation.md)

### <a name="using-windows-server-and-windows-computers-in-classic-portal"></a><span data-ttu-id="54f02-127">Using Windows Server and Windows computers in classic portal</span><span class="sxs-lookup"><span data-stu-id="54f02-127">Using Windows Server and Windows computers in classic portal</span></span>

- [<span data-ttu-id="54f02-128">Back up Windows Server and Windows client computers</span><span class="sxs-lookup"><span data-stu-id="54f02-128">Back up Windows Server and Windows client computers</span></span>](../backup/backup-configure-vault-classic.md)
- [<span data-ttu-id="54f02-129">Restore Windows Server and Windows client computers</span><span class="sxs-lookup"><span data-stu-id="54f02-129">Restore Windows Server and Windows client computers</span></span>](../backup/backup-azure-restore-windows-server-classic.md)
- [<span data-ttu-id="54f02-130">Manage Windows Server and Windows client computer backups</span><span class="sxs-lookup"><span data-stu-id="54f02-130">Manage Windows Server and Windows client computer backups</span></span>](../backup/backup-azure-manage-windows-server-classic.md)
- [<span data-ttu-id="54f02-131">Using PowerShell to back up Windows Server</span><span class="sxs-lookup"><span data-stu-id="54f02-131">Using PowerShell to back up Windows Server</span></span>](../backup/backup-client-automation-classic.md)

### <a name="using-virtual-machines-in-azure-portal"></a><span data-ttu-id="54f02-132">Using Virtual Machines in Azure portal</span><span class="sxs-lookup"><span data-stu-id="54f02-132">Using Virtual Machines in Azure portal</span></span>

- [<span data-ttu-id="54f02-133">Prepare your virtual machine environment</span><span class="sxs-lookup"><span data-stu-id="54f02-133">Prepare your virtual machine environment</span></span>](../backup/backup-azure-arm-vms-prepare.md)
- [<span data-ttu-id="54f02-134">Back up virtual machines</span><span class="sxs-lookup"><span data-stu-id="54f02-134">Back up virtual machines</span></span>](../backup/backup-azure-vms-first-look-arm.md)
- [<span data-ttu-id="54f02-135">Restore virtual machines</span><span class="sxs-lookup"><span data-stu-id="54f02-135">Restore virtual machines</span></span>](../backup/backup-azure-arm-restore-vms.md)
- [<span data-ttu-id="54f02-136">Manage virtual machines</span><span class="sxs-lookup"><span data-stu-id="54f02-136">Manage virtual machines</span></span>](../backup/backup-azure-manage-vms.md)
- [<span data-ttu-id="54f02-137">Using PowerShell to back up virtual machines</span><span class="sxs-lookup"><span data-stu-id="54f02-137">Using PowerShell to back up virtual machines</span></span>](../backup/backup-azure-vms-automation.md)

### <a name="using-virtual-machines-in-classic-portal"></a><span data-ttu-id="54f02-138">Using Virtual Machines in classic portal</span><span class="sxs-lookup"><span data-stu-id="54f02-138">Using Virtual Machines in classic portal</span></span>

- [<span data-ttu-id="54f02-139">Prepare your virtual machine environment</span><span class="sxs-lookup"><span data-stu-id="54f02-139">Prepare your virtual machine environment</span></span>](../backup/backup-azure-vms-prepare.md)
- [<span data-ttu-id="54f02-140">Back up virtual machines</span><span class="sxs-lookup"><span data-stu-id="54f02-140">Back up virtual machines</span></span>](../backup/backup-azure-vms-first-look.md)
- [<span data-ttu-id="54f02-141">Restore virtual machines</span><span class="sxs-lookup"><span data-stu-id="54f02-141">Restore virtual machines</span></span>](../backup/backup-azure-restore-vms.md)
- [<span data-ttu-id="54f02-142">Manage virtual machines</span><span class="sxs-lookup"><span data-stu-id="54f02-142">Manage virtual machines</span></span>](../backup/backup-azure-manage-vms-classic.md)
- [<span data-ttu-id="54f02-143">Using PowerShell to back up virtual machines</span><span class="sxs-lookup"><span data-stu-id="54f02-143">Using PowerShell to back up virtual machines</span></span>](../backup/backup-azure-vms-classic-automation.md)

### <a name="using-system-center-data-protection-manager-in-azure-portal"></a><span data-ttu-id="54f02-144">Using System Center Data Protection Manager in Azure portal</span><span class="sxs-lookup"><span data-stu-id="54f02-144">Using System Center Data Protection Manager in Azure portal</span></span>

- [<span data-ttu-id="54f02-145">Back up System Center Data Protection Manager</span><span class="sxs-lookup"><span data-stu-id="54f02-145">Back up System Center Data Protection Manager</span></span>](../backup/backup-azure-dpm-introduction.md)

### <a name="using-system-center-data-protection-manager-in-classic-portal"></a><span data-ttu-id="54f02-146">Using System Center Data Protection Manager in classic portal</span><span class="sxs-lookup"><span data-stu-id="54f02-146">Using System Center Data Protection Manager in classic portal</span></span>

- [<span data-ttu-id="54f02-147">Back up System Center Data Protection Manager</span><span class="sxs-lookup"><span data-stu-id="54f02-147">Back up System Center Data Protection Manager</span></span>](../backup/backup-azure-dpm-introduction-classic.md)

### <a name="using-azure-backup-server-in-azure-portal"></a><span data-ttu-id="54f02-148">Using Azure Backup Server in Azure portal</span><span class="sxs-lookup"><span data-stu-id="54f02-148">Using Azure Backup Server in Azure portal</span></span>

<span data-ttu-id="54f02-149">Azure Backup Server is an Azure Backup component that functions similarly to System Center Data Protection Manager (DPM) with one exception - Azure Backup Server cannot save data to tape.</span><span class="sxs-lookup"><span data-stu-id="54f02-149">Azure Backup Server is an Azure Backup component that functions similarly to System Center Data Protection Manager (DPM) with one exception - Azure Backup Server cannot save data to tape.</span></span> <span data-ttu-id="54f02-150">Azure Backup Server can protect application workloads such as: Hyper-V VMs, Microsoft SQL Server, SharePoint Server, Microsoft Exchange, and Windows clients to the cloud from a single console.</span><span class="sxs-lookup"><span data-stu-id="54f02-150">Azure Backup Server can protect application workloads such as: Hyper-V VMs, Microsoft SQL Server, SharePoint Server, Microsoft Exchange, and Windows clients to the cloud from a single console.</span></span> <span data-ttu-id="54f02-151">Azure Backup Server does not require a System Center license.</span><span class="sxs-lookup"><span data-stu-id="54f02-151">Azure Backup Server does not require a System Center license.</span></span>

- [<span data-ttu-id="54f02-152">Azure Backup Server</span><span class="sxs-lookup"><span data-stu-id="54f02-152">Azure Backup Server</span></span>](../backup/backup-azure-microsoft-azure-backup.md)

### <a name="using-azure-backup-server-in-classic-portal"></a><span data-ttu-id="54f02-153">Using Azure Backup Server in classic portal</span><span class="sxs-lookup"><span data-stu-id="54f02-153">Using Azure Backup Server in classic portal</span></span>

- [<span data-ttu-id="54f02-154">Azure Backup Server</span><span class="sxs-lookup"><span data-stu-id="54f02-154">Azure Backup Server</span></span>](../backup/backup-azure-microsoft-azure-backup-classic.md)


## <a name="next-steps"></a><span data-ttu-id="54f02-155">Next steps</span><span class="sxs-lookup"><span data-stu-id="54f02-155">Next steps</span></span>

<span data-ttu-id="54f02-156">If you aren't sure where to begin, start with the article, [Back up a Windows server or client to Azure using the classic deployment model](../backup/backup-configure-vault-classic.md).</span><span class="sxs-lookup"><span data-stu-id="54f02-156">If you aren't sure where to begin, start with the article, [Back up a Windows server or client to Azure using the classic deployment model](../backup/backup-configure-vault-classic.md).</span></span> <span data-ttu-id="54f02-157">This tutorial leads you through the steps for setting up a backup project on a Windows Server or computer.</span><span class="sxs-lookup"><span data-stu-id="54f02-157">This tutorial leads you through the steps for setting up a backup project on a Windows Server or computer.</span></span>

<span data-ttu-id="54f02-158">If you already know that you could use Azure Backup, but want to know the costs, see the [Backup Pricing page](http://azure.microsoft.com/pricing/details/backup/).</span><span class="sxs-lookup"><span data-stu-id="54f02-158">If you already know that you could use Azure Backup, but want to know the costs, see the [Backup Pricing page](http://azure.microsoft.com/pricing/details/backup/).</span></span> <span data-ttu-id="54f02-159">There is a list of Frequently Asked Questions that may provide useful information.</span><span class="sxs-lookup"><span data-stu-id="54f02-159">There is a list of Frequently Asked Questions that may provide useful information.</span></span> <span data-ttu-id="54f02-160">Also note there are two Azure Government regions in the **Region** dropdown menu.</span><span class="sxs-lookup"><span data-stu-id="54f02-160">Also note there are two Azure Government regions in the **Region** dropdown menu.</span></span>
