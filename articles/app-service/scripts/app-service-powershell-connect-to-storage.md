---
title: Azure PowerShell Script Sample - Connect a web app to a storage account | Microsoft Docs
description: Azure PowerShell Script Sample - Connect a web app to a storage account
services: app-service\web
documentationcenter: ''
author: syntaxc4
manager: erikre
editor: ''
tags: azure-service-management
ms.assetid: e4831bdc-2068-4883-9474-0b34c2e3e255
ms.service: app-service
ms.devlang: multiple
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: e9255db4acc827d9a713e9d57e6defeec420dbfc
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871353"
---
# <a name="connect-a-web-app-to-a-storage-account"></a><span data-ttu-id="f404f-103">Connect a web app to a storage account</span><span class="sxs-lookup"><span data-stu-id="f404f-103">Connect a web app to a storage account</span></span>

<span data-ttu-id="f404f-104">In this scenario you will learn how to create an Azure storage account and an Azure web app.</span><span class="sxs-lookup"><span data-stu-id="f404f-104">In this scenario you will learn how to create an Azure storage account and an Azure web app.</span></span> <span data-ttu-id="f404f-105">Then you will link the storage account to the web app using app settings.</span><span class="sxs-lookup"><span data-stu-id="f404f-105">Then you will link the storage account to the web app using app settings.</span></span>

<span data-ttu-id="f404f-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Connect-AzureRmAccount` to create a connection with Azure.</span><span class="sxs-lookup"><span data-stu-id="f404f-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Connect-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="f404f-107">Sample script</span><span class="sxs-lookup"><span data-stu-id="f404f-107">Sample script</span></span>

[!code-azurepowershell-interactive[main](../../../powershell_scripts/app-service/connect-to-storage/connect-to-storage.ps1 "Connect a web app to a storage account")]

## <a name="clean-up-deployment"></a><span data-ttu-id="f404f-108">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="f404f-108">Clean up deployment</span></span> 

<span data-ttu-id="f404f-109">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="f404f-109">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="f404f-110">Script explanation</span><span class="sxs-lookup"><span data-stu-id="f404f-110">Script explanation</span></span>

<span data-ttu-id="f404f-111">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="f404f-111">This script uses the following commands.</span></span> <span data-ttu-id="f404f-112">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="f404f-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="f404f-113">Command</span><span class="sxs-lookup"><span data-stu-id="f404f-113">Command</span></span> | <span data-ttu-id="f404f-114">Notes</span><span class="sxs-lookup"><span data-stu-id="f404f-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f404f-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="f404f-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="f404f-116">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="f404f-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="f404f-117">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="f404f-117">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="f404f-118">Creates an App Service plan.</span><span class="sxs-lookup"><span data-stu-id="f404f-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="f404f-119">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="f404f-119">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="f404f-120">Creates a web app.</span><span class="sxs-lookup"><span data-stu-id="f404f-120">Creates a web app.</span></span> |
| [<span data-ttu-id="f404f-121">New-AzureRMStorageAccount</span><span class="sxs-lookup"><span data-stu-id="f404f-121">New-AzureRMStorageAccount</span></span>](/powershell/module/azurerm.storage/new-azurermstorageaccount) | <span data-ttu-id="f404f-122">Creates a Storage account.</span><span class="sxs-lookup"><span data-stu-id="f404f-122">Creates a Storage account.</span></span> |
| [<span data-ttu-id="f404f-123">Get-AzureRMStorageAccountKey</span><span class="sxs-lookup"><span data-stu-id="f404f-123">Get-AzureRMStorageAccountKey</span></span>](/powershell/module/azurerm.storage/get-azurermstorageaccountkey) | <span data-ttu-id="f404f-124">Gets the access keys for an Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="f404f-124">Gets the access keys for an Azure Storage account.</span></span> |
| [<span data-ttu-id="f404f-125">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="f404f-125">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="f404f-126">Modifies a web app's configuration.</span><span class="sxs-lookup"><span data-stu-id="f404f-126">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f404f-127">Next steps</span><span class="sxs-lookup"><span data-stu-id="f404f-127">Next steps</span></span>

<span data-ttu-id="f404f-128">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f404f-128">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="f404f-129">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="f404f-129">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
