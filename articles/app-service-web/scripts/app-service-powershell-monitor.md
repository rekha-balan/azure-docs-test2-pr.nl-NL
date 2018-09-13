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
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.openlocfilehash: c4a11079b04e53ab688189e79fe2e19fd9dfb071
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556171"
---
# <a name="monitor-a-web-app-with-web-server-logs"></a><span data-ttu-id="61c93-103">Monitor a web app with web server logs</span><span class="sxs-lookup"><span data-stu-id="61c93-103">Monitor a web app with web server logs</span></span>

<span data-ttu-id="61c93-104">In this scenario you will create a resource group, app service plan, web app and configure the web app to enable web server logs.</span><span class="sxs-lookup"><span data-stu-id="61c93-104">In this scenario you will create a resource group, app service plan, web app and configure the web app to enable web server logs.</span></span> <span data-ttu-id="61c93-105">You will then download the log files for review.</span><span class="sxs-lookup"><span data-stu-id="61c93-105">You will then download the log files for review.</span></span>

<span data-ttu-id="61c93-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` to create a connection with Azure.</span><span class="sxs-lookup"><span data-stu-id="61c93-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="61c93-107">Sample script</span><span class="sxs-lookup"><span data-stu-id="61c93-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/monitor-with-logs/monitor-with-logs.ps1 "Monitor a web app with web server logs")]

## <a name="clean-up-deployment"></a><span data-ttu-id="61c93-108">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="61c93-108">Clean up deployment</span></span> 

<span data-ttu-id="61c93-109">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="61c93-109">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="61c93-110">Script explanation</span><span class="sxs-lookup"><span data-stu-id="61c93-110">Script explanation</span></span>

<span data-ttu-id="61c93-111">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="61c93-111">This script uses the following commands.</span></span> <span data-ttu-id="61c93-112">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="61c93-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="61c93-113">Command</span><span class="sxs-lookup"><span data-stu-id="61c93-113">Command</span></span> | <span data-ttu-id="61c93-114">Notes</span><span class="sxs-lookup"><span data-stu-id="61c93-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="61c93-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="61c93-115">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="61c93-116">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="61c93-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="61c93-117">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="61c93-117">New-AzureRmAppServicePlan</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.websites/v2.5.0/new-azurermappserviceplan) | <span data-ttu-id="61c93-118">Creates an App Service plan.</span><span class="sxs-lookup"><span data-stu-id="61c93-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="61c93-119">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="61c93-119">New-AzureRmWebApp</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.websites/v2.5.0/new-azurermwebapp) | <span data-ttu-id="61c93-120">Creates a web app.</span><span class="sxs-lookup"><span data-stu-id="61c93-120">Creates a web app.</span></span> |
| [<span data-ttu-id="61c93-121">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="61c93-121">Set-AzureRmWebApp</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.websites/v2.5.0/set-azurermwebapp) | <span data-ttu-id="61c93-122">Modifies a web app's configuration.</span><span class="sxs-lookup"><span data-stu-id="61c93-122">Modifies a web app's configuration.</span></span> |
| [<span data-ttu-id="61c93-123">Get-AzureRMWebAppMetrics</span><span class="sxs-lookup"><span data-stu-id="61c93-123">Get-AzureRMWebAppMetrics</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.websites/v2.5.0/get-azurermwebappmetrics) | <span data-ttu-id="61c93-124">Gets a web app's metrics.</span><span class="sxs-lookup"><span data-stu-id="61c93-124">Gets a web app's metrics.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="61c93-125">Next steps</span><span class="sxs-lookup"><span data-stu-id="61c93-125">Next steps</span></span>

<span data-ttu-id="61c93-126">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/).</span><span class="sxs-lookup"><span data-stu-id="61c93-126">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/).</span></span>

<span data-ttu-id="61c93-127">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="61c93-127">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
