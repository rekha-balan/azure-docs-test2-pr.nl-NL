---
title: Azure Resource Manager templates for Azure Backup
description: Azure Backup PowerShell Samples
services: backup
author: markgalioto
manager: carmonm
ms.service: backup
ms.topic: sample
ms.date: 04/18/2018
ms.author: markgal
ms.custom: mvc
ms.openlocfilehash: 0aac49be397f5e1c86fa834d341399775fd71cfa
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870385"
---
# <a name="azure-resource-manager-templates-for-azure-backup"></a><span data-ttu-id="fe19e-103">Azure Resource Manager templates for Azure Backup</span><span class="sxs-lookup"><span data-stu-id="fe19e-103">Azure Resource Manager templates for Azure Backup</span></span>

<span data-ttu-id="fe19e-104">The following table includes links to Azure Resource Manager templates for use with Recovery Services vaults and Azure Backup features.</span><span class="sxs-lookup"><span data-stu-id="fe19e-104">The following table includes links to Azure Resource Manager templates for use with Recovery Services vaults and Azure Backup features.</span></span>

|   |   |
|---|---|
|<span data-ttu-id="fe19e-105">**Recovery Services vault**</span><span class="sxs-lookup"><span data-stu-id="fe19e-105">**Recovery Services vault**</span></span> | |
| [<span data-ttu-id="fe19e-106">Create a Recovery Services vault</span><span class="sxs-lookup"><span data-stu-id="fe19e-106">Create a Recovery Services vault</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-recovery-services-vault-create)| <span data-ttu-id="fe19e-107">Create a Recovery Services vault.</span><span class="sxs-lookup"><span data-stu-id="fe19e-107">Create a Recovery Services vault.</span></span> <span data-ttu-id="fe19e-108">The vault can be used for Azure Backup and Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="fe19e-108">The vault can be used for Azure Backup and Azure Site Recovery.</span></span> |
|<span data-ttu-id="fe19e-109">**Back up virtual machines**</span><span class="sxs-lookup"><span data-stu-id="fe19e-109">**Back up virtual machines**</span></span>| |
| [<span data-ttu-id="fe19e-110">Back up Resource Manager VMs</span><span class="sxs-lookup"><span data-stu-id="fe19e-110">Back up Resource Manager VMs</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-recovery-services-backup-vms) | <span data-ttu-id="fe19e-111">Use the existing Recovery Services vault and Backup policy to back up Resource Manager-virtual machines in the same resource group.</span><span class="sxs-lookup"><span data-stu-id="fe19e-111">Use the existing Recovery Services vault and Backup policy to back up Resource Manager-virtual machines in the same resource group.</span></span>|
| [<span data-ttu-id="fe19e-112">Back up IaaS VMs to Recovery Services vault</span><span class="sxs-lookup"><span data-stu-id="fe19e-112">Back up IaaS VMs to Recovery Services vault</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-recovery-services-backup-classic-resource-manager-vms) | <span data-ttu-id="fe19e-113">Template to back up classic and Resource Manager-virtual machines.</span><span class="sxs-lookup"><span data-stu-id="fe19e-113">Template to back up classic and Resource Manager-virtual machines.</span></span> |
| [<span data-ttu-id="fe19e-114">Create Weekly Backup policy for IaaS VMs</span><span class="sxs-lookup"><span data-stu-id="fe19e-114">Create Weekly Backup policy for IaaS VMs</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-recovery-services-weekly-backup-policy-create) | <span data-ttu-id="fe19e-115">Template creates Recovery Services vault and a weekly backup policy which is used to back up classic and Resource Manager-virtual machines.</span><span class="sxs-lookup"><span data-stu-id="fe19e-115">Template creates Recovery Services vault and a weekly backup policy which is used to back up classic and Resource Manager-virtual machines.</span></span>|
| [<span data-ttu-id="fe19e-116">Create Daily Backup policy for IaaS VMs</span><span class="sxs-lookup"><span data-stu-id="fe19e-116">Create Daily Backup policy for IaaS VMs</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-recovery-services-daily-backup-policy-create) | <span data-ttu-id="fe19e-117">Template creates Recovery Services vault and a daily backup policy which is used to back up classic and Resource Manager-virtual machines.</span><span class="sxs-lookup"><span data-stu-id="fe19e-117">Template creates Recovery Services vault and a daily backup policy which is used to back up classic and Resource Manager-virtual machines.</span></span>|
| [<span data-ttu-id="fe19e-118">Deploy Windows Server VM with backup enabled</span><span class="sxs-lookup"><span data-stu-id="fe19e-118">Deploy Windows Server VM with backup enabled</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-recovery-services-create-vm-and-configure-backup) | <span data-ttu-id="fe19e-119">Template creates a Windows Server VM and Recovery Services vault with the default backup policy enabled.</span><span class="sxs-lookup"><span data-stu-id="fe19e-119">Template creates a Windows Server VM and Recovery Services vault with the default backup policy enabled.</span></span>|
|<span data-ttu-id="fe19e-120">**Monitor Backup jobs**</span><span class="sxs-lookup"><span data-stu-id="fe19e-120">**Monitor Backup jobs**</span></span> |  |
| [<span data-ttu-id="fe19e-121">Use OMS Log Analytics to monitor Azure Backup</span><span class="sxs-lookup"><span data-stu-id="fe19e-121">Use OMS Log Analytics to monitor Azure Backup</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-backup-oms-monitoring) | <span data-ttu-id="fe19e-122">Template deploys OMS Monitoring for Azure Backup which allows you to monitor backup and restore jobs, backup alerts and the Cloud storage used in your Recovery Services vaults.</span><span class="sxs-lookup"><span data-stu-id="fe19e-122">Template deploys OMS Monitoring for Azure Backup which allows you to monitor backup and restore jobs, backup alerts and the Cloud storage used in your Recovery Services vaults.</span></span>|  
|   |   |

