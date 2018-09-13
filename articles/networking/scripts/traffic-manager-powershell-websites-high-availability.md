---
title: Azure PowerShell Script Sample - Route traffic for high availability of applications | Microsoft Docs
description: Azure PowerShell Script Sample - Route traffic for high availability of applications
services: traffic-manager
documentationcenter: traffic-manager
author: KumudD
manager: timlt
editor: georgewallace
tags: azure-infrastructure
ms.assetid: ''
ms.service: traffic-manager
ms.devlang: powershell
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: traffic-manager
ms.date: 05/16/2017
ms.author: gwallace
ms.openlocfilehash: 24054625870cb073eec9769f50f370deb2828535
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867507"
---
# <a name="route-traffic-for-high-availability-of-applications"></a><span data-ttu-id="5048f-103">Route traffic for high availability of applications</span><span class="sxs-lookup"><span data-stu-id="5048f-103">Route traffic for high availability of applications</span></span>

<span data-ttu-id="5048f-104">This script creates a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span><span class="sxs-lookup"><span data-stu-id="5048f-104">This script creates a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="5048f-105">Traffic Manager directs traffic to the application in one region as the primary region, and to the secondary region when the application in the primary region is unavailable.</span><span class="sxs-lookup"><span data-stu-id="5048f-105">Traffic Manager directs traffic to the application in one region as the primary region, and to the secondary region when the application in the primary region is unavailable.</span></span> <span data-ttu-id="5048f-106">Before executing the script, you must change the MyWebApp, MyWebAppL1 and MyWebAppL2 values to unique values across Azure.</span><span class="sxs-lookup"><span data-stu-id="5048f-106">Before executing the script, you must change the MyWebApp, MyWebAppL1 and MyWebAppL2 values to unique values across Azure.</span></span> <span data-ttu-id="5048f-107">After running the script, you can access the app in the primary region with the URL mywebapp.trafficmanager.net.</span><span class="sxs-lookup"><span data-stu-id="5048f-107">After running the script, you can access the app in the primary region with the URL mywebapp.trafficmanager.net.</span></span>

<span data-ttu-id="5048f-108">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Connect-AzureRmAccount` to create a connection with Azure.</span><span class="sxs-lookup"><span data-stu-id="5048f-108">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Connect-AzureRmAccount` to create a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="5048f-109">Sample script</span><span class="sxs-lookup"><span data-stu-id="5048f-109">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/traffic-manager/direct-traffic-for-increased-application-availability/direct-traffic-for-increased-application-availability.ps1 "Route traffic for high availability")]


<span data-ttu-id="5048f-110">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="5048f-110">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup1
Remove-AzureRmResourceGroup -Name myResourceGroup2
```


## <a name="script-explanation"></a><span data-ttu-id="5048f-111">Script explanation</span><span class="sxs-lookup"><span data-stu-id="5048f-111">Script explanation</span></span>

<span data-ttu-id="5048f-112">This script uses the following commands to create a resource group, web app, traffic manager profile, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="5048f-112">This script uses the following commands to create a resource group, web app, traffic manager profile, and all related resources.</span></span> <span data-ttu-id="5048f-113">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="5048f-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="5048f-114">Command</span><span class="sxs-lookup"><span data-stu-id="5048f-114">Command</span></span> | <span data-ttu-id="5048f-115">Notes</span><span class="sxs-lookup"><span data-stu-id="5048f-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5048f-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="5048f-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup)  | <span data-ttu-id="5048f-117">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="5048f-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="5048f-118">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="5048f-118">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="5048f-119">Creates an App Service plan.</span><span class="sxs-lookup"><span data-stu-id="5048f-119">Creates an App Service plan.</span></span> <span data-ttu-id="5048f-120">This is like a server farm for your Azure web app.</span><span class="sxs-lookup"><span data-stu-id="5048f-120">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="5048f-121">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="5048f-121">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="5048f-122">Creates an Azure web app within the App Service plan.</span><span class="sxs-lookup"><span data-stu-id="5048f-122">Creates an Azure web app within the App Service plan.</span></span> |
| [<span data-ttu-id="5048f-123">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="5048f-123">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/new-azurermresource) | <span data-ttu-id="5048f-124">Creates an Azure web app within the App Service plan.</span><span class="sxs-lookup"><span data-stu-id="5048f-124">Creates an Azure web app within the App Service plan.</span></span> |
| [<span data-ttu-id="5048f-125">New-AzureRmTrafficManagerProfile</span><span class="sxs-lookup"><span data-stu-id="5048f-125">New-AzureRmTrafficManagerProfile</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerprofile) | <span data-ttu-id="5048f-126">Creates an Azure Traffic Manager profile.</span><span class="sxs-lookup"><span data-stu-id="5048f-126">Creates an Azure Traffic Manager profile.</span></span> |
| [<span data-ttu-id="5048f-127">New-AzureRmTrafficManagerEndpoint</span><span class="sxs-lookup"><span data-stu-id="5048f-127">New-AzureRmTrafficManagerEndpoint</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerendpoint) | <span data-ttu-id="5048f-128">Adds a endpoint to an Azure Traffic Manager Profile.</span><span class="sxs-lookup"><span data-stu-id="5048f-128">Adds a endpoint to an Azure Traffic Manager Profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5048f-129">Next steps</span><span class="sxs-lookup"><span data-stu-id="5048f-129">Next steps</span></span>

<span data-ttu-id="5048f-130">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5048f-130">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="5048f-131">Additional networking PowerShell script samples can be found in the [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5048f-131">Additional networking PowerShell script samples can be found in the [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
