---
title: Azure PowerShell Script-Move a SQL database and elastic pools | Microsoft Docs
description: Azure PowerShell Script Sample - Move a SQL database between elastic pools using PowerShell
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
ms.openlocfilehash: 65017a5583e0709376d583871c7ed4eaf9a08d2e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564303"
---
# <a name="create-elastic-pools-and-move-databases-between-pools-and-out-of-a-pool-using-powershell"></a><span data-ttu-id="4c031-103">Create elastic pools and move databases between pools and out of a pool using PowerShell</span><span class="sxs-lookup"><span data-stu-id="4c031-103">Create elastic pools and move databases between pools and out of a pool using PowerShell</span></span>

<span data-ttu-id="4c031-104">This sample PowerShell script creates two elastic pools and moves a database from one elastic pool into another elastic pool, and then moves a database out of an elastic pool to a single database performance level.</span><span class="sxs-lookup"><span data-stu-id="4c031-104">This sample PowerShell script creates two elastic pools and moves a database from one elastic pool into another elastic pool, and then moves a database out of an elastic pool to a single database performance level.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="4c031-105">Sample script</span><span class="sxs-lookup"><span data-stu-id="4c031-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/move-database-between-pools-and-standalone/move-database-between-pools-and-standalone.ps1 "Move database between pools")]

## <a name="clean-up-deployment"></a><span data-ttu-id="4c031-106">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="4c031-106">Clean up deployment</span></span>

<span data-ttu-id="4c031-107">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span><span class="sxs-lookup"><span data-stu-id="4c031-107">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="4c031-108">Script explanation</span><span class="sxs-lookup"><span data-stu-id="4c031-108">Script explanation</span></span>

<span data-ttu-id="4c031-109">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="4c031-109">This script uses the following commands.</span></span> <span data-ttu-id="4c031-110">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="4c031-110">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="4c031-111">Command</span><span class="sxs-lookup"><span data-stu-id="4c031-111">Command</span></span> | <span data-ttu-id="4c031-112">Notes</span><span class="sxs-lookup"><span data-stu-id="4c031-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="4c031-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="4c031-113">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="4c031-114">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="4c031-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="4c031-115">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="4c031-115">New-AzureRmSqlServer</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.5.0/new-azurermsqlserver) | <span data-ttu-id="4c031-116">Creates a logical server that hosts a database or elastic pool.</span><span class="sxs-lookup"><span data-stu-id="4c031-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="4c031-117">New-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="4c031-117">New-AzureRmSqlElasticPool</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.5.0/new-azurermsqlelasticpool) | <span data-ttu-id="4c031-118">Creates an elastic pool within a logical server.</span><span class="sxs-lookup"><span data-stu-id="4c031-118">Creates an elastic pool within a logical server.</span></span> |
| [<span data-ttu-id="4c031-119">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="4c031-119">New-AzureRmSqlDatabase</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.5.0/new-azurermsqldatabase) | <span data-ttu-id="4c031-120">Creates a database in a logical server as a single or a pooled database.</span><span class="sxs-lookup"><span data-stu-id="4c031-120">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="4c031-121">Set-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="4c031-121">Set-AzureRmSqlDatabase</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.5.0/set-azurermsqldatabase) | <span data-ttu-id="4c031-122">Updates database properties or moves a database into, out of, or between elastic pools.</span><span class="sxs-lookup"><span data-stu-id="4c031-122">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="4c031-123">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="4c031-123">Remove-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/remove-azurermresourcegroup) | <span data-ttu-id="4c031-124">Deletes a resource group including all nested resources.</span><span class="sxs-lookup"><span data-stu-id="4c031-124">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="4c031-125">Next steps</span><span class="sxs-lookup"><span data-stu-id="4c031-125">Next steps</span></span>

<span data-ttu-id="4c031-126">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span><span class="sxs-lookup"><span data-stu-id="4c031-126">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="4c031-127">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="4c031-127">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
