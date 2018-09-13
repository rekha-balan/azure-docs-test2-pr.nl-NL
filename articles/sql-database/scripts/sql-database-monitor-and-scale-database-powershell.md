---
title: Azure PowerShell Script-Monitor & scale a single SQL database | Microsoft Docs
description: Azure PowerShell Script Sample - Monitor and scale a single SQL database using PowerShell
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
ms.openlocfilehash: 6dcf44e7ce623da3a0ff4cb009154198eea7a7d4
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549740"
---
# <a name="monitor-and-scale-a-single-sql-database-using-powershell"></a><span data-ttu-id="88be2-103">Monitor and scale a single SQL database using PowerShell</span><span class="sxs-lookup"><span data-stu-id="88be2-103">Monitor and scale a single SQL database using PowerShell</span></span>

<span data-ttu-id="88be2-104">This sample PowerShell script monitors the performance metrics of a database, scales it to a higher performance level, and creates an alert rule on one of the performance metrics.</span><span class="sxs-lookup"><span data-stu-id="88be2-104">This sample PowerShell script monitors the performance metrics of a database, scales it to a higher performance level, and creates an alert rule on one of the performance metrics.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="88be2-105">Sample script</span><span class="sxs-lookup"><span data-stu-id="88be2-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/monitor-and-scale-database/monitor-and-scale-database.ps1 "Monitor and scale single SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="88be2-106">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="88be2-106">Clean up deployment</span></span>

<span data-ttu-id="88be2-107">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span><span class="sxs-lookup"><span data-stu-id="88be2-107">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="88be2-108">Script explanation</span><span class="sxs-lookup"><span data-stu-id="88be2-108">Script explanation</span></span>

<span data-ttu-id="88be2-109">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="88be2-109">This script uses the following commands.</span></span> <span data-ttu-id="88be2-110">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="88be2-110">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="88be2-111">Command</span><span class="sxs-lookup"><span data-stu-id="88be2-111">Command</span></span> | <span data-ttu-id="88be2-112">Notes</span><span class="sxs-lookup"><span data-stu-id="88be2-112">Notes</span></span> |
|---|---|
 [<span data-ttu-id="88be2-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="88be2-113">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="88be2-114">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="88be2-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="88be2-115">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="88be2-115">New-AzureRmSqlServer</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.5.0/new-azurermsqlserver) | <span data-ttu-id="88be2-116">Creates a logical server that hosts a database or elastic pool.</span><span class="sxs-lookup"><span data-stu-id="88be2-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="88be2-117">Get-AzureRmMetric</span><span class="sxs-lookup"><span data-stu-id="88be2-117">Get-AzureRmMetric</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.insights/v2.5.0/get-azurermmetric) | <span data-ttu-id="88be2-118">Shows the size usage information for the database.</span><span class="sxs-lookup"><span data-stu-id="88be2-118">Shows the size usage information for the database.</span></span>|
| [<span data-ttu-id="88be2-119">Set-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="88be2-119">Set-AzureRmSqlDatabase</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.5.0/set-azurermsqldatabase) | <span data-ttu-id="88be2-120">Updates database properties or moves a database into, out of, or between elastic pools.</span><span class="sxs-lookup"><span data-stu-id="88be2-120">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="88be2-121">Add-AzureRMMetricAlertRule</span><span class="sxs-lookup"><span data-stu-id="88be2-121">Add-AzureRMMetricAlertRule</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.insights/v2.5.0/add-azurermmetricalertrule) | <span data-ttu-id="88be2-122">Sets an alert rule to automatically monitor DTUs in the future.</span><span class="sxs-lookup"><span data-stu-id="88be2-122">Sets an alert rule to automatically monitor DTUs in the future.</span></span> |
| [<span data-ttu-id="88be2-123">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="88be2-123">Remove-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/remove-azurermresourcegroup) | <span data-ttu-id="88be2-124">Deletes a resource group including all nested resources.</span><span class="sxs-lookup"><span data-stu-id="88be2-124">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="88be2-125">Next steps</span><span class="sxs-lookup"><span data-stu-id="88be2-125">Next steps</span></span>

<span data-ttu-id="88be2-126">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span><span class="sxs-lookup"><span data-stu-id="88be2-126">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="88be2-127">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="88be2-127">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
