---
title: Update Azure modules in Azure Automation
description: This article describes how you can now update common Azure PowerShell modules provided by default in Azure Automation.
services: automation
ms.service: automation
ms.component: process-automation
author: georgewallace
ms.author: gwallace
ms.date: 03/16/2018
ms.topic: conceptual
manager: carmonm
ms.openlocfilehash: 9358c7ba72e16ed54514d42c1366420ef2f37324
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44776886"
---
# <a name="how-to-update-azure-powershell-modules-in-azure-automation"></a><span data-ttu-id="daccf-103">How to update Azure PowerShell modules in Azure Automation</span><span class="sxs-lookup"><span data-stu-id="daccf-103">How to update Azure PowerShell modules in Azure Automation</span></span>

<span data-ttu-id="daccf-104">The most common Azure PowerShell modules are provided by default in each Automation account.</span><span class="sxs-lookup"><span data-stu-id="daccf-104">The most common Azure PowerShell modules are provided by default in each Automation account.</span></span> <span data-ttu-id="daccf-105">The Azure team updates the Azure modules regularly, so in the Automation account you are provided a way to update the modules in the account when new versions are available from the portal.</span><span class="sxs-lookup"><span data-stu-id="daccf-105">The Azure team updates the Azure modules regularly, so in the Automation account you are provided a way to update the modules in the account when new versions are available from the portal.</span></span>

<span data-ttu-id="daccf-106">Because modules are updated regularly by the product group, changes can occur with the  included cmdlets, which may negatively impact your runbooks depending on the type of change, such as renaming a parameter or deprecating a cmdlet entirely.</span><span class="sxs-lookup"><span data-stu-id="daccf-106">Because modules are updated regularly by the product group, changes can occur with the  included cmdlets, which may negatively impact your runbooks depending on the type of change, such as renaming a parameter or deprecating a cmdlet entirely.</span></span> <span data-ttu-id="daccf-107">To avoid impacting your runbooks and the processes they automate, it is recommended that you test and validate before proceeding.</span><span class="sxs-lookup"><span data-stu-id="daccf-107">To avoid impacting your runbooks and the processes they automate, it is recommended that you test and validate before proceeding.</span></span> <span data-ttu-id="daccf-108">If you do not have a dedicated Automation account intended for this purpose, consider creating one so that you can test many different scenarios and permutations during the development of your runbooks, in addition to iterative changes such as updating the PowerShell modules.</span><span class="sxs-lookup"><span data-stu-id="daccf-108">If you do not have a dedicated Automation account intended for this purpose, consider creating one so that you can test many different scenarios and permutations during the development of your runbooks, in addition to iterative changes such as updating the PowerShell modules.</span></span> <span data-ttu-id="daccf-109">After the results are validated and you have applied any changes required, proceed with coordinating the migration of any runbooks that required modification and perform the following update as described in production.</span><span class="sxs-lookup"><span data-stu-id="daccf-109">After the results are validated and you have applied any changes required, proceed with coordinating the migration of any runbooks that required modification and perform the following update as described in production.</span></span>

> [!NOTE]
> <span data-ttu-id="daccf-110">A new Automation account might not contain the latest modules.</span><span class="sxs-lookup"><span data-stu-id="daccf-110">A new Automation account might not contain the latest modules.</span></span>

## <a name="updating-azure-modules"></a><span data-ttu-id="daccf-111">Updating Azure Modules</span><span class="sxs-lookup"><span data-stu-id="daccf-111">Updating Azure Modules</span></span>

1. <span data-ttu-id="daccf-112">In the Modules page of your Automation account, there is an option called **Update Azure Modules**.</span><span class="sxs-lookup"><span data-stu-id="daccf-112">In the Modules page of your Automation account, there is an option called **Update Azure Modules**.</span></span> <span data-ttu-id="daccf-113">It is always enabled.</span><span class="sxs-lookup"><span data-stu-id="daccf-113">It is always enabled.</span></span><br><br> <span data-ttu-id="daccf-114">![Update Azure Modules option in Modules page](media/automation-update-azure-modules/automation-update-azure-modules-option.png)</span><span class="sxs-lookup"><span data-stu-id="daccf-114">![Update Azure Modules option in Modules page](media/automation-update-azure-modules/automation-update-azure-modules-option.png)</span></span>

2. <span data-ttu-id="daccf-115">Click **Update Azure Modules**, a confirmation notification is shown that asks if you want to continue.</span><span class="sxs-lookup"><span data-stu-id="daccf-115">Click **Update Azure Modules**, a confirmation notification is shown that asks if you want to continue.</span></span><br><br> <span data-ttu-id="daccf-116">![Update Azure Modules notification](media/automation-update-azure-modules/automation-update-azure-modules-popup.png)</span><span class="sxs-lookup"><span data-stu-id="daccf-116">![Update Azure Modules notification](media/automation-update-azure-modules/automation-update-azure-modules-popup.png)</span></span>

