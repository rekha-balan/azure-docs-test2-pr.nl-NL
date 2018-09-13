---
title: PowerShell example-active geo-replication-pooled Azure SQL database | Microsoft Docs
description: Azure PowerShell example script to set up active geo-replication for a pooled Azure SQL database and fail it over.
services: sql-database
documentationcenter: sql-database
author: CarlRabeler
manager: craigg
editor: carlrab
tags: azure-service-management
ms.assetid: ''
ms.service: sql-database
ms.custom: business continuity, mvc
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 09/07/2018
ms.author: carlrab
ms.openlocfilehash: db788652a73b82b8d6a8dab2ecd888d66b2057ca
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44819356"
---
# <a name="use-powershell-to-configure-active-geo-replication-for-a-pooled-azure-sql-database"></a><span data-ttu-id="b4dd8-103">Use PowerShell to configure active geo-replication for a pooled Azure SQL database</span><span class="sxs-lookup"><span data-stu-id="b4dd8-103">Use PowerShell to configure active geo-replication for a pooled Azure SQL database</span></span>

<span data-ttu-id="b4dd8-104">This PowerShell script example configures active geo-replication for an Azure SQL database in an elastic pool and fails it over to the secondary replica of the Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="b4dd8-104">This PowerShell script example configures active geo-replication for an Azure SQL database in an elastic pool and fails it over to the secondary replica of the Azure SQL database.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]
[!INCLUDE [cloud-shell-powershell.md](../../../includes/cloud-shell-powershell.md)]

<span data-ttu-id="b4dd8-105">If you choose to install and use the PowerShell locally, this tutorial requires the Azure PowerShell module version 5.7.0 or later.</span><span class="sxs-lookup"><span data-stu-id="b4dd8-105">If you choose to install and use the PowerShell locally, this tutorial requires the Azure PowerShell module version 5.7.0 or later.</span></span> <span data-ttu-id="b4dd8-106">Run `Get-Module -ListAvailable AzureRM` to find the version.</span><span class="sxs-lookup"><span data-stu-id="b4dd8-106">Run `Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="b4dd8-107">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="b4dd8-107">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span> <span data-ttu-id="b4dd8-108">If you are running PowerShell locally, you also need to run `Connect-AzureRmAccount` to create a connection with Azure.</span><span class="sxs-lookup"><span data-stu-id="b4dd8-108">If you are running PowerShell locally, you also need to run `Connect-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-scripts"></a><span data-ttu-id="b4dd8-109">Sample scripts</span><span class="sxs-lookup"><span data-stu-id="b4dd8-109">Sample scripts</span></span>

[!code-powershell-interactive[main](../../../powershell_scripts/sql-database/setup-geodr-and-failover-pool/setup-geodr-and-failover-pool.ps1?highlight=16-19 "Set up active geo-replication for elastic pool")]

## <a name="clean-up-deployment"></a><span data-ttu-id="b4dd8-110">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="b4dd8-110">Clean up deployment</span></span>

<span data-ttu-id="b4dd8-111">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span><span class="sxs-lookup"><span data-stu-id="b4dd8-111">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName $primaryresourcegroupname
Remove-AzureRmResourceGroup -ResourceGroupName $secondaryresourcegroupname
```

## <a name="script-explanation"></a><span data-ttu-id="b4dd8-112">Script explanation</span><span class="sxs-lookup"><span data-stu-id="b4dd8-112">Script explanation</span></span>

<span data-ttu-id="b4dd8-113">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="b4dd8-113">This script uses the following commands.</span></span> <span data-ttu-id="b4dd8-114">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="b4dd8-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="b4dd8-115">Command</span><span class="sxs-lookup"><span data-stu-id="b4dd8-115">Command</span></span> | <span data-ttu-id="b4dd8-116">Notes</span><span class="sxs-lookup"><span data-stu-id="b4dd8-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b4dd8-117">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="b4dd8-117">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="b4dd8-118">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="b4dd8-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="b4dd8-119">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="b4dd8-119">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="b4dd8-120">Creates a logical server that hosts a database or elastic pool.</span><span class="sxs-lookup"><span data-stu-id="b4dd8-120">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="b4dd8-121">New-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="b4dd8-121">New-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) | <span data-ttu-id="b4dd8-122">Creates an elastic pool within a logical server.</span><span class="sxs-lookup"><span data-stu-id="b4dd8-122">Creates an elastic pool within a logical server.</span></span> |
| [<span data-ttu-id="b4dd8-123">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="b4dd8-123">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="b4dd8-124">Creates a database in a logical server as a single or a pooled database.</span><span class="sxs-lookup"><span data-stu-id="b4dd8-124">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="b4dd8-125">Set-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="b4dd8-125">Set-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabase) | <span data-ttu-id="b4dd8-126">Updates database properties or moves a database into, out of, or between elastic pools.</span><span class="sxs-lookup"><span data-stu-id="b4dd8-126">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="b4dd8-127">New-AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="b4dd8-127">New-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabasesecondary)| <span data-ttu-id="b4dd8-128">Creates a secondary database for an existing database and starts data replication.</span><span class="sxs-lookup"><span data-stu-id="b4dd8-128">Creates a secondary database for an existing database and starts data replication.</span></span> |
| [<span data-ttu-id="b4dd8-129">Get-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="b4dd8-129">Get-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabase)| <span data-ttu-id="b4dd8-130">Gets one or more databases.</span><span class="sxs-lookup"><span data-stu-id="b4dd8-130">Gets one or more databases.</span></span> |
| [<span data-ttu-id="b4dd8-131">Set-AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="b4dd8-131">Set-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabasesecondary)| <span data-ttu-id="b4dd8-132">Switches a secondary database to be primary in order to initiate failover.</span><span class="sxs-lookup"><span data-stu-id="b4dd8-132">Switches a secondary database to be primary in order to initiate failover.</span></span>|
| [<span data-ttu-id="b4dd8-133">Get-AzureRmSqlDatabaseReplicationLink</span><span class="sxs-lookup"><span data-stu-id="b4dd8-133">Get-AzureRmSqlDatabaseReplicationLink</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabasereplicationlink) | <span data-ttu-id="b4dd8-134">Gets the geo-replication links between an Azure SQL Database and a resource group or SQL Server.</span><span class="sxs-lookup"><span data-stu-id="b4dd8-134">Gets the geo-replication links between an Azure SQL Database and a resource group or SQL Server.</span></span> |
| [<span data-ttu-id="b4dd8-135">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="b4dd8-135">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="b4dd8-136">Deletes a resource group including all nested resources.</span><span class="sxs-lookup"><span data-stu-id="b4dd8-136">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="b4dd8-137">Next steps</span><span class="sxs-lookup"><span data-stu-id="b4dd8-137">Next steps</span></span>

<span data-ttu-id="b4dd8-138">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b4dd8-138">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="b4dd8-139">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="b4dd8-139">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
