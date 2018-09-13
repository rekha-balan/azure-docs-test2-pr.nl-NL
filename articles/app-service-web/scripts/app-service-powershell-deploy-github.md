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
ms.topic: article
ms.date: 03/20/2017
ms.author: cephalin
ms.openlocfilehash: f85a45f453bf707ffb544440c6592d29755406a6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555469"
---
# <a name="create-a-web-app-and-deploy-code-from-github"></a><span data-ttu-id="45225-103">Create a web app and deploy code from GitHub</span><span class="sxs-lookup"><span data-stu-id="45225-103">Create a web app and deploy code from GitHub</span></span>

<span data-ttu-id="45225-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code from a public GitHub repository (without continuous deployment).</span><span class="sxs-lookup"><span data-stu-id="45225-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code from a public GitHub repository (without continuous deployment).</span></span> <span data-ttu-id="45225-105">For GitHub deployment with continuous deployment, see [Create a web app with continuous deployment from GitHub](app-service-powershell-continuous-deployment-github.md).</span><span class="sxs-lookup"><span data-stu-id="45225-105">For GitHub deployment with continuous deployment, see [Create a web app with continuous deployment from GitHub](app-service-powershell-continuous-deployment-github.md).</span></span>

<span data-ttu-id="45225-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/).</span><span class="sxs-lookup"><span data-stu-id="45225-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/).</span></span> <span data-ttu-id="45225-107">Also, you need a link to GitHub repository that contains the web app code.</span><span class="sxs-lookup"><span data-stu-id="45225-107">Also, you need a link to GitHub repository that contains the web app code.</span></span>

## <a name="sample-script"></a><span data-ttu-id="45225-108">Sample script</span><span class="sxs-lookup"><span data-stu-id="45225-108">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/deploy-github/deploy-github.ps1?highlight=1-2 "Create a web app and deploy code from GitHub")]

## <a name="clean-up-deployment"></a><span data-ttu-id="45225-109">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="45225-109">Clean up deployment</span></span> 

<span data-ttu-id="45225-110">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="45225-110">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="45225-111">Script explanation</span><span class="sxs-lookup"><span data-stu-id="45225-111">Script explanation</span></span>

<span data-ttu-id="45225-112">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="45225-112">This script uses the following commands.</span></span> <span data-ttu-id="45225-113">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="45225-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="45225-114">Command</span><span class="sxs-lookup"><span data-stu-id="45225-114">Command</span></span> | <span data-ttu-id="45225-115">Notes</span><span class="sxs-lookup"><span data-stu-id="45225-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="45225-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="45225-116">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="45225-117">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="45225-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="45225-118">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="45225-118">New-AzureRmAppServicePlan</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.websites/v2.5.0/new-azurermappserviceplan) | <span data-ttu-id="45225-119">Creates an App Service plan.</span><span class="sxs-lookup"><span data-stu-id="45225-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="45225-120">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="45225-120">New-AzureRmWebApp</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.websites/v2.5.0/new-azurermwebapp) | <span data-ttu-id="45225-121">Creates a web app.</span><span class="sxs-lookup"><span data-stu-id="45225-121">Creates a web app.</span></span> |
| [<span data-ttu-id="45225-122">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="45225-122">Set-AzureRmResource</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/set-azurermresource) | <span data-ttu-id="45225-123">Modifies a resource in a resource group.</span><span class="sxs-lookup"><span data-stu-id="45225-123">Modifies a resource in a resource group.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="45225-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="45225-124">Next steps</span></span>

<span data-ttu-id="45225-125">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/).</span><span class="sxs-lookup"><span data-stu-id="45225-125">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/).</span></span>

<span data-ttu-id="45225-126">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="45225-126">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
