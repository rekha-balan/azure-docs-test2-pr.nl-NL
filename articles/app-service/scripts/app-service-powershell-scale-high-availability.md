---
title: Azure PowerShell Script Sample - Scale a web app worldwide with a high-availability architecture | Microsoft Docs
description: Azure PowerShell Script Sample - Scale a web app worldwide with a high-availability architecture
services: app-service\web
documentationcenter: ''
author: syntaxc4
manager: erikre
editor: ''
tags: azure-service-management
ms.assetid: 470f0129-1efe-462c-a029-5c66e04158a8
ms.service: app-service
ms.devlang: multiple
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 92f830786f19190fc61479db42117c831bba007c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865423"
---
# <a name="scale-a-web-app-worldwide-with-a-high-availability-architecture"></a><span data-ttu-id="f4eac-103">Scale a web app worldwide with a high-availability architecture</span><span class="sxs-lookup"><span data-stu-id="f4eac-103">Scale a web app worldwide with a high-availability architecture</span></span>

<span data-ttu-id="f4eac-104">In this scenario you will create a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span><span class="sxs-lookup"><span data-stu-id="f4eac-104">In this scenario you will create a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="f4eac-105">Once the exercise is complete you will have a high-available architecture which allows provides global availability of your web app based on the lowest network latency.</span><span class="sxs-lookup"><span data-stu-id="f4eac-105">Once the exercise is complete you will have a high-available architecture which allows provides global availability of your web app based on the lowest network latency.</span></span>

<span data-ttu-id="f4eac-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Connect-AzureRmAccount` to create a connection with Azure.</span><span class="sxs-lookup"><span data-stu-id="f4eac-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Connect-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="f4eac-107">Sample script</span><span class="sxs-lookup"><span data-stu-id="f4eac-107">Sample script</span></span>

[!code-azurepowershell-interactive[main](../../../powershell_scripts/app-service/scale-geographic/scale-geographic.ps1 "Scale a web app worldwide with a high-availability architecture")]

## <a name="clean-up-deployment"></a><span data-ttu-id="f4eac-108">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="f4eac-108">Clean up deployment</span></span> 

<span data-ttu-id="f4eac-109">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="f4eac-109">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="f4eac-110">Script explanation</span><span class="sxs-lookup"><span data-stu-id="f4eac-110">Script explanation</span></span>

<span data-ttu-id="f4eac-111">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="f4eac-111">This script uses the following commands.</span></span> <span data-ttu-id="f4eac-112">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="f4eac-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="f4eac-113">Command</span><span class="sxs-lookup"><span data-stu-id="f4eac-113">Command</span></span> | <span data-ttu-id="f4eac-114">Notes</span><span class="sxs-lookup"><span data-stu-id="f4eac-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f4eac-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="f4eac-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="f4eac-116">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="f4eac-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="f4eac-117">New-AzureRMTrafficManagerProfile</span><span class="sxs-lookup"><span data-stu-id="f4eac-117">New-AzureRMTrafficManagerProfile</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerprofile) | <span data-ttu-id="f4eac-118">Creates a Traffic Manager profile.</span><span class="sxs-lookup"><span data-stu-id="f4eac-118">Creates a Traffic Manager profile.</span></span> |
| [<span data-ttu-id="f4eac-119">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="f4eac-119">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="f4eac-120">Creates an App Service plan.</span><span class="sxs-lookup"><span data-stu-id="f4eac-120">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="f4eac-121">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="f4eac-121">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="f4eac-122">Creates a web app.</span><span class="sxs-lookup"><span data-stu-id="f4eac-122">Creates a web app.</span></span> |
| [<span data-ttu-id="f4eac-123">New-AzureRMTrafficManagerEndpoint</span><span class="sxs-lookup"><span data-stu-id="f4eac-123">New-AzureRMTrafficManagerEndpoint</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerendpoint) | <span data-ttu-id="f4eac-124">Creates an endpoint in a Traffic Manager profile.</span><span class="sxs-lookup"><span data-stu-id="f4eac-124">Creates an endpoint in a Traffic Manager profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f4eac-125">Next steps</span><span class="sxs-lookup"><span data-stu-id="f4eac-125">Next steps</span></span>

<span data-ttu-id="f4eac-126">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f4eac-126">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="f4eac-127">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="f4eac-127">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
