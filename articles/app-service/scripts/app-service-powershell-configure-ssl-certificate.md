---
title: Azure PowerShell Script Sample - Bind a custom SSL certificate to a web app | Microsoft Docs
description: Azure PowerShell Script Sample - Bind a custom SSL certificate to a web app
services: app-service\web
documentationcenter: ''
author: cephalin
manager: erikre
editor: ''
tags: azure-service-management
ms.assetid: 23e83b74-614a-49a0-bc08-7542120eeec5
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 4ab6ad5e8a022c577e9382cde7bdcb3059a18a14
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870030"
---
# <a name="bind-a-custom-ssl-certificate-to-a-web-app"></a><span data-ttu-id="6ec09-103">Bind a custom SSL certificate to a web app</span><span class="sxs-lookup"><span data-stu-id="6ec09-103">Bind a custom SSL certificate to a web app</span></span>

<span data-ttu-id="6ec09-104">This sample script creates a web app in App Service with its related resources, then binds the SSL certificate of a custom domain name to it.</span><span class="sxs-lookup"><span data-stu-id="6ec09-104">This sample script creates a web app in App Service with its related resources, then binds the SSL certificate of a custom domain name to it.</span></span> 

<span data-ttu-id="6ec09-105">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Connect-AzureRmAccount` to create a connection with Azure.</span><span class="sxs-lookup"><span data-stu-id="6ec09-105">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Connect-AzureRmAccount` to create a connection with Azure.</span></span> <span data-ttu-id="6ec09-106">Also, ensure that:</span><span class="sxs-lookup"><span data-stu-id="6ec09-106">Also, ensure that:</span></span>

- <span data-ttu-id="6ec09-107">A connection with Azure has been created using the `az login` command.</span><span class="sxs-lookup"><span data-stu-id="6ec09-107">A connection with Azure has been created using the `az login` command.</span></span>
- <span data-ttu-id="6ec09-108">You have access to your domain registrar's DNS configuration page.</span><span class="sxs-lookup"><span data-stu-id="6ec09-108">You have access to your domain registrar's DNS configuration page.</span></span>
- <span data-ttu-id="6ec09-109">You have a valid .PFX file and its password for the SSL certificate you want to upload and bind.</span><span class="sxs-lookup"><span data-stu-id="6ec09-109">You have a valid .PFX file and its password for the SSL certificate you want to upload and bind.</span></span>

## <a name="sample-script"></a><span data-ttu-id="6ec09-110">Sample script</span><span class="sxs-lookup"><span data-stu-id="6ec09-110">Sample script</span></span>

[!code-azurepowershell-interactive[main](../../../powershell_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.ps1?highlight=1-3 "Bind a custom SSL certificate to a web app")]

## <a name="clean-up-deployment"></a><span data-ttu-id="6ec09-111">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="6ec09-111">Clean up deployment</span></span> 

<span data-ttu-id="6ec09-112">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="6ec09-112">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="6ec09-113">Script explanation</span><span class="sxs-lookup"><span data-stu-id="6ec09-113">Script explanation</span></span>

<span data-ttu-id="6ec09-114">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="6ec09-114">This script uses the following commands.</span></span> <span data-ttu-id="6ec09-115">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="6ec09-115">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="6ec09-116">Command</span><span class="sxs-lookup"><span data-stu-id="6ec09-116">Command</span></span> | <span data-ttu-id="6ec09-117">Notes</span><span class="sxs-lookup"><span data-stu-id="6ec09-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="6ec09-118">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="6ec09-118">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="6ec09-119">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="6ec09-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="6ec09-120">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="6ec09-120">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="6ec09-121">Creates an App Service plan.</span><span class="sxs-lookup"><span data-stu-id="6ec09-121">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="6ec09-122">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="6ec09-122">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="6ec09-123">Creates a web app.</span><span class="sxs-lookup"><span data-stu-id="6ec09-123">Creates a web app.</span></span> |
| [<span data-ttu-id="6ec09-124">Set-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="6ec09-124">Set-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/set-azurermappserviceplan) | <span data-ttu-id="6ec09-125">Modifies an App Service plan to change its pricing tier.</span><span class="sxs-lookup"><span data-stu-id="6ec09-125">Modifies an App Service plan to change its pricing tier.</span></span> |
| [<span data-ttu-id="6ec09-126">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="6ec09-126">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="6ec09-127">Modifies a web app's configuration.</span><span class="sxs-lookup"><span data-stu-id="6ec09-127">Modifies a web app's configuration.</span></span> |
| [<span data-ttu-id="6ec09-128">New-AzureRmWebAppSSLBinding</span><span class="sxs-lookup"><span data-stu-id="6ec09-128">New-AzureRmWebAppSSLBinding</span></span>](/powershell/module/azurerm.websites/new-azurermwebappsslbinding) | <span data-ttu-id="6ec09-129">Creates an SSL certificate binding for a web app.</span><span class="sxs-lookup"><span data-stu-id="6ec09-129">Creates an SSL certificate binding for a web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6ec09-130">Next steps</span><span class="sxs-lookup"><span data-stu-id="6ec09-130">Next steps</span></span>

<span data-ttu-id="6ec09-131">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6ec09-131">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="6ec09-132">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="6ec09-132">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
