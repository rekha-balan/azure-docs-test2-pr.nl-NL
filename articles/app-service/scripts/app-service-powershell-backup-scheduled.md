---
title: Azure PowerShell Script Sample - Create a scheduled backup for a web app | Microsoft Docs
description: Azure PowerShell Script Sample - Create a scheduled backup for a web app
services: app-service\web
documentationcenter: ''
author: cephalin
manager: cfowler
editor: ''
tags: azure-service-management
ms.assetid: a2a27d94-d378-4c17-a6a9-ae1e69dc4a72
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 10/30/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: b2e5b66e93f94085484658f4cc43141354910e3a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869291"
---
# <a name="create-a-scheduled-backup-for-a-web-app"></a><span data-ttu-id="64e37-103">Create a scheduled backup for a web app</span><span class="sxs-lookup"><span data-stu-id="64e37-103">Create a scheduled backup for a web app</span></span>

<span data-ttu-id="64e37-104">This sample script creates a web app in App Service with its related resources, and then creates a scheduled backup for it.</span><span class="sxs-lookup"><span data-stu-id="64e37-104">This sample script creates a web app in App Service with its related resources, and then creates a scheduled backup for it.</span></span> 

<span data-ttu-id="64e37-105">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Connect-AzureRmAccount` to create a connection with Azure.</span><span class="sxs-lookup"><span data-stu-id="64e37-105">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Connect-AzureRmAccount` to create a connection with Azure.</span></span> 

## <a name="sample-script"></a><span data-ttu-id="64e37-106">Sample script</span><span class="sxs-lookup"><span data-stu-id="64e37-106">Sample script</span></span>

[!code-azurepowershell-interactive[main](../../../powershell_scripts/app-service/backup-scheduled/backup-scheduled.ps1?highlight=1-4 "Create a scheduled backup for a web app")]

## <a name="clean-up-deployment"></a><span data-ttu-id="64e37-107">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="64e37-107">Clean up deployment</span></span> 

<span data-ttu-id="64e37-108">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="64e37-108">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="64e37-109">Script explanation</span><span class="sxs-lookup"><span data-stu-id="64e37-109">Script explanation</span></span>

<span data-ttu-id="64e37-110">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="64e37-110">This script uses the following commands.</span></span> <span data-ttu-id="64e37-111">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="64e37-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="64e37-112">Command</span><span class="sxs-lookup"><span data-stu-id="64e37-112">Command</span></span> | <span data-ttu-id="64e37-113">Notes</span><span class="sxs-lookup"><span data-stu-id="64e37-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="64e37-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="64e37-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="64e37-115">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="64e37-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="64e37-116">New-AzureRmStorageAccount</span><span class="sxs-lookup"><span data-stu-id="64e37-116">New-AzureRmStorageAccount</span></span>](/powershell/module/azurerm.storage/new-azurermstorageaccount) | <span data-ttu-id="64e37-117">Creates a Storage account.</span><span class="sxs-lookup"><span data-stu-id="64e37-117">Creates a Storage account.</span></span> |
| [<span data-ttu-id="64e37-118">New-AzureStorageContainer</span><span class="sxs-lookup"><span data-stu-id="64e37-118">New-AzureStorageContainer</span></span>](/powershell/module/azure.storage/new-azurestoragecontainer) | <span data-ttu-id="64e37-119">Creates an Azure storage container.</span><span class="sxs-lookup"><span data-stu-id="64e37-119">Creates an Azure storage container.</span></span> |
| [<span data-ttu-id="64e37-120">New-AzureStorageContainerSASToken</span><span class="sxs-lookup"><span data-stu-id="64e37-120">New-AzureStorageContainerSASToken</span></span>](/powershell/module/azure.storage/new-azurestoragecontainersastoken) | <span data-ttu-id="64e37-121">Generates an SAS token for an Azure storage container.</span><span class="sxs-lookup"><span data-stu-id="64e37-121">Generates an SAS token for an Azure storage container.</span></span> |
| [<span data-ttu-id="64e37-122">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="64e37-122">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="64e37-123">Creates an App Service plan.</span><span class="sxs-lookup"><span data-stu-id="64e37-123">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="64e37-124">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="64e37-124">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="64e37-125">Creates a web app.</span><span class="sxs-lookup"><span data-stu-id="64e37-125">Creates a web app.</span></span> |
| [<span data-ttu-id="64e37-126">Edit-AzureRmWebAppBackupConfiguration</span><span class="sxs-lookup"><span data-stu-id="64e37-126">Edit-AzureRmWebAppBackupConfiguration</span></span>](/powershell/module/azurerm.websites/edit-azurermwebappbackupconfiguration) | <span data-ttu-id="64e37-127">Edits the backup configuration for web app.</span><span class="sxs-lookup"><span data-stu-id="64e37-127">Edits the backup configuration for web app.</span></span> |
| [<span data-ttu-id="64e37-128">Get-AzureRmWebAppBackupList</span><span class="sxs-lookup"><span data-stu-id="64e37-128">Get-AzureRmWebAppBackupList</span></span>](/powershell/module/azurerm.websites/get-azurermwebappbackuplist) | <span data-ttu-id="64e37-129">Gets a list of backups for a web app.</span><span class="sxs-lookup"><span data-stu-id="64e37-129">Gets a list of backups for a web app.</span></span> |
| [<span data-ttu-id="64e37-130">Get-AzureRmWebAppBackupConfiguration</span><span class="sxs-lookup"><span data-stu-id="64e37-130">Get-AzureRmWebAppBackupConfiguration</span></span>](/powershell/module/azurerm.websites/get-azurermwebappbackupconfiguration) | <span data-ttu-id="64e37-131">Gets the backup configuration for web app.</span><span class="sxs-lookup"><span data-stu-id="64e37-131">Gets the backup configuration for web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="64e37-132">Next steps</span><span class="sxs-lookup"><span data-stu-id="64e37-132">Next steps</span></span>

<span data-ttu-id="64e37-133">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="64e37-133">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="64e37-134">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="64e37-134">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
