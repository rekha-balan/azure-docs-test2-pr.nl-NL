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
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: bb4f4dbb0486687353f60667f158539df492dcf2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856997"
---
# <a name="scale-a-web-app-manually"></a><span data-ttu-id="1193e-103">Scale a web app manually</span><span class="sxs-lookup"><span data-stu-id="1193e-103">Scale a web app manually</span></span>

<span data-ttu-id="1193e-104">In this scenario you will learn to create a resource group, app service plan and web app.</span><span class="sxs-lookup"><span data-stu-id="1193e-104">In this scenario you will learn to create a resource group, app service plan and web app.</span></span> <span data-ttu-id="1193e-105">You will then scale the App Service Plan from a single instance to multiple instances.</span><span class="sxs-lookup"><span data-stu-id="1193e-105">You will then scale the App Service Plan from a single instance to multiple instances.</span></span>

<span data-ttu-id="1193e-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Connect-AzureRmAccount` to create a connection with Azure.</span><span class="sxs-lookup"><span data-stu-id="1193e-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Connect-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="1193e-107">Sample script</span><span class="sxs-lookup"><span data-stu-id="1193e-107">Sample script</span></span>

[!code-azurepowershell-interactive[main](../../../powershell_scripts/app-service/scale-manual/scale-manual.ps1 "Scale a web app manually")]

## <a name="clean-up-deployment"></a><span data-ttu-id="1193e-108">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="1193e-108">Clean up deployment</span></span> 

<span data-ttu-id="1193e-109">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="1193e-109">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="1193e-110">Script explanation</span><span class="sxs-lookup"><span data-stu-id="1193e-110">Script explanation</span></span>

<span data-ttu-id="1193e-111">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="1193e-111">This script uses the following commands.</span></span> <span data-ttu-id="1193e-112">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="1193e-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="1193e-113">Command</span><span class="sxs-lookup"><span data-stu-id="1193e-113">Command</span></span> | <span data-ttu-id="1193e-114">Notes</span><span class="sxs-lookup"><span data-stu-id="1193e-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="1193e-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="1193e-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="1193e-116">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="1193e-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="1193e-117">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="1193e-117">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="1193e-118">Creates an App Service plan.</span><span class="sxs-lookup"><span data-stu-id="1193e-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="1193e-119">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="1193e-119">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="1193e-120">Creates a web app.</span><span class="sxs-lookup"><span data-stu-id="1193e-120">Creates a web app.</span></span> |
| [<span data-ttu-id="1193e-121">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="1193e-121">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="1193e-122">Modifies a web app's configuration.</span><span class="sxs-lookup"><span data-stu-id="1193e-122">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="1193e-123">Next steps</span><span class="sxs-lookup"><span data-stu-id="1193e-123">Next steps</span></span>

<span data-ttu-id="1193e-124">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1193e-124">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="1193e-125">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="1193e-125">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
