---
title: Update Azure modules in Azure Automation | Microsoft Docs
description: This article describes how you can now update common Azure PowerShell modules provided by default in Azure Automation.
services: automation
documentationcenter: ''
author: MGoedtel
manager: carmonm
editor: tysonn
ms.assetid: ''
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/13/2017
ms.author: magoedte
ms.openlocfilehash: a4cc4de6a7a53b8fcd743767257d74d237e87551
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553607"
---
# <a name="how-to-update-azure-powershell-modules-in-azure-automation"></a><span data-ttu-id="c2661-103">How to update Azure PowerShell modules in Azure Automation</span><span class="sxs-lookup"><span data-stu-id="c2661-103">How to update Azure PowerShell modules in Azure Automation</span></span>

<span data-ttu-id="c2661-104">The most common Azure PowerShell modules are provided by default in each Automation account.</span><span class="sxs-lookup"><span data-stu-id="c2661-104">The most common Azure PowerShell modules are provided by default in each Automation account.</span></span>  <span data-ttu-id="c2661-105">The Azure team updates the Azure modules regularly, so in the Automation account we provide a way for you to update the modules in the account when new versions are available.</span><span class="sxs-lookup"><span data-stu-id="c2661-105">The Azure team updates the Azure modules regularly, so in the Automation account we provide a way for you to update the modules in the account when new versions are available.</span></span>

## <a name="updating-azure-modules"></a><span data-ttu-id="c2661-106">Updating Azure Modules</span><span class="sxs-lookup"><span data-stu-id="c2661-106">Updating Azure Modules</span></span>

1. <span data-ttu-id="c2661-107">In the Modules blade of your Automation account there is an option called **Update Azure Modules**.</span><span class="sxs-lookup"><span data-stu-id="c2661-107">In the Modules blade of your Automation account there is an option called **Update Azure Modules**.</span></span>  <span data-ttu-id="c2661-108">It is always enabled.</span><span class="sxs-lookup"><span data-stu-id="c2661-108">It is always enabled.</span></span><br><br> <span data-ttu-id="c2661-109">![Update Azure Modules option in Modules blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-update-azure-modules/automation-update-azure-modules-option.png)</span><span class="sxs-lookup"><span data-stu-id="c2661-109">![Update Azure Modules option in Modules blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-update-azure-modules/automation-update-azure-modules-option.png)</span></span>

2. <span data-ttu-id="c2661-110">Click **Update Azure Modules** and you will be presented with a confirmation notification that asks you if you want to continue.</span><span class="sxs-lookup"><span data-stu-id="c2661-110">Click **Update Azure Modules** and you will be presented with a confirmation notification that asks you if you want to continue.</span></span><br><br> <span data-ttu-id="c2661-111">![Update Azure Modules notification](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-update-azure-modules/automation-update-azure-modules-notification.png)</span><span class="sxs-lookup"><span data-stu-id="c2661-111">![Update Azure Modules notification](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-update-azure-modules/automation-update-azure-modules-notification.png)</span></span>

3. <span data-ttu-id="c2661-112">Click **Yes** and the module update process will begin.</span><span class="sxs-lookup"><span data-stu-id="c2661-112">Click **Yes** and the module update process will begin.</span></span>  <span data-ttu-id="c2661-113">The update process takes about 15-20 minutes to update the following modules:</span><span class="sxs-lookup"><span data-stu-id="c2661-113">The update process takes about 15-20 minutes to update the following modules:</span></span>

  * <span data-ttu-id="c2661-114">Azure</span><span class="sxs-lookup"><span data-stu-id="c2661-114">Azure</span></span>
  * <span data-ttu-id="c2661-115">Azure.Storage</span><span class="sxs-lookup"><span data-stu-id="c2661-115">Azure.Storage</span></span>
  * <span data-ttu-id="c2661-116">AzureRm.Automation</span><span class="sxs-lookup"><span data-stu-id="c2661-116">AzureRm.Automation</span></span>
  * <span data-ttu-id="c2661-117">AzureRm.Compute</span><span class="sxs-lookup"><span data-stu-id="c2661-117">AzureRm.Compute</span></span>
  * <span data-ttu-id="c2661-118">AzureRm.Profile</span><span class="sxs-lookup"><span data-stu-id="c2661-118">AzureRm.Profile</span></span>
  * <span data-ttu-id="c2661-119">AzureRm.Resources</span><span class="sxs-lookup"><span data-stu-id="c2661-119">AzureRm.Resources</span></span>
  * <span data-ttu-id="c2661-120">AzureRm.Sql</span><span class="sxs-lookup"><span data-stu-id="c2661-120">AzureRm.Sql</span></span>
  * <span data-ttu-id="c2661-121">AzureRm.Storage</span><span class="sxs-lookup"><span data-stu-id="c2661-121">AzureRm.Storage</span></span>

    <span data-ttu-id="c2661-122">If the modules are already up to date, then the process will complete in a few seconds.</span><span class="sxs-lookup"><span data-stu-id="c2661-122">If the modules are already up to date, then the process will complete in a few seconds.</span></span>  <span data-ttu-id="c2661-123">When the update process completes you will be notified.</span><span class="sxs-lookup"><span data-stu-id="c2661-123">When the update process completes you will be notified.</span></span><br><br> ![Update Azure Modules update status](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-update-azure-modules/automation-update-azure-modules-updatestatus.png)

<span data-ttu-id="c2661-125">As part of the update process, the schedules for any scheduled runbooks will be updated to use the latest module version.</span><span class="sxs-lookup"><span data-stu-id="c2661-125">As part of the update process, the schedules for any scheduled runbooks will be updated to use the latest module version.</span></span>

<span data-ttu-id="c2661-126">If you use cmdlets from these Azure PowerShell modules in your runbooks to manage Azure resources, then you will want to perform this update process every month or so to assure that you have the latest modules.</span><span class="sxs-lookup"><span data-stu-id="c2661-126">If you use cmdlets from these Azure PowerShell modules in your runbooks to manage Azure resources, then you will want to perform this update process every month or so to assure that you have the latest modules.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c2661-127">Next steps</span><span class="sxs-lookup"><span data-stu-id="c2661-127">Next steps</span></span>

<span data-ttu-id="c2661-128">To learn more about Integration Modules and how to create custom modules to further integrate Automation with other systems, services, or solutions, see [Integration Modules](automation-integration-modules.md).</span><span class="sxs-lookup"><span data-stu-id="c2661-128">To learn more about Integration Modules and how to create custom modules to further integrate Automation with other systems, services, or solutions, see [Integration Modules](automation-integration-modules.md).</span></span>


