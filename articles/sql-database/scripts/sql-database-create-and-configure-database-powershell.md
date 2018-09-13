---
title: Azure PowerShell Script-Create a SQL database | Microsoft Docs
description: Azure PowerShell Script Sample - Create a SQL database using PowerShell
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
ms.openlocfilehash: 0840741bb29717fe0c9f4a66c0a0b8458d0abfdb
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556474"
---
# <a name="create-a-single-sql-database-and-configure-a-firewall-rule-using-powershell"></a><span data-ttu-id="811e5-103">Create a single SQL database and configure a firewall rule using PowerShell</span><span class="sxs-lookup"><span data-stu-id="811e5-103">Create a single SQL database and configure a firewall rule using PowerShell</span></span>

<span data-ttu-id="811e5-104">This sample PowerShell script creates an Azure SQL database and configures a server-level firewall rule.</span><span class="sxs-lookup"><span data-stu-id="811e5-104">This sample PowerShell script creates an Azure SQL database and configures a server-level firewall rule.</span></span> <span data-ttu-id="811e5-105">Once the script has been successfully run, the SQL Database can be accessed from all Azure services and the configured IP address.</span><span class="sxs-lookup"><span data-stu-id="811e5-105">Once the script has been successfully run, the SQL Database can be accessed from all Azure services and the configured IP address.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="811e5-106">Sample script</span><span class="sxs-lookup"><span data-stu-id="811e5-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/create-and-configure-database/create-and-configure-database.ps1?highlight=7-8 "Create SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="811e5-107">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="811e5-107">Clean up deployment</span></span>

<span data-ttu-id="811e5-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span><span class="sxs-lookup"><span data-stu-id="811e5-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="811e5-109">Script explanation</span><span class="sxs-lookup"><span data-stu-id="811e5-109">Script explanation</span></span>

<span data-ttu-id="811e5-110">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="811e5-110">This script uses the following commands.</span></span> <span data-ttu-id="811e5-111">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="811e5-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="811e5-112">Command</span><span class="sxs-lookup"><span data-stu-id="811e5-112">Command</span></span> | <span data-ttu-id="811e5-113">Notes</span><span class="sxs-lookup"><span data-stu-id="811e5-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="811e5-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="811e5-114">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="811e5-115">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="811e5-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="811e5-116">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="811e5-116">New-AzureRmSqlServer</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.5.0/new-azurermsqlserver) | <span data-ttu-id="811e5-117">Creates a logical server that hosts a database or elastic pool.</span><span class="sxs-lookup"><span data-stu-id="811e5-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="811e5-118">New-AzureRmSqlServerFirewallRule</span><span class="sxs-lookup"><span data-stu-id="811e5-118">New-AzureRmSqlServerFirewallRule</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.5.0/new-azurermsqlserverfirewallrule) | <span data-ttu-id="811e5-119">Creates a firewall rule to allow access to all SQL Databases on the server from the entered IP address range.</span><span class="sxs-lookup"><span data-stu-id="811e5-119">Creates a firewall rule to allow access to all SQL Databases on the server from the entered IP address range.</span></span> |
| [<span data-ttu-id="811e5-120">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="811e5-120">New-AzureRmSqlDatabase</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.5.0/new-azurermsqldatabase) | <span data-ttu-id="811e5-121">Creates a database in a logical server as a single or a pooled database.</span><span class="sxs-lookup"><span data-stu-id="811e5-121">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="811e5-122">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="811e5-122">Remove-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/remove-azurermresourcegroup) | <span data-ttu-id="811e5-123">Deletes a resource group including all nested resources.</span><span class="sxs-lookup"><span data-stu-id="811e5-123">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="811e5-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="811e5-124">Next steps</span></span>

<span data-ttu-id="811e5-125">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span><span class="sxs-lookup"><span data-stu-id="811e5-125">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="811e5-126">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="811e5-126">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>



