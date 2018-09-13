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
ms.author: markgal, sogup;
ms.openlocfilehash: 31e8bdcf3d607fabbe96f4b9aaec1002c1925deb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44775534"
---
# <a name="azure-government-backup"></a><span data-ttu-id="c61ec-103">Azure Government Backup</span><span class="sxs-lookup"><span data-stu-id="c61ec-103">Azure Government Backup</span></span>

<span data-ttu-id="c61ec-104">This article provides an overview of the Azure Backup service and lists the Backup features available in Azure Government.</span><span class="sxs-lookup"><span data-stu-id="c61ec-104">This article provides an overview of the Azure Backup service and lists the Backup features available in Azure Government.</span></span> <span data-ttu-id="c61ec-105">Azure Backup is the Azure-based service you can use to back up (or protect) your data to the Microsoft cloud.</span><span class="sxs-lookup"><span data-stu-id="c61ec-105">Azure Backup is the Azure-based service you can use to back up (or protect) your data to the Microsoft cloud.</span></span> <span data-ttu-id="c61ec-106">Protecting your data in Azure not only means backing it up to the cloud, but restoring the data either to the cloud, or to an on-premises installation.</span><span class="sxs-lookup"><span data-stu-id="c61ec-106">Protecting your data in Azure not only means backing it up to the cloud, but restoring the data either to the cloud, or to an on-premises installation.</span></span> <span data-ttu-id="c61ec-107">Azure Backup provides these key benefits:</span><span class="sxs-lookup"><span data-stu-id="c61ec-107">Azure Backup provides these key benefits:</span></span>

- <span data-ttu-id="c61ec-108">Automatic storage management</span><span class="sxs-lookup"><span data-stu-id="c61ec-108">Automatic storage management</span></span>
- <span data-ttu-id="c61ec-109">Unlimited scaling</span><span class="sxs-lookup"><span data-stu-id="c61ec-109">Unlimited scaling</span></span>
- <span data-ttu-id="c61ec-110">Multiple storage options</span><span class="sxs-lookup"><span data-stu-id="c61ec-110">Multiple storage options</span></span>
- <span data-ttu-id="c61ec-111">Unlimited data transfer</span><span class="sxs-lookup"><span data-stu-id="c61ec-111">Unlimited data transfer</span></span>
- <span data-ttu-id="c61ec-112">Data encryption</span><span class="sxs-lookup"><span data-stu-id="c61ec-112">Data encryption</span></span>
- <span data-ttu-id="c61ec-113">Application-consistent backup</span><span class="sxs-lookup"><span data-stu-id="c61ec-113">Application-consistent backup</span></span>
- <span data-ttu-id="c61ec-114">Long-term retention</span><span class="sxs-lookup"><span data-stu-id="c61ec-114">Long-term retention</span></span>

<span data-ttu-id="c61ec-115">If you're new to Azure Backup and would like an overview of the available features, read the article, [What is Azure Backup](../backup/backup-introduction-to-azure-backup.md).</span><span class="sxs-lookup"><span data-stu-id="c61ec-115">If you're new to Azure Backup and would like an overview of the available features, read the article, [What is Azure Backup](../backup/backup-introduction-to-azure-backup.md).</span></span>

[!INCLUDE [learn-about-backup-deployment models](../../includes/backup-deployment-models.md)]

## <a name="azure-backup-components-available-in-azure-government-backup"></a><span data-ttu-id="c61ec-116">Azure Backup components available in Azure Government Backup</span><span class="sxs-lookup"><span data-stu-id="c61ec-116">Azure Backup components available in Azure Government Backup</span></span>

