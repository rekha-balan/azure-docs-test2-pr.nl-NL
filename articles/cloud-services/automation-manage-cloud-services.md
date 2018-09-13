---
title: Manage Azure Cloud Services using Azure Automation | Microsoft Docs
description: Learn about how the Azure Automation service can be used to manage Azure cloud services at scale.
services: cloud-services, automation
documentationcenter: ''
author: jodoglevy
manager: timlt
editor: ''
ms.assetid: 3789810a-2892-4eef-bf29-c781c1b5af48
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2016
ms.author: timlt
ms.openlocfilehash: 6b5acac1b8647c324988c316cd5602b3dba98a1d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552477"
---
# <a name="managing-azure-cloud-services-using-azure-automation"></a><span data-ttu-id="e7bdb-103">Managing Azure Cloud Services using Azure Automation</span><span class="sxs-lookup"><span data-stu-id="e7bdb-103">Managing Azure Cloud Services using Azure Automation</span></span>
<span data-ttu-id="e7bdb-104">This guide will introduce you to the Azure Automation service, and how it can be used to simplify management of your Azure cloud services.</span><span class="sxs-lookup"><span data-stu-id="e7bdb-104">This guide will introduce you to the Azure Automation service, and how it can be used to simplify management of your Azure cloud services.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="e7bdb-105">What is Azure Automation?</span><span class="sxs-lookup"><span data-stu-id="e7bdb-105">What is Azure Automation?</span></span>
<span data-ttu-id="e7bdb-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span><span class="sxs-lookup"><span data-stu-id="e7bdb-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="e7bdb-107">Using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated to increase reliability, efficiency, and time to value for your organization.</span><span class="sxs-lookup"><span data-stu-id="e7bdb-107">Using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated to increase reliability, efficiency, and time to value for your organization.</span></span>

<span data-ttu-id="e7bdb-108">Azure Automation provides a highly-reliable and highly-available workflow execution engine that scales to meet your needs as your organization grows.</span><span class="sxs-lookup"><span data-stu-id="e7bdb-108">Azure Automation provides a highly-reliable and highly-available workflow execution engine that scales to meet your needs as your organization grows.</span></span> <span data-ttu-id="e7bdb-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span><span class="sxs-lookup"><span data-stu-id="e7bdb-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="e7bdb-110">Lower operational overhead and free up IT / DevOps staff to focus on work that adds business value by moving your cloud management tasks to be run automatically by Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="e7bdb-110">Lower operational overhead and free up IT / DevOps staff to focus on work that adds business value by moving your cloud management tasks to be run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-cloud-services"></a><span data-ttu-id="e7bdb-111">How can Azure Automation help manage Azure cloud services?</span><span class="sxs-lookup"><span data-stu-id="e7bdb-111">How can Azure Automation help manage Azure cloud services?</span></span>
<span data-ttu-id="e7bdb-112">Azure cloud services can be managed in Azure Automation by using the PowerShell cmdlets that are available in the [Azure PowerShell tools](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span><span class="sxs-lookup"><span data-stu-id="e7bdb-112">Azure cloud services can be managed in Azure Automation by using the PowerShell cmdlets that are available in the [Azure PowerShell tools](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span></span> <span data-ttu-id="e7bdb-113">Azure Automation has these cloud service PowerShell cmdlets available out of the box, so that you can perform all of your cloud service management tasks within the service.</span><span class="sxs-lookup"><span data-stu-id="e7bdb-113">Azure Automation has these cloud service PowerShell cmdlets available out of the box, so that you can perform all of your cloud service management tasks within the service.</span></span> <span data-ttu-id="e7bdb-114">You can also pair these cmdlets in Azure Automation with the cmdlets for other Azure services, to automate complex tasks across Azure services and 3rd party systems.</span><span class="sxs-lookup"><span data-stu-id="e7bdb-114">You can also pair these cmdlets in Azure Automation with the cmdlets for other Azure services, to automate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="e7bdb-115">Some example uses of Azure Automation to manage Azure Cloud Services include:</span><span class="sxs-lookup"><span data-stu-id="e7bdb-115">Some example uses of Azure Automation to manage Azure Cloud Services include:</span></span>

* [<span data-ttu-id="e7bdb-116">Continous deployment of a Cloud Service whenever cscfg or cspkg is updated in Azure Blob storage</span><span class="sxs-lookup"><span data-stu-id="e7bdb-116">Continous deployment of a Cloud Service whenever cscfg or cspkg is updated in Azure Blob storage</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Continuous-Deployment-of-A-eeebf3a6)
* [<span data-ttu-id="e7bdb-117">Rebooting Cloud Service instances in parallel, one upgrade domain at a time</span><span class="sxs-lookup"><span data-stu-id="e7bdb-117">Rebooting Cloud Service instances in parallel, one upgrade domain at a time</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Reboot-Cloud-Service-PaaS-b337a06d)

## <a name="next-steps"></a><span data-ttu-id="e7bdb-118">Next Steps</span><span class="sxs-lookup"><span data-stu-id="e7bdb-118">Next Steps</span></span>
<span data-ttu-id="e7bdb-119">Now that you've learned the basics of Azure Automation and how it can be used to manage Azure cloud services, follow these links to learn more about Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="e7bdb-119">Now that you've learned the basics of Azure Automation and how it can be used to manage Azure cloud services, follow these links to learn more about Azure Automation.</span></span>

* [<span data-ttu-id="e7bdb-120">Azure Automation Overview</span><span class="sxs-lookup"><span data-stu-id="e7bdb-120">Azure Automation Overview</span></span>](../automation/automation-intro.md)
* [<span data-ttu-id="e7bdb-121">My first runbook</span><span class="sxs-lookup"><span data-stu-id="e7bdb-121">My first runbook</span></span>](../automation/automation-first-runbook-graphical.md)
* [<span data-ttu-id="e7bdb-122">Azure Automation learning map</span><span class="sxs-lookup"><span data-stu-id="e7bdb-122">Azure Automation learning map</span></span>](https://azure.microsoft.com/documentation/learning-paths/automation/)
