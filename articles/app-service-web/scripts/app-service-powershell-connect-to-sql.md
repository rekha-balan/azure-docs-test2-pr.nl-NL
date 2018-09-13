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
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.openlocfilehash: f42112b7a97f2ddcb678ba32deca710d9dc66851
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662431"
---
# <a name="connect-a-web-app-to-a-sql-database"></a><span data-ttu-id="06a21-103">Connect a web app to a SQL database</span><span class="sxs-lookup"><span data-stu-id="06a21-103">Connect a web app to a SQL database</span></span>

<span data-ttu-id="06a21-104">In this scenario you will learn how to create an Azure SQL database and an Azure web app.</span><span class="sxs-lookup"><span data-stu-id="06a21-104">In this scenario you will learn how to create an Azure SQL database and an Azure web app.</span></span> <span data-ttu-id="06a21-105">Then you will link the SQL database to the web app using app settings.</span><span class="sxs-lookup"><span data-stu-id="06a21-105">Then you will link the SQL database to the web app using app settings.</span></span>

<span data-ttu-id="06a21-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` to create a connection with Azure.</span><span class="sxs-lookup"><span data-stu-id="06a21-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="06a21-107">Sample script</span><span class="sxs-lookup"><span data-stu-id="06a21-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/connect-to-sql/connect-to-sql.ps1?highlight=13 "Connect a web app to a SQL database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="06a21-108">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="06a21-108">Clean up deployment</span></span> 

<span data-ttu-id="06a21-109">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="06a21-109">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="06a21-110">Script explanation</span><span class="sxs-lookup"><span data-stu-id="06a21-110">Script explanation</span></span>

<span data-ttu-id="06a21-111">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="06a21-111">This script uses the following commands.</span></span> <span data-ttu-id="06a21-112">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="06a21-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="06a21-113">Command</span><span class="sxs-lookup"><span data-stu-id="06a21-113">Command</span></span> | <span data-ttu-id="06a21-114">Notes</span><span class="sxs-lookup"><span data-stu-id="06a21-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="06a21-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="06a21-115">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="06a21-116">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="06a21-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="06a21-117">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="06a21-117">New-AzureRmAppServicePlan</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.websites/v2.5.0/new-azurermappserviceplan) | <span data-ttu-id="06a21-118">Creates an App Service plan.</span><span class="sxs-lookup"><span data-stu-id="06a21-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="06a21-119">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="06a21-119">New-AzureRmWebApp</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.websites/v2.5.0/new-azurermwebapp) | <span data-ttu-id="06a21-120">Creates a web app.</span><span class="sxs-lookup"><span data-stu-id="06a21-120">Creates a web app.</span></span> |
| [<span data-ttu-id="06a21-121">New-AzureRMSQLServer</span><span class="sxs-lookup"><span data-stu-id="06a21-121">New-AzureRMSQLServer</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.5.0/new-azurermsqlserver) | <span data-ttu-id="06a21-122">Creates a SQL Database server.</span><span class="sxs-lookup"><span data-stu-id="06a21-122">Creates a SQL Database server.</span></span> |
| [<span data-ttu-id="06a21-123">New-AzureRmSqlServerFirewallRule</span><span class="sxs-lookup"><span data-stu-id="06a21-123">New-AzureRmSqlServerFirewallRule</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.5.0/new-azurermsqlserverfirewallrule) | <span data-ttu-id="06a21-124">Creates a firewall rule for a SQL Database server.</span><span class="sxs-lookup"><span data-stu-id="06a21-124">Creates a firewall rule for a SQL Database server.</span></span> |
| [<span data-ttu-id="06a21-125">New-AzureRMSQLDatabase</span><span class="sxs-lookup"><span data-stu-id="06a21-125">New-AzureRMSQLDatabase</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.5.0/new-azurermsqldatabase) | <span data-ttu-id="06a21-126">Creates a database or an elastic database.</span><span class="sxs-lookup"><span data-stu-id="06a21-126">Creates a database or an elastic database.</span></span> |
| [<span data-ttu-id="06a21-127">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="06a21-127">Set-AzureRmWebApp</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.websites/v2.5.0/set-azurermwebapp) | <span data-ttu-id="06a21-128">Modifies a web app's configuration.</span><span class="sxs-lookup"><span data-stu-id="06a21-128">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="06a21-129">Next steps</span><span class="sxs-lookup"><span data-stu-id="06a21-129">Next steps</span></span>

<span data-ttu-id="06a21-130">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/).</span><span class="sxs-lookup"><span data-stu-id="06a21-130">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/).</span></span>

<span data-ttu-id="06a21-131">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="06a21-131">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
