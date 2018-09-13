---
title: Azure PowerShell Script Sample - Monitor a web app with web server logs | Microsoft Docs
description: Azure PowerShell Script Sample - Monitor a web app with web server logs
services: app-service\web
documentationcenter: ''
author: syntaxc4
manager: erikre
editor: ''
tags: azure-service-management
ms.assetid: 5805d7cd-9e56-4eba-bd85-75b013690ff5
ms.service: app-service
ms.devlang: multiple
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 6d4b8c1874dc46552cefc4d984951c7a3a1b9f3b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864484"
---
# <a name="monitor-a-web-app-with-web-server-logs"></a><span data-ttu-id="30ea1-103">Monitor a web app with web server logs</span><span class="sxs-lookup"><span data-stu-id="30ea1-103">Monitor a web app with web server logs</span></span>

<span data-ttu-id="30ea1-104">In this scenario you will create a resource group, app service plan, web app and configure the web app to enable web server logs.</span><span class="sxs-lookup"><span data-stu-id="30ea1-104">In this scenario you will create a resource group, app service plan, web app and configure the web app to enable web server logs.</span></span> <span data-ttu-id="30ea1-105">You will then download the log files for review.</span><span class="sxs-lookup"><span data-stu-id="30ea1-105">You will then download the log files for review.</span></span>

<span data-ttu-id="30ea1-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Connect-AzureRmAccount` to create a connection with Azure.</span><span class="sxs-lookup"><span data-stu-id="30ea1-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Connect-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="30ea1-107">Sample script</span><span class="sxs-lookup"><span data-stu-id="30ea1-107">Sample script</span></span>

[!code-azurepowershell-interactive[main](../../../powershell_scripts/app-service/monitor-with-logs/monitor-with-logs.ps1 "Monitor a web app with web server logs")]

## <a name="clean-up-deployment"></a><span data-ttu-id="30ea1-108">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="30ea1-108">Clean up deployment</span></span> 

<span data-ttu-id="30ea1-109">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="30ea1-109">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="30ea1-110">Script explanation</span><span class="sxs-lookup"><span data-stu-id="30ea1-110">Script explanation</span></span>

<span data-ttu-id="30ea1-111">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="30ea1-111">This script uses the following commands.</span></span> <span data-ttu-id="30ea1-112">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="30ea1-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="30ea1-113">Command</span><span class="sxs-lookup"><span data-stu-id="30ea1-113">Command</span></span> | <span data-ttu-id="30ea1-114">Notes</span><span class="sxs-lookup"><span data-stu-id="30ea1-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="30ea1-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="30ea1-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="30ea1-116">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="30ea1-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="30ea1-117">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="30ea1-117">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="30ea1-118">Creates an App Service plan.</span><span class="sxs-lookup"><span data-stu-id="30ea1-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="30ea1-119">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="30ea1-119">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="30ea1-120">Creates a web app.</span><span class="sxs-lookup"><span data-stu-id="30ea1-120">Creates a web app.</span></span> |
| [<span data-ttu-id="30ea1-121">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="30ea1-121">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="30ea1-122">Modifies a web app's configuration.</span><span class="sxs-lookup"><span data-stu-id="30ea1-122">Modifies a web app's configuration.</span></span> |
| [<span data-ttu-id="30ea1-123">Get-AzureRMWebAppMetrics</span><span class="sxs-lookup"><span data-stu-id="30ea1-123">Get-AzureRMWebAppMetrics</span></span>](/powershell/module/azurerm.websites/get-azurermwebappmetrics) | <span data-ttu-id="30ea1-124">Gets a web app's metrics.</span><span class="sxs-lookup"><span data-stu-id="30ea1-124">Gets a web app's metrics.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="30ea1-125">Next steps</span><span class="sxs-lookup"><span data-stu-id="30ea1-125">Next steps</span></span>

<span data-ttu-id="30ea1-126">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="30ea1-126">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="30ea1-127">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="30ea1-127">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
