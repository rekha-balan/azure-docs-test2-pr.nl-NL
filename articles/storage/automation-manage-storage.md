---
title: Manage Azure Storage using Azure Automation
description: Learn about how the Azure Automation service can be used to manage Azure Storage at scale.
services: storage, automation
documentationcenter: ''
author: jodoglevy
manager: eamono
editor: ''
ms.assetid: bac41c39-1d95-46aa-a481-ec17bbb21b40
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2016
ms.author: eamono
ms.openlocfilehash: fbf1cd9e73615f8d991f348cb705aa9df8b55b4e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549103"
---
# <a name="managing-azure-storage-using-azure-automation"></a><span data-ttu-id="4d073-103">Managing Azure Storage using Azure Automation</span><span class="sxs-lookup"><span data-stu-id="4d073-103">Managing Azure Storage using Azure Automation</span></span>
<span data-ttu-id="4d073-104">This guide will introduce you to the Azure Automation service, and how it can be used to simplify management of your Azure Storage blobs, tables, and queues.</span><span class="sxs-lookup"><span data-stu-id="4d073-104">This guide will introduce you to the Azure Automation service, and how it can be used to simplify management of your Azure Storage blobs, tables, and queues.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="4d073-105">What is Azure Automation?</span><span class="sxs-lookup"><span data-stu-id="4d073-105">What is Azure Automation?</span></span>
<span data-ttu-id="4d073-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span><span class="sxs-lookup"><span data-stu-id="4d073-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="4d073-107">Using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated to increase reliability and efficiency, and reduce time to value for your organization.</span><span class="sxs-lookup"><span data-stu-id="4d073-107">Using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated to increase reliability and efficiency, and reduce time to value for your organization.</span></span>

<span data-ttu-id="4d073-108">Azure Automation provides a highly-reliable and highly-available workflow execution engine that scales to meet your needs as your organization grows.</span><span class="sxs-lookup"><span data-stu-id="4d073-108">Azure Automation provides a highly-reliable and highly-available workflow execution engine that scales to meet your needs as your organization grows.</span></span> <span data-ttu-id="4d073-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span><span class="sxs-lookup"><span data-stu-id="4d073-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="4d073-110">Lower operational overhead and free up IT / DevOps staff to focus on work that adds business value by moving your cloud management tasks to be run automatically by Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="4d073-110">Lower operational overhead and free up IT / DevOps staff to focus on work that adds business value by moving your cloud management tasks to be run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-storage"></a><span data-ttu-id="4d073-111">How can Azure Automation help manage Azure Storage?</span><span class="sxs-lookup"><span data-stu-id="4d073-111">How can Azure Automation help manage Azure Storage?</span></span>
<span data-ttu-id="4d073-112">Azure Storage can be managed in Azure Automation by using the PowerShell cmdlets that are available in [Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span><span class="sxs-lookup"><span data-stu-id="4d073-112">Azure Storage can be managed in Azure Automation by using the PowerShell cmdlets that are available in [Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span></span> <span data-ttu-id="4d073-113">Azure Automation has these Storage PowerShell cmdlets available out of the box, so that you can perform all of your blob, table, and queue management tasks within the service.</span><span class="sxs-lookup"><span data-stu-id="4d073-113">Azure Automation has these Storage PowerShell cmdlets available out of the box, so that you can perform all of your blob, table, and queue management tasks within the service.</span></span> <span data-ttu-id="4d073-114">You can also pair these cmdlets in Azure Automation with the cmdlets for other Azure services, to automate complex tasks across Azure services and 3rd party systems.</span><span class="sxs-lookup"><span data-stu-id="4d073-114">You can also pair these cmdlets in Azure Automation with the cmdlets for other Azure services, to automate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="4d073-115">The [Azure Automation runbook gallery](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) contains a variety of product team and community runbooks to get started automating management of Azure Storage, other Azure services, and 3rd party systems.</span><span class="sxs-lookup"><span data-stu-id="4d073-115">The [Azure Automation runbook gallery](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) contains a variety of product team and community runbooks to get started automating management of Azure Storage, other Azure services, and 3rd party systems.</span></span> <span data-ttu-id="4d073-116">Gallery runbooks include:</span><span class="sxs-lookup"><span data-stu-id="4d073-116">Gallery runbooks include:</span></span>

* [<span data-ttu-id="4d073-117">Remove Azure Storage Blobs that are Certain Days Old Using Automation Service</span><span class="sxs-lookup"><span data-stu-id="4d073-117">Remove Azure Storage Blobs that are Certain Days Old Using Automation Service</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Remove-Storage-Blobs-that-aae4b761)
* [<span data-ttu-id="4d073-118">Download a Blob from Azure Storage</span><span class="sxs-lookup"><span data-stu-id="4d073-118">Download a Blob from Azure Storage</span></span>](https://gallery.technet.microsoft.com/scriptcenter/a-Blob-from-Azure-Storage-6bc13745)
* [<span data-ttu-id="4d073-119">Backup all disks for a single Azure VM or for all VMs in a Cloud Service</span><span class="sxs-lookup"><span data-stu-id="4d073-119">Backup all disks for a single Azure VM or for all VMs in a Cloud Service</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Backup-all-disks-for-a-ede940d5)

## <a name="next-steps"></a><span data-ttu-id="4d073-120">Next Steps</span><span class="sxs-lookup"><span data-stu-id="4d073-120">Next Steps</span></span>
<span data-ttu-id="4d073-121">Now that you've learned the basics of Azure Automation and how it can be used to manage Azure Storage blobs, tables, and queues, follow these links to learn more about Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="4d073-121">Now that you've learned the basics of Azure Automation and how it can be used to manage Azure Storage blobs, tables, and queues, follow these links to learn more about Azure Automation.</span></span>

<span data-ttu-id="4d073-122">See the Azure Automation tutorial [Creating or importing a runbook in Azure Automation](../automation/automation-creating-importing-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="4d073-122">See the Azure Automation tutorial [Creating or importing a runbook in Azure Automation](../automation/automation-creating-importing-runbook.md).</span></span>