<span data-ttu-id="c61ec-117">You can use Azure Backup to protect: files, folders, volumes, virtual machines, applications, and workloads.</span><span class="sxs-lookup"><span data-stu-id="c61ec-117">You can use Azure Backup to protect: files, folders, volumes, virtual machines, applications, and workloads.</span></span> <span data-ttu-id="c61ec-118">Depending on what you want to protect, and where that data exists, you use a different Azure Backup component.</span><span class="sxs-lookup"><span data-stu-id="c61ec-118">Depending on what you want to protect, and where that data exists, you use a different Azure Backup component.</span></span> <span data-ttu-id="c61ec-119">The following sections have links to articles in the Azure Backup public documentation for each component.</span><span class="sxs-lookup"><span data-stu-id="c61ec-119">The following sections have links to articles in the Azure Backup public documentation for each component.</span></span> 

### <a name="using-windows-server-and-windows-computers-in-azure-portal"></a><span data-ttu-id="c61ec-120">Using Windows Server and Windows computers in Azure portal</span><span class="sxs-lookup"><span data-stu-id="c61ec-120">Using Windows Server and Windows computers in Azure portal</span></span>

- [<span data-ttu-id="c61ec-121">Back up Windows Server and Windows client computers</span><span class="sxs-lookup"><span data-stu-id="c61ec-121">Back up Windows Server and Windows client computers</span></span>](../backup/backup-configure-vault.md)
- [<span data-ttu-id="c61ec-122">Restore Windows Server and Windows client computers</span><span class="sxs-lookup"><span data-stu-id="c61ec-122">Restore Windows Server and Windows client computers</span></span>](../backup/backup-azure-restore-windows-server.md)
- [<span data-ttu-id="c61ec-123">Manage Windows Server and Windows client computer backups</span><span class="sxs-lookup"><span data-stu-id="c61ec-123">Manage Windows Server and Windows client computer backups</span></span>](../backup/backup-azure-manage-windows-server.md)
- [<span data-ttu-id="c61ec-124">Using PowerShell to back up Windows Server</span><span class="sxs-lookup"><span data-stu-id="c61ec-124">Using PowerShell to back up Windows Server</span></span>](../backup/backup-client-automation.md)

### <a name="using-virtual-machines-in-azure-portal"></a><span data-ttu-id="c61ec-125">Using Virtual Machines in Azure portal</span><span class="sxs-lookup"><span data-stu-id="c61ec-125">Using Virtual Machines in Azure portal</span></span>

- [<span data-ttu-id="c61ec-126">Prepare your virtual machine environment</span><span class="sxs-lookup"><span data-stu-id="c61ec-126">Prepare your virtual machine environment</span></span>](../backup/backup-azure-arm-vms-prepare.md)
- [<span data-ttu-id="c61ec-127">Back up virtual machines</span><span class="sxs-lookup"><span data-stu-id="c61ec-127">Back up virtual machines</span></span>](../backup/backup-azure-vms-first-look-arm.md)
- [<span data-ttu-id="c61ec-128">Restore virtual machines</span><span class="sxs-lookup"><span data-stu-id="c61ec-128">Restore virtual machines</span></span>](../backup/backup-azure-arm-restore-vms.md)
- [<span data-ttu-id="c61ec-129">Manage virtual machines</span><span class="sxs-lookup"><span data-stu-id="c61ec-129">Manage virtual machines</span></span>](../backup/backup-azure-manage-vms.md)
- [<span data-ttu-id="c61ec-130">Using PowerShell to back up virtual machines</span><span class="sxs-lookup"><span data-stu-id="c61ec-130">Using PowerShell to back up virtual machines</span></span>](../backup/backup-azure-vms-automation.md)

### <a name="using-system-center-data-protection-manager-in-azure-portal"></a><span data-ttu-id="c61ec-131">Using System Center Data Protection Manager in Azure portal</span><span class="sxs-lookup"><span data-stu-id="c61ec-131">Using System Center Data Protection Manager in Azure portal</span></span>

- [<span data-ttu-id="c61ec-132">Back up System Center Data Protection Manager</span><span class="sxs-lookup"><span data-stu-id="c61ec-132">Back up System Center Data Protection Manager</span></span>](../backup/backup-azure-dpm-introduction.md)

