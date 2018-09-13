---
title: Azure PowerShell Script-Restore a SQL database | Microsoft Docs
description: Azure PowerShell Script Sample - Restore a SQL database using PowerShell
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
ms.openlocfilehash: c9aad737b76666921ca60cd1e6b3bd86adb1904c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556453"
---
# <a name="restore-a-sql-database-using-powershell"></a><span data-ttu-id="c1a58-103">Restore a SQL database using PowerShell</span><span class="sxs-lookup"><span data-stu-id="c1a58-103">Restore a SQL database using PowerShell</span></span>

<span data-ttu-id="c1a58-104">This sample PowerShell script restores an Azure SQL database from a geo-redundant backup and restores a deleted database to the latest backup.</span><span class="sxs-lookup"><span data-stu-id="c1a58-104">This sample PowerShell script restores an Azure SQL database from a geo-redundant backup and restores a deleted database to the latest backup.</span></span>  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="c1a58-105">Sample script</span><span class="sxs-lookup"><span data-stu-id="c1a58-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/restore-database/restore-database.ps1 "Create SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="c1a58-106">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="c1a58-106">Clean up deployment</span></span>

<span data-ttu-id="c1a58-107">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span><span class="sxs-lookup"><span data-stu-id="c1a58-107">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="c1a58-108">Script explanation</span><span class="sxs-lookup"><span data-stu-id="c1a58-108">Script explanation</span></span>

<span data-ttu-id="c1a58-109">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="c1a58-109">This script uses the following commands.</span></span> <span data-ttu-id="c1a58-110">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="c1a58-110">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="c1a58-111">Command</span><span class="sxs-lookup"><span data-stu-id="c1a58-111">Command</span></span> | <span data-ttu-id="c1a58-112">Notes</span><span class="sxs-lookup"><span data-stu-id="c1a58-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c1a58-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c1a58-113">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="c1a58-114">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="c1a58-114">Creates a resource group in which all resources are stored.</span></span> | [<span data-ttu-id="c1a58-115">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="c1a58-115">New-AzureRmSqlServer</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.5.0/new-azurermsqlserver) | <span data-ttu-id="c1a58-116">Creates a logical server that hosts a database or elastic pool.</span><span class="sxs-lookup"><span data-stu-id="c1a58-116">Creates a logical server that hosts a database or elastic pool.</span></span> | 
| [<span data-ttu-id="c1a58-117">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="c1a58-117">New-AzureRmSqlDatabase</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.5.0/new-azurermsqldatabase) | <span data-ttu-id="c1a58-118">Creates a database in a logical server as a single or a pooled database.</span><span class="sxs-lookup"><span data-stu-id="c1a58-118">Creates a database in a logical server as a single or a pooled database.</span></span> |
[<span data-ttu-id="c1a58-119">Get-AzureRmSqlDatabaseGeoBackup</span><span class="sxs-lookup"><span data-stu-id="c1a58-119">Get-AzureRmSqlDatabaseGeoBackup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.5.0/get-azurermsqldatabasegeobackup) | <span data-ttu-id="c1a58-120">Gets a geo-redundant backup of a database.</span><span class="sxs-lookup"><span data-stu-id="c1a58-120">Gets a geo-redundant backup of a database.</span></span> |
| [<span data-ttu-id="c1a58-121">Restore-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="c1a58-121">Restore-AzureRmSqlDatabase</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.5.0/restore-azurermsqldatabase) | <span data-ttu-id="c1a58-122">Restores a SQL database.</span><span class="sxs-lookup"><span data-stu-id="c1a58-122">Restores a SQL database.</span></span> |
|[<span data-ttu-id="c1a58-123">Remove-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="c1a58-123">Remove-AzureRmSqlDatabase</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.5.0/remove-azurermsqldatabase) | <span data-ttu-id="c1a58-124">Removes an Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="c1a58-124">Removes an Azure SQL database.</span></span> |
| [<span data-ttu-id="c1a58-125">Get-AzureRmSqlDeletedDatabaseBackup</span><span class="sxs-lookup"><span data-stu-id="c1a58-125">Get-AzureRmSqlDeletedDatabaseBackup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.5.0/get-azurermsqldeleteddatabasebackup) | <span data-ttu-id="c1a58-126">Gets a deleted database that you can restore.</span><span class="sxs-lookup"><span data-stu-id="c1a58-126">Gets a deleted database that you can restore.</span></span> |
| [<span data-ttu-id="c1a58-127">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c1a58-127">Remove-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.2.0/remove-azurermresourcegroup) | <span data-ttu-id="c1a58-128">Deletes a resource group including all nested resources.</span><span class="sxs-lookup"><span data-stu-id="c1a58-128">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c1a58-129">Next steps</span><span class="sxs-lookup"><span data-stu-id="c1a58-129">Next steps</span></span>

<span data-ttu-id="c1a58-130">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span><span class="sxs-lookup"><span data-stu-id="c1a58-130">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="c1a58-131">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="c1a58-131">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>