---
title: Azure PowerShell Script-Copy a SQL database to new server | Microsoft Docs
description: Azure PowerShell Script Sample - Copy a SQL database to a new server using PowerShell
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
ms.openlocfilehash: af2b60f110a99cd62bbfa8bac44fcf742012ac11
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550421"
---
# <a name="copy-a-sql-database-to-a-new-server-using-powershell"></a><span data-ttu-id="17bc8-103">Copy a SQL database to a new server using PowerShell</span><span class="sxs-lookup"><span data-stu-id="17bc8-103">Copy a SQL database to a new server using PowerShell</span></span>

<span data-ttu-id="17bc8-104">This sample PowerShell script creates a copy of an existing database in a new server.</span><span class="sxs-lookup"><span data-stu-id="17bc8-104">This sample PowerShell script creates a copy of an existing database in a new server.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="copy-a-database-to-a-new-server"></a><span data-ttu-id="17bc8-105">Copy a database to a new server</span><span class="sxs-lookup"><span data-stu-id="17bc8-105">Copy a database to a new server</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/copy-database-to-new-server/copy-database-to-new-server.ps1 "Copy database to new server")]

## <a name="clean-up-deployment"></a><span data-ttu-id="17bc8-106">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="17bc8-106">Clean up deployment</span></span>

<span data-ttu-id="17bc8-107">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span><span class="sxs-lookup"><span data-stu-id="17bc8-107">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="17bc8-108">Script explanation</span><span class="sxs-lookup"><span data-stu-id="17bc8-108">Script explanation</span></span>

<span data-ttu-id="17bc8-109">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="17bc8-109">This script uses the following commands.</span></span> <span data-ttu-id="17bc8-110">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="17bc8-110">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="17bc8-111">Command</span><span class="sxs-lookup"><span data-stu-id="17bc8-111">Command</span></span> | <span data-ttu-id="17bc8-112">Notes</span><span class="sxs-lookup"><span data-stu-id="17bc8-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="17bc8-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="17bc8-113">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="17bc8-114">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="17bc8-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="17bc8-115">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="17bc8-115">New-AzureRmSqlServer</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.5.0/new-azurermsqlserver) | <span data-ttu-id="17bc8-116">Creates a logical server that hosts a database or elastic pool.</span><span class="sxs-lookup"><span data-stu-id="17bc8-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="17bc8-117">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="17bc8-117">New-AzureRmSqlDatabase</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.5.0/new-azurermsqldatabase) | <span data-ttu-id="17bc8-118">Creates a database in a logical server as a single or a pooled database.</span><span class="sxs-lookup"><span data-stu-id="17bc8-118">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="17bc8-119">New-AzureRmSqlDatabaseCopy</span><span class="sxs-lookup"><span data-stu-id="17bc8-119">New-AzureRmSqlDatabaseCopy</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.5.0/new-azurermsqldatabasecopy) | <span data-ttu-id="17bc8-120">Creates a copy of a database that uses the snapshot at the current time.</span><span class="sxs-lookup"><span data-stu-id="17bc8-120">Creates a copy of a database that uses the snapshot at the current time.</span></span> |
| [<span data-ttu-id="17bc8-121">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="17bc8-121">Remove-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/remove-azurermresourcegroup) | <span data-ttu-id="17bc8-122">Deletes a resource group including all nested resources.</span><span class="sxs-lookup"><span data-stu-id="17bc8-122">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="17bc8-123">Next steps</span><span class="sxs-lookup"><span data-stu-id="17bc8-123">Next steps</span></span>

<span data-ttu-id="17bc8-124">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span><span class="sxs-lookup"><span data-stu-id="17bc8-124">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="17bc8-125">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="17bc8-125">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
