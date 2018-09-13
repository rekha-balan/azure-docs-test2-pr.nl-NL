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
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.openlocfilehash: e64b4f3bfc16de82e0f9d900b2dcc4b0ca11e3cb
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549412"
---
# <a name="scale-a-web-app-worldwide-with-a-high-availability-architecture"></a><span data-ttu-id="8e435-103">Scale a web app worldwide with a high-availability architecture</span><span class="sxs-lookup"><span data-stu-id="8e435-103">Scale a web app worldwide with a high-availability architecture</span></span>

<span data-ttu-id="8e435-104">In this scenario you will create a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span><span class="sxs-lookup"><span data-stu-id="8e435-104">In this scenario you will create a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="8e435-105">Once the exercise is complete you will have a high-available architecture which allows provides global availability of your web app based on the lowest network latency.</span><span class="sxs-lookup"><span data-stu-id="8e435-105">Once the exercise is complete you will have a high-available architecture which allows provides global availability of your web app based on the lowest network latency.</span></span>

<span data-ttu-id="8e435-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` to create a connection with Azure.</span><span class="sxs-lookup"><span data-stu-id="8e435-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="8e435-107">Sample script</span><span class="sxs-lookup"><span data-stu-id="8e435-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/scale-geographic/scale-geographic.ps1 "Scale a web app worldwide with a high-availability architecture")]

## <a name="clean-up-deployment"></a><span data-ttu-id="8e435-108">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="8e435-108">Clean up deployment</span></span> 

<span data-ttu-id="8e435-109">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="8e435-109">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="8e435-110">Script explanation</span><span class="sxs-lookup"><span data-stu-id="8e435-110">Script explanation</span></span>

<span data-ttu-id="8e435-111">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="8e435-111">This script uses the following commands.</span></span> <span data-ttu-id="8e435-112">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="8e435-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="8e435-113">Command</span><span class="sxs-lookup"><span data-stu-id="8e435-113">Command</span></span> | <span data-ttu-id="8e435-114">Notes</span><span class="sxs-lookup"><span data-stu-id="8e435-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="8e435-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="8e435-115">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="8e435-116">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="8e435-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="8e435-117">New-AzureRMTrafficManagerProfile</span><span class="sxs-lookup"><span data-stu-id="8e435-117">New-AzureRMTrafficManagerProfile</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.trafficmanager/v2.5.0/new-azurermtrafficmanagerprofile) | <span data-ttu-id="8e435-118">Creates a Traffic Manager profile.</span><span class="sxs-lookup"><span data-stu-id="8e435-118">Creates a Traffic Manager profile.</span></span> |
| [<span data-ttu-id="8e435-119">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="8e435-119">New-AzureRmAppServicePlan</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.websites/v2.5.0/new-azurermappserviceplan) | <span data-ttu-id="8e435-120">Creates an App Service plan.</span><span class="sxs-lookup"><span data-stu-id="8e435-120">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="8e435-121">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="8e435-121">New-AzureRmWebApp</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.websites/v2.5.0/new-azurermwebapp) | <span data-ttu-id="8e435-122">Creates a web app.</span><span class="sxs-lookup"><span data-stu-id="8e435-122">Creates a web app.</span></span> |
| [<span data-ttu-id="8e435-123">New-AzureRMTrafficManagerEndpoint</span><span class="sxs-lookup"><span data-stu-id="8e435-123">New-AzureRMTrafficManagerEndpoint</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.trafficmanager/v2.5.0/new-azurermtrafficmanagerendpoint) | <span data-ttu-id="8e435-124">Creates an endpoint in a Traffic Manager profile.</span><span class="sxs-lookup"><span data-stu-id="8e435-124">Creates an endpoint in a Traffic Manager profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="8e435-125">Next steps</span><span class="sxs-lookup"><span data-stu-id="8e435-125">Next steps</span></span>

<span data-ttu-id="8e435-126">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/).</span><span class="sxs-lookup"><span data-stu-id="8e435-126">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/).</span></span>

<span data-ttu-id="8e435-127">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="8e435-127">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
