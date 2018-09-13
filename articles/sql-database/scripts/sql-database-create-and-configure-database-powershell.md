---
title: PowerShell example-create an Azure SQL database | Microsoft Docs
description: Azure PowerShell example script to create a Azure SQL database
services: sql-database
documentationcenter: sql-database
author: CarlRabeler
manager: craigg
editor: carlrab
tags: azure-service-management
ms.assetid: ''
ms.service: sql-database
ms.custom: DBs & servers, mvc
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 09/07/2018
ms.author: carlrab
ms.openlocfilehash: fb1f38932af4d502406f87b0eaa1f3a307268c30
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44813825"
---
# <a name="use-powershell-to-create-a-single-azure-sql-database-and-configure-a-firewall-rule"></a><span data-ttu-id="269fe-103">Use PowerShell to create a single Azure SQL database and configure a firewall rule</span><span class="sxs-lookup"><span data-stu-id="269fe-103">Use PowerShell to create a single Azure SQL database and configure a firewall rule</span></span>

<span data-ttu-id="269fe-104">This PowerShell script example creates an Azure SQL database and configures a server-level firewall rule.</span><span class="sxs-lookup"><span data-stu-id="269fe-104">This PowerShell script example creates an Azure SQL database and configures a server-level firewall rule.</span></span> <span data-ttu-id="269fe-105">Once the script has been successfully run, the SQL Database can be accessed from all Azure services and the configured IP address.</span><span class="sxs-lookup"><span data-stu-id="269fe-105">Once the script has been successfully run, the SQL Database can be accessed from all Azure services and the configured IP address.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]
[!INCLUDE [cloud-shell-powershell.md](../../../includes/cloud-shell-powershell.md)]

<span data-ttu-id="269fe-106">If you choose to install and use the PowerShell locally, this tutorial requires the Azure PowerShell module version 5.7.0 or later.</span><span class="sxs-lookup"><span data-stu-id="269fe-106">If you choose to install and use the PowerShell locally, this tutorial requires the Azure PowerShell module version 5.7.0 or later.</span></span> <span data-ttu-id="269fe-107">Run `Get-Module -ListAvailable AzureRM` to find the version.</span><span class="sxs-lookup"><span data-stu-id="269fe-107">Run `Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="269fe-108">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="269fe-108">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span> <span data-ttu-id="269fe-109">If you are running PowerShell locally, you also need to run `Connect-AzureRmAccount` to create a connection with Azure.</span><span class="sxs-lookup"><span data-stu-id="269fe-109">If you are running PowerShell locally, you also need to run `Connect-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="269fe-110">Sample script</span><span class="sxs-lookup"><span data-stu-id="269fe-110">Sample script</span></span>

[!code-powershell-interactive[main](../../../powershell_scripts/sql-database/create-and-configure-database/create-and-configure-database.ps1?highlight=13-14 "Create SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="269fe-111">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="269fe-111">Clean up deployment</span></span>

<span data-ttu-id="269fe-112">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span><span class="sxs-lookup"><span data-stu-id="269fe-112">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName $resourcegroupname
```

## <a name="script-explanation"></a><span data-ttu-id="269fe-113">Script explanation</span><span class="sxs-lookup"><span data-stu-id="269fe-113">Script explanation</span></span>

<span data-ttu-id="269fe-114">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="269fe-114">This script uses the following commands.</span></span> <span data-ttu-id="269fe-115">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="269fe-115">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="269fe-116">Command</span><span class="sxs-lookup"><span data-stu-id="269fe-116">Command</span></span> | <span data-ttu-id="269fe-117">Notes</span><span class="sxs-lookup"><span data-stu-id="269fe-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="269fe-118">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="269fe-118">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="269fe-119">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="269fe-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="269fe-120">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="269fe-120">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="269fe-121">Creates a logical server that hosts a database or elastic pool.</span><span class="sxs-lookup"><span data-stu-id="269fe-121">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="269fe-122">New-AzureRmSqlServerFirewallRule</span><span class="sxs-lookup"><span data-stu-id="269fe-122">New-AzureRmSqlServerFirewallRule</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) | <span data-ttu-id="269fe-123">Creates a firewall rule to allow access to all SQL Databases on the server from the entered IP address range.</span><span class="sxs-lookup"><span data-stu-id="269fe-123">Creates a firewall rule to allow access to all SQL Databases on the server from the entered IP address range.</span></span> |
| [<span data-ttu-id="269fe-124">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="269fe-124">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="269fe-125">Creates a database in a logical server as a single or a pooled database.</span><span class="sxs-lookup"><span data-stu-id="269fe-125">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="269fe-126">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="269fe-126">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="269fe-127">Deletes a resource group including all nested resources.</span><span class="sxs-lookup"><span data-stu-id="269fe-127">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="269fe-128">Next steps</span><span class="sxs-lookup"><span data-stu-id="269fe-128">Next steps</span></span>

<span data-ttu-id="269fe-129">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="269fe-129">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="269fe-130">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="269fe-130">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>



