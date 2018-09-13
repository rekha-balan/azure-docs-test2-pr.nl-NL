---
title: Azure PowerShell Script Sample - Create a web app and deploy code from a local Git repository | Microsoft Docs
description: Azure PowerShell Script Sample - Create a web app and deploy code from a local Git repository
services: app-service\web
documentationcenter: ''
author: cephalin
manager: erikre
editor: ''
tags: azure-service-management
ms.assetid: 5a927f23-8e70-45fd-9aae-980d4e7a007d
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: cephalin
ms.openlocfilehash: ec3407f54c3affc21bde4e2e6fa76a174a46159c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670162"
---
# <a name="create-a-web-app-and-deploy-code-from-a-local-git-repository"></a><span data-ttu-id="3e02c-103">Create a web app and deploy code from a local Git repository</span><span class="sxs-lookup"><span data-stu-id="3e02c-103">Create a web app and deploy code from a local Git repository</span></span>

<span data-ttu-id="3e02c-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code in a local Git repository.</span><span class="sxs-lookup"><span data-stu-id="3e02c-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code in a local Git repository.</span></span>

<span data-ttu-id="3e02c-105">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` to create a connection with Azure.</span><span class="sxs-lookup"><span data-stu-id="3e02c-105">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span> <span data-ttu-id="3e02c-106">Also, your application code needs to be committed into a local Git repository.</span><span class="sxs-lookup"><span data-stu-id="3e02c-106">Also, your application code needs to be committed into a local Git repository.</span></span>

## <a name="sample-script"></a><span data-ttu-id="3e02c-107">Sample script</span><span class="sxs-lookup"><span data-stu-id="3e02c-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/deploy-local-git/deploy-local-git.ps1?highlight=1 "Create a web app and deploy code from a local Git repository")]

## <a name="clean-up-deployment"></a><span data-ttu-id="3e02c-108">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="3e02c-108">Clean up deployment</span></span> 

<span data-ttu-id="3e02c-109">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="3e02c-109">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="3e02c-110">Script explanation</span><span class="sxs-lookup"><span data-stu-id="3e02c-110">Script explanation</span></span>

<span data-ttu-id="3e02c-111">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="3e02c-111">This script uses the following commands.</span></span> <span data-ttu-id="3e02c-112">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="3e02c-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="3e02c-113">Command</span><span class="sxs-lookup"><span data-stu-id="3e02c-113">Command</span></span> | <span data-ttu-id="3e02c-114">Notes</span><span class="sxs-lookup"><span data-stu-id="3e02c-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="3e02c-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="3e02c-115">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="3e02c-116">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="3e02c-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="3e02c-117">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="3e02c-117">New-AzureRmAppServicePlan</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.websites/v2.5.0/new-azurermappserviceplan) | <span data-ttu-id="3e02c-118">Creates an App Service plan.</span><span class="sxs-lookup"><span data-stu-id="3e02c-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="3e02c-119">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="3e02c-119">New-AzureRmWebApp</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.websites/v2.5.0/new-azurermwebapp) | <span data-ttu-id="3e02c-120">Creates a web app.</span><span class="sxs-lookup"><span data-stu-id="3e02c-120">Creates a web app.</span></span> |
| [<span data-ttu-id="3e02c-121">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="3e02c-121">Set-AzureRmResource</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/set-azurermresource) | <span data-ttu-id="3e02c-122">Modifies a resource in a resource group.</span><span class="sxs-lookup"><span data-stu-id="3e02c-122">Modifies a resource in a resource group.</span></span> |
| [<span data-ttu-id="3e02c-123">Get-AzureRmWebAppPublishingProfile</span><span class="sxs-lookup"><span data-stu-id="3e02c-123">Get-AzureRmWebAppPublishingProfile</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.websites/v2.5.0/get-azurermwebapppublishingprofile) | <span data-ttu-id="3e02c-124">Get a web app's publishing profile.</span><span class="sxs-lookup"><span data-stu-id="3e02c-124">Get a web app's publishing profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="3e02c-125">Next steps</span><span class="sxs-lookup"><span data-stu-id="3e02c-125">Next steps</span></span>

<span data-ttu-id="3e02c-126">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/).</span><span class="sxs-lookup"><span data-stu-id="3e02c-126">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/).</span></span>

<span data-ttu-id="3e02c-127">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="3e02c-127">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
