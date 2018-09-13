---
title: Azure PowerShell Script Sample - Assign a custom domain to a web app | Microsoft Docs
description: Azure PowerShell Script Sample - Assign a custom domain to a web app
services: app-service\web
documentationcenter: ''
author: cephalin
manager: erikre
editor: ''
tags: azure-service-management
ms.assetid: 356f5af9-f62e-411c-8b24-deba05214103
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: f07a43f3bb0895bf05565c0d683e1242c4518545
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869195"
---
# <a name="assign-a-custom-domain-to-a-web-app"></a><span data-ttu-id="43efa-103">Assign a custom domain to a web app</span><span class="sxs-lookup"><span data-stu-id="43efa-103">Assign a custom domain to a web app</span></span>

<span data-ttu-id="43efa-104">This sample script creates a web app in App Service with its related resources, and then maps `www.<yourdomain>` to it.</span><span class="sxs-lookup"><span data-stu-id="43efa-104">This sample script creates a web app in App Service with its related resources, and then maps `www.<yourdomain>` to it.</span></span> 

<span data-ttu-id="43efa-105">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Connect-AzureRmAccount` to create a connection with Azure.</span><span class="sxs-lookup"><span data-stu-id="43efa-105">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Connect-AzureRmAccount` to create a connection with Azure.</span></span> <span data-ttu-id="43efa-106">Also, you need to have access to your domain registrar's DNS configuration page.</span><span class="sxs-lookup"><span data-stu-id="43efa-106">Also, you need to have access to your domain registrar's DNS configuration page.</span></span>

## <a name="sample-script"></a><span data-ttu-id="43efa-107">Sample script</span><span class="sxs-lookup"><span data-stu-id="43efa-107">Sample script</span></span>

[!code-azurepowershell-interactive[main](../../../powershell_scripts/app-service/map-custom-domain/map-custom-domain.ps1?highlight=1 "Assign a custom domain to a web app")]

## <a name="clean-up-deployment"></a><span data-ttu-id="43efa-108">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="43efa-108">Clean up deployment</span></span> 

<span data-ttu-id="43efa-109">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="43efa-109">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="43efa-110">Script explanation</span><span class="sxs-lookup"><span data-stu-id="43efa-110">Script explanation</span></span>

<span data-ttu-id="43efa-111">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="43efa-111">This script uses the following commands.</span></span> <span data-ttu-id="43efa-112">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="43efa-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="43efa-113">Command</span><span class="sxs-lookup"><span data-stu-id="43efa-113">Command</span></span> | <span data-ttu-id="43efa-114">Notes</span><span class="sxs-lookup"><span data-stu-id="43efa-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="43efa-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="43efa-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="43efa-116">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="43efa-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="43efa-117">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="43efa-117">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="43efa-118">Creates an App Service plan.</span><span class="sxs-lookup"><span data-stu-id="43efa-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="43efa-119">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="43efa-119">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="43efa-120">Creates a web app.</span><span class="sxs-lookup"><span data-stu-id="43efa-120">Creates a web app.</span></span> |
| [<span data-ttu-id="43efa-121">Set-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="43efa-121">Set-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/set-azurermappserviceplan) | <span data-ttu-id="43efa-122">Modifies an App Service plan to change its pricing tier.</span><span class="sxs-lookup"><span data-stu-id="43efa-122">Modifies an App Service plan to change its pricing tier.</span></span> |
| [<span data-ttu-id="43efa-123">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="43efa-123">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="43efa-124">Modifies a web app's configuration.</span><span class="sxs-lookup"><span data-stu-id="43efa-124">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="43efa-125">Next steps</span><span class="sxs-lookup"><span data-stu-id="43efa-125">Next steps</span></span>

<span data-ttu-id="43efa-126">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="43efa-126">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="43efa-127">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="43efa-127">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
