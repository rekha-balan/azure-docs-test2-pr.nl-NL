---
title: Azure PowerShell Script Sample - Scale a web app manually | Microsoft Docs
description: Azure PowerShell Script Sample - Scale a web app manually
services: app-service\web
documentationcenter: ''
author: syntaxc4
manager: erikre
editor: ''
tags: azure-service-management
ms.assetid: de5d4285-9c7d-4735-a695-288264047375
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.openlocfilehash: 7eb6698b6dab3714bfa7844b7d7a29f9755c2f35
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552958"
---
# <a name="scale-a-web-app-manually"></a><span data-ttu-id="9b032-103">Scale a web app manually</span><span class="sxs-lookup"><span data-stu-id="9b032-103">Scale a web app manually</span></span>

<span data-ttu-id="9b032-104">In this scenario you will learn to create a resource group, app service plan and web app.</span><span class="sxs-lookup"><span data-stu-id="9b032-104">In this scenario you will learn to create a resource group, app service plan and web app.</span></span> <span data-ttu-id="9b032-105">You will then scale the App Service Plan from a single instance to multiple instances.</span><span class="sxs-lookup"><span data-stu-id="9b032-105">You will then scale the App Service Plan from a single instance to multiple instances.</span></span>

<span data-ttu-id="9b032-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` to create a connection with Azure.</span><span class="sxs-lookup"><span data-stu-id="9b032-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="9b032-107">Sample script</span><span class="sxs-lookup"><span data-stu-id="9b032-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/scale-manual/scale-manual.ps1 "Scale a web app manually")]

## <a name="clean-up-deployment"></a><span data-ttu-id="9b032-108">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="9b032-108">Clean up deployment</span></span> 

<span data-ttu-id="9b032-109">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="9b032-109">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="9b032-110">Script explanation</span><span class="sxs-lookup"><span data-stu-id="9b032-110">Script explanation</span></span>

<span data-ttu-id="9b032-111">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="9b032-111">This script uses the following commands.</span></span> <span data-ttu-id="9b032-112">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="9b032-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="9b032-113">Command</span><span class="sxs-lookup"><span data-stu-id="9b032-113">Command</span></span> | <span data-ttu-id="9b032-114">Notes</span><span class="sxs-lookup"><span data-stu-id="9b032-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="9b032-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="9b032-115">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="9b032-116">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="9b032-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="9b032-117">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="9b032-117">New-AzureRmAppServicePlan</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.websites/v2.5.0/new-azurermappserviceplan) | <span data-ttu-id="9b032-118">Creates an App Service plan.</span><span class="sxs-lookup"><span data-stu-id="9b032-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="9b032-119">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="9b032-119">New-AzureRmWebApp</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.websites/v2.5.0/new-azurermwebapp) | <span data-ttu-id="9b032-120">Creates a web app.</span><span class="sxs-lookup"><span data-stu-id="9b032-120">Creates a web app.</span></span> |
| [<span data-ttu-id="9b032-121">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="9b032-121">Set-AzureRmWebApp</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.websites/v2.5.0/set-azurermwebapp) | <span data-ttu-id="9b032-122">Modifies a web app's configuration.</span><span class="sxs-lookup"><span data-stu-id="9b032-122">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9b032-123">Next steps</span><span class="sxs-lookup"><span data-stu-id="9b032-123">Next steps</span></span>

<span data-ttu-id="9b032-124">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/).</span><span class="sxs-lookup"><span data-stu-id="9b032-124">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/).</span></span>

<span data-ttu-id="9b032-125">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="9b032-125">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
