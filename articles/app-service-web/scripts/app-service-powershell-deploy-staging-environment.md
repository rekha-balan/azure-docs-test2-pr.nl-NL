---
title: Azure PowerShell Script Sample - Create a web app and deploy code to a staging environment | Microsoft Docs
description: Azure PowerShell Script Sample - Create a web app and deploy code to a staging environment
services: app-service\web
documentationcenter: ''
author: cephalin
manager: erikre
editor: ''
tags: azure-service-management
ms.assetid: 27cf0680-c3a9-4a58-9f71-6dec09f6b874
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: cephalin
ms.openlocfilehash: 9fbedec9cee316b22837373e7895fc6012eb39a6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562923"
---
# <a name="create-a-web-app-and-deploy-code-to-a-staging-environment"></a><span data-ttu-id="0f02c-103">Create a web app and deploy code to a staging environment</span><span class="sxs-lookup"><span data-stu-id="0f02c-103">Create a web app and deploy code to a staging environment</span></span>

<span data-ttu-id="0f02c-104">This sample script creates a web app in App Service with an additional deployment slot called "staging", and then deploys a sample app to the "staging" slot.</span><span class="sxs-lookup"><span data-stu-id="0f02c-104">This sample script creates a web app in App Service with an additional deployment slot called "staging", and then deploys a sample app to the "staging" slot.</span></span>

<span data-ttu-id="0f02c-105">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` to create a connection with Azure.</span><span class="sxs-lookup"><span data-stu-id="0f02c-105">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="0f02c-106">Sample script</span><span class="sxs-lookup"><span data-stu-id="0f02c-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/deploy-deployment-slot/deploy-deployment-slot.ps1?highlight=1 "Create a web app and deploy code to a staging environment")]

## <a name="clean-up-deployment"></a><span data-ttu-id="0f02c-107">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="0f02c-107">Clean up deployment</span></span> 

<span data-ttu-id="0f02c-108">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="0f02c-108">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="0f02c-109">Script explanation</span><span class="sxs-lookup"><span data-stu-id="0f02c-109">Script explanation</span></span>

<span data-ttu-id="0f02c-110">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="0f02c-110">This script uses the following commands.</span></span> <span data-ttu-id="0f02c-111">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="0f02c-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="0f02c-112">Command</span><span class="sxs-lookup"><span data-stu-id="0f02c-112">Command</span></span> | <span data-ttu-id="0f02c-113">Notes</span><span class="sxs-lookup"><span data-stu-id="0f02c-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="0f02c-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="0f02c-114">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="0f02c-115">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="0f02c-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="0f02c-116">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="0f02c-116">New-AzureRmAppServicePlan</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.websites/v2.5.0/new-azurermappserviceplan) | <span data-ttu-id="0f02c-117">Creates an App Service plan.</span><span class="sxs-lookup"><span data-stu-id="0f02c-117">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="0f02c-118">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="0f02c-118">New-AzureRmWebApp</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.websites/v2.5.0/new-azurermwebapp) | <span data-ttu-id="0f02c-119">Creates a web app.</span><span class="sxs-lookup"><span data-stu-id="0f02c-119">Creates a web app.</span></span> |
| [<span data-ttu-id="0f02c-120">Set-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="0f02c-120">Set-AzureRmAppServicePlan</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.websites/v2.5.0/set-azurermappserviceplan) | <span data-ttu-id="0f02c-121">Modifies an App Service plan to change its pricing tier.</span><span class="sxs-lookup"><span data-stu-id="0f02c-121">Modifies an App Service plan to change its pricing tier.</span></span> |
| [<span data-ttu-id="0f02c-122">New-AzureRmWebAppSlot</span><span class="sxs-lookup"><span data-stu-id="0f02c-122">New-AzureRmWebAppSlot</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.websites/v2.5.0/new-azurermwebappslot) | <span data-ttu-id="0f02c-123">Creates a deployment slot for a web app.</span><span class="sxs-lookup"><span data-stu-id="0f02c-123">Creates a deployment slot for a web app.</span></span> |
| [<span data-ttu-id="0f02c-124">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="0f02c-124">Set-AzureRmResource</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/set-azurermresource) | <span data-ttu-id="0f02c-125">Modifies a resource in a resource group.</span><span class="sxs-lookup"><span data-stu-id="0f02c-125">Modifies a resource in a resource group.</span></span> |
| [<span data-ttu-id="0f02c-126">Swap-AzureRmWebAppSlot</span><span class="sxs-lookup"><span data-stu-id="0f02c-126">Swap-AzureRmWebAppSlot</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.websites/v2.5.0/swap-azurermwebappslot) | <span data-ttu-id="0f02c-127">Swaps a web app's deployment slot into production.</span><span class="sxs-lookup"><span data-stu-id="0f02c-127">Swaps a web app's deployment slot into production.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="0f02c-128">Next steps</span><span class="sxs-lookup"><span data-stu-id="0f02c-128">Next steps</span></span>

<span data-ttu-id="0f02c-129">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/).</span><span class="sxs-lookup"><span data-stu-id="0f02c-129">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/).</span></span>

<span data-ttu-id="0f02c-130">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="0f02c-130">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
