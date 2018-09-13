---
title: Azure PowerShell Script Sample - Delete a backup for a web app | Microsoft Docs
description: Azure PowerShell Script Sample - Delete a backup for a web app
services: app-service\web
documentationcenter: ''
author: cephalin
manager: cfowler
editor: ''
tags: azure-service-management
ms.assetid: ebcadb49-755d-4202-a5eb-f211827a9168
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 10/30/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 6fede6d7c8de473debea927366fca0ab52cf6e5b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856217"
---
# <a name="delete-a-backup-for-a-web-app"></a><span data-ttu-id="bd43b-103">Delete a backup for a web app</span><span class="sxs-lookup"><span data-stu-id="bd43b-103">Delete a backup for a web app</span></span>

<span data-ttu-id="bd43b-104">This sample script creates a web app in App Service with its related resources, and then creates a one-time backup for it.</span><span class="sxs-lookup"><span data-stu-id="bd43b-104">This sample script creates a web app in App Service with its related resources, and then creates a one-time backup for it.</span></span> 

<span data-ttu-id="bd43b-105">To run this script, you need an existing backup for a web app.</span><span class="sxs-lookup"><span data-stu-id="bd43b-105">To run this script, you need an existing backup for a web app.</span></span> <span data-ttu-id="bd43b-106">To create one, see [Backup up a web app](app-service-powershell-backup-onetime.md) or [Create a scheduled backup for a web app](app-service-powershell-backup-scheduled.md).</span><span class="sxs-lookup"><span data-stu-id="bd43b-106">To create one, see [Backup up a web app](app-service-powershell-backup-onetime.md) or [Create a scheduled backup for a web app](app-service-powershell-backup-scheduled.md).</span></span>

## <a name="sample-script"></a><span data-ttu-id="bd43b-107">Sample script</span><span class="sxs-lookup"><span data-stu-id="bd43b-107">Sample script</span></span>

[!code-azurepowershell-interactive[main](../../../powershell_scripts/app-service/backup-delete/backup-delete.ps1?highlight=1-2,11 "Delete a backup for a web app")]

## <a name="clean-up-deployment"></a><span data-ttu-id="bd43b-108">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="bd43b-108">Clean up deployment</span></span> 

<span data-ttu-id="bd43b-109">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="bd43b-109">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="bd43b-110">Script explanation</span><span class="sxs-lookup"><span data-stu-id="bd43b-110">Script explanation</span></span>

<span data-ttu-id="bd43b-111">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="bd43b-111">This script uses the following commands.</span></span> <span data-ttu-id="bd43b-112">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="bd43b-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="bd43b-113">Command</span><span class="sxs-lookup"><span data-stu-id="bd43b-113">Command</span></span> | <span data-ttu-id="bd43b-114">Notes</span><span class="sxs-lookup"><span data-stu-id="bd43b-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="bd43b-115">Get-AzureRmWebAppBackupList</span><span class="sxs-lookup"><span data-stu-id="bd43b-115">Get-AzureRmWebAppBackupList</span></span>](/powershell/module/azurerm.websites/get-azurermwebappbackuplist) | <span data-ttu-id="bd43b-116">Gets a list of backups for a web app.</span><span class="sxs-lookup"><span data-stu-id="bd43b-116">Gets a list of backups for a web app.</span></span> |
| [<span data-ttu-id="bd43b-117">Remove-AzureRmWebAppBackup</span><span class="sxs-lookup"><span data-stu-id="bd43b-117">Remove-AzureRmWebAppBackup</span></span>](/powershell/module/azurerm.websites/remove-azurermwebappbackup) | <span data-ttu-id="bd43b-118">Removes the specified backup of a web app.</span><span class="sxs-lookup"><span data-stu-id="bd43b-118">Removes the specified backup of a web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="bd43b-119">Next steps</span><span class="sxs-lookup"><span data-stu-id="bd43b-119">Next steps</span></span>

<span data-ttu-id="bd43b-120">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="bd43b-120">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="bd43b-121">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="bd43b-121">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
