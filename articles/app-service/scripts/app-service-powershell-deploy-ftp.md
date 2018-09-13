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
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 5d9cf2cf491afdfeadf620cc32dc08ae29cfe448
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866469"
---
# <a name="upload-files-to-a-web-app-using-ftp"></a><span data-ttu-id="a6579-103">Upload files to a web app using FTP</span><span class="sxs-lookup"><span data-stu-id="a6579-103">Upload files to a web app using FTP</span></span>

<span data-ttu-id="a6579-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code using FTP (via [WebClient.UploadFile()](https://msdn.microsoft.com/library/ms144229.aspx)).</span><span class="sxs-lookup"><span data-stu-id="a6579-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code using FTP (via [WebClient.UploadFile()](https://msdn.microsoft.com/library/ms144229.aspx)).</span></span>

<span data-ttu-id="a6579-105">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Connect-AzureRmAccount` to create a connection with Azure.</span><span class="sxs-lookup"><span data-stu-id="a6579-105">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Connect-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="a6579-106">Sample script</span><span class="sxs-lookup"><span data-stu-id="a6579-106">Sample script</span></span>

[!code-azurepowershell-interactive[main](../../../powershell_scripts/app-service/deploy-ftp/deploy-ftp.ps1?highlight=1 "Upload files to a web app using FTP")]

## <a name="clean-up-deployment"></a><span data-ttu-id="a6579-107">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="a6579-107">Clean up deployment</span></span> 

<span data-ttu-id="a6579-108">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="a6579-108">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name $webappname -Force
```

## <a name="script-explanation"></a><span data-ttu-id="a6579-109">Script explanation</span><span class="sxs-lookup"><span data-stu-id="a6579-109">Script explanation</span></span>

<span data-ttu-id="a6579-110">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="a6579-110">This script uses the following commands.</span></span> <span data-ttu-id="a6579-111">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="a6579-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="a6579-112">Command</span><span class="sxs-lookup"><span data-stu-id="a6579-112">Command</span></span> | <span data-ttu-id="a6579-113">Notes</span><span class="sxs-lookup"><span data-stu-id="a6579-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a6579-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="a6579-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="a6579-115">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="a6579-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="a6579-116">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="a6579-116">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="a6579-117">Creates an App Service plan.</span><span class="sxs-lookup"><span data-stu-id="a6579-117">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="a6579-118">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="a6579-118">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="a6579-119">Creates a web app.</span><span class="sxs-lookup"><span data-stu-id="a6579-119">Creates a web app.</span></span> |
| [<span data-ttu-id="a6579-120">Get-AzureRmWebAppPublishingProfile</span><span class="sxs-lookup"><span data-stu-id="a6579-120">Get-AzureRmWebAppPublishingProfile</span></span>](/powershell/module/azurerm.websites/get-azurermwebapppublishingprofile) | <span data-ttu-id="a6579-121">Get a web app's publishing profile.</span><span class="sxs-lookup"><span data-stu-id="a6579-121">Get a web app's publishing profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a6579-122">Next steps</span><span class="sxs-lookup"><span data-stu-id="a6579-122">Next steps</span></span>

<span data-ttu-id="a6579-123">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a6579-123">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="a6579-124">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="a6579-124">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
