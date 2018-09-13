---
title: PowerShell example-monitor-scale-single Azure SQL database | Microsoft Docs
description: Azure PowerShell example script to monitor and scale a single Azure SQL database
services: sql-database
documentationcenter: sql-database
author: CarlRabeler
manager: craigg
editor: carlrab
tags: azure-service-management
ms.assetid: ''
ms.service: sql-database
ms.custom: monitor & tune, mvc
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 09/07/2018
ms.author: carlrab
ms.openlocfilehash: 8766ffe34263b80a5f4c9023620a7e0fb9002ec7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44811693"
---
# <a name="use-powershell-to-monitor-and-scale-a-single-sql-database"></a><span data-ttu-id="8cb6d-103">Use PowerShell to monitor and scale a single SQL database</span><span class="sxs-lookup"><span data-stu-id="8cb6d-103">Use PowerShell to monitor and scale a single SQL database</span></span>

<span data-ttu-id="8cb6d-104">This PowerShell script example monitors the performance metrics of a database, scales it to a higher performance level, and creates an alert rule on one of the performance metrics.</span><span class="sxs-lookup"><span data-stu-id="8cb6d-104">This PowerShell script example monitors the performance metrics of a database, scales it to a higher performance level, and creates an alert rule on one of the performance metrics.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]
[!INCLUDE [cloud-shell-powershell.md](../../../includes/cloud-shell-powershell.md)]

<span data-ttu-id="8cb6d-105">If you choose to install and use the PowerShell locally, this tutorial requires the Azure PowerShell module version 5.7.0 or later.</span><span class="sxs-lookup"><span data-stu-id="8cb6d-105">If you choose to install and use the PowerShell locally, this tutorial requires the Azure PowerShell module version 5.7.0 or later.</span></span> <span data-ttu-id="8cb6d-106">Run `Get-Module -ListAvailable AzureRM` to find the version.</span><span class="sxs-lookup"><span data-stu-id="8cb6d-106">Run `Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="8cb6d-107">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="8cb6d-107">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span> <span data-ttu-id="8cb6d-108">If you are running PowerShell locally, you also need to run `Connect-AzureRmAccount` to create a connection with Azure.</span><span class="sxs-lookup"><span data-stu-id="8cb6d-108">If you are running PowerShell locally, you also need to run `Connect-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="8cb6d-109">Sample script</span><span class="sxs-lookup"><span data-stu-id="8cb6d-109">Sample script</span></span>

[!code-powershell-interactive[main](../../../powershell_scripts/sql-database/monitor-and-scale-database/monitor-and-scale-database.ps1?highlight=13-14 "Monitor and scale single SQL Database")]

> [!TIP]
> <span data-ttu-id="8cb6d-110">Use [Get-AzureRmSqlDatabaseActivity](/powershell/module/azurerm.sql/get-azurermsqldatabaseactivity) to get the status of database operations and use [Stop-AzureRmSqlDatabaseActivity](/powershell/module/azurerm.sql/stop-azurermsqldatabaseactivity) to cancels an update operation on the database.</span><span class="sxs-lookup"><span data-stu-id="8cb6d-110">Use [Get-AzureRmSqlDatabaseActivity](/powershell/module/azurerm.sql/get-azurermsqldatabaseactivity) to get the status of database operations and use [Stop-AzureRmSqlDatabaseActivity](/powershell/module/azurerm.sql/stop-azurermsqldatabaseactivity) to cancels an update operation on the database.</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="8cb6d-111">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="8cb6d-111">Clean up deployment</span></span>

<span data-ttu-id="8cb6d-112">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span><span class="sxs-lookup"><span data-stu-id="8cb6d-112">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName $resourcegroupname
```

## <a name="script-explanation"></a><span data-ttu-id="8cb6d-113">Script explanation</span><span class="sxs-lookup"><span data-stu-id="8cb6d-113">Script explanation</span></span>

<span data-ttu-id="8cb6d-114">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="8cb6d-114">This script uses the following commands.</span></span> <span data-ttu-id="8cb6d-115">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="8cb6d-115">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="8cb6d-116">Command</span><span class="sxs-lookup"><span data-stu-id="8cb6d-116">Command</span></span> | <span data-ttu-id="8cb6d-117">Notes</span><span class="sxs-lookup"><span data-stu-id="8cb6d-117">Notes</span></span> |
|---|---|
 [<span data-ttu-id="8cb6d-118">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="8cb6d-118">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="8cb6d-119">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="8cb6d-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="8cb6d-120">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="8cb6d-120">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="8cb6d-121">Creates a logical server that hosts a database or elastic pool.</span><span class="sxs-lookup"><span data-stu-id="8cb6d-121">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="8cb6d-122">Get-AzureRmMetric</span><span class="sxs-lookup"><span data-stu-id="8cb6d-122">Get-AzureRmMetric</span></span>](/powershell/module/azurerm.insights/get-azurermmetric) | <span data-ttu-id="8cb6d-123">Shows the size usage information for the database.</span><span class="sxs-lookup"><span data-stu-id="8cb6d-123">Shows the size usage information for the database.</span></span>|
| [<span data-ttu-id="8cb6d-124">Set-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="8cb6d-124">Set-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabase) | <span data-ttu-id="8cb6d-125">Updates database properties or moves a database into, out of, or between elastic pools.</span><span class="sxs-lookup"><span data-stu-id="8cb6d-125">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="8cb6d-126">Add-AzureRMMetricAlertRule</span><span class="sxs-lookup"><span data-stu-id="8cb6d-126">Add-AzureRMMetricAlertRule</span></span>](/powershell/module/azurerm.insights/add-azurermmetricalertrule) | <span data-ttu-id="8cb6d-127">Sets an alert rule to automatically monitor DTUs in the future.</span><span class="sxs-lookup"><span data-stu-id="8cb6d-127">Sets an alert rule to automatically monitor DTUs in the future.</span></span> |
| [<span data-ttu-id="8cb6d-128">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="8cb6d-128">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="8cb6d-129">Deletes a resource group including all nested resources.</span><span class="sxs-lookup"><span data-stu-id="8cb6d-129">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="8cb6d-130">Next steps</span><span class="sxs-lookup"><span data-stu-id="8cb6d-130">Next steps</span></span>

<span data-ttu-id="8cb6d-131">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8cb6d-131">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="8cb6d-132">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="8cb6d-132">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
