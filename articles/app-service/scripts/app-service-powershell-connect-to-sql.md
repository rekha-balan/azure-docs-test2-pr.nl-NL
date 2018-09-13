---
title: Azure PowerShell Script Sample - Connect a web app to a SQL database | Microsoft Docs
description: Azure PowerShell Script Sample - Connect a web app to a SQL database
services: app-service\web
documentationcenter: ''
author: syntaxc4
manager: erikre
editor: ''
tags: azure-service-management
ms.assetid: 055440a9-fff1-49b2-b964-9c95b364e533
ms.service: app-service
ms.devlang: multiple
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: be9a1f138ce858465ba8ded85365043cd823dac1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965905"
---
# <a name="connect-a-web-app-to-a-sql-database"></a><span data-ttu-id="21fab-103">Connect a web app to a SQL database</span><span class="sxs-lookup"><span data-stu-id="21fab-103">Connect a web app to a SQL database</span></span>

<span data-ttu-id="21fab-104">In this scenario you will learn how to create an Azure SQL database and an Azure web app.</span><span class="sxs-lookup"><span data-stu-id="21fab-104">In this scenario you will learn how to create an Azure SQL database and an Azure web app.</span></span> <span data-ttu-id="21fab-105">Then you will link the SQL database to the web app using app settings.</span><span class="sxs-lookup"><span data-stu-id="21fab-105">Then you will link the SQL database to the web app using app settings.</span></span>

<span data-ttu-id="21fab-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Connect-AzureRmAccount` to create a connection with Azure.</span><span class="sxs-lookup"><span data-stu-id="21fab-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Connect-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="21fab-107">Sample script</span><span class="sxs-lookup"><span data-stu-id="21fab-107">Sample script</span></span>

[!code-azurepowershell-interactive[main](../../../powershell_scripts/app-service/connect-to-sql/connect-to-sql.ps1?highlight=13 "Connect a web app to a SQL database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="21fab-108">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="21fab-108">Clean up deployment</span></span> 

<span data-ttu-id="21fab-109">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="21fab-109">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="21fab-110">Script explanation</span><span class="sxs-lookup"><span data-stu-id="21fab-110">Script explanation</span></span>

<span data-ttu-id="21fab-111">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="21fab-111">This script uses the following commands.</span></span> <span data-ttu-id="21fab-112">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="21fab-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="21fab-113">Command</span><span class="sxs-lookup"><span data-stu-id="21fab-113">Command</span></span> | <span data-ttu-id="21fab-114">Notes</span><span class="sxs-lookup"><span data-stu-id="21fab-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="21fab-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="21fab-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="21fab-116">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="21fab-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="21fab-117">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="21fab-117">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="21fab-118">Creates an App Service plan.</span><span class="sxs-lookup"><span data-stu-id="21fab-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="21fab-119">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="21fab-119">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="21fab-120">Creates a web app.</span><span class="sxs-lookup"><span data-stu-id="21fab-120">Creates a web app.</span></span> |
| [<span data-ttu-id="21fab-121">New-AzureRMSQLServer</span><span class="sxs-lookup"><span data-stu-id="21fab-121">New-AzureRMSQLServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="21fab-122">Creates a SQL Database server.</span><span class="sxs-lookup"><span data-stu-id="21fab-122">Creates a SQL Database server.</span></span> |
| [<span data-ttu-id="21fab-123">New-AzureRmSqlServerFirewallRule</span><span class="sxs-lookup"><span data-stu-id="21fab-123">New-AzureRmSqlServerFirewallRule</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) | <span data-ttu-id="21fab-124">Creates a firewall rule for a SQL Database server.</span><span class="sxs-lookup"><span data-stu-id="21fab-124">Creates a firewall rule for a SQL Database server.</span></span> |
| [<span data-ttu-id="21fab-125">New-AzureRMSQLDatabase</span><span class="sxs-lookup"><span data-stu-id="21fab-125">New-AzureRMSQLDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="21fab-126">Creates a database or an elastic database.</span><span class="sxs-lookup"><span data-stu-id="21fab-126">Creates a database or an elastic database.</span></span> |
| [<span data-ttu-id="21fab-127">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="21fab-127">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="21fab-128">Modifies a web app's configuration.</span><span class="sxs-lookup"><span data-stu-id="21fab-128">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="21fab-129">Next steps</span><span class="sxs-lookup"><span data-stu-id="21fab-129">Next steps</span></span>

<span data-ttu-id="21fab-130">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="21fab-130">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="21fab-131">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="21fab-131">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
