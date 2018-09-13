---
title: Azure PowerShell Script-Set up geo-replication-pooled SQL database | Microsoft Docs
description: Azure PowerShell Script Sample - Set up Active Geo-Replication for a pooled Azure SQL database using PowerShell
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
ms.openlocfilehash: e6ca56cd89752ba12e377c0b6fe840e14c078fdd
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562868"
---
# <a name="configure-active-geo-replication-for-a-pooled-azure-sql-database-using-powershell"></a><span data-ttu-id="d1f90-103">Configure Active Geo-Replication for a pooled Azure SQL database using PowerShell</span><span class="sxs-lookup"><span data-stu-id="d1f90-103">Configure Active Geo-Replication for a pooled Azure SQL database using PowerShell</span></span>

<span data-ttu-id="d1f90-104">This sample PowerShell script configures Active Geo-Replication for a database in an elastic pool and fails it over to the secondary replica.</span><span class="sxs-lookup"><span data-stu-id="d1f90-104">This sample PowerShell script configures Active Geo-Replication for a database in an elastic pool and fails it over to the secondary replica.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-scripts"></a><span data-ttu-id="d1f90-105">Sample Scripts</span><span class="sxs-lookup"><span data-stu-id="d1f90-105">Sample Scripts</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/setup-geodr-and-failover-pool/setup-geodr-and-failover-pool.ps1 "Set up Active Geo-Replication for elastic pool")]

## <a name="clean-up-deployment"></a><span data-ttu-id="d1f90-106">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="d1f90-106">Clean up deployment</span></span>

<span data-ttu-id="d1f90-107">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span><span class="sxs-lookup"><span data-stu-id="d1f90-107">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myPrimaryResourceGroup"
Remove-AzureRmResourceGroup -ResourceGroupName "mySecondaryResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="d1f90-108">Script explanation</span><span class="sxs-lookup"><span data-stu-id="d1f90-108">Script explanation</span></span>

<span data-ttu-id="d1f90-109">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="d1f90-109">This script uses the following commands.</span></span> <span data-ttu-id="d1f90-110">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="d1f90-110">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="d1f90-111">Command</span><span class="sxs-lookup"><span data-stu-id="d1f90-111">Command</span></span> | <span data-ttu-id="d1f90-112">Notes</span><span class="sxs-lookup"><span data-stu-id="d1f90-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d1f90-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="d1f90-113">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="d1f90-114">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="d1f90-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="d1f90-115">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="d1f90-115">New-AzureRmSqlServer</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.5.0/new-azurermsqlserver) | <span data-ttu-id="d1f90-116">Creates a logical server that hosts a database or elastic pool.</span><span class="sxs-lookup"><span data-stu-id="d1f90-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="d1f90-117">New-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="d1f90-117">New-AzureRmSqlElasticPool</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.5.0/new-azurermsqlelasticpool) | <span data-ttu-id="d1f90-118">Creates an elastic pool within a logical server.</span><span class="sxs-lookup"><span data-stu-id="d1f90-118">Creates an elastic pool within a logical server.</span></span> |
| [<span data-ttu-id="d1f90-119">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="d1f90-119">New-AzureRmSqlDatabase</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.5.0/new-azurermsqldatabase) | <span data-ttu-id="d1f90-120">Creates a database in a logical server as a single or a pooled database.</span><span class="sxs-lookup"><span data-stu-id="d1f90-120">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="d1f90-121">Set-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="d1f90-121">Set-AzureRmSqlDatabase</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.5.0/set-azurermsqldatabase) | <span data-ttu-id="d1f90-122">Updates database properties or moves a database into, out of, or between elastic pools.</span><span class="sxs-lookup"><span data-stu-id="d1f90-122">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="d1f90-123">New-AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="d1f90-123">New-AzureRmSqlDatabaseSecondary</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.5.0/new-azurermsqldatabasesecondary)| <span data-ttu-id="d1f90-124">Creates a secondary database for an existing database and starts data replication.</span><span class="sxs-lookup"><span data-stu-id="d1f90-124">Creates a secondary database for an existing database and starts data replication.</span></span> |
| [<span data-ttu-id="d1f90-125">Get-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="d1f90-125">Get-AzureRmSqlDatabase</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.5.0/get-azurermsqldatabase)| <span data-ttu-id="d1f90-126">Gets one or more databases.</span><span class="sxs-lookup"><span data-stu-id="d1f90-126">Gets one or more databases.</span></span> |
| [<span data-ttu-id="d1f90-127">Set-AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="d1f90-127">Set-AzureRmSqlDatabaseSecondary</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.5.0/set-azurermsqldatabasesecondary)| <span data-ttu-id="d1f90-128">Switches a secondary database to be primary in order to initiate failover.</span><span class="sxs-lookup"><span data-stu-id="d1f90-128">Switches a secondary database to be primary in order to initiate failover.</span></span>|
| [<span data-ttu-id="d1f90-129">Get-AzureRmSqlDatabaseReplicationLink</span><span class="sxs-lookup"><span data-stu-id="d1f90-129">Get-AzureRmSqlDatabaseReplicationLink</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.5.0/get-azurermsqldatabasereplicationlink) | <span data-ttu-id="d1f90-130">Gets the geo-replication links between an Azure SQL Database and a resource group or SQL Server.</span><span class="sxs-lookup"><span data-stu-id="d1f90-130">Gets the geo-replication links between an Azure SQL Database and a resource group or SQL Server.</span></span> |
| [<span data-ttu-id="d1f90-131">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="d1f90-131">Remove-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/remove-azurermresourcegroup) | <span data-ttu-id="d1f90-132">Deletes a resource group including all nested resources.</span><span class="sxs-lookup"><span data-stu-id="d1f90-132">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="d1f90-133">Next steps</span><span class="sxs-lookup"><span data-stu-id="d1f90-133">Next steps</span></span>

<span data-ttu-id="d1f90-134">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span><span class="sxs-lookup"><span data-stu-id="d1f90-134">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="d1f90-135">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="d1f90-135">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