3. <span data-ttu-id="daccf-117">Click **Yes** and the module update process begins.</span><span class="sxs-lookup"><span data-stu-id="daccf-117">Click **Yes** and the module update process begins.</span></span> <span data-ttu-id="daccf-118">The update process takes about 15-20 minutes to update the following modules:</span><span class="sxs-lookup"><span data-stu-id="daccf-118">The update process takes about 15-20 minutes to update the following modules:</span></span>

  * <span data-ttu-id="daccf-119">Azure</span><span class="sxs-lookup"><span data-stu-id="daccf-119">Azure</span></span>
  * <span data-ttu-id="daccf-120">Azure.Storage</span><span class="sxs-lookup"><span data-stu-id="daccf-120">Azure.Storage</span></span>
  * <span data-ttu-id="daccf-121">AzureRm.Automation</span><span class="sxs-lookup"><span data-stu-id="daccf-121">AzureRm.Automation</span></span>
  * <span data-ttu-id="daccf-122">AzureRm.Compute</span><span class="sxs-lookup"><span data-stu-id="daccf-122">AzureRm.Compute</span></span>
  * <span data-ttu-id="daccf-123">AzureRm.Profile</span><span class="sxs-lookup"><span data-stu-id="daccf-123">AzureRm.Profile</span></span>
  * <span data-ttu-id="daccf-124">AzureRm.Resources</span><span class="sxs-lookup"><span data-stu-id="daccf-124">AzureRm.Resources</span></span>
  * <span data-ttu-id="daccf-125">AzureRm.Sql</span><span class="sxs-lookup"><span data-stu-id="daccf-125">AzureRm.Sql</span></span>
  * <span data-ttu-id="daccf-126">AzureRm.Storage</span><span class="sxs-lookup"><span data-stu-id="daccf-126">AzureRm.Storage</span></span>

    <span data-ttu-id="daccf-127">If the modules are already up-to-date, then the process completes in a few seconds.</span><span class="sxs-lookup"><span data-stu-id="daccf-127">If the modules are already up-to-date, then the process completes in a few seconds.</span></span> <span data-ttu-id="daccf-128">When the update process completes, you are notified.</span><span class="sxs-lookup"><span data-stu-id="daccf-128">When the update process completes, you are notified.</span></span><br><br> ![Update Azure Modules update status](media/automation-update-azure-modules/automation-update-azure-modules-updatestatus.png)

> [!NOTE]
> <span data-ttu-id="daccf-130">Azure Automation uses the latest modules in your Automation account when a new scheduled job is run.</span><span class="sxs-lookup"><span data-stu-id="daccf-130">Azure Automation uses the latest modules in your Automation account when a new scheduled job is run.</span></span>    

<span data-ttu-id="daccf-131">If you use cmdlets from these Azure PowerShell modules in your runbooks, you want to run this update process every month or so to make sure that you have the latest modules.</span><span class="sxs-lookup"><span data-stu-id="daccf-131">If you use cmdlets from these Azure PowerShell modules in your runbooks, you want to run this update process every month or so to make sure that you have the latest modules.</span></span> <span data-ttu-id="daccf-132">Azure Automation uses the AzureRunAsConnection connection to authenticate when updating the modules, if the service principal is expired or no longer exists on the subscription level, the module update will fail.</span><span class="sxs-lookup"><span data-stu-id="daccf-132">Azure Automation uses the AzureRunAsConnection connection to authenticate when updating the modules, if the service principal is expired or no longer exists on the subscription level, the module update will fail.</span></span>

## <a name="next-steps"></a><span data-ttu-id="daccf-133">Next steps</span><span class="sxs-lookup"><span data-stu-id="daccf-133">Next steps</span></span>

* <span data-ttu-id="daccf-134">To learn more about Integration Modules and how to create custom modules to further integrate Automation with other systems, services, or solutions, see [Integration Modules](automation-integration-modules.md).</span><span class="sxs-lookup"><span data-stu-id="daccf-134">To learn more about Integration Modules and how to create custom modules to further integrate Automation with other systems, services, or solutions, see [Integration Modules](automation-integration-modules.md).</span></span>

* <span data-ttu-id="daccf-135">Consider source control integration using [GitHub Enterprise](automation-scenario-source-control-integration-with-github-ent.md) or [Azure DevOps](automation-scenario-source-control-integration-with-vsts.md) to centrally manage and control releases of your Automation runbook and configuration portfolio.</span><span class="sxs-lookup"><span data-stu-id="daccf-135">Consider source control integration using [GitHub Enterprise](automation-scenario-source-control-integration-with-github-ent.md) or [Azure DevOps](automation-scenario-source-control-integration-with-vsts.md) to centrally manage and control releases of your Automation runbook and configuration portfolio.</span></span>  
