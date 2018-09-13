---
title: Azure PowerShell Script-Monitor & scale SQL elastic pool | Microsoft Docs
description: Azure PowerShell Script Sample - Monitor and scale a SQL Database elastic pool using PowerShell
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: ''
ms.service: sql-database
ms.custom: sample
ms.devlang: PowerShell
ms.topic: article
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 03/07/2017
ms.author: janeng
ms.openlocfilehash: 5ccf9f3c4e7851fadfb052f34c0d217a00e534f9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554156"
---
# <a name="monitor-and-scale-a-sql-database-elastic-pool-using-powershell"></a><span data-ttu-id="1fc65-103">Monitor and scale a SQL Database elastic pool using PowerShell</span><span class="sxs-lookup"><span data-stu-id="1fc65-103">Monitor and scale a SQL Database elastic pool using PowerShell</span></span>

<span data-ttu-id="1fc65-104">This sample PowerShell script monitors the performance metrics of an elastic pool, scales it to a higher performance level, and creates an alert rule on one of the performance metrics.</span><span class="sxs-lookup"><span data-stu-id="1fc65-104">This sample PowerShell script monitors the performance metrics of an elastic pool, scales it to a higher performance level, and creates an alert rule on one of the performance metrics.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="1fc65-105">Sample script</span><span class="sxs-lookup"><span data-stu-id="1fc65-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/monitor-and-scale-pool/monitor-and-scale-pool.ps1 "Monitor and scale single SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="1fc65-106">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="1fc65-106">Clean up deployment</span></span>

<span data-ttu-id="1fc65-107">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span><span class="sxs-lookup"><span data-stu-id="1fc65-107">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="1fc65-108">Script explanation</span><span class="sxs-lookup"><span data-stu-id="1fc65-108">Script explanation</span></span>

<span data-ttu-id="1fc65-109">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="1fc65-109">This script uses the following commands.</span></span> <span data-ttu-id="1fc65-110">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="1fc65-110">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="1fc65-111">Command</span><span class="sxs-lookup"><span data-stu-id="1fc65-111">Command</span></span> | <span data-ttu-id="1fc65-112">Notes</span><span class="sxs-lookup"><span data-stu-id="1fc65-112">Notes</span></span> |
|---|---|
 [<span data-ttu-id="1fc65-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="1fc65-113">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="1fc65-114">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="1fc65-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="1fc65-115">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="1fc65-115">New-AzureRmSqlServer</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.5.0/new-azurermsqlserver) | <span data-ttu-id="1fc65-116">Creates a logical server that hosts a database or elastic pool.</span><span class="sxs-lookup"><span data-stu-id="1fc65-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="1fc65-117">New-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="1fc65-117">New-AzureRmSqlElasticPool</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.5.0/new-azurermsqlelasticpool) | <span data-ttu-id="1fc65-118">Creates an elastic pool within a logical server.</span><span class="sxs-lookup"><span data-stu-id="1fc65-118">Creates an elastic pool within a logical server.</span></span> |
| [<span data-ttu-id="1fc65-119">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="1fc65-119">New-AzureRmSqlDatabase</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.5.0/new-azurermsqldatabase) | <span data-ttu-id="1fc65-120">Creates a database in a logical server as a single or a pooled database.</span><span class="sxs-lookup"><span data-stu-id="1fc65-120">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="1fc65-121">Get-AzureRmMetric</span><span class="sxs-lookup"><span data-stu-id="1fc65-121">Get-AzureRmMetric</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.insights/v2.5.0/get-azurermmetric) | <span data-ttu-id="1fc65-122">Shows the size usage information for the database.</span><span class="sxs-lookup"><span data-stu-id="1fc65-122">Shows the size usage information for the database.</span></span>|
| [<span data-ttu-id="1fc65-123">Add-AzureRMMetricAlertRule</span><span class="sxs-lookup"><span data-stu-id="1fc65-123">Add-AzureRMMetricAlertRule</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.insights/v2.5.0/add-azurermmetricalertrule) | <span data-ttu-id="1fc65-124">Adds or updates a metric-based alert rule.</span><span class="sxs-lookup"><span data-stu-id="1fc65-124">Adds or updates a metric-based alert rule.</span></span> |
| [<span data-ttu-id="1fc65-125">Set-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="1fc65-125">Set-AzureRmSqlElasticPool</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.5.0/set-azurermsqlelasticpool) | <span data-ttu-id="1fc65-126">Updates elastic pool properties</span><span class="sxs-lookup"><span data-stu-id="1fc65-126">Updates elastic pool properties</span></span> |
| [<span data-ttu-id="1fc65-127">Add-AzureRMMetricAlertRule</span><span class="sxs-lookup"><span data-stu-id="1fc65-127">Add-AzureRMMetricAlertRule</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.insights/v2.5.0/add-azurermmetricalertrule) | <span data-ttu-id="1fc65-128">Sets an alert rule to automatically monitor DTUs in the future.</span><span class="sxs-lookup"><span data-stu-id="1fc65-128">Sets an alert rule to automatically monitor DTUs in the future.</span></span> |
| [<span data-ttu-id="1fc65-129">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="1fc65-129">Remove-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/remove-azurermresourcegroup) | <span data-ttu-id="1fc65-130">Deletes a resource group including all nested resources.</span><span class="sxs-lookup"><span data-stu-id="1fc65-130">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="1fc65-131">Next steps</span><span class="sxs-lookup"><span data-stu-id="1fc65-131">Next steps</span></span>

<span data-ttu-id="1fc65-132">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span><span class="sxs-lookup"><span data-stu-id="1fc65-132">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="1fc65-133">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="1fc65-133">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
