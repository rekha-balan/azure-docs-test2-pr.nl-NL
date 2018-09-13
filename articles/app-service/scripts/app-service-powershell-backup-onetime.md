---
title: Azure PowerShell Script Sample - Back up a web app | Microsoft Docs
description: Azure PowerShell Script Sample - Back up a web app
services: app-service\web
documentationcenter: ''
author: cephalin
manager: cfowler
editor: ''
tags: azure-service-management
ms.assetid: fc755f82-ca3e-4532-b251-690b699324d6
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 10/30/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 1b10de7b102ea2e8e55d48fa9753dbe115e2016b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857770"
---
# <a name="back-up-a-web-app"></a><span data-ttu-id="7456f-103">Back up a web app</span><span class="sxs-lookup"><span data-stu-id="7456f-103">Back up a web app</span></span>

<span data-ttu-id="7456f-104">This sample script creates a web app in App Service with its related resources, and then creates a one-time backup for it.</span><span class="sxs-lookup"><span data-stu-id="7456f-104">This sample script creates a web app in App Service with its related resources, and then creates a one-time backup for it.</span></span> 

<span data-ttu-id="7456f-105">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Connect-AzureRmAccount` to create a connection with Azure.</span><span class="sxs-lookup"><span data-stu-id="7456f-105">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Connect-AzureRmAccount` to create a connection with Azure.</span></span> 

## <a name="sample-script"></a><span data-ttu-id="7456f-106">Sample script</span><span class="sxs-lookup"><span data-stu-id="7456f-106">Sample script</span></span>

[!code-azurepowershell-interactive[main](../../../powershell_scripts/app-service/backup-onetime/backup-onetime.ps1?highlight=1-5 "Back up a web app")]

## <a name="clean-up-deployment"></a><span data-ttu-id="7456f-107">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="7456f-107">Clean up deployment</span></span> 

<span data-ttu-id="7456f-108">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="7456f-108">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="7456f-109">Script explanation</span><span class="sxs-lookup"><span data-stu-id="7456f-109">Script explanation</span></span>

<span data-ttu-id="7456f-110">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="7456f-110">This script uses the following commands.</span></span> <span data-ttu-id="7456f-111">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="7456f-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="7456f-112">Command</span><span class="sxs-lookup"><span data-stu-id="7456f-112">Command</span></span> | <span data-ttu-id="7456f-113">Notes</span><span class="sxs-lookup"><span data-stu-id="7456f-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="7456f-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="7456f-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="7456f-115">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="7456f-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="7456f-116">New-AzureRmStorageAccount</span><span class="sxs-lookup"><span data-stu-id="7456f-116">New-AzureRmStorageAccount</span></span>](/powershell/module/azurerm.storage/new-azurermstorageaccount) | <span data-ttu-id="7456f-117">Creates a Storage account.</span><span class="sxs-lookup"><span data-stu-id="7456f-117">Creates a Storage account.</span></span> |
| [<span data-ttu-id="7456f-118">New-AzureStorageContainer</span><span class="sxs-lookup"><span data-stu-id="7456f-118">New-AzureStorageContainer</span></span>](/powershell/module/azure.storage/new-azurestoragecontainer) | <span data-ttu-id="7456f-119">Creates an Azure storage container.</span><span class="sxs-lookup"><span data-stu-id="7456f-119">Creates an Azure storage container.</span></span> |
| [<span data-ttu-id="7456f-120">New-AzureStorageContainerSASToken</span><span class="sxs-lookup"><span data-stu-id="7456f-120">New-AzureStorageContainerSASToken</span></span>](/powershell/module/azure.storage/new-azurestoragecontainersastoken) | <span data-ttu-id="7456f-121">Generates an SAS token for an Azure storage container.</span><span class="sxs-lookup"><span data-stu-id="7456f-121">Generates an SAS token for an Azure storage container.</span></span>  |
| [<span data-ttu-id="7456f-122">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="7456f-122">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="7456f-123">Creates an App Service plan.</span><span class="sxs-lookup"><span data-stu-id="7456f-123">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="7456f-124">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="7456f-124">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="7456f-125">Creates a web app.</span><span class="sxs-lookup"><span data-stu-id="7456f-125">Creates a web app.</span></span> |
| [<span data-ttu-id="7456f-126">New-AzureRmWebAppBackup</span><span class="sxs-lookup"><span data-stu-id="7456f-126">New-AzureRmWebAppBackup</span></span>](/powershell/module/azurerm.websites/new-azurermwebappbackup) | <span data-ttu-id="7456f-127">Creates a backup for a web app.</span><span class="sxs-lookup"><span data-stu-id="7456f-127">Creates a backup for a web app.</span></span> |
| [<span data-ttu-id="7456f-128">Get-AzureRmWebAppBackupList</span><span class="sxs-lookup"><span data-stu-id="7456f-128">Get-AzureRmWebAppBackupList</span></span>](/powershell/module/azurerm.websites/get-azurermwebappbackuplist) | <span data-ttu-id="7456f-129">Gets a list of backups for a web app.</span><span class="sxs-lookup"><span data-stu-id="7456f-129">Gets a list of backups for a web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="7456f-130">Next steps</span><span class="sxs-lookup"><span data-stu-id="7456f-130">Next steps</span></span>

<span data-ttu-id="7456f-131">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7456f-131">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="7456f-132">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="7456f-132">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
