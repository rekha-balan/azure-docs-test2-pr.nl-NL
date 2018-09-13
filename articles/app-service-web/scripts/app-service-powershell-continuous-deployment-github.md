---
title: Azure PowerShell Script Sample - Create a web app with continuous deployment from GitHub | Microsoft Docs
description: Azure PowerShell Script Sample - Create a web app with continuous deployment from GitHub
services: app-service\web
documentationcenter: ''
author: cephalin
manager: erikre
editor: ''
tags: azure-service-management
ms.assetid: 42f901f8-02f7-4869-b22d-d99ef59f874c
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: cephalin
ms.openlocfilehash: b6b82aa6f129a008091e4abc1798b9b5d402c28e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549413"
---
# <a name="create-a-web-app-with-continuous-deployment-from-github"></a><span data-ttu-id="770a6-103">Create a web app with continuous deployment from GitHub</span><span class="sxs-lookup"><span data-stu-id="770a6-103">Create a web app with continuous deployment from GitHub</span></span>

<span data-ttu-id="770a6-104">This sample script creates a web app in App Service with its related resources, and then sets up continuous deployment from a GitHub repository.</span><span class="sxs-lookup"><span data-stu-id="770a6-104">This sample script creates a web app in App Service with its related resources, and then sets up continuous deployment from a GitHub repository.</span></span> <span data-ttu-id="770a6-105">For GitHub deployment without continuous deployment, see [Create a web app and deploy code from GitHub](app-service-powershell-deploy-github.md).</span><span class="sxs-lookup"><span data-stu-id="770a6-105">For GitHub deployment without continuous deployment, see [Create a web app and deploy code from GitHub](app-service-powershell-deploy-github.md).</span></span>

<span data-ttu-id="770a6-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/).</span><span class="sxs-lookup"><span data-stu-id="770a6-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/).</span></span> <span data-ttu-id="770a6-107">Also, ensure that:</span><span class="sxs-lookup"><span data-stu-id="770a6-107">Also, ensure that:</span></span>

- <span data-ttu-id="770a6-108">A connection with Azure has been created using the `az login` command.</span><span class="sxs-lookup"><span data-stu-id="770a6-108">A connection with Azure has been created using the `az login` command.</span></span>
- <span data-ttu-id="770a6-109">The application code is in a public or private GitHub repository that you own.</span><span class="sxs-lookup"><span data-stu-id="770a6-109">The application code is in a public or private GitHub repository that you own.</span></span>
- <span data-ttu-id="770a6-110">You have [created an access token in your GitHub account](https://help.github.com/articles/creating-an-access-token-for-command-line-use/).</span><span class="sxs-lookup"><span data-stu-id="770a6-110">You have [created an access token in your GitHub account](https://help.github.com/articles/creating-an-access-token-for-command-line-use/).</span></span>

## <a name="sample-script"></a><span data-ttu-id="770a6-111">Sample script</span><span class="sxs-lookup"><span data-stu-id="770a6-111">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/deploy-github-continuous/deploy-github-continuous.ps1?highlight=1-2 "Create a web app with continuous deployment from GitHub")]

## <a name="clean-up-deployment"></a><span data-ttu-id="770a6-112">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="770a6-112">Clean up deployment</span></span> 

<span data-ttu-id="770a6-113">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="770a6-113">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="770a6-114">Script explanation</span><span class="sxs-lookup"><span data-stu-id="770a6-114">Script explanation</span></span>

<span data-ttu-id="770a6-115">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="770a6-115">This script uses the following commands.</span></span> <span data-ttu-id="770a6-116">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="770a6-116">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="770a6-117">Command</span><span class="sxs-lookup"><span data-stu-id="770a6-117">Command</span></span> | <span data-ttu-id="770a6-118">Notes</span><span class="sxs-lookup"><span data-stu-id="770a6-118">Notes</span></span> |
|---|---|
| [<span data-ttu-id="770a6-119">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="770a6-119">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="770a6-120">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="770a6-120">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="770a6-121">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="770a6-121">New-AzureRmAppServicePlan</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.websites/v2.5.0/new-azurermappserviceplan) | <span data-ttu-id="770a6-122">Creates an App Service plan.</span><span class="sxs-lookup"><span data-stu-id="770a6-122">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="770a6-123">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="770a6-123">New-AzureRmWebApp</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.websites/v2.5.0/new-azurermwebapp) | <span data-ttu-id="770a6-124">Creates a web app.</span><span class="sxs-lookup"><span data-stu-id="770a6-124">Creates a web app.</span></span> |
| [<span data-ttu-id="770a6-125">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="770a6-125">Set-AzureRmResource</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/set-azurermresource) | <span data-ttu-id="770a6-126">Modifies a resource in a resource group.</span><span class="sxs-lookup"><span data-stu-id="770a6-126">Modifies a resource in a resource group.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="770a6-127">Next steps</span><span class="sxs-lookup"><span data-stu-id="770a6-127">Next steps</span></span>

<span data-ttu-id="770a6-128">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/).</span><span class="sxs-lookup"><span data-stu-id="770a6-128">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/).</span></span>

<span data-ttu-id="770a6-129">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="770a6-129">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
