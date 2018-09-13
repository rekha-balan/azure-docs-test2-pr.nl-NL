---
title: Azure PowerShell Script-Set up geo-replication-single SQL Database | Microsoft Docs
description: Azure PowerShell Script Sample - Set up Active Geo-Replication for a single Azure SQL database using PowerShell
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
ms.openlocfilehash: 9600983f9a829a5d142144d3a3ba25856b3853e7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554600"
---
# <a name="configure-active-geo-replication-for-a-single-azure-sql-database-using-powershell"></a><span data-ttu-id="a4d00-103">Configure Active Geo-Replication for a single Azure SQL database using PowerShell</span><span class="sxs-lookup"><span data-stu-id="a4d00-103">Configure Active Geo-Replication for a single Azure SQL database using PowerShell</span></span>

<span data-ttu-id="a4d00-104">This sample PowerShell script configures Active Geo-Replication for a single database and fails it over to the secondary replica.</span><span class="sxs-lookup"><span data-stu-id="a4d00-104">This sample PowerShell script configures Active Geo-Replication for a single database and fails it over to the secondary replica.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-scripts"></a><span data-ttu-id="a4d00-105">Sample Scripts</span><span class="sxs-lookup"><span data-stu-id="a4d00-105">Sample Scripts</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/setup-geodr-and-failover-database/setup-geodr-and-failover-database.ps1 "Set up Active Geo-Replication for single database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="a4d00-106">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="a4d00-106">Clean up deployment</span></span>

<span data-ttu-id="a4d00-107">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span><span class="sxs-lookup"><span data-stu-id="a4d00-107">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myPrimaryResourceGroup"
Remove-AzureRmResourceGroup -ResourceGroupName "mySecondaryResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="a4d00-108">Script explanation</span><span class="sxs-lookup"><span data-stu-id="a4d00-108">Script explanation</span></span>

<span data-ttu-id="a4d00-109">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="a4d00-109">This script uses the following commands.</span></span> <span data-ttu-id="a4d00-110">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="a4d00-110">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="a4d00-111">Command</span><span class="sxs-lookup"><span data-stu-id="a4d00-111">Command</span></span> | <span data-ttu-id="a4d00-112">Notes</span><span class="sxs-lookup"><span data-stu-id="a4d00-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a4d00-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="a4d00-113">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="a4d00-114">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="a4d00-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="a4d00-115">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="a4d00-115">New-AzureRmSqlServer</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.5.0/new-azurermsqlserver) | <span data-ttu-id="a4d00-116">Creates a logical server that hosts a database or elastic pool.</span><span class="sxs-lookup"><span data-stu-id="a4d00-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="a4d00-117">New-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="a4d00-117">New-AzureRmSqlElasticPool</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.5.0/new-azurermsqlelasticpool) | <span data-ttu-id="a4d00-118">Creates an elastic pool within a logical server.</span><span class="sxs-lookup"><span data-stu-id="a4d00-118">Creates an elastic pool within a logical server.</span></span> |
| [<span data-ttu-id="a4d00-119">Set-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="a4d00-119">Set-AzureRmSqlDatabase</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.5.0/set-azurermsqldatabase) | <span data-ttu-id="a4d00-120">Updates database properties or moves a database into, out of, or between elastic pools.</span><span class="sxs-lookup"><span data-stu-id="a4d00-120">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="a4d00-121">New-AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="a4d00-121">New-AzureRmSqlDatabaseSecondary</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.5.0/new-azurermsqldatabasesecondary)| <span data-ttu-id="a4d00-122">Creates a secondary database for an existing database and starts data replication.</span><span class="sxs-lookup"><span data-stu-id="a4d00-122">Creates a secondary database for an existing database and starts data replication.</span></span> |
| [<span data-ttu-id="a4d00-123">Get-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="a4d00-123">Get-AzureRmSqlDatabase</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.5.0/get-azurermsqldatabase)| <span data-ttu-id="a4d00-124">Gets one or more databases.</span><span class="sxs-lookup"><span data-stu-id="a4d00-124">Gets one or more databases.</span></span> |
| [<span data-ttu-id="a4d00-125">Set-AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="a4d00-125">Set-AzureRmSqlDatabaseSecondary</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.5.0/set-azurermsqldatabasesecondary)| <span data-ttu-id="a4d00-126">Switches a secondary database to be primary to initiate failover.</span><span class="sxs-lookup"><span data-stu-id="a4d00-126">Switches a secondary database to be primary to initiate failover.</span></span>|
| [<span data-ttu-id="a4d00-127">Get-AzureRmSqlDatabaseReplicationLink</span><span class="sxs-lookup"><span data-stu-id="a4d00-127">Get-AzureRmSqlDatabaseReplicationLink</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.5.0/get-azurermsqldatabasereplicationlink) | <span data-ttu-id="a4d00-128">Gets the geo-replication links between an Azure SQL Database and a resource group or SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a4d00-128">Gets the geo-replication links between an Azure SQL Database and a resource group or SQL Server.</span></span> |
| [<span data-ttu-id="a4d00-129">Remove-AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="a4d00-129">Remove-AzureRmSqlDatabaseSecondary</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.5.0/remove-azurermsqldatabasesecondary) | <span data-ttu-id="a4d00-130">Terminates data replication between a SQL Database and the specified secondary database.</span><span class="sxs-lookup"><span data-stu-id="a4d00-130">Terminates data replication between a SQL Database and the specified secondary database.</span></span> |
| [<span data-ttu-id="a4d00-131">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="a4d00-131">Remove-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/remove-azurermresourcegroup) | <span data-ttu-id="a4d00-132">Deletes a resource group including all nested resources.</span><span class="sxs-lookup"><span data-stu-id="a4d00-132">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="a4d00-133">Next steps</span><span class="sxs-lookup"><span data-stu-id="a4d00-133">Next steps</span></span>

<span data-ttu-id="a4d00-134">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span><span class="sxs-lookup"><span data-stu-id="a4d00-134">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="a4d00-135">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="a4d00-135">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
