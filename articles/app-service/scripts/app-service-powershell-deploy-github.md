---
title: Azure PowerShell Script Sample - Create a web app and deploy code from GitHub | Microsoft Docs
description: Azure PowerShell Script Sample - Create a web app and deploy code from GitHub
services: app-service\web
documentationcenter: ''
author: cephalin
manager: erikre
editor: ''
tags: azure-service-management
ms.assetid: 0f9c8bc5-3789-4eb3-8deb-ae6e2200795a
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: d60503e195c1a8f32992cfb1978ad7a181c069b0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867554"
---
# <a name="create-a-web-app-and-deploy-code-from-github"></a><span data-ttu-id="d4a71-103">Create a web app and deploy code from GitHub</span><span class="sxs-lookup"><span data-stu-id="d4a71-103">Create a web app and deploy code from GitHub</span></span>

<span data-ttu-id="d4a71-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code from a public GitHub repository (without continuous deployment).</span><span class="sxs-lookup"><span data-stu-id="d4a71-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code from a public GitHub repository (without continuous deployment).</span></span> <span data-ttu-id="d4a71-105">For GitHub deployment with continuous deployment, see [Create a web app with continuous deployment from GitHub](app-service-powershell-continuous-deployment-github.md).</span><span class="sxs-lookup"><span data-stu-id="d4a71-105">For GitHub deployment with continuous deployment, see [Create a web app with continuous deployment from GitHub](app-service-powershell-continuous-deployment-github.md).</span></span>

<span data-ttu-id="d4a71-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Connect-AzureRmAccount` to create a connection with Azure.</span><span class="sxs-lookup"><span data-stu-id="d4a71-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Connect-AzureRmAccount` to create a connection with Azure.</span></span> <span data-ttu-id="d4a71-107">Also, you need a link to GitHub repository that contains the web app code.</span><span class="sxs-lookup"><span data-stu-id="d4a71-107">Also, you need a link to GitHub repository that contains the web app code.</span></span>

## <a name="sample-script"></a><span data-ttu-id="d4a71-108">Sample script</span><span class="sxs-lookup"><span data-stu-id="d4a71-108">Sample script</span></span>

[!code-azurepowershell-interactive[main](../../../powershell_scripts/app-service/deploy-github/deploy-github.ps1?highlight=1-2 "Create a web app and deploy code from GitHub")]

## <a name="clean-up-deployment"></a><span data-ttu-id="d4a71-109">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="d4a71-109">Clean up deployment</span></span> 

<span data-ttu-id="d4a71-110">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="d4a71-110">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="d4a71-111">Script explanation</span><span class="sxs-lookup"><span data-stu-id="d4a71-111">Script explanation</span></span>

<span data-ttu-id="d4a71-112">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="d4a71-112">This script uses the following commands.</span></span> <span data-ttu-id="d4a71-113">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="d4a71-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="d4a71-114">Command</span><span class="sxs-lookup"><span data-stu-id="d4a71-114">Command</span></span> | <span data-ttu-id="d4a71-115">Notes</span><span class="sxs-lookup"><span data-stu-id="d4a71-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d4a71-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="d4a71-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="d4a71-117">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="d4a71-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="d4a71-118">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="d4a71-118">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="d4a71-119">Creates an App Service plan.</span><span class="sxs-lookup"><span data-stu-id="d4a71-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="d4a71-120">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="d4a71-120">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="d4a71-121">Creates a web app.</span><span class="sxs-lookup"><span data-stu-id="d4a71-121">Creates a web app.</span></span> |
| [<span data-ttu-id="d4a71-122">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="d4a71-122">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/set-azurermresource) | <span data-ttu-id="d4a71-123">Modifies a resource in a resource group.</span><span class="sxs-lookup"><span data-stu-id="d4a71-123">Modifies a resource in a resource group.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d4a71-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="d4a71-124">Next steps</span></span>

<span data-ttu-id="d4a71-125">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d4a71-125">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="d4a71-126">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="d4a71-126">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
