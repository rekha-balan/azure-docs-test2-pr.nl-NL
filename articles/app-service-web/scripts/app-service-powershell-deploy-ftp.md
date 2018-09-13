---
title: Azure PowerShell Script Sample - Upload files to a web app using FTP | Microsoft Docs
description: Azure PowerShell Script Sample - Upload files to a web app using FTP
services: app-service\web
documentationcenter: ''
author: cephalin
manager: erikre
editor: ''
tags: azure-service-management
ms.assetid: b7d46d6f-44fd-454c-8008-87dab6eefbc1
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: cephalin
ms.openlocfilehash: f4729e9daf788220358e7cca2508c820a1f2006a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551504"
---
# <a name="upload-files-to-a-web-app-using-ftp"></a><span data-ttu-id="e76da-103">Upload files to a web app using FTP</span><span class="sxs-lookup"><span data-stu-id="e76da-103">Upload files to a web app using FTP</span></span>

<span data-ttu-id="e76da-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code using FTP (via [WebClient.UploadFile()](https://msdn.microsoft.com/library/ms144229.aspx)).</span><span class="sxs-lookup"><span data-stu-id="e76da-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code using FTP (via [WebClient.UploadFile()](https://msdn.microsoft.com/library/ms144229.aspx)).</span></span>

<span data-ttu-id="e76da-105">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` to create a connection with Azure.</span><span class="sxs-lookup"><span data-stu-id="e76da-105">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="e76da-106">Sample script</span><span class="sxs-lookup"><span data-stu-id="e76da-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/deploy-ftp/deploy-ftp.ps1?highlight=1 "Upload files to a web app using FTP")]

## <a name="clean-up-deployment"></a><span data-ttu-id="e76da-107">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="e76da-107">Clean up deployment</span></span> 

<span data-ttu-id="e76da-108">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="e76da-108">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name $webappname -Force
```

## <a name="script-explanation"></a><span data-ttu-id="e76da-109">Script explanation</span><span class="sxs-lookup"><span data-stu-id="e76da-109">Script explanation</span></span>

<span data-ttu-id="e76da-110">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="e76da-110">This script uses the following commands.</span></span> <span data-ttu-id="e76da-111">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="e76da-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="e76da-112">Command</span><span class="sxs-lookup"><span data-stu-id="e76da-112">Command</span></span> | <span data-ttu-id="e76da-113">Notes</span><span class="sxs-lookup"><span data-stu-id="e76da-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e76da-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="e76da-114">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="e76da-115">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="e76da-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="e76da-116">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="e76da-116">New-AzureRmAppServicePlan</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.websites/v2.5.0/new-azurermappserviceplan) | <span data-ttu-id="e76da-117">Creates an App Service plan.</span><span class="sxs-lookup"><span data-stu-id="e76da-117">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="e76da-118">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="e76da-118">New-AzureRmWebApp</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.websites/v2.5.0/new-azurermwebapp) | <span data-ttu-id="e76da-119">Creates a web app.</span><span class="sxs-lookup"><span data-stu-id="e76da-119">Creates a web app.</span></span> |
| [<span data-ttu-id="e76da-120">Get-AzureRmWebAppPublishingProfile</span><span class="sxs-lookup"><span data-stu-id="e76da-120">Get-AzureRmWebAppPublishingProfile</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.websites/v2.5.0/get-azurermwebapppublishingprofile) | <span data-ttu-id="e76da-121">Get a web app's publishing profile.</span><span class="sxs-lookup"><span data-stu-id="e76da-121">Get a web app's publishing profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e76da-122">Next steps</span><span class="sxs-lookup"><span data-stu-id="e76da-122">Next steps</span></span>

<span data-ttu-id="e76da-123">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/).</span><span class="sxs-lookup"><span data-stu-id="e76da-123">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/).</span></span>

<span data-ttu-id="e76da-124">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="e76da-124">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
