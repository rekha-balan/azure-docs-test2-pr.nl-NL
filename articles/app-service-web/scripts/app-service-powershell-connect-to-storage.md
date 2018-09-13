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
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.openlocfilehash: 05b0463704abcb33f9a967beb276c5a9422b4908
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564446"
---
# <a name="connect-a-web-app-to-a-storage-account"></a><span data-ttu-id="68744-103">Connect a web app to a storage account</span><span class="sxs-lookup"><span data-stu-id="68744-103">Connect a web app to a storage account</span></span>

<span data-ttu-id="68744-104">In this scenario you will learn how to create an Azure storage account and an Azure web app.</span><span class="sxs-lookup"><span data-stu-id="68744-104">In this scenario you will learn how to create an Azure storage account and an Azure web app.</span></span> <span data-ttu-id="68744-105">Then you will link the storage account to the web app using app settings.</span><span class="sxs-lookup"><span data-stu-id="68744-105">Then you will link the storage account to the web app using app settings.</span></span>

<span data-ttu-id="68744-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` to create a connection with Azure.</span><span class="sxs-lookup"><span data-stu-id="68744-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="68744-107">Sample script</span><span class="sxs-lookup"><span data-stu-id="68744-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/connect-to-storage/connect-to-storage.ps1 "Connect a web app to a storage account")]

## <a name="clean-up-deployment"></a><span data-ttu-id="68744-108">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="68744-108">Clean up deployment</span></span> 

<span data-ttu-id="68744-109">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="68744-109">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="68744-110">Script explanation</span><span class="sxs-lookup"><span data-stu-id="68744-110">Script explanation</span></span>

<span data-ttu-id="68744-111">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="68744-111">This script uses the following commands.</span></span> <span data-ttu-id="68744-112">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="68744-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="68744-113">Command</span><span class="sxs-lookup"><span data-stu-id="68744-113">Command</span></span> | <span data-ttu-id="68744-114">Notes</span><span class="sxs-lookup"><span data-stu-id="68744-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="68744-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="68744-115">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="68744-116">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="68744-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="68744-117">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="68744-117">New-AzureRmAppServicePlan</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.websites/v2.5.0/new-azurermappserviceplan) | <span data-ttu-id="68744-118">Creates an App Service plan.</span><span class="sxs-lookup"><span data-stu-id="68744-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="68744-119">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="68744-119">New-AzureRmWebApp</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.websites/v2.5.0/new-azurermwebapp) | <span data-ttu-id="68744-120">Creates a web app.</span><span class="sxs-lookup"><span data-stu-id="68744-120">Creates a web app.</span></span> |
| [<span data-ttu-id="68744-121">New-AzureRMStorageAccount</span><span class="sxs-lookup"><span data-stu-id="68744-121">New-AzureRMStorageAccount</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.storage/v2.5.0/New-AzureRmStorageAccount) | <span data-ttu-id="68744-122">Creates a Storage account.</span><span class="sxs-lookup"><span data-stu-id="68744-122">Creates a Storage account.</span></span> |
| [<span data-ttu-id="68744-123">Get-AzureRMStorageAccountKey</span><span class="sxs-lookup"><span data-stu-id="68744-123">Get-AzureRMStorageAccountKey</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.storage/v2.5.0/get-azurermstorageaccountkey) | <span data-ttu-id="68744-124">Gets the access keys for an Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="68744-124">Gets the access keys for an Azure Storage account.</span></span> |
| [<span data-ttu-id="68744-125">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="68744-125">Set-AzureRmWebApp</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.websites/v2.5.0/set-azurermwebapp) | <span data-ttu-id="68744-126">Modifies a web app's configuration.</span><span class="sxs-lookup"><span data-stu-id="68744-126">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="68744-127">Next steps</span><span class="sxs-lookup"><span data-stu-id="68744-127">Next steps</span></span>

<span data-ttu-id="68744-128">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/).</span><span class="sxs-lookup"><span data-stu-id="68744-128">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/).</span></span>

<span data-ttu-id="68744-129">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="68744-129">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
