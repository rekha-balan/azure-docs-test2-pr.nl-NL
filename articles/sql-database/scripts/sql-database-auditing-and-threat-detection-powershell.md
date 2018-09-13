---
title: PowerShell example-auditing-threat detection-Azure SQL Database  | Microsoft Docs
description: Azure PowerShell example script to configure auditing & threat detection in an Azure SQL Database
services: sql-database
documentationcenter: sql-database
author: CarlRabeler
manager: craigg
editor: carlrab
tags: azure-service-management
ms.assetid: ''
ms.service: sql-database
ms.custom: mvc,security
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 09/07/2018
ms.author: carlrab
ms.openlocfilehash: 1be7f049435f39d164cdcb151dc948d55da1c740
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44797945"
---
# <a name="use-powershell-to-configure-sql-database-auditing-and-threat-detection"></a><span data-ttu-id="20ca5-103">Use PowerShell to configure SQL Database auditing and threat detection</span><span class="sxs-lookup"><span data-stu-id="20ca5-103">Use PowerShell to configure SQL Database auditing and threat detection</span></span>

<span data-ttu-id="20ca5-104">This PowerShell script example configures SQL Database auditing and threat detection.</span><span class="sxs-lookup"><span data-stu-id="20ca5-104">This PowerShell script example configures SQL Database auditing and threat detection.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]
[!INCLUDE [cloud-shell-powershell.md](../../../includes/cloud-shell-powershell.md)]

<span data-ttu-id="20ca5-105">If you choose to install and use the PowerShell locally, this tutorial requires the Azure PowerShell module version 5.7.0 or later.</span><span class="sxs-lookup"><span data-stu-id="20ca5-105">If you choose to install and use the PowerShell locally, this tutorial requires the Azure PowerShell module version 5.7.0 or later.</span></span> <span data-ttu-id="20ca5-106">Run `Get-Module -ListAvailable AzureRM` to find the version.</span><span class="sxs-lookup"><span data-stu-id="20ca5-106">Run `Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="20ca5-107">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="20ca5-107">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span> <span data-ttu-id="20ca5-108">If you are running PowerShell locally, you also need to run `Connect-AzureRmAccount` to create a connection with Azure.</span><span class="sxs-lookup"><span data-stu-id="20ca5-108">If you are running PowerShell locally, you also need to run `Connect-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="20ca5-109">Sample script</span><span class="sxs-lookup"><span data-stu-id="20ca5-109">Sample script</span></span>

[!code-powershell-interactive[main](../../../powershell_scripts/sql-database/database-auditing-and-threat-detection/database-auditing-and-threat-detection.ps1?highlight=13-14 "Configure auditing and threat detection")]

## <a name="clean-up-deployment"></a><span data-ttu-id="20ca5-110">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="20ca5-110">Clean up deployment</span></span>

<span data-ttu-id="20ca5-111">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span><span class="sxs-lookup"><span data-stu-id="20ca5-111">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName $resourcegroupname
```

## <a name="script-explanation"></a><span data-ttu-id="20ca5-112">Script explanation</span><span class="sxs-lookup"><span data-stu-id="20ca5-112">Script explanation</span></span>

<span data-ttu-id="20ca5-113">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="20ca5-113">This script uses the following commands.</span></span> <span data-ttu-id="20ca5-114">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="20ca5-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="20ca5-115">Command</span><span class="sxs-lookup"><span data-stu-id="20ca5-115">Command</span></span> | <span data-ttu-id="20ca5-116">Notes</span><span class="sxs-lookup"><span data-stu-id="20ca5-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="20ca5-117">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="20ca5-117">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="20ca5-118">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="20ca5-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="20ca5-119">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="20ca5-119">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="20ca5-120">Creates a logical server that hosts a database or elastic pool.</span><span class="sxs-lookup"><span data-stu-id="20ca5-120">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="20ca5-121">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="20ca5-121">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="20ca5-122">Creates a database in a logical server as a single or a pooled database.</span><span class="sxs-lookup"><span data-stu-id="20ca5-122">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="20ca5-123">New-AzureRmStorageAccount</span><span class="sxs-lookup"><span data-stu-id="20ca5-123">New-AzureRmStorageAccount</span></span>](/powershell/module/azurerm.storage/new-azurermstorageaccount) | <span data-ttu-id="20ca5-124">Creates a Storage account.</span><span class="sxs-lookup"><span data-stu-id="20ca5-124">Creates a Storage account.</span></span> |
| [<span data-ttu-id="20ca5-125">Set-AzureRmSqlDatabaseAuditingPolicy</span><span class="sxs-lookup"><span data-stu-id="20ca5-125">Set-AzureRmSqlDatabaseAuditingPolicy</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabaseauditingpolicy) | <span data-ttu-id="20ca5-126">Sets the auditing policy for a database.</span><span class="sxs-lookup"><span data-stu-id="20ca5-126">Sets the auditing policy for a database.</span></span> |
| [<span data-ttu-id="20ca5-127">Set-AzureRmSqlDatabaseThreatDetectionPolicy</span><span class="sxs-lookup"><span data-stu-id="20ca5-127">Set-AzureRmSqlDatabaseThreatDetectionPolicy</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabasethreatdetectionpolicy) | <span data-ttu-id="20ca5-128">Sets a threat detection policy on a database.</span><span class="sxs-lookup"><span data-stu-id="20ca5-128">Sets a threat detection policy on a database.</span></span> |
| [<span data-ttu-id="20ca5-129">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="20ca5-129">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="20ca5-130">Deletes a resource group including all nested resources.</span><span class="sxs-lookup"><span data-stu-id="20ca5-130">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="20ca5-131">Next steps</span><span class="sxs-lookup"><span data-stu-id="20ca5-131">Next steps</span></span>

<span data-ttu-id="20ca5-132">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="20ca5-132">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="20ca5-133">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="20ca5-133">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
