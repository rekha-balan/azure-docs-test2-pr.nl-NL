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
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: afa2feaee4283f008f2c255de7b64e3085fbc6ef
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866704"
---
# <a name="create-a-web-app-and-deploy-code-to-a-staging-environment"></a><span data-ttu-id="83fa5-103">Create a web app and deploy code to a staging environment</span><span class="sxs-lookup"><span data-stu-id="83fa5-103">Create a web app and deploy code to a staging environment</span></span>

<span data-ttu-id="83fa5-104">This sample script creates a web app in App Service with an additional deployment slot called "staging", and then deploys a sample app to the "staging" slot.</span><span class="sxs-lookup"><span data-stu-id="83fa5-104">This sample script creates a web app in App Service with an additional deployment slot called "staging", and then deploys a sample app to the "staging" slot.</span></span>

<span data-ttu-id="83fa5-105">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Connect-AzureRmAccount` to create a connection with Azure.</span><span class="sxs-lookup"><span data-stu-id="83fa5-105">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Connect-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="83fa5-106">Sample script</span><span class="sxs-lookup"><span data-stu-id="83fa5-106">Sample script</span></span>

[!code-azurepowershell-interactive[main](../../../powershell_scripts/app-service/deploy-deployment-slot/deploy-deployment-slot.ps1?highlight=1 "Create a web app and deploy code to a staging environment")]

## <a name="clean-up-deployment"></a><span data-ttu-id="83fa5-107">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="83fa5-107">Clean up deployment</span></span> 

<span data-ttu-id="83fa5-108">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="83fa5-108">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="83fa5-109">Script explanation</span><span class="sxs-lookup"><span data-stu-id="83fa5-109">Script explanation</span></span>

<span data-ttu-id="83fa5-110">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="83fa5-110">This script uses the following commands.</span></span> <span data-ttu-id="83fa5-111">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="83fa5-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="83fa5-112">Command</span><span class="sxs-lookup"><span data-stu-id="83fa5-112">Command</span></span> | <span data-ttu-id="83fa5-113">Notes</span><span class="sxs-lookup"><span data-stu-id="83fa5-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="83fa5-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="83fa5-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="83fa5-115">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="83fa5-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="83fa5-116">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="83fa5-116">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="83fa5-117">Creates an App Service plan.</span><span class="sxs-lookup"><span data-stu-id="83fa5-117">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="83fa5-118">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="83fa5-118">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="83fa5-119">Creates a web app.</span><span class="sxs-lookup"><span data-stu-id="83fa5-119">Creates a web app.</span></span> |
| [<span data-ttu-id="83fa5-120">Set-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="83fa5-120">Set-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/set-azurermappserviceplan) | <span data-ttu-id="83fa5-121">Modifies an App Service plan to change its pricing tier.</span><span class="sxs-lookup"><span data-stu-id="83fa5-121">Modifies an App Service plan to change its pricing tier.</span></span> |
| [<span data-ttu-id="83fa5-122">New-AzureRmWebAppSlot</span><span class="sxs-lookup"><span data-stu-id="83fa5-122">New-AzureRmWebAppSlot</span></span>](/powershell/module/azurerm.websites/new-azurermwebappslot) | <span data-ttu-id="83fa5-123">Creates a deployment slot for a web app.</span><span class="sxs-lookup"><span data-stu-id="83fa5-123">Creates a deployment slot for a web app.</span></span> |
| [<span data-ttu-id="83fa5-124">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="83fa5-124">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/set-azurermresource) | <span data-ttu-id="83fa5-125">Modifies a resource in a resource group.</span><span class="sxs-lookup"><span data-stu-id="83fa5-125">Modifies a resource in a resource group.</span></span> |
| [<span data-ttu-id="83fa5-126">Switch-AzureRmWebAppSlot</span><span class="sxs-lookup"><span data-stu-id="83fa5-126">Switch-AzureRmWebAppSlot</span></span>](/powershell/module/azurerm.websites/switch-azurermwebappslot) | <span data-ttu-id="83fa5-127">Swaps a web app's deployment slot into production.</span><span class="sxs-lookup"><span data-stu-id="83fa5-127">Swaps a web app's deployment slot into production.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="83fa5-128">Next steps</span><span class="sxs-lookup"><span data-stu-id="83fa5-128">Next steps</span></span>

<span data-ttu-id="83fa5-129">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="83fa5-129">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="83fa5-130">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="83fa5-130">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
