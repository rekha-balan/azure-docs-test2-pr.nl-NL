---
title: Azure PowerShell Script Sample - Create a web app and deploy code from a local Git repository | Microsoft Docs
description: Azure PowerShell Script Sample - Create a web app and deploy code from a local Git repository
services: app-service\web
documentationcenter: ''
author: cephalin
manager: erikre
editor: ''
tags: azure-service-management
ms.assetid: 5a927f23-8e70-45fd-9aae-980d4e7a007d
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: cdd691d156d182c3d85dcc731ddf1bc62204b072
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865210"
---
# <a name="create-a-web-app-and-deploy-code-from-a-local-git-repository"></a><span data-ttu-id="984f8-103">Create a web app and deploy code from a local Git repository</span><span class="sxs-lookup"><span data-stu-id="984f8-103">Create a web app and deploy code from a local Git repository</span></span>

<span data-ttu-id="984f8-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code from a local Git repository.</span><span class="sxs-lookup"><span data-stu-id="984f8-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code from a local Git repository.</span></span>

<span data-ttu-id="984f8-105">If needed, update to the latest Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Connect-AzureRmAccount` to create a connection with Azure.</span><span class="sxs-lookup"><span data-stu-id="984f8-105">If needed, update to the latest Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Connect-AzureRmAccount` to create a connection with Azure.</span></span> <span data-ttu-id="984f8-106">Also, your application code needs to be committed into a local Git repository.</span><span class="sxs-lookup"><span data-stu-id="984f8-106">Also, your application code needs to be committed into a local Git repository.</span></span>

## <a name="sample-script"></a><span data-ttu-id="984f8-107">Sample script</span><span class="sxs-lookup"><span data-stu-id="984f8-107">Sample script</span></span>

[!code-azurepowershell-interactive[main](../../../powershell_scripts/app-service/deploy-local-git/deploy-local-git.ps1?highlight=1 "Create a web app and deploy code from a local Git repository")]

## <a name="clean-up-deployment"></a><span data-ttu-id="984f8-108">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="984f8-108">Clean up deployment</span></span> 

<span data-ttu-id="984f8-109">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="984f8-109">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name $webappname -Force
```

## <a name="script-explanation"></a><span data-ttu-id="984f8-110">Script explanation</span><span class="sxs-lookup"><span data-stu-id="984f8-110">Script explanation</span></span>

<span data-ttu-id="984f8-111">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="984f8-111">This script uses the following commands.</span></span> <span data-ttu-id="984f8-112">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="984f8-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="984f8-113">Command</span><span class="sxs-lookup"><span data-stu-id="984f8-113">Command</span></span> | <span data-ttu-id="984f8-114">Notes</span><span class="sxs-lookup"><span data-stu-id="984f8-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="984f8-115">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="984f8-115">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="984f8-116">Creates a web app with necessary resource group and App Service group.</span><span class="sxs-lookup"><span data-stu-id="984f8-116">Creates a web app with necessary resource group and App Service group.</span></span> <span data-ttu-id="984f8-117">When the current directory contains a Git repository, also add an `azure` remote.</span><span class="sxs-lookup"><span data-stu-id="984f8-117">When the current directory contains a Git repository, also add an `azure` remote.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="984f8-118">Next steps</span><span class="sxs-lookup"><span data-stu-id="984f8-118">Next steps</span></span>

<span data-ttu-id="984f8-119">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="984f8-119">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="984f8-120">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="984f8-120">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
