---
title: Azure PowerShell Script-Import-bacpac-SQL database | Microsoft Docs
description: Azure PowerShell Script Sample - Import from a bacpac into a SQL database using PowerShell
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
ms.openlocfilehash: ff27ec5eb86b11bbbc91e648ffa72956436f445a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553049"
---
# <a name="import-from-a-bacpac-into-a-sql-database-using-powershell"></a><span data-ttu-id="e2945-103">Import from a bacpac into a SQL database using PowerShell</span><span class="sxs-lookup"><span data-stu-id="e2945-103">Import from a bacpac into a SQL database using PowerShell</span></span>

<span data-ttu-id="e2945-104">This sample PowerShell script imports a database from a **bacpac** file.</span><span class="sxs-lookup"><span data-stu-id="e2945-104">This sample PowerShell script imports a database from a **bacpac** file.</span></span>  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="e2945-105">Sample script</span><span class="sxs-lookup"><span data-stu-id="e2945-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/import-from-bacpac/import-from-bacpac.ps1 "Create SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="e2945-106">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="e2945-106">Clean up deployment</span></span>

<span data-ttu-id="e2945-107">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span><span class="sxs-lookup"><span data-stu-id="e2945-107">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="e2945-108">Script explanation</span><span class="sxs-lookup"><span data-stu-id="e2945-108">Script explanation</span></span>

<span data-ttu-id="e2945-109">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="e2945-109">This script uses the following commands.</span></span> <span data-ttu-id="e2945-110">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="e2945-110">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="e2945-111">Command</span><span class="sxs-lookup"><span data-stu-id="e2945-111">Command</span></span> | <span data-ttu-id="e2945-112">Notes</span><span class="sxs-lookup"><span data-stu-id="e2945-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e2945-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="e2945-113">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.3.0/new-azurermresourcegroup) | <span data-ttu-id="e2945-114">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="e2945-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="e2945-115">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="e2945-115">New-AzureRmSqlServer</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.5.0/new-azurermsqlserver) | <span data-ttu-id="e2945-116">Creates a logical server that hosts the SQL Database.</span><span class="sxs-lookup"><span data-stu-id="e2945-116">Creates a logical server that hosts the SQL Database.</span></span> |
| [<span data-ttu-id="e2945-117">New-AzureRmSqlServerFirewallRule</span><span class="sxs-lookup"><span data-stu-id="e2945-117">New-AzureRmSqlServerFirewallRule</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.3.0/new-azurermsqlserverfirewallrule) | <span data-ttu-id="e2945-118">Creates a firewall rule to allow access to all SQL Databases on the server from the entered IP address range.</span><span class="sxs-lookup"><span data-stu-id="e2945-118">Creates a firewall rule to allow access to all SQL Databases on the server from the entered IP address range.</span></span> |
| [<span data-ttu-id="e2945-119">New-AzureRmSqlDatabaseImport</span><span class="sxs-lookup"><span data-stu-id="e2945-119">New-AzureRmSqlDatabaseImport</span></span>](https://docs.microsoft.com/powershell/module/azurerm.sql/new-azurermsqldatabaseimport?view=azurermps-3.7.0) | <span data-ttu-id="e2945-120">Imports a .bacpac file and create a new database on the server.</span><span class="sxs-lookup"><span data-stu-id="e2945-120">Imports a .bacpac file and create a new database on the server.</span></span> |
| [<span data-ttu-id="e2945-121">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="e2945-121">Remove-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.2.0/remove-azurermresourcegroup) | <span data-ttu-id="e2945-122">Deletes a resource group including all nested resources.</span><span class="sxs-lookup"><span data-stu-id="e2945-122">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e2945-123">Next steps</span><span class="sxs-lookup"><span data-stu-id="e2945-123">Next steps</span></span>

<span data-ttu-id="e2945-124">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span><span class="sxs-lookup"><span data-stu-id="e2945-124">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="e2945-125">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="e2945-125">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>