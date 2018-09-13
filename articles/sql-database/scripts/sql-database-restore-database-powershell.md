---
title: PowerShell example-restore-backup-Azure SQL database | Microsoft Docs
description: Azure PowerShell example script to restore an Azure SQL database from geo-redundant backups
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
ms.openlocfilehash: fdce110c0349afa138bf547287a08ecb0e25915d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44780824"
---
# <a name="use-powershell-to-restore-an-azure-sql-database-from-backups"></a><span data-ttu-id="5dc13-103">Use PowerShell to restore an Azure SQL database from backups</span><span class="sxs-lookup"><span data-stu-id="5dc13-103">Use PowerShell to restore an Azure SQL database from backups</span></span>

<span data-ttu-id="5dc13-104">This PowerShell script example restores an Azure SQL database from a geo-redundant backup, restores a deleted Azure SQL database to its latest backup, and restores an Azure SQL database to a specific point in time.</span><span class="sxs-lookup"><span data-stu-id="5dc13-104">This PowerShell script example restores an Azure SQL database from a geo-redundant backup, restores a deleted Azure SQL database to its latest backup, and restores an Azure SQL database to a specific point in time.</span></span>  

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]
[!INCLUDE [cloud-shell-powershell.md](../../../includes/cloud-shell-powershell.md)]

<span data-ttu-id="5dc13-105">If you choose to install and use the PowerShell locally, this tutorial requires the Azure PowerShell module version 5.7.0 or later.</span><span class="sxs-lookup"><span data-stu-id="5dc13-105">If you choose to install and use the PowerShell locally, this tutorial requires the Azure PowerShell module version 5.7.0 or later.</span></span> <span data-ttu-id="5dc13-106">Run `Get-Module -ListAvailable AzureRM` to find the version.</span><span class="sxs-lookup"><span data-stu-id="5dc13-106">Run `Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="5dc13-107">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="5dc13-107">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span> <span data-ttu-id="5dc13-108">If you are running PowerShell locally, you also need to run `Connect-AzureRmAccount` to create a connection with Azure.</span><span class="sxs-lookup"><span data-stu-id="5dc13-108">If you are running PowerShell locally, you also need to run `Connect-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="5dc13-109">Sample script</span><span class="sxs-lookup"><span data-stu-id="5dc13-109">Sample script</span></span>

[!code-powershell-interactive[main](../../../powershell_scripts/sql-database/restore-database/restore-database.ps1?highlight=17-18 "Create SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="5dc13-110">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="5dc13-110">Clean up deployment</span></span>

<span data-ttu-id="5dc13-111">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span><span class="sxs-lookup"><span data-stu-id="5dc13-111">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName $resourcegroupname
```

## <a name="script-explanation"></a><span data-ttu-id="5dc13-112">Script explanation</span><span class="sxs-lookup"><span data-stu-id="5dc13-112">Script explanation</span></span>

<span data-ttu-id="5dc13-113">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="5dc13-113">This script uses the following commands.</span></span> <span data-ttu-id="5dc13-114">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="5dc13-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="5dc13-115">Command</span><span class="sxs-lookup"><span data-stu-id="5dc13-115">Command</span></span> | <span data-ttu-id="5dc13-116">Notes</span><span class="sxs-lookup"><span data-stu-id="5dc13-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5dc13-117">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="5dc13-117">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="5dc13-118">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="5dc13-118">Creates a resource group in which all resources are stored.</span></span> | [<span data-ttu-id="5dc13-119">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="5dc13-119">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="5dc13-120">Creates a logical server that hosts a database or elastic pool.</span><span class="sxs-lookup"><span data-stu-id="5dc13-120">Creates a logical server that hosts a database or elastic pool.</span></span> | 
| [<span data-ttu-id="5dc13-121">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="5dc13-121">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="5dc13-122">Creates a database in a logical server as a single or a pooled database.</span><span class="sxs-lookup"><span data-stu-id="5dc13-122">Creates a database in a logical server as a single or a pooled database.</span></span> |
[<span data-ttu-id="5dc13-123">Get-AzureRmSqlDatabaseGeoBackup</span><span class="sxs-lookup"><span data-stu-id="5dc13-123">Get-AzureRmSqlDatabaseGeoBackup</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabasegeobackup) | <span data-ttu-id="5dc13-124">Gets a geo-redundant backup of a database.</span><span class="sxs-lookup"><span data-stu-id="5dc13-124">Gets a geo-redundant backup of a database.</span></span> |
| [<span data-ttu-id="5dc13-125">Restore-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="5dc13-125">Restore-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/restore-azurermsqldatabase) | <span data-ttu-id="5dc13-126">Restores a SQL database.</span><span class="sxs-lookup"><span data-stu-id="5dc13-126">Restores a SQL database.</span></span> |
|[<span data-ttu-id="5dc13-127">Remove-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="5dc13-127">Remove-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/remove-azurermsqldatabase) | <span data-ttu-id="5dc13-128">Removes an Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="5dc13-128">Removes an Azure SQL database.</span></span> |
| [<span data-ttu-id="5dc13-129">Get-AzureRmSqlDeletedDatabaseBackup</span><span class="sxs-lookup"><span data-stu-id="5dc13-129">Get-AzureRmSqlDeletedDatabaseBackup</span></span>](/powershell/module/azurerm.sql/get-azurermsqldeleteddatabasebackup) | <span data-ttu-id="5dc13-130">Gets a deleted database that you can restore.</span><span class="sxs-lookup"><span data-stu-id="5dc13-130">Gets a deleted database that you can restore.</span></span> |
| [<span data-ttu-id="5dc13-131">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="5dc13-131">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="5dc13-132">Deletes a resource group including all nested resources.</span><span class="sxs-lookup"><span data-stu-id="5dc13-132">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5dc13-133">Next steps</span><span class="sxs-lookup"><span data-stu-id="5dc13-133">Next steps</span></span>

<span data-ttu-id="5dc13-134">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5dc13-134">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="5dc13-135">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="5dc13-135">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