### <a name="using-azure-backup-server-in-azure-portal"></a><span data-ttu-id="c61ec-133">Using Azure Backup Server in Azure portal</span><span class="sxs-lookup"><span data-stu-id="c61ec-133">Using Azure Backup Server in Azure portal</span></span>

<span data-ttu-id="c61ec-134">Azure Backup Server is an Azure Backup component that functions similarly to System Center Data Protection Manager (DPM) with one exception - Azure Backup Server cannot save data to tape.</span><span class="sxs-lookup"><span data-stu-id="c61ec-134">Azure Backup Server is an Azure Backup component that functions similarly to System Center Data Protection Manager (DPM) with one exception - Azure Backup Server cannot save data to tape.</span></span> <span data-ttu-id="c61ec-135">Azure Backup Server can protect application workloads such as: Hyper-V VMs, Microsoft SQL Server, SharePoint Server, Microsoft Exchange, and Windows clients to the cloud from a single console.</span><span class="sxs-lookup"><span data-stu-id="c61ec-135">Azure Backup Server can protect application workloads such as: Hyper-V VMs, Microsoft SQL Server, SharePoint Server, Microsoft Exchange, and Windows clients to the cloud from a single console.</span></span> <span data-ttu-id="c61ec-136">Azure Backup Server does not require a System Center license.</span><span class="sxs-lookup"><span data-stu-id="c61ec-136">Azure Backup Server does not require a System Center license.</span></span>

- [<span data-ttu-id="c61ec-137">Azure Backup Server</span><span class="sxs-lookup"><span data-stu-id="c61ec-137">Azure Backup Server</span></span>](../backup/backup-azure-microsoft-azure-backup.md)

### <a name="upgrade-a-backup-vault-to-a-recovery-services-vault"></a><span data-ttu-id="c61ec-138">Upgrade a Backup vault to a Recovery Services vault</span><span class="sxs-lookup"><span data-stu-id="c61ec-138">Upgrade a Backup vault to a Recovery Services vault</span></span>

- [<span data-ttu-id="c61ec-139">Upgrade now</span><span class="sxs-lookup"><span data-stu-id="c61ec-139">Upgrade now</span></span>](../backup/backup-azure-upgrade-backup-to-recovery-services.md)


## <a name="next-steps"></a><span data-ttu-id="c61ec-140">Next steps</span><span class="sxs-lookup"><span data-stu-id="c61ec-140">Next steps</span></span>

<span data-ttu-id="c61ec-141">If you aren't sure where to begin, start with the article, [Back up Windows Server and Windows client computers](../backup/backup-configure-vault.md).</span><span class="sxs-lookup"><span data-stu-id="c61ec-141">If you aren't sure where to begin, start with the article, [Back up Windows Server and Windows client computers](../backup/backup-configure-vault.md).</span></span> <span data-ttu-id="c61ec-142">This tutorial leads you through the steps for setting up a backup project on a Windows Server or computer.</span><span class="sxs-lookup"><span data-stu-id="c61ec-142">This tutorial leads you through the steps for setting up a backup project on a Windows Server or computer.</span></span>

<span data-ttu-id="c61ec-143">If you already know that you could use Azure Backup, but want to know the costs, see the [Backup Pricing page](http://azure.microsoft.com/pricing/details/backup/).</span><span class="sxs-lookup"><span data-stu-id="c61ec-143">If you already know that you could use Azure Backup, but want to know the costs, see the [Backup Pricing page](http://azure.microsoft.com/pricing/details/backup/).</span></span> <span data-ttu-id="c61ec-144">There is a list of Frequently Asked Questions that may provide useful information.</span><span class="sxs-lookup"><span data-stu-id="c61ec-144">There is a list of Frequently Asked Questions that may provide useful information.</span></span> <span data-ttu-id="c61ec-145">Also note there are multiple Azure Government regions in the **Region** dropdown menu.</span><span class="sxs-lookup"><span data-stu-id="c61ec-145">Also note there are multiple Azure Government regions in the **Region** dropdown menu.</span></span>
